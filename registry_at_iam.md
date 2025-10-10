---

copyright:
  years: 2020, 2025
lastupdated: "2025-10-10"

keywords: IBM Cloud, api method, registry, iam, activity tracking, actions, vulnerability, api, image, iam action, targeted account, tag

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# IAM and activity tracker audit event actions by API method for {{site.data.keyword.registryshort_notm}}
{: #registry_at_iam}

When you use {{site.data.keyword.registrylong}} through the command-line interface (CLI) or the {{site.data.keyword.cloud_notm}} console, the service calls application programming interface (API) methods to complete your requests.
{: shortdesc}

You might need certain permissions to call these API methods, and you can track the requests that you make with an {{site.data.keyword.atracker_full_notm}} and {{site.data.keyword.logs_full_notm}} instance.

Review the following {{site.data.keyword.iamshort}} (IAM) actions and the activity tracker audit events that correspond to each API method in {{site.data.keyword.registryshort_notm}}.

For more information, see the following topics:

- [{{site.data.keyword.registryshort_notm}} API documentation](https://cloud.ibm.com/apidocs/container-registry){: external}
- [Vulnerability Advisor for {{site.data.keyword.registryshort_notm}} API documentation](https://cloud.ibm.com/apidocs/vulnerability-advisor){: external}
- [Activity tracking events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events)
- [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam)

## {{site.data.keyword.registryshort_notm}}
{: #registry_at_iam_reg}

Review the following account API methods, their required actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.atracker_full_notm}} for {{site.data.keyword.registryshort_notm}}.

### Authorization API methods
{: #registry_at_iam_reg_auth}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get authorization options for the targeted account. | `GET /api/v1/auth` | `container-registry.auth.get`  | `container-registry.auth.get`  |
| Update authorization options for the targeted account. | `PATCH /api/v1/auth` | `container-registry.auth.set` | `container-registry.auth.set`  |
{: caption="Auth" caption-side="bottom"}
{: #table_registry_at_iam_auth}

### Image API methods
{: #registry_at_iam_reg_images}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List the images. | `GET /api/v1/images` | `container-registry.image.list` | `container-registry.image.list` |
| Delete more than one image. | `POST /api/v1/images/bulkdelete` | `container-registry.image.delete` | `container-registry.image.bulkdelete` |
| List the images by digest. | `POST /api/v1/images/digests` | `container-registry.image.list` | `container-registry.image.list` |
| Create a tag. | `POST /api/v1/images/tags` | `container-registry.image.pull`  \n  \n `container-registry.image.push` | `container-registry.image.tag` |
| Delete an image. | `DELETE /api/v1/images/{image}` | `container-registry.image.delete` | `container-registry.image.delete`|
| Inspect an image. | `GET /api/v1/images/{image}/json` | `container-registry.image.inspect` | `container-registry.image.inspect` |
| Get the image manifest. | `GET /api/v1/images/{image}/manifest` | `container-registry.image.inspect` | `container-registry.manifest.inspect` |
{: caption="Images" caption-side="bottom"}
{: #table_registry_at_iam_images}

### Message API methods
{: #registry_at_iam_reg_messages}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Return any published system messages. | `GET /api/v1/messages` | Not applicable | Not applicable |
{: caption="Messages" caption-side="bottom"}
{: #table_registry_at_iam_messages}

### Namespace API methods
{: #registry_at_iam_reg_namespace}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List the namespaces. | `GET /api/v1/namespaces` | `container-registry.namespace.list` | `container-registry.namespace.list` |
| Detailed namespace list. | `GET /api/v1/namespaces/details` | `container-registry.namespace.list` | `container-registry.namespace.list` |
| Create a namespace. | `PUT /api/v1/namespaces/{namespace}` | `container-registry.namespace.create` | `container-registry.namespace.create` |
| Assign a namespace. | `PATCH /api/v1/namespaces/{namespace}` | `container-registry.namespace.create` | `container-registry.namespace.update` |
| Delete a namespace. | `DELETE /api/v1/namespaces/{namespace}` | `container-registry.namespace.delete` | `container-registry.namespace.delete` |
{: caption="Namespaces" caption-side="bottom"}
{: #table_registry_at_iam_namespaces}

### Plan API methods
{: #registry_at_iam_reg_plans}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get plans for the targeted account. | `GET /api/v1/plans` | `container-registry.plan.get` | `container-registry.plan.get` |
| Update plans for the targeted account. | `PATCH /api/v1/plans` | `container-registry.plan.set` | `container-registry.plan.set` |
{: caption="Plans" caption-side="bottom"}
{: #table_registry_at_iam_plans}

### Quota API methods
{: #registry_at_iam_reg_quota}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get the quotas for the targeted account. | `GET /api/v1/quotas` | `container-registry.quota.get` | `container-registry.quota.get` |
| Update the quotas for the targeted account. | `PATCH /api/v1/quotas` | `container-registry.quota.set` | `container-registry.quota.set` |
{: caption="Quotas" caption-side="bottom"}
{: #table_registry_at_iam_quotas}

### Retention API methods
{: #registry_at_iam_reg_retention}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List the retention policies for all namespaces in the targeted {{site.data.keyword.cloud_notm}} account. | `GET /api/v1/retentions` | `container-registry.retention.list` | `container-registry.retention.list` |
| Set the retention policy for the specified namespace. | `POST /api/v1/retentions` | `container-registry.retention.set` | `container-registry.retention.set` |
| Analyze a retention policy, and get a list of what would be deleted by it. | `POST /api/v1/retentions/analyze` | `container-registry.retention.analyze`  | `container-registry.retention.analyze`  |
| Get the retention policy for the specified namespace. | `GET /api/v1/retentions/{namespace}` | `container-registry.retention.get` | `container-registry.retention.get`  |
{: caption="Retentions" caption-side="bottom"}
{: #table_registry_at_iam_retentions}

### Settings API methods
{: #registry_at_iam_reg_set}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get the registry service settings for the targeted account, such as whether platform metrics are enabled. | `GET /api/v1/settings` | `container-registry.settings.get` | `container-registry.settings.get` |
| Update the registry service settings for the targeted account, such as enabling platform metrics. | `PATCH /api/v1/settings` | `container-registry.settings.set` | `container-registry.settings.set` |
{: caption="Settings" caption-side="bottom"}
{: #table_registry_at_iam_settings}

### Tag API methods
{: #registry_at_iam_reg_tags}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Delete a tag. | `DELETE /api/v1/tags/{image}` | `container-registry.image.delete` | `container-registry.image.untag` |
{: caption="Tags" caption-side="bottom"}
{: #table_registry_at_iam_tags}

### Trash API methods
{: #registry_at_iam_reg_trash}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List the images in the trash. | `GET /api/v1/trash` | `container-registry.image.delete` | `container-registry.trash.list` |
| Restore a digest and all associated tags. | `POST /api/v1/trash/{digest}/restoretags` | `container-registry.image.push` | `container-registry.trash.restore` |
| Restore a deleted image. | `POST /api/v1/trash/{image}/restore` | `container-registry.image.push` | `container-registry.trash.restore` |
{: caption="Trash" caption-side="bottom"}
{: #table_registry_at_iam_trash}

## Vulnerability Advisor API methods
{: #registry_at_iam_vuln}

### Report API methods
{: #registry_at_iam_vuln_report}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get the vulnerability assessment for all images. | `GET /va/api/v4/report/account` | `container-registry.exemption.list` | `container-registry.account-vulnerability-report.list` |
| Get the vulnerability assessment status for all images. | `GET /va/api/v4/report/account/status` | `container-registry.exemption.list` | `container-registry.account-vulnerability-status.list` |
| Get the vulnerability status. | `GET /va/api/v4/report/image/status/{name}` | `container-registry.exemption.list` | `container-registry.image-vulnerability-status.read` |
| Get the vulnerability assessment status. | `GET /va/api/v4/report/image/{name}` | `container-registry.exemption.list` | `container-registry.image-vulnerability-report.read` |
{: caption="Report for version 4" caption-side="bottom"}
{: #table_registry_at_iam_v4_report}

### Exemption API methods
{: #registry_at_iam_vuln_exempt}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List the account-level exemptions. | `GET /va/api/v4/exempt/image` | `container-registry.exemption.list` | Not applicable |
| Get an account-level exemption. | `GET /va/api/v4/exempt/image/issue/{issueType}/{issueID}` | `container-registry.exemption.list` | Not applicable |
| Create or update an account-level exemption. | `POST /va/api/v4/exempt/image/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.create` |
| Delete an account-level exemption. | `DELETE /va/api/v4/exempt/image/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.delete` |
| List the resource exemptions. | `GET /va/api/v4/exempt/image/{resource}` | `container-registry.exemption.list` | Not applicable |
| Get the details of a resource exemption. | `GET /va/api/v4/exempt/image/{resource}/issue/{issueType}/{issueID}` | `container-registry.exemption.list` | Not applicable |
| Create or update a resource exemption. | `POST /va/api/v4/exempt/image/{resource}/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.create` |
| Delete a resource exemption. | `DELETE /va/api/v4/exempt/image/{resource}/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.delete` |
| List the types of exemption. | `GET /va/api/v4/exempt/types` | Not applicable | Not applicable |
| List all exemptions. | `GET /va/api/v4/exemptions/account` | `container-registry.exemption.list` | Not applicable |
| Delete all exemptions. | `POST /va/api/v4/exemptions/deleteAll` | `container-registry.exemption.manager` | `container-registry.exemption.delete` |
| List the image exemptions. | `GET /va/api/v4/exemptions/image/{resource}` | `container-registry.exemption.list` | Not applicable |
| List the exemptions for images. | `POST /va/api/v4/exemptions/images` | `container-registry.exemption.list` | Not applicable |
{: caption="Exemptions for version 4" caption-side="bottom"}
{: #table_registry_at_iam_v4_exempt}
