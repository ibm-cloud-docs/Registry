---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, public IBM images, images

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

# 공용 {{site.data.keyword.IBM_notm}} 이미지
{: #public_images}

명령행을 사용하여 {{site.data.keyword.IBM}}에서 제공되는 이미지에 액세스할 수 있습니다. 더 이상 그래픽 사용자 인터페이스를 사용하여 공용 {{site.data.keyword.IBM_notm}} 이미지에 액세스할 수 없습니다.
{:shortdesc}

## CLI를 사용하여 공용 IBM 이미지에 액세스
{: #public_images_cli}

명령행을 사용하여 공용 {{site.data.keyword.IBM_notm}} 이미지에 액세스할 수 있습니다.
{:shortdesc}

**시작하기 전에**

- [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login)에 로그인하십시오.

  ```
  ibmcloud login
  ```
  {: pre}

공용 이미지를 나열하려면 다음 단계를 완료하십시오.

1. 글로벌 레지스트리를 대상으로 지정하십시오.

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. {{site.data.keyword.IBM_notm}} 공용 이미지를 나열하십시오.

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
