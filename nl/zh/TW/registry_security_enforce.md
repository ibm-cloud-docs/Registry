---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 強制執行容器映像檔安全（測試版）
{: #security_enforce}

使用 IBM Container Image Security Enforcement（測試版），您可以先驗證容器映像檔，然後再將它們部署到 {{site.data.keyword.containerlong}} 中的叢集。您可以控制從何處部署映像檔、強制執行「漏洞警告器」原則，以及確定[內容信任](registry_trusted_content.html)已適當地套用至映像檔。如果 Pod 不符合您的原則需求，則不會修改您的叢集。
{:shortdesc}

IBM Container Image Security Enforcement 會從 {{site.data.keyword.registrylong}} 取得映像檔內容信任及漏洞的相關資訊。您可以選擇是要在您的原則裡封鎖還是容許來自其他登錄的映像檔，但您無法針對這些映像檔使用漏洞或信任強制執行。


## 在叢集中安裝 Container Image Security Enforcement
{: #sec_enforce_install}

開始之前：
* 使用 **Kubernetes 1.9 版或更新版本**來[建立](../../containers/cs_clusters.html#clusters_ui)或[更新](../../containers/cs_cluster_update.html)您要使用的叢集。
* [將 `kubectl` CLI 的目標](../../containers/cs_cli_install.html#cs_cli_configure)設為叢集。

步驟：
1.  [在叢集中設定 Helm](../../containers/cs_integrations.html#helm)。

1.  將 IBM 圖表儲存庫新增至 Helm。

    ```
    helm repo add ibm-incubator https://registry.bluemix.net/helm/ibm-incubator
    ```
    {: pre}

1.  將 IBM Container Image Security Enforcement Helm 圖表安裝至您的 `ibm-system` 叢集名稱空間。將它命名為例如 `<cise>`。

    ```
    helm install --name=<cise> --namespace=ibm-system ibm-incubator/ibmcloud-image-enforcement
    ```
    {: pre}

IBM Container Image Security Enforcement 現在已安裝，並針對叢集中的所有 Kubernetes 名稱空間套用[預設安全原則](#default_policies)。如需為叢集中的 Kubernetes 名稱空間或叢集整體自訂安全原則的相關資訊，請參閱[自訂原則](#customize_policies)。

## 預設原則
{: #default_policies}

IBM Container Image Security Enforcement 依預設會安裝部分原則，為您提供建置安全原則的起點。
{:shortdesc}

若要置換這些原則，請使用下列其中一個選項：
* 撰寫新的原則文件，並使用 `kubectl apply` 將它套用至您的叢集
* 使用 `kubectl edit` 編輯預設原則

如需撰寫安全原則的相關資訊，請參閱[自訂原則](#customize_policies)。

### 叢集層面原則
{: #cluster-wide}

依預設，叢集層面的原則會強制所有登錄中的所有映像檔都具有信任資訊，且在「漏洞警告器」中沒有已報告的漏洞。
{:shortdesc}

**預設的叢集層面原則 `.yaml` 檔案**：

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

當您為非 {{site.data.keyword.registrylong_notm}} 的容器登錄將 `va` 或 `trust` 設為 `enabled: true`時，任何要從該登錄的映像檔部署 Pod 的嘗試都會遭到拒絕。如果您要從其他登錄部署映像檔，請移除 `va` 和 `trust` 原則。
{:tip}

### Kube-system 原則
{: #kube-system}

依預設，會為 `kube-system` 名稱空間安裝名稱空間層面的原則。此原則容許將任何容器登錄的所有映像檔部署到 `kube-system` 而不強制執行。它也容許用來配置叢集的儲存庫。
{:shortdesc}

**預設 `kube-system` 原則 `.yaml` 檔案**：

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
    # These policies allow all IBM Cloud Container Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```

### IBM-system 原則
{: #ibm-system}

依預設，會為 `ibm-system` 名稱空間安裝名稱空間層面的原則。此原則容許將任何容器登錄的所有映像檔部署到 `ibm-system` 而不強制執行。它也容許用來配置叢集的儲存庫，以及安裝或升級 Image Security Enforcement。
{:shortdesc}

**預設 `ibm-system` 原則 `.yaml` 檔案**：

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
    # These policies allow all IBM Cloud Container Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
    # This policy prevents Image Security Enforcement from blocking itself
    - name: "registry*.bluemix.net/ibm/ibmcloud-image-enforcement"
      policy:
    # This policy allows Image Security Enforcement to use Hyperkube to configure your cluster. This policy must exist if you uninstall Image Security Enforcement.
    - name: quay.io/coreos/hyperkube
      policies:
```

## 自訂原則
{: #customize_policies}

您可以在叢集或 Kubernetes 名稱空間層次，變更 IBM Container Image Security Enforcement 用來允許映像檔的原則。在原則中，您可以為不同映像檔指定不同的強制執行規則。
{:shortdesc}

您必須設定某個原則。否則，部署至您的叢集將會失敗。如果您不要強制執行任何映像檔安全原則，[請移除安全強制執行](#remove)。
{:tip}

當您套用部署時，Container Image Security Enforcement 會檢查您正在部署至的 Kubernetes 名稱空間是否有原則可套用。如果沒有，Container Image Security Enforcement 會使用叢集層面原則。如果沒有任何名稱空間或叢集層面原則存在，就會拒絕您的部署。

在開始之前，請[將 `kubectl` CLI 的目標](../../containers/cs_cli_install.html#cs_cli_configure)設為叢集。

1.  建立 <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">Kubernetes 自訂資源定義 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> `.yaml` 檔。

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

    <table>
    <caption>表. 瞭解這個 YAML 元件</caption>
    <thead>
    <th>欄位</th>
    <th>說明</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>若為叢集層面的原則，請將 `kind` 指定為 `ClusterImagePolicy`。若為 Kubernetes 名稱空間原則，請指定為 `ImagePolicy`。</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>命名自訂資源定義。</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>指定容許映像檔的來源儲存庫。儲存庫名稱接受萬用字元 (`*`)。除非 `repositories` 中有符合的項目允許，或是進一步套用驗證，否則會拒絕儲存庫。空的 `repositories` 清單會封鎖所有映像檔的部署。若要容許所有映像檔而不驗證任何原則，請將名稱設為 `*`，然後省略 policy 子區段。</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>填寫子區段以進行 `trust` 和 `va` 強制執行。如果您省略 policy 子區段，則等同於針對每一個都指定 `enabled: false`。</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>設為 `true`，只容許部署[針對內容信任簽署](registry_trusted_content.html)的映像檔。設為 `false` 會忽略是否簽署映像檔。</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>如果您只想要容許特定使用者簽署的映像檔，請指定具有簽章者名稱的 Kubernetes 密碼。省略此區段或將其保留空白，可驗證映像檔已簽署且不強制執行特定簽章者。如需相關資訊，請參閱[在自訂原則中指定受信任內容簽章者](#signers)。</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>設為 `true`，只容許通過[漏洞警告器](../va/va_index.html)掃描的映像檔。設為 `false` 會忽略漏洞警告器掃描。</td>
    </tr>
    </tbody>
    </table>

1.  將 `.yaml` 檔套用至您的叢集。

    ```
    kubectl apply -f <filepath>
    ```
    {: pre}

### 在自訂原則中指定受信任內容簽章者
{: #signers}

如果您使用內容信任，則可以驗證映像檔是否由特定簽章者簽署。只有在所有列出的簽章者已簽署最新的簽署版本時，才容許部署。如果要新增簽章者到儲存庫中，請參閱[管理受信任的簽章者](registry_trusted_content.html#trustedcontent_signers)。
{:shortdesc}

若要配置原則來驗證映像檔是否由特定的簽章者簽署，請執行下列動作：

1.  取得簽章者名稱（在 `docker trust signer add` 中使用的名稱`）和簽章者的公開金鑰。
1.  使用簽章者名稱及其公開金鑰產生 Kubernetes 密碼。
    ```
    kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
    ```
1.  將密碼新增至原則中儲存庫的 `signerSecrets` 清單。
    ```yaml
    - name: example
      policy:
        trust:
          enabled: true
          signerSecrets:
          - name: <secret_name>
    ```

## 控制可以自訂原則的人員
{: #assign_user_policy}

如果您在 Kubernetes 叢集上啟用了角色型存取控制 (RBAC)，則可以建立角色來控管誰可以在叢集上管理安全原則。如需將 RBAC 規則套用至叢集的相關資訊，請參閱 [IBM Cloud Container Service 文件](../../containers/cs_users.html#rbac)。
{:shortdesc}

在您的角色中，新增安全原則的規則：
```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```

您可以建立多個角色來控制使用者可以採取的動作。例如，變更 `verbs`，讓部分使用者只能 `get` 或 `list` 原則。或者，您可以從 `resources` 清單中省略 `clusterimagepolicies`，以便只授與對 Kubbernetes 名稱空間原則的存取權。
{:tip}

具有刪除自訂資源定義 (CRG) 之存取權的使用者，可以刪除安全原則的資源定義，這也會刪除您的安全原則。請務必控制被允許刪除 CRD 的人員。若要授與刪除 CRD 的存取權，請新增規則：

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```

**附註**：具有 `cluster-admin` 角色的使用者和服務帳戶都具有所有資源的存取權。即使您未編輯角色，cluster-admin 角色也會授與管理安全原則的存取權。請務必控制誰具有 `cluster-admin` 角色，並且只將存取權授與您要容許修改安全原則的人員。

## 使用強制執行安全來部署容器映像檔
{: #deploy_containers}

套用原則時，您可以正常地將內容部署至叢集。您的原則會由 Kubernetes 叢集自動強制執行。如果您的部署符合原則，且該原則容許它，則叢集將接受您的部署並套用。
{:shortdesc}

如果 Container Image Security Enforcement 拒絕「部署」，則會建立「部署」，但由它建立的 ReplicaSet 無法擴增，且不會建立任何 Pod。您可以執行 `kubectl describe deployment <deployment-name>` 來尋找 ReplicaSet，然後執行 `kubectl describe rs <replicaset-name>` 查看部署遭拒的原因。

**範例錯誤訊息**：

*  如果您的映像檔不符合任何原則，或名稱空間或叢集中沒有原則。

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

*  如果您的映像檔符合原則，但不滿足該原則的「漏洞警告器」需求。

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Refer to your image vulnerability report for more details by using the command `bx cr va`.
   ```
   {: screen}

*  如果您的映像檔符合原則，但不滿足該原則的信任需求。

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

*  如果您的原則指定了映像檔的信任強制執行，但您的映像檔不是來自受支援的登錄。

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

您可以在原則中啟用 `va` 選項，以強制執行「漏洞警告器」作業，之後便可以部署映像檔。容許「漏洞警告器」不支援的映像檔。

您可以在原則中啟用 `trust` 選項，以強制執行內容信任。如果您未指定任何 `signerSecret`，則會容許任何人簽署的映像檔。如果您指定 `signerSecret`，則映像檔的最新簽署版本必須已由您指定的所有簽章者簽署。IBM Container Image Security Enforcement 會驗證所提供的公開金鑰是否屬於簽章者。如需內容信任的相關資訊，請參閱[簽署受信任內容的映像檔](registry_trusted_content.html)。

只有在所有映像檔都通過 IBM Container Image Security Enforcement 檢查時才會容許部署。

## 移除 Container Image Security Enforcement
{: #remove}

在開始之前，請[將 `kubectl` CLI 的目標](../../containers/cs_cli_install.html#cs_cli_configure)設為叢集。



1.  停用 Container Image Security Enforcement。

    ```
    $ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config 
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config 
    ```
    {: codeblock}

2.  移除圖表。

    ```
    helm delete --purge cise
    ```
    {: pre}
