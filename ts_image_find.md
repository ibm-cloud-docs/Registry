---

copyright:
  years: 2023, 2025
lastupdated: "2025-04-01"

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
- **Scenario B.** Check your instance of {{site.data.keyword.logs_full_notm}} that is configured to receive events from {{site.data.keyword.atracker_full_notm}} to see whether the image or namespace was deleted. For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).
