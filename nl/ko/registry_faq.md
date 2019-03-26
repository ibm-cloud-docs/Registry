---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, 

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
