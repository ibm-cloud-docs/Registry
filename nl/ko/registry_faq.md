---

copyright:
  years: 2018, 
lastupdated: "2018-09-03"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# FAQ
{: #registry_faq}


## 공용 이미지를 나열하는 방법은 무엇입니까?
{: #faq_list_public_images}

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

예, 이는 도구에서 OCI 이미지 형식과 프로토콜을 지원하는 경우 가능합니다. 
