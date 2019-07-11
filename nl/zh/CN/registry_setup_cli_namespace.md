---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

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

要管理 {{site.data.keyword.registrylong}} 中的 Docker 映像，您必须安装 `container-registry` CLI 插件并创建名称空间。
{:shortdesc}

不要将个人信息放入容器映像、名称空间名称、描述字段或任何映像配置数据（例如，映像名称或映像标签）中。
{: important}

开始之前，安装 {{site.data.keyword.cloud_notm}} CLI，具体请参阅 [{{site.data.keyword.cloud_notm}} CLI 使用入门](/docs/cli?topic=cloud-cli-getting-started)。

## 安装 `container-registry` CLI 插件
{: #cli_namespace_registry_cli_install}

安装 `container-registry` CLI 插件，以使用命令行在 {{site.data.keyword.registrylong_notm}} 中管理名称空间和 Docker 映像。
{:shortdesc}

1. [安装 `container-registry` CLI 插件](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)。
2. 可选：[配置 Docker 客户机以在没有 root 用户许可权的情况下运行命令 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.docker.com/install/linux/linux-postinstall/)。如果未执行此步骤，那么必须以 `sudo` 或以 root 用户身份运行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 和 `docker push` 命令。

现在，您可以在 {{site.data.keyword.registrylong_notm}} 中设置您自己的[名称空间](#registry_namespace_setup)。

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

## 规划名称空间
{: #registry_setup_cli_namespace_plan}

{{site.data.keyword.registrylong_notm}} 提供由 IBM 托管和管理的多租户专用映像注册表。
您可以通过设置注册表名称空间，在此注册表中存储和共享 Docker 映像。
{:shortdesc}

例如，您可以设置多个名称空间，以针对生产和打包编译环境具有不同的存储库。
如果要在多个 {{site.data.keyword.cloud_notm}} 区域中使用注册表，那么必须为每个区域设置名称空间。
在区域中，名称空间名称是唯一的。您可以对每个区域使用相同的名称空间名称，除非别人已经在该区域中设置了使用该名称的名称空间。

您可以使用 IAM 策略来控制对名称空间的访问权。有关更多信息，请参阅[定义用户访问角色策略](/docs/services/Registry?topic=registry-user#user)。

要仅使用 IBM 提供的公共映像，您无需设置名称空间。

如果您不确定是否已为帐户设置名称空间，请运行 `ibmcloud cr namespace-list` 命令以检索现有名称空间信息。
{:tip}

选择名称空间时，请考虑以下规则：


- 您的名称空间在同一区域的所有 {{site.data.keyword.cloud_notm}} 帐户中必须唯一。
- 您的名称空间必须为 4 - 30 个字符。
- 您的名称空间必须以字母或数字开头和结尾。
- 您的名称空间必须只包含小写字母、数字、连字符 (-) 和下划线 (_)。

不要将个人信息放入名称空间名称中。
{: important}

设置第一个名称空间后，如果您尚未[升级套餐](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade)，那么为您分配的是免费的 {{site.data.keyword.registrylong_notm}} 服务套餐。

## 设置名称空间
{: #registry_namespace_setup}

必须创建名称空间才能在 {{site.data.keyword.registrylong_notm}} 中存储 Docker 映像。
{:shortdesc}

**开始之前**

- [安装 {{site.data.keyword.cloud_notm}} CLI 和 `container-registry` CLI 插件](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)。
- [规划如何使用注册表名称空间并为其命名](#registry_setup_cli_namespace_plan)。

要创建名称空间，请参阅“入门”文档中的[设置名称空间](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add)。

名称空间在同一区域的所有 {{site.data.keyword.cloud_notm}} 帐户中必须唯一。名称空间必须具有 4 到 30 个字符，并且只能包含小写字母、数字、连字符 (-) 和下划线 (_)。名称空间必须以字母或数字开头和结尾。
{: tip}

现在，您可以[将 Docker 映像推送到 {{site.data.keyword.registrylong_notm}} 中的名称空间](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace)，并与帐户中的其他用户共享这些映像。要控制对 {{site.data.keyword.cloud_notm}} IAM 中名称空间的访问权，请参阅[创建策略](/docs/services/Registry?topic=registry-user#create)。

## 除去名称空间
{: #registry_remove}

如果不再需要某个注册表名称空间，那么可以从 {{site.data.keyword.cloud_notm}} 帐户除去该名称空间。
{:shortdesc}

1. 登录到 {{site.data.keyword.cloud_notm}}。

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

    将 `<my_namespace>` 替换为您想要除去的名称空间。

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    删除名称空间后，可能会花费几分钟，才可以复用该名称空间。

