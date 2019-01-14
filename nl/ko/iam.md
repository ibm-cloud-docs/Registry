---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# IAM(Identity and Access Management)으로 사용자 액세스 관리
{: #iam}

계정의 사용자와 관련한 {{site.data.keyword.registrylong}}에 대한 액세스는 {{site.data.keyword.IBM_notm}} IAM({{site.data.keyword.iamshort}})에서 제어됩니다.
{: shortdesc}

{{site.data.keyword.registrylong_notm}}의 계정에 대한 IAM 정책이 사용으로 설정된 경우 계정에서 {{site.data.keyword.registrylong_notm}} 서비스에 액세스하는 모든 사용자에게 IAM 사용자 역할이 정의된 액세스 정책이 지정되어야 합니다. 해당 정책에 따라 서비스의 컨텍스트 내에서 사용자가 보유하는 역할 및 사용자가 수행할 수 있는 조치가 결정됩니다. {{site.data.keyword.registrylong_notm}}의 각 조치는 하나 이상의 [IAM 사용자 역할](/docs/iam/users_roles.html)에 맵핑됩니다.

IAM 정책은 IAM을 사용하여 {{site.data.keyword.registrylong_notm}}에 로그인하는 경우에만 적용됩니다. 레지스트리 토큰과 같은 다른 방법을 사용하여 {{site.data.keyword.registrylong_notm}}에 로그인하는 경우 해당 정책이 적용되지 않습니다. 자동화에서 사용하는 ID에 대해 하나 이상의 네임스페이스에 대한 액세스를 제한하려면 레지스트리 토큰 대신에 IAM 서비스 ID를 사용하는 것을 고려하십시오. 서비스 ID에 대한 자세한 정보는 [서비스 ID 작성 및 작업](/docs/iam/serviceid.html#serviceids)을 참조하십시오.

IAM에 대한 자세한 정보는 [IBM Cloud 액세스 및 관리](/docs/iam/index.html#iamoverview)를 참조하십시오.

{{site.data.keyword.registrylong_notm}}에 대한 정책 사용과 관련된 정보는 [사용자 액세스 역할 정책 정의](/docs/services/Registry/registry_users.html#user)를 참조하십시오.

정책은 액세스 권한이 서로 다른 레벨에서 부여될 수 있도록 합니다. 일부 옵션에는 다음 액세스 레벨이 포함됩니다.

* 계정의 서비스에 대한 액세스
* 서비스 내의 특정 리소스에 대한 액세스
* 계정의 모든 IAM 사용 서비스에 대한 액세스

액세스 정책의 범위를 정의한 후 역할을 지정합니다. {{site.data.keyword.registrylong_notm}} 서비스 내에서 각 역할이 허용하는 조치가 개략적으로 설명된 다음 표를 정보를 검토하십시오.

UI에서 사용자 역할을 지정하는 방법에 대한 정보는 [IAM 액세스 관리](/docs/iam/mngiam.html#iammanidaccser)를 참조하십시오.

[튜토리얼: {{site.data.keyword.registrylong_notm}} 리소스에 대한 액세스 부여](/docs/services/Registry/registry_tutorial_configure_iam.html#iam_access) 튜토리얼을 사용해 보십시오.
{: tip}

## 플랫폼 관리 역할
{: #platform_management_roles}

다음 표에서는 플랫폼 관리 역할에 맵핑된 조치에 대해 자세히 설명합니다. 사용자는 플랫폼 관리 역할을 사용하여 플랫폼 레벨에서 서비스 리소스에 대한 태스크를 수행할 수 있습니다. 예를 들어, 서비스에 대한 사용자 액세스를 지정하고 서비스 ID를 작성하거나 삭제할 수 있습니다.

|플랫폼 관리 역할 |조치에 대한 설명 |예제 조치|
|:-----------------|:-----------------|:-----------------|
|뷰어 |지원되지 않음 | |
|편집자 |지원되지 않음 | |
|운영자 |지원되지 않음 | |
|관리자 | <ul><li>다른 사용자에 대한 액세스 구성</li><li>레지스트리 토큰 구성</li><li>클러스터 작성</li></ul> | <ul><li>UI에서 사용자 역할을 지정하는 방법에 대한 정보는 [IAM 액세스 관리](/docs/iam/mngiam.html#iammanidaccser)를 참조하십시오.</li><li>레지스트리 토큰 추가, 나열, 검색 및 제거</li><li>{{site.data.keyword.containerlong_notm}}에서 클러스터를 작성하려면 사용자에게 {{site.data.keyword.registrylong_notm}}에 대한 관리자 역할을 지정해야 합니다. [클러스터 작성 준비](/docs/containers/cs_clusters.html#cluster_prepare)를 참조하십시오.</li></ul> |
{: caption="표 1. IAM 사용자 역할 및 조치" caption-side="top"}

{{site.data.keyword.registrylong_notm}}의 경우에는 다음 조치가 존재합니다.

|조치|서비스에 대한 오퍼레이션 |역할
|:-----------------|:-----------------|:--------------|
|`container-registry.registrytoken.create` |[`ibmcloud cr token-add`](/docs/services/Registry/registry_cli.html#bx_cr_token_add) 레지스트리에 대한 액세스를 제어하는 데 사용할 수 있는 토큰을 추가합니다. |관리자 |
|`container-registry.registrytoken.delete` |[`ibmcloud cr token-rm`](/docs/services/Registry/registry_cli.html#bx_cr_token_rm) 하나 이상의 지정된 토큰을 제거합니다. |관리자 |
|`container-registry.registrytoken.get` |[`ibmcloud cr token-get`](/docs/services/Registry/registry_cli.html#bx_cr_token_get) 레지스트리에서 지정된 토큰을 검색합니다. |관리자 |
|`container-registry.registrytoken.list` |[`ibmcloud cr token-list`](/docs/services/Registry/registry_cli.html#bx_cr_token_list) {{site.data.keyword.Bluemix_notm}} 계정에 대해 존재하는 모든 토큰을 표시합니다. |관리자 |
{: caption="표 2. {{site.data.keyword.registrylong_notm}}를 구성하기 위한 플랫폼 조치 및 오퍼레이션" caption-side="top"}

## 서비스 액세스 역할
{: #service_access_roles}

다음 표에서는 서비스 액세스 역할에 맵핑된 조치에 대해 자세히 설명합니다. 사용자는 서비스 액세스 역할을 사용하여 {{site.data.keyword.registrylong_notm}} API 호출 기능은 물론 {{site.data.keyword.registrylong_notm}}에 액세스할 수 있습니다.

|서비스 액세스 역할 |조치에 대한 설명 |예제 조치|
|:-----------------|:-----------------|:-----------------|
|독자 |독자 역할은 정보를 볼 수 있습니다. | <ul><li>이미지 보기, 검사 및 가져오기</li><li>네임스페이스 보기</li><li>할당량 보기</li><li>취약성 보고서 보기</li><li>이미지 서명 보기</li></ul>|
|작성자 |작성자 역할은 정보를 편집할 수 있습니다. |<ul><li>이미지 빌드, 푸시 및 삭제</li><li>할당량 보기</li><li>이미지 서명</li><li>네임스페이스 추가 및 제거</li></ul> |
|관리자 |관리자 역할은 모든 조치를 수행할 수 있습니다. | <ul><li>이미지 보기, 검사, 가져오기, 빌드, 푸시 및 삭제</li><li>네임스페이스 보기, 추가 및 제거</li><li>할당량 보기 및 설정</li><li>취약성 보고서 보기</li><li>이미지 서명 보기 및 작성</li><li>가격 책정 플랜 검토 및 변경</li><li>IAM 정책 적용 사용</li><li>Vulnerability Advisor 면제 항목 관리</li></ul> |
{: caption="표 3. IAM 서비스 액세스 역할 및 조치" caption-side="top"}

 다음 {{site.data.keyword.registrylong_notm}} 명령의 경우 다음 표에 표시된 대로 지정된 역할 중 하나 이상이 있어야 합니다. {{site.data.keyword.registrylong_notm}}에 대한 액세스를 허용하는 정책을 작성하려면 서비스 이름이 `container-registry`이고, 서비스 인스턴스가 비어 있고, 지역이 액세스를 부여할 지역이거나 모든 지역에 대한 액세스를 부여하려는 경우 지역이 비어 있는 정책을 작성해야 합니다.

### {{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할
{: #access_roles_configure}

사용자에게 계정에서 {{site.data.keyword.registrylong_notm}}를 구성할 수 있는 권한을 부여하려면 다음 표에 있는 하나 이상의 역할을 부여하는 정책을 작성해야 합니다. 정책을 작성할 때 `resource type` 또는 `resource`를 지정해서는 안됩니다.

**예**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

|조치|서비스에 대한 오퍼레이션 |역할
|:-----------------|:-----------------|:--------------|
|`container-registry.auth.set` |[`ibmcloud cr iam-policies-enable`](/docs/services/Registry/registry_cli.html#bx_cr_iam_policies_enable) IAM 정책 적용을 사용으로 설정합니다. |관리자 |
|`container-registry.exemption.manager` | <ul><li>[`ibmcloud cr exemption-add`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_add) 보안 문제에 대한 면제 항목을 작성합니다.</li><li>[`ibmcloud cr exemption-list`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_list) 보안 문제에 대한 면제 항목을 나열합니다.</li><li>[`ibmcloud cr exemption-rm`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_rm) 보안 문제에 대한 면제 항목을 삭제합니다.</li><li>[`ibmcloud cr exemption-types`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_types) 면제할 수 있는 보안 문제의 유형을 나열합니다.</li></ul> |관리자 |
|`container-registry.plan.get` |[`ibmcloud cr plan`](/docs/services/Registry/registry_cli.html#bx_cr_plan) 가격 책정 플랜을 표시합니다. |관리자 |
|`container-registry.plan.set` |[`ibmcloud cr plan-upgrade`](/docs/services/Registry/registry_cli.html#bx_cr_plan_upgrade) 표준 플랜으로 업그레이드합니다. |관리자 |
|`container-registry.quota.get` |[`ibmcloud cr quota`](/docs/services/Registry/registry_cli.html#bx_cr_quota) 트래픽과 스토리지에 대한 현재 할당량 및 이 할당량에 대한 사용량 정보를 표시합니다. |독자, 작성자, 관리자 |
|`container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/services/Registry/registry_cli.html#bx_cr_quota_set) 지정된 할당량을 수정합니다. |관리자 |
{: caption="표 4. {{site.data.keyword.registrylong_notm}}를 구성하기 위한 서비스 조치 및 오퍼레이션" caption-side="top"}

### {{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할
{: #access_roles_using}

사용자에게 계정에서 {{site.data.keyword.registrylong_notm}} 컨텐츠에 액세스할 수 있는 권한을 부여하려면 다음 표에 있는 하나 이상의 역할을 부여하는 정책을 작성해야 합니다. 정책을 작성할 때 리소스 유형을 `namespace`로 지정하고 네임스페이스 이름을 리소스로 지정하여 특정 네임스페이스에 대한 액세스를 제한할 수 있습니다. `resource-type` 및 `resource`를 지정하지 않으면 정책이 계정의 모든 리소스에 대한 액세스를 부여합니다.

**예**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Reader> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

|조치 |서비스에 대한 오퍼레이션 |역할
|:-----------------|:-----------------|:--------------|
|`container-registry.image.build` |[`ibmcloud cr build`](/docs/services/Registry/registry_cli.html#bx_cr_build) 컨테이너 이미지를 빌드합니다. |작성자, 관리자 |
|`container-registry.image.delete` |[`ibmcloud cr image-rm`](/docs/services/Registry/registry_cli.html#bx_cr_image_rm) 하나 이상의 이미지를 삭제합니다. |작성자, 관리자 |
|`container-registry.image.inspect` |[`ibmcloud cr image-inspect`](/docs/services/Registry/registry_cli.html#bx_cr_image_inspect) 특정 이미지에 대한 세부사항을 표시합니다. |독자, 관리자 |
|`container-registry.image.list` |[`ibmcloud cr image-list`](/docs/services/Registry/registry_cli.html#bx_cr_image_list) 컨테이너 이미지를 나열합니다. |독자, 관리자 |
|`container-registry.image.pull` |`docker pull` 이미지를 가져옵니다. |독자, 작성자, 관리자 |
|`container-registry.image.push` | <ul><li>`docker push` 이미지를 푸시합니다.</li><li>[`ibmcloud cr ppa-archive-load`](/docs/services/Registry/registry_cli.html#bx_cr_ppa_archive_load) [IBM Passport Advantage Online for customers ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/software/passportadvantage/pao_customer.html)에서 다운로드했으며 Helm과 함께 사용할 수 있도록 패키지된 IBM 소프트웨어를 개인용 레지스트리 네임스페이스로 가져옵니다.</li></ul> |작성자, 관리자 |
|`container-registry.image.vulnerabilities` |[`ibmcloud cr vulnerability-assessment`](/docs/services/Registry/registry_cli.html#bx_cr_va) 이미지의 취약성 평가 보고서를 봅니다. |독자, 관리자 |
|`container-registry.namespace.create` |[`ibmcloud cr namespace-add`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_add) 네임스페이스를 추가합니다. |작성자, 관리자 |
|`container-registry.namespace.delete` |[`ibmcloud cr namespace-rm`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_rm) 네임스페이스를 제거합니다. |작성자, 관리자 |
|`container-registry.namespace.list` |[`ibmcloud cr namespace-list`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_list) 네임스페이스를 표시합니다. |독자, 관리자 |
|`container-registry.signature.create` |`docker trust sign` 이미지에 서명합니다. |작성자, 관리자 |
|`container-registry.signature.delete` |`docker trust revoke` 서명을 삭제합니다. |작성자, 관리자 |
|`container-registry.signature.get` |`docker trust inspect` 서명을 검사합니다. |독자, 관리자 |
{: caption="표 5. {{site.data.keyword.registrylong_notm}}를 사용하기 위한 서비스 조치 및 오퍼레이션" caption-side="top"}
