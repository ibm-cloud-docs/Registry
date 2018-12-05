---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-19"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 이미지의 취약성 모니터링
{: #registry_ui}

{{site.data.keyword.Bluemix_notm}} 콘솔을 사용하여 {{site.data.keyword.registrylong}} 공용 및 개인용 저장소의 이미지 보안과 잠재적 취약성에 대한 정보를 볼 수 있습니다.
{:shortdesc}

**보안 상태** 열에는 이미지에 대한 다음 정보가 표시됩니다.
- `보안` 보안 문제가 발견되지 않았습니다.
- `취약성` 보안 또는 구성 문제가 발견되지 않았으며 이미지를 배치하려면 해당 문제를 해결해야 합니다.
- `불완전` 스캔이 완료되지 않았습니다. 스캔이 아직 실행 중이거나 이미지의 운영 체제가 호환 가능하지 않을 수 있습니다. 잠시 기다린 후 다시 스캔을 시도하십시오. 스캔이 아직 완료되지 않은 경우 다시 이미지를 푸시하여 새 스캔을 시작하십시오. 스캔이 불완전한 이미지는 배치에 대해 차단되지 않습니다.
- `지원되지 않는 운영 체제` 이미지의 운영 체제가 지원되지 않습니다.

그래픽 사용자 인터페이스를 보려면 다음 단계를 사용하십시오.

1. IBM ID를 사용하여 {{site.data.keyword.Bluemix_notm}} 콘솔([https://console.bluemix.net ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net))에 로그인하십시오.
2. {{site.data.keyword.Bluemix_notm}} 계정이 여러 개인 경우 계정 메뉴에서 사용할 계정과 지역을 선택하십시오.
3. **카탈로그**를 클릭하십시오.
4. **컨테이너** 카테고리를 선택하고 **컨테이너 레지스트리** 타일을 클릭하십시오.
5. 개인용 저장소의 이미지에 대한 정보를 보려면 **이미지**를 클릭하십시오. 개인용 저장소의 이미지 목록과 각 이미지의 보안 상태가 표시됩니다. 
6. 태그 및 이미지 요약을 포함한 잠재적 취약성에 대한 자세한 정보를 알아보려면 표에서 이미지에 대한 행을 클릭하십시오. **이미지 세부사항** 탭이 열립니다.
7. 유형별 문제에 대해 알아보려면 **유형별 문제** 탭을 클릭하십시오.
8. 연관된 컨테이너에 대해 알아보려면 **연관된 컨테이너** 탭을 클릭하십시오.

보안 보고서의 정보가 의미하는 내용에 대해 자세히 알아보려면 [Vulnerability Advisor로 이미지 보안 관리](/docs/services/va/va_index.html)를 참조하십시오.
