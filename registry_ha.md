---

copyright:
  years: 2018, 2020
lastupdated: "2020-04-14"

keywords: high availability, load balancing, back ups, disaster recovery,


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
{:term: .term}
{:external: target="_blank" .external}

# High availability and disaster recovery
{: #ha-dr}

The {{site.data.keyword.registrylong}} service is a highly available, regional, service.
{:shortdesc}

* In each supported region, traffic is load balanced across registry infrastructure in multiple availability zones, with no single point of failure.

* Data that is stored in {{site.data.keyword.registrylong_notm}} is replicated and it is also backed up regularly.

* If you're worried about the availability of your images if an entire region is unavailable, you can choose to push your images to multiple regional registries.

  You might also choose to push your images to multiple registries in case you accidentally delete or overwrite your images.

  For more information about regions, see [Regions](/docs/Registry?topic=registry-registry_overview#registry_regions).

For more information about service availability, see [Service Level Agreements](/docs/overview?topic=overview-slas).

## Frequently asked questions about high availability and disaster recovery
{: #ha-dr_faq}

### Does the service replicate the data?
{: #ha-dr_replicate_data}

All customer data in {{site.data.keyword.registrylong_notm}} is replicated and backed up. Backups include service and policy settings and image data, but not vulnerability results, which can be reconstructed. All data, including vulnerability results, is replicated within each region so that the loss of a single availability zone is tolerated transparently. Additionally, point-in-time backups are used by {{site.data.keyword.IBM_notm}} to restore the content if the data is corrupted, and out-of-region backups are used by {{site.data.keyword.IBM_notm}} to restore the service in a disaster recovery situation.

### Do users have to replicate the data?
{: #ha-dr_client}

You're not expected to replicate your images. However, if you want to do so, you can create a service instance in another {{site.data.keyword.registrylong_notm}} region and choose from a range of tools, including pushing to multiple locations from your development pipeline, and the use of replication tools, such as [`skopeo copy`](https://github.com/containers/skopeo/blob/master/docs/skopeo-copy.1.md){: external}. {{site.data.keyword.IBM_notm}} doesn't replicate service instances.

### What data is backed-up or replicated?
{: #ha-dr_backup}

The image data and service and policy settings are backed up by {{site.data.keyword.IBM_notm}}.

### Does {{site.data.keyword.cloud_notm}} replicate the service?
{: #ha-dr_service}

{{site.data.keyword.IBM_notm}} doesn't make replicas of your data available in any region other than the one where you stored it.

### Do users have to replicate the service?
{: #ha-dr_service_replicate}

You're not required to replicate your data into another region, but you do have the option to do it yourself by using tools such as [`skopeo copy`](https://github.com/containers/skopeo/blob/master/docs/skopeo-copy.1.md){: external}.
