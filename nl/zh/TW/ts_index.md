---

copyright:
  years: 2017
lastupdated: "2017-10-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# 疑難排解
{: #ts_index}

以下是使用 {{site.data.keyword.registrylong}} 的一般疑難排解問題的回答。
{:shortdesc}


## 取得 {{site.data.keyword.registrylong_notm}} 的協助及支援
{: #gettinghelp}

如果您在使用 {{site.data.keyword.registrylong_notm}} 時發生問題或有疑問，可以搜尋資訊或透過討論區提問來取得協助。您也可以開立 {{site.data.keyword.IBM_notm}} 支援問題單。

當您要使用討論區提問時，請標記問題，讓 {{site.data.keyword.registrylong_notm}} 開發團隊可以看到它。

-   如果您有關於使用 {{site.data.keyword.registrylong_notm}} 開發或部署應用程式的技術問題，請將問題張貼到 [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix)，並使用 `ibm-bluemix` 及 `container-registry` 來標記問題。
-   若是服務及開始使用指示的相關問題，請使用 [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) 討論區。請包含 `bluemix` 及 `container-registry` 標籤。

如需使用討論區的詳細資料，請參閱[取得協助](../../support/index.html#getting-help)。

如需開立 {{site.data.keyword.IBM_notm}} 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[與支援中心聯絡](../../support/index.html#contacting-support)。

## 登入 {{site.data.keyword.registrylong_notm}} 失敗
{: #ts_login}

您無法登入 {{site.data.keyword.registrylong_notm}}。

{: tsSymptoms}
`bx cr login` 指令失敗。

{: tsCauses}
-   container-registry 外掛程式過舊，需要更新。
-   Docker 未安裝在您的本端機器上，或是不在執行中。
-   您的 {{site.data.keyword.Bluemix_notm}} 登入認證已過期。

{: tsResolve}
您可以使用下列方式修正此問題：

-   升級至最新版的 {{site.data.keyword.registryshort_notm}} 外掛程式，請參閱[更新 {{site.data.keyword.registrylong_notm}} (`bx cr`) 外掛程式](registry_setup_cli_namespace.html#registry_cli_update)。
-   確定 Docker 已安裝在您的機器上。如果已安裝，請重新啟動 Docker 常駐程式。
-   重新執行 `bx login` 指令，以重新整理您的 {{site.data.keyword.Bluemix_notm}} 登入認證。


## {{site.data.keyword.registrylong_notm}} 指令失敗，並傳回 `'cr' is not a registered command. See 'bx help'. `
{: #ts_login_error}

您無法執行 `bx cr` 指令，因為 `cr` 不是已登錄的 `bx` 指令。

{: tsSymptoms}
您看到類似於下列其中一則錯誤訊息的錯誤訊息： 

```
bx cr login 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

```
bx cr namespace 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

{: tsCauses}
-   未安裝 container-registry 外掛程式。


{: tsResolve}
您可以使用下列方式修正此問題：

-   安裝 container-registry 外掛程式，請參閱[安裝 {{site.data.keyword.registryshort_notm}} CLI (bx cr) 外掛程式](registry_setup_cli_namespace.html#registry_cli_install)。


## 設定名稱空間失敗
{: #ts_problem}

{: tsSymptoms}
當您執行 `bx cr namespace-add` 時，無法將所輸入的值設定為名稱空間。

{: tsCauses}
-   您已輸入另一個 {{site.data.keyword.Bluemix_notm}} 組織已在使用的名稱空間值。
-   最近已刪除名稱空間，而您要使用其名稱。如果已刪除的名稱空間包含許多資源，則 {{site.data.keyword.registrylong_notm}} 可能尚未完整處理這項刪除。
-   您已在名稱空間值中使用無效字元。

{: tsResolve}
您可以使用下列方式修正此問題：

-   遵循所傳回錯誤訊息中出現的任何指示。
-   檢查您已輸入有效的名稱空間：
    -   名稱空間的長度必須是 4 - 30 個字元。
    -   名稱空間的開頭必須至少使用一個字母或數字。
    -   名稱空間只能包含小寫字母、數字或底線 (_)。
-   為名稱空間選擇不同的值。
-   如果您要重建已刪除的名稱空間，而且它包含許多映像檔，請稍後再試一次。

## 推送或取回 Docker 映像檔失敗
{: #ts_pushpull}

{: tsSymptoms}
當您執行指令以推送或取回 Docker 映像檔時，會收到一則錯誤訊息。錯誤訊息會根據主要原因而不同。潛在的錯誤訊息可能是：

```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan
```
{: screen}

```
You have exceeded your pull traffic quota for the current month. Review your pull traffic quota and pricing plan
```
{: screen}

```
unauthorized: authentication required
```
{: screen}

```
denied: requested access to the resource is denied
```
{: screen}

{: tsCauses}
-   未安裝 Docker。
-   Docker 用戶端未登入 {{site.data.keyword.registrylong_notm}}。
-   您的 {{site.data.keyword.Bluemix_notm}} 存取記號可能已過期。
-   您已超出針對 {{site.data.keyword.Bluemix_notm}} 帳戶所設定的儲存空間或取回資料流量的配額限制。

{: tsResolve}
您可以使用下列方式修正此問題：

-   [確定已在機器上安裝 Docker](index.html#registry_cli_install)。
-   檢查 Docker 安裝路徑。
-   執行 `bx login`，以登入 {{site.data.keyword.Bluemix_notm}}。然後，執行 `bx cr login`，以登入 {{site.data.keyword.registrylong_notm}} CLI。
-   [檢閱在 {{site.data.keyword.registrylong_notm}} 中儲存及取回 Docker 映像檔的配額限制及用量](registry_quota.html#registry_quota_get)。

## 無法使用 latest 標籤取回最新映像檔
{: #ts_docker_latest}

{: tsSymptoms}
您正在嘗試執行指令 `docker pull`，但傳回不是所建置最新版本的映像檔版本。

{: tsCauses}
依預設，會套用 `latest` 標籤，以在未指定標籤值的情況下執行 Docker 指令時參照映像檔。`latest` 標籤會套用至在未明確設定標籤值的情況下執行的最新 `docker build` 或 `docker tag` 指令。因此，可能會不正常地執行 `docker` 指令，或明確地設定部分映像檔的標籤，以及 `latest` 標籤來參照不是最新的建置。

{: tsResolve}
一般最好每次都明確地定義映像檔的不同循序標籤，而且不要依賴 `latest` 標籤。

## 使用自訂防火牆存取登錄失敗
{: #ts_firewall}

{: tsSymptoms}
您在開發環境中設定了額外的防火牆，針對入埠和出埠網路資料流量使用自訂設定。嘗試存取 {{site.data.keyword.registrylong_notm}} 時，連線失敗。

{: tsCauses}
您的自訂防火牆需要針對入埠及出埠網路資料流量開啟特定的網路群組，才能容許與登錄之間的通訊。

{: tsResolve}
請在您的自訂防火牆中開啟下列網路群組。

1.  記下您要用來連接 {{site.data.keyword.registrylong_notm}} 之機器的公用 IP 位址。如果使用 Kubernetes，請使用您的工作者節點的公用 IP 位址。請執行 `bx cs workers <cluster_name_or_id>`，擷取工作者節點的公用 IP 位址，其中 *&lt;cluster_name_or_id&gt;* 是您的叢集名稱或 ID。
2.  在您的防火牆中，容許進出您機器的下列連線：
    -   針對機器的「入埠」連線功能，容許從下列來源網路群組到您機器之目的地公用 IP 位址的送入網路資料流量。

        `registry.au-syd.bluemix.net`：

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`：

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`：

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`：

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   針對機器的「出埠」連線功能，使用相同的網路群組並容許從您機器之來源公用 IP 位址到這些網路群組的送出網路資料流量。

