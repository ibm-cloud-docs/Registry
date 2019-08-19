---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-05"

keywords: IBM Cloud Container Registry, public IBM images, images, accessing images,

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

# 公用 {{site.data.keyword.IBM_notm}} 映像檔
{: #public_images}

您可以使用指令行來存取 {{site.data.keyword.IBM}} 所提供的映像檔。您無法再使用圖形使用者介面來存取公用 {{site.data.keyword.IBM_notm}} 映像檔。
{:shortdesc}

## 使用 CLI 存取公用 IBM 映像檔
{: #public_images_cli}

您可以使用指令行來存取公用 {{site.data.keyword.IBM_notm}} 映像檔。
{:shortdesc}

在開始之前，請完成下列作業：

- 登入 [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login)：

  ```
  ibmcloud login
  ```
  {: pre}

若要列出公用映像檔，請完成下列步驟：

1. 將全球登錄設為目標：

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. 列出 {{site.data.keyword.IBM_notm}} 公用映像檔：

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
