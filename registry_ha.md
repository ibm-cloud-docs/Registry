---

copyright:
  years: 2018
lastupdated: "2018-09-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# High availability and disaster recovery
{: #ha-dr}

The {{site.data.keyword.registrylong}} service is a highly available, regional, service.
{:shortdesc}

* In each supported region, traffic is load balanced across registry infrastructure in multiple availability zones, with no single point of failure.

* Data stored in {{site.data.keyword.registrylong_notm}} is backed up regularly, providing additional resilience.

* If you are worried about the availability of your images in the case of an entire region being unavailable, you can choose to push your images to multiple regional registries. 
  
  You might also choose to push your images to multiple registries in case you accidentally delete or overwrite your images.

  For more information about regions, see [Regions](/docs/services/Registry/registry_overview.html#registry_regions).
