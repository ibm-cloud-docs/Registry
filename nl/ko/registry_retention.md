---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# 이미지 보관
{: #registry_retention}

이미지를 삭제할지 아니면 보관할지 여부를 결정할 수 있습니다.
{:shortdesc}

## 보관 계획
{: #retention_plan}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) 명령은 네임스페이스별로 실행됩니다. 그러므로 파이프라인에서 다중 네임스페이스를 사용하여 사용자의 요구사항에 가장 적합하도록 여러 보관 기준을 적용할 수 있음을 의미합니다.

개발, 스테이징 및 프로덕션 환경에서 일반적인 Delivery Pipeline을 고려하십시오. 코드가 제공될 때 지속적인 통합 및 지속적인 배치는 이미지를 레지스트리에 푸시한 후 개발 환경에 바로 배치합니다. 테스트 후 개발에서 생성된 일부 빌드는 스테이징으로 승격된 후 잠재적으로 프로덕션으로 승격됩니다. 이 시나리오에서 이미지 변경 비율은 개발에서 가장 빠르고 프로덕션에서 가장 느립니다. 모든 환경의 동일한 네임스페이스에서 이미지를 가져오는 경우 이러한 속도의 차이로 인해 적절한 수의 이미지를 선택하는 것은 어려울 수 있습니다.

올바른 접근 방법은 모든 이미지를 개발 네임스페이스에  전달하고(예: `project-development`), 그런 다음 파이프라인의 상위 단계로 승격될 때 [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) 명령을 사용하여 다른 네임스페이스로 이미지에 태그를 지정하는 것입니다. 이전 예에서 개발(`project-development`), 스테이징(`project-staging`) 및 프로덕션(`project-production`)의 세 가지 네임스페이스가 제공될 수 있습니다. 개발에서 스테이징으로 승격되면 `project-development` 네임스페이스에서 `project-staging` 네임스페이스로 이미지에 태그가 지정되며 `project-staging` 네임스페이스의 이미지가 배치에 사용됩니다. 이와 유사하게, 스테이징에서 프로덕션으로 승격되면 `project-staging` 네임스페이스에서 `project-production` 네임스페이스로 이미지에 태그가 지정되며 `project-production` 네임스페이스 이미지가 프로덕션 배치에 사용됩니다.

이 기술을 사용하면 다음과 같은 이점이 있습니다.

* 개발, 스테이징 및 프로덕션 네임스페이스마다 다른 보관 설정을 선택할 수 있습니다.
* 모든 이미지에 적합한 단일 네임스페이스 사용과 비교하면 스테이징 또는 프로덕션 환경에 사용될 수 있는 이미지를 실수로 제거할 가능성을 최소화합니다.
* 여러 [IAM](/docs/services/Registry?topic=registry-iam) 정책을 사용할 수 있습니다. 예를 들어, 프로덕션 이미지에 대한 더 많은 제한적인 액세스 권한이 부여될 수 있습니다.
* 프로덕션 이미지를 서명할 수 있으나 개발 및 스테이징 이미지를 서명되지 않은 상태로 유지할 수 있습니다.

## 기준을 충족하는 이미지만 보유하여 네임스페이스 정리
{: #retention_images}

지정된 기준을 적용하여 {{site.data.keyword.registrylong_notm}}의 네임스페이스 내 저장소마다 이미지를 보관합니다. 네임스페이스의 기타 모든 이미지가 삭제됩니다.
{:shortdesc}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) 명령은 삭제될 이미지를 나열하고 삭제 전에 취소할 수 있는 옵션을 제공합니다.

저장소 내의 이미지는 여러 태그로 참조되며, 해당 이미지는 한 번만 계수됩니다. 최신 이미지가 보관됩니다. 수명은 레지스트리에 푸시되는 시간이 아닌 이미지가 작성된 시간에 따라 결정됩니다.
{: tip}

이미지 삭제는 실행 취소할 수 없습니다. 기존 배치에서 사용 중인 이미지를 삭제하면 스케일 업 또는 재스케줄(또는 둘 다)이 실패할 수 있습니다.
{: important}

CLI를 사용하여 네임스페이스 내 각 저장소에 있는 이미지의 수를 줄이려면 다음 단계를 완료하십시오.

1. `ibmcloud login` 명령을 실행하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오.
2. 다음 명령을 실행하고 적절한 지역을 선택하여 이미지를 정리할 레지스트리를 선택하십시오.

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. 일부 이미지를 보관하고 기타 이미지를 삭제하려면 다음 명령을 실행하십시오.

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   여기서, `IMAGECOUNT`는 사용자 네임스페이스 `NAMESPACE` 내 저장소마다 보관할 이미지의 수입니다.

3. 다음 명령을 실행하여 이미지가 삭제되었는지 확인하고 이미지가 목록에 표시되지 않는지 검사하십시오.

   ```
   ibmcloud cr image-list
   ```
   {: pre}
