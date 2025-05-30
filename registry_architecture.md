---

copyright:
  years: 2020, 2025
lastupdated: "2025-04-30"

keywords: IBM Cloud Container Registry architecture, segmentation, private connections, data plane, control plane, registry

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort_notm}} architecture and workload
{: #registry_architecture}

{{site.data.keyword.registrylong}} is a multi-tenant, highly available, scalable, and encrypted private image [registry](#x2064940){: term} that's hosted and managed by {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Both the control plane (management of images and configuration) and data plane (pushing and pulling your images) are multi-tenant. All parts of the service are hosted in an {{site.data.keyword.IBM_notm}} service account, which is not shared with users or other services.

In each regional instance of the [registry](/docs/Registry?topic=Registry-registry_overview#overview_elements_registry), the service runs in three physically separate data centers to ensure availability. All data and the configuration for each instance of the registry is retained within the region in which it is hosted. The global instance is also hosted in physically separate data centers. The data centers might not be in the same region as each other. For more information about regions, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

{{site.data.keyword.registrylong_notm}} runs in {{site.data.keyword.containerlong_notm}} clusters, and uses {{site.data.keyword.cos_full_notm}} to store images. Image data in {{site.data.keyword.cos_full_notm}} is encrypted at rest.

![Diagram showing deployment.](images/container_registry_architecture_mul.svg "Diagram that shows deployment in your account, MZRs, public ingress, private ingress, customer data flows, and dependencies (public and private)."){: caption="Diagram showing deployment" caption-side="bottom"}{: external download="../images/container_registry_architecture_mul.svg"}

## Segmentation of data
{: #registry_architecture_segment}

Segmentation of data within {{site.data.keyword.registrylong_notm}} is achieved by using private [namespaces](#x2031005){: term}, which are strictly owned by single accounts.

You can control access to [namespaces](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace) within the account by using {{site.data.keyword.iamshort}} (IAM) access policies. Storage in {{site.data.keyword.cos_full_notm}} is not segmented, but user accounts do not have direct access to the {{site.data.keyword.cos_full_notm}} that contains the image data. For more information, see [Managing IAM access for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam).

All traffic to the registry, and from the service to {{site.data.keyword.registrylong_notm}} dependencies is encrypted in transit. No additional network-level segmentation of traffic is provided. The control plane and data plane are not separated from each other.

## Private connections
{: #registry_architecture_private_connections}

You can decide whether your data plane interactions use private connections. Additionally, you can choose to prohibit public data plane connections for your account.

The flow of all customer data between {{site.data.keyword.registrylong_notm}} and its dependencies uses private network connections. For more information about private connections, see [Securing your connection to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_private).
