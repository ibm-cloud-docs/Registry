---

copyright:
  years: 2020
lastupdated: "2020-07-13"

keywords: external registry, private registry, OpenShift

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

# Using {{site.data.keyword.registrylong_notm}} as a private registry on Red Hat OpenShift
{: #registry_rhos}

You can add value to your Red Hat® OpenShift® clusters by using {{site.data.keyword.registrylong}} even where an internal registry is already provided.
{: shortdesc}

For example, if you have multiple clusters, {{site.data.keyword.registrylong_notm}} integrates conveniently with OpenShift Container Platform clusters so that you can build, share, synchronize, and scan image assets across clusters. For more information, see [Choosing an image registry solution](/docs/openshift?topic=openshift-registry#openshift_registry_options).

You can set up {{site.data.keyword.registrylong_notm}} to work with the internal registry of [{{site.data.keyword.openshiftlong_notm}}](#registry_rhos_rhoks) or [other OpenShift Container Platform providers](#registry_rhos_os).

## Set up {{site.data.keyword.openshiftlong_notm}} to use {{site.data.keyword.registrylong_notm}}
{: #registry_rhos_rhoks}

By default, your {{site.data.keyword.openshiftlong_notm}} clusters are set up with an internal registry that stores images locally in your cluster. The clusters are also set up with image pull secrets in the `default` project to pull images that you store in your private {{site.data.keyword.registrylong_notm}} repositories.

You can use either registry separately or in combination. When you set up the {{site.data.keyword.openshiftshort}} internal registry to import images from {{site.data.keyword.registrylong_notm}}, you get the advantage of a private registry that is common to multiple clusters. Another benefit is that copies of the pulled images from {{site.data.keyword.registrylong_notm}} are stored locally on the cluster, therefore reducing latency and external traffic, but you are subject to storage limitations.

To set up your {{site.data.keyword.openshiftlong_notm}} clusters to use the internal registry in combination with {{site.data.keyword.registrylong_notm}}, see the following topics in the {{site.data.keyword.openshiftlong_notm}} documentation:

- [Importing images from {{site.data.keyword.registrylong_notm}} into the internal registry image stream](/docs/openshift?topic=openshift-registry#imagestream_registry)
- [Setting up builds in the internal registry to push images to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#builds_registry)

## Set up Red Hat OpenShift Container Platform to use {{site.data.keyword.registrylong_notm}}
{: #registry_rhos_os}

To set up Red Hat OpenShift Container Platform, you must create secrets that have the credentials to access {{site.data.keyword.registrylong_notm}} so that you can perform the following actions.

- **Pull**: Create image pull secrets to [pull images](#registry_rhos_os_pull) from {{site.data.keyword.registrylong_notm}} to your OpenShift cluster. For example, you might deploy an app that uses an image in a private registry.
- **Push**: Create image push secrets to [push images](#registry_rhos_os_push) from your OpenShift cluster to a repository in {{site.data.keyword.registrylong_notm}}. For example, you might set up a continuous delivery pipeline that builds an image to a private registry instead of the internal registry.
- **Both**: Create a secret that can pull images from and push images to {{site.data.keyword.registrylong_notm}}. For example, you might set up a continuous delivery pipeline that builds an image to a private registry so that your team can pull the latest image across multiple clusters.

### Set up the Red Hat OpenShift Container Platform internal registry to pull from {{site.data.keyword.registrylong_notm}}
{: #registry_rhos_os_pull}

To configure Red Hat OpenShift Container Platform to pull from {{site.data.keyword.registrylong_notm}}, you must complete the following steps:

1. [Set up image pull secrets to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#other_registry_accounts) for each project that you want to pull images in.

2. [Configure Red Hat OpenShift Container Platform to use the image pull secrets](/docs/openshift?topic=openshift-registry#use_imagePullSecret) by adding the secrets to a service account in each project or by referring to the secret in your pod deployment. You are only required to add the secret to the projects that you want to pull to.

### Set up the Red Hat OpenShift Container Platform build to push images to {{site.data.keyword.registrylong_notm}}
{: #registry_rhos_os_push}

If you want to push application images from Red Hat OpenShift Container Platform to {{site.data.keyword.registrylong_notm}}, you must edit the Red Hat OpenShift Container Platform build configuration to point at {{site.data.keyword.registrylong_notm}}, where `myregistry.mycompany.io` is `<region_domain_name>.icr.io`. For more information about {{site.data.keyword.registrylong_notm}} regions and domain names, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

For instructions, see [Setting up builds in the internal registry to push images to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#builds_registry).
