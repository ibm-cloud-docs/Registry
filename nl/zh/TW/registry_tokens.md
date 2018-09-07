---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 自動化 {{site.data.keyword.registrylong_notm}} 的存取
{: #registry_access}

您可以使用登錄記號或 {{site.data.keyword.iamlong}} (IAM) API 金鑰來自動化 {{site.data.keyword.registrylong_notm}} 名稱空間的存取，以推送及取回映像檔。
{:shortdesc}

您嘗試在 Kubernetes 部署中使用您的登錄映像檔嗎？請參閱[存取其他 Kubernetes 名稱空間、{{site.data.keyword.Bluemix_notm}} 地區及帳戶中的映像檔](/docs/containers/cs_images.html#other)。
{: tip}

API 金鑰與您的帳戶鏈結，可跨 {{site.data.keyword.Bluemix_notm}} 使用，因此您不需要為每一個服務提供不同的認證。您可以在 CLI 中使用 API 金鑰，也可以在自動化程序當中使用，以您的使用者身分登入。

登錄記號的範圍僅限於 {{site.data.keyword.registrylong_notm}}。您可以將其限制為唯讀存取，也可以選擇它們是否會到期。

如需 {{site.data.keyword.registrylong_notm}} API 金鑰的相關資訊，請參閱[使用 API 金鑰](/docs/iam/apikeys.html#manapikey)。

開始之前，請[安裝 {{site.data.keyword.registrylong_notm}} 及 Docker CLI](registry_setup_cli_namespace.html#registry_cli_install)。


## 使用 API 金鑰自動化名稱空間的存取
{: #registry_api_key}

您可以使用 API 金鑰，以自動化將 Docker 映像檔推送至名稱空間以及從其中取回 Docker 映像檔的作業。
{:shortdesc}

### 建立 API 金鑰
{: #registry_api_key_create}

您可以建立 API 金鑰，之後就可以用來登入您的登錄。
{:shortdesc}

若要建立 IAM API 金鑰，請參閱[建立 API 金鑰](/docs/iam/userid_keys.html#creating-an-api-key)。

### 使用 API 金鑰以自動化存取
{: #registry_api_key_use}

您可以使用 API 金鑰，以自動化 {{site.data.keyword.registrylong_notm}} 名稱空間的存取。
{:shortdesc}

請執行下列 Docker 指令，以使用 API 金鑰登入您的登錄。將 &lt;your_apikey&gt; 取代為您的 API 金鑰，並將 &lt;registry_url&gt; 取代為已設定名稱空間之登錄的 URL。

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

如需指令的相關參考資訊，請參閱[建立新的 {{site.data.keyword.Bluemix_notm}} 平台 API 金鑰](/docs/cli/reference/ibmcloud/cli_api_policy.html#ibmcloud_iam_api_key_create)。


## 使用記號自動化名稱空間的存取
{: #registry_tokens}

您可以使用記號，以自動化將 Docker 映像檔推送至 {{site.data.keyword.registrylong_notm}} 名稱空間以及從其中取回 Docker 映像檔的作業。
{:shortdesc}

擁有登錄記號的每個人都可以存取受保護的資訊。建立 {{site.data.keyword.Bluemix_notm}} 帳戶的記號，即可將地區中設定之所有名稱空間的存取權，授與給 {{site.data.keyword.Bluemix_notm}} 帳戶之外的使用者。每個擁有此記號的使用者或應用程式都可以將映像檔推送至名稱空間以及從中取回映像檔，而不需要安裝 container-registry 外掛程式。

建立 {{site.data.keyword.Bluemix_notm}} 帳戶的記號時，您可以決定該記號是要授權登錄的唯讀（取回）還是寫入權（推送及取回）。您也可以指定記號是永久性的，還是在 24 小時之後到期。您可以建立及使用多個記號來控制不同類型的存取權。

請使用下列作業來管理記號：

-  [建立 {{site.data.keyword.Bluemix_notm}} 帳戶的記號](#registry_tokens_create)
-  [使用記號自動化名稱空間的存取](#registry_tokens_use)
-  [從 {{site.data.keyword.Bluemix_notm}} 帳戶中移除記號](#registry_tokens_remove)


### 建立 {{site.data.keyword.Bluemix_notm}} 帳戶的記號
{: #registry_tokens_create}

您可以建立記號，來授與對地區中所有 {{site.data.keyword.registrylong_notm}} 名稱空間的存取權。
{:shortdesc}

1.  建立記號。下列範例會建立不會到期的記號，它具有對地區中已設定之所有名稱空間的讀寫權。

    ```
    ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="電燈泡圖示"/> 瞭解這個指令的元件</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>選用項目。使用此選項來說明記號，以便您之後可以更輕鬆地識別它。</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>選用項目。使用此選項來建立不會到期的記號。如果您未指定此選項，則記號會在 24 小時之後失效。<br> **提示：**當您不再需要不會到期的記號來封鎖名稱空間存取時，請記得移除記號。</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>選用項目。使用此選項來建立記號，以容許使用者將映像檔推送至名稱空間以及從中取回映像檔。如果您未指定此選項，則記號只能用來取回映像檔。</td>
        </tr>
        </tbody>
        </table>

    CLI 輸出與下列輸出類似：

    ```
Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
    Token              <token_value>
    ```
    {: screen}

2.  驗證已建立記號。

    ```
    ibmcloud cr token-list
    ```
    {: pre}


### 使用記號自動化名稱空間的存取
{: #registry_tokens_use}

您可以在 `docker login` 指令中使用記號，以自動化 {{site.data.keyword.registrylong_notm}} 名稱空間的存取。取決於您設定記號的唯讀權還是讀寫權，使用者可以將映像檔推送至名稱空間以及從中取回映像檔。
{:shortdesc}

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2.  列出 {{site.data.keyword.Bluemix_notm}} 帳戶中的所有記號，並記下您要使用的記號 ID。

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  擷取記號的記號值。將 &lt;token_id&gt; 取代為記號的 ID。

    ```
    ibmcloud cr token-get <token_id>
    ```
    {: pre}

    您的記號值即會顯示在 CLI 輸出的**記號**中。

4.  在 `docker login` 指令中使用記號。將 &lt;token_value&gt; 取代為您在上一步所擷取的記號值，並將 &lt;registry_url&gt; 取代為已設定名稱空間之登錄的 URL。

    -   針對美國南部中所設定的名稱空間：`registry.ng.bluemix.net`
    -   針對英國南部中所設定的名稱空間：`registry.eu-gb.bluemix.net`
    -   針對歐盟中部中所設定的名稱空間：`registry.eu-de.bluemix.net`
    -   針對亞太地區南部中所設定的名稱空間：`registry.au-syd.bluemix.net`

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}
    
    針對 `-u` 參數，確定您鍵入字串 `token`，而非記號 ID。
    {: tip}

    在使用記號登入 Docker 之後，您可以將映像檔推送至名稱空間或從中取回映像檔。


### 從 {{site.data.keyword.Bluemix_notm}} 帳戶中移除記號
{: #registry_tokens_remove}

當您不再需要 {{site.data.keyword.registrylong_notm}} 記號時，請將它移除。
{:shortdesc}

會自動從 {{site.data.keyword.Bluemix_notm}} 帳戶中移除到期的 {{site.data.keyword.registrylong_notm}} 記號，不需要手動移除。
{:tip}

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2.  列出 {{site.data.keyword.Bluemix_notm}} 帳戶中的所有記號，並記下您要移除的記號 ID。

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  移除記號。

    ```
    ibmcloud cr token-rm <token_id>
    ```
    {: pre}
