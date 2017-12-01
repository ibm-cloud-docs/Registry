---

copyright:
  years: 2017
lastupdated: "2017-10-31"

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

{{site.data.keyword.Bluemix_notm}} 主控台包含了簡短的「快速入門」。若要找出如何使用 {{site.data.keyword.Bluemix_notm}} 主控台的詳細資訊，請參閱[在 {{site.data.keyword.Bluemix_notm}} 主控台中檢視映像檔的相關資訊](registry_ui.html)。


## 安裝 {{site.data.keyword.registrylong_notm}} CLI
{: #registry_cli_install}

1.  安裝 [{{site.data.keyword.Bluemix_notm}} CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://clis.ng.bluemix.net/ui/home.html)，以執行 {{site.data.keyword.Bluemix_notm}} **bx** 指令。
2.  安裝 container-registry 外掛程式：

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}


## 設定名稱空間
{: #registry_namespace_add}

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
    bx login
    ```
    {: pre}

2.  新增名稱空間，以建立自己的映像檔儲存庫。請將 _&lt;my_namespace&gt;_ 取代為您偏好的名稱空間。

    ```
    bx cr namespace-add <my_namespace>
    ```
    {: pre}


## 將映像檔從另一個登錄取回到本端機器
{: #registry_images_pulling}

1.  [安裝 Docker CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.docker.com/community-edition#/download)。針對 Windows 8 或是 OS X Yosemite 10.10.x 或更早版本，請改為安裝 [Docker 工具箱 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.docker.com/products/docker-toolbox)。

2.  登入 CLI：

    ```
    bx cr login
    ```
    {: pre}

    **附註：**如果從您的專用 {{site.data.keyword.registrylong_notm}} 取回映像檔，您必須登入。

3.  將映像檔下載（_取回_）至本端機器。請將 _&lt;source_image&gt;_ 取代為映像檔的儲存庫，並將 _&lt;tag&gt;_ 取代為您要使用之映像檔的標籤，例如 _latest_。

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    範例：

    ```
    docker pull hello-world:latest
    ```
    {: pre}

4.  標記映像檔。請將 _&lt;source_image&gt;_ 取代為儲存庫，並將 _&lt;tag&gt;_ 取代為您先前取回之本端映像檔的標籤。取代 _&lt;new_image_repo&gt;_ 及 _&lt;new_tag&gt;_，以定義名稱空間中您要使用之映像檔的儲存庫及標籤。

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    範例：

    ```
    docker tag hello-world:latest registry.<region>.bluemix.net/my_namespace/hw_repo:1
    ```
    {: pre}


## 將 Docker 映像檔推送至名稱空間
{: #registry_images_pushing}

1.  將映像檔上傳（_推送_）至名稱空間。請將 _&lt;my_namespace&gt;_ 取代為您要上傳映像檔的名稱空間，並將 _&lt;image_repo&gt;_ 及 _&lt;tag&gt;_ 取代為您在標記映像檔時所選擇映像檔的儲存庫及標籤。

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    範例：

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/hw_repo:1
    ```
    {: pre}

2.  執行下列指令，驗證已順利推送映像檔。

    ```
    bx cr image-list
    ```
    {: pre}


做得好！您已在 {{site.data.keyword.registrylong_notm}} 中設定名稱空間，並將您的第一個映像檔推送至名稱空間。

**下一步為何？**

-   [使用漏洞警告器管理映像檔安全](../va/va_index.html)。
-   [檢閱服務方案及用量](registry_overview.html#registry_plans)。
-   [儲存及管理名稱空間中的其他映像檔](registry_images_.html)。
-   [從映像檔建立容器，並將其部署至 Kubernetes 叢集](../../containers/cs_cluster.html)。

