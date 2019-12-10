---

copyright:
  years: 2018, 2019
lastupdated: "2019-12-10"

keywords: user access, policies, user roles, access policies, platform management roles, service access roles, access roles, access management,

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
{:term: .term}

# Managing user access with Identity and Access Management
{: #iam}

Access to {{site.data.keyword.registrylong}} for users in your account is controlled by {{site.data.keyword.iamlong}} (IAM).
{: shortdesc}

When IAM policies are enabled for your account in {{site.data.keyword.registrylong_notm}}, every user that accesses the {{site.data.keyword.registrylong_notm}} service in your account must be assigned an access policy with an IAM user role defined. That policy determines what role the user has within the context of the service, and what actions the user can perform. Each action in {{site.data.keyword.registrylong_notm}} is mapped to one or more [IAM user roles](/docs/iam?topic=iam-userroles).

IAM policies are enforced only when you use IAM to log in to {{site.data.keyword.registrylong_notm}}. If you log in to {{site.data.keyword.registrylong_notm}} by using another method, such as a registry token (deprecated), your policies are not enforced. If you want to restrict access to one or more namespaces for an ID that you are using for automation, use an IAM service ID instead of a registry token. For more information about service IDs, see [Creating and working with service IDs](/docs/iam?topic=iam-serviceids#serviceids).

For more information about IAM, see [What is {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}?](/docs/iam?topic=iam-iamoverview#iamoverview).

For information about enabling policies for {{site.data.keyword.registrylong_notm}}, see [Defining user access role policies](/docs/services/Registry?topic=registry-user#user).

Policies enable access to be granted at different levels. Some of the options include the following access levels:

* Access to the service in your account
* Access to a specific resource within the service
* Access to all IAM-enabled services in your account

After you define the scope of the access policy, you assign a role. Review the following tables that outline what actions each role allows within the {{site.data.keyword.registrylong_notm}} service.

For information about assigning user roles in the UI, see [Managing IAM access](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

Try out the tutorial [Tutorial: Granting access to {{site.data.keyword.registrylong_notm}} resources](/docs/services/Registry?topic=registry-iam_access#iam_access).
{: tip}

## Platform management roles
{: #platform_management_roles}

The following table details actions that are mapped to platform management roles. Platform management roles enable users to perform tasks on service resources at the platform level, for example assign user access for the service, and create or delete service IDs.

| Platform management role | Description of actions | Example actions |
|-----------------|-----------------|-----------------|
| Viewer | Not supported | |
| Editor | Not supported | |
| Operator | Not supported | |
| Administrator | Configure access for other users</br></br>Configure registry tokens (deprecated)</br></br>Create clusters | For information about assigning user roles in the UI, see [Managing IAM access](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).</br></br>List, retrieve, and remove registry tokens (deprecated)</br></br>To create clusters in {{site.data.keyword.containerlong_notm}}, you must assign the Administrator role for {{site.data.keyword.registrylong_notm}} to the user, see [Preparing to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare). |
{: caption="Table 1. IAM user roles and actions" caption-side="top"}

For {{site.data.keyword.registrylong_notm}}, the following actions exist:

| Action| Operation on service | Role | Status |
|-----------------|-----------------|--------------|
| `container-registry.registrytoken.delete` | [`ibmcloud cr token-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_rm) Remove one or more specified tokens. | Administrator | Deprecated |
| `container-registry.registrytoken.get` | [`ibmcloud cr token-get`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_get) Retrieve the specified token from the registry. | Administrator | Deprecated |
| `container-registry.registrytoken.list` | [`ibmcloud cr token-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_list) Display all tokens that exist for your {{site.data.keyword.cloud_notm}} account. | Administrator | Deprecated |
{: caption="Table 2. Platform actions and operations for configuring {{site.data.keyword.registrylong_notm}}" caption-side="top"}

Using {{site.data.keyword.registrylong_notm}} tokens is deprecated.
{: deprecated}

## Service access roles
{: #service_access_roles}

The following table details actions that are mapped to service access roles. Service access roles enable users access to {{site.data.keyword.registrylong_notm}} as well as the ability to call the {{site.data.keyword.registrylong_notm}} API.

| Service access role | Description of actions | Example actions|
|-----------------|-----------------|-----------------|
| Reader | The Reader role can view information. | View, inspect, and pull images.</br></br>View namespaces.</br></br>View quotas.</br></br>View vulnerability reports.</br></br>View image signatures.</br></br>View retention policies.</br></br>Clean up your namespaces by retaining only images that meet your criteria. (You must also have the Writer role.)</br></br>View the contents of the trash. </br></br> View the contents of the manifest for an image. |
| Writer | The Writer role can edit information. | Build, push, delete, and restore images.</br></br>View quotas.</br></br>Sign images.</br></br>Add and remove namespaces.</br></br>Clean up your namespaces by retaining only images that meet your criteria. (You must also have the Reader role.)</br></br>Set retention policies. |
| Manager | The Manager role can perform all actions. | View, inspect, pull, build, push, delete, and restore images.</br></br>View, add, and remove namespaces.</br></br>View and set quotas.</br></br>View vulnerability reports.</br></br>View and create image signatures.</br></br>Review and change pricing plans.</br></br>Enable IAM policy enforcement.</br></br>Manage Vulnerability Advisor exemptions.</br></br>Clean up your namespaces by retaining only images that meet your criteria.</br></br>Set retention policies.</br></br>View the contents of the trash.</br></br>Restore images.</br></br> View the contents of the manifest for an image. |
{: caption="Table 3. IAM service access roles and actions" caption-side="top"}

 For the following {{site.data.keyword.registrylong_notm}} commands, you must have at least one of the specified roles as shown in the following tables. To create a policy that allows access to {{site.data.keyword.registrylong_notm}} you must create a policy where the service name is `container-registry`, the service instance is empty, and the region is the region that you want to grant access to, or empty to give access to all regions.

### Access roles for configuring {{site.data.keyword.registrylong_notm}}
{: #access_roles_configure}

To grant a user permission to configure your {{site.data.keyword.registrylong_notm}} in your account, you must create a policy that grants one or more of the roles in the following table. When creating your policy, you must not specify a `resource type` or `resource`.

For example, use the following command, where `<user_email>` is the user's email address:

```
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

| Action| Operation on service | Role |
|-----------------|-----------------|--------------|
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) Enable IAM policy enforcement. | Manager |
| `container-registry.exemption.manager` | [`ibmcloud cr exemption-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add) Create an exemption for a security issue.</br></br>[`ibmcloud cr exemption-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list) List your exemptions for security issues.</br></br>[`ibmcloud cr exemption-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm) Delete an exemption for a security issue.</br></br>[`ibmcloud cr exemption-types`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types) List the types of security issues that you can exempt. | Manager |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan) Display your pricing plan. | Manager |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade) Upgrade to the standard plan. | Manager |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota) Display your current quotas for traffic and storage, and usage information against those quotas. | Reader, Writer, Manager |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set) Modify the specified quota. | Manager |
{: caption="Table 4. Service actions and operations for configuring {{site.data.keyword.registrylong_notm}}" caption-side="top"}

### Access roles for using {{site.data.keyword.registrylong_notm}}
{: #access_roles_using}

To grant a user permission to access {{site.data.keyword.registrylong_notm}} content in your account you must create a policy that grants one or more of the roles in the following table. When creating your policy, you can restrict access to a specific namespace by specifying the resource type `namespace` and the namespace name as the resource. If you don't specify a `resource-type` and a `resource`, the policy grants access to all resource in the account.

You cannot organize and assign access to registry namespaces in resource groups.
{: note}

For example, use the following command, where `<user_email>` is the user's email address:

```
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Reader> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

| Action | Operation on service | Role |
|-----------------|-----------------|--------------|
| `container-registry.image.build` | [`ibmcloud cr build`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) Build a container image. | Writer, Manager |
| `container-registry.image.delete` | [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) Delete one or more container images.</br></br>[`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) Remove a tag, or tags, from each specified container image in {{site.data.keyword.registrylong_notm}}.</br></br>`docker trust revoke` Delete the signature for a container image.</br></br>[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) Clean up your namespaces by retaining only container images that meet your criteria.</br></br>[`ibmcloud cr retention-policy-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria. | Writer, Manager</br></br>To run `ibmcloud cr retention-run` and `ibmcloud cr retention-policy-set` you must have Manager, or  both Reader and Writer. |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) Display details about a specific container image. </br></br>[`ibmcloud cr manifest-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect) View the contents of the manifest for an image. | Reader, Manager |
| `container-registry.image.list` | [`ibmcloud cr image-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) List your container images.</br></br>[`ibmcloud cr trash-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list) Display the container images that are in the trash. | Reader, Manager |
| `container-registry.image.pull` | `docker pull` Pull a container image.</br></br>`docker trust inspect` Inspect the signature for a container image.</br></br>[`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) Create a new container image that refers to a source image. | Reader, Writer, Manager |
| `container-registry.image.push` | `docker push` Push a container image.</br></br>`docker trust sign` Sign a container image.</br></br>[`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load) Import IBM software that is downloaded from [IBM Passport Advantage Online ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/passportadvantage/pao_customer.html).</br></br>[`ibmcloud cr image-restore`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) Restore a deleted container image from the trash.</br></br>[`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) Create a new container image that refers to a source image. | Writer, Manager |
| `container-registry.image.vulnerabilities` | [`ibmcloud cr vulnerability-assessment`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va) View a vulnerability assessment report for your container image. | Reader, Manager |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add) Add a namespace. | Writer, Manager |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm) Remove a namespace. | Writer, Manager |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list) List your namespaces. | Reader, Manager |
| `container-registry.retention.analyze` | [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) Clean up your namespaces by retaining only container images that meet your criteria.</br></br>[`ibmcloud cr retention-policy-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria. | Reader, Manager</br></br>To run `ibmcloud cr retention-run` and `ibmcloud cr retention-policy-set` you must have Manager, or both Reader and Writer. |
| `container-registry.retention.get` | View the image retention policy for a namespace by using the API, see [{{site.data.keyword.registrylong_notm}} API](https://{DomainName}/apidocs/container-registry). | Reader, Manager |
| `container-registry.retention.set` | [`ibmcloud cr retention-policy-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria. | Writer, Manager |
| `container-registry.retention.list` | [`ibmcloud cr retention-policy-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list) List the image retention policies for your account. | Reader, Manager |
{: caption="Table 5. Service actions and operations for using {{site.data.keyword.registrylong_notm}}" caption-side="top"}
