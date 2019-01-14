---

copyright:
  years: 2018
lastupdated: "2018-10-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 指導教學：授與 {{site.data.keyword.registrylong_notm}} 資源存取權
{: #iam_access}

使用本指導教學，瞭解如何配置 {{site.data.keyword.registrylong_notm}} 的 {{site.data.keyword.iamlong}} (IAM) 以授與資源存取權。
{:shortdesc}

本指導教學大約需要 45 分鐘。

**開始之前**

- 完成[開始使用 {{site.data.keyword.registrylong_notm}}](/docs/services/Registry/index.html#index) 中的指示。

- 確保您具有最新版的 {{site.data.keyword.cloud_notm}} CLI container-registry 外掛程式，請參閱[更新 container-registry 外掛程式](https://console.bluemix.net/docs/services/Registry/registry_setup_cli_namespace.html#registry_cli_update)。

- 您必須有權存取可用於本指導教學的兩個 [{{site.data.keyword.cloud_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/)：一個適用於「使用者 A」，一個適用於「使用者 B」，而且每個都必須使用唯一的電子郵件位址。您使用自己的帳戶（使用者 A）工作，並邀請另一位使用者（使用者 B）使用您的帳戶。您可以選擇建立第二個 {{site.data.keyword.cloud_notm}} 帳戶，也可以與具有 {{site.data.keyword.cloud_notm}} 帳戶的同事一起工作。

- 如果您在 2018 年 10 月 4 日之前開始在帳戶中使用 {{site.data.keyword.registrylong_notm}}，則必須執行 `ibmcloud cr iam-policies-enable` 指令來啟用 IAM 原則強制執行。如果您已邀請其他使用您 {{site.data.keyword.registrylong_notm}} 名稱空間的使用者加入您的 IBM Cloud 帳戶，則請使用與「使用者 A」不同的帳戶來防止中斷其存取。

## 步驟 1：授權使用者配置登錄
{: #configure_registry}

在本節中，您將第二位使用者新增至您的帳戶，並將配置 {{site.data.keyword.registrylong_notm}} 的能力授與他們。
{:shortdesc}

1. 將「使用者 B」新增至「使用者 A」的帳戶：

    1. 執行下列指令，以登入「使用者 A」的帳戶：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 執行下列指令，以邀請「使用者 B」存取「使用者 A」的帳戶，其中 _`<user.b@example.com>`_ 是「使用者 B」的電子郵件位址：

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. 執行下列指令，以取得「使用者 A」的「帳戶 ID」：

        ```
        ibmcloud target
        ```
        {: pre}

        記下「帳戶」列之括弧 ( ) 中的「帳戶 ID」。

2. 證明「使用者 B」可以將「使用者 A」的帳戶設為目標，但還不能使用 {{site.data.keyword.registrylong_notm}} 執行任何作業：

    1. 以「使用者 B」身分登入，並執行下列指令以將「使用者 A」的帳戶設為目標，其中 _`<YourAccountID>`_ 是「使用者 A」的「帳戶 ID」：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 執行下列指令，以嘗試將登錄限額編輯為 4 GB 的資料流量：

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        因為「使用者 B」沒有正確的存取權，所以指令失敗。

3. 將「管理員」角色授與「使用者 B」，讓「使用者 B」可以配置 {{site.data.keyword.registrylong_notm}}：

    1. 執行下列指令，以您自己的身分（使用者 A）重新登入帳戶：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 執行下列指令，建立原則以將「管理員」角色授與「使用者 B」：

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. 證明「使用者 B」現在可以變更「使用者 A」帳戶中的配額：

    1. 以「使用者 B」身分登入，並執行下列指令以將「使用者 A」的帳戶設為目標：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 執行下列指令，以嘗試將登錄限額編輯為 4 GB 的資料流量：

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        其運作原因是「使用者 B」具有正確的存取權類型。

    3. 現在，執行下列指令，以變更回配額：
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. 清除：

    1. 執行下列指令，以您自己的身分（使用者 A）重新登入帳戶：
  
        ```
    ibmcloud login
    ```
        {: pre}
  
    2. 列出「使用者 B」的原則，並執行下列指令找到您剛才建立的原則，然後記下 ID：
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. 執行下列指令，以刪除原則，其中 _`<Policy_ID>`_ 是「原則 ID」：
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## 步驟 2：授權使用者存取特定名稱空間
{: #access_resources}

在本節中，您會建立一些具有範例映像檔的名稱空間，並授與其存取權。您可以建立原則，以將不同的角色授與每個名稱空間，並顯示所具有的效果。
{:shortdesc}

1. 在「使用者 A」的帳戶中，建立三個新的名稱空間。這些名稱空間在地區中必須是唯一的，因此，請選擇您自己的名稱空間名稱，但本指導教學使用 `namespace_a`、`namespace_b` 及 `namespace_c` 作為範例：

    1. 執行下列指令，以「使用者 A」身分登入：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 執行下列指令，以建立名稱空間 `namespace_b`：

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}

        名稱空間名稱在地區中必須是唯一的。
        {: tip}

    3. 執行下列指令，以建立另一個名稱空間 `namespace_c`：

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. 證明「使用者 B」看不到任何項目：

    1. 以「使用者 B」身分登入，並執行下列指令以將「使用者 A」的帳戶設為目標：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 執行下列指令，嘗試以「使用者 B」身分列出映像檔：

        ```
    ibmcloud cr images
    ```
        {: pre}

        它會傳回空清單，因為「使用者 B」無法存取任何名稱空間。

3. 執行下列指令，建立原則以將與名稱空間互動的能力授與「使用者 B」：

    1. 執行下列指令，以「使用者 A」的帳戶身分登入：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 執行下列指令，以確認至少列出三個名稱空間：

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        顯示您在本指導教學中建立的三個名稱空間（`namespace_a`、`namespace_b` 及 `namespace_c`）。如果您沒有看到這些名稱空間，請返回並遵循指示再次建立它們。

    3. 執行下列指令，建立原則以將 `namespace_b` 的「讀者」角色授與「使用者 B」，其中 _`<Region>`_ 是[地區](/docs/services/Registry/registry_overview.html#registry_regions)的簡稱，例如 `us-south`：

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource <namespace_b> --roles Reader
        ```
        {: pre}

    4. 執行下列指令，建立第二個原則以將 `namespace_c` 的「讀者」及「作者」角色授與「使用者 B」：

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        此指令會將兩個角色新增至相同原則中的相同資源。
        {: tip}

4. 將映像檔推送至 `namespace_a` 及 `namespace_b`：

    1. 執行下列指令，以取回 `hello-world` 映像檔：

        ```
        docker pull hello-world
        ```
        {: pre}

    2. 執行下列指令，以將映像檔標記至 `namespace_a`：

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

    3. 執行下列指令，以將映像檔標記至 `namespace_b`：

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

    4. 執行下列指令，以登入 {{site.data.keyword.registrylong_notm}}：

        ```
  ibmcloud cr login
  ```
        {: pre}

    5. 執行下列指令，以將映像檔推送至 `namespace_a`：

        ```
        docker push registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

    6. 執行下列指令，以將映像檔推送至 `namespace_b`：

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

5. 證明「使用者 B」可以與 `namespace_b` 及 `namespace_c` 互動，但不能與 `namespace_a` 互動：

    1. 執行下列指令，以「使用者 B」身分登入：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 執行下列指令，以顯示「使用者 B」可以看到 `namespace_b` 及 `namespace_c`，但看不到 `namespace_a`，因為「使用者 B」無法存取 `namespace_a`：

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. 執行下列指令，以列出映像檔：

        ```
    ibmcloud cr images
    ```
        {: pre}

        `namespace_b` 中的映像檔會顯示在清單中，但 `namespace_a` 中的映像檔不會，因為「使用者 B」無法存取 `namespace_a`。

    4. 執行下列指令，以登入 {{site.data.keyword.registrylong_notm}}：

        ```
  ibmcloud cr login
  ```
        {: pre}

    5. 執行下列指令，以取回映像檔：

        ```
        docker pull registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

    6. 執行下列指令，以將映像檔推送至 `namespace_b`：

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

        因為「使用者 B」沒有 `namespace_b` 的「作者」角色，所以此指令失敗。

    7. 執行下列指令，以使用 `namespace_c` 來標記映像檔：

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

    8. 執行下列指令，以將映像檔推送至 `namespace_c`：

        ```
        docker push registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

        此指令的運作原因是「使用者 B」具有 `namespace_c` 的「作者」角色。

    9. 執行下列指令，以從 `namespace_c` 取回：

        ```
        docker pull registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

        此指令的運作原因是「使用者 B」具有 `namespace_c` 的「讀者」角色。

6. 清除：

    1. 執行下列指令，以重新登入「使用者 A」的帳戶：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 執行下列指令，以列出「使用者 B」的原則：

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        找到您剛才建立的原則，並記下「原則 ID」。

    3. 執行下列指令，以刪除原則，其中 _`<Policy_ID>`_ 是「原則 ID」：

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## 步驟 3：建立服務 ID 並授與資源存取權
{: #service_id}

在本節中，您會配置「服務 ID」，並將您 {{site.data.keyword.registrylong_notm}} 名稱空間的存取權授與它。
{:shortdesc}

1. 設定具有 {{site.data.keyword.registrylong_notm}} 存取權的「服務 ID」，並為其建立 API 金鑰：

    1. 執行下列指令，以登入「使用者 A」的帳戶：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 執行下列指令，以建立名為 `cr-roles-tutorial` 的「服務 ID」，且說明為 `"Created during the access control tutorial for Container Registry"`：

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. 執行下列指令，建立「服務 ID」的服務原則，以授與 `namespace_a` 的「讀者」角色：

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. 執行下列指令，建立第二個服務原則，以授與 `namespace_b` 的「作者」角色：

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. 執行下列指令，以建立「服務 ID」的 API 金鑰：

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. 使用 Docker 以利用「服務 ID」API 金鑰登入，其中 _`<API_Key>`_ 是 API 金鑰，並與登錄互動：

    1. 執行下列指令，以登入 {{site.data.keyword.registrylong_notm}}：

        ```
        docker login -u iamapikey -p <API_Key> registry.<Region>.bluemix.net
        ```
        {: pre}

    2. 執行下列指令，以取回映像檔：

        ```
        docker pull registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

        此指令會運作。

    3. 執行下列指令，以將映像檔推送至 `namespace_a`：

        ```
        docker push registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

        因為使用者沒有 `namespace_a` 的「作者」角色，所以此指令未運作。

    4. 執行下列指令，以將映像檔推送至 `namespace_b`：

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

        此指令的運作原因是使用者具有 `namespace_b` 的「作者」角色。

3. 清除：

    1. 執行下列指令，以列出服務原則：

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        記下「原則 ID」。

    2. 針對每個原則，執行下列指令，以刪除服務原則：

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. 執行下列指令，以刪除「服務 ID」：

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. 以「使用者 A」身分重新登入 {{site.data.keyword.registrylong_notm}}：

        ```
  ibmcloud cr login
  ```
        {: pre}

## 步驟 4：清除
{: #clean_up}

在本節中，您會移除在前幾個小節中建立的資源，讓帳戶維持本指導教學開始處的狀態。
{:shortdesc}

1. 執行下列指令，以登入帳戶：

    ```
    ibmcloud login
    ```
    {: pre}

2. 執行下列指令，以刪除 `namespace_a`、`namespace_b` 及 `namespace_c`：

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. 執行下列指令，以從帳戶中移除「使用者 B」：

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

很好！您已順利完成本指導教學。
