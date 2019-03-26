---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, user access, Identity and Access Management, policies, user roles, access policies, platform management roles, service access roles, access roles,

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

# Identity and Access Management を使用したユーザー・アクセス権限の管理
{: #iam}

{{site.data.keyword.registrylong}} に対する、アカウント内のユーザーに関するアクセス権限は、{{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) によって制御されます。
{: shortdesc}

{{site.data.keyword.registrylong_notm}} 内のご使用のアカウントを対象に IAM ポリシーを有効にする際には、アカウント内の {{site.data.keyword.registrylong_notm}} サービスにアクセスするすべてのユーザーに、IAM ユーザー役割が定義されたアクセス・ポリシーを割り当てる必要があります。 そのポリシーによって、サービスのコンテキスト内でユーザーが持つ役割や、ユーザーが実行できるアクションが決まります。 {{site.data.keyword.registrylong_notm}} での各アクションは、1 つ以上の [IAM ユーザー役割](/docs/iam?topic=iam-userroles)にマップされます。

IAM ポリシーは、IAM を使用して {{site.data.keyword.registrylong_notm}} にログインする場合に限り適用されます。 レジストリー・トークンなどの別の方式を使用して {{site.data.keyword.registrylong_notm}} にログインする場合には、ポリシーは適用されません。 自動化に使用している ID について、1 つ以上の名前空間へのアクセスを制限する場合は、レジストリー・トークンではなく IAM サービス ID の使用を検討してください。 サービス ID について詳しくは、[サービス ID の作成と処理](/docs/iam?topic=iam-serviceids#serviceids)を参照してください。

IAM について詳しくは、[IBM Cloud Access and Access Management](/docs/iam?topic=iam-iamoverview#iamoverview) を参照してください。

{{site.data.keyword.registrylong_notm}} のポリシーの有効化について詳しくは、[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry?topic=registry-user#user)を参照してください。

ポリシーにより、さまざまなレベルでアクセス権限を付与できます。 一部のオプションには、以下のアクセス・レベルが含まれています。

* アカウント内のサービスに対するアクセス権限
* サービス内の特定のリソースに対するアクセス権限
* アカウント内のすべての IAM 対応サービスに対するアクセス権限

アクセス・ポリシーの有効範囲を定義した後に、役割を割り当てることができます。 {{site.data.keyword.registrylong_notm}} サービス内で各役割が実行できるアクションを示した、下記の表を参照してください。

UI でのユーザー役割の割り当てについては、[IAM アクセス権限の管理](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)を参照してください。

[チュートリアル: {{site.data.keyword.registrylong_notm}} リソースに対するアクセス権限の付与](/docs/services/Registry?topic=registry-iam_access#iam_access)のチュートリアルをお試しください。
{: tip}

## プラットフォーム管理の役割
{: #platform_management_roles}

下記の表は、プラットフォーム管理役割にマップされたアクションの詳細を示しています。 プラットフォーム管理役割により、ユーザーはプラットフォーム・レベルでサービス・リソースに対するタスクを実行できます。例えば、サービスに関するユーザー・アクセス権限の割り当てや、サービス ID の作成または削除などを実行できます。

| プラットフォーム管理の役割 | アクションの説明 | アクションの例|
|:-----------------|:-----------------|:-----------------|
| ビューアー | サポートなし | |
| エディター | サポートなし | |
| オペレーター | サポートなし | |
| 管理者 | <ul><li>他のユーザー用のアクセス権の構成</li><li>レジストリー・トークンの構成</li><li>クラスターの作成</li></ul> | <ul><li>UI でのユーザー役割の割り当てについては、[IAM アクセス権限の管理](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)を参照してください。</li><li>レジストリー・トークンの追加、リスト、取得、削除</li><li>{{site.data.keyword.containerlong_notm}} でクラスターを作成するには、{{site.data.keyword.registrylong_notm}} の管理者の役割をユーザーに割り当てなければなりません。[クラスターの作成の準備](/docs/containers?topic=containers-clusters#cluster_prepare) を参照してください。</li></ul> |
{: caption="表 1. IAM ユーザーの役割とアクション" caption-side="top"}

{{site.data.keyword.registrylong_notm}} のために、以下のアクションが用意されています。

| 操作| サービスに対する操作 | 役割
|:-----------------|:-----------------|:--------------|
| `container-registry.registrytoken.create` | [`ibmcloud cr token-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_add) - レジストリーへのアクセスを制御するために使用できるトークンを追加します。 | 管理者 |
| `container-registry.registrytoken.delete` | [`ibmcloud cr token-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_rm) - 指定した 1 つ以上のトークンを削除します。 | 管理者 |
| `container-registry.registrytoken.get` | [`ibmcloud cr token-get`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_get) - 指定したトークンをレジストリーから取得します。 | 管理者 |
| `container-registry.registrytoken.list` | [`ibmcloud cr token-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_list) - {{site.data.keyword.Bluemix_notm}} アカウント用に存在するすべてのトークンを表示します。 | 管理者 |
{: caption="表 2. {{site.data.keyword.registrylong_notm}} の構成に関するプラットフォームのアクションと操作" caption-side="top"}

## サービス・アクセス役割
{: #service_access_roles}

次の表は、サービス・アクセス役割にマップされたアクションの詳細を示しています。 ユーザーは、サービス・アクセス役割を持つことで、{{site.data.keyword.registrylong_notm}} にアクセスしたり、{{site.data.keyword.registrylong_notm}} API を呼び出したりすることができます。

| サービス・アクセス役割 | アクションの説明 | アクションの例|
|:-----------------|:-----------------|:-----------------|
| リーダー | リーダーの役割は情報を表示できます。 | <ul><li>イメージの表示、検査、プル</li><li>名前空間の表示</li><li>割り当て量の表示</li><li>脆弱性レポートの表示</li><li>イメージの署名の表示</li></ul>|
| ライター | ライターの役割は情報を編集できます。 |<ul><li>イメージのビルド、プッシュ、削除</li><li>割り当て量の表示</li><li>イメージへの署名</li><li>名前空間の追加と削除</li></ul> |
| 管理者 | マネージャーの役割はすべてのアクションを実行できます。 | <ul><li>イメージの表示、検査、プル、ビルド、プッシュ、削除</li><li>名前空間の表示、追加、削除</li><li>割り当て量の表示と設定</li><li>脆弱性レポートの表示</li><li>イメージの署名の表示と作成</li><li>料金プランの確認と変更</li><li>IAM ポリシーの制約の有効化</li><li>脆弱性アドバイザーの免除の管理</li></ul> |
{: caption="表 3. IAM のサービス・アクセス役割とアクション" caption-side="top"}

 以下の {{site.data.keyword.registrylong_notm}} コマンドの場合、以下の表に示されているように、1 つ以上の役割が指定されていなければなりません。 {{site.data.keyword.registrylong_notm}} へのアクセスを許可するポリシーを作成するには、サービス名 `container-registry`、空のサービス・インスタンス、アクセス権限を付与しようとしている地域または空の地域 (すべての地域にアクセス権限を付与する) を指定してポリシーを作成しなければなりません。

### {{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割
{: #access_roles_configure}

アカウント内で {{site.data.keyword.registrylong_notm}} を構成するユーザー権限を付与するには、以下の表にある役割を 1 つ以上付与するポリシーを作成しなければなりません。 ポリシーの作成時に `resource type` 、および `resource` を指定することはできません。

**例**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

| 操作| サービスに対する操作 | 役割
|:-----------------|:-----------------|:--------------|
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) IAM ポリシーの制約を有効化します。 | 管理者 |
| `container-registry.exemption.manager` | <ul><li>[`ibmcloud cr exemption-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add) - セキュリティー問題の免除を作成します。</li><li>[`ibmcloud cr exemption-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list) - セキュリティー問題の免除をリストします。</li><li>[`ibmcloud cr exemption-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm) - セキュリティー問題の免除を削除します。</li><li>[`ibmcloud cr exemption-types`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types) - 免除できるセキュリティー問題のタイプをリストします。</li></ul> | 管理者 |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan) - 価格プランを表示します。 | 管理者 |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade) - 標準プランにアップグレードします。 | 管理者 |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota) - トラフィックおよびストレージの現在の割り当て量、およびそれらの割り当て量に対する使用量の情報を表示します。 | リーダー、ライター、管理者 |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set) - 指定された割り当て量を変更します。 | 管理者 |
{: caption="表 4. {{site.data.keyword.registrylong_notm}} の構成に関するサービスのアクションと操作" caption-side="top"}

### {{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割
{: #access_roles_using}

アカウント内で {{site.data.keyword.registrylong_notm}} のコンテンツにアクセスするユーザー権限を付与するには、以下の表にある役割を 1 つ以上付与するポリシーを作成しなければなりません。 ポリシーの作成時に、リソース・タイプ `namespace` 、およびリソースとして名前空間名を指定することにより、特定の名前空間にアクセスを制限できます。 `resource-type` と `resource` を指定しないと、ポリシーはアカウント内のすべてのリソースへのアクセス権限を付与します。

**例**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Reader> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

| アクション | サービスに対する操作 | 役割
|:-----------------|:-----------------|:--------------|
| `container-registry.image.build` | [`ibmcloud cr build`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) - コンテナー・イメージを構築します。 | ライター、管理者 |
| `container-registry.image.delete` | <ul><li> [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) 1 つ以上のイメージを削除します。</li><li>`docker trust revoke` - 署名を削除します。 </li></ul> | ライター、管理者 |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) - 特定のイメージに関する詳細を表示します。 | リーダー、管理者 |
| `container-registry.image.list` | [`ibmcloud cr image-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) - コンテナー・イメージをリストします。 | リーダー、管理者 |
| `container-registry.image.pull` | <ul><li>`docker pull` イメージをプルします。 </li><li>`docker trust inspect` 署名を検査します。 </li></ul> | リーダー、ライター、管理者 |
| `container-registry.image.push` | <ul><li>`docker push` - イメージをプッシュします。</li><li>`docker trust sign` イメージに署名します。</li><li>[`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load) - [IBM お客様向けパスポート・アドバンテージ・オンライン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/software/passportadvantage/pao_customer.html) からダウンロードした、Helm で使用できるようにパッケージ化された IBM ソフトウェアを、{{site.data.keyword.registrylong_notm}}名前空間にインポートします。</li></ul> | ライター、管理者 |
| `container-registry.image.tag` | [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) ソース・イメージを参照する新しいイメージを作成します。 ソース・イメージとターゲット・イメージは、同一の領域内になければなりません。 | ソース・イメージのリーダー、ライター、または管理者; ターゲット・イメージのリーダー、ライター、または管理者 |
| `container-registry.image.vulnerabilities` | [`ibmcloud cr vulnerability-assessment`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va) - イメージの脆弱性評価レポートを表示します。 | リーダー、管理者 |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add) - 名前空間を追加します。 | ライター、管理者 |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm) - 名前空間を削除します。 | ライター、管理者 |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list) - 名前空間を表示します。 | リーダー、管理者 |
{: caption="表 5. {{site.data.keyword.registrylong_notm}} の使用に関するサービスのアクションと操作" caption-side="top"}
