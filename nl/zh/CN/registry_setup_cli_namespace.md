---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, 

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

# 设置 {{site.data.keyword.registrylong_notm}} CLI 和注册表名称空间
{: #registry_setup_cli_namespace}

必须创建名称空间后，才能在 {{site.data.keyword.registrylong}} 中存储 Docker 映像。要使用名称空间，请安装 `container-registry` CLI 插件。
{:shortdesc}

不要将个人信息放入容器映像、名称空间名称、描述字段（例如，注册表令牌）或任何映像配置数据（例如，映像名称或映像标签）中。
{: important}

开始之前，安装 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

## 安装 `container-registry` CLI 插件
{: #cli_namespace_registry_cli_install}

安装 `container-registry` CLI 插件，以使用命令行在 {{site.data.keyword.registrylong_notm}} 中管理名称空间和 Docker 映像。
{:shortdesc}

1. [安装 `container-registry` CLI 插件](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)。
2. 可选：[配置 Docker 客户机以在没有 root 用户许可权的情况下运行命令 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.docker.com/engine/installation/linux/linux-postinstall)。如果未执行此步骤，那么必须以 `sudo` 或以 root 用户身份运行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 和 **docker push** 命令。

现在，您可以在 {{site.data.keyword.registrylong_notm}} 中设置自己的名称空间。

## 更新 `container-registry` CLI 插件
{: #registry_cli_update}

您可能希望定期更新 `container-registry` CLI 插件以使用新功能。
{:shortdesc}

1. 更新 `container-registry` CLI 插件。

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. 验证 `container-registry` CLI 插件是否已成功更新。

    ```
    ibmcloud plugin list
    ```
     {: pre}

## 卸载 `container-registry` CLI 插件
{: #registry_cli_uninstall}

如果不再需要 `container-registry` CLI 插件，可以将其卸载。
{:shortdesc}

1. 卸载 `container-registry` CLI 插件。

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. 验证 `container-registry` CLI 插件是否已成功卸载。

    ```
    ibmcloud plugin list
    ```
    {: pre}

    结果中不会显示 `container-registry` CLI 插件。

## 设置名称空间
{: #registry_namespace_setup}

必须创建名称空间才能在 {{site.data.keyword.registrylong_notm}} 中存储 Docker 映像。
{:shortdesc}

**开始之前**

- [安装 {{site.data.keyword.Bluemix_notm}} CLI 和 `container-registry` CLI 插件](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)。
- [规划如何使用注册表名称空间并为其命名](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces)。

创建名称空间；请参阅“入门”文档中的[设置名称空间](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add)。

现在，您可以[将 Docker 映像推送到 {{site.data.keyword.registrylong_notm}} 中的名称空间](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace)，并与帐户中的其他用户共享这些映像。

## 除去名称空间
{: #registry_remove}

如果不再需要某个注册表名称空间，那么可以从 {{site.data.keyword.Bluemix_notm}} 帐户除去该名称空间。
{:shortdesc}

1. 登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2. 列出可用的名称空间。

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. 除去名称空间。

    **注意：**除去名称空间时，还会删除存储在该名称空间中的所有映像。此操作无法撤销。

    将 `<my_namespace>` 替换为要除去的名称空间。

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    删除名称空间后，可能会花费几分钟，才可以复用该名称空间。

