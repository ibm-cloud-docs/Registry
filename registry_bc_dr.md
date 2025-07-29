---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-29"

keywords: DR for IBM Cloud Container Registry, high availability for IBM Cloud Container Registry, disaster recovery for IBM Cloud Container Registry, failover for IBM Cloud Container Registry, BC for IBM Cloud Container Registry, DR for IBM Cloud Container Registry, business continuity for IBM Cloud Container Registry, disaster recovery for IBM Cloud Container Registry, disaster recovery, responsibilities, locations, data

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Business continuity and disaster recovery for {{site.data.keyword.registryshort_notm}}
{: #bc-dr}

Find out about the business continuity and disaster recovery strategy for {{site.data.keyword.registrylong}}.
{: shortdesc}

[Disaster recovery](#x2113280){: term} involves a set of policies, tools, and procedures for returning a system, an application, or an entire data center to full operation after a catastrophic interruption. It includes procedures for copying and storing an installed system's essential data in a secure location, and for recovering that data to restore normalcy of operation.

## Your responsibilities when you're using {{site.data.keyword.registryshort_notm}}
{: #bc-dr-responsibilities}

For more information about your responsibilities when you're using {{site.data.keyword.registrylong_notm}}, see [Shared responsibilities for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_responsibilities).

## Disaster recovery strategy
{: #bc-dr-strategy}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You're responsible for your data backup and associated recovery of your content.

{{site.data.keyword.registryshort}} provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for {{site.data.keyword.registryshort}}.

| Disaster recovery objective | Target Value |
|-----------------------------|--------------|
| Recovery point objective (RPO) | 48 hours |
| Recovery time objective (RTO) | 24 hours |
{: caption="RPO and RTO for {{site.data.keyword.registryshort}}" caption-side="bottom"}
{: #table_registry_bc_dr_rpo_rto}

## Locations for service availability
{: #bc-dr-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

## FAQ about disaster recovery
{: #bc-dr_faq}

Review the following frequently asked questions about disaster recovery.

### Does the service replicate the data?
{: #bc-dr_replicate_data}

All customer data in {{site.data.keyword.registrylong_notm}} is replicated and backed up. Backups include service and policy settings and image data, but not vulnerability results, which can be reconstructed. All data, including vulnerability results, is replicated within each region so that the loss of a single availability zone is tolerated transparently. Regular point-in-time backups are used by {{site.data.keyword.IBM_notm}} to restore the content if the data is corrupted. More backups are created in other regions with compatible privacy policies that are used by {{site.data.keyword.IBM_notm}} to restore the service in a disaster situation.

The following table shows the backup locations.

| Environment | Environment that was formerly known as | Active location | Backup location |
|-------------|---------------------------------------|-----------------|-----------------|
| `au-syd` | `ap-south` | `au-syd` | `jp-tok` |
| `br-sao` | Not applicable | `br-sao` | `us-south` |
| `ca-mon` | Not applicable | `ca-mon` | `ca-tor` |
| `ca-tor` | Not applicable | `ca-tor` | `us-east` (service and policy settings)  \n  \n `ca-mon` (images) |
| `eu-de` | `eu-central` | `eu-de` | `eu-gb` |
| `eu-es` | Not applicable | `eu-es` | `eu-de` |
| `eu-gb` | `uk-south` | `eu-gb` | `eu-de` |
| `global` | Not applicable | `us-east` | `us-south` |
| `jp-osa` | Not applicable | `jp-osa` | `jp-tok` |
| `jp-tok` | `ap-north` | `jp-tok` | `au-syd` |
| `us-south` | Not applicable | `us-south` | `us-east` |
{: caption="Backup locations" caption-side="bottom"}
{: #table_registry_bc_dr_backup_locations}

### What data is backed up or replicated?
{: #bc-dr_backup}

The image data, service settings, and policy settings are backed up by {{site.data.keyword.IBM_notm}}.

### Are users required to replicate the data?
{: #bc-dr_client}

You are not expected to replicate your images. However, you can create a service instance in another {{site.data.keyword.registrylong_notm}} region. You can also choose from a range of tools, including pushing to multiple locations from your development pipeline, and the use of replication tools, such as [`skopeo copy`](https://github.com/containers/skopeo/blob/main/docs/skopeo-copy.1.md){: external}. {{site.data.keyword.IBM_notm}} doesn't replicate service instances.
