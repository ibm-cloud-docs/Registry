---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, FAQ, Vulnerability Advisor,

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
{:faq: data-hd-content-type='faq'}

# 자주 질문되는 내용(FAQ)
{: #registry_faq}

{{site.data.keyword.registrylong}}에 대한 자주 질문되는 내용(FAQ)입니다.
{: shortdesc}

## 공용 이미지를 나열하는 방법은 무엇입니까?
{: #faq_list_public_images}
{: faq}

공용 이미지를 나열하려면 다음 `ibmcloud` 명령을 실행하여 글로벌 레지스트리를 대상으로 지정하고 IBM 제공 공용 이미지를 나열하십시오.

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## docker 이외의 도구를 사용하여 내 이미지를 빌드하고 이를 레지스트리에 푸시할 수 있습니까?
{: #faq_tools}
{: faq}

예, 이는 도구에서 OCI 이미지 형식과 프로토콜을 지원하는 경우 가능합니다.

## {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}에서 액세스 제어를 사용하는 방법은 무엇입니까?
{: #faq_access_control}
{: faq}

{{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}(IAM) 정책을 작성하여 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 대한 액세스를 제어할 수 있습니다. 자세한 정보는 [튜토리얼: {{site.data.keyword.registrylong_notm}} 리소스에 대한 액세스 부여](/docs/services/Registry?topic=registry-iam_access) 및 [IAM(Identity and Access Management)으로 사용자 액세스 관리](/docs/services/Registry?topic=registry-iam)를 참조하십시오.

## 어느 지역에서 {{site.data.keyword.registrylong_notm}}를 사용할 수 있습니까?
{: #faq_regions}
{: faq}

[로컬 지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local)에서 이미지를 호스팅할 수 있습니다. IBM에서 호스팅하는 공용 이미지는 [글로벌 레지스트리](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)에서 사용할 수 있습니다.

## 새로 추가된 이미지에 대해 스캔을 찾을 수 없음 오류 메시지가 표시되는 이유는 무엇입니까?
{: #faq_va_new_scan_error}
{: faq}

이미지를 레지스트리에 추가한 직후에 취약성 보고서를 가져오면 다음과 같은 오류가 표시될 수 있습니다.

```
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

이미지는 결과에 대한 요청과 비동기적으로 스캔되고 스캔 프로세스는 완료되는 데 시간이 걸리기 때문에 이러한 메시지가 표시됩니다. 정상 작동 중에는 이미지를 레지스트리에 추가한 후 처음 몇 분 내에 스캔이 완료됩니다. 소요 시간은 이미지 크기와 레지스트리가 수신하는 트래픽의 양과 같은 변수에 따라 달라집니다.

빌드 파이프라인의 일부로 이 메시지가 표시되고 이 오류가 정기적으로 표시되는 경우 짧은 일시정지를 포함하는 재시도 로직을 추가해 보십시오.

허용할 수 없는 수준의 성능이 지속되면 지원 부서에 문의하십시오. [{{site.data.keyword.registrylong_notm}}에 대한 도움 및 지원 받기](/docs/services/Registry?topic=registry-ts_index#gettinghelp)를 참조하십시오.

## Vulnerability Advisor 스캔이 트리거되는 방법은 무엇입니까?
{: #faq_va_trigger_scan}
{: faq}

이미지의 스캔은 다음 방법 중 하나로 트리거됩니다.

- 새 이미지가 레지스트리로 푸시되는 경우
- 마지막으로 스캔된지 7일이 지난 경우 다시 스캔을 위해 큐에 대기되며 완료하는 데 시간이 걸릴 수 있습니다.
- 이미지에 설치된 패키지에 대한 새 보안 알림이 공지되면 이미지는 다시 스캔을 위해 큐에 대기되며 완료하는 데 시간이 걸릴 수 있습니다. 새 보안 알림의 공지로 트리거되는 다시 스캔은 Ubuntu 및 Debian 이미지에만 사용 가능합니다.

## 보안 알림이 업데이트되는 주기는 어떻게 됩니까?
{: #faq_va_update_security_notice}
{: faq}

Vulnerability Advisor의 보안 알림은 약 12시간마다 공급업체의 운영 체제 사이트에서 로드됩니다.
