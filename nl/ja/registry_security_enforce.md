---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

keywords: IBM Cloud Container Registry, Vulnerability Advisor policies, container image security, policy requirements, policies, Container Image Security Enforcement, policies, content trust, Kube-system policies, IBM-system policies, CISE, removing policies,

subcollection: registry

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# コンテナー・イメージ・セキュリティーの適用
{: #security_enforce}

Container Image Security Enforcement を使用すると、{{site.data.keyword.containerlong}} のクラスターにコンテナー・イメージをデプロイする前に、コンテナー・イメージを検査できます。 イメージのデプロイ元を制御し、脆弱性アドバイザーのポリシーを適用して、[コンテント・トラスト](/docs/services/Registry?topic=registry-registry_trustedcontent)をイメージに適切に適用することができます。 イメージがポリシーの要件を満たさない場合、ポッドはクラスターにデプロイされることも更新されることもありません。
{:shortdesc}

Container Image Security Enforcement は、イメージ・コンテンツの信頼性と脆弱性に関する情報を {{site.data.keyword.registrylong}} から取得します。 他のレジストリーに保管されているイメージについては、そのデプロイメントをブロックするか許可するかを選択することはできますが、それらのイメージに対して脆弱性や信頼性の制約を使用することはできません。

## クラスターへの Container Image Security Enforcement のインストール
{: #sec_enforce_install}

**始めに**

* **Kubernetes バージョン 1.9 以降**で使用するクラスターを [作成](/docs/containers?topic=containers-clusters#clusters_ui)または[更新](/docs/containers?topic=containers-update#update)します。
* クラスターを [`kubectl` CLI のターゲットとして設定します](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)。

以下の手順を実行してください。

1. [クラスターに Helm をセットアップします](/docs/containers?topic=containers-helm#helm)。

2. IBM のチャート・リポジトリーを Helm クライアントに追加します。

   ```
   helm repo add iks-charts https://icr.io/helm/iks-charts
   ```
   {: pre}

3. Container Image Security Enforcement の Helm チャートをクラスターにインストールします。 `cise` などの名前を指定します。

   ```
   helm install --name cise iks-charts/ibmcloud-image-enforcement
   ```
   {: pre}

これで、Container Image Security Enforcement がインストールされ、クラスター内のすべての Kubernetes 名前空間に[デフォルトのセキュリティー・ポリシー](#default_policies)が適用されました。 クラスター内の Kubernetes 名前空間またはクラスター全体のセキュリティー・ポリシーをカスタマイズする方法については、[ポリシーのカスタマイズ](#customize_policies)を参照してください。

## デフォルトのポリシー
{: #default_policies}

Container Image Security Enforcement は、セキュリティー・ポリシーを作成するための開始点として使用できるように、いくつかのポリシーをデフォルトでインストールします。
{:shortdesc}

これらのポリシーをオーバーライドする方法としては、以下の選択肢があります。

* 新しいポリシー文書を作成し、`kubectl apply` を使用してクラスターに適用する。
* `kubectl edit` を使用してデフォルトのポリシーを編集する。

セキュリティー・ポリシーの作成方法について詳しくは、[ポリシーのカスタマイズ](#customize_policies)を参照してください。

### クラスター規模のポリシー
{: #cluster-wide}

デフォルトでは、クラスター規模のポリシーにより、すべてのレジストリー内のすべてのイメージに、トラスト情報を保持していること、および脆弱性アドバイザーで脆弱性が報告されていないことが求められます。
{:shortdesc}

**クラスター規模のデフォルトのポリシー `.yaml` ファイル**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ClusterImagePolicy
metadata:
  name: ibmcloud-default-cluster-image-policy
spec:
   repositories:
    # This enforces that all images deployed to this cluster pass trust and VA
    # To override, set an ImagePolicy for a specific Kubernetes namespace or modify this policy
    - name: "*"
      policy:
        trust:
          enabled: true
        va:
          enabled: true
```
{: codeblock}

{{site.data.keyword.registrylong_notm}} 以外のコンテナー・レジストリーに対して `va` または `trust` を `enabled: true` に設定した場合、そのレジストリー内のイメージからポッドをデプロイしようとすると拒否されます。 他のレジストリーからイメージをデプロイする場合は、`va` ポリシーと `trust` ポリシーを削除してください。
{:tip}

### kube-system ポリシー
{: #kube-system}

デフォルトでは、`kube-system` 名前空間に対して名前空間規模のポリシーがインストールされます。 このポリシーは、制約なしですべてのコンテナー・レジストリーのすべてのイメージを `kube-system` にデプロイすることを許可します。ただし、ポリシーのこの部分は変更可能です。 デフォルト・ポリシーに含まれるいくつかのリポジトリーは、クラスターが正しく構成されるようにするためにそのまま残しておく必要があります。
{:shortdesc}

**デフォルトの `kube-system` ポリシーの `.yaml` ファイル**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: kube-system
spec:
   repositories:
    # This policy allows all images to be deployed into this namespace. This policy prevents breaking any existing third party applications in this namespace.
    # IMPORTANT: Review this policy and replace it with one that meets your requirements. If you do not run any third party applications in this namespace, you can remove this policy entirely.
    - name: "*"
      policy:
    # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```
{: codeblock}

### ibm-system ポリシー
{: #ibm-system}

デフォルトでは、`ibm-system` 名前空間に対して名前空間規模のポリシーがインストールされます。 このポリシーは、制約なしですべてのコンテナー・レジストリーのすべてのイメージを `ibm-system` にデプロイすることを許可します。ただし、ポリシーのこの部分は変更可能です。 デフォルト・ポリシーの中には、クラスターを正しく構成し、Container Image Security Enforcement をインストールまたはアップグレードできるようにするためにそのまま残しておく必要のあるリポジトリーもいくつか含まれています。
{:shortdesc}

**デフォルトの `ibm-system` ポリシー `.yaml` ファイル**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: ibm-system
spec:
   repositories:
    # This policy allows all images to be deployed into this namespace. This policy prevents breaking any existing third party applications in this namespace.
    # IMPORTANT: Review this policy and replace it with one that meets your requirements. If you do not run any third party applications in this namespace, you can remove this policy entirely.
    - name: "*"
      policy:
    # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
    # This policy prevents Container Image Security Enforcement from blocking itself.
    - name: "registry*.bluemix.net/ibm/ibmcloud-image-enforcement"
      policy:
    # This policy allows Container Image Security Enforcement to use Hyperkube to configure your cluster. This policy must exist if you uninstall Container Image Security Enforcement.
    - name: quay.io/coreos/hyperkube
      policies:
```
{: codeblock}


## ポリシーのカスタマイズ
{: #customize_policies}

イメージを許可するために Container Image Security Enforcement で使用されるポリシーは、ユーザーがクラスター・レベルまたは Kubernetes 名前空間レベルで変更できます。 ポリシーには、さまざまなイメージに対するさまざまな制約ルールを指定できます。
{:shortdesc}

何らかのポリシーを設定する必要があります。 そうしないと、クラスターへのデプロイメントは失敗します。 イメージのセキュリティー・ポリシーを一切適用しない場合は、[Container Image Security Enforcement を削除](#remove)してください。
{:tip}

デプロイメントを行うと、Container Image Security Enforcement が、デプロイ先の Kubernetes 名前空間に適用すべきポリシーがあるかどうかを検査します。 ない場合、Container Image Security Enforcement はクラスター規模のポリシーを使用します。 名前空間規模のポリシーもクラスター規模のポリシーも存在しない場合、デプロイメントは拒否されます。

始める前に、クラスターを [`kubectl` CLI のターゲットとして設定](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)してください。 次に、以下の手順を実行します。

1. [Kubernetes カスタム・リソース定義 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/) `.yaml` ファイルを作成します。

    ```yaml
    apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
    kind: <ClusterImagePolicy_or_ImagePolicy>
    metadata:
      name: <crd_name>
    spec:
       repositories:
        - name: <repository_name>
          policy:
            trust:
              enabled: <true_or_false>
              signerSecrets:
              - name: <secret_name>
            va:
              enabled: <true_or_false>
    ```
    {: codeblock}

    <table>
    <caption>表 1. YAML コンポーネントについて</caption>
    <thead>
    <th>フィールド</th>
    <th>説明</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>クラスター規模のポリシーでは、`kind` に `ClusterImagePolicy` を指定します。 Kubernetes 名前空間ポリシーの場合は、`ImagePolicy` を指定します。</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>このカスタム・リソース定義に名前を付けます。</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>イメージを許可するリポジトリーを指定します。 リポジトリー名にはワイルドカード (`*`) を使用できます。 許可するリポジトリーまたは追加検証を適用するリポジトリーを表す `repositories` の項目と一致しない場合、リポジトリーは拒否されます。 `repositories` リストが空の場合、すべてのイメージのデプロイメントがブロックされます。 どのポリシーも検証せずにイメージをすべて許可するには、name を `*` に設定し、policy サブセクションを省略します。</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>`trust` 制約と `va` 制約のサブセクションを入力します。 policy サブセクションを省略すると、どちらにも `enabled: false` を指定したことになります。</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>[コンテント・トラストの署名](/docs/services/Registry?topic=registry-registry_trustedcontent)があるイメージのデプロイだけを許可する場合は、`true` に設定します。 イメージに署名があるかどうかを無視する場合は、`false` に設定します。</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>特定のユーザーの署名があるイメージだけを許可する場合は、署名者の名前の Kubernetes シークレットを指定します。 特定の署名者に限定せずに、イメージに署名があることを確認する場合は、このセクションを省略するか空のままにしてください。 詳しくは、[信頼できるコンテンツの署名者をカスタム・ポリシーで指定する](#signers)を参照してください。</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>[脆弱性アドバイザー](/docs/services/va?topic=va-va_index)のスキャンに合格したイメージだけを許可する場合は、`true` に設定します。 脆弱性アドバイザーのスキャンを無視する場合は、`false` に設定します。</td>
    </tr>
    </tbody>
    </table>

2. `.yaml` ファイルをクラスターに適用します。

   ```
   kubectl apply -f <filepath>
   ```
   {: pre}

### 信頼できるコンテンツの署名者をカスタム・ポリシーに指定する
{: #signers}

コンテント・トラストを使用する場合は、イメージに特定の署名者の署名があることを検証できます。 署名付きの最新のバージョンに、リストしたすべての署名者の署名がある場合に限り、デプロイメントは許可されます。 署名者をリポジトリーに追加するには、[信頼できる署名者の管理](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_signers)を参照してください。
{:shortdesc}

イメージに特定の署名者の署名があることを検証するようにポリシーを構成するには、以下のようにします。

1. 署名者の名前 (`docker trust signer add` で使用された名前) と公開鍵を取得します。
2. 署名者の名前と公開鍵を使用して、Kubernetes シークレットを生成します。

   ```
   kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
   ```
   {: pre}

3. ポリシーのリポジトリーの `signerSecrets` リストにシークレットを追加します。

   ```yaml
   - name: example
     policy:
       trust:
         enabled: true
         signerSecrets:
         - name: <secret_name>
   ```
   {: codeblock}

## ポリシーをカスタマイズできるユーザーの制御
{: #assign_user_policy}

Kubernetes クラスターで役割ベースのアクセス制御 (RBAC) を有効にしている場合は、役割を作成して、クラスターのセキュリティー・ポリシーを管理できるユーザーを制御できます。 クラスターに RBAC ルールを適用する方法について詳しくは、[{{site.data.keyword.containerlong_notm}} の資料](/docs/containers?topic=containers-users#rbac)を参照してください。
{:shortdesc}

役割にセキュリティー・ポリシーのルールを追加します。

```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```
{: codeblock}

複数の役割を作成して、ユーザーが実行できるアクションを制御できます。 例えば、`verbs` を変更して、一部のユーザーが `get` または `list` ポリシーだけを使用できるようにしたりします。 また、`resources` リストから `clusterimagepolicies` を省いて、Kubernetes 名前空間ポリシーへのアクセスだけを付与することもできます。
{:tip}

カスタム・リソース定義 (CRD) を削除する権限を持つユーザーは、セキュリティー・ポリシーのリソース定義を削除できます。これにより、セキュリティー・ポリシーも削除されます。 CRD を削除できるユーザーの制御は、必ず行ってください。 CRD を削除する権限を付与するには、以下のようにルールを追加します。

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```
{: codeblock}

`cluster-admin` 役割を持つユーザーおよびサービス・アカウントは、すべてのリソースにアクセスできます。 cluster-admin 役割は、編集を行わなくても、セキュリティー・ポリシーを管理する権限を付与します。 `cluster-admin` 役割を持つユーザーの制御を必ず行い、セキュリティー・ポリシーの変更を許可するユーザーだけにアクセス権限を付与するようにしてください。
{:tip}

## セキュリティーを強化したコンテナー・イメージのデプロイ
{: #deploy_containers}

ポリシーを適用した後は、通常どおりにコンテンツをクラスターにデプロイできます。 ポリシーは、Kubernetes クラスターによって自動的に適用されます。 デプロイメントがポリシーに一致し、そのポリシーで許可されると、そのデプロイメントはクラスターに承認され、適用されます。
{:shortdesc}

Container Image Security Enforcement がデプロイメントを拒否した場合、デプロイメントは作成されますが、そのデプロイメントによって作成された ReplicaSet はスケールアップできず、ポッドは作成されません。 `kubectl describe deployment <deployment-name>` を実行することで ReplicaSet を見つけられます。また `kubectl describe rs<replicaset-name>` を実行することでデプロイメントが拒否された理由を確認できます。

**エラー・メッセージの例**

* イメージがどのポリシーにも一致しない場合、または名前空間にもクラスターにもポリシーがない場合。

   ```
   admission webhook 
   "trust.hooks.securityenforcement.admission.cloud.ibm.com" 
   denied the request: Deny, no image policies or cluster 
   polices for <image-name>
   ```
   {: screen}

* イメージがポリシーに一致するが、そのポリシーの脆弱性アドバイザーの要件を満たしていない場合。

   ```
   admission webhook 
   "va.hooks.securityenforcement.admission.cloud.ibm.com" 
   denied the request: The Vulnerability Advisor image scan 
   assessment found issues with the container image that 
   are not exempted. Refer to your image vulnerability report 
   for more details by using the command `ibmcloud cr va`.
   ```
   {: screen}

* イメージがポリシーに一致するが、そのポリシーのトラスト要件を満たしていない場合。

   ```
   admission webhook 
   "trust.hooks.securityenforcement.admission.cloud.ibm.com" 
   denied the request: Deny, failed to get content trust information: 
   No valid trust data for latest
   ```
   {: screen}

* イメージに対するトラスト制約がポリシーに指定されているが、イメージがサポート対象レジストリーからのものではない場合。

   ```
   admission webhook 
   "trust.hooks.securityenforcement.admission.cloud.ibm.com" 
   denied the request: Trust is not supported for images 
   from this registry
   ```
   {: screen}

ポリシーで `va` オプションを有効にすると、脆弱性アドバイザーに合格したイメージだけがデプロイできるようになります。 脆弱性アドバイザーでサポートされないイメージは許可されます。

ポリシーで `trust` オプションを有効にすると、コンテント・トラストを適用できます。 `signerSecrets` を指定しない場合、だれの署名であろうと署名があるイメージは、デプロイメントを許可されます。 `signerSecrets` を指定する場合は、署名付きの最新バージョンのイメージに、指定したすべての署名者の署名がなければなりません。 Container Image Security Enforcement は、提供された公開鍵が署名者のものかどうかを検証します。 コンテント・トラストについて詳しくは、[信頼できるコンテンツのイメージへの署名](/docs/services/Registry?topic=registry-registry_trustedcontent)を参照してください。

すべてのイメージが Container Image Security Enforcement の検査に合格した場合に限り、デプロイメントは許可されます。

## Container Image Security Enforcement の削除
{: #remove}

始める前に、クラスターを [`kubectl` CLI のターゲットとして設定](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)してください。



1. Container Image Security Enforcement を無効にします。

   ```
   $ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config
   ```
   {: codeblock}

2. チャートを削除します。

   ```
   helm delete --purge cise
   ```
   {: pre}
