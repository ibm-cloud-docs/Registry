---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 開始使用 {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}} 提供多方承租戶專用映像檔登錄，可用來安全地儲存 Docker 映像檔，並與 {{site.data.keyword.Bluemix_notm}} 帳戶中的使用者共用。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 主控台包含了簡短的「快速入門」。若要找出如何使用 {{site.data.keyword.Bluemix_notm}} 主控台的詳細資訊，請參閱[使用漏洞警告器管理映像檔安全](/docs/services/va/va_index.html)。

請不要將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。
{:tip}

## 安裝 {{site.data.keyword.registrylong_notm}} CLI
{: #registry_cli_install}

1. 安裝 [{{site.data.keyword.Bluemix_notm}} CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://clis.ng.bluemix.net/ui/home.html)，讓您可以執行 {{site.data.keyword.Bluemix_notm}} `ibmcloud` 指令。此安裝也會安裝 {{site.data.keyword.containerlong_notm}} 及 {{site.data.keyword.registrylong_notm}} 的外掛程式。

## 設定名稱空間
{: #registry_namespace_add}

1. 登入 {{site.data.keyword.Bluemix_notm}}。

   ```
    ibmcloud login
    ```
   {: pre}

2. 新增名稱空間，以建立自己的映像檔儲存庫。將 _&lt;my_namespace&gt;_ 取代為您偏好的名稱空間。

   ```
    ibmcloud cr namespace-add <my_namespace>
    ```
   {: pre}

3. 若要確定已建立名稱空間，請執行 `ibmcloud cr namespace-list` 指令。

   ```
    ibmcloud cr namespace-list
    ```
   {: pre}

## 將映像檔從另一個登錄取回到本端機器
{: #registry_images_pulling}

1. [安裝 Docker CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.docker.com/community-edition#/download)。若為 Windows 8 或是 OS X Yosemite 10.10.x 或更早版本，請改為安裝 [Docker 工具箱 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/toolbox/)。

2. 將映像檔下載（_取回_）至本端機器。將 _&lt;source_image&gt;_ 取代為映像檔的儲存庫，並將 _&lt;tag&gt;_ 取代為您要使用之映像檔的標籤，例如 _latest_。

   ```
docker pull <source_image>:<tag>
    ```
   {: pre}

   例如，其中 _&lt;source_image&gt;_ 是 `hello-world`，而 _&lt;tag&gt;_ 是 `latest`：

   ```
docker pull hello-world:latest
    ```
   {: pre}

3. 標記映像檔。將 _&lt;source_image&gt;_ 取代為儲存庫，並將 _&lt;tag&gt;_ 取代為您先前取回之本端映像檔的標籤。將 _&lt;region&gt;_ 取代為您的[地區](registry_overview.html#registry_regions)名稱。將 _&lt;my_namespace&gt;_ 取代為您在[設定名稱空間](index.html#registry_namespace_add)中建立的名稱空間。取代 _&lt;new_image_repo&gt;_ 及 _&lt;new_tag&gt;_，以定義您要在名稱空間中使用之映像檔的儲存庫及標籤。

   ```
docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
   {: pre}

   例如，其中 _&lt;source_image&gt;_ 是 `hello-world`、_&lt;tag&gt;_ 是 `latest`、_&lt;region&gt;_ 是 `eu-gb`、_&lt;my_namespace&gt;_ 是 `namespace1`、_&lt;new_image_repo&gt;_ 是 `hw_repo`，而 _&lt;new_tag&gt;_ 是 `1`：

   ```
    docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
    ```
   {: pre}

## 將 Docker 映像檔推送至名稱空間
{: #registry_images_pushing}

1. 執行 `ibmcloud cr login` 指令，以讓本端 Docker 常駐程式登入 {{site.data.keyword.registrylong_notm}}。

   ```
  ibmcloud cr login
  ```
   {: pre}

2. 將映像檔上傳（_推送_）至名稱空間。將 _&lt;my_namespace&gt;_ 取代為您在[設定名稱空間](index.html#registry_namespace_add)中建立的名稱空間，並將 _&lt;image_repo&gt;_ 及 _&lt;tag&gt;_ 取代為您在標記映像檔時所選擇映像檔的儲存庫及標籤。

   ```
docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
   {: pre}

   例如，其中 _&lt;region&gt;_ 是 `eu-gb`、_&lt;my_namespace&gt;_ 是 `namespace1`、_&lt;image_repo&gt;_ 是 `hw_repo`，而 _&lt;tag&gt;_ 是 `1`：

   ```
    docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
    ```
   {: pre}

3. 執行下列指令，驗證已順利推送映像檔。

   ```
    ibmcloud cr image-list
    ```
   {: pre}

做得好！您已在 {{site.data.keyword.registrylong_notm}} 中設定名稱空間，並將您的第一個映像檔推送至名稱空間。

**下一步為何？**

- [使用漏洞警告器管理映像檔安全](../va/va_index.html)
- [檢閱服務方案及用量](registry_overview.html#registry_plans)
- [儲存及管理名稱空間中的其他映像檔](registry_images_.html)
- [定義使用者存取角色原則](/docs/services/Registry/registry_users.html#user)
- [設定叢集與工作者節點](/docs/containers/cs_clusters.html#clusters)
