---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

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

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

您可以使用 {{site.data.keyword.registrylong}} CLI（其在 `container-registry` 外掛程式中提供），針對您的 {{site.data.keyword.Bluemix_notm}} 帳戶管理登錄及其資源。
{: shortdesc}

**必要條件**

* 安裝 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。使用 {{site.data.keyword.Bluemix_notm}} CLI 來執行指令的字首是 `ibmcloud`。
* 在執行登錄指令之前，請先使用 `ibmcloud login` 指令登入 {{site.data.keyword.Bluemix_notm}}，以產生存取記號並鑑別您的階段作業。

在指令行中，當有 `ibmcloud` CLI 及 `container-registry` CLI 外掛程式的更新可用時，即會通知您。請確定您保持最新的 CLI，讓您可以使用所有可用的指令及旗標。

如果您要檢視 `container-registry` CLI 外掛程式的現行版本，請執行 `ibmcloud plugin list`。

若要找出如何使用 {{site.data.keyword.registrylong_notm}} CLI 的詳細資訊，請參閱[開始使用 {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started)。

如需部分指令所需 IAM 平台及服務存取角色的相關資訊，請參閱[使用 Identity and Access Management 管理使用者存取](/docs/services/Registry?topic=registry-iam#iam)。

請不要將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。
{:tip}

## `ibmcloud cr api`
{: #bx_cr_api}

傳回執行指令所針對之登錄 API 端點的相關詳細資料。

```
ibmcloud cr api
```
{: codeblock}

**必要條件**

無

## `ibmcloud cr build`
{: #bx_cr_build}

在 {{site.data.keyword.registrylong_notm}} 中建置 Docker 映像檔。

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
<dt>`DIRECTORY`</dt>
<dd>建置環境定義的位置，其中包含您的 Dockerfile 及必要檔案。如果您在工作目錄設為建置環境定義儲存所在的位置時執行指令，則可以將 `DIRECTORY` 取代為句號 (.)。</dd>
<dt>`--no-cache`</dt>
<dd>（選用）如果指定，這個建置中不會使用來自先前建置的已快取映像檔層。</dd>
<dt>`--pull`</dt>
<dd>（選用）如果指定，則即使建置主機上已有具備相符標籤的映像檔存在，也會取回基礎映像檔。</dd>
<dt>`--quiet`, `-q`</dt>
<dd>（選用）如果指定，即會暫停建置輸出，除非發生錯誤。</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>（選用）以 `'KEY=VALUE'` 格式指定其他建置引數。藉由多次包含此參數，即可指定多個建置引數。當您指定符合 Dockerfile 中之金鑰的 ARG 行時，每一個建置引數的值會以環境變數的方式提供使用。</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>（選用）如果您對多個建置使用相同的檔案，則可以選擇另一個 Dockerfile 的路徑。請指定與建置環境定義相關的 Dockerfile 位置。如果未指定，則預設值為 `PATH/Dockerfile`，其中 PATH 是建置環境定義的根目錄。</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>您要建置之映像檔的完整名稱，其中包含登錄 URL 及名稱空間。</dd>
</dl>

**範例**

建置不使用先前建置之建置快取的 Docker 映像檔，其中會暫停建置輸出、標籤為 *`us.icr.io/birds/bluebird:1`*，且目錄是您的工作目錄。

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

建立安全問題的豁免。您可以建立適用於不同範圍之安全問題的豁免。範圍可以是帳戶、名稱空間、儲存庫或標籤。

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**指令選項**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>若要將帳戶設定為範圍，請使用 `"*"` 作為值。若要將名稱空間、儲存庫或標籤設定為範圍，請以下列其中一種格式來輸入值：`namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>您要豁免的安全問題類型。若要尋找有效的問題類型，請執行 `ibmcloud cr exemption-types`。
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>您要豁免的安全問題 ID。若要尋找問題 ID，請執行 `ibmcloud cr va <image>`，其中 `<image>` 是您映像檔的名稱，並且使用**漏洞 ID** 或**配置問題 ID** 直欄中的相關值。</dd>
</dl>

**範例**

對於 `us.icr.io/birds/bluebird` 儲存庫中的所有映像檔，建立 ID 為 `CVE-2018-17929` 之 CVE 的 CVE 豁免。

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

建立 ID 為 `CVE-2018-17929` 之 CVE 的帳戶層面 CVE 豁免。

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

對於標籤為 `us.icr.io/birds/bluebird:1` 的單一映像檔，建立問題 `application_configuration:nginx.ssl_protocols` 的配置問題豁免。

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

列出安全問題的豁免。

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**指令選項**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>（選用）僅列出適用於此範圍的豁免。若要將名稱空間、儲存庫或標籤設定為範圍，請以下列其中一種格式來輸入值：`namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
</dl>

**範例**

列出套用至 *`birds/bluebird`* 儲存庫中映像檔之安全問題的所有豁免。輸出包括帳戶層面的豁免、範圍限於 *`birds`* 名稱空間的豁免，以及範圍限於 *`birds/bluebird`* 儲存庫的豁免，但不包括所有範圍限於 *`birds/bluebird`* 儲存庫內特定標籤的豁免。

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

刪除安全問題的豁免。若要檢視現有豁免，請執行 `ibmcloud cr exemption-list`。

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**指令選項**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>若要將帳戶設定為範圍，請使用 `"*"` 作為值。若要將名稱空間、儲存庫或標籤設定為範圍，請以下列其中一種格式來輸入值：`namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>您要移除之安全問題的豁免問題類型。若要尋找豁免的問題類型，請執行 `ibmcloud cr exemption-list`。
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>您要移除之安全問題的豁免 ID。若要尋找豁免的問題 ID，請執行 `ibmcloud cr exemption-list`。
</dd>
</dl>

**範例**

對於 `us.icr.io/birds/bluebird` 儲存庫中的所有映像檔，刪除 ID 為 `CVE-2018-17929` 之 CVE 的 CVE 豁免。

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

刪除 ID 為 `CVE-2018-17929` 之 CVE 的帳戶層面 CVE 豁免。

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

對於標籤為 `us.icr.io/birds/bluebird:1` 的單一映像檔，刪除問題 `application_configuration:nginx.ssl_protocols` 的配置問題豁免。

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

列出您可豁免的安全問題類型。

```
ibmcloud cr exemption-types
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

如果您使用 IAM 鑑別，則此指令會啟用精細授權。如需相關資訊，請參閱[使用 Identity and Access Management 管理使用者存取](/docs/services/Registry?topic=registry-iam#iam)及[定義使用者存取角色原則](/docs/services/Registry?topic=registry-user#user)。

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

顯示目標 {{site.data.keyword.registryshort_notm}} 帳戶的 IAM 原則狀態。如需相關資訊，請參閱[使用 Identity and Access Management 管理使用者存取](/docs/services/Registry?topic=registry-iam#iam)及[定義使用者存取角色原則](/docs/services/Registry?topic=registry-user#user)。

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

顯示特定映像檔的詳細資料。

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
<dt>`--format FORMAT`</dt>
<dd>（選用）使用 Go 範本來將輸出元素格式化。

如需相關資訊，請參閱[格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)。

</dd>
<dt>`IMAGE`</dt>
<dd>您要取得其報告的映像檔名稱。您可以藉由在指令中列出每一個映像檔，並以空格隔開每一個名稱，來檢查多個映像檔。

<p>若要尋找映像檔的名稱，請執行 `ibmcloud cr image-list`。請以 `repository:tag` 格式，結合 **Repository** 及 **Tag** 直欄的內容，以建立映像檔名稱。如果映像檔名稱中未指定標籤，則會檢查以 `latest` 標記的映像檔。</p>

</dd>
</dl>

**範例**

使用格式化指引 *`"{{ .Config.ExposedPorts }}"`*，以顯示映像檔 *`us.icr.io/birds/bluebird:1`* 之已公開埠的詳細資料。

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

顯示 {{site.data.keyword.Bluemix_notm}} 帳戶中的所有映像檔。

映像檔名稱是 **Repository** 及 **Tag** 直欄的內容組合，格式為：`repository:tag`
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
<dt>`--no-trunc`</dt>
<dd>（選用）不要截斷映像檔摘要。</dd>
<dt>`--format FORMAT`</dt>
<dd>（選用）使用 Go 範本來將輸出元素格式化。

如需相關資訊，請參閱[格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)。

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>（選用）以下列格式列出每一個映像檔：`repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>（選用）限制輸出，只顯示所指定名稱空間或名稱空間及儲存庫中的映像檔。</dd>
<dt>`--include-ibm`</dt>
<dd>（選用）將 {{site.data.keyword.IBM_notm}} 提供的公用映像檔包括在輸出中。若不使用此選項，依預設只會列出專用映像檔。</dd>
</dl>

**範例**

顯示 *`birds`* 名稱空間中的映像檔，格式為 `repository:tag`，而不截斷映像檔摘要。

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

從 {{site.data.keyword.registrylong_notm}} 中刪除一個以上的指定映像檔。

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**

<dl>
<dt>`IMAGE`</dt>
<dd>您要刪除之映像檔的名稱。您可以藉由在指令中列出每一個映像檔，並以空格隔開每一個名稱，來同時刪除多個映像檔。`IMAGE` 的格式必須為 `repository:tag`，例如：`us.icr.io/namespace/image:latest`

<p>若要尋找映像檔的名稱，請執行 `ibmcloud cr image-list`。請以 `repository:tag` 格式，結合 **Repository** 及 **Tag** 直欄的內容，以建立映像檔名稱。如果映像檔名稱中未指定標籤，則依預設會刪除以 `latest` 標記的映像檔。</p>

</dd>
</dl>

**範例**
刪除映像檔 `us.icr.io/birds/bluebird:1`。

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

在 {{site.data.keyword.registrylong_notm}} 中，建立一個新映像檔 TARGET_IMAGE，其參照來源映像檔 SOURCE_IMAGE。來源及目標映像檔必須位於相同地區。

若要尋找映像檔的名稱，請執行 `ibmcloud cr image-list`。請以 `repository:tag` 格式，結合 **Repository** 及 **Tag** 直欄的內容，以建立映像檔名稱。
{: tip}

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>來源映像檔的名稱。`SOURCE_IMAGE` 的格式必須為 `repository:tag`，例如：`us.icr.io/namespace/image:latest`

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>目標映像檔的名稱。`TARGET_IMAGE` 的格式必須為 `repository:tag`，例如：`us.icr.io/namespace/image:latest`

</dd>
</dl>

**範例**

將另一個標記參照 `latest` 新增至映像檔 `us.icr.io/birds/bluebird:1`。

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

將映像檔 `us.icr.io/birds/bluebird:peck` 複製到相同名稱空間 `birds/pigeon` 中的另一個儲存庫。

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

將映像檔 `us.icr.io/birds/bluebird:peck` 複製到您有存取權的另一個名稱空間 `animals`。

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

顯示您所登入之登錄的名稱及帳戶。

```
ibmcloud cr info
```
{: codeblock}

**必要條件**

無

## `ibmcloud cr login`
{: #bx_cr_login}

這個指令會針對登錄執行 `docker login` 指令。必須執行 `docker login` 指令，才能對登錄執行 `docker push` 或 `docker pull` 指令。若要執行其他 `ibmcloud cr` 指令，則不需要執行這個指令。如果未安裝 Docker，則這個指令會傳回錯誤訊息。

```
ibmcloud cr login
```
{: codeblock}

**必要條件**

無

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

選擇名稱空間的名稱，並將其新增至 {{site.data.keyword.Bluemix_notm}} 帳戶。

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
<dt>`NAMESPACE`</dt>
<dd>您要新增的名稱空間。此名稱空間在相同地區的所有 {{site.data.keyword.Bluemix_notm}} 帳戶中必須是唯一的。名稱空間必須有 4-30 個字元，且只能包含小寫字母、數字、連字號及底線。名稱空間的開頭和結尾必須是字母或數字。
  
<p>  
<strong>提示</strong>：請不要將個人資訊放在名稱空間名稱中。
</p>
  
</dd>
</dl>

**範例**

建立名稱為 *`birds`* 的名稱空間。

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

顯示 {{site.data.keyword.Bluemix_notm}} 帳戶所擁有的所有名稱空間。

```
ibmcloud cr namespace-list
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

從 {{site.data.keyword.Bluemix_notm}} 帳戶中移除名稱空間。移除名稱空間時，會刪除此名稱空間中的映像檔。

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
<dt>`NAMESPACE`</dt>
<dd>您要移除的名稱空間。</dd>
<dt>`--force`, `-f`</dt>
<dd>（選用）強制執行指令而不產生使用者提示。</dd>
</dl>

**範例**

移除名稱空間 *`birds`*。

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

顯示定價方案。

```
ibmcloud cr plan
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

升級為標準方案。

如需方案的相關資訊，請參閱[登錄方案](/docs/services/Registry?topic=registry-registry_overview#registry_plans)。

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**指令選項**
<dl>
<dt>`PLAN`</dt>
<dd>（選用）您要升級到的定價方案名稱。如果未指定 `PLAN`，則預設值為 `standard`。</dd>
</dl>

**範例**

升級至標準定價方案。

```
   ibmcloud cr plan-upgrade standard
   ```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

將從 [IBM Passport Advantage Online for customers ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/software/passportadvantage/pao_customer.html) 下載並包裝以與 Helm 搭配使用的 {{site.data.keyword.IBM_notm}} 軟體，匯入到您的 {{site.data.keyword.registrylong_notm}} 名稱空間。

容器映像檔會推送至您的專用 {{site.data.keyword.registryshort_notm}} 名稱空間。Helm 圖表會寫入至您執行指令所在目錄中建立的 `ppa-import` 目錄。您可以選擇使用 [Chart Museum 開放程式碼專案 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 來管理 helm 圖表。

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>從 IBM Passport Advantage 下載之壓縮檔的路徑。</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>您的其中一個名稱空間。壓縮檔中的容器映像檔會推送至此名稱空間。若要列出名稱空間，請執行 `ibmcloud cr namespace-list`。</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>（選用）您的 [Chart Museum ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 唯一資源 ID。</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>（選用）您的 [Chart Museum ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 使用者名稱。</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>（選用）您的 [Chart Museum ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 密碼。</dd>
</dl>

**範例**

匯入 IBM 軟體，並將它包裝至您的 {{site.data.keyword.registrylong_notm}} 名稱空間 *`birds`* 以與 Helm 搭配使用，其中，壓縮檔的路徑為 *`downloads/compressed_file.tgz`*。

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

顯示資料流量及儲存空間的現行配額，以及這些配額的用量資訊。

```
ibmcloud cr quota
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

修改指定的配額。

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[配置 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**指令選項**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>（選用）將資料流量配額變更為指定的值 (MB)。如果您未獲授權，無法設定資料流量，或是設定了超出現行定價方案的值，則作業會失敗。</dd>
<dt>`--storage STORAGE`</dt>
<dd>（選用）將儲存空間配額變更為指定的值 (MB)。如果您未獲授權，無法設定儲存空間配額，或是設定了超出現行定價方案的值，則作業會失敗。</dd>
</dl>

**範例**

將取回資料流量的配額限制設為 *7000* MB，並將儲存空間設為 *600* MB。

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

顯示目標地區及登錄。

```
ibmcloud cr region
```
{: codeblock}

**必要條件**

無

如需相關資訊，請參閱[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)。

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

設定 {{site.data.keyword.registrylong_notm}} 指令的目標地區。若要列出可用的地區，請執行不含任何參數的指令。

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**必要條件**

無

**指令選項**
<dl>
<dt>`REGION`</dt>
<dd>（選用）目標地區的名稱，例如 `us-south`。

如需相關資訊，請參閱[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)。

</dd>
</dl>

**範例**

將「美國南部」地區設為目標。

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-add`
{: #bx_cr_token_add}

新增可用來控制登錄存取權的記號。

```
ibmcloud cr token-add [--description DESCRIPTION] [--quiet | -q] [--non-expiring] [--readwrite]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**指令選項**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>（選用）指定值作為記號說明，這會在您執行 `ibmcloud cr token-list` 時顯示。如果 {{site.data.keyword.containerlong_notm}} 自動建立您的記號，則會將說明設為 Kubernetes 叢集名稱。在此情況下，移除您的叢集時，即會自動移除此記號。
  
<p> 
  <strong>提示</strong>：請不要將個人資訊放在記號說明中。
</p>

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>（選用）僅顯示記號，不含任何周圍文字。</dd>
<dt>`--non-expiring`</dt>
<dd>（選用）建立具有不會到期之存取權的記號。若未設定此參數，記號的存取權依預設會在 24 小時之後到期。</dd>
<dt>`--readwrite`</dt>
<dd>（選用）建立授與讀取權及寫入權的記號。若未使用此選項，則依預設為唯讀存取權。</dd>
</dl>

**範例**

新增說明為 *Token for my account* 且未到期並具有讀寫存取權的記號。

```
ibmcloud cr token-add --description "Token for my account" --non-expiring --readwrite
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

從登錄中擷取指定的記號。

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**指令選項**
<dl>
<dt>`TOKEN`</dt>
<dd>您要擷取之記號的唯一 ID。若要列出記號，請執行 `ibmcloud cr token-list`。</dd>
</dl>

**範例**

擷取記號 *10101010-101x-1x10-x1xx-x10xx10xxx10*。

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

顯示 {{site.data.keyword.Bluemix_notm}} 帳戶的所有現有記號。

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**指令選項**
<dl>
<dt>`--format FORMAT`</dt>
<dd>（選用）使用 Go 範本來將輸出元素格式化。

如需相關資訊，請參閱[格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)。

</dd>
</dl>

**範例**

使用格式化指引 *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`*，以顯示所有唯讀記號。

```
  ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
  ```
{: pre}

此範例會產生下列格式的輸出：

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

移除一個以上的指定登錄記號。

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**指令選項**
<dl>
<dt>`TOKEN`</dt>
<dd>TOKEN 可以是記號本身，或記號的唯一 ID（如 `ibmcloud cr token-list` 中所示）。您可以指定多個記號，且必須以空格予以區隔。</dd>
<dt>`--force`, `-f`</dt>
<dd>（選用）強制執行指令而不產生使用者提示。</dd>
</dl>

**範例**

移除記號 *10101010-101x-1x10-x1xx-x10xx10xxx10*。

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

檢視映像檔的漏洞評量報告。

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**必要條件**

若要瞭解必要的許可權，請參閱[使用 {{site.data.keyword.registrylong_notm}} 時所適用的存取角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**指令選項**
<dl>
<dt>`IMAGE`</dt>
<dd>您要取得其報告的映像檔名稱。報告會告訴您映像檔是否有任何已知的套件漏洞。您可以藉由在指令中列出每一個映像檔，並以空格隔開每一個名稱，來同時要求多個映像檔的報告。

<p>若要尋找映像檔的名稱，請執行 `ibmcloud cr image-list`。請以 `repository:tag` 格式，結合 **Repository** 及 **Tag** 直欄的內容，以建立映像檔名稱。如果映像檔名稱中未指定標籤，則報告會評量以 `latest` 標記的映像檔。</p>

<p>支援下列作業系統：

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

如需相關資訊，請參閱[使用漏洞警告器管理映像檔安全](/docs/services/va?topic=va-va_index)。

</dd>
<dt>`--extended`, `-e`</dt>
<dd>（選用）指令輸出會針對有漏洞的套件顯示有關修正程式的其他資訊。</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>（選用）指令輸出限制為只顯示漏洞。</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>（選用）指令輸出限制為只顯示配置問題。</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>（選用）以選擇的格式傳回指令輸出。預設格式為 `text`。支援的格式如下：

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**範例**

檢視映像檔的標準漏洞評量報告。

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

檢視 `us.icr.io/birds/bluebird:1` 映像檔的漏洞評量報告（JSON 格式），並僅顯示漏洞。

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
