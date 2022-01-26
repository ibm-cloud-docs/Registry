---

copyright:
  years: 2020, 2022
lastupdated: "2022-01-26"

keywords: IBM Cloud Container Registry architecture,

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registrylong_notm}} architecture and workload
{: #registry_architecture}

{{site.data.keyword.registrylong}} is a multi-tenant, highly available, scalable, and encrypted private image registry that is hosted and managed by {{site.data.keyword.IBM}}. Both the control plane (management of images and configuration) and data plane (pushing and pulling your images) are multi-tenant. All parts of the service are hosted in an {{site.data.keyword.IBM_notm}} service account, which is not shared with users or other services.
{: shortdesc}

In each regional instance of the registry, the service runs in three physically separate data centers to ensure availability. All data and the configuration for each instance of the registry is retained within the region in which it is hosted. The global instance is also hosted in physically separate data centers. The data centers might not be in the same region as each other. For more information about regions, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

{{site.data.keyword.registrylong_notm}} runs in {{site.data.keyword.containerlong_notm}} clusters, and uses {{site.data.keyword.cos_full_notm}} to store images. Image data in {{site.data.keyword.cos_full_notm}} is encrypted at rest.

![Image showing deployment.](images/container-registry_deployment_model.svg "Image showing deployment in your account, MZRs, public ingress, private ingress, customer data flows, and dependencies (public and private)."){: caption="Figure 1. Image showing deployment" caption-side="bottom"}

## Segmentation
{: #registry_architecture_segregation}

Segmentation of data within {{site.data.keyword.registrylong_notm}} is achieved by using private namespaces, which are strictly owned by single accounts.
{: shortdesc}

You can control access to namespaces within the account by using {{site.data.keyword.iamlong}} (IAM) access policies. Storage in {{site.data.keyword.cos_full_notm}} is not segregated, but user accounts do not have direct access to the {{site.data.keyword.cos_full_notm}} that contains the image data. For more information, see [Managing access for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam).

All traffic to the registry, and from the service to {{site.data.keyword.registrylong_notm}} dependencies is encrypted in transit. No additional network level segmentation of traffic is provided. The control plane and data plane are not segregated from each other.

## Private connections
{: #registry_architecture_private_connections}

You can decide whether your data plane interactions use private connections. Additionally, you can choose to prohibit public data plane connections for your account.
{: shortdesc}

The flow of all customer data between {{site.data.keyword.registrylong_notm}} and its dependencies uses private network connections. For more information about private connections, see [Securing your connection to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_private).

## Dependencies to other {{site.data.keyword.cloud_notm}} services
{: #registry_architecture_dependencies_cloud}

Review the {{site.data.keyword.cloud_notm}} services that {{site.data.keyword.registrylong_notm}} connects to over public or private connections.
{: shortdesc}

| Service name | Description |
|------------|-------------------------------------|
| {{site.data.keyword.at_full_notm}} | {{site.data.keyword.registrylong_notm}} integrates with {{site.data.keyword.at_short}}, by using a private connection, to forward {{site.data.keyword.registryshort_notm}} audit events to the {{site.data.keyword.at_short}} service instances that you set up. For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events). |
| {{site.data.keyword.databases-for-postgresql_full_notm}} | {{site.data.keyword.databases-for-postgresql_full_notm}} is a fully managed, highly available object-relational SQL database. {{site.data.keyword.registrylong_notm}} integrates with {{site.data.keyword.databases-for-postgresql_full_notm}} to store metadata. Connections to {{site.data.keyword.databases-for-postgresql_full_notm}} are private. |
| {{site.data.keyword.cis_full_notm}} | {{site.data.keyword.cis_full_notm}} is used as a provider for DNS and load-balancing capabilities in {{site.data.keyword.registrylong_notm}}. |
| {{site.data.keyword.containerlong_notm}} | {{site.data.keyword.registrylong_notm}} uses {{site.data.keyword.containerlong_notm}} to run its service. |
| {{site.data.keyword.mon_full_notm}} | {{site.data.keyword.registrylong_notm}} integrates with {{site.data.keyword.mon_short}}, by using a private connection, to send platform metrics. For more information, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor). |
| {{site.data.keyword.cos_full_notm}} | {{site.data.keyword.registryshort_notm}} stores customer data (images) in {{site.data.keyword.cos_short}} by using a private connection. All data is encrypted in transit and at rest. For more information, see [Managing your data in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-delete-data).|
| {{site.data.keyword.cloud_notm}} Platform | To authenticate requests to the service and authorize user actions, {{site.data.keyword.registrylong_notm}} implements platform and service access roles in {{site.data.keyword.iamshort}} (IAM). For more information about required IAM permissions to work with the service, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam). Connections from {{site.data.keyword.registrylong_notm}} to IAM do not use private connections. |
| {{site.data.keyword.cloudant_short_notm}} for {{site.data.keyword.cloud_notm}} | Cloudant is a managed, distributed database. {{site.data.keyword.registrylong_notm}} integrates with {{site.data.keyword.cloudant_short_notm}} to store metadata. Connections to {{site.data.keyword.cloudant_short_notm}} are private. |
| {{site.data.keyword.keymanagementservicefull_notm}} | {{site.data.keyword.keymanagementserviceshort}} is used to help secure the parts of {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.cos_full_notm}} that are used by {{site.data.keyword.registrylong_notm}}. |
| {{site.data.keyword.la_full_notm}} | {{site.data.keyword.registrylong_notm}} generates platform services logs, which are displayed in your logging instances. The logs are sent to {{site.data.keyword.la_full_notm}} by using private connections. For more information, see [Analyzing logs for Container Registry](/docs/Registry?topic=Registry-registry_logs). |
{: caption="Table 1. {{site.data.keyword.registryshort_notm}} dependencies to other {{site.data.keyword.cloud_notm}} services" caption-side="bottom"}
{: summary="The first column is the service. The second column is a description of the service."}

## Dependencies to third-party services
{: #registry_architecture_dependencies_third_party}

Review the list of third-party services that {{site.data.keyword.registrylong_notm}} connects to over the public network.
{: shortdesc}

| Service name | Description |
|------------|-------------------------------------|
| Akamai | Akamai is used as a provider for DNS, global load-balancing, and web firewall capabilities in {{site.data.keyword.registrylong_notm}}. |
{: caption="Table 2. {{site.data.keyword.registryshort_notm}} dependencies to third-party services" caption-side="bottom"}
{: summary="The first column is the service. The second column is a description of the service."}


