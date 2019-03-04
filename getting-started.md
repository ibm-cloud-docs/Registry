---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-04"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security, cli, namespaces, tutorial, Docker, images, registry

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

# Getting started tutorial
{: #getting-started}

{{site.data.keyword.registrylong}} provides a multi-tenant private image registry that you can use to store and share your Docker images with users in your {{site.data.keyword.Bluemix_notm}} account.
{:shortdesc}

The {{site.data.keyword.Bluemix_notm}} console includes a brief Quick Start. To find out more about how to use the {{site.data.keyword.Bluemix_notm}} console, see [Managing image security with Vulnerability Advisor](/docs/services/va?topic=va-va_index).

Do not put personal information in your container images, namespace names, description fields (for example, in registry tokens), or in any image configuration data (for example, image names or image labels).
{: important}

## Install the {{site.data.keyword.registrylong_notm}} CLI
{: #registry_cli_install}

1. Install the [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli) so that you can run the {{site.data.keyword.Bluemix_notm}} `ibmcloud` commands. This installation also installs the CLI plug-ins for {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.registrylong_notm}}.

## Set up a namespace
{: #registry_namespace_add}

1. Log in to {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

   If you have a federated ID, log in by using the following command:

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. Add a namespace to create your own image repository. Replace `<my_namespace>` with your preferred namespace.

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

3. To ensure that your namespace is created, run the `ibmcloud cr namespace-list` command.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Pull images from another registry to your local machine
{: #registry_images_pulling}

1. [Install the Docker CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.docker.com/community-edition#/download). For Windows 8, or OS X Yosemite 10.10.x or earlier, install [Docker Toolbox ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.docker.com/toolbox/) instead. {{site.data.keyword.registrylong_notm}} supports Docker Engine v1.12.6, or later.

2. Download (_pull_) the image to your local machine. Replace `<source_image>` with the repository of the image and `<tag>` with the tag of the image that you want to use, for example, _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Example, where `<source_image>` is `hello-world` and `<tag>` is `latest`:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Tag the image. Replace `<source_image>` with the repository and `<tag>` with the tag of your local image that you pulled earlier. Replace `<region>` with the name of your [region](/docs/services/Registry?topic=registry-registry_overview#registry_regions). Replace `<my_namespace>` with the namespace that you created in [Set up a namespace](/docs/services/Registry?topic=registry-index#registry_namespace_add). Define the repository and tag of the image that you want to use in your namespace by replacing `<new_image_repo>` and `<new_tag>`.

   ```
   docker tag <source_image>:<tag> <region>.icr.io/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Example, where `<source_image>` is `hello-world`, `<tag>` is `latest`, `<region>` is `uk`, `<my_namespace>` is `namespace1`, `<new_image_repo>` is `hw_repo`, and `<new_tag>` is `1`:

   ```
   docker tag hello-world:latest uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

## Push Docker images to your namespace
{: #registry_images_pushing}

1. Run the `ibmcloud cr login` command to log your local Docker daemon into {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Upload (_push_) the image to your namespace. Replace `<my_namespace>` with the namespace that you created in [Set up a namespace](/docs/services/Registry?topic=registry-index#registry_namespace_add), and `<image_repo>` and `<tag>` with the repository and the tag of the image that you chose when you tagged the image.

   ```
   docker push <region>.icr.io/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}
   
   Example, where `<region>` is `uk`, `<my_namespace>` is `namespace1`, `<image_repo>` is `hw_repo`, and `<tag>` is `1`:

   ```
   docker push uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

3. Verify that the image was pushed successfully by running the following command.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Good work! You set up a namespace in {{site.data.keyword.registrylong_notm}} and pushed your first image to your namespace.

## Next steps
{: #get_start_next}

- [Managing image security with Vulnerability Advisor](/docs/services/va?topic=va-va_index)
- [Review your service plans and usage](/docs/services/Registry?topic=registry-registry_overview#registry_plans)
- [Store and manage more images in your namespace](/docs/services/Registry?topic=registry-registry_images_)
- [Defining user access role policies](/docs/services/Registry?topic=registry-user#user)
- [Setting up clusters and worker nodes](/docs/containers?topic=containers-clusters#clusters)
