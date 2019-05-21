---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-26"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker events, Activity Tracker events, events, track,

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

# {{site.data.keyword.cloudaccesstrailshort}} 이벤트
{: #at_events}

{{site.data.keyword.cloudaccesstrailfull}} 서비스를 사용하여 사용자와 애플리케이션이 {{site.data.keyword.cloud}}에서 {{site.data.keyword.registrylong}} 서비스와 상호작용하는 방법을 추적할 수 있습니다.
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 서비스는 {{site.data.keyword.cloud_notm}}에서 서비스의 상태를 변경하는 사용자 시작 활동을 기록합니다.
추가 정보는 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)의 내용을 참조하십시오.

다음 표에는 호출 시에 이벤트를 생성하는 API 메소드가 나열되어 있습니다.

<table>
  <caption>표 1. 이벤트를 생성하는 조치</caption>
  <tr>
    <th>조치</th>
	  <th>설명</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Vulnerability Advisor 면제 항목을 작성합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Vulnerability Advisor 면제 항목을 삭제합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>{{site.data.keyword.registrylong_notm}}에서 Docker 이미지를 빌드합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>{{site.data.keyword.registrylong_notm}}에서 이미지를 삭제합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>이미지에 대한 세부사항을 표시합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>{{site.data.keyword.IBM_notm}} 계정의 이미지를 나열합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>{{site.data.keyword.registrylong_notm}}에서 이미지를 가져옵니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>이미지를 {{site.data.keyword.registrylong_notm}}에 푸시합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>기존 {{site.data.keyword.registrylong_notm}} 이미지를 참조하는 새 태그를 추가합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>네임스페이스를 {{site.data.keyword.registrylong_notm}}에 추가합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>{{site.data.keyword.registrylong_notm}}에서 네임스페이스를 삭제합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>{{site.data.keyword.IBM_notm}} 계정의 네임스페이스를 나열합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>트래픽과 스토리지에 대한 현재 할당량 및 이 할당량에 대한 사용량 정보를 표시합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>할당량을 수정합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.create`</td>
	  <td>새 레지스트리 토큰을 작성합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>레지스트리 토큰을 삭제합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>레지스트리 토큰에 대한 정보를 검색합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>{{site.data.keyword.IBM_notm}} 계정의 레지스트리 토큰을 나열합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>다중 레지스트리 토큰을 삭제합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>현재 가격 플랜에 대한 정보를 표시합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>표준 플랜으로 업그레이드합니다.</td>
  </tr>
 </table>

## 이벤트를 찾는 위치
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 이벤트는 이벤트가 생성되는 {{site.data.keyword.cloud_notm}} 지역에서 사용할 수 있는 {{site.data.keyword.cloudaccesstrailshort}} **계정 도메인**에서 사용 가능합니다(`ap-north`는 제외됨). `ap-north`에 대한 이벤트는 `ap-south`에 표시됩니다.

{{site.data.keyword.registrylong_notm}} 또는 Vulnerability Advisor 이벤트가 사용 가능한 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)은 리소스(예: 이미지 또는 네임스페이스)가 사용 가능한 {{site.data.keyword.registrylong_notm}}의 지역에 해당합니다.
