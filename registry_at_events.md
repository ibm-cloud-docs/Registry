---

copyright:
  years: 2018, 2020
lastupdated: "2020-01-21"

keywords: activity tracker, events, track, tracking events, find events, look for events,

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

# Activity Tracker events
{: #at_events}

Track how users and applications interact with the {{site.data.keyword.registrylong}} service in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

The {{site.data.keyword.at_full_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}. For more information, see [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started).

The following table lists the API methods that generate an event when they are called:

| Action | Description | Status |
|-----------------|-----------------|
| `container-registry.exemption.create` | Create a Vulnerability Advisor exemption. | |
| `container-registry.exemption.delete` | Delete a Vulnerability Advisor exemption. | |
| `container-registry.image.build` | Build a Docker image in {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.image.bulkdelete` | Delete multiple images from {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.image.delete` | Delete an image from {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.image.inspect` | Display details about an image. | |
| `container-registry.image.list` | List the images in your {{site.data.keyword.IBM_notm}} account. | |
| `container-registry.image.pull` | Pull an image from {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.image.push` | Push an image to {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.image.tag` | Add a tag that refers to a pre-existing {{site.data.keyword.registrylong_notm}} image. | |
| `container-registry.image.untag` | Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.manifest.inspect` | View the contents of the manifest for an image. | |
| `container-registry.namespace.create` | Add a namespace to {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.namespace.delete` | Delete a namespace from {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.namespace.list` | List the namespaces in your {{site.data.keyword.IBM_notm}} account. | |
| `container-registry.plan.get` | Display information about the current pricing plan. | |
| `container-registry.plan.set` | Upgrade to the standard plan. | |
| `container-registry.quota.get` | Display the current quotas for traffic and storage, and the usage information against those quotas. | |
| `container-registry.quota.set` | Modify the quotas. | |
| `container-registry.registrytoken.delete` | Delete a registry token. | Deprecated |
| `container-registry.registrytoken.get` | Retrieve information about a registry token. | Deprecated |
| `container-registry.registrytoken.list` | List the registry tokens in your {{site.data.keyword.IBM_notm}} account. | Deprecated |
| `container-registry.registrytokens.delete` | Delete multiple registry tokens. | Deprecated |
| `container-registry.retention.analyze` | List the images that are deleted if you apply a given retention policy. | |
| `container-registry.retention.list` | List the image retention policies for your account. | |
| `container-registry.retention.set` | Set a policy to retain images in a namespace in {{site.data.keyword.registrylong_notm}} by applying specified criteria. | |
| `container-registry.trash.list` | Display all the images in the trash in your {{site.data.keyword.cloud_notm}} account. | |
| `container-registry.trash.restore` | Restore a deleted image from the trash. | |
{: caption="Table 1. Actions that generate events" caption-side="top"}

Using {{site.data.keyword.registrylong_notm}} tokens is deprecated.
{: deprecated}

## Where to look for the events
{: #ui}

### {{site.data.keyword.at_full_notm}} events
{: #ui_atlogdna}

The [region](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor event is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} that generated the event, except for `ap-south`. Events for `ap-south` show in `Tokyo (jp-tok)`.

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
