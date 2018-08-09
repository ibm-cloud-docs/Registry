---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 设置 {{site.data.keyword.registrylong_notm}} CLI 和注册表名称空间
{: #registry_setup_cli_namespace}

必须在 {{site.data.keyword.registrylong}} 中安装 {{site.data.keyword.Bluemix_notm}} CLI 和 container-registry 插件，并设置注册表名称空间以创建自己的映像存储库，然后才能在 {{site.data.keyword.registrylong_notm}} 中存储 Docker 映像。
{:shortdesc}

不要将个人信息放入容器映像、名称空间名称、描述字段（例如，注册表令牌）或任何映像配置数据（例如，映像名称或映像标签）中。
{:tip}

开始之前，安装 [{{site.data.keyword.Bluemix_notm}} CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://clis.ng.bluemix.net/ui/home.html)。


## 安装 {{site.data.keyword.registrylong_notm}} CLI（container-registry 插件）
{: #registry_cli_install}

安装 {{site.data.keyword.registrylong_notm}} CLI，以使用命令行，在 {{site.data.keyword.Bluemix_notm}} 专用注册表中管理名称空间和 Docker 映像。
{:shortdesc}

1.  [安装 container-registry 插件。](index.html#registry_cli_install)
2.  可选：[配置 Docker 客户机以在没有 root 用户许可权的情况下运行命令](https://docs.docker.com/engine/installation/linux/linux-postinstall)。如果未执行此步骤，那么必须以 `sudo` 或以 root 用户身份运行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 和 **docker push** 命令。

现在，您可以在 {{site.data.keyword.registrylong_notm}} 专用注册表中设置自己的名称空间。

## 更新 container-registry 插件
{: #registry_cli_update}

您可能希望定期更新 {{site.data.keyword.registrylong_notm}} CLI 以使用新功能。
{:shortdesc}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2.  更新 container-registry 插件。

    ```
    ibmcloud plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  验证插件是否已成功更新。

    ```
    ibmcloud plugin list
    ```
     {: pre}


## 卸载 container-registry 插件
{: #registry_cli_uninstall}

如果不再需要 container-registry 插件，可以将其卸载。
{:shortdesc}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2.  卸载 container-registry 插件。

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

3.  验证插件是否已成功卸载。

    ```
    ibmcloud plugin list
    ```
    {: pre}

    结果中不会显示 container-registry 插件。


## 设置名称空间
{: #registry_namespace_add}

要安全地存储 Docker 映像，您必须在 {{site.data.keyword.registrylong_notm}} 专用注册表中创建名称空间。
{:shortdesc}

开始之前：

-   [安装 {{site.data.keyword.Bluemix_notm}} CLI 和容器注册表插件](#registry_cli_install)。
-   [规划如何使用注册表名称空间并为其命名](registry_overview.html#registry_namespaces)。

创建名称空间；请参阅“入门”文档中的[设置名称空间](index.html#registry_namespace_add)。

现在，您可以[将 Docker 映像推送至 {{site.data.keyword.Bluemix_notm}} 注册表中的名称空间](registry_images_.html#registry_images_pushing)，并与帐户中的其他用户共享这些映像。


## 除去名称空间
{: #registry_remove}

如果不再需要某个注册表名称空间，那么可以从 {{site.data.keyword.Bluemix_notm}} 帐户除去该名称空间。
{:shortdesc}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2.  列出可用的名称空间。

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3.  除去名称空间。

    **注意：**除去名称空间时，还会删除存储在该名称空间中的所有映像。此操作无法撤销。

    将 _&lt;my_namespace&gt;_ 替换为要除去的名称空间。


    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    删除名称空间后，根据所存储的映像数，可能会花费几分钟，才可以复用该名称空间。

