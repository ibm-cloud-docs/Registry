---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-28"

keywords: track, tracking events, find events, look for events, activity tracker for IBM Cloud Container Registry, LogDNA for IBM Cloud Container Registry, IBM Cloud Container Registry events, IBM Cloud Container Registry security, audit logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry events, IBM Cloud Container Registry events,

subcollection: Registry

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

# Auditing the events for {{site.data.keyword.registryshort_notm}}
{: #at_events}

Use {{site.data.keyword.at_full_notm}} to track how users and applications interact with the {{site.data.keyword.registrylong}} service in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

The {{site.data.keyword.at_full_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}. For more information, see [{{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started).

The following table lists the API methods that generate an event when they are called.

| Action | Description | Status | Data Event |
|-----------------|-----------------|-----------------|-----------------|
| `container-registry.auth.get` | Check whether the use of public connections is prevented for image pushes or pulls in your account. | | |
| `container-registry.auth.set` | Prevent or allow image pulls or pushes over public network connections for your account. | | |
| `container-registry.exemption.create` | Create a Vulnerability Advisor exemption. | | |
| `container-registry.exemption.delete` | Delete a Vulnerability Advisor exemption. | | |
| `container-registry.image.build` | Build a Docker image in {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.bulkdelete` | Delete multiple images from {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.delete` | Delete an image from {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.inspect` | Display details about an image. | | |
| `container-registry.image.list` | List the images in your {{site.data.keyword.IBM_notm}} account. | | |
| `container-registry.image.pull` | Pull an image from {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.push` | Push an image to {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.tag` | Add a tag that refers to a pre-existing {{site.data.keyword.registrylong_notm}} image. | | |
| `container-registry.image.untag` | Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}. | | |
| `container-registry.manifest.inspect` | View the contents of the manifest for an image. | | |
| `container-registry.namespace.create` | Add a namespace to {{site.data.keyword.registrylong_notm}}. | | |
| `container-registry.namespace.delete` | Delete a namespace from {{site.data.keyword.registrylong_notm}}. | | |
| `container-registry.namespace.list` | List the {{site.data.keyword.registrylong_notm}} namespaces in your {{site.data.keyword.IBM_notm}} account. | | |
| `container-registry.plan.get` | Display information about the current pricing plan. | | |
| `container-registry.plan.set` | Upgrade to the standard plan. | | |
| `container-registry.quota.get` | Display the current quotas for traffic and storage, and the usage information against those quotas. | | |
| `container-registry.quota.set` | Modify the quotas. | | |
| `container-registry.registrytoken.delete` | Delete a registry token. | Deprecated | |
| `container-registry.registrytoken.get` | Retrieve information about a registry token. | Deprecated | |
| `container-registry.registrytoken.list` | List the registry tokens in your {{site.data.keyword.IBM_notm}} account. | Deprecated | |
| `container-registry.registrytokens.delete` | Delete multiple registry tokens. | Deprecated | |
| `container-registry.retention.analyze` | List the images that are deleted if you apply a given retention policy. | | |
| `container-registry.retention.list` | List the image retention policies for your account. | | |
| `container-registry.retention.set` | Set a policy to retain images in a namespace in {{site.data.keyword.registrylong_notm}} by applying specified criteria. | | |
| `container-registry.trash.list` | Display all the images in the trash in your {{site.data.keyword.cloud_notm}} account. | | |
| `container-registry.trash.restore` | Restore a deleted image from the trash. | | |
{: caption="Table 1. Actions that generate events" caption-side="top"}

Using {{site.data.keyword.registrylong_notm}} tokens is deprecated. From 12 August 2020, UAA and registry tokens will no longer be accepted for authentication. For more information, see [Announcing End of IBM Cloud Container Registry Support for Registry and UAA Tokens](https://www.ibm.com/cloud/blog/announcements/announcing-end-of-ibm-cloud-container-registry-support-for-registry-and-uaa-tokens){: external}.
{: deprecated}

## Where to look for the events
{: #ui}

### {{site.data.keyword.at_full_notm}} events
{: #ui_atlogdna}

The [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor event is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} that generated the event, except for `ap-south`. Events for `ap-south` show in `Tokyo (jp-tok)`.

The following table shows the location of {{site.data.keyword.at_full_notm}} events.

| Region for your account's registry | Domain name of your registry | Location of {{site.data.keyword.at_full_notm}} events |
|-----------------|-----------------|-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="Table 2. Location of {{site.data.keyword.at_full_notm}} events" caption-side="top"}

The following table shows the location of global registry {{site.data.keyword.at_full_notm}} events.

| Registry | Global registry | Location of {{site.data.keyword.at_full_notm}} events |
|-----------------|-----------------|-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 3. Location of global registry {{site.data.keyword.at_full_notm}} events" caption-side="top"}
