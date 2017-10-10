---

copyright:
  years: 2017
lastupdated: "2017-10-10"

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

Before you can store your Docker images in {{site.data.keyword.registrylong}}, you must install the {{site.data.keyword.Bluemix_notm}} CLI and the {{site.data.keyword.registrylong_notm}} plug-in, and then set up a registry namespace to create your own image repository in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}


## Installing the {{site.data.keyword.registrylong_notm}} CLI (`bx cr`) plug-in
{: #registry_cli_install}

Install the {{site.data.keyword.registrylong_notm}} CLI to use the command line to manage your namespaces and Docker images in the {{site.data.keyword.Bluemix_notm}} private registry.
{:shortdesc}

1.  [Install the container-registry plug-in.](index.html#registry_cli_install)
2.  Optional: [Configure your Docker client to run commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If you do not perform this step, you must run `bx login`, `bx cr login`, `docker pull`, and `docker push` commands with **sudo** or as root.

You can now set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry.

## Updating the {{site.data.keyword.registrylong_notm}} (`bx cr`) plug-in
{: #registry_cli_update}

You might want to update the {{site.data.keyword.registrylong_notm}} CLI periodically to use new features.
{:shortdesc}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Update the container-registry plug-in.

    ```
    bx plugin update container-registry -r {{site.data.keyword.Bluemix_notm}}
    ```
    {: pre}

3.  Verify that the plug-in is updated successfully.

    ```
    bx plugin list
    ```
     {: pre}


## Uninstalling the {{site.data.keyword.registrylong_notm}} (`bx cr`) plug-in
{: #registry_cli_uninstall}

If you no longer need the container-registry plug-in, you can uninstall it.
{:shortdesc}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Uninstall the container-registry plug-in.

    ```
    bx plugin uninstall container-registry
    ```
    {: pre}

3.  Verify that the plug-in was uninstalled successfully.

    ```
    bx plugin list
    ```
    {: pre}

    The container-registry plug-in is not displayed in the results.


## Setting up a namespace in {{site.data.keyword.registrylong_notm}}
{: #registry_namespace_add}

To securely store your Docker images, you must create a namespace in the {{site.data.keyword.registrylong_notm}} private registry.
{:shortdesc}

Before you begin:

-   [Install the {{site.data.keyword.Bluemix_notm}} CLI and the container-registry plug-in](#registry_cli_install).
-   [Plan how to use and name your registry namespaces](registry_overview.html#registry_namespaces).

Create a namespace, see [Set up a namespace](index.html#registry_namespace_add) in the Getting Started documentation.

You can now [push Docker images to your namespace in the {{site.data.keyword.Bluemix_notm}} registry](registry_images_.html#registry_images_pushing) and share these images with other users in your account.

## Removing namespaces in {{site.data.keyword.registrylong_notm}}
{: #registry_remove}

If you no longer require a namespace, you can remove the namespace from your {{site.data.keyword.Bluemix_notm}} account.
{:shortdesc}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  List available namespaces.

    ```
    bx cr namespace-list
    ```
    {: pre}

3.  Remove a namespace. 

    **Attention:** When you remove a namespace, any images that are stored in that namespace are also deleted. This action cannot be undone.
    
    Replace _&lt;my_namespace&gt;_ with the namespace that you want to remove.

    ```
    bx cr namespace-rm <my_namespace>
    ```
    {: pre}

    After you delete a namespace, depending on the number of images that were stored, it might take a few minutes before that namespace becomes available again to reuse.
