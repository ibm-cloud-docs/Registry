---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, 

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

# Setting up the {{site.data.keyword.registrylong_notm}} CLI and your registry namespace
{: #registry_setup_cli_namespace}

Before you can store your Docker images in {{site.data.keyword.registrylong}}, you must create a namespace. To work with namespaces, install the `container-registry` CLI plug-in.
{:shortdesc}

Do not put personal information in your container images, namespace names, description fields (for example, in registry tokens), or in any image configuration data (for example, image names or image labels).
{: important}

Before you begin, install the [{{site.data.keyword.Bluemix_notm}} CLI)](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

## Installing the `container-registry` CLI plug-in
{: #cli_namespace_registry_cli_install}

Install the `container-registry` CLI plug-in to use the command line to manage your namespaces and Docker images in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Install the `container-registry` CLI plug-in.](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Optional: [Configure your Docker client to run commands without root permissions ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.docker.com/engine/installation/linux/linux-postinstall). If you do not do this step, you must run `ibmcloud login`, `ibmcloud cr login`, `docker pull`, and `docker push` commands with **sudo** or as root.

You can now set up your own namespace in {{site.data.keyword.registrylong_notm}}.

## Updating the `container-registry` CLI plug-in
{: #registry_cli_update}

You might want to update the `container-registry` CLI plug-in periodically to use new features.
{:shortdesc}

1. Update the `container-registry` CLI plug-in.

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. Verify that the `container-registry` CLI plug-in was updated successfully.

    ```
    ibmcloud plugin list
    ```
     {: pre}

## Uninstalling the `container-registry` CLI plug-in
{: #registry_cli_uninstall}

If you no longer need the `container-registry` CLI plug-in, you can uninstall it.
{:shortdesc}

1. Uninstall the `container-registry` CLI plug-in.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. Verify that the `container-registry` CLI plug-in was uninstalled successfully.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    The `container-registry` CLI plug-in is not displayed in the results.

## Setting up a namespace
{: #registry_namespace_setup}

You must create a namespace to store your Docker images in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Before you begin**

- [Install the {{site.data.keyword.Bluemix_notm}} CLI and the `container-registry` CLI plug-in](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Plan how to use and name your registry namespaces](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces).

Create a namespace, see [Set up a namespace](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add) in the Getting Started documentation.

You can now [push Docker images to your namespace in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) and share these images with other users in your account.

## Removing namespaces
{: #registry_remove}

If you no longer require a registry namespace, you can remove the namespace from your {{site.data.keyword.Bluemix_notm}} account.
{:shortdesc}

1. Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. List available namespaces.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. Remove a namespace.

    **Attention:** When you remove a namespace, any images that are stored in that namespace are also deleted. This action cannot be undone.

    Replace `<my_namespace>` with the namespace that you want to remove.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    After you delete a namespace, it might take a few minutes before that namespace becomes available again to reuse.
