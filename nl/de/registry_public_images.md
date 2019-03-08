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

# Öffentliche {{site.data.keyword.IBM_notm}}-Images
{: #public_images}

Sie können auf die Images, die von {{site.data.keyword.IBM}} bereitgestellt werden, über die Befehlszeile zugreifen. Sie können nicht mehr über die grafische Benutzerschnittstelle auf die öffentlichen {{site.data.keyword.IBM_notm}}-Images zugreifen.
{:shortdesc}

## Auf die öffentlichen IBM Images über die Befehlszeilenschnittstelle zugreifen
{: #public_images_cli}

Sie können auf die öffentlichen {{site.data.keyword.IBM_notm}} Images über die Befehlszeile zugreifen.
{:shortdesc}

**Vorbereitung**

- Melden Sie sich bei [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login) an:

  ```
  ibmcloud login
  ```
  {: pre}

Führen Sie die folgenden Schritte aus, um die öffentlichen Images aufzulisten:

1. Legen Sie die globale Registry als Ziel fest:

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. Listen Sie die öffentlichen {{site.data.keyword.IBM_notm}} Images auf:

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
