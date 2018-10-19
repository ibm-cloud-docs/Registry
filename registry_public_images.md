---

copyright:
  years: 2018
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

# Public {{site.data.keyword.IBM_notm}} images
{: #public_images}

You can't access public {{site.data.keyword.IBM}} images in the graphical user interface anymore. However, you can still access the images by using the command line.
{:shortdesc}

## Accessing the public IBM images by using the CLI
{: #public_images_cli}

You can access the IBM public images by using the command line.
{:shortdesc}

**Before you begin**

- Log in to [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login):

  ```
  ibmcloud login
  ```
  {: pre}

- Log in to {{site.data.keyword.registrylong_notm}}:
  
  ```
  ibmcloud cr login
  ```
  {: pre}

To list public images, run the following `ibmcloud` commands to target the global registry and list the IBM-provided public images:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}
