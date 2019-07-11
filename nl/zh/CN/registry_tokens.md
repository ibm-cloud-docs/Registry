---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

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

您可以使用 {{site.data.keyword.iamlong}} (IAM) API 密钥，自动访问 {{site.data.keyword.registrylong_notm}} 名称空间，以便可推送和拉出映像。
{:shortdesc}

要尝试在 Kubernetes 部署中使用注册表映像吗？请查看[访问其他 Kubernetes 名称空间、{{site.data.keyword.cloud_notm}} 区域和帐户中的映像](/docs/containers?topic=containers-images#other)。
{: tip}

API 密钥链接到您的帐户，可在 {{site.data.keyword.cloud_notm}} 中使用，从而不需要针对每种服务具有不同凭证。您可以在 CLI 中或者在自动化过程中使用 API 密钥，以使用您的用户身份登录。

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

## 认证选项（适用于所有客户机）
{: #registry_authentication}

您可以使用 `docker login` 命令或其他注册表客户机进行认证。
{:shortdesc}

大多数用户都可使用 `ibmcloud cr login` 命令来简化 `docker login`，但如果您是实施自动化或使用不同的客户机，那么可能需要手动认证。您必须提供用户名和密码。在 {{site.data.keyword.registrylong_notm}} 中，用户名会指示密码中提供的私钥类型。

以下用户名有效：

- `iambearer` 密码包含 IAM 访问令牌。此类型认证的有效时间较短，但可从所有类型的 IAM 身份派生。
- `iamrefresh` 密码必须包含在内部用于生成和刷新 IAM 访问令牌的 IAM 刷新令牌。此类型认证的有效时间较长，由 `ibmcloud cr login` 命令来使用。
- `iamapikey` 密码是 IAM API 密钥。此类型认证是实施自动化情况的首选类型。您可以使用用户或服务标识 API 密钥，请参阅[创建 API 密钥](#registry_api_key_create)。

您无需使用 `docker` 命令来向注册表进行认证。例如，您可以使用 Cloud Foundry CLI 通过注册表中的映像来启动 Cloud Foundry 应用程序：

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

将 `<apikey>` 替换为 API 密钥，将 `<region>` 替换为您的[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)名称，将 `<my_namespace>` 替换为名称空间，将 `<image_repo>` 替换为存储库。

有关更多信息，请参阅[使用专用映像注册表](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry)。
