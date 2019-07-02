---

copyright:
  years: 2019
lastupdated: "2019-06-13"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# 릴리스 정보
{: #registry_release_notes}

다음 릴리스 정보를 사용하여 {{site.data.keyword.registrylong}} 및 Vulnerability Advisor의 최신 변경사항에 대해 알아보십시오. 변경사항은 날짜별로 그룹화되어 있습니다.
{:shortdesc}

## 2019년 6월 13일
{: #13jun2019}

- **이미지에서 태그 제거**

  {{site.data.keyword.registrylong_notm}}의 각 지정된 이미지에서 태그를 제거합니다.

  특정 태그를 이미지에서 제거하고 기본 이미지 및 기타 모든 태그를 그대로 남겨두려면 [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) 명령을 사용하십시오. 기본 이미지 및 해당 태그를 모두 삭제하려면 대신 [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) 명령을 사용하십시오.

  자세한 정보는 [개인용 {{site.data.keyword.cloud_notm}} 저장소에 있는 이미지에서 태그 제거](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag)를 참조하십시오.

## 2019년 5월 13일
{: #13may2019}

- **컨테이너 스캐너에 대한 지원 종료**

  이제 컨테이너 스캐너는 더 이상 사용되지 않으며 더 이상 사용할 수 없습니다.

  자세한 정보는 [컨테이너 스캐너 설치(더 이상 사용되지 않음)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)를 참조하십시오.

## 2019년 4월 2일
{: #2apr2019}

- **Container Image Security Enforcement GA(General Availability)**

  Container Image Security Enforcement를 사용하면 컨테이너 이미지를 {{site.data.keyword.containerlong_notm}}의 클러스터에 배치하기 전에 확인할 수 있습니다. 이미지가 배치되는 위치를 제어하고 Vulnerability Advisor 정책을 적용하며 [컨텐츠 신뢰](/docs/services/Registry?topic=registry-registry_trustedcontent)가 올바르게 이미지에 적용되었는지 확인할 수 있습니다.

  자세한 정보는 [컨테이너 이미지 보안 적용](/docs/services/Registry?topic=registry-security_enforce#security_enforce)을 참조하십시오.

## 2019년 3월 14일
{: #14mar2019}

- **{{site.data.keyword.registrylong_notm}}에 사용 가능한 {{site.data.keyword.cloudaccesstrailfull_notm}}**

  {{site.data.keyword.cloudaccesstraillong_notm}} 서비스를 사용하여 사용자와 애플리케이션이 {{site.data.keyword.cloud}}에서 {{site.data.keyword.registrylong_notm}} 서비스와 상호작용하는 방법을 추적할 수 있습니다.

  자세한 정보는 [Activity Tracker 이벤트](/docs/services/Registry?topic=registry-at_events#at_events)를 참조하십시오.

## 2019년 2월 25일
{: #25feb2019}

- **새 DNS 이름**

  {{site.data.keyword.registrylong_notm}}에서 새 도메인 이름을 채택합니다. 콘솔 및 CLI에서 새 도메인 이름이 사용 가능합니다. 이제 새로운 `icr.io` 도메인 이름을 사용할 수 있습니다. 기존 `registry.bluemix.net` 도메인 이름은 더 이상 사용되지 않지만 당분간은 계속 사용할 수 있습니다. 지원이 종료되는 날짜는 추후 공지될 예정입니다. 자세한 정보는 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions) 및 [Introducing New IBM Cloud Container Registry Domain Names ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names)를 참조하십시오.

  컨텐츠 신뢰를 사용 중인 경우 서명이 도메인 이름을 포함한 전체 이미지 이름에 적용되기 때문에 새 도메인 이름 아래의 컨텐츠 신뢰를 이용할 수 있도록 새 서명을 추가해야 합니다. 이미지에 서명하는 방법에 대한 자세한 정보는 [신뢰할 수 있는 컨텐츠의 이미지에 서명](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)을 참조하십시오.

- **{{site.data.keyword.containerlong_notm}} 클러스터에 대한 IAM API 키 풀 시크릿**

  `icr.io` 도메인에 대한 새 클러스터 이미지 풀 시크릿에는 IAM API 키를 사용하여 권한이 부여되므로 {{site.data.keyword.registrylong_notm}} 리소스에 대한 액세스의 제어를 강화하려는 경우 IAM 정책을 사용할 수 있습니다. 예를 들어, 특정 레지스트리 지역 또는 네임스페이스에서만 이미지를 가져오도록 클러스터 풀 시크릿의 API 키 정책을 변경할 수 있습니다.
  
  자세한 정보는 [{{site.data.keyword.registrylong_notm}}에서 이미지를 가져올 수 있는 권한을 클러스터에 부여하는 방법 이해](/docs/containers?topic=containers-images#cluster_registry_auth)를 참조하십시오.

- **ap-north의 새 지역**

  `ap-north`에서 새 지역이 사용 가능합니다. 도메인 이름 `jp.icr.io`를 사용하여 새 지역을 사용할 수 있습니다.
  
  자세한 정보는 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)을 참조하십시오.

## 2019년 2월 21일
{: #21feb2019}

- **네임스페이스에 대한 액세스 자동화**

  토큰을 사용하여 네임스페이스에 대한 Docker 이미지의 푸시 및 가져오기를 자동화하는 기능이 더 이상 사용되지 않습니다. 이제 API 키를 사용하여 이미지를 푸시하고 가져올 수 있도록 {{site.data.keyword.registrylong_notm}} 네임스페이스에 대한 액세스를 자동화해야 합니다.

  자세한 정보는 [API 키를 사용하여 네임스페이스에 대한 액세스 자동화](/docs/services/Registry?topic=registry-registry_access#registry_api_key)를 참조하십시오.

## 2019년 1월 8일
{: #8jan2019}

- **Vulnerability Advisor API 버전 2에 대한 지원 종료**

  Vulnerability Advisor API 버전 2는 더 이상 사용되지 않으며 더 이상 사용할 수 없습니다. API 버전 3을 사용하십시오. [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/apidocs/container-registry/va)를 참조하십시오.

  자세한 정보는 [Vulnerability Advisor v2 API Deprecation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/)을 참조하십시오.

## 2018년 10월 4일
{: #4oct2018}

- **사용자 액세스 관리**

  {{site.data.keyword.IBM_notm}} IAM({{site.data.keyword.iamshort}})을 사용하여 계정에 있는 사용자의 {{site.data.keyword.registrylong_notm}}에 대한 액세스를 제어할 수 있습니다. {{site.data.keyword.registrylong_notm}}의 계정에 대한 IAM 정책이 사용으로 설정된 경우 계정에서 {{site.data.keyword.registrylong_notm}} 서비스에 액세스하는 모든 사용자에게 IAM 사용자 역할이 정의된 액세스 정책이 지정되어야 합니다. 해당 정책에 따라 서비스의 컨텍스트 내에서 사용자가 보유하는 역할 및 사용자가 수행할 수 있는 조치가 결정됩니다.

  자세한 정보는 [{{site.data.keyword.iamshort}}를 사용한 사용자 액세스 관리](/docs/services/Registry?topic=registry-iam#iam), [사용자 액세스 역할 정책 정의](/docs/services/Registry?topic=registry-user#user) 및 [튜토리얼: IBM Cloud Container Registry 리소스에 대한 액세스 부여](/docs/services/Registry?topic=registry-iam_access#iam_access)를 참조하십시오.

## 2018년 8월 7일
{: #7aug2018}

- **Vulnerability Advisor에서 사용 가능한 면제 정책**

  {{site.data.keyword.cloud_notm}} 조직의 보안을 관리하려는 경우 정책 설정을 사용하여 문제 면제 여부를 판별할 수 있습니다. Container Image Security Enforcement를 사용하여 사용자 정책에 따라 면제된 문제를 처리한 후 보안 문제가 없는 이미지에서만 배치가 허용되도록 선택할 수 있습니다.

  자세한 정보는 [조직 면제 정책 설정](/docs/services/Registry?topic=va-va_index#va_managing_policy)을 참조하십시오.

## 2018년 7월 25일
{: #25jul2018}

- **Vulnerability Advisor에 사용 가능한 {{site.data.keyword.cloudaccesstrailfull_notm}}**

  {{site.data.keyword.cloudaccesstrailfull_notm}} 서비스를 사용하여 사용자와 애플리케이션이 {{site.data.keyword.cloud}}에서 {{site.data.keyword.registrylong_notm}} 서비스와 상호작용하는 방법을 추적할 수 있습니다.

  자세한 정보는 [Activity Tracker 이벤트](/docs/services/Registry?topic=registry-at_events#at_events)를 참조하십시오.
  
## 2018년 7월 12일
{: #12jul2018}

- **Vulnerability Advisor API 버전 3**

  이 API의 버전 3에서는 면제를 나열하는 데 사용되는 API 엔드포인트의 동작이 변경되었습니다. API 사용이 버전 2의 동작에 의존하지 않는지 확인해야 합니다.

  자세한 정보는 [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/apidocs/container-registry/va)를 참조하십시오.

## 2018년 3월 31일
{: #31may2018}

- **Passport Advantage 이미지에 Helm 사용**

  [IBM Passport Advantage Online for customers ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/software/passportadvantage/pao_customer.html)에서 다운로드되고 Helm과 함께 사용할 수 있도록 패키징된 {{site.data.keyword.IBM_notm}} 소프트웨어를 {{site.data.keyword.registrylong_notm}} 네임스페이스로 가져오십시오.

  자세한 정보는 [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load)를 참조하십시오.

## 2018년 3월 21일
{: #21mar2018}

- **컨테이너 스캐너**

  컨테이너 스캐너를 사용하면 Vulnerability Advisor를 통해 컨테이너의 기본 이미지에 없는 실행 중인 컨테이너에서 찾은 문제점을 보고할 수 있습니다.

  자세한 정보는 [컨테이너 스캐너 설치](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)를 참조하십시오.

## 2018년 3월 16일
{: #16mar2018}

- **Container Image Security Enforcement 베타**

  Container Image Security Enforcement 베타를 사용하면 컨테이너 이미지를 {{site.data.keyword.containerlong_notm}}의 클러스터에 배치하기 전에 확인할 수 있습니다. 이미지가 배치되는 위치를 제어하고 Vulnerability Advisor 정책을 적용하며 [컨텐츠 신뢰](/docs/services/Registry?topic=registry-registry_trustedcontent)가 올바르게 이미지에 적용되었는지 확인할 수 있습니다.

  자세한 정보는 [컨테이너 이미지 보안 적용](/docs/services/Registry?topic=registry-security_enforce#security_enforce)을 참조하십시오.

## 2018년 2월 20일
{: #20feb2018}

- **신뢰할 수 있는 컨텐츠**

  {{site.data.keyword.registrylong_notm}}에서는 사용자가 이미지에 서명하여 레지스트리 네임스페이스에서 이미지의 무결성을 보장할 수 있도록 신뢰할 수 있는 컨텐츠 기술을 제공합니다. 서명된 이미지를 가져오고 푸시하여 CI(Continuous Integration) 도구와 같이 올바른 당사자가 이미지를 푸시했는지 확인할 수 있습니다.

  자세한 정보는 [신뢰할 수 있는 컨텐츠의 이미지에 서명](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)을 참조하십시오.

## 2017년 11월 6일
{: #6nov2017}

- **글로벌 레지스트리**

  글로벌 레지스트리가 사용 가능하며, 해당 이름(`icr.io`)에 포함된 지역은 없습니다. IBM에서 제공하는 공용 이미지만 이 레지스트리에서 호스팅됩니다.

  자세한 정보는 [글로벌 레지스트리](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)를 참조하십시오.

## 2017년 9월 29일
{: #29sep2017}

- **Docker 이미지 빌드**

  이제 `ibmcloud cr build` 명령을 컨테이너 빌드 실행에 사용할 수 있습니다. {{site.data.keyword.cloud_notm}}에서 직접 Docker 이미지를 빌드하거나 로컬 컴퓨터에 고유 Docker 이미지를 작성하고 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 업로드(푸시)할 수 있습니다.

  자세한 정보는 [네임스페이스와 사용할 Docker 이미지 빌드](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) 및 [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build)를 참조하십시오.

## 2017년 8월 24일
{: #24aug2017}

- **그래픽 사용자 인터페이스가 릴리스됨**

  {{site.data.keyword.registrylong_notm}} 그래픽 사용자 인터페이스를 카탈로그에서 사용할 수 있습니다. [Container Registry ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/kubernetes/catalog/registry)를 참조하십시오.

## 2017년 6월 27일
{: #27jun2017}

- **{{site.data.keyword.registrylong_notm}}의 GA(General Availability)**

  {{site.data.keyword.registrylong_notm}}가 {{site.data.keyword.cloud_notm}}의 서비스로 GA(General Available)되었습니다. {{site.data.keyword.registrylong_notm}}는 {{site.data.keyword.containerlong_notm}}를 지원합니다.

  {{site.data.keyword.containerlong_notm}}에 대한 자세한 정보는 [시작하기 튜토리얼](/docs/containers?topic=containers-getting-started)을 참조하십시오.
