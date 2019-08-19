---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker with LogDNA events, Activity Tracker events, events, track,

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

# Activity Tracker 이벤트
{: #at_events}

사용자와 애플리케이션이 {{site.data.keyword.cloud}}에서 {{site.data.keyword.registrylong}} 서비스와 상호작용하는 방법을 추적합니다.
{:shortdesc}

{{site.data.keyword.at_full_notm}} 서비스 또는 {{site.data.keyword.cloudaccesstrailfull_notm}} 서비스(기존 사용자 전용)는 {{site.data.keyword.cloud_notm}}에서 서비스의 상태를 변경하는 사용자 시작 활동을 기록합니다.
자세한 정보는 [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started) 또는 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)(기존 사용자의 경우)의 내용을 참조하십시오.

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
    <td>`container-registry.image.bulkdelete`</td>
	  <td>{{site.data.keyword.registrylong_notm}}에서 여러 이미지를 삭제합니다.</td>
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
    <td>`container-registry.image.rm`</td>
	  <td>{{site.data.keyword.registrylong_notm}}에서 하나 이상의 지정된 이미지를 삭제합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>기존 {{site.data.keyword.registrylong_notm}} 이미지를 참조하는 태그를 추가합니다.</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>{{site.data.keyword.registrylong_notm}}의 각 지정된 이미지에서 태그를 제거합니다.</td>
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
  </tr><tr>
    <td>`container-registry.retentionanalysis`</td>
	  <td>기준을 충족하는 이미지만 보유하여 네임스페이스를 정리합니다. 지정된 기준을 적용하여 {{site.data.keyword.registrylong_notm}}의 네임스페이스 내 저장소마다 이미지를 보관합니다. 네임스페이스의 기타 모든 이미지가 삭제됩니다. </br> 삭제할 이미지의 목록을 가져오는 요청은 `retentionanalysis` 이벤트 유형에 대한 `post` 조치입니다. 삭제는 `images` 이벤트 유형에 대한 `bulkdelete` 조치이며 각 개별 이미지에 대한 `delete` 조치이기도 합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>현재 가격 플랜에 대한 정보를 표시합니다.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>표준 플랜으로 업그레이드하십시오.</td>
  </tr>
 </table>

## 이벤트를 찾는 위치
{: #ui}

### {{site.data.keyword.at_full_notm}} 이벤트
{: #ui_atlogdna}

{{site.data.keyword.at_full_notm}} 이벤트는 이벤트가 생성되는 {{site.data.keyword.cloud_notm}} 지역에서 사용할 수 있는 {{site.data.keyword.at_full_notm}} **계정 도메인**에서 사용 가능합니다(`ap-south`는 제외됨). `ap-south`에 대한 이벤트는 `Tokyo (jp-tok)`에 표시됩니다.

{{site.data.keyword.registrylong_notm}} 또는 Vulnerability Advisor 이벤트가 사용 가능한 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)은 리소스가 사용 가능한 {{site.data.keyword.registrylong_notm}}의 지역에 해당합니다. 이미지 및 네임스페이스는 리소스의 예입니다.

| 계정 레지스트리의 지역 | 레지스트리의 도메인 이름 | {{site.data.keyword.at_full_notm}} 이벤트의 위치 |
|:-----------------|:-----------------|:-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="표 2. {{site.data.keyword.at_full_notm}} 이벤트의 위치" caption-side="top"}

| 레지스트리 | 글로벌 레지스트리 | {{site.data.keyword.at_full_notm}} 이벤트의 위치 |
|:-----------------|:-----------------|:-----------------|
| 글로벌 | `icr.io` | `Dallas (us-south)` |
{: caption="표 3. 글로벌 레지스트리 {{site.data.keyword.at_full_notm}} 이벤트의 위치" caption-side="top"}

### {{site.data.keyword.cloudaccesstraillong_notm}} 이벤트
{: #ui_at}

{{site.data.keyword.cloudaccesstraillong_notm}} 이벤트(기존 사용자 전용)는 이벤트가 생성되는 {{site.data.keyword.cloud_notm}} 지역에서 사용할 수 있는 {{site.data.keyword.cloudaccesstraillong_notm}} **계정 도메인**에서 사용 가능합니다(`ap-north`는 제외됨). `ap-north`에 대한 이벤트는 `ap-south`에 표시됩니다.

{{site.data.keyword.cloudaccesstrailfull_notm}}는 더 이상 사용되지 않습니다. 2019년 5월 9일 이후로 새 {{site.data.keyword.cloudaccesstrailshort}} 인스턴스를 프로비저닝할 수 없습니다. 기존 프리미엄 플랜 인스턴스는 2019년 9월 30일까지 지원됩니다. {{site.data.keyword.cloud_notm}} 계정의 활동을 계속해서 모니터링하려면 [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started)의 인스턴스를 프로비저닝하십시오.
{: deprecated}

{{site.data.keyword.registrylong_notm}} 또는 Vulnerability Advisor 이벤트가 사용 가능한 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)은 리소스가 사용 가능한 {{site.data.keyword.registrylong_notm}}의 지역에 해당합니다. 이미지 및 네임스페이스는 리소스의 예입니다.
