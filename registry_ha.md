---

copyright:
  years: 2018, 2025
lastupdated: "2025-08-06"

keywords: load balancing, back ups, HA for IBM Cloud Container Registry, DR for IBM Cloud Container Registry, high availability for IBM Cloud Container Registry, disaster recovery for IBM Cloud Container Registry, failover for IBM Cloud Container Registry, high availability, replicate the data, replicate the service, availability, responsibilities, location, service, region

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# High availability for {{site.data.keyword.registryshort_notm}}
{: #ha-dr}

The {{site.data.keyword.registrylong}} service is a highly available, regional, service.
{: shortdesc}

[High availability](#x2284708){: term} (HA) is a core discipline in an IT infrastructure that keeps your apps up and running, even after a partial or full site failure. The main purpose of high availability is to eliminate potential points of failures in an IT infrastructure.

- In each supported region, traffic is load balanced across registry infrastructure in multiple [availability zones](#x7018171){: term}, with no single point of failure.
- Data that is stored in {{site.data.keyword.registrylong_notm}} is replicated over the availability zones and it is also backed up in another region regularly.
- If you're worried about the availability of your images if an entire region is unavailable, you can choose to push your images to multiple registry regions.

    You might also choose to push your images to multiple registry regions in case you accidentally delete or overwrite your images.

    For more information about regions, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

For more information about service availability, see [Service Level Agreements](/docs/overview?topic=overview-slas).

## Ownership of responsibilities
{: #ha-responsibilities}

To find out more about responsibility ownership for using {{site.data.keyword.cloud_notm}} products between {{site.data.keyword.IBM_notm}} and the customer, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).

For more information about your responsibilities when you are using {{site.data.keyword.registrylong_notm}}, see [Shared responsibilities for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_responsibilities).

## What level of availability do I need?
{: #ha-level}

You can achieve high availability on different levels in your IT infrastructure and within different components of your cluster. The level of availability that is appropriate for you depends on several factors, such as your business requirements, the service level agreements (SLAs) that you have with your customers, and the resources that you want to expend.

## What level of availability does {{site.data.keyword.cloud_notm}} offer?
{: #ha-service}

The level of availability that you set up for your cluster impacts your coverage under the {{site.data.keyword.cloud_notm}} high availability service level agreement terms.

Service level objectives (SLO) describe the design points that the {{site.data.keyword.cloud_notm}} services are engineered to meet. {{site.data.keyword.registrylong_notm}} is designed to achieve the following availability target.

| Availability target | Target Value |
|---------------------|--------------|
| Availability % | 99.999 |
{: caption="SLO for {{site.data.keyword.registryshort}}" caption-side="bottom"}
{: #table_registry_ha_slo}

The SLO is not a warranty and {{site.data.keyword.IBM_notm}} does not issue credits for failure to meet an objective. Refer to the SLAs for commitments and credits that are issued for failure to meet any committed SLAs. For a summary of all service level objectives, see [{{site.data.keyword.cloud_notm}} service level objectives](/docs/resiliency?topic=resiliency-slo).

## Locations for service availability
{: #ha-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

## FAQ about high availability
{: #ha-dr_faq}

Review the following frequently asked questions about high availability.

### Does {{site.data.keyword.cloud_notm}} replicate the service?
{: #ha-dr_service}

{{site.data.keyword.IBM_notm}} doesn't make replicas of your data available in any region other than the region where you stored it. High availability is achieved by running the service in three data centers in each region.

### Are users required to replicate the service?
{: #ha-dr_service_replicate}

You're not required to replicate your data into another region, but you can do it yourself by using tools such as [`skopeo copy`](https://github.com/containers/skopeo/blob/main/docs/skopeo-copy.1.md){: external}.
