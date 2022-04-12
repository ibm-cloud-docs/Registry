---

copyright:
  years: 2018, 2022
lastupdated: "2022-04-12"

keywords: Public IBM images, images, accessing images, container images, public images

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Public {{site.data.keyword.IBM_notm}} images
{: #public_images}

You can access the images that are provided by {{site.data.keyword.IBM_notm}} by using the {{site.data.keyword.registrylong}} command line.
{: shortdesc}

 You can't access the public {{site.data.keyword.IBM_notm}} images by using the {{site.data.keyword.cloud_notm}} console anymore.
 {: note}

## Accessing the public IBM images by using the CLI
{: #public_images_cli}

You can access the public {{site.data.keyword.IBM_notm}} images by using the command line.

Before you begin, complete the following tasks.

1. Ensure that the {{site.data.keyword.registrylong_notm}} CLI is installed, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

2. Log in to [{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).

    ```txt
    ibmcloud login
    ```
    {: pre}

To list the public images, complete the following steps.

1. Target the global registry:

    ```txt
    ibmcloud cr region-set global
    ```
    {: pre}

2. List the {{site.data.keyword.IBM_notm}} public images.

    ```txt
    ibmcloud cr images --include-ibm
    ```
    {: pre}


