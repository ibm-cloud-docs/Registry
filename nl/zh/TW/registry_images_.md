---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-29"

keywords: IBM Cloud Container Registry, Docker build command, delete images, add images, pull images, push images, copy images, delete private repositories,

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

# 將映像檔新增至名稱空間
{: #registry_images_}

藉由將映像檔新增至 {{site.data.keyword.registrylong}} 中的名稱空間，即可安全地儲存 Docker 映像檔，並將它與其他使用者共用。
{:shortdesc}

您要新增至名稱空間的每個映像檔都必須先存在於本端電腦上。您可以將映像檔從另一個儲存庫下載（取回）至本端電腦，或使用 Docker `build` 指令，以從 Dockerfile 建置自己的映像檔。若要將映像檔新增至名稱空間，您必須將本端映像檔上傳（推送）至 {{site.data.keyword.registrylong_notm}} 中的名稱空間。

請不要將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。
{: important}

## 從另一個登錄取回映像檔
{: #registry_images_pulling_reg}

您可以從任何專用或公用登錄來源中取回（下載）映像檔，然後標記它，以供稍後在 {{site.data.keyword.registrylong_notm}} 中使用。
{:shortdesc}

<img src="images/images_pull.svg" width="800" style="width:800px;" alt="將映像檔從專用或公用登錄取回至您的電腦。"/>

**開始之前**

- [安裝 CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)，以使用名稱空間中的映像檔。
- [在 {{site.data.keyword.registrylong_notm}} 中設定自己的名稱空間](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)。
- [確定您可以在沒有 root 使用者權限 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/install/linux/linux-postinstall/) 的情況下執行 Docker 指令。如果您的 Docker 用戶端設定成需要 root 許可權，則必須使用 `sudo` 來執行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 及 `docker push` 指令。

  如果您變更許可權以在沒有 root 專用權的情況下執行 Docker 指令，則必須再次執行 `ibmcloud login` 指令。

下載映像檔，請參閱「開始使用」文件中的[取回映像檔](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pulling)。

如果您收到 `unauthorized: authentication required` 或 `denied: requested access to the resource is denied` 訊息，請執行 `ibmcloud cr login` 指令。
  {:tip}

在您取回映像檔並針對名稱空間標記它之後，可以將映像檔從本端電腦上傳（推送）至名稱空間。

## 將 Docker 映像檔推送至名稱空間
{: #registry_images_pushing_namespace}

您可以將映像檔推送（上傳）至 {{site.data.keyword.registrylong_notm}} 中的名稱空間，以儲存映像檔，並將它與其他使用者共用。
{:shortdesc}

<img src="images/images_push.svg" width="800" style="width:800px;" alt="將映像檔從您的電腦推送至 {{site.data.keyword.registrylong_notm}}。"/>

**開始之前**

- [安裝 CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)，以使用名稱空間中的映像檔。
- [在 {{site.data.keyword.registrylong_notm}} 中設定自己的名稱空間](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)。
- 在本端電腦上[取回](#registry_images_pulling_reg)或[建置](#registry_images_creating)映像檔，並以您的名稱空間資訊標記映像檔。
- [確定您可以在沒有 root 使用者權限 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/install/linux/linux-postinstall/) 的情況下執行 Docker 指令。如果您的 Docker 用戶端設定成需要 root 許可權，則必須使用 `sudo` 來執行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 及 `docker push` 指令。

  如果您變更許可權以在沒有 root 專用權的情況下執行 Docker 指令，則必須再次執行 `ibmcloud login` 指令。

若要上傳（推送）映像檔，請完成下列步驟：

1. 登入 CLI。

   ```
   ibmcloud cr login
   ```
   {: pre}

   如果您從專用 {{site.data.keyword.registrylong_notm}} 取回映像檔，則必須登入。
  {:tip}

2. 若要檢視帳戶中可用的所有名稱空間，請執行 `ibmcloud cr namespace-list` 指令。
3. [將映像檔上傳至名稱空間。](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)

   如果您收到 `unauthorized: authentication required` 或 `denied: requested access to the resource is denied` 訊息，請執行 `ibmcloud cr login` 指令。
  {:tip}

在將映像檔推送至 {{site.data.keyword.registrylong_notm}} 之後，您可以執行下列其中一項作業：

- [使用 Vulnerability Advisor 管理安全](/docs/services/va?topic=va-va_index)，以尋找潛在安全問題及漏洞的相關資訊。
- [建立叢集以及使用此映像檔來部署容器](/docs/containers?topic=containers-getting-started#getting-started)至 {{site.data.keyword.containerlong_notm}} 中的叢集。

## 在登錄之間複製映像檔
{: #registry_images_copying}

您可以從某個地區的登錄取回映像檔，然後將它推送至另一個地區的登錄，即可與這兩個地區的使用者共用映像檔。
{:shortdesc}

<img src="images/images_copy.svg" width="800" style="width:800px;" alt="將映像檔從任何專用或公用登錄複製到您的專用 {{site.data.keyword.cloud_notm}} 登錄。"/>

**開始之前**

- [安裝 CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)，以使用名稱空間中的映像檔。
- [在 {{site.data.keyword.registrylong_notm}} 中設定自己的名稱空間](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)。
- [確定您可以在沒有 root 使用者權限 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/install/linux/linux-postinstall/) 的情況下執行 Docker 指令。如果您的 Docker 用戶端設定成需要 root 許可權，則必須使用 `sudo` 來執行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 及 `docker push` 指令。

  如果您變更許可權以在沒有 root 專用權的情況下執行 Docker 指令，則必須再次執行 `ibmcloud login` 指令。

若要在兩個登錄之間複製映像檔，請完成下列步驟：

1. [從登錄取回映像檔](#registry_images_pulling_reg)。
2. [將映像檔推送至另一個登錄](#registry_images_pushing_namespace)。請確定您針對目標新地區使用正確的網域名稱。

複製映像檔之後，您可以執行下列其中一項作業：

- [使用 Vulnerability Advisor 管理映像檔安全](/docs/services/va?topic=va-va_index)，以尋找潛在安全問題及漏洞的相關資訊。
- [建立叢集以及使用此映像檔來部署容器](/docs/containers?topic=containers-getting-started#getting-started)至 {{site.data.keyword.containerlong_notm}} 中的叢集。

## 建立參照來源映像檔的新映像檔
{: #registry_images_source}

在您登入的地區中，在 {{site.data.keyword.registrylong_notm}} 中建立一個新的映像檔，其參照相同地區中的現有映像檔。只有使用 Docker Engine 1.12 版或更新版本所建立的來源映像檔，才支援此動作。

使用此機制所建立的新映像檔並不會保留簽章。如果您要求簽署新的映像檔，請勿使用此機制。
{: tip}

**開始之前**

- [安裝 CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)，以使用名稱空間中的映像檔。
- 對於 {{site.data.keyword.registrylong_notm}} 中，包含您要另一個映像檔參照之來源映像檔的專用名稱空間，請確定您具有該名稱空間的存取權。

如需指令的相關資訊，請參閱 [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag)。

若要從來源映像檔建立新的映像檔，請完成下列步驟：

1. 登入 CLI。

   ```
   ibmcloud cr login
   ```
   {: pre}

2. 執行下列指令，以新增參照，其中，`SOURCE_IMAGE` 是來源映像檔的名稱，而 `TARGET_IMAGE` 為目標映像檔的名稱。來源及目標映像檔必須位於相同地區。`SOURCE_IMAGE` 及 `TARGET_IMAGE` 的格式必須為 `<REPOSITORY>:<TAG>`，例如：`us.icr.io/namespace/image:latest`

   ```
   ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
   ```
   {: pre}

3. 執行下列指令，驗證已建立新的映像檔，並確認映像檔顯示在清單中，且映像檔摘要同於來源映像檔。

   ```
    ibmcloud cr image-list
    ```
   {: pre}

## 建置 Docker 映像檔以與名稱空間搭配使用
{: #registry_images_creating}

您可以直接在 {{site.data.keyword.cloud_notm}} 建置 Docker 映像檔，或在本端電腦上建立自己的 Docker 映像檔，並將它上傳（推送）至 {{site.data.keyword.registrylong_notm}} 中的名稱空間。
{:shortdesc}

**開始之前**

- [安裝 CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)，以使用名稱空間中的映像檔。
- [在 {{site.data.keyword.registrylong_notm}} 中設定自己的名稱空間](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)。
- [確定您可以在沒有 root 使用者權限 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/install/linux/linux-postinstall/) 的情況下執行 Docker 指令。如果您的 Docker 用戶端設定成需要 root 許可權，則必須使用 `sudo` 來執行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 及 `docker push` 指令。

  如果您變更許可權以在沒有 root 專用權的情況下執行 Docker 指令，則必須再次執行 `ibmcloud login` 指令。

Docker 映像檔是每個您建立的容器的基準。映像檔是從 Dockerfile 建立的，而 Dockerfile 是包含映像檔建置指示的檔案。Dockerfile 可能會在其指示中參照個別儲存的建置構件，例如應用程式、應用程式的配置，以及其相依關係。

如果您要充分運用 {{site.data.keyword.cloud_notm}} 運算資源與網際網路連線，或是您的工作站上未安裝 Docker，請直接在 {{site.data.keyword.cloud_notm}} 中建置映像檔。如果您需要在建置中存取資源，而這些資源位於防火牆之後的伺服器上，請在本端建置您的映像檔。

若要建置自己的 Docker 映像檔，請完成下列步驟：

1. 建立您要在其中儲存建置環境定義的本端目錄。建置環境定義包含您的 Dockerfile 及相關建置構件（例如應用程式碼）。在指令行視窗中，導覽至此目錄。
2. 建立 Dockerfile。
    1. 在本端目錄中建立 Dockerfile。

        ```
    touch Dockerfile
    ```
        {: pre}

    2. 使用文字編輯器來開啟 Dockerfile。您至少必須新增基礎映像檔，以根據它建置映像檔。請將 `<source_image>` 及 `<tag>` 取代為您要使用的映像檔儲存庫及標籤。如果您要使用另一個專用登錄中的映像檔，請定義 {{site.data.keyword.registrylong_notm}} 中映像檔的完整路徑。

       ```
    FROM <source_image>:<tag>
    ```
       {: pre}

       **範例**
     若要建立以公用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty (ibmliberty) 映像檔為基礎之 Dockerfile 的範例，請使用下列程式碼：

       ```
       FROM <region>.icr.io/ibmliberty:latest
       LABEL description="This is my test Dockerfile"
       EXPOSE 9080
       ```
       {: pre}

       此範例會將標籤新增至映像檔 meta 資料，並公開埠 9080。如需您可以使用的其他 Dockerfile 指示，請參閱 [Dockerfile 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/engine/reference/builder/)。

3. 決定映像檔的名稱。映像檔名稱必須為下列格式：

   ```
   <region>.icr.io/<my_namespace>/<repo_name>:<tag>
   ```
   {: pre}

   其中 `<my_namespace>` 是您的名稱空間資訊、`<repo_name>` 是儲存庫名稱，而 `<tag>` 是您要用於映像檔的版本。若要尋找名稱空間，請執行 `ibmcloud cr namespace-list` 指令。

4. 記下包含 Dockerfile 的目錄路徑。如果您在下列步驟中執行指令，而工作目錄設為儲存建置環境定義之處，則可以將 `<directory>` 取代為句號 (.)。
5. 選擇直接在 {{site.data.keyword.cloud_notm}} 中建置映像檔，或先在本端建置並測試映像檔，再將它推送至 {{site.data.keyword.cloud_notm}}。
   - 若要直接在 {{site.data.keyword.cloud_notm}} 中建置映像檔，請執行下列指令：

     ```
    ibmcloud cr build -t <image_name> <directory>
    ```
     {: pre}

     其中 `<image_name>` 是您映像檔的名稱，而 `<directory>` 是目錄的路徑。如果您在工作目錄設為建置環境定義儲存所在的位置時執行指令，則可以將 `<directory>` 取代為句號 (.)。
  
     如需 `ibmcloud cr build` 指令的相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} CLI](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build)。

   - 若要先在本端建置並測試映像檔，再將它推送至 {{site.data.keyword.cloud_notm}}，請完成下列步驟：
      1. 在本端電腦上從 Dockerfile 建置映像檔，並以映像檔名稱來標記它。

         ```
       docker build -t <image_name> <directory>
       ```
         {: pre}

         其中 `<image_name>` 是您映像檔的名稱，而 `<directory>` 是目錄的路徑。

      2. 選用項目：先在本端電腦上測試映像檔，再將它推送至名稱空間。

         ```
      docker run <image_name>
      ```
         {: pre}

         將 `<image_name>` 取代為您的映像檔名稱。

      3. 在您建立映像檔並針對名稱空間標記它之後，[可以將映像檔推送至 {{site.data.keyword.registrylong_notm}} 中的名稱空間](#registry_images_pushing_namespace)。

若要使用 Vulnerability Advisor 來檢查映像檔的安全，請參閱[使用 Vulnerability Advisor 管理映像檔安全](/docs/services/va?topic=va-va_index)。

## 使用 API 金鑰將映像檔推送至 {{site.data.keyword.registrylong_notm}}
{: #registry_api_key_push_image}

建立一個服務 ID，使用 API 金鑰將映像檔推送至 {{site.data.keyword.registrylong_notm}}。
{:shortdesc}

1. 建立一個服務 ID。如需相關資訊，請參閱[建立及使用服務 ID](/docs/iam?topic=iam-serviceids#serviceids)。
2. 建立一個原則，給與服務 ID 存取登錄的許可權，例如`管理者`及`管理員`角色。如需相關資訊，請參閱[使用 Identity and Access Management 管理使用者存取](/docs/services/Registry?topic=registry-iam#iam)。
3. 建立一個 API 金鑰。如需相關資訊，請參閱[建立服務 ID 的 API 金鑰](/docs/iam?topic=iam-serviceidapikeys#create_service_key)。
4. 使用 API 金鑰來登入至登錄，以便您可以將映像檔推送至登錄。如需相關資訊，請參閱[使用 API 金鑰以自動化存取](/docs/services/Registry?topic=registry-registry_access#registry_api_key_use)。
5. 推送您的映像檔。如需相關資訊，請參閱[將 Docker 映像檔推送至名稱空間](#registry_images_pushing_namespace)。

您現在可以使用叢集來取回映像檔。如需相關資訊，請參閱[從映像檔建置容器](/docs/containers?topic=containers-images#other_registry_accounts)。

## 刪除專用 {{site.data.keyword.cloud_notm}} 儲存庫中的映像檔
{: #registry_images_remove}

您可以使用圖形使用者介面 (GUI) 或 CLI 刪除專用儲存庫中不想要的映像檔。
{:shortdesc}

如果您要刪除專用儲存庫及其相關聯映像檔，請參閱[刪除專用儲存庫及任何相關聯映像檔](#registry_repo_remove)。

無法刪除您專用 {{site.data.keyword.cloud_notm}} 儲存庫中的公用 {{site.data.keyword.IBM_notm}} 映像檔，且它們不會計入您的配額。

刪除映像檔無法復原。刪除現有部署正在使用的映像檔，可能會導致擴增及（或）重新排程失敗。
{:tip}

### 使用 CLI 刪除專用 {{site.data.keyword.cloud_notm}} 儲存庫中的映像檔
{: #registry_images_remove_cli}

您可以使用 CLI 刪除專用儲存庫中不想要的映像檔。
{:shortdesc}

刪除映像檔無法復原。刪除現有部署正在使用的映像檔，可能會導致擴增及（或）重新排程失敗。
{:tip}

若要使用 CLI 刪除映像檔，請完成下列步驟：

1. 執行 `ibmcloud login` 指令，以登入 {{site.data.keyword.cloud_notm}}。
2. 若要刪除映像檔，請執行下列指令：

   ```
   ibmcloud cr image-rm IMAGE
   ```
   {: pre}

   其中 _IMAGE_ 是您要移除之映像檔的名稱，格式為 `repository:tag`。

   如果映像檔名稱中未指定標籤，則依預設會刪除以 `latest` 標記的映像檔。您可以藉由在指令中列出每一個專用 {{site.data.keyword.cloud_notm}} 登錄路徑，並以空格隔開每一個路徑，來刪除多個映像檔。

       若要尋找映像檔的名稱，請執行 `ibmcloud cr image-list`。請以 `repository:tag` 格式，結合 Repository 及 Tag 直欄的內容，以建立映像檔名稱。
   {:tip}

3. 執行下列指令，驗證已刪除映像檔，並確認映像檔未顯示在清單中。

   ```
   ibmcloud cr image-list
   ```
   {: pre}

### 使用 GUI 刪除專用 {{site.data.keyword.cloud_notm}} 儲存庫中的映像檔
{: #registry_images_remove_gui}

您可以使用圖形使用者介面 (GUI) 刪除專用映像檔儲存庫中不想要的映像檔。
{:shortdesc}

刪除映像檔無法復原。刪除現有部署正在使用的映像檔，可能會導致擴增及（或）重新排程失敗。
{:tip}

若要使用 GUI 刪除映像檔，請完成下列步驟：

1. 使用您的 IBM ID 登入 {{site.data.keyword.cloud_notm}} 主控台 ([https://cloud.ibm.com/login ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login))。
2. 如果您有多個 {{site.data.keyword.cloud_notm}} 帳戶，請從帳戶功能表中選取要使用的帳戶及地區。
3. 按一下**型錄**。
4. 選取**容器**種類，然後按一下 **Container Registry** 磚。
5. 按一下**映像檔**。即會顯示映像檔清單。
6. 在包含您要刪除之映像檔的列中，選取勾選框。

   請確定您已選取正確的映像檔，因為此動作無法復原。
   {: tip}

7. 按一下**刪除映像檔**。

## 刪除專用儲存庫及任何相關聯映像檔
{: #registry_repo_remove}

您可以使用圖形使用者介面 (GUI)，刪除不再需要的專用儲存庫及任何相關聯映像檔。
{:shortdesc}

當您刪除儲存庫時，會刪除該儲存庫中的所有映像檔。此動作無法復原。
{:tip}

**開始之前**

您必須備份要保留的所有映像檔。

若要使用 GUI 刪除專用儲存庫，請完成下列步驟：

1. 使用您的 IBM ID 登入 {{site.data.keyword.cloud_notm}} 主控台 ([https://cloud.ibm.com/login ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login))。
2. 如果您有多個 {{site.data.keyword.cloud_notm}} 帳戶，請從帳戶功能表中選取要使用的帳戶及地區。
3. 按一下**型錄**。
4. 選取**容器**種類，然後按一下 **Container Registry** 磚。
5. 按一下**儲存庫**。即會顯示您的專用儲存庫清單。
6. 在包含您要刪除之專用儲存庫的列中，選取勾選框。

    請確定您已選取正確的儲存庫，因為此動作無法復原。
    {: tip}

7. 按一下**刪除儲存庫**。
