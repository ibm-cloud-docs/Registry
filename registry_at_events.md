---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.registrylong}} service in {{site.data.keyword.Bluemix}}.
{:shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.Bluemix_notm}}.
For more information, see [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).

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
 </table>

## Where to look for the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.

The [region](/docs/services/Registry/registry_overview.html#registry_regions) in which a Vulnerability Advisor event is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} where the resource (for example, the image or namespace) is available.
