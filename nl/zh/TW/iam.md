---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, user access

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

# 使用 Identity and Access Management 管理使用者存取
{: #iam}

您帳戶中使用者的 {{site.data.keyword.registrylong}} 存取權是由 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) 所控制。
{: shortdesc}

在 {{site.data.keyword.registrylong_notm}} 中啟用帳戶的 IAM 原則時，您帳戶中存取 {{site.data.keyword.registrylong_notm}} 服務的每位使用者都必須獲指派已定義 IAM 使用者角色的存取原則。該原則決定使用者在服務環境定義內所具有的角色，以及使用者可執行的動作。{{site.data.keyword.registrylong_notm}} 中的每個動作都會對映至一個以上的 [IAM 使用者角色](/docs/iam/users_roles.html)。

只有在使用 IAM 登入 {{site.data.keyword.registrylong_notm}} 時，才會強制執行 IAM 原則。如果您使用另一種方法（例如登錄記號）登入 {{site.data.keyword.registrylong_notm}}，則不會強制執行您的原則。如果您要將存取權限制在自動化中所使用 ID 的一個以上名稱空間，則請考慮使用 IAM 服務 ID，而不要使用登錄記號。如需服務 ID 的相關資訊，請參閱[建立及使用服務 ID](/docs/iam/serviceid.html#serviceids)。

如需 IAM 的相關資訊，請參閱 [IBM Cloud Access and Management](/docs/iam/index.html#iamoverview)。

如需啟用 {{site.data.keyword.registrylong_notm}} 之原則的相關資訊，請參閱[定義使用者存取角色原則](/docs/services/Registry/registry_users.html#user)。

原則讓您能在不同層次授與存取權。部分選項包括下列存取層次：

* 存取您帳戶中的服務
* 存取服務內的特定資源
* 存取您帳戶中所有已啟用 IAM 功能的服務

在定義存取原則的範圍之後，您即可指派角色。請檢閱下列表格，其中概述每個角色容許在 {{site.data.keyword.registrylong_notm}} 服務內執行的動作。

如需在使用者介面中指派使用者角色的相關資訊，請參閱[管理 IAM 存取](/docs/iam/mngiam.html#iammanidaccser)。

請嘗試[指導教學：授與對 {{site.data.keyword.registrylong_notm}} 資源的存取權](/docs/services/Registry/registry_tutorial_configure_iam.html#iam_access)指導教學。
{: tip}

## 平台管理角色
{: #platform_management_roles}

下表詳述對映至平台管理角色的動作。平台管理角色可讓使用者在平台層次對服務資源執行作業，例如，指派服務的使用者存取權，以及建立或刪除服務 ID。

| 平台管理角色 | 動作的說明 | 範例動作 |
|:-----------------|:-----------------|:-----------------|
| 檢視者 | 不支援 | |
| 編輯者 | 不支援 | |
| 操作員 | 不支援 | |
| 管理者 | <ul><li>配置其他使用者的存取權</li><li>配置登錄記號</li><li>建立叢集</li></ul> | <ul><li>如需在使用者介面中指派使用者角色的相關資訊，請參閱[管理 IAM 存取](/docs/iam/mngiam.html#iammanidaccser)。</li><li>新增、列出、擷取及移除登錄記號</li><li>若要在 {{site.data.keyword.containerlong_notm}} 中建立叢集，您必須將 {{site.data.keyword.registrylong_notm}} 的「管理者」角色指派給使用者，請參閱[準備建立叢集](/docs/containers/cs_clusters.html#cluster_prepare)。</li></ul> |
{: caption="表 1. IAM 使用者角色及動作" caption-side="top"}

對於 {{site.data.keyword.registrylong_notm}}，存在下列動作：

|動作|對服務的作業| 角色
|:-----------------|:-----------------|:--------------|
| `container-registry.registrytoken.create` | [`ibmcloud cr token-add`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_token_add) 新增可用來控制登錄存取權的記號。| 管理者 |
| `container-registry.registrytoken.delete` | [`ibmcloud cr token-rm`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_token_rm) 移除一個以上的指定記號。| 管理者 |
| `container-registry.registrytoken.get` |[`ibmcloud cr token-get`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_token_get) 從登錄擷取指定的記號。| 管理者 |
| `container-registry.registrytoken.list` | [`ibmcloud cr token-list`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_token_list) 顯示 {{site.data.keyword.Bluemix_notm}} 帳戶的所有現有記號。| 管理者 |
{: caption="表 2. 用來配置 {{site.data.keyword.registrylong_notm}} 的平台動作及作業" caption-side="top"}

## 服務存取角色
{: #service_access_roles}

下表詳述對映至服務存取角色的動作。服務存取角色可讓使用者存取 {{site.data.keyword.registrylong_notm}} 以及能夠呼叫 {{site.data.keyword.registrylong_notm}} API。

| 服務存取角色 | 動作的說明 | 範例動作 |
|:-----------------|:-----------------|:-----------------|
| 讀者 |「讀者」角色可以檢視資訊。| <ul><li>檢視、檢查及取回映像檔</li><li>檢視名稱空間</li><li>檢視配額</li><li>檢視漏洞報告</li><li>檢視映像檔簽章</li></ul>|
| 撰寫者 |「撰寫者」角色可以編輯資訊。|<ul><li>建置、推送及刪除映像檔</li><li>檢視配額</li><li>簽署映像檔</li><li>新增及移除名稱空間</li></ul> |
| 管理員 |「管理員」角色可以執行所有動作。| <ul><li>檢視、檢查、取回、建置、推送及刪除映像檔</li><li>檢視、新增及移除名稱空間</li><li>檢視及設定配額</li><li>檢視漏洞報告</li><li>檢視及建立映像檔簽章</li><li>檢閱及變更定價方案</li><li>啟用 IAM 原則強制執行</li><li>管理漏洞警告器豁免</li></ul> |
{: caption="表 3. IAM 服務存取角色及動作" caption-side="top"}

 對於下列 {{site.data.keyword.registrylong_notm}} 指令，您必須至少具有下列各表格中所顯示的其中一個指定角色。若要建立容許存取 {{site.data.keyword.registrylong_notm}} 的原則，您必須建立原則，其中，服務名稱是 `container-registry`、服務實例是空的，而且地區是您要授與存取權的地區，或是空的地區以授與對所有地區的存取權。

### 用來配置 {{site.data.keyword.registrylong_notm}} 的存取角色
{: #access_roles_configure}

若要將在您帳戶中配置 {{site.data.keyword.registrylong_notm}} 的許可權授與給使用者，您必須建立原則，以授與下表中的一個以上角色。建立原則時，您不得指定 `resource-type` 或 `resource`。

**範例**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

|動作|對服務的作業| 角色
|:-----------------|:-----------------|:--------------|
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_iam_policies_enable) 啟用 IAM 原則強制執行。| 管理員 |
| `container-registry.exemption.manager` | <ul><li>[`ibmcloud cr exemption-add`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_exemption_add) 建立安全問題的豁免。</li><li>[`ibmcloud cr exemption-list`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_exemption_list) 列出安全問題的豁免。</li><li>[`ibmcloud cr exemption-rm`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_exemption_rm) 刪除安全問題的豁免。</li><li>[`ibmcloud cr exemption-types`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_exemption_types) 列出您可豁免的安全問題類型。</li></ul> | 管理員 |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_plan) 顯示您的定價方案。| 管理員 |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_plan_upgrade) 升級至標準方案。| 管理員 |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_quota) 顯示資料流量及儲存空間的現行配額，以及這些配額的用量資訊。| 讀者、撰寫者、管理員 |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_quota_set) 修改指定的配額。| 管理員 |
{: caption="表 4. 用來配置 {{site.data.keyword.registrylong_notm}} 的服務動作及作業" caption-side="top"}

### 用來使用 {{site.data.keyword.registrylong_notm}} 的存取角色
{: #access_roles_using}

若要將在您帳戶中存取 {{site.data.keyword.registrylong_notm}} 內容的許可權授與給使用者，您必須建立原則，以授與下表中的一個以上角色。建立原則時，您可以指定資源類型 `namespace` 及名稱空間名稱作為資源，將存取權限制在特定名稱空間。如果您未指定 `resource-type` 及 `resource`，則原則會授與對帳戶中所有資源的存取權。

**範例**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Reader> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

|動作|對服務的作業| 角色
|:-----------------|:-----------------|:--------------|
| `container-registry.image.build` | [`ibmcloud cr build`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_build) 建置容器映像檔。| 撰寫者、管理員 |
| `container-registry.image.delete` | <ul><li> [`ibmcloud cr image-rm`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_image_rm) 刪除一個以上的映像檔。</li><li> `docker trust revoke` 刪除簽章。</li></ul> | 撰寫者、管理員 |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_image_inspect) 顯示特定映像檔的詳細資料。| 讀者、管理員 |
| `container-registry.image.list` | [`ibmcloud cr image-list`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_image_list) 列出容器映像檔。| 讀者、管理員 |
| `container-registry.image.pull` | <ul><li> `docker pull` 取回映像檔。</li><li> `docker trust inspect` 檢查簽章。</li></ul> | 讀者、撰寫者、管理員 |
| `container-registry.image.push` | <ul><li>`docker push` 推送映像檔。</li><li>`docker trust sign` 簽署映像檔。</li><li>[`ibmcloud cr ppa-archive-load`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_ppa_archive_load) 將從 [IBM Passport Advantage Online for customers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/software/passportadvantage/pao_customer.html) 下載並包裝以與 Helm 搭配使用的 IBM 軟體，匯入到您的 {{site.data.keyword.registrylong_notm}} 名稱空間。</li></ul> | 撰寫者、管理員 |
| `container-registry.image.tag` | [`ibmcloud cr image-tag`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_image_tag) 建立參照來源映像檔的新映像檔。來源及目標映像檔必須位於相同地區。|來源映像檔的「讀者」、「撰寫者」或「管理員」；目標映像檔的「撰寫者」或「管理員」|
| `container-registry.image.vulnerabilities` | [`ibmcloud cr vulnerability-assessment`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_va) 檢視映像檔的漏洞評量報告。| 讀者、管理員 |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_namespace_add) 新增名稱空間。| 撰寫者、管理員 |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_namespace_rm) 移除名稱空間。| 撰寫者、管理員 |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_namespace_list) 顯示名稱空間。| 讀者、管理員 |
{: caption="表 5. 用來使用 {{site.data.keyword.registrylong_notm}} 的服務動作及作業" caption-side="top"}
