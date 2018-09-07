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


# 自动访问 {{site.data.keyword.registrylong_notm}}
{: #registry_access}

您可以使用注册表令牌或 {{site.data.keyword.iamlong}} (IAM) API 密钥，自动访问 {{site.data.keyword.registrylong_notm}} 名称空间，以便可推送和拉出映像。
{:shortdesc}

要尝试在 Kubernetes 部署中使用注册表映像吗？请查看[访问其他 Kubernetes 名称空间、{{site.data.keyword.Bluemix_notm}} 区域和帐户中的映像](/docs/containers/cs_images.html#other)。
{: tip}

API 密钥链接到您的帐户，可在 {{site.data.keyword.Bluemix_notm}} 中使用，从而不需要针对每种服务具有不同凭证。您可以在 CLI 中或者在自动化过程中使用 API 密钥，以使用您的用户身份登录。

注册表令牌仅限定用于 {{site.data.keyword.registrylong_notm}}。您可以对其进行限制以仅具有只读访问权，可选择其是会过期还是不过期。

有关 {{site.data.keyword.registrylong_notm}} API 密钥的更多信息，请参阅[使用 API 密钥](/docs/iam/apikeys.html#manapikey)。

开始之前，[安装 {{site.data.keyword.registrylong_notm}} 和 Docker CLI](registry_setup_cli_namespace.html#registry_cli_install)。


## 使用 API 密钥自动访问名称空间
{: #registry_api_key}

您可以使用 API 密钥，将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。
{:shortdesc}

### 创建 API 密钥
{: #registry_api_key_create}

您可以创建 API 密钥，然后用于登录到注册表。
{:shortdesc}

创建 IAM API 密钥，请参阅[创建 API 密钥](/docs/iam/userid_keys.html#creating-an-api-key)。

### 使用 API 密钥自动访问
{: #registry_api_key_use}

您可以使用 API 密钥自动访问 {{site.data.keyword.registrylong_notm}} 中的名称空间。
{:shortdesc}

通过运行以下 Docker 命令，使用 API 密钥登录到注册表。将 &lt;your_apikey&gt; 替换为 API 密钥，将 &lt;registry_url&gt; 替换为在其中设置名称空间的注册表的 URL。

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

有关命令的参考信息，请参阅[创建新的 {{site.data.keyword.Bluemix_notm}} 平台 API 密钥](/docs/cli/reference/ibmcloud/cli_api_policy.html#ibmcloud_iam_api_key_create)。


## 使用令牌自动访问名称空间
{: #registry_tokens}

您可以使用令牌，将 Docker 映像自动推送到 {{site.data.keyword.registrylong_notm}} 名称空间，以及从名称空间自动拉出 Docker 映像。
{:shortdesc}

拥有注册表令牌的所有人都可访问安全信息。通过为 {{site.data.keyword.Bluemix_notm}} 帐户创建令牌，可以为您的 {{site.data.keyword.Bluemix_notm}} 帐户外的用户，授予对您在区域中所设置的所有名称空间的访问权。拥有此令牌的每一位用户或每一个应用程序都可以将映像推送到名称空间，以及从名称空间拉出映像，而无需安装 container-registry 插件。

为 {{site.data.keyword.Bluemix_notm}} 帐户创建令牌时，可以决定该令牌是授权对注册表的只读访问权（拉出）还是写访问权（推送和拉出）。您还可以指定令牌是永久性的还是在 24 小时后到期。您可以创建并使用多个令牌来控制不同类型的访问权。


使用以下任务管理令牌：

-  [为 {{site.data.keyword.Bluemix_notm}} 帐户创建令牌](#registry_tokens_create)
-  [使用令牌自动访问名称空间](#registry_tokens_use)
-  [从 {{site.data.keyword.Bluemix_notm}} 帐户除去令牌](#registry_tokens_remove)


### 为 {{site.data.keyword.Bluemix_notm}} 帐户创建令牌
{: #registry_tokens_create}

您可以创建令牌，以授予对区域中所有 {{site.data.keyword.registrylong_notm}} 名称空间的访问权。
{:shortdesc}

1.  创建令牌。以下示例创建非到期令牌，其具有对区域中所设置的所有名称空间的读写访问权。


    ```
    ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="灯泡图标"/> 了解此命令的组成部分</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>可选。使用此选项，可以描述令牌，以便您可以在稍后轻松地对其加以识别。</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>可选。使用此选项，可以创建非到期令牌。如果您未指定此选项，那么令牌将在 24 小时后失效。<br> **提示：**如果不再需要非到期令牌来阻止访问名称空间，请记得除去该令牌。</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>可选。使用此选项，可以创建令牌，以允许用户将映像推送到名称空间，以及从名称空间拉出映像。如果您未指定此选项，那么令牌仅可用于拉出映像。</td>
        </tr>
        </tbody>
        </table>

    您的 CLI 输出看起来与以下输出类似：

    ```
Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
   
    Token              <token_value>
    ```
    {: screen}

2.  验证已创建令牌。

    ```
    ibmcloud cr token-list
    ```
    {: pre}


### 使用令牌自动访问名称空间
{: #registry_tokens_use}

您可以在 `docker login` 命令中使用令牌，以自动访问 {{site.data.keyword.registrylong_notm}} 中的名称空间。
根据您为令牌设置的是只读还是读/写访问权，用户可以将映像推送到名称空间，以及从名称空间拉出映像。
{:shortdesc}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2.  列出 {{site.data.keyword.Bluemix_notm}} 帐户中的所有令牌，并记下要使用的令牌标识。

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  检索令牌的令牌值。将 &lt;token_id&gt; 替换为令牌的标识。


    ```
    ibmcloud cr token-get <token_id>
    ```
    {: pre}

    令牌值会显示在 CLI 输出的**令牌**中。

4.  将令牌用作 `docker login` 命令的一部分。将 &lt;token_value&gt; 替换为在上一步中检索到的令牌值，将 &lt;registry_url&gt; 替换为设置名称空间的注册表的 URL。

    -   对于在美国南部设置的名称空间：`registry.ng.bluemix.net`
    -   对于在英国南部设置的名称空间：`registry.eu-gb.bluemix.net`
    -   对于在欧洲中部设置的名称空间：`registry.eu-de.bluemix.net`
    -   对于在亚太南部设置的名称空间：`registry.au-syd.bluemix.net`

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}
    
    对于 `-u` 参数，请确保输入的是字符串 `token`，而不是令牌标识。
    {: tip}

    使用令牌登录到 Docker 后，就可以将映像推送到名称空间或从名称空间拉出映像。


### 从 {{site.data.keyword.Bluemix_notm}} 帐户除去令牌
{: #registry_tokens_remove}

不再需要 {{site.data.keyword.registrylong_notm}} 令牌时，请移除该令牌。
{:shortdesc}

到期的 {{site.data.keyword.registrylong_notm}} 令牌会自动从 {{site.data.keyword.Bluemix_notm}} 帐户除去，而无需手动除去。
{:tip}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2.  列出 {{site.data.keyword.Bluemix_notm}} 帐户中的所有令牌，并记下要除去的令牌标识。

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  除去令牌。

    ```
    ibmcloud cr token-rm <token_id>
    ```
    {: pre}
