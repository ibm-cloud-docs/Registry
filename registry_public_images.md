---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

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

# Public {{site.data.keyword.IBM_notm}} images
{: #public_images}

You can access the images that are provided by {{site.data.keyword.IBM}} by using the command line. You can't access the public {{site.data.keyword.IBM_notm}} images by using the graphical user interface anymore.
{:shortdesc}

## Accessing the public IBM images by using the CLI
{: #public_images_cli}

You can access the public {{site.data.keyword.IBM_notm}} images by using the command line.
{:shortdesc}

**Before you begin**

- Log in to [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login):

  ```
  ibmcloud login
  ```
  {: pre}

To list the public images, complete the following steps:

1. Target the global registry:

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. List the {{site.data.keyword.IBM_notm}} public images:

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
