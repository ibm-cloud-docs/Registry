---

copyright:
  years: 2018
lastupdated: "2018-09-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# 고가용성 및 재해 복구
{: #ha-dr}

{{site.data.keyword.registrylong}} 서비스는 고가용성의 지역 서비스입니다.
{:shortdesc}

* 지원되는 각 지역에서 트래픽은 단일 장애 지점이 없는 여러 가용성 구역의 레지스트리 인프라 간에 로드 밸런싱됩니다.

* {{site.data.keyword.registrylong_notm}}에 저장된 데이터는 정기적으로 백업되며, 추가 복원성을 제공합니다.

* 전체 지역이 사용 불가능하게 되는 경우의 이미지 가용성이 염려되면 이미지를 여러 지역 레지스트리에 푸시하도록 선택할 수 있습니다. 
  
  이미지를 실수로 삭제하거나 겹쳐쓴 경우 이미지를 여러 레지스트리에 푸시하도록 선택할 수도 있습니다.

  지역에 대한 자세한 정보는 [지역](/docs/services/Registry/registry_overview.html#registry_regions)을 참조하십시오.
