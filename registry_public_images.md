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

You can no longer access public {{site.data.keyword.IBM}} images in the graphical user interface. However, you can still access the images by using the CLI.
{:shortdesc}

## Accessing the public IBM images by using the CLI
{: #public_images_cli}

You can access the IBM public images by using the command line.
{:shortdesc}

To list public images, run the following `ibmcloud` commands to target the global registry and list the IBM-provided public images:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}
