---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, Activity Tracker events, events

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

{{site.data.keyword.cloudaccesstrailfull}} 서비스를 사용하여 사용자와 애플리케이션이 {{site.data.keyword.Bluemix}}에서 {{site.data.keyword.registrylong}} 서비스와 상호작용하는 방법을 추적할 수 있습니다.
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 서비스는 {{site.data.keyword.Bluemix_notm}}에서 서비스의 상태를 변경하는 사용자 시작 활동을 기록합니다.
추가 정보는 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla)의 내용을 참조하십시오.

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
 </table>

## 이벤트를 찾는 위치
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 이벤트는 이벤트가 생성되는 {{site.data.keyword.Bluemix_notm}} 지역에서 사용할 수 있는 {{site.data.keyword.cloudaccesstrailshort}} **계정 도메인**에서 사용 가능합니다.

Vulnerability Advisor 이벤트가 사용 가능한 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)은 리소스(예: 이미지 또는 네임스페이스)가 사용 가능한 {{site.data.keyword.registrylong_notm}}의 지역에 해당합니다.
