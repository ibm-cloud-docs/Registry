---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-18"

keywords: Public IBM images, images, accessing images, container images, public images,

subcollection: Registry

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
{:term: .term}
{:external: target="_blank" .external}

# Public {{site.data.keyword.IBM_notm}} images
{: #public_images}

You can access the images that are provided by {{site.data.keyword.IBM}} by using the command line. You can't access the public {{site.data.keyword.IBM_notm}} images by using the {{site.data.keyword.cloud_notm}} console anymore.
{: shortdesc}

## Accessing the public IBM images by using the CLI
{: #public_images_cli}

You can access the public {{site.data.keyword.IBM_notm}} images by using the command line.
{: shortdesc}

Before you begin, complete the following tasks:

- Ensure that the {{site.data.keyword.registrylong_notm}} CLI is installed, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).
- Log in to [{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).

    ```
    ibmcloud login
    ```
    {: pre}

To list the public images, complete the following steps.

1. Target the global registry:

    ```
    ibmcloud cr region-set global
    ```
    {: pre}

2. List the {{site.data.keyword.IBM_notm}} public images.

    ```
    ibmcloud cr images --include-ibm
    ```
    {: pre}


