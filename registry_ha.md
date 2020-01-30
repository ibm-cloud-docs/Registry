---

copyright:
  years: 2018, 2020
lastupdated: "2020-01-30"

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

* Data that is stored in {{site.data.keyword.registrylong_notm}} is backed up regularly, providing extra resilience.

* If you are worried about the availability of your images if an entire region is unavailable, you can choose to push your images to multiple regional registries.
  
  You might also choose to push your images to multiple registries in case you accidentally delete or overwrite your images.

  For more information about regions, see [Regions](/docs/Registry?topic=registry-registry_overview#registry_regions).
