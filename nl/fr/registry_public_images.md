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

# Images {{site.data.keyword.IBM_notm}} publiques
{: #public_images}

Vous pouvez accéder aux images qui sont fournies par {{site.data.keyword.IBM}} à l'aide de la ligne de commande. Vous ne pouvez plus accéder aux images {{site.data.keyword.IBM_notm}} publiques à l'aide de l'interface graphique.
{:shortdesc}

## Accès aux images IBM publiques à l'aide de l'interface de ligne de commande
{: #public_images_cli}

Vous pouvez accéder aux images {{site.data.keyword.IBM_notm}} publiques à l'aide de la ligne de commande.
{:shortdesc}

**Avant de commencer**

- Connectez-vous à [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login) :

  ```
  ibmcloud login
  ```
  {: pre}

Pour répertorier les images publiques, procédez comme suit :

1. Ciblez le registre global :

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. Répertoriez les images {{site.data.keyword.IBM_notm}} publiques :

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
