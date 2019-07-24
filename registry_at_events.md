---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-24"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker events, Activity Tracker events, events, track,

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

# {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud}}.
{:shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}.
For more information, see [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

The following table lists the API methods that generate an event when they are called:

<table>
  <caption>Table 1. Actions that generate events</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Create a Vulnerability Advisor exemption.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Delete a Vulnerability Advisor exemption.</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>Build a Docker image in {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>Delete an image from {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>Display details about an image.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>List the images in your {{site.data.keyword.IBM_notm}} account.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>Pull an image from {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>Push an image to {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>Delete one or more specified images from {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Add a new tag that refers to a pre-existing {{site.data.keyword.registrylong_notm}} image.</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>Add a namespace to {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>Delete a namespace from {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>List the namespaces in your {{site.data.keyword.IBM_notm}} account.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>Display the current quotas for traffic and storage, and the usage information against those quotas.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>Modify the quotas.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>Delete a registry token.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>Retrieve information about a registry token.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>List the registry tokens in your {{site.data.keyword.IBM_notm}} account.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>Delete multiple registry tokens.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Display information about the current pricing plan.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Upgrade to the standard plan.</td>
  </tr>
 </table>

## Where to look for the events
{: #ui}



{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.cloud_notm}} region where the events are generated, except for `ap-north`. Events for `ap-north` show in `ap-south`.

The [region](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor event is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} where the resource (for example, the image or namespace) is available.
