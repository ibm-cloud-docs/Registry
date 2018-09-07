---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

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

有关使用论坛的更多详细信息，请参阅[使用支持中心](/docs/get-support/howtogetsupport.html#using-avatar)。

有关开具 {{site.data.keyword.IBM_notm}} 支持凭单的信息，或有关支持级别和凭单严重性的信息，请参阅[开具支持凭单](/docs/get-support/howtogetsupport.html#open-ticket)。

## 登录 {{site.data.keyword.registrylong_notm}} 失败
{: #ts_login}

无法登录 {{site.data.keyword.registrylong_notm}}。

{: tsSymptoms}
`ibmcloud cr login` 命令失败。

{: tsCauses}
-   容器注册表插件不是最新的，需要更新。
-   Docker 未安装在本地计算机上，或者未运行。
-   {{site.data.keyword.Bluemix_notm}} 登录凭证已到期。

{: tsResolve}
可以通过以下方式来解决此问题：

-   升级到 container-registry 插件的最新版本；请参阅[更新 container-registry 插件](registry_setup_cli_namespace.html#registry_cli_update)。
-   确保 Docker 安装在您的计算机上。如果已安装，请重新启动 Docker 守护程序。
-   重新运行 `ibmcloud login` 命令以刷新 {{site.data.keyword.Bluemix_notm}} 登录凭证。
  
## 无法运行任何 {{site.data.keyword.registrylong_notm}} 命令，消息为：`失败 您未登录到 IBM Cloud。` 
{: #ts_login_cloud}

尽管您已登录到 {{site.data.keyword.Bluemix_notm}}，还是无法运行任何 {{site.data.keyword.registrylong_notm}} 命令。

{: tsSymptoms}
所有 `ibmcloud cr` 命令都失败。

{: tsCauses}
-   容器注册表插件不是最新的，需要更新。

{: tsResolve}
可以通过以下方式来解决此问题：

-   升级到 container-registry 插件的最新版本；请参阅[更新 container-registry 插件](registry_setup_cli_namespace.html#registry_cli_update)。



## {{site.data.keyword.registrylong_notm}} 命令失败，消息为：`'cr' is not a registered command. See 'ibmcloud help'. `
{: #ts_login_error}

无法运行 `ibmcloud cr` 命令，因为 `cr` 不是注册的 `ibmcloud` 命令。

{: tsSymptoms}
您看到的错误消息类似于下列其中一个错误消息：

```
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

{: tsCauses}
-   未安装 container-registry 插件。


{: tsResolve}
可以通过以下方式来解决此问题：

-   安装 container-registry 插件；请参阅[安装 {{site.data.keyword.registryshort_notm}} CLI（container-registry 插件）](registry_setup_cli_namespace.html#registry_cli_install)。


## 设置名称空间失败
{: #ts_problem}

{: tsSymptoms}
运行 `ibmcloud cr namespace-add` 时，无法将输入的值设置为名称空间。

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
-   通过运行 `ibmcloud login` 登录到 {{site.data.keyword.Bluemix_notm}}。然后，通过运行 `ibmcloud cr login` 登录到 {{site.data.keyword.registrylong_notm}} CLI。
-   [查看在 {{site.data.keyword.registrylong_notm}} 中存储和拉出 Docker 映像的配额限制和使用量](registry_quota.html#registry_quota_get)。


## 无法使用 `latest` 标记拉出最新的映像
{: #ts_docker_latest}

{: tsSymptoms}
您尝试运行 `docker pull` 命令，但该命令返回的映像版本不是构建的最新版本。

{: tsCauses}
运行 Docker 命令而未指定标记值时，缺省情况下将应用 `latest` 标记来引用映像。`latest` 标记将应用于在未显式设置标记值的情况下运行的最新 `docker build` 或 `docker tag` 命令。因此，有可能按错误顺序运行 `docker` 命令或在某些映像上显式设置标记，并且 `latest` 标记有可能引用非最新的构建。

{: tsResolve}
一般情况下，最好每次都为映像显式定义不同的顺序标记，而不要依赖于 `latest` 标记。


## 无法将其他 IBM 映像添加到注册表
{: #ts_ppa}


{: tsSymptoms}
尝试导入您在其他 IBM 产品（例如，{{site.data.keyword.Bluemix_notm}} Private）中使用的内容时，无法将您的映像以及其他来自 [IBM Passport Advantage ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/passportadvantage/index.html) 的许可软件存储在注册表中。

{: tsCauses}
对于来自 IBM Passport Advantage 的软件包（例如，映像和 Helm 图表），必须使用 `ibmcloud cr ppa-archive-load` 命令将它们导入到注册表中。

{: tsResolve}
开始之前：
* 通过运行 `ibmcloud login [--sso]` 登录到 {{site.data.keyword.Bluemix_notm}}。
* 通过运行 `ibmcloud login` 登录到 {{site.data.keyword.registrylong_notm}}。
* [将 `kubectl` CLI 的目标设定为集群](/docs/containers/cs_cli_install.html#cs_cli_configure)。
* 如果尚未在集群中设置 Helm，请[立即在集群中设置 Helm](/docs/containers/cs_integrations.html#helm)。
* 如果要在组织内共享图表，可以安装 [Chart Museum 开放式源代码项目 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum)。有关指示信息，请参阅此 [developerWorks 诀窍 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/)。


### 导入 IBM Passport Advantage 产品以在 {{site.data.keyword.Bluemix_notm}} 中使用

1.  从 [IBM Passport Advantage ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/passportadvantage/index.html) 获取要导入的压缩文件。

2.  将要使用的区域设定为目标。如果您不知道区域名称，请运行不带区域的命令，然后选择区域。

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

3.  导入压缩归档文件。指定压缩文件的路径以及要将映像推送到的注册表名称空间。

    ```
    ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
    ```
    {: pre}

    此命令会解开压缩文件，将其中包含的所有映像都装入到本地 Docker 客户机中，然后将这些映像推送到注册表中的名称空间。
    
    如果要将 IBM Passport Advantage 归档中的 Helm 图表上传到 Chart Museum，请在命令中包含以下选项：`ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **示例输出**
    
    ```
user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

    OK
    ```
    {: screen}

4.  如果压缩文件包含 Helm 图表，这些图表会放在当前工作目录中创建的名为 `ppa-import` 的归档目录中。打开该目录以找到 Helm 图表名称 `<helm_chart>`，然后检查其值。

    ```
helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    如果在上一步中已将图表上传到 Chart Museum，可以使用 `helm inspect` 在 Chart Museum 中检查图表。
    {: tip}

5.  根据 `helm inspect values` 命令输出的值来配置 Helm 图表 `<helm_chart>`。

6.  使用 `helm install` 命令来部署 Helm 图表 `<helm_chart>`。可以根据需要使用 `--set` 选项来覆盖图表中的值。

    ```
helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## 使用定制防火墙访问注册表失败
{: #ts_firewall}

{: tsSymptoms}
您在开发环境中使用定制设置，为入站和出站网络流量设置附加防火墙。
尝试访问 {{site.data.keyword.registrylong_notm}} 时，连接失败。

{: tsCauses}
定制防火墙需要为入站和出站网络流量打开特定网络组，才能允许与注册表进行通信。


{: tsResolve}
在定制防火墙中打开以下网络组。

1.  记下要用于连接 {{site.data.keyword.registrylong_notm}} 的计算机的公共 IP 地址。如果您使用 Kubernetes，请使用工作程序节点的公共 IP 地址。
通过运行 `ibmcloud ks workers <cluster_name_or_id>`，检索工作程序节点的公共 IP 地址；其中，*&lt;cluster_name_or_id&gt;* 是集群的名称或标识。
2.  在防火墙中，允许与计算机进行以下连接：
    -   对于指向计算机的 INBOUND 连接，允许入局网络流量从以下源网络组流向计算机的目标公共 IP 地址。


        `registry.bluemix.net`：

        ```
169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

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

    -   对于来自计算机的 OUTBOUND 连接，使用相同的网络组并允许出局网络流量从计算机的源公共 IP 地址流向这些网络组。



## 恢复丢失或遭到破坏的密钥
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
使用[可信内容](registry_trusted_content.html)时，由于签名密钥丢失或遭到破坏，无法再管理可信映像。

{: tsCauses}
您的存储库密钥或根密钥已丢失或遭到破坏。

{: tsResolve}
用于恢复丢失或受影响密钥的选项取决于密钥的类型：存储库密钥或根密钥。

*  对于[存储库密钥](#trustedcontent_lostrepokey)，可以为存储库生成一组新的签名密钥。
*  对于[根密钥](#trustedcontent_lostrootkey)，可以请求删除存储库并创建新的存储库。


### 存储库密钥
{: #trustedcontent_lostrepokey}

如果存储库密钥丢失或遭到破坏，请生成一组新的存储库签名密钥。
{:shortdesc}

可以轮换的唯一签名角色是 `targets`，即存储库管理员。如果其他角色受到影响，请为这些角色生成新密钥，除去旧密钥，然后将新密钥添加为签署者。
{:tip}

开始之前，请先检索首次[推送签名的映像](registry_trusted_content.html#trustedcontent_push)时创建的根密钥口令。

1.  安装 [Notary 项目 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli) 的 CLI 版本。

2.  [设置可信内容环境](registry_trusted_content.html#trustedcontent_setup)。

3.  记下先前步骤中 export 命令中的 URL。例如，`https://registry.ng.bluemix.net:4443`。

4.  生成注册表令牌。

    ```
    ibmcloud cr token-add --readwrite
    ```
    {: pre}

5.	轮换密钥，以便不再信任已使用这些密钥签名的内容。将 _&lt;URL&gt;_ 替换为在步骤 2 中记录的 export 命令的 URL，并将 _&lt;image&gt;_ 替换为其存储库密钥受影响的映像。

    ```
notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	如果出现提示，请输入根密钥口令。然后，在提示时，输入新的根密钥口令用于新的存储库密钥。

7.	[推送签名的映像](registry_trusted_content.html#trustedcontent_push)，此映像将使用新的签名密钥。


### 根密钥
{: #trustedcontent_lostrootkey}

如果根密钥丢失或遭到破坏，您将无法更新使用该根密钥的任何可信内容存储库。
{:shortdesc}

可以[删除名称空间](registry_setup_cli_namespace.html#registry_remove)，即具有使用受影响根密钥的存储库的名称空间，这样将删除映像和信任数据。

如果名称空间包含使用不受影响的根密钥的存储库（例如，生产映像的名称空间），那么您可能希望仅删除与受影响的根密钥相关联的信任数据。请开具支持凭单。

1.  [联系 {{site.data.keyword.Bluemix_notm}} 支持](/docs/get-support/howtogetsupport.html#getting-customer-support)。请包含问题的简短描述和帐户标识，以及包含使用受影响根密钥的映像存储库的名称空间列表。

2.  {{site.data.keyword.Bluemix_notm}} 解决此问题后，请删除本地计算机上的 Docker Content Trust 存储库。

    * Linux 和 Mac 目录：`~/.docker/trust/private` 和 `~/.docker/trust/tuf`

    * Windows 目录：`%HOMEPATH%\.docker\trust\private` 和 `%HOMEPATH%\.docker\trust\tuf`

    因为根密钥受到影响，所以此步骤将删除所有签名密钥，包括其他信任服务器的签名密钥。
    {:tip}

3.  如果在 {{site.data.keyword.containershort_notm}} 集群中使用了 [{{site.data.keyword.Bluemix_notm}} Image Enforcement](registry_security_enforce.html)，请重新启动每个映像强制实施 pod。要触发 Kubernetes 自动对 pod 执行滚动重新启动，可以更改 pod 上的一些元数据。例如，[设定 Kubernetes CLI 的目标为集群](/docs/containers/cs_cli_install.html#cs_cli_configure)，然后修改部署。
    

    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  生成可信内容存储库。

    *  如果要创建新的可信内容，请[推送新的签名映像](registry_trusted_content.html#trustedcontent_push)。

    *  如果不想更改先前的可信内容，请将签名添加到注册表中的最新映像。

       ```
docker trust sign <image>:<tag>
       ```
       {: pre}
       

## Container Image Security Enforcement 安装失败，消息为：`helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists`
{: #ts_install_cise_fail}

{: tsSymptoms}
Container Image Security Enforcement 安装失败，并收到以下消息：

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
先前安装失败，后续卸载未除去与安装关联的所有 Kubernetes 作业。

{: tsResolve}
通过运行以下命令，除去剩余的 Kubernetes 作业：

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}


## 在所有工作程序停机后，Pod 不会重新启动
{: #ts_pods}


{: tsSymptoms}
在所有集群工作程序停机后，Pod 不会重新启动。部署 Container Image Security Enforcement。集群工作程序显示为正常运行，但是未安排任何项。

{: tsCauses}
缺省情况下，Container Image Security Enforcement 添加故障时关闭许可 Webhook。如果所有 Container Image Security Enforcement pod 停机，那么 pod 不可用于核准其自己的恢复。

{: tsResolve}
要恢复处于此状态的集群，必须更改 Webhook 配置以使其在发生故障时打开而不是关闭。 

您必须具有足够的基于角色的访问控制 (RBAC) 特权才能使用以下动词：
*  `GET`
*  `PATCH`

在以下资源上：
*  `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
*  `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration` 

有关 RBAC 的更多信息，请参阅[使用定制 Kubernetes RBAC 角色授权用户](/docs/containers/cs_users.html#rbac)和 [Kubernetes：使用 RBAC 授权 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)。

完成以下步骤以更改 Webhook 配置，从而使其在发生故障时打开而不是关闭，然后，在至少有一个 Container Image Security Enforcement pod 运行时，复原 Webhook 配置，从而使其在发生故障时关闭：

1.  通过运行以下命令更新 `MutatingWebhookConfiguration`：

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    将 `failurePolicy` 更改为 `Ignore`，保存并关闭。

2.  通过运行以下命令更新 `ValidatingWebhookConfiguration`：

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    将 `failurePolicy` 更改为 `Ignore`，保存并关闭。

3.  等待一些 Container Image Security Enforcement pod 启动。您可以通过运行以下命令检查 pod 是否已启动，直至看到至少一个 pod 的**状态**列显示 `Running`：

    ```
    kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
    ```
    {: pre}

4.  在至少有一个 Container Image Security Enforcement pod 运行时，通过运行以下命令更新 `MutatingWebhookConfiguration`：

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    将 `failurePolicy` 更改为 `Fail`，保存并关闭。

5.  通过运行以下命令更新 `ValidatingWebhookConfiguration`：

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    将 `failurePolicy` 更改为 `Fail`，保存并关闭。
