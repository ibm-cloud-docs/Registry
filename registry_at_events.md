---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-19"

keywords: Track, tracking events, find events, look for events, activity tracker for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry events, IBM Cloud Container Registry security, audit logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry events, IBM Cloud Container Registry events,

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

Use {{site.data.keyword.at_full}} to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

The {{site.data.keyword.at_full_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}. For more information, see [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

## API methods
{: #at_events_api_methods}

The following table lists the API methods that generate an event when they are called.

| Action | Description | Status | Data Event |
|-----------------|-----------------|-----------------|-----------------|
| `container-registry.account-vulnerability-report.list` | View the Vulnerability Advisor reports for images in your {{site.data.keyword.registrylong_notm}} account.<br/><br/>For more information about request data, see [Request data for `container-registry.account-vulnerability-report.list`](#at_events_analyze_report_list). | | |
| `container-registry.account-vulnerability-status.list` | View Vulnerability Advisor security status for images in your {{site.data.keyword.registrylong_notm}} account.<br/><br/>For more information about request data, see [Request data for `container-registry.account-vulnerability-status.list`](#at_events_analyze_status_list). | | |
| `container-registry.auth.get` | Check whether the use of public connections is prevented for image pushes or pulls in your account. | | |
| `container-registry.auth.set` | Prevent or allow image pulls or pushes over public network connections for your account. | | |
| `container-registry.exemption.create` | Create a Vulnerability Advisor exemption. | | |
| `container-registry.exemption.delete` | Delete a Vulnerability Advisor exemption. | | |
| `container-registry.image.build` | Build a Docker image in {{site.data.keyword.registrylong_notm}}. | Deprecated | True |
| `container-registry.image.bulkdelete` | Delete multiple images from {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.delete` | Delete an image from {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.inspect` | Display details about an image. | | |
| `container-registry.image.list` | List the images in your {{site.data.keyword.IBM_notm}} account. | | |
| `container-registry.image.pull` | Pull an image from {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.push` | Push an image to {{site.data.keyword.registrylong_notm}}. | | True |
| `container-registry.image.tag` | Add a tag that refers to a pre-existing {{site.data.keyword.registrylong_notm}} image. | | |
| `container-registry.image.untag` | Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}. | | |
| `container-registry.image-vulnerability-report.read` | View the Vulnerability Advisor report for an image in {{site.data.keyword.registrylong_notm}}.<br/><br/>For more information about request and response data, see [Request and response data for `container-registry.image-vulnerability-report.read`](#at_events_analyze_report_read). | | |
| `container-registry.image-vulnerability-status.read` | View the Vulnerability Advisor security status for an image in {{site.data.keyword.registrylong_notm}}.<br/><br/>For more information about request and response data, see [Request and response data for `container-registry.image-vulnerability-status.read`](#at_events_analyze_status_read). | | |
| `container-registry.manifest.inspect` | View the contents of the manifest for an image. | | |
| `container-registry.namespace.create` | Create a namespace in {{site.data.keyword.registrylong_notm}}.<br/><br/>Assign an {{site.data.keyword.registrylong_notm}} namespace to a resource group. | | |
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
| `container-registry.retention.analyze` | List the images that are deleted if you apply a specific retention policy. | | |
| `container-registry.retention.list` | List the image retention policies for your account. | | |
| `container-registry.retention.set` | Set a policy to retain images in a namespace in {{site.data.keyword.registrylong_notm}} by applying specified criteria. | | |
| `container-registry.settings.get` | Get registry service settings for the targeted account, such as whether platform metrics are enabled. | | |
| `container-registry.settings.set` | Update registry service settings for the targeted account, such as enabling platform metrics. | | |
| `container-registry.trash.list` | Display all the images in the trash in your {{site.data.keyword.cloud_notm}} account. | | |
| `container-registry.trash.restore` | Restore a deleted image from the trash. | | |
{: caption="Table 1. Actions that generate events" caption-side="top"}

Using {{site.data.keyword.registrylong_notm}} tokens is deprecated.
{: deprecated}

The [`ibmcloud cr build`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) command is deprecated from 6 October 2020. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead. For more information, see the [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecating-container-builds){: external} blog post.
{: deprecated}

## Where to look for the events
{: #ui}

### {{site.data.keyword.at_full_notm}} events
{: #ui_at}

The [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor event is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} that generated the event, except for `ap-south`. Events for `ap-south` show in `Tokyo (jp-tok)`.

The following table shows the location of {{site.data.keyword.at_full_notm}} events.

| Region for your account's registry | Domain name of your registry | Location of {{site.data.keyword.at_full_notm}} events |
|-----------------|-----------------|-----------------|
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ca-tor` | `ca.icr.io` | `Toronto (ca-tor)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `jp-osa` | `jp2.icr.io` | `Osaka (jp-osa)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
{: caption="Table 2. Location of {{site.data.keyword.at_full_notm}} events" caption-side="top"}

The following table shows the location of global registry {{site.data.keyword.at_full_notm}} events.

| Registry | Global registry | Location of {{site.data.keyword.at_full_notm}} events |
|-----------------|-----------------|-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 3. Location of global registry {{site.data.keyword.at_full_notm}} events" caption-side="top"}

For more information about {{site.data.keyword.cloud_notm}} services by location, see [Container services](/docs/activity-tracker?topic=activity-tracker-cloud_services_locations#cloud_services_locations_container).

## Analyzing Activity Tracker events
{: #at_events_analyze}

The following fields are populated as described, depending on how you populate the request:

- `target.name` shows the image name and, if you request an image name with a tag, a tag. If you request an image name by digest, the digest is shown instead of the tag because the digest might have many tags.

- `target.id` shows the image name by digest to represent a searchable unique ID for the image, unless the request is for an image with a tag and the request fails before the digest is discovered. To see all the events for this digest across all tags, you can search by `target.id`.

### Request data for `container-registry.account-vulnerability-report.list`
{: #at_events_analyze_report_list}

Get the vulnerability assessment for the list of registry images that belong to a specific account.
{: shortdesc}

The following table lists the fields that are available through the `requestData` field in events with the action `container-registry.account-vulnerability-report.list`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.repository` | String | The name of the repository that you want to see image vulnerability assessments for. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.includeIBM` | String | When set to `true`, the returned list contains {{site.data.keyword.IBM_notm}} public images and the account images. If not set, or set to `false`, the list contains only the account images. |
| `requestData.RequestParameters.includePrivate` | String | When set to `false`, the returned list does not contain the private account images. If not set, or set to `true`, the list contains the private account images. |
{: caption="Table 4. Custom event fields for {{site.data.keyword.registryshort_notm}} account vulnerability reports list" caption-side="top"}

For more information about the action `container-registry.account-vulnerability-report.list`, see [Get the vulnerability assessment for all images](https://{DomainName}/apidocs/container-registry/va#accountreportquerypath){: external} in the API documentation.

### Request data for `container-registry.account-vulnerability-status.list`
{: #at_events_analyze_status_list}

Get the vulnerability assessment status for the list of registry images that belong to a specific account.
{: shortdesc}

The following table lists the fields that are available through the `requestData` field in events with the action `container-registry.account-vulnerability-status.list`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.repository` | String | The name of the repository that you want to see image vulnerability assessments for. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.includeIBM` | String | When set to `true`, the returned list contains {{site.data.keyword.IBM_notm}} public images and the account images. If not set, or set to `false`, the list contains only the account images. |
| `requestData.RequestParameters.includePrivate` | String | When set to `false`, the returned list does not contain the private account images. If not set, or set to `true`, the list contains the private account images. |
{: caption="Table 5. Custom event fields for {{site.data.keyword.registryshort_notm}} account vulnerability status list" caption-side="top"}

For more information about the action `container-registry.account-vulnerability-status.list`, see [Get vulnerability assessment status for all images](https://{DomainName}/apidocs/container-registry/va#accountstatusquerypath){: external} in the API documentation.

### Request and response data for `container-registry.image-vulnerability-report.read`
{: #at_events_analyze_report_read}

Get the vulnerability assessment for a registry image.
{: shortdesc}

The following table lists the fields that are available through the `requestData` and `responseData` fields in events with the action `container-registry.image-vulnerability-report.read`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.name` | String | The name of the image. For example, `us.icr.io/namespace/repository:tag`.<br/><br/>**Constraints** Value must match regular expression `.*`. |
| `responseData.id` | String | The unique ID of the report. |
| `responseData.status` | String | **Overall vulnerability assessment status** `OK`, `WARN`, `FAIL`, `UNSUPPORTED`, `INCOMPLETE`, `UNSCANNED`. For more information about these status codes, see [Vulnerability report status codes](https://{DomainName}/apidocs/container-registry/va#vulnerability-report-status-codes){: external} in the API documentation. |
{: caption="Table 6. Custom event fields for {{site.data.keyword.registryshort_notm}} image vulnerability reports read" caption-side="top"}

For more information, see [Get vulnerability assessment status](https://{DomainName}/apidocs/container-registry/va#imagereportquerypath){: external} in the API documentation.

### Request and response data for `container-registry.image-vulnerability-status.read`
{: #at_events_analyze_status_read}

Get the overall vulnerability status for a registry image.
{: shortdesc}

The following table lists the fields that are available through the `requestData` and `responseData` fields in events with the action `container-registry.image-vulnerability-status.read`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.name` | String | The name of the image. For example, `us.icr.io/namespace/repository:tag`.<br/><br/>**Constraints** Value must match regular expression `.*`. |
| `responseData.status` | String | **Overall vulnerability assessment status** `OK`, `WARN`, `FAIL`, `UNSUPPORTED`, `INCOMPLETE`, `UNSCANNED`. For more information about these status codes, see [Vulnerability report status codes](https://{DomainName}/apidocs/container-registry/va#vulnerability-report-status-codes){: external} in the API documentation.
{: caption="Table 7. Custom event fields for {{site.data.keyword.registryshort_notm}} image vulnerability status read" caption-side="top"}

For more information, see [Get vulnerability status](https://{DomainName}/apidocs/container-registry/va#imagestatusquerypath){: external} in the API documentation.


