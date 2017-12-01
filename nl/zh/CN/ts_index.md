---

copyright:
  years: 2017
lastupdated: "2017-10-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# 故障诊断
{: #ts_index}

以下是关于使用 {{site.data.keyword.registrylong}} 的常见故障诊断问题的解答。
{:shortdesc}


## 获取有关 {{site.data.keyword.registrylong_notm}} 的帮助和支持
{: #gettinghelp}

如果您在使用 {{site.data.keyword.registrylong_notm}} 时遇到问题或有疑问，可以通过在论坛中搜索相关信息或提问来获取帮助。您还可以开具 {{site.data.keyword.IBM_notm}} 支持凭单。

使用论坛提问时，请标记您的问题，以使其可由 {{site.data.keyword.registrylong_notm}} 开发团队看到。

-   如果有使用 {{site.data.keyword.registrylong_notm}} 开发或部署应用程序相关的技术问题，请在 [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) 上发布问题，并使用 `ibm-bluemix` 和 `container-registry` 标记您的问题。
-   有关服务和入门指示信息的问题，请使用 [IBM developerWorks dWAnswers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) 论坛。请包含 `bluemix` 和 `container-registry` 标记。

有关使用论坛的更多详细信息，请参阅[获取帮助](../../support/index.html#getting-help)。

有关开具 {{site.data.keyword.IBM_notm}} 支持凭单的信息，或有关支持级别和凭单严重性的信息，请参阅[联系支持人员](../../support/index.html#contacting-support)。

## 登录 {{site.data.keyword.registrylong_notm}} 失败
{: #ts_login}

无法登录 {{site.data.keyword.registrylong_notm}}。

{: tsSymptoms}
`bx cr login` 命令失败。

{: tsCauses}
-   容器注册表插件不是最新的，需要更新。
-   Docker 未安装在本地计算机上，或者未运行。
-   {{site.data.keyword.Bluemix_notm}} 登录凭证已到期。

{: tsResolve}
可以通过以下方式来解决此问题：

-   升级到 {{site.data.keyword.registryshort_notm}} 插件的最新版本；请参阅[更新 {{site.data.keyword.registrylong_notm}} (`bx cr`) 插件](registry_setup_cli_namespace.html#registry_cli_update)。
-   确保 Docker 安装在您的机器上。如果已安装，请重新启动 Docker 守护程序。
-   重新运行 `bx login` 命令以刷新 {{site.data.keyword.Bluemix_notm}} 登录凭证。


## {{site.data.keyword.registrylong_notm}} 命令失败，消息为：`'cr' is not a registered command. See 'bx help'. `
{: #ts_login_error}

无法运行`bx cr` 命令，因为 `cr` 不是注册的 `bx` 命令。

{: tsSymptoms}
您看到的错误消息类似于下列其中一个错误消息： 

```
bx cr login
'cr' is not a registered command. See 'bx help'.
```
{: pre}

```
bx cr namespace
'cr' is not a registered command. See 'bx help'.
```
{: pre}

{: tsCauses}
-   未安装 container-registry 插件。


{: tsResolve}
可以通过以下方式来解决此问题：

-   安装 container-registry 插件；请参阅[安装 {{site.data.keyword.registryshort_notm}} CLI (bx cr) 插件](registry_setup_cli_namespace.html#registry_cli_install)。


## 设置名称空间失败
{: #ts_problem}

{: tsSymptoms}
运行 `bx cr namespace-add` 时，无法将输入的值设置为名称空间。

{: tsCauses}
-   输入的名称空间值已经由其他 {{site.data.keyword.Bluemix_notm}} 组织在使用。
-   某个名称空间最近已删除，而您复用的是该名称空间的名称。如果已删除的名称空间包含大量资源，那么 {{site.data.keyword.registrylong_notm}} 可能尚未完全处理完删除操作。
-   在名称空间值中使用了无效字符。

{: tsResolve}
可以通过以下方式来解决此问题：

-   按照返回的错误消息中显示的所有指示信息进行操作。
-   检查输入的名称空间是否有效：
    -   名称空间的长度必须为 4 - 30 个字符。
    -   名称空间必须至少以一个字母或数字开头。
    -   名称空间必须只包含小写字母、数字或下划线 (_)。
-   为名称空间选择其他值。
-   如果要重新创建已删除的名称空间，而该名称空间含有大量映像，请稍后重试。

## 推送或拉出 Docker 映像失败
{: #ts_pushpull}

{: tsSymptoms}
运行命令来推送或拉出 Docker 映像时，收到错误消息。错误消息会依据根本原因而变化。潜在的错误消息可能为：


```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan
```
{: screen}

```
You have exceeded your pull traffic quota for the current month. Review your pull traffic quota and pricing plan
```
{: screen}

```
unauthorized: authentication required
```
{: screen}

```
denied: requested access to the resource is denied
```
{: screen}

{: tsCauses}
-   Docker 未安装。
-   Docker 客户机未登录到 {{site.data.keyword.registrylong_notm}}。
-   {{site.data.keyword.Bluemix_notm}} 访问令牌可能已到期。
-   超过了为 {{site.data.keyword.Bluemix_notm}} 帐户设置的存储量或拉出流量的配额限制。

{: tsResolve}
可以通过以下方式来解决此问题：

-   [确保已在计算机上安装 Docker](index.html#registry_cli_install)。
-   检查 Docker 安装路径。
-   通过运行 `bx login` 登录到 {{site.data.keyword.Bluemix_notm}}。然后，通过运行 `bx cr login` 登录到 {{site.data.keyword.registrylong_notm}} CLI。
-   [查看在 {{site.data.keyword.registrylong_notm}} 中存储和拉出 Docker 映像的配额限制和使用量](registry_quota.html#registry_quota_get)。

## 无法使用 latest 标记拉出最新的映像
{: #ts_docker_latest}

{: tsSymptoms}
您尝试运行 `docker pull` 命令，但该命令返回的映像版本不是构建的最新版本。

{: tsCauses}
运行 Docker 命令而未指定标记值时，缺省情况下将应用 `latest` 标记来引用映像。`latest` 标记将应用于在未显式设置标记值的情况下运行的最新 `docker build` 或 `docker tag` 命令。因此，有可能按错误顺序运行 `docker` 命令或在某些映像上显式设置标记，并且 `latest` 标记有可能引用非最新的构建。

{: tsResolve}
一般情况下，最好每次都为映像显式定义不同的顺序标记，而不要依赖于 `latest` 标记。

## 使用定制防火墙访问注册表失败
{: #ts_firewall}

{: tsSymptoms}
您在开发环境中使用定制设置，为入站和出站网络流量设置附加防火墙。
尝试访问 {{site.data.keyword.registrylong_notm}} 时，连接失败。

{: tsCauses}
定制防火墙需要为入站和出站网络流量打开特定网络组，才能允许与注册表进行通信。


{: tsResolve}
在定制防火墙中打开以下网络组。

1.  记下要用于连接 {{site.data.keyword.registrylong_notm}} 的机器的公共 IP 地址。如果您使用 Kubernetes，请使用工作程序节点的公共 IP 地址。
通过运行 `bx cs workers <cluster_name_or_id>`，检索工作程序节点的公共 IP 地址；其中，*&lt;cluster_name_or_id&gt;* 是集群的名称或标识。
2.  在防火墙中，允许与机器进行以下连接：
    -   对于指向机器的 INBOUND 连接，允许入局网络流量从以下源网络组流向机器的公共 IP 地址。


        `registry.au-syd.bluemix.net`：

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`：

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`：

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`：

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   对于来自机器的 OUTBOUND 连接，使用相同的网络组并允许出局网络流量从机器的源公共 IP 地址流向这些网络组。


