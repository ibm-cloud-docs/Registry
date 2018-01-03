---

copyright:
  years: 2017
lastupdated: "2017-11-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 管理名稱空間中 Docker 映像檔的 {{site.data.keyword.registrylong_notm}} (`bx cr`) 指令
{: #registry_cli_reference}

您可以使用 container-registry 外掛程式，在 IBM 所管理專用登錄中設定自己的映像檔名稱空間，而在此專用登錄中，您可以安全地儲存 Docker 映像檔，並將其與 {{site.data.keyword.Bluemix}} 帳戶中的所有使用者共用。
{:shortdesc}


## bx cr 指令
{: #registry_cli_reference_bxcr}

在 {{site.data.keyword.registryshort_notm}} CLI 中執行 `bx cr` 指令。{:shortdesc}

如需支援的指令，請參閱 [{{site.data.keyword.registrylong_notm}} CLI](../../cli/plugins/registry/index.html#containerregcli)。

## 格式化及過濾 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出
{: #registry_cli_listing}

您可以格式化及過濾所支援 {{site.data.keyword.registrylong_notm}} 指令的 CLI 輸出。
{:shortdesc}

依預設，會以人類可讀格式顯示 CLI 輸出。不過，此視圖可能會限制您使用輸出的能力，特別是以程式設計方式執行指令時。例如，在 `bx cr image-list` CLI 輸出中，您可能要依數值大小排序 `Size` 欄位，但指令傳回大小的字串說明。container-registry 外掛程式提供 format 選項，可用來將 Go 範本套用至 CLI 輸出。Go 範本是 [Go 程式設計語言](https://golang.org/pkg/text/template/)的特性，可讓您自訂 CLI 輸出。

您可以使用兩種不同方式套用 format 選項，以變更 CLI 輸出：

1.  格式化 CLI 輸出中的資料。例如，將 `Created` 欄位輸出從 Unix 時間 變更為標準時間。
2.  過濾 CLI 輸出中的資料。例如，依映像檔詳細資料進行過濾，以使用 Go 範本 `if gt` 條件來顯示特定映像檔子集。

您可以搭配使用 format 選項與下列 {{site.data.keyword.registrylong_notm}} 指令。按一下指令，以檢視可用欄位及其資料類型的清單。

-   [`bx cr image-list`](registry_cli_reference.html#registry_cli_listing_imagelist)
-   [`bx cr image-inspect`](registry_cli_reference.html#registry_cli_listing_imageinspect)
-   [`bx cr token-list`](registry_cli_reference.html#registry_cli_listing_tokenlist)

下列程式碼範例示範如何使用格式化及過濾選項。

-   執行下列 `bx cr image-list` 指令，以顯示大小超過 1 MB 的所有映像檔的儲存庫、標籤及漏洞狀態：

    ```
    bx cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .Vulnerable }}{{end}}"
    ```
    {: pre}

    輸出範例：

    ```
    example-registry.<region>.bluemix.net/user1/ibmliberty:latest OK
    example-registry.<region>.bluemix.net/user1/ibmnode:1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode:test1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode2:test2 Vulnerable
    ```
    {: screen}

-   執行下列 `bx cr image-inspect` 指令，以顯示管理所指定 IBM 公用映像檔的 IBM 文件的位置：

    ```
    bx cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"

    ```
    {: pre}

    輸出範例：

    ```
    map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
    ```
    {: screen}

-   執行下列 `bx cr image-inspect` 指令，以顯示所指定映像檔的公開埠：

    ```
    bx cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"

    ```
    {: pre}

    輸出範例：

    ```
    map[9080/tcp: 9443/tcp:]
    ```
    {: screen}

-   執行下列 `bx cr token-list` 指令，以顯示所有唯讀記號：

    ```
    bx cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
    {: pre}

    輸出範例：

    ```
    0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
    ```
    {: screen}


### `bx cr image-list` 指令中的 Go 範本選項及資料類型
{: #registry_cli_listing_imagelist}

檢閱下表，以尋找 `bx cr image-list` 指令的可用 Go 範本選項及資料類型。
{:shortdesc}

|欄位|類型|說明|
|-----|----|-----------|
|`Created`|整數（64 位元）|以 [Unix 時間](https://en.wikipedia.org/wiki/Unix_time)顯示映像檔的建立時間（以秒數表示）。|
|`Digest`|字串|顯示映像檔的唯一 ID。|
|`Namespace`|字串|顯示儲存映像檔的名稱空間。|
|`Repository`|字串|顯示映像檔的儲存庫。|
|`Size`|整數（64 位元）|顯示映像檔的大小（以位元組為單位）。|
|`Tag`|字串|顯示映像檔的標籤。|
|`Vulnerable`|字串|顯示映像檔的漏洞狀態。[使用漏洞警告器管理映像檔安全](../va/va_index.html)中會說明可能的狀態。|
{: caption="表 1. bx cr image-list 指令中的可用欄位及資料類型。" caption-side="top"}

### `bx cr image-inspect` 指令中的 Go 範本選項及資料類型
{: #registry_cli_listing_imageinspect}

檢閱下表，以尋找 `bx cr image-inspect` 指令的可用 Go 範本選項及資料類型。
{:shortdesc}

|欄位|類型|說明|
|-----|----|-----------|
|`ID`|字串|顯示映像檔的唯一 ID。|
|`Parent`|字串|顯示已用來建置此映像檔的主映像檔的 ID。|
|`Comment`|字串|顯示映像檔的說明。|
|`Created`|字串|顯示建立映像檔時的 [Unix 時間戳記](https://en.wikipedia.org/wiki/Unix_time)。|
|`Container`|字串|顯示已建立映像檔的容器的 ID。|
|`ContainerConfig`|物件|顯示已從此映像檔啟動的容器的預設配置。請參閱 [Config](registry_cli_reference.html#config) 中的欄位詳細資料。|
|`DockerVersion`|字串|顯示已用來建置此映像檔的 Docker 版本。|
|`Author`|字串|顯示映像檔的作者。|
|`Config`|物件|顯示映像檔的配置 meta 資料。請參閱 [Config](registry_cli_reference.html#config) 中的欄位詳細資料。|
|`Architecture`|字串|顯示已用來建置此映像檔且為執行映像檔所需的處理器架構。|
|`Os`|字串|顯示已用來建置此映像檔且為執行映像檔所需的作業系統系列。|
|`OsVersion`|字串|顯示已用來建置此映像檔的作業系統的版本。|
|`Size`|整數（64 位元）|顯示映像檔的大小（以位元組為單位）。|
|`VirtualSize`|整數（64 位元）|顯示映像檔中每層大小的總和（以位元組為單位）。|
|`RootFS`|物件|顯示可說明映像檔的 root 檔案系統的 meta 資料。請參閱 [RootFS](registry_cli_reference.html#rootfs) 中的欄位詳細資料。|
{: caption="表 2. bx cr image-inspect 指令中的可用欄位及資料類型。" caption-side="top"}

#### Config

|欄位|類型|說明|
|-----|----|-----------|
|`Hostname`|字串|顯示容器的主機名稱。|
|`Domainname`|字串|顯示容器的完整網域名稱。|
|`User`|字串|顯示在使用映像檔的容器內執行指令的使用者。|
|`AttachStdin`|布林|如果將標準輸入串流連接至容器，會顯示 _true_，否則會顯示 _false_。|
|`AttachStdout`|布林|如果將標準輸出串流連接至容器，會顯示 _true_，否則會顯示 _false_。|
|`AttachStderr`|布林|如果將標準錯誤串流連接至容器，會顯示 _true_，否則會顯示 _false_。|
|`ExposedPorts`|鍵值對映|顯示已公開埠的清單，格式為 `[123:,456:]`。|
|`Tty`|布林|如果將 pseudo-tty 連接至容器，會顯示 _true_，否則會顯示 _false_。|
|`OpenStdin`|布林|如果開啟標準輸入串流，會顯示 _true_，如果關閉標準輸入串流，會顯示 _false_。|
|`StdinOnce`|布林|如果在連接的用戶端中斷連線之後關閉標準輸入串流，會顯示 _true_，如果標準輸入串流保持開啟，會顯示 _false_。|
|`Env`|字串陣列|顯示環境變數清單，形式為鍵值配對。|
|`Cmd`|字串陣列|說明傳遞給容器以在啟動容器時執行的指令及引數。|
|`Healthcheck`|物件|說明如何檢查容器是否健全。請參閱 [Healthcheck](registry_cli_reference.html#healthcheck) 中的欄位詳細資料。|
|`ArgsEscaped`|布林|如果已跳出指令（Windows 特有），會顯示 true。|
|`Image`|字串|顯示運算子已傳遞的映像檔的名稱。|
|`Volumes`|鍵值對映|顯示裝載至容器的磁區裝載清單。|
|`WorkingDir`|字串|顯示執行所指定指令的容器內的工作目錄。|
|`Entrypoint`|字串陣列|說明容器啟動時所執行的指令。|
|`NetworkDisabled`|布林|如果停用容器的網路，會顯示 _true_，如果啟用容器的網路，會顯示 _false_。|
|`MacAddress`|字串|顯示指派給容器的 MAC 位址。|
|`OnBuild`|字串陣列|顯示已在映像檔 Dockerfile 上定義的 ONBUILD meta 資料。|
|`Labels`|鍵值對映|顯示以鍵值配對形式新增至映像檔的標籤清單。|
|`StopSignal`|字串|說明停止容器時所傳送的 UNIX 停止信號。|
|`StopTimeout`|整數|顯示停止容器的逾時（以秒為單位）。|
|`Shell`|字串陣列|顯示 Shell 形式的 RUN、CMD、ENTRYPOINT。|
{: caption="表. " caption-side="top"}

#### Healthcheck

|欄位|類型|說明|
|-----|----|-----------|
|`Test`|字串陣列|顯示如何執行性能檢查測試。可用的選項為：<ul><li>{}：繼承性能檢查</li><li>{"NONE"}：停用性能檢查</li><li>{"CMD", args...}：直接執行引數</li><li>{"CMD-SHELL", command}：使用系統預設 Shell 來執行指令</li></ul>|
|`Interval`|整數（64 位元）|顯示在兩個性能檢查之間等待的時間（以十億分之一秒為單位）。|
|`Timeout`|整數（64 位元）|顯示將性能檢查視為失敗之前等待的時間（以十億分之一秒為單位）。|
|`Retries`|整數|顯示將容器視為性能不佳所需的連續失敗次數。|
{: caption="表 4. Healthcheck 結構中的可用欄位及資料類型。" caption-side="top"}

#### RootFS

|選項|類型|說明|
|------|----|-----------|
|`Type`|字串|顯示檔案系統的類型。|
|`Layers`|字串陣列|顯示每一個映像檔層的描述子。|
|`BaseLayer`|字串|顯示映像檔中基礎層的描述子。|
{: caption="表 5. RootFS 結構中的可用欄位及資料類型。" caption-side="top"}

### `bx cr token-list` 指令中的 Go 範本選項及資料類型
{: #registry_cli_listing_tokenlist}

檢閱下表，以尋找 `bx cr token-list` 指令的可用 Go 範本選項及資料類型。
{:shortdesc}

|欄位|類型|說明|
|-----|----|-----------|
|`ID`|字串|顯示記號的唯一 ID。|
|`Expiry`|整數（64 位元）|顯示記號過期時的 [Unix 時間戳記](https://en.wikipedia.org/wiki/Unix_time)。|
|`ReadOnly`|布林|只有在只取回映像檔時才會顯示 _true_，當您可以從名稱空間推送及取回映像檔時會顯示 _false_。|
|`Description`|字串|顯示記號的說明。|
{: caption="表 6. bx cr token-list 指令中的可用欄位及資料類型。" caption-side="top"}
