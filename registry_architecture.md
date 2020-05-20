---

copyright:
  years: 2020
lastupdated: "2020-05-20"

keywords: IBM Cloud Container Registry architecture,

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

# {{site.data.keyword.registrylong_notm}} architecture and workload
{: #registry_architecture}

{{site.data.keyword.registrylong}} is a multi-tenant, highly available, scalable, and encrypted private image registry that is hosted and managed by {{site.data.keyword.IBM}}. Both the control plane (management of images and configuration) and data plane (pushing and pulling your images) are multi-tenant. All parts of the service are hosted in an {{site.data.keyword.IBM_notm}} service account, which is not shared with users or other services.
{: shortdesc}

In each regional instance of the registry, the service runs in three physically separate datacenters to ensure availability. All data and the configuration for each instance of the registry is retained within the region in which it is hosted. The global instance is also hosted in physically separate datacenters. The datacenters might not be in the same region as each other. For more information about regions, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

{{site.data.keyword.registrylong_notm}} runs in {{site.data.keyword.containerlong_notm}} clusters, and uses {{site.data.keyword.cos_full_notm}} to store images. Image data in {{site.data.keyword.cos_full_notm}} is encrypted at rest.

![Image showing deployment.](images/container-registry_deployment_model.svg "Image showing deployment in your account, MZRs, public ingress, private ingress, customer data flows, and dependencies (public/private)."){: caption="Figure 1. Image showing deployment" caption-side="bottom"}

## Segregation
{: #registry_architecture_segregation}

Segregation of data within {{site.data.keyword.registrylong_notm}} is achieved by using private namespaces, which are strictly owned by single accounts. You can control access to namespaces within the account by using {{site.data.keyword.iamlong}} (IAM) access policies. Storage in {{site.data.keyword.cos_full_notm}} is not segregated, but user accounts do not have direct access to the {{site.data.keyword.cos_full_notm}} that contains the image data. For more informatiom, see [Managing access for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam).

All traffic to the registry, and from the service to {{site.data.keyword.registrylong_notm}} dependencies is encrypted in transit. No additional network level segregation of traffic is provided.

The control plane and data plane are not segregated from each other.

## Private connections
{: #registry_architecture_private_connections}

You can decide whether your data plane interactions use private connections. Additionally, you can choose to prohibit public data plane connections for your account.

The flow of all customer data between {{site.data.keyword.registrylong_notm}} and its dependencies uses private network connections.

For more information about private connections, see [Securing your connection to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_private).

## Dependencies
{: #registry_architecture_dependencies}

### Dependencies that are used for customer data, all of which use private network connections
{: #registry_architecture_dependencies_private}

- [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started)

### Other dependencies that use private network connections
{: #registry_architecture_dependencies_other}

- [{{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant) \*
- [{{site.data.keyword.la_full_notm}}](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-getting-started)
- [{{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started)
- [{{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started)

\* Connection to {{site.data.keyword.cloudant_short_notm}} is not private in eu-central (`de.icr.io`).

### Dependencies that use public connections
{: #registry_architecture_dependencies_public}

- [{{site.data.keyword.iamlong}} (IAM)](/docs/iam?topic=iam-getstarted)
