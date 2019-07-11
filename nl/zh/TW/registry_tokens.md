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

# 自動化 {{site.data.keyword.registrylong_notm}} 的存取
{: #registry_access}

您可以使用 {{site.data.keyword.iamlong}} (IAM) API 金鑰來自動化 {{site.data.keyword.registrylong_notm}} 名稱空間的存取，以推送及取回映像檔。
{:shortdesc}

您嘗試在 Kubernetes 部署中使用您的登錄映像檔嗎？請參閱[存取其他 Kubernetes 名稱空間、{{site.data.keyword.cloud_notm}} 地區及帳戶中的映像檔](/docs/containers?topic=containers-images#other)。
{: tip}

API 金鑰與您的帳戶鏈結，可跨 {{site.data.keyword.cloud_notm}} 使用，因此您不需要為每一個服務提供不同的認證。您可以在 CLI 中使用 API 金鑰，也可以在以您的使用者身分自動登入的過程中使用。

如果您使用 API 金鑰，則可以使用 IAM 原則來控制對名稱空間的存取權。如需相關資訊，請參閱[定義使用者存取角色原則](/docs/services/Registry?topic=registry-user#user)。

如需 {{site.data.keyword.registrylong_notm}} API 金鑰的相關資訊，請參閱[使用 API 金鑰](/docs/iam?topic=iam-manapikey#manapikey)。

開始之前，請[安裝 {{site.data.keyword.registrylong_notm}} 及 Docker CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)。

## 使用 API 金鑰自動化名稱空間的存取
{: #registry_api_key}

您可以使用 API 金鑰，以自動化將 Docker 映像檔推送至名稱空間以及從其中取回 Docker 映像檔的作業。
{:shortdesc}

### 建立 API 金鑰
{: #registry_api_key_create}

您可以建立 API 金鑰，之後就可以用來登入您的登錄。
{:shortdesc}

您可以建立使用者 API 金鑰及服務 ID API 金鑰。

- 若要建立服務 ID API 金鑰，請參閱[建立服務 ID 的 API 金鑰](/docs/iam?topic=iam-serviceidapikeys#create_service_key)。
- 若要建立使用者 API 金鑰，請參閱[建立 API 金鑰](/docs/iam?topic=iam-userapikey#create_user_key)。

### 使用 API 金鑰以自動化存取
{: #registry_api_key_use}

您可以使用 API 金鑰，以自動化 {{site.data.keyword.registrylong_notm}} 名稱空間的存取。
{:shortdesc}

請執行下列 Docker 指令，以使用 API 金鑰登入您的登錄。將 `<your_apikey>` 取代為您的 API 金鑰，並將 `<registry_url>` 取代為已設定名稱空間之登錄的 URL。

- 針對亞太地區北部中所設定的名稱空間，使用 `jp.icr.io`
- 針對亞太地區南部中所設定的名稱空間，使用 `au.icr.io`
- 針對歐盟中部中所設定的名稱空間，使用 `de.icr.io`
- 針對英國南部中所設定的名稱空間，使用 `uk.icr.io`
- 針對美國南部中所設定的名稱空間，使用 `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

如需指令的相關參考資訊，請參閱[建立新的 {{site.data.keyword.cloud_notm}} 平台 API 金鑰](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create)。

## 所有用戶端的鑑別選項
{: #registry_authentication}

您可以使用 `docker login` 指令或其他登錄用戶端來進行鑑別。
{:shortdesc}

大部分使用者可以使用 `ibmcloud cr login` 指令，以簡化 `docker login`，但如果您實作自動化，或是您使用不同的用戶端，則建議您進行手動鑑別。您必須提出使用者名稱及密碼。在 {{site.data.keyword.registrylong_notm}} 中，使用者名稱指出在密碼 (password) 中所呈現的密碼 (secret) 類型。

以下是有效的使用者名稱：

- `iambearer` 密碼包含 IAM 存取記號。這種鑑別存在時間很短，但可以從所有類型的 IAM 身分衍生。
- `iamrefresh` 密碼必須包含 IAM 重新整理記號，其在內部用來產生及重新整理 IAM 存取記號。這種鑑別存在時間較長，並且由 `ibmcloud cr login` 指令使用。
- `iamapikey` 密碼是一個 IAM API 金鑰。這種鑑別是自動化的偏好類型。您可以使用使用者或服務 ID API 金鑰，請參閱[建立 API 金鑰](#registry_api_key_create)。

您不需要使用 `docker` 指令即可向登錄進行鑑別。例如，您可以使用 Cloud Foundry CLI，從登錄的映像檔中啟動 Cloud Foundry 應用程式：

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

請將 `<apikey>` 取代為您的 API 金鑰、將 `<region>` 取代為[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)的名稱、將 `<my_namespace>` 取代為名稱空間，以及將 `<image_repo>` 取代為儲存庫。

如需相關資訊，請參閱[使用專用映像檔登錄](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry)。
