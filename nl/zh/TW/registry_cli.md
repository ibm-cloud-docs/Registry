---



copyright:
  years: 2017, 2018
lastupdated: "2018-05-31"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI 是一個外掛程式，可為您的 {{site.data.keyword.Bluemix_notm}} 帳戶管理登錄及其資源。
{: shortdesc}

**必要條件**
* 在執行登錄指令之前，請先使用 `bx login` 指令登入 {{site.data.keyword.Bluemix_notm}}，以產生存取記號並鑑別您的階段作業。

若要找出如何使用 {{site.data.keyword.registrylong_notm}} CLI 的詳細資訊，請參閱[開始使用 {{site.data.keyword.registrylong_notm}}](index.html)。

**附註**：請勿將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。


<table summary="管理 {{site.data.keyword.registrylong_notm}}">
<caption>表 1. 用於管理 {{site.data.keyword.registrylong_notm}} 的指令
</caption>
 <thead>
 <th colspan="5">用於管理登錄的指令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr build](#bx_cr_build)</td>
 <td>[bx cr info](#bx_cr_info)</td>
 <td>[bx cr image-inspect](#bx_cr_image_inspect)</td>
 <td>[bx cr image-list (bx cr images)](#bx_cr_image_list)</td>
 </tr>
 <tr>
 <td>[bx cr image-rm](#bx_cr_image_rm)</td>
 <td>[bx cr login](#bx_cr_login)</td>
 <td>[bx cr namespace-add](#bx_cr_namespace_add)</td>
 <td>[bx cr namespace-list (bx cr namespaces)](#bx_cr_namespace_list)</td>
 <td>[bx cr namespace-rm](#bx_cr_namespace_rm)</td>
 </tr>
 <tr>
 <td>[bx cr plan](#bx_cr_plan)</td>
 <td>[bx cr plan-upgrade](#bx_cr_plan_upgrade)</td>
 <td>[bx cr ppa-archive-load](#bx_cr_ppa_archive_load)</td>
 <td>[bx cr quota](#bx_cr_quota)</td>
 <td>[bx cr quota-set](#bx_cr_quota_set)</td>
 </tr>
 <tr>
 <td>[bx cr region](#bx_cr_region)</td>
 <td>[bx cr region-set](#bx_cr_region_set)</td>
 <td>[bx cr token-add](#bx_cr_token_add)</td>
 <td>[bx cr token-get](#bx_cr_token_get)</td>
 <td>[bx cr token-list (bx cr tokens)](#bx_cr_token_list)</td>
 </tr><tr>
 <td>[bx cr token-rm](#bx_cr_token_rm)</td>
 <td>[bx cr vulnerability-assessment (bx cr va)](#bx_cr_va)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

傳回執行指令所針對之登錄 API 端點的相關詳細資料。

```
bx cr api
```
{: codeblock}


## bx cr build
{: #bx_cr_build}

在 {{site.data.keyword.registrylong_notm}} 中建置 Docker 映像檔。

```
bx cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**參數**
<dl>
<dt>DIRECTORY</dt>
<dd>建置環境定義的位置，其中包含您的 Dockerfile 及必要檔案。</dd>
<dt>--no-cache</dt>
<dd>（選用）如果指定的話，這個建置中不會使用來自先前建置的已快取映像檔層。</dd>
<dt>--pull</dt>
<dd>（選用）如果指定的話，即使建置主機上已有具備相符標籤的映像檔存在，也會取回基礎映像檔。</dd>
<dt>--quiet, -q</dt>
<dd>（選用）如果指定的話，將會暫停建置輸出，除非發生錯誤。</dd>
<dt> --build-arg KEY=VALUE</dt>
<dd>（選用）以 'KEY=VALUE' 格式指定其他建置引數。多次包含此參數，即可指定多個建置引數。當您指定符合 Dockerfile 中之金鑰的 ARG 行時，每一個建置引數的值就可以當成環境變數使用。</dd>
<dt>--file FILE, -f FILE</dt>
<dd>（選用）如果您對多個建置使用相同的檔案，則可以選擇另一個 Dockerfile 的路徑。請指定相對於建置環境定義的 Dockerfile 位置。如果未指定，則預設值為 `PATH/Dockerfile`，其中 PATH 是建置環境定義的根目錄。</dd>
<dt>--tag TAG, -t TAG</dt>
<dd>您要建置之映像檔的完整名稱，其中包括登錄 URL 和名稱空間。</dd>
</dl>


## bx cr info
{: #bx_cr_info}

顯示所登入之登錄的名稱及帳戶。

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
{: #bx_cr_image_inspect}

顯示特定映像檔的詳細資料。

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**參數**
<dl>
<dt>--format FORMAT</dt>
<dd>（選用）使用 Go 範本將輸出元素格式化。

如需相關資訊，請參閱[格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出](registry_cli_reference.html#registry_cli_listing)。

</dd>
<dt>IMAGE</dt>
<dd>您要取得其報告的映像檔名稱。若要檢查多個映像檔，您可以在指令中列出每一個映像檔，並以空格隔開每一個名稱。

<p>若要尋找映像檔的名稱，請執行 `bx cr image-list`。請以 `repository:tag` 格式，結合 Repository 及 Tag 直欄的內容來建立映像檔名稱。如果映像檔名稱中未指定標籤，則會檢查以 `latest` 標記的映像檔。</p>

</dd>
</dl>


## bx cr image-list (bx cr images)
{: #bx_cr_image_list}

顯示 {{site.data.keyword.Bluemix_notm}} 帳戶中的所有映像檔。

<p>**附註：**映像檔名稱是 Repository 及 Tag 直欄的內容組合，格式為 `repository:tag`。</p>

```
 bx cr image-list [--no-trunc] [--format FORMAT] [-q, --quiet] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**參數**
<dl>
<dt>--no-trunc</dt>
<dd>（選用）不要截斷映像檔摘要。</dd>
<dt>--format FORMAT</dt>
<dd>（選用）使用 Go 範本將輸出元素格式化。

如需相關資訊，請參閱[格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出](registry_cli_reference.html#registry_cli_listing)。

</dd>
<dt>-q, --quiet</dt>
<dd>（選用）以下列格式列出每一個映像檔：`repository:tag`</dd>
<dt>--restrict RESTRICTION</dt>
<dd>（選用）限制輸出，只顯示所指定名稱空間或名稱空間及儲存庫中的映像檔。</dd>
<dt>--include-ibm</dt>
<dd>（選用）將 {{site.data.keyword.IBM_notm}} 提供的公用映像檔包含在輸出中。若不使用此選項，依預設只會列出專用映像檔。</dd>
</dl>



## bx cr image-rm
{: #bx_cr_image_rm}

從登錄中刪除一個以上的指定映像檔。

```
bx cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**參數**
<dl>
<dt>IMAGE</dt>
<dd>您要取得其報告的映像檔名稱。若要同時刪除多個映像檔，您可以在指令中列出每一個映像檔，並以空格隔開每一個名稱。

<p>若要尋找映像檔的名稱，請執行 `bx cr image-list`。請以 `repository:tag` 格式，結合 Repository 及 Tag 直欄的內容來建立映像檔名稱。如果映像檔名稱中未指定標籤，則依預設會刪除以 `latest` 標記的映像檔。</p>

</dd>
</dl>


## bx cr login
{: #bx_cr_login}

這個指令會對登錄執行 `docker login` 指令。必須執行 `docker login` 指令，才能針對登錄執行 `docker push` 或 `docker pull` 指令。若要執行其他 `bx cr` 指令，則不需要執行這個指令。如果未安裝 Docker，則這個指令會傳回錯誤訊息。

```
  bx cr login
  ```
{: codeblock}


## bx cr namespace-add
{: #bx_cr_namespace_add}

將名稱空間新增至 {{site.data.keyword.Bluemix_notm}} 帳戶。

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**參數**
<dl>
<dt>NAMESPACE</dt>
<dd>您要新增的名稱空間。此名稱空間在相同地區的所有 {{site.data.keyword.Bluemix_notm}} 帳戶中必須是唯一的。
  
<p>  
<strong>附註</strong>：請勿將個人資訊放在名稱空間名稱中。</p>
  
</dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
{: #bx_cr_namespace_list}

顯示 {{site.data.keyword.Bluemix_notm}} 帳戶所擁有的所有名稱空間。

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
{: #bx_cr_namespace_rm}

從 {{site.data.keyword.Bluemix_notm}} 帳戶中移除名稱空間。移除名稱空間時，會刪除此名稱空間中的映像檔。

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**參數**
<dl>
<dt>NAMESPACE</dt>
<dd>您要移除的名稱空間。</dd>
</dl>


## bx cr plan
{: #bx_cr_plan}

顯示定價方案。

```
bx cr plan
```
{: codeblock}


## bx cr plan-upgrade
{: #bx_cr_plan_upgrade}

升級為標準方案。

如需方案的相關資訊，請參閱[登錄方案](registry_overview.html#registry_plans)。

```
bx cr plan-upgrade [PLAN]
```
{: codeblock}

**參數**
<dl>
<dt>PLAN</dt>
<dd>您要升級到的定價方案名稱。如果未指定 PLAN，則預設值為 `standard`。</dd>
</dl>


## bx cr ppa-archive-load
{: #bx_cr_ppa_archive_load}

將從 [IBM Passport Advantage ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www-01.ibm.com/software/passportadvantage/pao_customer.html) 下載，並包裝以搭配 Helm 使用的 IBM 軟體，匯入到您的專用登錄名稱空間。

容器映像檔會推送至您的專用 {{site.data.keyword.registryshort_notm}} 名稱空間。Helm 圖表會寫入到您執行指令所在目錄中建立的 `ppa-import` 目錄裡。您可以選擇性地使用 [Chart Museum 開放程式碼專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 來管理 helm 圖表。

**範例指令**：
```
bx cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**參數**：
<dl>
  <dt>--archive FILE</dt>
  <dd>從 IBM Passport Advantage 下載之壓縮檔的路徑。</dd>
  <dt>--namespace NAMESPACE</dt>
  <dd>您的其中一個名稱空間。壓縮檔中的容器映像檔會推送至此名稱空間。若要列出名稱空間，請執行 `bx cr namespace-list`。</dd>
  <dt>--chartmuseum-uri URI</dt>
  <dd>（選用）您的 [Chart Museum ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 唯一資源 ID。</dd>
  <dt>--chartmuseum-user USER</dt>
  <dd>（選用）您的 [Chart Museum ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 使用者名稱。</dd>
  <dt>--chartmuseum-password PASSWORD</dt>
  <dd>（選用）您的 [Chart Museum ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 密碼。</dd>
</dl>


## bx cr quota
{: #bx_cr_quota}

顯示資料流量及儲存空間的現行配額，以及這些配額的用量資訊。

```
bx cr quota
```
{: codeblock}


## bx cr quota-set
{: #bx_cr_quota_set}

修改指定的配額。

```
bx cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**參數**
<dl>
<dt>--traffic TRAFFIC</dt>
<dd>（選用）將資料流量配額變更為指定的值 (MB)。如果您未獲授權，無法設定資料流量，或是設定了超出現行定價方案的值，則作業會失敗。</dd>
<dt>--storage STORAGE</dt>
<dd>（選用）將儲存空間配額變更為指定的值 (MB)。如果您未獲授權，無法設定儲存空間配額，或是設定了超出現行定價方案的值，則作業會失敗。</dd>
</dl>


## bx cr region
{: #bx_cr_region}

顯示目標地區及登錄。

```
bx cr region
```
{: codeblock}

如需相關資訊，請參閱[地區](registry_overview.html#registry_regions)。


## bx cr region-set
{: #bx_cr_region_set}

設定 {{site.data.keyword.registrylong_notm}} 指令的目標地區。若要列出可用的地區，請執行不含任何參數的指令。

```
bx cr region-set [REGION]
```
{: codeblock}

**參數**
<dl>
<dt>REGION</dt>
<dd>（選用）目標地區的名稱，例如 `us-south`。

如需相關資訊，請參閱[地區](registry_overview.html#registry_regions)。

</dd>
</dl>


## bx cr token-add
{: #bx_cr_token_add}

新增可用來控制登錄存取權的記號。

```
bx cr token-add [--description DESCRIPTION] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**參數**
<dl>
<dt>--description DESCRIPTION</dt>
<dd>（選用）指定值作為記號說明，在您執行 `bx cr token-list` 時顯示。如果 {{site.data.keyword.containerlong_notm}} 自動建立您的記號，則會將說明設為 Kubernetes 叢集名稱。在此情況下，移除您的叢集時，會自動移除此記號。
  
<p> 
  <strong>附註</strong>：請勿將個人資訊放在記號說明中。</p>

  </dd>
<dt>-q, --quiet</dt>
<dd>（選用）僅顯示記號，不含任何周圍文字。</dd>
<dt>--non-expiring</dt>
<dd>（選用）建立具有不會到期之存取權的記號。若未設定此參數，記號的存取權依預設會在 24 個小時之後到期。</dd>
<dt>--readwrite</dt>
<dd>（選用）建立授與讀取權及寫入權的記號。若未使用此選項，則依預設為唯讀存取權。</dd>
</dl>


## bx cr token-get
{: #bx_cr_token_get}

從登錄中擷取指定的記號。

```
bx cr token-get TOKEN
```

{: codeblock}

**參數**
<dl>
<dt>TOKEN</dt>
<dd>（選用）您要擷取之記號的唯一 ID。</dd>
</dl>


## bx cr token-list (bx cr tokens)
{: #bx_cr_token_list}

顯示 {{site.data.keyword.Bluemix_notm}} 帳戶的所有現有記號。

```
bx cr token-list --format FORMAT
```
{: codeblock}

**參數**
<dl>
<dt>--format FORMAT</dt>
<dd>（選用）使用 Go 範本將輸出元素格式化。

如需相關資訊，請參閱[格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出](registry_cli_reference.html#registry_cli_listing)。

</dd>
</dl>


## bx cr token-rm
{: #bx_cr_token_rm}

移除一個以上的指定記號。

```
bx cr token-rm TOKEN [TOKEN...]
```
{: codeblock}

**參數**
<dl>
<dt>TOKEN</dt>
<dd>（選用）TOKEN 可以是記號本身，或記號的唯一 ID（如 `bx cr token-list` 中所示）。您可以指定多個記號，而且必須以空格予以區隔。</dd>
</dl>


## bx cr vulnerability-assessment (bx cr va)
{: #bx_cr_va}

檢視映像檔的漏洞評量報告。

```
bx cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**參數**
<dl>
<dt>IMAGE</dt>
<dd>您要取得其報告的映像檔名稱。報告會告訴您映像檔是否有任何已知的套件漏洞。若要同時要求多個映像檔的報告，您可以在指令中列出每一個映像檔，並以空格隔開每一個名稱。

<p>若要尋找映像檔的名稱，請執行 `bx cr image-list`。請以 `repository:tag` 格式，結合 Repository 及 Tag 直欄的內容來建立映像檔名稱。如果映像檔名稱中未指定標籤，則報告會評量以 `latest` 標記的映像檔。</p>

<p>支援下列作業系統：

<ul>

<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>

</p>

如需相關資訊，請參閱[使用漏洞警告器管理映像檔安全](../va/va_index.html)。

</dd>
<dt>--output FORMAT, -o FORMAT</dt>
<dd>（選用）以選擇的格式傳回指令輸出。預設格式為 `text`。支援的格式如下：

<ul>

<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
<dt>--vulnerabilities, -v</dt>
<dd>（選用）指令輸出限制為只顯示漏洞。</dd>
<dt>--configuration-issues, -c</dt>
<dd>（選用）指令輸出限制為只顯示配置問題。</dd>
<dt>--extended, -e </dt>
<dd>（選用）指令輸出會針對有漏洞的套件顯示修正程式的其他資訊。</dd>

</dl>
