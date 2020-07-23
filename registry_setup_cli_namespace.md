---

copyright:
  years: 2017, 2020
lastupdated: "2020-07-23"

keywords: namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, setting up cli, installing cli, uninstalling cli, 

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

# Setting up the {{site.data.keyword.registrylong_notm}} CLI and your registry namespace
{: #registry_setup_cli_namespace}

To manage your Docker images in {{site.data.keyword.registrylong}}, you must install the `container-registry` CLI plug-in and create a namespace.
{:shortdesc}

Do not put personal information in your container images, namespace names, description fields, or in any image configuration data (for example, image names or image labels).
{: important}

To add and remove namespaces, you must have the Manager role at the account level, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).
{: tip}

Before you begin, install the {{site.data.keyword.cloud_notm}} CLI, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

## Installing the `container-registry` CLI plug-in
{: #cli_namespace_registry_cli_install}

Install the `container-registry` CLI plug-in to use the command line to manage your namespaces and Docker images in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Install the `container-registry` CLI plug-in.](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install)
2. Optional: [Configure your Docker client to run commands without root permissions](https://docs.docker.com/install/linux/linux-postinstall/){: external}. If you do not do this step, you must run `ibmcloud login`, `ibmcloud cr login`, `docker pull`, and `docker push` commands with `sudo` or as root.

You can now [set up your own namespace](#registry_namespace_setup) in {{site.data.keyword.registrylong_notm}}.

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

## Planning namespaces
{: #registry_setup_cli_namespace_plan}

{{site.data.keyword.registrylong_notm}} provides a multi-tenant private image registry that is hosted and managed by IBM. You can store and share your Docker images in this registry by setting up a registry namespace.
{:shortdesc}



You can set up multiple namespaces, for example, to have separate repositories for your production and staging environments. If you want to use the registry in multiple {{site.data.keyword.cloud_notm}} regions, you must set up a namespace for each region. Namespace names are unique within regions. You can use the same namespace name for each region, unless someone else already has a namespace with that name set up in that region.

You can have 100 namespaces in each region.
{: note}

To add and remove namespaces, you must have the Manager role at the account level, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

You can control access to your namespaces by using IAM policies. For more information, see [Defining user access role policies](/docs/Registry?topic=Registry-user#user).

To work with the IBM-provided public images only, you do not need to set up a namespace.

If you are unsure whether a namespace is already set for your account, run the `ibmcloud cr namespace-list` command to retrieve existing namespace information.
{:tip}

Consider the following rules when you choose a namespace:

- Your namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region.
- Your namespace must have 4 - 30 characters.
- Your namespace must start and end with a letter or number.
- Your namespace must contain lowercase letters, numbers, hyphens (-), and underscores (_) only.

Do not put personal information in your namespace names.
{: important}

After you set your first namespace, you are assigned the free {{site.data.keyword.registrylong_notm}} service plan if you have not already [upgraded your plan](/docs/Registry?topic=Registry-registry_overview#registry_plan_upgrade).

## Setting up a namespace
{: #registry_namespace_setup}

You must create a namespace to store your Docker images in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Before you begin, complete the following tasks:

- [Install the {{site.data.keyword.cloud_notm}} CLI and the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install).
- [Plan how to use and name your registry namespaces](#registry_setup_cli_namespace_plan).

To create a namespace, see [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add) in the Getting Started documentation.

The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters, and contain lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.
{: tip}

You can now [push Docker images to your namespace in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_images_#registry_images_pushing_namespace) and share these images with other users in your account. To control access to namespaces in {{site.data.keyword.cloud_notm}} IAM, see [Creating policies](/docs/Registry?topic=Registry-user#create).

## Removing namespaces
{: #registry_remove}

If you no longer require a registry namespace, you can remove the namespace from your {{site.data.keyword.cloud_notm}} account.
{:shortdesc}

1. Log in to {{site.data.keyword.cloud_notm}}.

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
