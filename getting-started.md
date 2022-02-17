---

copyright:
  years: 2017, 2022
lastupdated: "2022-02-17"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security, cli, tutorial, Docker, images, registry, Podman

subcollection: Registry

content-type: tutorial
services: containers
account-plan: lite
completion-time: 45m

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.registrylong_notm}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-services="containers"}
{: toc-completion-time="45m"}

{{site.data.keyword.registrylong}} provides a multi-tenant private image registry that you can use to store and share your container images with users in your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

The {{site.data.keyword.cloud_notm}} console includes a brief Quick Start. To find out more about how to use the {{site.data.keyword.cloud_notm}} console, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index).

Do not put personal information in your container images, namespace names, description fields, or in any image configuration data (for example, image names or image labels).
{: important}

## Install the {{site.data.keyword.registrylong_notm}} CLI
{: #gs_registry_cli_install}
{: step}

1. Install the {{site.data.keyword.cloud_notm}} CLI so that you can run the {{site.data.keyword.cloud_notm}} `ibmcloud` commands, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). This installation also installs the CLI plug-ins for {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.registrylong_notm}}.

## Set up a namespace
{: #gs_registry_namespace_add}
{: step}
{: help}
{: support}

Create a namespace. The namespace is created in the [resource group](x2161955){: term} that you specify so that you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. If you don't specify a resource group, and you don't target a resource group, the default resource group is used. Namespaces that are assigned to a resource group show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

1. Log in to {{site.data.keyword.cloud_notm}}.

    ```txt
    ibmcloud login
    ```
    {: pre}

    If you have a federated ID, use `ibmcloud login --sso` to log in. Enter your username and use the provided URL in your CLI output to retrieve your one-time passcode. If you have a federated ID, the login fails without the `--sso` and succeeds with the `--sso` option.
    {: tip}

2. Add a namespace to create your own image repository. Replace `<my_namespace>` with your preferred namespace.

    The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters, and contain lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.
    {: tip}

    ```txt
    ibmcloud cr namespace-add <my_namespace>
    ```
    {: pre}

    You can put the namespace in a resource group of your choice by using one of the following options.

    - Before you create the namespace, run the [`ibmcloud target -g <resource_group>`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target) command, where `<resource_group>` is the resource group.
    - Specify the resource group by using the `-g` option on the [`ibmcloud cr namespace-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add) command.

3. To ensure that your namespace is created, run the `ibmcloud cr namespace-list` command.

    ```txt
    ibmcloud cr namespace-list -v
    ```
    {: pre}

## Pull images from another registry to your local computer
{: #gs_registry_images_pulling}
{: step}
{: help}
{: support}

1. [Install the Docker Engine CLI](https://www.docker.com/products/container-runtime#/download){: external}. For Windows&reg; 8, or OS X Yosemite 10.10.x or earlier, install [Docker Toolbox](https://docs.docker.com/toolbox/){: external} instead. {{site.data.keyword.registrylong_notm}} supports Docker Engine v1.12.6, or later.

2. Download (_pull_) the image to your local computer. Replace `<source_image>` with the repository of the image and `<tag>` with the tag of the image that you want to use, for example, `latest`.

    ```txt
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Example, where `<source_image>` is `hello-world` and `<tag>` is `latest`:

    ```txt
    docker pull hello-world:latest
    ```
    {: pre}

3. Tag the image. Replace `<source_image>` with the repository and `<tag>` with the tag of your local image that you pulled earlier. Replace `<region>` with the name of your [region](/docs/Registry?topic=Registry-registry_overview#registry_regions). Replace `<my_namespace>` with the namespace that you created in [Step 2. Set up a namespace](#gs_registry_namespace_add). Define the repository and tag of the image that you want to use in your namespace by replacing `<new_image_repo>` and `<new_tag>`.

    ```txt
    docker tag <source_image>:<tag> <region>.icr.io/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    To find the name of your region, run the `ibmcloud cr region` command.
    {: tip}

    Example, where `<source_image>` is `hello-world`, `<tag>` is `latest`, `<region>` is `uk`, `<my_namespace>` is `namespace1`, `<new_image_repo>` is `hw_repo`, and `<new_tag>` is `1`:

    ```txt
    docker tag hello-world:latest uk.icr.io/namespace1/hw_repo:1
    ```
    {: pre}

## Push Docker images to your namespace
{: #gs_registry_images_pushing}
{: step}
{: help}
{: support}

{{site.data.keyword.registrylong_notm}} supports other clients as well as Docker. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).
{: tip}

1. Run the `ibmcloud cr login` command to log your local Docker daemon into {{site.data.keyword.registrylong_notm}}.

    ```txt
    ibmcloud cr login
    ```
    {: pre}

2. Upload (_push_) the image to your namespace. Replace `<my_namespace>` with the namespace that you created in [Step 2. Set up a namespace](#gs_registry_namespace_add). Replace `<image_repo>` and `<tag>` with the repository and the tag of the image that you chose when you tagged the image.

    ```txt
    docker push <region>.icr.io/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    Example, where `<region>` is `uk`, `<my_namespace>` is `namespace1`, `<image_repo>` is `hw_repo`, and `<tag>` is `1`:

    ```txt
    docker push uk.icr.io/namespace1/hw_repo:1
    ```
    {: pre}

3. Verify that the image was pushed successfully by running the following command.

    ```txt
    ibmcloud cr image-list
    ```
    {: pre}

You set up a namespace in {{site.data.keyword.registrylong_notm}} and pushed your first image to your namespace.

## Next steps
{: #gs_get_start_next}

- [Manage image security with Vulnerability Advisor.](/docs/Registry?topic=va-va_index)
- [Review your service plans.](/docs/Registry?topic=Registry-registry_overview#registry_plans)
- [Store and manage more images in your namespace.](/docs/Registry?topic=Registry-registry_images_)
- [Define user access role policies.](/docs/Registry?topic=Registry-user#user)
- [Set up clusters and worker nodes.](/docs/containers?topic=containers-clusters#clusters)


