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

# {{site.data.keyword.registrylong_notm}}에 대한 액세스 자동화
{: #registry_access}

이미지를 푸시하고 가져올 수 있도록 {{site.data.keyword.iamlong}}(IAM) API 키를 사용하여 {{site.data.keyword.registrylong_notm}} 네임스페이스에 대한 액세스를 자동화할 수 있습니다.
{:shortdesc}

Kubernetes 배치에서 레지스트리 이미지를 사용하시겠습니까? [기타 Kubernetes 네임스페이스, {{site.data.keyword.cloud_notm}} 지역 및 계정의 이미지에 액세스](/docs/containers?topic=containers-images#other)를 확인하십시오.
{: tip}

API 키가 계정에 연결되고 {{site.data.keyword.cloud_notm}}에서 사용할 수 있으므로 각 서비스에 대해 다른 인증 정보가 필요하지 않습니다. CLI에서 API 키를 사용하거나 사용자 ID로 로그인하기 위한 자동화의 일부로 API 키를 사용할 수 있습니다.

API 키를 사용하는 경우 IAM 정책을 사용하여 네임스페이스에 대한 액세스를 제어할 수 있습니다. 자세한 정보는 [사용자 액세스 역할 정책 정의](/docs/services/Registry?topic=registry-user#user)를 참조하십시오.

{{site.data.keyword.registrylong_notm}} API 키에 대한 자세한 정보는 [API 키 작업](/docs/iam?topic=iam-manapikey#manapikey)을 참조하십시오.

시작하기 전에 [{{site.data.keyword.registrylong_notm}} 및 Docker CLI를 설치](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)하십시오.

## API 키를 사용하여 네임스페이스에 대한 액세스 자동화
{: #registry_api_key}

API 키를 사용하여 네임스페이스에 대한 Docker 이미지의 푸시 및 가져오기를 자동화할 수 있습니다.
{:shortdesc}

### API 키 작성
{: #registry_api_key_create}

API 키를 작성한 후 레지스트리에 로그인하는 데 사용할 수 있습니다.
{:shortdesc}

사용자 API 키와 서비스 ID API 키를 둘 다 작성할 수 있습니다.

- 서비스 ID API 키를 작성하려면 [서비스 ID의 API 키 작성](/docs/iam?topic=iam-serviceidapikeys#create_service_key)을 참조하십시오.
- 사용자 API 키를 작성하려면 [API 키 작성](/docs/iam?topic=iam-userapikey#create_user_key)을 참조하십시오.

### API 키를 사용하여 액세스 자동화
{: #registry_api_key_use}

API 키를 사용하여 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 액세스할 수 있습니다.
{:shortdesc}

다음 Docker 명령을 실행하여 API 키로 레지스트리에 로그인하십시오. `<your_apikey>`를 API 키로 대체하고 `<registry_url>`을 네임스페이스가 설정된 레지스트리의 URL로 대체하십시오.

- 아시아/태평양 북부의 네임스페이스 설정의 경우 `jp.icr.io`를 사용하십시오.
- 아시아/태평양 남부의 네임스페이스 설정의 경우 `au.icr.io`을 사용하십시오.
- 유럽 연합 중부의 네임스페이스 설정의 경우 `de.icr.io`를 사용하십시오.
- 영국 남부의 네임스페이스 설정의 경우 `uk.icr.io`를 사용하십시오.
- 미국 남부의 네임스페이스 설정의 경우 `us.icr.io`를 사용하십시오.

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

명령에 대한 참조 정보는 [새 {{site.data.keyword.cloud_notm}} 플랫폼 API 키 작성](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create)을 참조하십시오.

## 모든 클라이언트에 대한 인증 옵션
{: #registry_authentication}

`docker login` 명령이나 기타 레지스트리 클라이언트를 사용하여 인증할 수 있습니다.
{:shortdesc}

대부분의 사용자는 `ibmcloud cr login` 명령을 사용하여 `docker login`을 단순화하지만, 자동화를 구현 중이거나 다른 클라이언트를 사용 중이면 수동 인증을 원할 수 있습니다. 사용자 이름과 비밀번호를 제시해야 합니다. {{site.data.keyword.registrylong_notm}}에서 사용자 이름은 비밀번호에서 제시된 시크릿의 유형을 표시합니다.

다음의 사용자 이름이 유효합니다.

- `iambearer`: 비밀번호에 IAM 액세스 토큰이 포함됩니다. 이 인증 유형은 단기간 유효하지만, 모든 유형의 IAM ID에서 파생될 수 있습니다.
- `iamrefresh`: 비밀번호에 IAM 액세스 토큰을 생성하고 새로 고치기 위해 내부적으로 사용되는 IAM 새로 고치기 토큰이 포함되어야 합니다. 이 인증 유형은 더 오래 사용되며 `ibmcloud cr login` 명령에 의해 사용됩니다.
- `iamapikey`: 비밀번호가 IAM API 키입니다. 이 인증 유형은 자동화에 선호되는 유형입니다. 사용자 또는 서비스 ID API 키를 사용할 수 있습니다. [API 키 작성](#registry_api_key_create)을 참조하십시오.

`docker` 명령을 사용하여 레지스트리를 인증할 필요는 없습니다. 예를 들어, Cloud Foundry CLI를 사용하여 레지스트리의 이미지에서 Cloud Foundry 앱을 시작할 수 있습니다.

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

`<apikey>`는 API 키로, `<region>`은 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions) 이름으로, `<my_namespace>`는 네임스페이스로, `<image_repo>`는 저장소로 대체하십시오.

자세한 정보는 [개인용 이미지 레지스트리 사용](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry)을 참조하십시오.
