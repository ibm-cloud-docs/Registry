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

# Immagini {{site.data.keyword.IBM_notm}} pubbliche
{: #public_images}

Puoi accedere alle immagini fornite da {{site.data.keyword.IBM}} utilizzando la riga di comando. Non puoi più accedere alle immagini {{site.data.keyword.IBM_notm}} pubbliche utilizzando la GUI (graphical user interface).
{:shortdesc}

## Accesso alle immagini IBM pubbliche utilizzando la CLI
{: #public_images_cli}

Puoi accedere alle immagini {{site.data.keyword.IBM_notm}} pubbliche utilizzando la riga di comando.
{:shortdesc}

Prima di cominciare, completa la seguente attività:

- Accedi a [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login):

  ```
  ibmcloud login
  ```
  {: pre}

Per elencare le immagini pubbliche, completa la seguente procedura:

1. Specifica il registro globale:

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. Elenca le immagini pubbliche {{site.data.keyword.IBM_notm}}:

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
