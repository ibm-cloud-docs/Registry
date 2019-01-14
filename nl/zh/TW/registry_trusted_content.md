---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 簽署受信任內容的映像檔
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} 提供受信任內容技術，讓您可以簽署映像檔，以確保登錄名稱空間中之映像檔的完整性。透過取回及推送已簽署的映像檔，您可以驗證映像檔已由正確的參與方推送，例如您的持續整合 (CI) 工具。若要使用此特性，您必須具有 Docker 18.03 版或更新版本。您可以藉由檢閱 [Docker Content Trust ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/engine/security/trust/content_trust/) 及 [Notary 專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/theupdateframework/notary) 文件，進一步瞭解。
{:shortdesc}

當您推送映像檔並啟用受信任內容時，您的 Docker 用戶端也會將已簽署的 meta 資料物件推送至 {{site.data.keyword.Bluemix_notm}} 信任伺服器。當您取回已標記的映像檔並啟用 Docker Content Trust 時，您的 Docker 用戶端會與信任伺服器聯絡，以建立您所要求標籤的最新簽署版本、驗證內容簽章，並下載已簽署的映像檔。

映像檔名稱由儲存庫及標籤組成。使用受信任內容時，每一個儲存庫都使用唯一的簽署金鑰。儲存庫中的每一個標籤都使用屬於該儲存庫的金鑰。如果您有多個團隊在發佈內容，而每個團隊都會發佈到 {{site.data.keyword.registrylong_notm}} 名稱空間內自己的儲存庫，則每個團隊都可以使用自己的金鑰來簽署他們的內容，如此您就可以驗證每個映像檔都是由適當的團隊產生。

儲存庫可以包含已簽署及未簽署的內容。如果已啟用 Docker Content Trust，您可以存取儲存庫中已簽署的內容，即使一旁還有其他未簽署的內容。

Docker Content Trust 使用「首次使用時信任」的安全模型。第一次從儲存庫取回已簽署的映像檔時，會從信任伺服器取回儲存庫金鑰，並在未來使用該金鑰來驗證來自該儲存庫的映像檔。第一次取回儲存庫之前，您必須先驗證您信任信任伺服器，或是信任映像檔及其發佈者。如果伺服器中的信任資訊已洩漏，且您之前未曾從儲存庫取回映像檔，則 Docker 用戶端可能會從信任伺服器取回已洩漏的資訊。如果信任資料在您第一次取回映像檔之後洩漏，則在後續取回時，您的 Docker 用戶端將無法驗證已洩漏的資料，而不會取回映像檔。如需如何檢查映像檔信任資料的相關資訊，請參閱[檢視已簽署的映像檔](#trustedcontent_viewsigned)。

如需「首次使用時信任」安全模型的相關資訊，請參閱 [The Update Framework (TUF) ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://theupdateframework.github.io/)。

## 設定受信任內容環境
{: #trustedcontent_setup}

依預設，會停用 Docker Content Trust。請先啟用 Content Trust 環境，再登入 {{site.data.keyword.registrylong_notm}} 並使用已簽署的映像檔。
{:shortdesc}

1. 在您的終端機中，啟用 Docker Content Trust 環境變數。

   若為 Linux 或 Mac：

   ```
export DOCKER_CONTENT_TRUST=1
    ```
   {: codeblock}

   若為 Windows：

   ```
set DOCKER_CONTENT_TRUST=1
    ```
   {: codeblock}

2. 登入 {{site.data.keyword.Bluemix_notm}} CLI。

   ```
    ibmcloud login [--sso]
    ```
   {: pre}

   如果您有聯合 ID，請使用 `ibmcloud login --sso` 來登入。請輸入您的使用者名稱，並使用 CLI 輸出中提供的 URL，來擷取一次性密碼。若未使用 `--sso` 時登入失敗，而有使用 `--sso` 選項時登入成功，即表示您有聯合 ID。
    {: tip}

3. 將目標設為您要使用的地區。如果您不知道地區名稱，則可以執行不含地區的指令，然後選擇地區。

   ```
    ibmcloud cr region-set <region>
    ```
   {: pre}

4. 登入 {{site.data.keyword.registrylong_notm}}。

   ```
  ibmcloud cr login
  ```
   {: pre}

   輸出會指示您匯出 Docker Content Trust 環境變數。

   **範例**

   ```
    user:~ user$ ibmcloud cr login
    Logging in to 'registry.ng.bluemix.net'...
    Logged in to 'registry.ng.bluemix.net'.To set up your Docker client with content trust, export the following environment variable:
    export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
   {: screen}

5. 在終端機中，複製並貼上環境變數指令。例如：

   ```
export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
   {: pre}

現在，您可以開始推送、取回及管理受信任的已簽署映像檔。

在啟用 Docker Content Trust 的階段作業期間，如果您要執行作業並停用受信任內容（例如取回未簽署的映像檔），請使用 `--disable-content-trust` 旗標與指令搭配。
{: tip}

## 推送已簽署的映像檔
{: #trustedcontent_push}

第一次推送已簽署的映像檔時，Docker 會自動建立一對簽署金鑰：主要金鑰與儲存庫金鑰。若要在先前已推送已簽署映像檔的儲存庫中簽署映像檔，您必須在推送映像檔的機器上，載入正確的儲存庫簽署金鑰。
{:shortdesc}

開始之前，請[設定登錄名稱空間](index.html#registry_namespace_add)。

1. [設定受信任內容環境](#trustedcontent_setup)。

2. [推送映像](index.html#registry_images_pushing)。標籤對於受信任內容而言是必要的。在指令輸出中，您會看到 "Signing and pushing image metadata"。

3. **首次推送已簽署的儲存庫。**將已簽署的映像檔推送至新儲存庫時，指令會建立兩個簽署金鑰：主要金鑰及儲存庫金鑰，並將它們儲存在您的本端機器。請輸入並儲存每一個金鑰的安全通行詞組，然後[備份金鑰](#trustedcontent_backupkeys)。備份金鑰很重要，因為您的[回復選項](ts_index.html#ts_recoveringtrustedcontent)受到限制。

## 取回已簽署的映像檔
{: #trustedcontent_pull}

第一次取回已簽署的映像檔並啟用 Docker Content Trust 時，您的 Docker 用戶端會將簽章辨識為受信任。Docker 用戶端會取回您所指定映像檔的最新簽署版本。不會取回未簽署的映像檔或不受信任的內容。
{:shortdesc}

1. [設定受信任內容環境](#trustedcontent_setup)。

2. 取回映像檔。將 _&lt;source_image&gt;_ 取代為映像檔的儲存庫，並將 _&lt;tag&gt;_ 取代為您要使用之映像檔的標籤，例如 _latest_。若要列出可取回的可用映像檔，請執行 `ibmcloud cr image-list`。

   ```
docker pull <source_image>:<tag>
    ```
   {: pre}

    當您推送或取回已簽署的映像檔時，請指定標籤。只有在停用內容信任時，才會預設為 `latest` 標籤。
    {: tip}

## 管理受信任的內容
{: #trustedcontent_managetrust}

使用 `docker trust` 指令，您可以檢視映像檔的簽章者，以及撤銷信任內容狀態。若要執行 `docker trust` 指令，您必須具有 Docker 18.03 或更新版本。
{:shortdesc}

### 檢視已簽署的映像檔
{: #trustedcontent_viewsigned}

您可以檢閱映像檔儲存庫或標籤的已簽署版本，包括金鑰 ID 及簽章者的相關資訊。
{:shortdesc}

1. [設定受信任內容環境](#trustedcontent_setup)。

2. 檢閱每一個映像檔的標籤、摘要及簽章者資訊。

   （選用）指定標籤 _&lt;tag&gt;_，以查看該映像檔版本的相關資訊。

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### 撤銷信任
{: #trustedcontent_revoketrust}

您可以撤銷映像檔的受信任內容狀態。
{:shortdesc}

開始之前，請擷取您在[第一次推送受信任儲存庫](#trustedcontent_push)時所儲存的儲存庫金鑰通行詞組。如果您需要識別用於受信任映像檔的金鑰，請使用 `docker view` [指令](#trustedcontent_viewsigned)。

1. [設定受信任內容環境](#trustedcontent_setup)。

2. 移除映像檔儲存庫的所有受信任 meta 資料。系統提示時，請輸入您的儲存庫金鑰通行詞組。

   （選用）指定標籤，僅針對該映像檔版本撤銷受信任的 meta 資料。

   ```
docker trust revoke <image>:<tag>
    ```
   {: pre}

3. 在受信任內容清單中，驗證信任已撤銷。

   （選用）如果您要驗證已標記映像檔的已撤銷內容，請包含標籤。

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   前一個指令的輸出：

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## 備份簽署金鑰
{: #trustedcontent_backupkeys}

第一次將已簽署的映像檔推送至新儲存庫時，Docker Content Trust 會建立兩個簽署金鑰：主要金鑰及儲存庫金鑰，並將它們儲存在您的本端機器：

* Linux 及 Mac 目錄：`~/.docker/trust/private`

* Windows 目錄：`%HOMEPATH%\.docker\trust\private`

   如果您已變更 Docker 配置目錄，請在那裡尋找 `trust` 子目錄。
   {: tip}

您必須備份所有金鑰，尤其是主要金鑰。如果金鑰遺失或洩漏，您的[回復選項](ts_index.html#ts_recoveringtrustedcontent)會受到限制。

若要備份您的金鑰，請參閱 [Docker Content Trust 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys)。

## 管理受信任的簽章者
{: #trustedcontent_signers}

您可以在儲存庫中，新增及移除簽署映像檔的簽章者。
{:shortdesc}

### 將簽章者新增至受信任的儲存庫
{: #trustedcontent_addsigners}

若要容許其他使用者在儲存庫中簽署映像檔，請將那些使用者的簽署金鑰新增至該儲存庫。
{:shortdesc}

**開始之前**

- 映像檔簽章者必須具有將映像檔推送至名稱空間的許可權。
- 儲存庫擁有者及其他簽章者必須已安裝 Docker 18.03 或更新版本。
- 藉由[推送已簽署的映像檔](#trustedcontent_push)來建立受信任內容儲存庫。儲存庫擁有者在其本端機器上的 Docker 信任資料夾中，必須有儲存庫的儲存庫管理金鑰可用。如果您沒有儲存庫管理金鑰，請與擁有者聯絡，以為您執行這項作業。

新增簽章者時，您無法再使用儲存庫管理金鑰來簽署該儲存庫中的映像檔。您必須持有其中一位已核准簽章者的私密金鑰才能簽署。新增簽章者之後，若要保留簽署映像檔的能力，請再次遵循這些指示，以產生並新增您自己的簽章者角色。
{:tip}

若要共用簽署金鑰，請執行下列動作：

1. 如果新的簽章者尚未產生金鑰組，則必須產生並載入金鑰組。
  
    a. 產生金鑰。您可以針對 _&lt;NAME&gt;_ 輸入任何名稱，不過，當有人對儲存庫檢查信任時，會看見您選取的名稱。請與儲存庫擁有者合作，以符合組織可能使用的任何命名慣例，並選取該簽章者可識別的名稱。

      ```
      docker trust key generate <NAME>
      ```
      {: pre}
  
    b. 輸入私密金鑰的通行詞組。會產生公開金鑰 (`.pub`)，且對應的私密金鑰會自動載入至 Docker 信任配置。
  
    c. 新的簽章者必須將公開金鑰傳送給儲存庫擁有者。

2. 儲存庫擁有者必須將簽章者的金鑰新增至儲存庫。

    a. [設定受信任內容環境](#trustedcontent_setup)。

    b. 將簽章者的金鑰新增至儲存庫。

      ```
      docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}

3. 簽章者可以設定其環境並簽署映像檔。

    a. [設定受信任內容環境](#trustedcontent_setup)。

    b. 簽章者必須簽署映像檔。系統提示時，請輸入私密金鑰的通行詞組。

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4. 若要驗證已新增簽章者，請參閱[檢視已簽署的映像檔](#trustedcontent_viewsigned)。

### 從儲存庫中移除簽章者
{: #trustedcontent_removesigner}

如果您不再希望簽章者能夠在儲存庫中簽署映像檔，您可以移除他們的簽章者身分。
{:shortdesc}

開始之前，儲存庫擁有者及其他簽章者必須已安裝 Docker 18.03 或更新版本。

如果您移除簽章者，則信任伺服器不會信任其已簽署的映像檔版本。若要確保在移除簽章者之後可以取回映像檔，在繼續之前，請先確定簽章者未簽署映像檔的最新版本。如果簽章者已簽署映像檔的最新版本，請先推送映像檔的更新，並用您的金鑰進行簽署，然後再繼續。
{:tip}

若要移除簽章者，請執行下列動作：

1. [設定受信任內容環境](#trustedcontent_setup)。

2. 移除簽章者。

   ```
    docker trust signer remove <NAME> <repository>
    ```
   {: pre}

3. 若要驗證已移除簽章者，請檢視映像檔的信任資料，並驗證不再列出該簽章者。如需檢視信任資料的相關資訊，請參閱[檢視已簽署的映像檔](#trustedcontent_viewsigned)。
