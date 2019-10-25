---

copyright:
  years: 2018, 2019
lastupdated: "2019-10-18"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker with LogDNA events, Activity Tracker events, events, track,

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

# Activity Tracker events
{: #at_events}

Track how users and applications interact with the {{site.data.keyword.registrylong}} service in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

The {{site.data.keyword.at_full_notm}} service or for existing users only, the {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}.
For more information, see [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started) or for existing users, [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

The following table lists the API methods that generate an event when they are called:

| Action | Description |
|-----------------|-----------------|
| `container-registry.exemption.create` | Create a Vulnerability Advisor exemption. |
| `container-registry.exemption.delete` | Delete a Vulnerability Advisor exemption. |
| `container-registry.image.build` | Build a Docker image in {{site.data.keyword.registrylong_notm}}. |
| `container-registry.image.bulkdelete` | Delete multiple images from {{site.data.keyword.registrylong_notm}}. |
| `container-registry.image.delete` | Delete an image from {{site.data.keyword.registrylong_notm}}. |
| `container-registry.image.inspect` | Display details about an image. |
| `container-registry.image.list` | List the images in your {{site.data.keyword.IBM_notm}} account. |
| `container-registry.image.pull` | Pull an image from {{site.data.keyword.registrylong_notm}}. |
| `container-registry.image.push` | Push an image to {{site.data.keyword.registrylong_notm}}. |
| `container-registry.image.rm` | Delete one or more specified images from {{site.data.keyword.registrylong_notm}}. |
| `container-registry.image.tag` | Add a tag that refers to a pre-existing {{site.data.keyword.registrylong_notm}} image. |
| `container-registry.image.untag` | Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}. |
| `container-registry.manifest.inspect` | View the contents of the manifest for an image. |
| `container-registry.namespace.create` | Add a namespace to {{site.data.keyword.registrylong_notm}}. |
| `container-registry.namespace.delete` | Delete a namespace from {{site.data.keyword.registrylong_notm}}. |
| `container-registry.namespace.list` | List the namespaces in your {{site.data.keyword.IBM_notm}} account. |
| `container-registry.plan.get` | Display information about the current pricing plan. |
| `container-registry.plan.set` | Upgrade to the standard plan. |
| `container-registry.quota.get` | Display the current quotas for traffic and storage, and the usage information against those quotas. |
| `container-registry.quota.set` | Modify the quotas. |
| `container-registry.registrytoken.delete` | Delete a registry token. |
| `container-registry.registrytoken.get` | Retrieve information about a registry token. |
| `container-registry.registrytoken.list` | List the registry tokens in your {{site.data.keyword.IBM_notm}} account. |
| `container-registry.registrytokens.delete` | Delete multiple registry tokens. |
| `container-registry.retention.analyze` | List the images that are deleted if you apply a given retention policy. |
| `container-registry.retention.list` | List the image retention policies for your account. |
| `container-registry.retention.set` | Set a policy to retain images in a namespace in {{site.data.keyword.registrylong_notm}} by applying specified criteria. |
| `container-registry.trash.list` | Display all the images in the trash in your {{site.data.keyword.cloud_notm}} account. |
| `container-registry.trash.restore` | Restore a deleted image from the trash. |
{: caption="Table 1. Actions that generate events" caption-side="top"}

## Where to look for the events
{: #ui}

### {{site.data.keyword.at_full_notm}} events
{: #ui_atlogdna}

{{site.data.keyword.at_full_notm}} events are available in the {{site.data.keyword.at_full_notm}} **account domain** that is available in the {{site.data.keyword.cloud_notm}} region where the events are generated, except for `ap-south`. Events for `ap-south` show in `Tokyo (jp-tok)`.

The [region](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor event is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} where the resource is available. Images and namespaces are examples of resources.

| Region for your account's registry | Domain name of your registry | Location of {{site.data.keyword.at_full_notm}} events |
|-----------------|-----------------|-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="Table 2. Location of {{site.data.keyword.at_full_notm}} events" caption-side="top"}

| Registry | Global registry | Location of {{site.data.keyword.at_full_notm}} events |
|-----------------|-----------------|-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 3. Location of global registry {{site.data.keyword.at_full_notm}} events" caption-side="top"}

### {{site.data.keyword.cloudaccesstraillong_notm}} events
{: #ui_at}

{{site.data.keyword.cloudaccesstraillong_notm}} events, for existing users only, are available in the {{site.data.keyword.cloudaccesstraillong_notm}} **account domain** that is available in the {{site.data.keyword.cloud_notm}} region where the events are generated, except for `ap-north`. Events for `ap-north` show in `ap-south`.

{{site.data.keyword.cloudaccesstrailfull_notm}} is deprecated. As of 9 May 2019, you cannot provision new {{site.data.keyword.cloudaccesstrailshort}} instances. Existing premium plan instances are supported until 30 September 2019. To continue monitoring the activity of your {{site.data.keyword.cloud_notm}} account, provision an instance of the [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).
{: deprecated}

The [region](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor event is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} where the resource is available. Images and namespaces are examples of resources.
