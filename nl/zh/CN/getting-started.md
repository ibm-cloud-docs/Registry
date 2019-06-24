---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-13"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security, cli, namespaces, tutorial, Docker, images, registry

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

# 入门教程
{: #getting-started}

{{site.data.keyword.registrylong}} 提供多租户专用映像注册表，可用于存储 Docker 映像并与您 {{site.data.keyword.cloud_notm}} 帐户中的用户共享。
{:shortdesc}

{{site.data.keyword.cloud_notm}} 控制台中有简要的“快速入门”。要了解有关如何使用 {{site.data.keyword.cloud_notm}} 控制台的更多信息，请参阅[使用漏洞顾问程序管理映像安全性](/docs/services/va?topic=va-va_index)。

不要将个人信息放入容器映像、名称空间名称、描述字段（例如，注册表令牌）或任何映像配置数据（例如，映像名称或映像标签）中。
{: important}

## 安装 {{site.data.keyword.registrylong_notm}} CLI
{: #gs_registry_cli_install}

1. 安装 [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)，以便可以运行 {{site.data.keyword.cloud_notm}} `ibmcloud` 命令。此安装还会安装 {{site.data.keyword.containerlong_notm}} 和 {{site.data.keyword.registrylong_notm}} 的 CLI 插件。

## 设置名称空间
{: #gs_registry_namespace_add}

1. 登录到 {{site.data.keyword.cloud_notm}}。

   ```
    ibmcloud login
    ```
   {: pre}

   如果拥有的是联合标识，请使用以下命令进行登录：

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. 添加名称空间以创建自己的映像存储库。将 `<my_namespace>` 替换为您首选的名称空间。

   ```
    ibmcloud cr namespace-add <my_namespace>
    ```
   {: pre}

   名称空间名称在区域中必须唯一。
        {: tip}

3. 要确保创建了名称空间，请运行 `ibmcloud cr namespace-list` 命令。

   ```
    ibmcloud cr namespace-list
    ```
   {: pre}

## 将映像从其他注册表拉出到本地计算机
{: #gs_registry_images_pulling}

1. [安装 Docker Engine CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.docker.com/products/docker-engine#/download)。对于 Windows 8 或 OS X Yosemite 10.10.x 或更低版本，请改为安装 [Docker Toolbox ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.docker.com/toolbox/)。{{site.data.keyword.registrylong_notm}} 支持 Docker Engine V1.12.6 或更高版本。

2. 将映像下载（_拉出_）到本地计算机。将 `<source_image>` 替换为映像的存储库，并将 `<tag>` 替换为要使用的映像标记，例如 _latest_。

   ```
    docker pull <source_image>:<tag>
    ```
   {: pre}

   例如，其中 `<source_image>` 是 `hello-world`，`<tag>` 是 `latest`：

   ```
    docker pull hello-world:latest
    ```
   {: pre}

3. 标记映像。将 `<source_image>` 替换为存储库，将 `<tag>` 替换为之前拉出的本地映像的标记。将 `<region>` 替换为[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)的名称。将 `<my_namespace>` 替换为您在[设置名称空间](#gs_registry_namespace_add)中创建的名称空间。通过替换 `<new_image_repo>` 和 `<new_tag>`，定义要在名称空间中使用的映像的存储库和标记。

   ```
   docker tag <source_image>:<tag> <region>.icr.io/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   要查找区域名称，请运行 `ibmcloud cr region` 命令。
   {: tip}

   例如，其中 `<source_image>` 是 `hello-world`，`<tag>` 是 `latest`，`<region>` 是 `uk`，
`<my_namespace>` 是 `namespace1`，`<new_image_repo>` 是 `hw_repo`，`<new_tag>` 是 `1`：

   ```
   docker tag hello-world:latest uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

## 将 Docker 映像推送到名称空间
{: #gs_registry_images_pushing}

1. 运行 `ibmcloud cr login` 命令，使本地 Docker 守护程序登录到 {{site.data.keyword.registrylong_notm}}。

   ```
  ibmcloud cr login
  ```
   {: pre}

2. 将映像上传（_推送_）至名称空间。将 `<my_namespace>` 替换为您在[设置名称空间](#gs_registry_namespace_add)中创建的名称空间，将 `<image_repo>` 和 `<tag>` 替换为您标记映像时选择的映像的存储库和标记。

   ```
   docker push <region>.icr.io/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}
   
   例如，其中 `<region>` 是 `uk`，`<my_namespace>` 是 `namespace1`，`<image_repo>` 是 `hw_repo`，并且
`<tag>` 是 `1`：

   ```
   docker push uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

3. 通过运行以下命令，验证已成功推送映像。

   ```
    ibmcloud cr image-list
    ```
   {: pre}

非常好！您已在 {{site.data.keyword.registrylong_notm}} 中设置名称空间，并将第一个映像推送到您的名称空间。

## 后续步骤
{: #gs_get_start_next}

- [使用漏洞顾问程序管理映像安全性](/docs/services/va?topic=va-va_index)
- [查看服务套餐和使用情况](/docs/services/Registry?topic=registry-registry_overview#registry_plans)
- [在名称空间中存储和管理更多映像](/docs/services/Registry?topic=registry-registry_images_)
- [定义用户访问角色策略](/docs/services/Registry?topic=registry-user#user)
- [设置集群和工作程序节点](/docs/containers?topic=containers-clusters#clusters)
