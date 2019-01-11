---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Setting up the {{site.data.keyword.registrylong_notm}} CLI and your registry namespace
{: #registry_setup_cli_namespace}

Before you can store your Docker images in {{site.data.keyword.registrylong}}, you must create a namespace. To work with namespaces, you must install the `container-registry` CLI plug-in.
{:shortdesc}

Do not put personal information in your container images, namespace names, description fields (for example, in registry tokens), or in any image configuration data (for example, image names or image labels).
{:tip}

Before you begin, install the [{{site.data.keyword.Bluemix_notm}} CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://clis.ng.bluemix.net/ui/home.html).

## Installing the `container-registry` CLI plug-in
{: #registry_cli_install}

Install the `container-registry` CLI plug-in to use the command line to manage your namespaces and Docker images in the {{site.data.keyword.Bluemix_notm}} private registry.
{:shortdesc}

1. [Install the `container-registry` CLI plug-in.](index.html#registry_cli_install)
2. Optional: [Configure your Docker client to run commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If you do not do this step, you must run `ibmcloud login`, `ibmcloud cr login`, `docker pull`, and `docker push` commands with **sudo** or as root.

You can now set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry.

## Updating the `container-registry` CLI plug-in
{: #registry_cli_update}

You might want to update the `container-registry` CLI plug-in periodically to use new features.
{:shortdesc}

1. Update the `container-registry` CLI plug-in.

    ```
    ibmcloud plugin update container-registry -r Bluemix
    ```
    {: pre}

2. Verify that the `container-registry` CLI plug-in updated successfully.

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

2. Verify that the `container-registry` CLI plug-in uninstalled successfully.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    The `container-registry` CLI plug-in is not displayed in the results.

## Setting up a namespace
{: #registry_namespace_add}

To securely store your Docker images, you must create a namespace in the {{site.data.keyword.registrylong_notm}} private registry.
{:shortdesc}

**Before you begin**

- [Install the {{site.data.keyword.Bluemix_notm}} CLI and the `container-registry` CLI plug-in](#registry_cli_install).
- [Plan how to use and name your registry namespaces](registry_overview.html#registry_namespaces).

Create a namespace, see [Set up a namespace](index.html#registry_namespace_add) in the Getting Started documentation.

You can now [push Docker images to your namespace in the {{site.data.keyword.registrylong_notm}} registry](registry_images_.html#registry_images_pushing) and share these images with other users in your account.

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

    Replace _&lt;my_namespace&gt;_ with the namespace that you want to remove.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    After you delete a namespace, depending on the number of images that were stored, it might take a few minutes before that namespace becomes available again to reuse.
