---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, commands, format commands, filter command output, private registry, registry commands, formatting output, filtering output, output, Go template options, data types, 

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

# 格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出
{: #registry_cli_list}

您可以格式化及過濾所支援 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出。
{:shortdesc}

依預設，會以人類可讀格式顯示 CLI 輸出。不過，此視圖可能會限制您使用輸出的能力，特別是以程式設計方式執行指令時。例如，在 `ibmcloud cr image-list` CLI 輸出中，您可能想要依數值大小排序 `Size` 欄位，但指令傳回大小的字串說明。`container-registry` CLI 外掛程式提供 format 選項，可用來將 Go 範本套用至 CLI 輸出。Go 範本是 [Go 程式設計語言 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://golang.org/pkg/text/template/) 的特性，可用來自訂 CLI 輸出。

您可以使用兩種不同方式套用 format 選項，以變更 CLI 輸出：

1. 格式化 CLI 輸出中的資料。例如，將 `Created` 欄位輸出從 UNIX 時間變更為標準時間。
2. 過濾 CLI 輸出中的資料。例如，依映像檔的詳細資料進行過濾，以使用 Go 範本 `if gt` 條件來顯示特定映像檔子集。

您可以搭配使用 format 選項與下列 {{site.data.keyword.registrylong_notm}} 指令。按一下指令，以檢視可用欄位及其資料類型的清單。

- [`ibmcloud cr image-list`](#registry_cli_list_imagelist)
- [`ibmcloud cr image-inspect`](#registry_cli_list_imageinspect)
- [`ibmcloud cr token-list`](#registry_cli_list_tokenlist)

下列程式碼範例示範如何使用格式化及過濾選項。

- 執行下列 `ibmcloud cr image-list` 指令，以顯示大小超過 1 MB 的所有映像檔的儲存庫、標籤及安全狀態：

  ```
  ibmcloud cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
  ```
  {: pre}

  **輸出範例**

  ```
  example-<region>.icr.io/user1/ibmliberty:latest No Issues
  example-<region>.icr.io/user1/ibmnode:1 2 Issues
  example-<region>.icr.io/user1/ibmnode:test1 1 Issue
  example-<region>.icr.io/user1/ibmnode2:test2 7 Issues
  ```
  {: screen}

- 執行下列 `ibmcloud cr image-inspect` 指令，以顯示管理所指定 IBM 公用映像檔的 IBM 文件的位置：

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"
  ```
  {: pre}

  **輸出範例**

  ```
  map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
  ```
  {: screen}

- 執行下列 `ibmcloud cr image-inspect` 指令，以顯示所指定映像檔的公開埠：

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"
  ```
  {: pre}

  **輸出範例**

  ```
  map[9080/tcp: 9443/tcp:]
  ```
  {: screen}

- 執行下列 `ibmcloud cr token-list` 指令，以顯示所有唯讀記號：

  ```
  ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
  ```
  {: pre}

  **輸出範例**

  ```
  0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
  ```
  {: screen}

## `ibmcloud cr image-list` 指令中的 Go 範本選項及資料類型
{: #registry_cli_list_imagelist}

檢閱下表，以尋找 `ibmcloud cr image-list` 指令的可用 Go 範本選項及資料類型。
{:shortdesc}

|欄位|類型|說明|
|-----|----|-----------|
|`Created`|整數（64 位元）|以 [UNIX 時間 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/Unix_time) 顯示映像檔的建立時間（以秒數表示）。|
|`Digest`|字串|顯示映像檔的唯一 ID。|
|`Namespace`|字串|顯示儲存映像檔的名稱空間。|
|`Repository`|字串|顯示映像檔的儲存庫。|
|`Size`|整數（64 位元）|顯示映像檔的大小（以位元組為單位）。|
|`Tag`|字串|顯示映像檔的標籤。|
|`SecurityStatus`|結構|顯示映像檔的漏洞狀態。您可以過濾及格式化下列值：*Status*  `string`、*IssueCount*  `int`，以及 *ExemptionCount*  `int`。[使用 CLI 檢閱漏洞報告](/docs/services/Registry?topic=va-va_index#va_registry_cli)中會說明可能的狀態。|
{: caption="表 1. <code>ibmcloud cr image-list</code> 指令中的可用欄位及資料類型。" caption-side="top"}

## `ibmcloud cr image-inspect` 指令中的 Go 範本選項及資料類型
{: #registry_cli_list_imageinspect}

檢閱下表，以尋找 `ibmcloud cr image-inspect` 指令的可用 Go 範本選項及資料類型。
{:shortdesc}

|欄位|類型|說明|
|-----|----|-----------|
|`ID`|字串|顯示映像檔的唯一 ID。|
|`Parent`|字串|顯示用來建置此映像檔之主映像檔的 ID。|
|`Comment`|字串|顯示映像檔的說明。|
|`Created`|字串|顯示建立映像檔時的 [UNIX 時間戳記 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/Unix_time)。|
|`Container`|字串|顯示已建立映像檔之容器的 ID。|
|`ContainerConfig`|物件|顯示已從此映像檔啟動之容器的預設配置。請參閱 [`Config`](#registry_cli_list_imageinspect_config) 中的欄位詳細資料。|
|`DockerVersion`|字串|顯示用來建置此映像檔的 Docker 版本。|
|`Author`|字串|顯示映像檔的作者。|
|`Config`|物件|顯示映像檔的配置 meta 資料。請參閱 [`Config`](#registry_cli_list_imageinspect_config) 中的欄位詳細資料。|
|`Architecture`|字串|顯示用來建置此映像檔、且為執行映像檔所需的處理器架構。|
|`Os`|字串|顯示用來建置此映像檔、且為執行映像檔所需的作業系統系列。|
|`OsVersion`|字串|顯示用來建置此映像檔的作業系統版本。|
|`Size`|整數（64 位元）|顯示映像檔的大小（以位元組為單位）。|
|`VirtualSize`|整數（64 位元）|顯示映像檔中每一層的大小總和（以位元組為單位）。|
|`RootFS`|物件|顯示說明映像檔根檔案系統的 meta 資料。請參閱 [`RootFS`](#registry_cli_list_imageinspect_rootfs) 中的欄位詳細資料。|
{: caption="表 2. <code>ibmcloud cr image-inspect</code> 指令中的可用欄位及資料類型。" caption-side="top"}

### `Config`
{: #registry_cli_list_imageinspect_config}

|欄位|類型|說明|
|-----|----|-----------|
|`Hostname`|字串|顯示容器的主機名稱。|
|`Domainname`|字串|顯示容器的完整網域名稱。|
|`User`|字串|顯示在使用映像檔的容器內執行指令的使用者。|
|`AttachStdin`|布林|如果標準輸入串流連接至容器，會顯示 _true_，否則會顯示 _false_。|
|`AttachStdout`|布林|如果標準輸出串流連接至容器，會顯示 _true_，否則會顯示 _false_。|
|`AttachStderr`|布林|如果標準錯誤串流連接至容器，會顯示 _true_，否則會顯示 _false_。|
|`ExposedPorts`|鍵值對映|顯示已公開埠的清單，格式為 `[123:,456:]`。|
|`Tty`|布林|如果 `pseudo-tty` 配置給容器，會顯示 _true_，否則會顯示 _false_。|
|`OpenStdin`|布林|如果標準輸入串流已開啟，會顯示 _true_，如果標準輸入串流已關閉，會顯示 _false_。|
|`StdinOnce`|布林|如果在連接的用戶端中斷連線之後關閉標準輸入串流，會顯示 _true_，如果標準輸入串流保持開啟，會顯示 _false_。|
|`Env`|字串陣列|以鍵值配對形式顯示環境變數清單。|
|`Cmd`|字串陣列|說明傳遞給容器以在容器啟動時執行的指令及引數。|
|`Healthcheck`|物件|說明如何確認容器正確運作。請參閱 [`Healthcheck`](#registry_cli_list_imageinspect_healthcheck) 中的欄位詳細資料。|
|`ArgsEscaped`|布林|如果已跳出指令（Windows 特有），會顯示 true。|
|`Image`|字串|顯示操作員所傳遞之映像檔的名稱。|
|`Volumes`|鍵值對映|顯示已裝載至容器的磁區裝載清單。|
|`WorkingDir`|字串|顯示執行所指定指令之容器內的工作目錄。|
|`Entrypoint`|字串陣列|說明容器啟動時所執行的指令。|
|`NetworkDisabled`|布林|如果已停用容器的網路，會顯示 _true_，如果已啟用容器的網路，會顯示 _false_。|
|`MacAddress`|字串|顯示指派給容器的 MAC 位址。|
|`OnBuild`|字串陣列|顯示已在映像檔 Dockerfile 上定義的 `ONBUILD` meta 資料。|
|`Labels`|鍵值對映|以鍵值配對形式顯示新增至映像檔的標籤清單。|
|`StopSignal`|字串|說明停止容器時所傳送的 UNIX 停止信號。|
|`StopTimeout`|整數|顯示停止容器的逾時（以秒為單位）。|
|`Shell`|字串陣列|顯示 Shell 形式的 RUN、CMD、ENTRYPOINT。|
{: caption="表 3. <code>Config</code> 中的可用欄位及資料類型。" caption-side="top"}

### `Healthcheck`
{: #registry_cli_list_imageinspect_healthcheck}

|欄位|類型|說明|
|-----|----|-----------|
|`Test`|字串陣列|顯示如何執行性能檢查測試。可用的選項包含：<ul><li>`{}`：繼承性能檢查</li><li>`{"NONE"}`：已停用性能檢查</li><li>`{"CMD", args...}`：直接執行引數</li><li>`{"CMD-SHELL", command}`：使用系統預設 Shell 來執行指令</li></ul>|
|`Interval`|整數（64 位元）|顯示在兩次性能檢查之間等待的時間（以十億分之一秒為單位）。|
|`Timeout`|整數（64 位元）|顯示將性能檢查視為失敗之前等待的時間（以十億分之一秒為單位）。|
|`Retries`|整數|顯示將容器視為未正確運作所需的連續失敗次數。|
{: caption="表 4. <code>Healthcheck</code> 結構中的可用欄位及資料類型。" caption-side="top"}

### `RootFS`
{: #registry_cli_list_imageinspect_rootfs}

|選項|類型|說明|
|------|----|-----------|
|`Type`|字串|顯示檔案系統的類型。|
|`Layers`|字串陣列|顯示每一個映像檔層的描述子。|
|`BaseLayer`|字串|顯示映像檔中基礎層的描述子。|
{: caption="表 5. <code>RootFS</code> 結構中的可用欄位及資料類型。" caption-side="top"}

## `ibmcloud cr token-list` 指令中的 Go 範本選項及資料類型
{: #registry_cli_list_tokenlist}

檢閱下表，以尋找 `ibmcloud cr token-list` 指令的可用 Go 範本選項及資料類型。
{:shortdesc}

|欄位|類型|說明|
|-----|----|-----------|
|`ID`|字串|顯示記號的唯一 ID。|
|`Expiry`|整數（64 位元）|顯示記號到期時的 [UNIX 時間戳記 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/Unix_time)。|
|`ReadOnly`|布林|當您只可以取回映像檔時會顯示 _true_，當您可以將映像檔推送至名稱空間以及從中取回映像檔時會顯示 _false_。|
|`Description`|字串|顯示記號的說明。|
{: caption="表 6. <code>ibmcloud cr token-list</code> 指令中的可用欄位及資料類型。" caption-side="top"}
