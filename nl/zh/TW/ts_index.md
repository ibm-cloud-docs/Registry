---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-07"

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

以下是使用 {{site.data.keyword.registrylong}} 的一般疑難排解問題的答案。
{:shortdesc}


## 取得 {{site.data.keyword.registrylong_notm}} 的協助及支援
{: #gettinghelp}

如果您在使用 {{site.data.keyword.registrylong_notm}} 時有問題或疑問，可以搜尋資訊或透過討論區提問來取得協助。您也可以開立 {{site.data.keyword.IBM_notm}} 支援問題單。

使用討論區提問時，請標記您的問題，讓 {{site.data.keyword.registrylong_notm}} 開發團隊能看到它。

-   如果您在使用 {{site.data.keyword.registrylong_notm}} 開發或部署應用程式時有技術方面的問題，請將問題張貼在 [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix)，並使用 `ibm-bluemix` 及 `container-registry` 來標記問題。
-   若為服務及開始使用指示的相關問題，請使用 [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) 討論區。請包括 `bluemix` 及 `container-registry` 標籤。

如需有關使用討論區的詳細資料，請參閱[使用支援中心](/docs/get-support/howtogetsupport.html#using-avatar)。

如需開立 {{site.data.keyword.IBM_notm}} 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[如何取得所需的支援？](/docs/get-support/howtogetsupport.html#getting-customer-support)。

## 登入 {{site.data.keyword.registrylong_notm}} 失敗
{: #ts_login}

您無法登入 {{site.data.keyword.registrylong_notm}}。

{: tsSymptoms}
`ibmcloud cr login` 指令失敗。

{: tsCauses}
-   container-registry 外掛程式已過期，需要更新。
-   Docker 未安裝在您的本端電腦上，或是不在執行中。
-   您的 {{site.data.keyword.Bluemix_notm}} 登入認證已過期。

{: tsResolve}
您可以使用下列方式修正此問題：

-   升級至最新版的 container-registry 外掛程式，請參閱[更新 container-registry 外掛程式](registry_setup_cli_namespace.html#registry_cli_update)。
-   確定 Docker 已安裝在您的電腦上。如果已安裝，請重新啟動 Docker 常駐程式。
-   重新執行 `ibmcloud login` 指令，以重新整理您的 {{site.data.keyword.Bluemix_notm}} 登入認證。
  
## 對 {{site.data.keyword.registrylong_notm}} 執行任何指令失敗，並顯示 `FAILED You are not logged in to IBM Cloud`。 
{: #ts_login_cloud}

您無法在 {{site.data.keyword.registrylong_notm}} 中執行任何指令，即使您已登入 {{site.data.keyword.Bluemix_notm}}。

{: tsSymptoms}
所有 `ibmcloud cr` 指令都失敗。

{: tsCauses}
-   container-registry 外掛程式已過期，需要更新。

{: tsResolve}
您可以使用下列方式修正此問題：

-   升級至最新版的 container-registry 外掛程式，請參閱[更新 container-registry 外掛程式](registry_setup_cli_namespace.html#registry_cli_update)。



## {{site.data.keyword.registrylong_notm}} 指令失敗，並傳回 `'cr' is not a registered command. See 'ibmcloud help'. `
{: #ts_login_error}

您無法執行 `ibmcloud cr` 指令，因為 `cr` 不是已登錄的 `ibmcloud` 指令。

{: tsSymptoms}
您看到類似於下列其中一則錯誤訊息的錯誤訊息：

```
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

{: tsCauses}
-   未安裝 container-registry 外掛程式。


{: tsResolve}
您可以使用下列方式修正此問題：

-   安裝 container-registry 外掛程式，請參閱[安裝 {{site.data.keyword.registryshort_notm}} CLI（container-registry 外掛程式）](registry_setup_cli_namespace.html#registry_cli_install)。


## 設定名稱空間失敗
{: #ts_problem}

{: tsSymptoms}
當您執行 `ibmcloud cr namespace-add` 時，無法將所輸入的值設定為名稱空間。

{: tsCauses}
-   您輸入的名稱空間值已由另一個 {{site.data.keyword.Bluemix_notm}} 組織使用中。
-   最近已刪除名稱空間，而您要重複使用其名稱。如果已刪除的名稱空間包含許多資源，則 {{site.data.keyword.registrylong_notm}} 可能尚未完全處理這項刪除作業。
-   您在名稱空間值中使用了無效字元。

{: tsResolve}
您可以使用下列方式修正此問題：

-   遵循所傳回錯誤訊息中出現的任何指示。
-   確認您已輸入有效的名稱空間：
    -   名稱空間的長度必須是 4 - 30 個字元。
    -   名稱空間的開頭必須至少使用一個字母或數字。
    -   名稱空間只能包含小寫字母、數字或底線 (_)。
-   為名稱空間選擇不同的值。
-   如果您要重建已刪除的名稱空間，而且它包含許多映像檔，請稍後再試一次。


## 推送或取回 Docker 映像檔失敗
{: #ts_pushpull}

{: tsSymptoms}
當您執行指令以推送或取回 Docker 映像檔時，收到一則錯誤訊息。錯誤訊息取決於主要原因而有所不同。潛在的錯誤訊息可能是：

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

-   [確定 Docker 已安裝在您的電腦上](index.html#registry_cli_install)。
-   檢查 Docker 安裝路徑。
-   執行 `ibmcloud login`，以登入 {{site.data.keyword.Bluemix_notm}}。然後，執行 `ibmcloud cr login`，以登入 {{site.data.keyword.registrylong_notm}} CLI。
-   [檢閱在 {{site.data.keyword.registrylong_notm}} 中儲存及取回 Docker 映像檔的配額限制及用量](registry_quota.html#registry_quota_get)。


## 無法使用 `latest` 標籤取回最近的映像檔
{: #ts_docker_latest}

{: tsSymptoms}
您嘗試執行指令 `docker pull`，但傳回不是所建置最近版本的映像檔版本。

{: tsCauses}
依預設，會套用 `latest` 標籤，以在未指定標籤值的情況下執行 Docker 指令時參照映像檔。`latest` 標籤會套用至在未明確設定標籤值的情況下執行的最近 `docker build` 或 `docker tag` 指令。因此，有可能會不正常地執行 `docker` 指令，或明確地設定部分映像檔的標籤，以及設定 `latest` 標籤來參照非最新的建置。

{: tsResolve}
一般最好每次都明確地為映像檔定義不同的循序標籤，而不要依賴 `latest` 標籤。


## 無法將其他 IBM 映像檔新增至登錄
{: #ts_ppa}


{: tsSymptoms}
當您嘗試匯入您在其他 IBM 產品（例如 {{site.data.keyword.Bluemix_notm}} Private）中所使用的內容時，您無法將來自 [IBM Passport Advantage ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/software/passportadvantage/index.html) 的映像檔及其他授權軟體儲存在登錄中。

{: tsCauses}
軟體套件（例如來自 IBM Passport Advantage 的映像檔及 Helm 圖表）必須使用 `ibmcloud cr ppa-archive-load` 指令匯入至登錄中。

{: tsResolve}
開始之前：
* 執行 `ibmcloud login [--sso]`，以登入 {{site.data.keyword.Bluemix_notm}}。
* 執行 `ibmcloud cr login`，以登入 {{site.data.keyword.registrylong_notm}}。
* [將 `kubectl` CLI 的目標](/docs/containers/cs_cli_install.html#cs_cli_configure)設為叢集。
* 如果您尚未在叢集中設定 Helm，請[立即在叢集中設定 Helm](/docs/containers/cs_integrations.html#helm)。
* 如果您要在組織內共用圖表，可以安裝 [Chart Museum 開放程式碼專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum)。如需指示，請參閱此 [developerWorks 秘訣 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/)。


### 匯入 IBM Passport Advantage 產品，以用於 {{site.data.keyword.Bluemix_notm}}

1.  從 [IBM Passport Advantage![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/software/passportadvantage/index.html) 取得您要匯入的壓縮檔。

2.  將目標設為您要使用的地區。如果您不知道地區名稱，請執行不含地區的指令，然後選擇地區。

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

3.  匯入壓縮保存檔。指定壓縮檔的路徑，以及您要將映像檔推送至其中的登錄名稱空間。

    ```
    ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
    ```
    {: pre}

    這個指令會展開壓縮檔、將任何包含的映像檔載入至本端 Docker 用戶端，然後將映像檔推送至登錄中的名稱空間。
    
    如果您要將 Helm 圖表從 IBM Passport Advantage 保存檔上傳至 Chart Museum，請在指令中包括下列選項：`ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **輸出範例**
    
    ```
    user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

    OK
    ```
    {: screen}

4.  如果壓縮檔包含 Helm 圖表，這些圖表會放在您現行工作目錄中建立的保存目錄，稱為 `ppa-import`。開啟目錄以取得 Helm 圖表 `<helm_chart>` 的名稱，然後檢查其值。

    ```
    helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    如果您已在前一個步驟中將圖表上傳至 Chart Museum，則可以使用 `helm inspect` 在 Chart Museum 中檢查圖表。
    {: tip}

5.  根據 `helm inspect values` 指令輸出的值，配置 Helm 圖表 `<helm_chart>`。

6.  使用 `helm install` 指令來部署 Helm 圖表 `<helm_chart>`。您可以使用 `--set` 選項，視需要置換圖表中的值。

    ```
    helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## 使用自訂防火牆存取登錄失敗
{: #ts_firewall}

{: tsSymptoms}
您在開發環境中設定了額外的防火牆，並針對入埠和出埠網路資料流量使用自訂設定。嘗試存取 {{site.data.keyword.registrylong_notm}} 時，連線失敗。

{: tsCauses}
您的自訂防火牆需要針對入埠及出埠網路資料流量開啟特定的網路群組，才能容許與登錄之間的通訊。

{: tsResolve}
請在您的自訂防火牆中，開啟下列網路群組。

1.  記下您要用來連接至 {{site.data.keyword.registrylong_notm}} 之電腦的公用 IP 位址。如果使用 Kubernetes，請使用您的工作者節點的公用 IP 位址。請執行 `ibmcloud ks workers <cluster_name_or_id>`，以擷取工作者節點的公用 IP 位址，其中 *&lt;cluster_name_or_id&gt;* 是您的叢集名稱或 ID。
2.  在您的防火牆中，容許下列連線進出您的電腦：
    -   針對電腦的「入埠」連線功能，容許從下列來源網路群組到您電腦之目的地公用 IP 位址的送入網路資料流量。

        `registry.bluemix.net`：

        ```
        169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

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

    -   針對電腦的「出埠」連線功能，使用相同的網路群組並容許從您電腦之來源公用 IP 位址到這些網路群組的送出網路資料流量。


## 回復遺失或洩漏的金鑰
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
使用[受信任內容](registry_trusted_content.html)時，您無法再管理受信任的映像檔，因為您的簽署金鑰已遺失或洩漏。

{: tsCauses}
您的儲存庫或主要金鑰已遺失或洩漏。

{: tsResolve}
您用來回復遺失或受影響金鑰的選項，取決於金鑰的類型 - 儲存庫金鑰或主要金鑰：

*  若為[儲存庫金鑰](#trustedcontent_lostrepokey)，您可以為儲存庫產生一組新的簽署金鑰。
*  若為[主要金鑰](#trustedcontent_lostrootkey)，您可以要求刪除儲存庫，並建立一個新的儲存庫。


### 儲存庫金鑰
{: #trustedcontent_lostrepokey}

如果儲存庫金鑰遺失或洩漏，請為儲存庫產生一組新的簽署金鑰。
{:shortdesc}

您唯一可以輪替的簽署角色是 `targets`，這是儲存庫管理者。如果其他角色受到影響，請為那些角色產生新的金鑰、移除舊的金鑰，並將新的金鑰新增為簽章者。
{:tip}

開始之前，請擷取您在第一次[推送已簽署的映像檔](registry_trusted_content.html#trustedcontent_push)時所建立的主要金鑰通行詞組。

1.  安裝 [Notary 專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli) 的 CLI 版本。

2.  [設定受信任內容環境](registry_trusted_content.html#trustedcontent_setup)。

3.  記下前一個步驟中，匯出指令的 URL。例如，`https://registry.ng.bluemix.net:4443`。

4.  產生登錄記號。

    ```
    ibmcloud cr token-add --readwrite
    ```
    {: pre}

5.	替換您的金鑰，讓使用那些金鑰所簽署的內容不再受到信任。將 _&lt;URL&gt;_ 取代為您在步驟 2 中記下的匯出指令 URL，並將 _&lt;image&gt;_ 取代為儲存庫金鑰受到影響的映像檔。

    ```
notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	系統提示時，請輸入主要金鑰通行詞組。然後，在系統提示時，輸入新的儲存庫金鑰的新主要金鑰通行詞組。

7.	[推送使用新簽署金鑰的已簽署映像檔](registry_trusted_content.html#trustedcontent_push)。


### 主要金鑰
{: #trustedcontent_lostrootkey}

如果您的主要金鑰遺失或洩漏，則無法更新使用該主要金鑰的任何受信任內容儲存庫。
{:shortdesc}

您可以[刪除具有使用受影響主要金鑰之儲存庫的名稱空間](registry_setup_cli_namespace.html#registry_remove)，這樣會刪除您的映像檔及信任資料。

如果名稱空間包含的儲存庫具有不受影響的主要金鑰（例如正式作業映像檔的名稱空間），則建議您只刪除與受影響之主要金鑰相關聯的信任資料。開立支援問題單。

1.  [與 {{site.data.keyword.Bluemix_notm}} 支援中心聯絡](/docs/get-support/howtogetsupport.html#getting-customer-support)。請包含問題的簡要說明、帳戶 ID，以及包含具有受影響主要金鑰之映像檔儲存庫的名稱空間清單。

2.  在 {{site.data.keyword.Bluemix_notm}} 處理該問題後，刪除本端電腦上的 Docker Content Trust 儲存庫。

    * Linux 及 Mac 目錄：`~/.docker/trust/private` 及 `~/.docker/trust/tuf`

    * Windows 目錄：`%HOMEPATH%\.docker\trust\private` 及 `%HOMEPATH%\.docker\trust\tuf`

    因為主要金鑰受到影響，所以此步驟會刪除所有簽署金鑰，包括其他信任伺服器的簽署金鑰。
    {:tip}

3.  如果您在 {{site.data.keyword.containershort_notm}} 叢集中使用 [{{site.data.keyword.Bluemix_notm}} Image Enforcement](registry_security_enforce.html)，請重新啟動每一個映像檔強制執行 Pod。若要觸發 Kubernetes 以自動執行 Pod 的漸進式重新啟動，您可以變更 Pod 上的部分 meta 資料。例如，[將您的 Kubernetes CLI 目標設為叢集](/docs/containers/cs_cli_install.html#cs_cli_configure)，並修改部署。
    

    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  產生受信任內容儲存庫。

    *  如果您要建立新的受信任內容，請[推送新的已簽署映像檔](registry_trusted_content.html#trustedcontent_push)。

    *  如果您不想要變更先前的受信任內容，請將簽章新增至登錄中的最近映像檔。

       ```
       docker trust sign <image>:<tag>
       ```
       {: pre}
       

## Container Image Security Enforcement 的安裝失敗，並顯示 `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists`
{: #ts_install_cise_fail}

{: tsSymptoms}
您的 Container Image Security Enforcement 安裝失敗，且您收到下列訊息：

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
前一個安裝失敗，且後續的解除安裝並未移除與安裝相關聯的所有 Kubernetes 工作。

{: tsResolve}
執行下列指令，以移除剩餘的 Kubernetes 工作：

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}


## 所有工作者節點都關閉之後，Pod 不會重新啟動
{: #ts_pods}


{: tsSymptoms}
所有叢集工作者節點都關閉之後，Pod 不會重新啟動。已部署 Container Image Security Enforcement。叢集工作者節點顯示為性能健全，但未排定任何項目。

{: tsCauses}
依預設，Container Image Security Enforcement 會新增失敗關閉許可 Webhook。如果所有 Container Image Security Enforcement Pod 都關閉，Pod 便無法核准自己的回復。

{: tsResolve}
若要回復處於此狀態的叢集，您必須變更 Webhook 配置，使它成為失敗開啟而不是關閉。 

您必須有足夠的角色型存取控制 (RBAC) 專用權，才能使用下列動詞：
*  `GET`
*  `PATCH`

於這些資源：
*  `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
*  `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration` 

如需 RBAC 的相關資訊，請參閱[授權具有自訂 Kubernetes RBAC 角色的使用者](/docs/containers/cs_users.html#rbac)及 [Kubernetes：使用 RBAC 授權 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)。

請完成下列步驟來變更 Webhook 配置，以讓開啟失敗，而非關閉，然後，至少一個 Container Image Security Enforcement Pod 正在執行時，請還原 Webhook 配置，以讓關閉失敗：

1.  執行下列指令，以更新 `MutatingWebhookConfiguration`：

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    將 `failurePolicy` 變更為 `Ignore`、儲存並關閉。

2.  執行下列指令，以更新 `ValidatingWebhookConfiguration`：

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    將 `failurePolicy` 變更為 `Ignore`、儲存並關閉。

3.  等待啟動一些 Container Image Security Enforcement Pod。您可以檢查是否已執行下列指令來啟動 Pod，直到您看到至少一個 Pod 的 **STATUS** 直欄顯示 `Running`：

    ```
    kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
    ```
    {: pre}

4.  至少一個 Container Image Security Enforcement Pod 正在執行時，請執行下列指令來更新 `MutatingWebhookConfiguration`：

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    將 `failurePolicy` 變更為 `Fail`、儲存並關閉。

5.  執行下列指令，以更新 `ValidatingWebhookConfiguration`：

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    將 `failurePolicy` 變更為 `Fail`、儲存並關閉。
