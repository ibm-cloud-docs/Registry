---

copyright:
  years: 2018
lastupdated: "2018-07-25"

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
For example, when you import a certificate, an {{site.data.keyword.cloudaccesstrailshort}} event is generated.

The following table lists the API methods that generate an event when they are called:

<table>
  <caption>Actions that generate events</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>container-registry.exemption.create</td>
	  <td>Create a Vulnerability Advisor exemption.</td>
  </tr>
  <tr>
    <td>container-registry.exemption.delete</td>
	  <td>Delete a Vulnerability Advisor exemption.</td>
  </tr>
 </table>



## Where to look for the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.

{{site.data.keyword.cloudaccesstrailshort}} events are automatically forwarded to the {{site.data.keyword.cloudaccesstrailshort}} service in the same region where the {{site.data.keyword.registrylong_notm}} service is provisioned.


## Additional information
{: #info}

The field *requestData_str* includes the human readable name of the certificate.



