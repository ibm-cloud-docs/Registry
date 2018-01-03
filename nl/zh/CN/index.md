---

copyright:
  years: 2017
lastupdated: "2017-11-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# {{site.data.keyword.registrylong_notm}} 入门
{: #index}

{{site.data.keyword.registrylong}} 提供多租户专用映像注册表，可用于安全地存储 Docker 映像并与您 {{site.data.keyword.Bluemix_notm}} 帐户中的用户共享。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 控制台中有简要的“快速入门”。要了解有关如何使用 {{site.data.keyword.Bluemix_notm}} 控制台的更多信息，请参阅[监视映像的漏洞](registry_ui.html)。


## 安装 {{site.data.keyword.registrylong_notm}} CLI
{: #registry_cli_install}

1.  安装 [{{site.data.keyword.Bluemix_notm}} CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://clis.ng.bluemix.net/ui/home.html)，以便可以运行 {{site.data.keyword.Bluemix_notm}} **bx** 命令。
2.  安装 container-registry 插件：

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}


## 设置名称空间
{: #registry_namespace_add}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    bx login
    ```
    {: pre}

2.  添加名称空间以创建自己的映像存储库。将 _&lt;my_namespace&gt;_ 替换为首选名称空间。

    ```
    bx cr namespace-add <my_namespace>
    ```
    {: pre}

3.  要确保创建了名称空间，请运行 `bx cr namespace-list` 命令。

    ```
    bx cr namespace-list
    ```
    {: pre}


## 将映像从其他注册表拉出到本地计算机
{: #registry_images_pulling}

1.  [安装 Docker CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.docker.com/community-edition#/download)。对于 Windows 8 或 OS X Yosemite 10.10.x 或更低版本，请改为安装 [Docker Toolbox ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.docker.com/products/docker-toolbox)。

2.  登录到 CLI：

    ```
    bx cr login
    ```
    {: pre}

    **注：**必须登录才能从专用 {{site.data.keyword.registrylong_notm}} 拉出映像。

3.  将映像下载（_拉出_）到本地计算机。将 _&lt;source_image&gt;_ 替换为映像的存储库，将 _&lt;tag&gt;_ 替换为要使用的映像标记，如 _latest_。 

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    例如，其中 _&lt;source_image&gt;_ 是 `hello-world`，_&lt;tag&gt;_ 是 `latest`：

    ```
    docker pull hello-world:latest
    ```
    {: pre}

4.  标记映像。将 _&lt;source_image&gt;_ 替换为存储库，将 _&lt;tag&gt;_ 替换为之前拉出的本地映像的标记。将 _&lt;region&gt;_ 替换为 [region](registry_overview.html#registry_regions) 的名称。将 _&lt;my_namespace&gt;_ 替换为在[设置名称空间](index.html#registry_namespace_add)中创建的名称空间。通过替换 _&lt;new_image_repo&gt;_ 和 _&lt;new_tag&gt;_，定义要在名称空间中使用的映像的存储库和标记。

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    例如，其中，_&lt;source_image&gt;_ 是 `hello-world`，_&lt;tag&gt;_ 是 `latest`，_&lt;region&gt;_ 是 `eu-gb`，_&lt;my_namespace&gt;_ 是 `Namespace1`，_&lt;new_image_repo&gt;_ 是 `hw_repo`，_&lt;new_tag&gt;_ 是 `1`：

    ```
    docker tag hello-world:latest registry.eu-gb.bluemix.net/Namespace1/hw_repo:1
    ```
    {: pre}


## 将 Docker 映像推送至名称空间
{: #registry_images_pushing}

1.  将映像上传（_推送_）至名称空间。将 _&lt;my_namespace&gt;_ 替换为在[设置名称空间](index.html#registry_namespace_add)中创建的名称空间，将 _&lt;image_repo&gt;_ 和 _&lt;tag&gt;_ 替换为标记映像时所选择的映像的存储库和标记。


    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    例如，其中，_&lt;region&gt;_ 是 `eu-gb`，_&lt;my_namespace&gt;_ 是 `Namespace1`，_&lt;image_repo&gt;_ 是 `hw_repo`，_&lt;tag&gt;_ 是 `1`：

    ```
    docker push registry.eu-gb.bluemix.net/Namespace1/hw_repo:1
    ```
    {: pre}

2.  通过运行以下命令，验证已成功推送映像。

    ```
    bx cr image-list
    ```
    {: pre}


非常好！您已在 {{site.data.keyword.registrylong_notm}} 中设置名称空间，并将第一个映像推送到您的名称空间。

**后续步骤**

-   [使用漏洞顾问程序管理映像安全性](../va/va_index.html)。
-   [查看服务套餐和使用情况](registry_overview.html#registry_plans)
-   [在名称空间中存储和管理更多映像](registry_images_.html)。
-   [基于映像创建容器并将其部署到 Kubernetes 集群](../../containers/cs_cluster.html)。

