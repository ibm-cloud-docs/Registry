---

copyright:
  years: 2018, 2022
lastupdated: "2022-03-22"

keywords: load balancing, back ups, HA for IBM Cloud Container Registry, DR for IBM Cloud Container Registry, high availability for IBM Cloud Container Registry, disaster recovery for IBM Cloud Container Registry, failover for IBM Cloud Container Registry, high availability, replicate the data, replicate the service, availability,

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability and disaster recovery for {{site.data.keyword.registryshort_notm}}
{: #ha-dr}

The {{site.data.keyword.registrylong}} service is a highly available, regional, service.
{: shortdesc}

- In each supported region, traffic is load balanced across registry infrastructure in multiple [availability zones](x7018171){: term}, with no single point of failure.
- Data that is stored in {{site.data.keyword.registrylong_notm}} is replicated and it is also backed up regularly.
- If you're worried about the availability of your images if an entire region is unavailable, you can choose to push your images to multiple registries.

    You might also choose to push your images to multiple registries in case you accidentally delete or overwrite your images.

    For more information about regions, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

For more information about service availability, see [Service Level Agreements](/docs/overview?topic=overview-slas).

## Frequently asked questions about high availability and disaster recovery
{: #ha-dr_faq}

Review the following FAQs about [high availability](x2284708){: term} and [disaster recovery](x2113280){: term}.

### Does the service replicate the data?
{: #ha-dr_replicate_data}

All customer data in {{site.data.keyword.registrylong_notm}} is replicated and backed up. Backups include image data, service settings, and policy settings, but not vulnerability results, which can be reconstructed. All data, including vulnerability results, is replicated within each region so that the loss of a single availability zone is tolerated transparently. Regular point-in-time backups are used by {{site.data.keyword.IBM_notm}} to restore the content if the data is corrupted. Extra backups are created in other regions with compatible privacy policies that are used by {{site.data.keyword.IBM_notm}} to restore the service in a disaster situation.

The following table shows the backup locations.

| Environment | Active location | Backup location |
|-------------|-----------------|-----------------|
| `ap-north` | `jp-tok` | `au-syd` |
| `ap-south` | `au-syd` | `jp-tok` |
| `br-sao` | `br-sao` | `us-south` |
| `ca-tor` | `ca-tor` | `us-east` (service and policy settings)  \n  \n `ca-mon` (images) |
| `eu-de` | `eu-de` | `eu-gb` |
| `eu-gb` | `eu-gb` | `eu-de` |
| `global` | `us-east` | `us-south` |
| `jp-osa` | `jp-osa` | `jp-tok` |
| `us-south` | `us-south` | `us-east` |
{: caption="Table 1. Backup locations" caption-side="bottom"}

### Are users required to replicate the data?
{: #ha-dr_client}

You're not expected to replicate your images. However, you can create a service instance in another {{site.data.keyword.registrylong_notm}} region. You can also choose from a range of tools, including pushing to multiple locations from your development pipeline, and the use of replication tools, such as [`skopeo copy`](https://github.com/containers/skopeo/blob/main/docs/skopeo-copy.1.md){: external}. {{site.data.keyword.IBM_notm}} doesn't replicate service instances.

### What data is backed-up or replicated?
{: #ha-dr_backup}

The image data, service settings, and policy settings are backed up by {{site.data.keyword.IBM_notm}}.

### Does {{site.data.keyword.cloud_notm}} replicate the service?
{: #ha-dr_service}

{{site.data.keyword.IBM_notm}} doesn't make replicas of your data available in any region other than the region where you stored it. High availability is achieved by running the service in three data centers in each region.

### Are users required to replicate the service?
{: #ha-dr_service_replicate}

You're not required to replicate your data into another region, but you can do it yourself by using tools such as [`skopeo copy`](https://github.com/containers/skopeo/blob/main/docs/skopeo-copy.1.md){: external}.


