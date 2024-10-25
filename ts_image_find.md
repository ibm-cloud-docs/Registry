---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-25"

keywords: registry, namespace, find, image, region

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I find my image or my namespace in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-image-find}
{: troubleshoot}
{: support}

Your image or your namespace is missing in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to find your image or your namespace, you can't find it.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- **Scenario A.** You're looking in the wrong region. Namespaces are region specific and you might be targeting the wrong region.
- **Scenario B.** The image or namespace was deleted.

You can fix this problem in the following ways:
{: tsResolve}

- **Scenario A.** Check that you're using the correct region. To change the region, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).
- **Scenario B.** Check your instance of {{site.data.keyword.at_full_notm}} or {{site.data.keyword.logs_full_notm}} to see whether the image or namespace was deleted. For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For more information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: deprecated}
