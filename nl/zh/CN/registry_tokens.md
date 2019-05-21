---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

# 自动访问 {{site.data.keyword.registrylong_notm}}
{: #registry_access}

您可以使用注册表令牌或 {{site.data.keyword.iamlong}} (IAM) API 密钥，自动访问 {{site.data.keyword.registrylong_notm}} 名称空间，以便可推送和拉出映像。
{:shortdesc}

要尝试在 Kubernetes 部署中使用注册表映像吗？请查看[访问其他 Kubernetes 名称空间、{{site.data.keyword.cloud_notm}} 区域和帐户中的映像](/docs/containers?topic=containers-images#other)。
{: tip}

API 密钥链接到您的帐户，可在 {{site.data.keyword.cloud_notm}} 中使用，从而不需要针对每种服务具有不同凭证。您可以在 CLI 中或者在自动化过程中使用 API 密钥，以使用您的用户身份登录。

注册表令牌仅限定用于 {{site.data.keyword.registrylong_notm}}。您可以对其进行限制以仅具有只读访问权，可选择其是会过期还是不过期。

如果使用 API 密钥，那么可以通过 IAM 策略来控制对名称空间的访问权。有关更多信息，请参阅[定义用户访问角色策略](/docs/services/Registry?topic=registry-user#user)。

有关 {{site.data.keyword.registrylong_notm}} API 密钥的更多信息，请参阅[使用 API 密钥](/docs/iam?topic=iam-manapikey#manapikey)。

开始之前，[安装 {{site.data.keyword.registrylong_notm}} 和 Docker CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)。

## 使用 API 密钥自动访问名称空间
{: #registry_api_key}

您可以使用 API 密钥，将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。
{:shortdesc}

### 创建 API 密钥
{: #registry_api_key_create}

您可以创建 API 密钥，然后用于登录到注册表。
{:shortdesc}

您可以创建用户 API 密钥和服务标识 API 密钥。

- 要创建服务标识 API 密钥，请参阅[为服务标识创建 API 密钥](/docs/iam?topic=iam-serviceidapikeys#create_service_key)。
- 要创建用户 API 密钥，请参阅[创建 API 密钥](/docs/iam?topic=iam-userapikey#create_user_key)。

### 使用 API 密钥自动访问
{: #registry_api_key_use}

您可以使用 API 密钥自动访问 {{site.data.keyword.registrylong_notm}} 中的名称空间。
{:shortdesc}

通过运行以下 Docker 命令，使用 API 密钥登录到注册表。将 `<your_apikey>` 替换为您的 API 密钥，将 `<registry_url>` 替换为在其中设置名称空间的注册表的 URL。

- 对于在亚太北部设置的名称空间，请使用 `jp.icr.io`
- 对于在亚太南部设置的名称空间，请使用 `au.icr.io`
- 对于在欧洲中部设置的名称空间，请使用 `de.icr.io`
- 对于在英国南部设置的名称空间，请使用 `uk.icr.io`
- 对于在美国南部设置的名称空间，请使用 `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

有关命令的参考信息，请参阅[创建新的 {{site.data.keyword.cloud_notm}} 平台 API 密钥](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create)。

## 使用令牌自动访问名称空间（不推荐）
{: #registry_tokens}

您可以使用令牌，将 Docker 映像自动推送到 {{site.data.keyword.registrylong_notm}} 名称空间，以及从名称空间自动拉出 Docker 映像。
{:shortdesc}

不推荐使用令牌将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。请改为使用 API 密钥自动访问名称空间，具体请参阅[使用 API 密钥自动访问名称空间](#registry_api_key)。
{: deprecated}

拥有注册表令牌的所有人都可访问安全信息。如果您希望您的 {{site.data.keyword.cloud_notm}} 帐户外的用户能够访问您在区域中设置的所有名称空间，那么可以为您的帐户创建令牌。拥有此令牌的每一位用户或每一个应用程序都可以将映像推送到名称空间，以及从名称空间拉出映像，而无需安装 `container-registry` CLI 插件。

为 {{site.data.keyword.cloud_notm}} 帐户创建令牌时，可以决定该令牌是授权对注册表的只读访问权（拉出）还是写访问权（推送和拉出）。您还可以指定令牌是永久性的还是在 24 小时后到期。您可以创建并使用多个令牌来控制不同类型的访问权。


如果是使用注册表令牌登录到 {{site.data.keyword.registrylong_notm}}，那么不会强制实施 IAM 访问策略。如果要限制对自动化中使用的标识的一个或多个名称空间的访问，请考虑使用 IAM 服务标识 API 密钥，而不使用注册表令牌。有关创建 API 密钥并将其用于 {{site.data.keyword.registrylong_notm}} 的更多信息，请参阅[使用 API 密钥自动访问名称空间](#registry_api_key)。

使用以下任务管理令牌：

- [为 {{site.data.keyword.cloud_notm}} 帐户创建令牌](#registry_tokens_create)
- [使用令牌自动访问名称空间](#registry_tokens_use)
- [从 {{site.data.keyword.cloud_notm}} 帐户除去令牌](#registry_tokens_remove)

### 为 {{site.data.keyword.cloud_notm}} 帐户创建令牌（不推荐）
{: #registry_tokens_create}

您可以创建令牌，以授予对区域中所有 {{site.data.keyword.registrylong_notm}} 名称空间的访问权。
{:shortdesc}

不推荐使用令牌将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。请改为使用 API 密钥自动访问名称空间，具体请参阅[使用 API 密钥自动访问名称空间](#registry_api_key)。
{: deprecated}

1. 创建令牌。以下示例创建非到期令牌，其具有对区域中所设置的所有名称空间的读写访问权。


   ```
    ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
    ```
   {: pre}

   <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="灯泡图标"/> 了解此命令的组成部分</th>
        </thead>
          <caption>表 1. `ibmcloud cr token-add` 命令的组成部分</caption>
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
   Token              eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJpYm0uY29tIiwibmFtZSI6Ikdpbm5pIFJvbWV0dHkiLCJpYXQiOjE1NDYzMDA4MDB9.wYMmTPHmrqhyHtgw5T8lbl1hxr2ykHq5T5s3mvMxjDw
   ```
   {: screen}

2. 验证已创建令牌。

   ```
    ibmcloud cr token-list
    ```
   {: pre}

### 使用令牌自动访问名称空间（不推荐）
{: #registry_tokens_use}

您可以在 `docker login` 命令中使用令牌，以自动访问 {{site.data.keyword.registrylong_notm}} 中的名称空间。
根据您为令牌设置的是只读还是读/写访问权，用户可以将映像推送到名称空间，以及从名称空间拉出映像。
{:shortdesc}

不推荐使用令牌将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。请改为使用 API 密钥自动访问名称空间，具体请参阅[使用 API 密钥自动访问名称空间](#registry_api_key)。
{: deprecated}

1. 登录到 {{site.data.keyword.cloud_notm}}。

   ```
    ibmcloud login
    ```
   {: pre}

2. 列出 {{site.data.keyword.cloud_notm}} 帐户中的所有令牌，并记下要使用的令牌标识。

   ```
    ibmcloud cr token-list
    ```
   {: pre}

3. 检索令牌的令牌值。将 `<token_id>` 替换为令牌的标识。

   ```
    ibmcloud cr token-get <token_id>
    ```
   {: pre}

    令牌值会显示在 CLI 输出的**令牌**中。

4. 将令牌用作 `docker login` 命令的一部分。将 `<token_value>` 替换为在上一步中检索到的令牌值，将 `<registry_url>` 替换为设置名称空间的注册表的 URL。

   - 对于在亚太北部设置的名称空间，请使用 `jp.icr.io`
   - 对于在亚太南部设置的名称空间，请使用 `au.icr.io`
   - 对于在欧洲中部设置的名称空间，请使用 `de.icr.io`
   - 对于在英国南部设置的名称空间，请使用 `uk.icr.io`
   - 对于在美国南部设置的名称空间，请使用 `us.icr.io`

   ```
    docker login -u token -p <token_value> <registry_url>
    ```
   {: pre}

   对于 `-u` 参数，请确保输入的是字符串 `token`，而不是令牌标识。
    {: tip}

   使用令牌登录到 Docker 后，就可以将映像推送到名称空间或从名称空间拉出映像。

### 从 {{site.data.keyword.cloud_notm}} 帐户中除去令牌（不推荐）
{: #registry_tokens_remove}

不再需要 {{site.data.keyword.registrylong_notm}} 令牌时，请除去该令牌。
{:shortdesc}

不推荐使用令牌将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。请改为使用 API 密钥自动访问名称空间，具体请参阅[使用 API 密钥自动访问名称空间](#registry_api_key)。
{: deprecated}

到期的 {{site.data.keyword.registrylong_notm}} 令牌会自动从 {{site.data.keyword.cloud_notm}} 帐户除去，而无需手动除去。
{:tip}

1. 登录到 {{site.data.keyword.cloud_notm}}。

   ```
    ibmcloud login
    ```
   {: pre}

2. 列出 {{site.data.keyword.cloud_notm}} 帐户中的所有令牌，并记下要除去的令牌标识。

   ```
    ibmcloud cr token-list
    ```
   {: pre}

3. 除去令牌。

   ```
    ibmcloud cr token-rm <token_id>
    ```
   {: pre}

## 认证选项（适用于所有客户机）
{: #registry_authentication}

您可以使用 `docker login` 命令或其他注册表客户机进行认证。
{:shortdesc}

大多数用户都可使用 `ibmcloud cr login` 命令来简化 `docker login`，但如果您是实施自动化或使用不同的客户机，那么可能需要手动认证。您必须提供用户名和密码。在 {{site.data.keyword.registrylong_notm}} 中，用户名会指示密码中提供的私钥类型。

以下用户名有效：

- `iambearer` 密码包含 IAM 访问令牌。此类型认证的有效时间较短，但可从所有类型的 IAM 身份派生。
- `iamrefresh` 密码必须包含在内部用于生成和刷新 IAM 访问令牌的 IAM 刷新令牌。此类型认证的有效时间较长，由 `ibmcloud cr login` 命令来使用。
- `iamapikey` 密码是 IAM API 密钥。此类型认证是实施自动化情况的首选类型。您可以使用用户或服务标识 API 密钥，请参阅[创建 API 密钥](#registry_api_key_create)。
- `token` （不推荐）该密码是注册表令牌。您可以使用此用户名来实施自动化。

  不推荐使用令牌将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。请改为使用 API 密钥自动访问名称空间，具体请参阅[使用 API 密钥自动访问名称空间](#registry_api_key)。
  {: deprecated}

您无需使用 `docker` 命令来向注册表进行认证。例如，您可以使用 Cloud Foundry CLI 通过注册表中的映像来启动 Cloud Foundry 应用程序：

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

将 `<apikey>` 替换为 API 密钥，将 `<region>` 替换为您的[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)名称，将 `<my_namespace>` 替换为名称空间，将 `<image_repo>` 替换为存储库。

有关更多信息，请参阅[使用专用映像注册表](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry)。
