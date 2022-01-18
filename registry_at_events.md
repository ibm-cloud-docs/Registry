---

copyright:
  years: 2018, 2022
lastupdated: "2022-01-18"

keywords: Track, tracking events, find events, look for events, activity tracker for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry events, IBM Cloud Container Registry security, audit logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry events, IBM Cloud Container Registry events,

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Auditing the events for {{site.data.keyword.registryshort_notm}}
{: #at_events}

Use {{site.data.keyword.at_full}} to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

The {{site.data.keyword.at_full_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}. For more information, see [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

From 19 August 2021, {{site.data.keyword.registrylong_notm}} tokens are discontinued and do not work. For more information, see [{{site.data.keyword.registrylong_notm}} Deprecates Registry Tokens for Authentication](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecates-registry-tokens-for-authentication){: external}.
{: deprecated}

The `ibmcloud cr build` command is discontinued from 5 October 2021. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead. For more information, see [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecating-container-builds){: external}.
{: deprecated}

## API methods
{: #at_events_api_methods}

The following tables list the API methods that generate an event when they are called.

### Actions that generate events for authorization
{: #at_events_api_methods_auth}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.auth.get` | Check whether the use of public connections is prevented for image pushes or pulls in your account. | |
| `container-registry.auth.set` | Prevent or allow image pulls or pushes over public network connections for your account. | |
{: caption="Table 1. Actions that generate events for your authorization" caption-side="bottom"}

### Actions that generate events for images
{: #at_events_api_methods_images}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.image.bulkdelete` | Delete multiple images from {{site.data.keyword.registrylong_notm}}. If the image is signed, the signature is deleted as well. | True |
| `container-registry.image.delete` | Delete an image from {{site.data.keyword.registrylong_notm}}. If the image is signed, the signature is deleted as well. | True |
| `container-registry.image.inspect` | Display details about an image. | |
| `container-registry.image.list` | List the images in your {{site.data.keyword.IBM_notm}} account. | |
| `container-registry.image.pull` | Pull an image from {{site.data.keyword.registrylong_notm}}. | True |
| `container-registry.image.push` | Push an image to {{site.data.keyword.registrylong_notm}}. | True |
| `container-registry.image.tag` | Add a tag that refers to a pre-existing {{site.data.keyword.registrylong_notm}} image. | |
| `container-registry.image.untag` | Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.manifest.inspect` | View the contents of the manifest for an image. | |
{: caption="Table 2. Actions that generate events for images" caption-side="bottom"}

### Actions that generate events for namespaces
{: #at_events_api_methods_namespaces}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.namespace.create` | Create a namespace in {{site.data.keyword.registrylong_notm}}.  \n  \n Assign an {{site.data.keyword.registrylong_notm}} namespace to a [resource group](x2161955){: term}. | |
| `container-registry.namespace.delete` | Delete a namespace from {{site.data.keyword.registrylong_notm}}. | |
| `container-registry.namespace.list` | List the {{site.data.keyword.registrylong_notm}} namespaces in your {{site.data.keyword.IBM_notm}} account. | |
{: caption="Table 3. Actions that generate events for namespaces" caption-side="bottom"}

### Actions that generate events for plans
{: #at_events_api_methods_plan}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.plan.get` | Display information about the current pricing plan. | |
| `container-registry.plan.set` | Upgrade to the standard plan. | |
{: caption="Table 4. Actions that generate events for plans" caption-side="bottom"}

### Actions that generate events for quotas
{: #at_events_api_methods_quota}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.quota.get` | Display the current quotas for traffic and storage, and the usage information against those quotas. | |
| `container-registry.quota.set` | Modify the quotas. Quota settings must be managed separately for your account in each registry instance. You can set quota limits for storage in your free or standard plan. | |
{: caption="Table 5. Actions that generate events for quotas" caption-side="bottom"}

### Actions that generate events for retention policies
{: #at_events_api_methods_retention}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.retention.analyze` | List the images that are deleted if you apply a specific retention policy. | |
| `container-registry.retention.list` | List the image retention policies for your account. | |
| `container-registry.retention.set` | Set a policy to retain images in a namespace in {{site.data.keyword.registrylong_notm}} by applying specified criteria. | |
{: caption="Table 6. Actions that generate events for retention policies" caption-side="bottom"}

### Actions that generate events for settings
{: #at_events_api_methods_setting}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.settings.get` | Get registry service settings for the targeted account, such as whether platform metrics are enabled. | |
| `container-registry.settings.set` | Update registry service settings for the targeted account, such as enabling platform metrics. | |
{: caption="Table 7. Actions that generate events for settings" caption-side="bottom"}

### Actions that generate events for signing images
{: #at_events_api_methods_sign}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.signature.delete` | Delete a signature from an image in {{site.data.keyword.registrylong_notm}}. | True |
| `container-registry.signature.read` | Read a signature from an image in {{site.data.keyword.registrylong_notm}}. | True |
| `container-registry.signature.write` | Write a signature to an image in {{site.data.keyword.registrylong_notm}}. | True |
{: caption="Table 8. Actions that generate events for signing images" caption-side="bottom"}

### Actions that generate events for trash
{: #at_events_api_methods_trash}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.trash.list` | Display all the images in the trash in your {{site.data.keyword.cloud_notm}} account. | |
| `container-registry.trash.restore` | Restore a deleted image from the trash. If the deleted image is signed, the signature is restored too. | |
{: caption="Table 9. Actions that generate events for trash" caption-side="bottom"}

### Actions that generate events for vulnerabilities
{: #at_events_api_methods_vuln}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.account-vulnerability-report.list` | View the Vulnerability Advisor reports for images in your {{site.data.keyword.registrylong_notm}} account.  \n  \n For more information about request data, see [Request data for `container-registry.account-vulnerability-report.list`](#at_events_analyze_report_list). | |
| `container-registry.account-vulnerability-status.list` | View Vulnerability Advisor security status for images in your {{site.data.keyword.registrylong_notm}} account.  \n  \n For more information about request data, see [Request data for `container-registry.account-vulnerability-status.list`](#at_events_analyze_status_list). | |
| `container-registry.image-vulnerability-report.read` | View the Vulnerability Advisor report for an image in {{site.data.keyword.registrylong_notm}}.  \n  \n For more information about request and response data, see [Request and response data for `container-registry.image-vulnerability-report.read`](#at_events_analyze_report_read). | |
| `container-registry.image-vulnerability-status.read` | View the Vulnerability Advisor security status for an image in {{site.data.keyword.registrylong_notm}}.  \n  \n For more information about request and response data, see [Request and response data for `container-registry.image-vulnerability-status.read`](#at_events_analyze_status_read). | |
{: caption="Table 10. Actions that generate events for vulnerabilities" caption-side="bottom"}

### Actions that generate events for Vulnerability Advisor exemption policies
{: #at_events_api_methods_exemptions}

| Action | Description | Data Event |
|--------|-------------|------------|
| `container-registry.exemption.create` | Create a Vulnerability Advisor exemption. | |
| `container-registry.exemption.delete` | Delete a Vulnerability Advisor exemption. | |
{: caption="Table 11. Actions that generate events for Vulnerability Advisor exemption policies" caption-side="bottom"}

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
| `br-sao` | `br.icr.io` | `Sao Paulo (br-sao)` |
| `ca-tor` | `ca.icr.io` | `Toronto (ca-tor)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `jp-osa` | `jp2.icr.io` | `Osaka (jp-osa)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
{: caption="Table 12. Location of {{site.data.keyword.at_full_notm}} events" caption-side="bottom"}

The following table shows the location of global registry {{site.data.keyword.at_full_notm}} events.

| Registry | Global registry | Location of {{site.data.keyword.at_full_notm}} events |
|-----------------|-----------------|-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 13. Location of global registry {{site.data.keyword.at_full_notm}} events" caption-side="bottom"}

For more information about {{site.data.keyword.cloud_notm}} services by location, see [Container services](/docs/activity-tracker?topic=activity-tracker-cloud_services_locations#cloud_services_locations_container).

## Analyzing Activity Tracker events
{: #at_events_analyze}

The following fields are populated as described, depending on how you populate the request:

- `target.name` shows the image name and, if you request an image name with a tag, a tag. If you request an image name by digest, the digest is shown instead of the tag because the digest might have many tags.

- `target.id` shows the image name by digest to represent a searchable unique ID for the image, unless the request is for an image with a tag and the request fails before the digest is discovered. To see all the events for this digest across all tags, you can search by `target.id`.

- `target.resourceGroupId` shows the resource group ID that is associated with a namespace and its resources. For more information, see [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).

    Legacy namespaces that are not migrated to IAM do not have a resource group, therefore this field is not available.
    {: note}

### Request data for vulnerability events
{: #at_events_vuln_events}

Get the data for vulnerability events in {{site.data.keyword.registryshort_notm}}.
{: shortdesc}

#### Request data for `container-registry.account-vulnerability-report.list`
{: #at_events_analyze_report_list}

Get the vulnerability assessment for the list of registry images that belong to a specific account.
{: shortdesc}

The following table lists the fields that are available through the `requestData` field in events with the action `container-registry.account-vulnerability-report.list`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.repository` | String | The name of the repository that you want to see image vulnerability assessments for. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.includeIBM` | String | When set to `true`, the returned list contains {{site.data.keyword.IBM_notm}} public images and the account images. If not set, or set to `false`, the list contains only the account images. |
| `requestData.RequestParameters.includePrivate` | String | When set to `false`, the returned list does not contain the private account images. If not set, or set to `true`, the list contains the private account images. |
{: caption="Table 14. Custom event fields for {{site.data.keyword.registryshort_notm}} account vulnerability reports list" caption-side="bottom"}

For more information about the action `container-registry.account-vulnerability-report.list`, see [Get the vulnerability assessment for all images](/apidocs/container-registry/va#accountreportquerypath) in the API documentation.

#### Request data for `container-registry.account-vulnerability-status.list`
{: #at_events_analyze_status_list}

Get the vulnerability assessment status for the list of registry images that belong to a specific account.
{: shortdesc}

The following table lists the fields that are available through the `requestData` field in events with the action `container-registry.account-vulnerability-status.list`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.repository` | String | The name of the repository that you want to see image vulnerability assessments for. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.includeIBM` | String | When set to `true`, the returned list contains {{site.data.keyword.IBM_notm}} public images and the account images. If not set, or set to `false`, the list contains only the account images. |
| `requestData.RequestParameters.includePrivate` | String | When set to `false`, the returned list does not contain the private account images. If not set, or set to `true`, the list contains the private account images. |
{: caption="Table 15. Custom event fields for {{site.data.keyword.registryshort_notm}} account vulnerability status list" caption-side="bottom"}

For more information about the action `container-registry.account-vulnerability-status.list`, see [Get vulnerability assessment status for all images](/apidocs/container-registry/va#accountstatusquerypath) in the API documentation.

#### Request and response data for `container-registry.image-vulnerability-report.read`
{: #at_events_analyze_report_read}

Get the vulnerability assessment for a registry image.
{: shortdesc}

The following table lists the fields that are available through the `requestData` and `responseData` fields in events with the action `container-registry.image-vulnerability-report.read`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.name` | String | The name of the image. For example, `us.icr.io/namespace/repository:tag`.  \n  \n Constraints: Value must match regular expression `.*`. |
| `responseData.id` | String | The unique ID of the report. |
| `responseData.status` | String | Overall vulnerability assessment status:  \n  \n `OK`  \n  \n `WARN`  \n  \n `FAIL`  \n  \n `UNSUPPORTED`  \n  \n `INCOMPLETE`  \n  \n `UNSCANNED`  \n  \n For more information about these status codes, see [Vulnerability report status codes](/apidocs/container-registry/va#vulnerability-report-status-codes) in the API documentation. |
{: caption="Table 16. Custom event fields for {{site.data.keyword.registryshort_notm}} image vulnerability reports read" caption-side="bottom"}

For more information, see [Get vulnerability assessment status](/apidocs/container-registry/va#imagereportquerypath) in the API documentation.

#### Request and response data for `container-registry.image-vulnerability-status.read`
{: #at_events_analyze_status_read}

Get the overall vulnerability status for a registry image.
{: shortdesc}

The following table lists the fields that are available through the `requestData` and `responseData` fields in events with the action `container-registry.image-vulnerability-status.read`.

| Custom Event Fields | Type | Description |
|-----------------|-----------------|-----------------|
| `requestData.RequestParameters.name` | String | The name of the image. For example, `us.icr.io/namespace/repository:tag`.  \n  \n Constraints: Value must match regular expression `.*`. |
| `responseData.status` | String | Overall vulnerability assessment status:  \n  \n `OK`  \n  \n `WARN`  \n  \n `FAIL`  \n  \n `UNSUPPORTED`  \n  \n `INCOMPLETE`  \n  \n `UNSCANNED`  \n  \n For more information about these status codes, see [Vulnerability report status codes](/apidocs/container-registry/va#vulnerability-report-status-codes) in the API documentation.
{: caption="Table 17. Custom event fields for {{site.data.keyword.registryshort_notm}} image vulnerability status read" caption-side="bottom"}

For more information, see [Get vulnerability status](/apidocs/container-registry/va#imagestatusquerypath) in the API documentation.

### Request data for image signing events
{: #at_events_sign_events}

Get the data for image signing events in {{site.data.keyword.registryshort_notm}}.
{: shortdesc}

The following table lists the fields that are available through the `requestData` field in events with the following actions:

-  `container-registry.signature.delete`
-  `container-registry.signature.read`
-  `container-registry.signature.write`

| Custom Event Fields | Type | Description |
|---------------------|------|-------------|
| `requestData.RequestParameters.repository` | String | The name of the repository for which you want to see image signing reports. For example, `us.icr.io/namespace/image`. |
| `requestData.RequestParameters.signatureMethod` | String | Displays the technology that is used to sign the image, such as [Red Hat Signing](https://www.redhat.com/en/blog/container-image-signing){: external}. |
| `requestData.RequestParameters.signatureObject` | String | Specifies the object type upon which a signing operation is performed, for example, `image`. |
{: caption="Table 18. Custom event fields for {{site.data.keyword.registryshort_notm}} signing" caption-side="bottom"}



