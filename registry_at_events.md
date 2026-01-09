---

copyright:
  years: 2018, 2026
lastupdated: "2026-01-09"

keywords: Track, tracking events, find events, activity tracking for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry events, IBM Cloud Container Registry security, audit logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry events, IBM Cloud Container Registry events, actions that generate events, request data, request and response data, events, api, actions, data event, request, custom event fields, response data, locations, service events

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.registryshort_notm}}
{: #at_events}


{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.registrylong}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, which is a platform service, to route audit events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where activity tracking events are generated
{: #at-locations}

You can track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service. The following tables list the locations where the automatic collection of {{site.data.keyword.registryshort_notm}} service events is enabled.

| Locations in Americas | Service events available |
|-----------------------|--------------------------|
| `Dallas (us-south)` | [Yes]{: tag-green} |
| `Sao Paulo (br-sao)` | [Yes]{: tag-green} |
| `Montreal (ca-mon)` | [Yes]{: tag-green} |
| `Toronto (ca-tor)` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service events in Americas locations" caption-side="bottom"}
{: #table_registry_at_event_collection_americas}

| Locations in Asia Pacific | Service events available |
|---------------------------|--------------------------|
| `Osaka (jp-osa)` | [Yes]{: tag-green} |
| `Sydney (au-syd)` | [Yes]{: tag-green} |
| `Tokyo (jp-tok)` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service events in Asia-Pacific locations" caption-side="bottom"}
{: #table_registry_at_event_collection_ap}

| Locations in Europe | Service events available |
|---------------------|--------------------------|
| `Frankfurt (eu-de)` | [Yes]{: tag-green} |
| `London (eu-gb)` | [Yes]{: tag-green} |
| `Madrid (eu-es)` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service events in Europe locations" caption-side="bottom"}
{: #table_registry_at_event_collection_europe}

| Location for Global | Service events available |
|---------------------|--------------------------|
| `Global` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service events for Global" caption-side="bottom"}
{: #table_registry_at_event_collection_global}

For more information about where to find {{site.data.keyword.registryshort_notm}} events, see [Viewing activity tracking events for {{site.data.keyword.registryshort}}](#at-viewing).

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}

{{site.data.keyword.registryshort}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following tables.

| Dallas (`us-south`) | Washington (`us-east`) | Montreal (`ca-mon`) | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|------------------------|---------------------|--------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} (`global`) | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`) | Sydney (`au-syd`) | Osaka (`jp-osa`) |
|------------------|-------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Asia-Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`) | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------|------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

## Viewing activity tracking events for {{site.data.keyword.registryshort}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Starting {{site.data.keyword.logs_full_notm}} from the Observability page
{: #at-launch-standalone}

For information about starting the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation](/docs/cloud-logs?topic=cloud-logs-instance-launch).

## Account management events
{: #at_actions_account}

Actions that generate account management events for authorization, plans, quotas, and settings.

| Action | Description |
|--------|-------------|
| `container-registry.auth.get` | Check whether the use of public connections is prevented for image pushes or pulls in your account. |
| `container-registry.auth.set` | Prevent or allow image pulls or pushes over public network connections for your account. |
| `container-registry.plan.get` | Display information about the current pricing plan. |
| `container-registry.plan.set` | Upgrade to the standard plan. |
| `container-registry.quota.get` | Display the current quotas for traffic and storage, and the usage information against those quotas. |
| `container-registry.quota.set` | Modify the quotas. Quota settings must be managed separately for your account in each registry instance. You can set quota limits for storage in your free or standard plan. |
| `container-registry.settings.get` | Get registry service settings for the targeted account, such as whether platform metrics are enabled. |
| `container-registry.settings.set` | Update registry service settings for the targeted account, such as enabling platform metrics. |
{: caption="Actions that generate account management events" caption-side="bottom"}
{: #table_account_mgmt_events}

## Events for images
{: #at_actions_images}

The following table shows actions that generate management and data events for images.

| Action | Description |
|--------|-------------|
| `container-registry.image.inspect` | Display details about an image. |
| `container-registry.image.list` | List the images in your {{site.data.keyword.IBM_notm}} account. |
| `container-registry.image.tag` | Add a tag that refers to a pre-existing {{site.data.keyword.registryshort}} image. |
| `container-registry.image.untag` | Remove a tag, or tags, from each specified image in {{site.data.keyword.registryshort}}. |
| `container-registry.manifest.inspect` | View the contents of the manifest for an image. |
| `container-registry.retention.analyze` | List the images that are deleted if you apply a specific retention policy. |
| `container-registry.retention.list` | List the image retention policies for your account. |
| `container-registry.retention.set` | Set a policy to retain images in a namespace in {{site.data.keyword.registryshort}} by applying specified criteria. |
| `container-registry.trash.list` | Display all the images in the trash in your {{site.data.keyword.cloud_notm}} account. |
| `container-registry.trash.restore` | Restore a deleted image from the trash. If the deleted image is signed, the signature is restored too. |
{: caption="Management events for images" caption-side="bottom"}
{: #images-table-1}
{: tab-title="Management events"}
{: tab-group="images"}
{: class="simple-tab-table"}
{: row-headers}

| Action | Description |
|--------|-------------|
| `container-registry.image.bulkdelete` | Delete multiple images from {{site.data.keyword.registryshort}}. If the image is signed, the signature is deleted as well. |
| `container-registry.image.delete` | Delete an image from {{site.data.keyword.registryshort}}. If the image is signed, the signature is deleted as well. |
| `container-registry.image.pull` | Pull an image from {{site.data.keyword.registryshort}}. |
| `container-registry.image.push` | Push an image to {{site.data.keyword.registryshort}}. |
| `container-registry.signature.delete` | Delete a signature from an image in {{site.data.keyword.registryshort}}. |
| `container-registry.signature.read` | Read a signature from an image in {{site.data.keyword.registryshort}}. |
| `container-registry.signature.write` | Write a signature to an image in {{site.data.keyword.registryshort}}. |
{: caption="Data events for images" caption-side="bottom"}
{: #images-table-2}
{: tab-title="Data events"}
{: tab-group="images"}
{: class="simple-tab-table"}
{: row-headers}

## Events for namespaces
{: #at_actions_namespaces}

The following table shows actions that generate management events for namespaces.

| Action | Description |
|--------|-------------|
| `container-registry.namespace.create` | Create a namespace in {{site.data.keyword.registryshort}}. |
| `container-registry.namespace.delete` | Delete a namespace from {{site.data.keyword.registryshort}}. |
| `container-registry.namespace.list` | List the {{site.data.keyword.registryshort}} namespaces in your {{site.data.keyword.IBM_notm}} account. |
{: caption="Management events for namespaces" caption-side="bottom"}
{: #table_events_namespaces}

## Events for vulnerabilities
{: #at_actions_vuln}

The following table shows actions that generate management events for vulnerabilities and Vulnerability Advisor exemption policies.

| Action | Description |
|--------|-------------|
| `container-registry.account-vulnerability-report.list` | View the Vulnerability Advisor reports for images in your {{site.data.keyword.registryshort}} account.  \n  \n For more information about request data, see [Request data for the account vulnerability report](#at_events_analyze_report_list). |
| `container-registry.account-vulnerability-status.list` | View Vulnerability Advisor security status for images in your {{site.data.keyword.registryshort}} account.  \n  \n For more information about request data, see [Request data for the account vulnerability status](#at_events_analyze_status_list). |
| `container-registry.image-vulnerability-report.read` | View the Vulnerability Advisor report for an image in {{site.data.keyword.registryshort}}.  \n  \n For more information about request and response data, see [Request and response data for the vulnerability report](#at_events_analyze_report_read). |
| `container-registry.image-vulnerability-status.read` | View the Vulnerability Advisor security status for an image in {{site.data.keyword.registryshort}}.  \n  \n For more information about request and response data, see [Request and response data for the vulnerability status](#at_events_analyze_status_read). |
| `container-registry.exemption.create` | Create a Vulnerability Advisor exemption. |
| `container-registry.exemption.delete` | Delete a Vulnerability Advisor exemption. |
{: caption="Management events for vulnerabilities" caption-side="bottom"}
{: #table_events_vulnerabilities}

## Analyzing {{site.data.keyword.registryshort}} activity tracking events
{: #at_events_iam_analyze}

The following fields are populated as described, depending on how you populate the request:

- `target.name` shows the image name and, if you request an image name with a tag, a tag. If you request an image name by digest, the digest is shown instead of the tag because the digest might have many tags.

- `target.id` shows the image name by digest to represent a searchable unique ID for the image, unless the request is for an image with a tag and the request fails before the digest is discovered. To see all the events for this digest across all tags, you can search by `target.id`.

- `target.resourceGroupId` shows the resource group ID that is associated with a namespace and its resources. For more information, see [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).

    Earlier namespaces that aren't migrated to IAM don't have a resource group; therefore, this field is not available.
    {: note}

### Request data for vulnerability events
{: #at_events_vuln_events}

Get the data for vulnerability events in {{site.data.keyword.registryshort_notm}}.

#### Request data for the account vulnerability report
{: #at_events_analyze_report_list}

Get the vulnerability assessment (`container-registry.account-vulnerability-report.list`) for the list of registry images that belong to a specific account.

The following table lists the fields that are available through the `requestData` field in events with the action `container-registry.account-vulnerability-report.list`.

| Custom Event Fields | Type | Description |
|---------------------|------|-------------|
| `requestData.RequestParameters.repository` | String | The name of the repository that you want to see image vulnerability assessments for. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.includeIBM` | String | When set to `true`, the returned list contains {{site.data.keyword.IBM_notm}} public images and the account images. If not set, or set to `false`, the list contains only the account images. |
| `requestData.RequestParameters.includePrivate` | String | When set to `false`, the returned list does not contain the private account images. If not set, or set to `true`, the list contains the private account images. |
{: caption="Custom event fields for {{site.data.keyword.registryshort_notm}} account vulnerability reports list" caption-side="bottom"}
{: #table_registry_at_event_va_custom_reports_list}

For more information about the action `container-registry.account-vulnerability-report.list`, see [Get the vulnerability assessment for all images](/apidocs/vulnerability-advisor#accountreportquerypath) in the API documentation.

#### Request data for the account vulnerability status
{: #at_events_analyze_status_list}

Get the vulnerability assessment status (`container-registry.account-vulnerability-status.list`) for the list of registry images that belong to a specific account.

The following table lists the fields that are available through the `requestData` field in events with the action `container-registry.account-vulnerability-status.list`.

| Custom Event Fields | Type | Description |
|---------------------|------|-------------|
| `requestData.RequestParameters.repository` | String | The name of the repository that you want to see image vulnerability assessments for. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.includeIBM` | String | When set to `true`, the returned list contains {{site.data.keyword.IBM_notm}} public images and the account images. If not set, or set to `false`, the list contains only the account images. |
| `requestData.RequestParameters.includePrivate` | String | When set to `false`, the returned list does not contain the private account images. If not set, or set to `true`, the list contains the private account images. |
{: caption="Custom event fields for {{site.data.keyword.registryshort_notm}} account vulnerability status list" caption-side="bottom"}
{: #table_registry_at_event_va_custom_status_list}

For more information about the action `container-registry.account-vulnerability-status.list`, see [Get vulnerability assessment status for all images](/apidocs/vulnerability-advisor#accountstatusquerypath) in the API documentation.

#### Request and response data for the vulnerability report
{: #at_events_analyze_report_read}

Get the vulnerability assessment (`container-registry.image-vulnerability-report.read`) for a registry image.

The following table lists the fields that are available through the `requestData` and `responseData` fields in events with the action `container-registry.image-vulnerability-report.read`.

| Custom Event Fields | Type | Description |
|---------------------|------|-------------|
| `requestData.RequestParameters.name` | String | The name of the image. For example, `us.icr.io/namespace/repository:tag`.  \n  \n The following constraint applies: The value must match the regular expression `.*`. |
| `responseData.id` | String | The unique ID of the report. |
| `responseData.status` | String | The following values for the overall vulnerability assessment status are available:  \n  \n `OK`  \n  \n `WARN`  \n  \n `FAIL`  \n  \n `UNSUPPORTED`  \n  \n `INCOMPLETE`  \n  \n `UNSCANNED`  \n  \n For more information about these status codes, see [Vulnerability report status codes](/apidocs/vulnerability-advisor#vulnerability-report-status-codes) in the API documentation. |
{: caption="Custom event fields for {{site.data.keyword.registryshort_notm}} image vulnerability reports read" caption-side="bottom"}
{: #table_registry_at_event_va_custom_reports_read}

For more information, see [Get vulnerability assessment status](/apidocs/vulnerability-advisor#imagereportquerypath) in the API documentation.

#### Request and response data for the vulnerability status
{: #at_events_analyze_status_read}

Get the overall vulnerability status (`container-registry.image-vulnerability-status.read`) for a registry image.

The following table lists the fields that are available through the `requestData` and `responseData` fields in events with the action `container-registry.image-vulnerability-status.read`.

| Custom Event Fields | Type | Description |
|---------------------|------|-------------|
| `requestData.RequestParameters.name` | String | The name of the image. For example, `us.icr.io/namespace/repository:tag`.  \n  \n The following constraint applies: The value must match the regular expression `.*`. |
| `responseData.status` | String | The following values for the overall vulnerability assessment status are available:  \n  \n `OK`  \n  \n `WARN`  \n  \n `FAIL`  \n  \n `UNSUPPORTED`  \n  \n `INCOMPLETE`  \n  \n `UNSCANNED`  \n  \n For more information about these status codes, see [Vulnerability report status codes](/apidocs/vulnerability-advisor#vulnerability-report-status-codes) in the API documentation. |
{: caption="Custom event fields for {{site.data.keyword.registryshort_notm}} image vulnerability status read" caption-side="bottom"}
{: #table_registry_at_event_va_custom_status_read}

For more information, see [Get vulnerability status](/apidocs/vulnerability-advisor#imagestatusquerypath) in the API documentation.

### Request data for image signing events
{: #at_events_sign_events}

Get the data for events about image signing in {{site.data.keyword.registryshort_notm}}.

The following table lists the fields that are available through the `requestData` field in events with the following actions:

- `container-registry.signature.delete`
- `container-registry.signature.read`
- `container-registry.signature.write`

| Custom Event Fields | Type | Description |
|---------------------|------|-------------|
| `requestData.RequestParameters.repository` | String | The name of the repository for which you want to see image signing reports. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.signatureMethod` | String | Displays the technology that is used to sign the image, such as [{{site.data.keyword.redhat_notm}} Signing](https://www.redhat.com/en/blog/container-image-signing){: external}. |
| `requestData.RequestParameters.signatureObject` | String | Specifies the object type upon which a signing operation is implemented, for example, `image`. |
{: caption="Custom event fields for {{site.data.keyword.registryshort_notm}} signing" caption-side="bottom"}
{: #table_registry_at_event_custom_sign}
