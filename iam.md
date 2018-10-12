---

copyright:
  years: 2018
lastupdated: "2018-10-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Managing user access with Identity and Access Management
{: #iam}

Access to {{site.data.keyword.registrylong}} for users in your account is controlled by {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM).
{: shortdesc}

When IAM policies are enabled for your account in {{site.data.keyword.registrylong_notm}}, every user that accesses the {{site.data.keyword.registrylong_notm}} service in your account must be assigned an access policy with an IAM user role defined. That policy determines what role the user has within the context of the service, and what actions the user can perform. Each action in {{site.data.keyword.registrylong_notm}} is mapped to one or more [IAM user roles](/docs/iam/users_roles.html).

IAM policies are enforced only when you use IAM to log in to {{site.data.keyword.registrylong_notm}}. If you log in to {{site.data.keyword.registrylong_notm}} by using another method, such as a registry token, your policies are not enforced. If you want to restrict access to one or more namespaces for an ID that is used in automation, consider using an IAM Service ID instead of a registry token. For more information about Service IDs, see [Creating and working with Service IDs](/docs/iam/serviceid.html#serviceids).

For more information about IAM, see [IBM Cloud Access and Management](/docs/iam/index.html#iamoverview).

For information about enabling policies for {{site.data.keyword.registrylong_notm}}, see [Defining user access role policies](/docs/services/Registry/registry_users.html#user).

Policies enable access to be granted at different levels. Some of the options include the following:

* Access to the service in your account
* Access to a specific resource within the service
* Access to all IAM-enabled services in your account

After you define the scope of the access policy, you assign a role. Review the following tables which outline what actions each role allows within the {{site.data.keyword.registrylong_notm}} service.

For information about managing user roles, see [Working with users](/docs/iam/iamusermanage.html#iamusermanage).

For information about assigning user roles in the UI, see [Managing IAM access](/docs/iam/mngiam.html#iammanidaccser).

Try out the tutorial [Tutorial: Granting access to {{site.data.keyword.registrylong_notm}} resources](/docs/services/Registry/registry_tutorial_configure_iam.html#iam_access).
{: tip}

## Platform management roles
{: #platform_management_roles}

The following table details actions that are mapped to platform management roles. Platform management roles enable users to perform tasks on service resources at the platform level, for example assign user access for the service, and create or delete Service IDs.

| Platform management role | Description of actions | Example actions|
|:-----------------|:-----------------|:-----------------|
| Viewer | Not supported | |
| Editor | Not supported | |
| Operator | Not supported | |
| Administrator | <ul><li>Configure access for other users</li><li> Configure registry tokens</li><li>Create clusters</li></ul> | <ul><li>For information about assigning user roles in the UI, see [Managing IAM access](/docs/iam/mngiam.html#iammanidaccser).</li><li>Add, list, retrieve, and remove registry tokens</li><li>To create clusters in {{site.data.keyword.containerlong_notm}}, you must assign the Administrator role for {{site.data.keyword.registrylong_notm}} to the user, see [Preparing to create clusters](/docs/containers/cs_clusters.html#cluster_prepare).</ul> |
{: caption="Table 1. IAM user roles and actions" caption-side="top"}

For {{site.data.keyword.registrylong_notm}}, the following actions exist:

| Action| Operation on service | Role
|:-----------------|:-----------------|:--------------|
| `container-registry.registrytoken.create` | [`ibmcloud cr token-add`](/docs/services/Registry/registry_cli.html#bx_cr_token_add) Add a token that you can use to control access to a registry. | Administrator |
| `container-registry.registrytoken.delete` | [`ibmcloud cr token-rm`](/docs/services/Registry/registry_cli.html#bx_cr_token_rm) Remove one or more specified tokens. | Administrator |
| `container-registry.registrytoken.get` | [`ibmcloud cr token-get`](/docs/services/Registry/registry_cli.html#bx_cr_token_get) Retrieve the specified token from the registry. | Administrator |
| `container-registry.registrytoken.list` | [`ibmcloud cr token-list`](/docs/services/Registry/registry_cli.html#bx_cr_token_list) Display all tokens that exist for your {{site.data.keyword.Bluemix_notm}} account. | Administrator |
{: caption="Table 2. Platform actions and operations for configuring {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Service access roles
{: #service_access_roles}

The following table details actions that are mapped to service access roles. Service access roles enable users access to {{site.data.keyword.registrylong_notm}} as well as the ability to call the {{site.data.keyword.registrylong_notm}} API.

| Service access role | Description of actions | Example actions|
|:-----------------|:-----------------|:-----------------|
| Reader | The Reader role can view information. | <ul><li>View, inspect, and pull images</li><li>View namespaces</li><li>View quotas</li><li>View vulnerability reports</li><li>View image signatures</li></ul>|
| Writer | The Writer role can edit information. |<ul><li>Build, push, and delete images</li><li>View quotas</li><li>Sign images</li><li>Add and remove namespaces</li></ul> |
| Manager | The Manager role can perform all actions. | <ul><li>View, inspect, pull, build, push, and delete images</li><li>View, add, and remove namespaces</li><li>View and set quotas</li><li>View vulnerability reports</li><li>View and create image signatures</li><li>Review and change pricing plans</li><li>Enable IAM policy enforcement</li><li>Manage Vulnerability Advisor exemptions</li></ul> |
{: caption="Table 3. IAM service access roles and actions" caption-side="top"}

 For the following {{site.data.keyword.registrylong_notm}} commands, you must have at least one of the specified roles as shown in the following tables. To create a policy that allows access to {{site.data.keyword.registrylong_notm}} you must create a policy where the service name is `container-registry`, the service instance is empty, and the region is the region that you want to grant access to, or empty to give access to all regions.

### Access roles for configuring {{site.data.keyword.registrylong_notm}}
{: #access_roles_configure}

To grant a user permission to configure your {{site.data.keyword.registrylong_notm}} in your account, you must create a policy that grants one or more of the roles in the following table. When creating your policy, you must not specify a `resource type` or `resource`.

**Example**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

| Action| Operation on service | Role
|:-----------------|:-----------------|:--------------|
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/services/Registry/registry_cli.html#bx_cr_iam_policies_enable) Enable IAM policy enforcement. | Manager |
| `container-registry.exemption.manager` | <ul><li>[`ibmcloud cr exemption-add`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_add) Create an exemption for a security issue.</li><li>[`ibmcloud cr exemption-list`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_list) List your exemptions for security issues. </li><li>[`ibmcloud cr exemption-rm`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_rm) Delete an exemption for a security issue.</li><li>[`ibmcloud cr exemption-types`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_types) List the types of security issues that you can exempt. | Manager |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/services/Registry/registry_cli.html#bx_cr_plan) Display your pricing plan. | Manager |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/services/Registry/registry_cli.html#bx_cr_plan_upgrade) Upgrade to the standard plan. | Manager |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/services/Registry/registry_cli.html#bx_cr_quota) Display your current quotas for traffic and storage, and usage information against those quotas. | Reader, Writer, Manager |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/services/Registry/registry_cli.html#bx_cr_quota_set) Modify the specified quota. | Manager |
{: caption="Table 4. Service actions and operations for configuring {{site.data.keyword.registrylong_notm}}" caption-side="top"}

### Access roles for using {{site.data.keyword.registrylong_notm}}
{: #access_roles_using}

To grant a user permission to access {{site.data.keyword.registrylong_notm}} content in your account you must create a policy that grants one or more of the roles in the following table. When creating your policy, you can restrict access to a specific namespace by specifying the resource type `namespace` and the namespace name as the resource. If you don't specify a `resource-type` and a `resource`, the policy grants access to all resource in the account. 

**Example**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Reader> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

| Action | Operation on service | Role
|:-----------------|:-----------------|:--------------|
| `container-registry.image.build` | [`ibmcloud cr build`](/docs/services/Registry/registry_cli.html#bx_cr_build) Build a container image. | Writer, Manager |
| `container-registry.image.delete` | [`ibmcloud cr image-rm`](/docs/services/Registry/registry_cli.html#bx_cr_image_rm) Delete one or more images. | Writer, Manager |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/services/Registry/registry_cli.html#bx_cr_image_inspect) Display details about a specific image. | Reader, Manager |
| `container-registry.image.list` | [`ibmcloud cr image-list`](/docs/services/Registry/registry_cli.html#bx_cr_image_list) List your container images. | Reader, Manager |
| `container-registry.image.pull` | `docker pull` Pull the image. | Reader, Writer, Manager |
| `container-registry.image.push` | <ul><li>`docker push` Push the image.</li><li>[`ibmcloud cr ppa-archive-load`](/docs/services/Registry/registry_cli.html#bx_cr_ppa_archive_load) Imports IBM software that is downloaded from [IBM Passport Advantage Online for customers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/passportadvantage/pao_customer.html) and packaged for use with Helm into your private registry namespace.</li></ul>| Writer, Manager |
| `container-registry.image.vulnerabilities` | [`ibmcloud cr vulnerability-assessment`](/docs/services/Registry/registry_cli.html#bx_cr_va) View a vulnerability assessment report for your image. | Reader, Manager |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_add) Add a namespace. | Writer, Manager |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_rm) Remove a namespace. | Writer, Manager |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_list) Display your namespaces. | Reader, Manager |
| `container-registry.signature.create` | `docker trust sign` Sign the image. | Writer, Manager |
| `container-registry.signature.delete` | `docker trust revoke` Delete the signature. | Writer, Manager |
| `container-registry.signature.get` | `docker trust inspect` Inspect the signature. | Reader, Manager |
{: caption="Table 5. Service actions and operations for using {{site.data.keyword.registrylong_notm}}" caption-side="top"}
