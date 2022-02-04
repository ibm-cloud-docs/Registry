---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-04"

keywords: IBM Cloud, observability, api methods, registry, iam, activity tracker, actions

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# IAM and Activity Tracker actions by API method
{: #registry_at_iam}

When you use {{site.data.keyword.registrylong}} through the command line or console, the service calls application programming interface (API) methods to complete your requests. You might need certain permissions to call these API methods, and you can track the requests that you make with an {{site.data.keyword.at_full_notm}} instance.
{: shortdesc}

Review the following list of {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) actions and {{site.data.keyword.at_full_notm}} events that correspond to each API method in {{site.data.keyword.registryshort_notm}}.

For more information, see the following topics:

- [{{site.data.keyword.registryshort_notm}} API documentation](https://cloud.ibm.com/apidocs/container-registry){: external}
- [Vulnerability Advisor for {{site.data.keyword.registryshort_notm}} API documentation](https://cloud.ibm.com/apidocs/container-registry/va){: external}
- [Auditing the events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events)
- [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam)

## {{site.data.keyword.registryshort_notm}}
{: #registry_at_iam_reg}

Review the following account API methods, their required actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for  {{site.data.keyword.registryshort_notm}}.

### Auth
{: #registry_at_iam_reg_auth}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get authorization options for the targeted account. | `GET /api/v1/auth` | `container-registry.auth.get`  | `container-registry.auth.get`  |
| Update authorization options for the targeted account. | `PATCH /api/v1/auth` | `container-registry.auth.set` | `container-registry.auth.set`  |
{: caption="Table 1. Auth" caption-side="bottom"}

### Images
{: #registry_at_iam_reg_images}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List images. | `GET /api/v1/images` | `container-registry.image.list` | `container-registry.image.list` |
| Bulk delete images. | `POST /api/v1/images/bulkdelete` | `container-registry.image.delete` | `container-registry.image.bulkdelete` |
| List images by digest. | `POST /api/v1/images/digests` | `container-registry.image.list` | `container-registry.image.list` |
| Create tag. | `POST /api/v1/images/tags` | `container-registry.image.pull`  \n  \n `container-registry.image.push` | `container-registry.image.tag` |
| Delete image. | `DELETE /api/v1/images/{image}` | `container-registry.image.delete` | `container-registry.image.delete`|
| Inspect an image. | `GET /api/v1/images/{image}/json` | `container-registry.image.inspect` | `container-registry.image.inspect` |
| Get image manifest. | `GET /api/v1/images/{image}/manifest` | `container-registry.image.inspect` | `container-registry.manifest.inspect` |
{: caption="Table 2. Images" caption-side="bottom"}

### Messages
{: #registry_at_iam_reg_messages}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Return any published system messages. | `GET /api/v1/messages` | | |
{: caption="Table 3. Messages" caption-side="bottom"}

### Namespaces
{: #registry_at_iam_reg_namespace}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List namespaces. | `GET /api/v1/namespaces` | `container-registry.namespace.list` | `container-registry.namespace.list` |
| Detailed namespace list. | `GET /api/v1/namespaces/details` | `container-registry.namespace.list` | `container-registry.namespace.list` |
| Create namespace. | `PUT /api/v1/namespaces/{namespace}` | `container-registry.namespace.create` | `container-registry.namespace.create` |
| Assign namespace. | `PATCH /api/v1/namespaces/{namespace}` | `container-registry.namespace.create` | `container-registry.namespace.update` |
| Delete namespace. | `DELETE /api/v1/namespaces/{namespace}` | `container-registry.namespace.delete` | `container-registry.namespace.delete` |
{: caption="Table 4. Namespaces" caption-side="bottom"}

### Plans
{: #registry_at_iam_reg_plans}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get plans for the targeted account. | `GET /api/v1/plans` | `container-registry.plan.get` | `container-registry.plan.get` |
| Update plans for the targeted account. | `PATCH /api/v1/plans` | `container-registry.plan.set` | `container-registry.plan.set` |
{: caption="Table 5. Plans" caption-side="bottom"}

### Quotas
{: #registry_at_iam_reg_quota}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get quotas for the targeted account. | `GET /api/v1/quotas` | `container-registry.quota.get` | `container-registry.quota.get` |
| Update quotas for the targeted account. | `PATCH /api/v1/quotas` | `container-registry.quota.set` | `container-registry.quota.set` |
{: caption="Table 6. Quotas" caption-side="bottom"}

### Retentions
{: #registry_at_iam_reg_retention}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List retention policies for all namespaces in the targeted {{site.data.keyword.cloud_notm}} account. | `GET /api/v1/retentions` | `container-registry.retention.list` | `container-registry.retention.list` |
| Set the retention policy for the specified namespace. | `POST /api/v1/retentions` | `container-registry.retention.set` | `container-registry.retention.set` |
| Analyze a retention policy, and get a list of what would be deleted by it. | `POST /api/v1/retentions/analyze` | `container-registry.retention.analyze`  | `container-registry.retention.analyze`  |
| Get the retention policy for the specified namespace. | `GET /api/v1/retentions/{namespace}` | `container-registry.retention.get` | `container-registry.retention.get`  |
{: caption="Table 7. Retentions" caption-side="bottom"}

### Settings
{: #registry_at_iam_reg_set}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get registry service settings for the targeted account, such as whether platform metrics are enabled. | `GET /api/v1/settings` | `container-registry.settings.get` | `container-registry.settings.get` |
| Update registry service settings for the targeted account, such as enabling platform metrics. | `PATCH /api/v1/settings` | `container-registry.settings.set` | `container-registry.settings.set` |
{: caption="Table 8. Settings" caption-side="bottom"}

### Tags
{: #registry_at_iam_reg_tags}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Delete tag. | `DELETE /api/v1/tags/{image}` | `container-registry.image.delete` | `container-registry.image.untag` |
{: caption="Table 9. Tags" caption-side="bottom"}

### Trash
{: #registry_at_iam_reg_trash}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List images in the trash. | `GET /api/v1/trash` | `container-registry.image.delete` | `container-registry.trash.list` |
| Restore a digest and all associated tags. | `POST /api/v1/trash/{digest}/restoretags` | `container-registry.image.push` | `container-registry.trash.restore` |
| Restore deleted image. | `POST /api/v1/trash/{image}/restore` | `container-registry.image.push` | `container-registry.trash.restore` |
{: caption="Table 10. Trash" caption-side="bottom"}

## Vulnerability Advisor
{: #registry_at_iam_vuln}

### Report
{: #registry_at_iam_vuln_report}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Get the vulnerability assessment for all images. | `GET /va/api/v3/report/account` | `container-registry.exemption.list` | `container-registry.account-vulnerability-report.list` |
| Get vulnerability assessment status for all images. | `GET /va/api/v3/report/account/status` | `container-registry.exemption.list` | `container-registry.account-vulnerability-status.list` |
| Get vulnerability status. | `GET /va/api/v3/report/image/status/{name}` | `container-registry.exemption.list` | `container-registry.image-vulnerability-status.read` |
| Get vulnerability assessment status. | `GET /va/api/v3/report/image/{name}` | `container-registry.exemption.list` | `container-registry.image-vulnerability-report.read` |
{: caption="Table 11. Report" caption-side="bottom"}

### Exemption
{: #registry_at_iam_vuln_exempt}

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| List account level exemptions. | `GET /va/api/v3/exempt/image` | `container-registry.exemption.list` | |
| Get an account level exemption. | `GET /va/api/v3/exempt/image/issue/{issueType}/{issueID}` | `container-registry.exemption.list` | |
| Create or update an account level exemption. | `POST /va/api/v3/exempt/image/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.create` |
| Delete an account level exemption. | `DELETE /va/api/v3/exempt/image/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.delete` |
| List resource exemptions. | `GET /va/api/v3/exempt/image/{resource}` | `container-registry.exemption.list` | |
| Get details of a resource exemption. | `GET /va/api/v3/exempt/image/{resource}/issue/{issueType}/{issueID}` | `container-registry.exemption.list` | |
| Create or update a resource exemption. | `POST /va/api/v3/exempt/image/{resource}/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.create` |
| Delete a resource exemption. | `DELETE /va/api/v3/exempt/image/{resource}/issue/{issueType}/{issueID}` | `container-registry.exemption.manager` | `container-registry.exemption.delete` |
| List the types of exemption. | `GET /va/api/v3/exempt/types` | | |
| List all exemptions. | `GET /va/api/v3/exemptions/account` | `container-registry.exemption.list` | |
| Delete all exemptions. | `POST /va/api/v3/exemptions/deleteAll` | `container-registry.exemption.manager` | `container-registry.exemption.delete` |
| List image exemptions. | `GET /va/api/v3/exemptions/image/{resource}` | `container-registry.exemption.list` | |
| List exemptions for images. | `POST /va/api/v3/exemptions/images` | `container-registry.exemption.list` | |
{: caption="Table 12. Exemption" caption-side="bottom"}


