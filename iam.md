---

copyright:
  years: 2018, 2021
lastupdated: "2021-05-04"

keywords: user access, policies, user roles, access policies, platform management roles, service access roles, access roles, access management, IAM access for IBM Cloud Container Registry, permissions for IBM Cloud Container Registry, identity and access management for IBM Cloud Container Registry, roles for IBM Cloud Container Registry, actions for IBM Cloud Container Registry, assigning access for IBM Cloud Container Registry,

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

# Managing access for {{site.data.keyword.registryshort_notm}}
{: #iam}

Access to {{site.data.keyword.registrylong}} for users in your account is controlled by {{site.data.keyword.iamlong}} (IAM).
{: shortdesc}

When IAM policies are enabled for your account in {{site.data.keyword.registrylong_notm}}, every user that accesses the {{site.data.keyword.registrylong_notm}} service in your account must be assigned an access policy with an IAM user role defined. That policy determines what role the user has within the context of the service, and what actions the user can perform. Each action in {{site.data.keyword.registrylong_notm}} is mapped to one or more [IAM access](/docs/account?topic=account-userroles) user roles.

IAM policies are enforced only when you use IAM to log in to {{site.data.keyword.registrylong_notm}}. If you log in to {{site.data.keyword.registrylong_notm}} by using another method, such as a registry token (deprecated), your policies are not enforced. If you want to restrict access to one or more namespaces for an ID that you are using for automation, use an IAM service ID instead of a registry token. For more information about service IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids#serviceids).

From version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, you can set permissions so that you can configure access to resources within a namespace at the [resource group](/docs/account?topic=account-rgs) level. For more information, see [User permissions for working with namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan_perm).

If you started to use {{site.data.keyword.registrylong_notm}} before 4 October 2018, you must enable policy enforcement for each region so that you can use {{site.data.keyword.iamlong}} (IAM) access role policies to manage access to the {{site.data.keyword.registrylong_notm}} service. If you do not enable this policy, any user in the account can manage registry resources. For more information, see [Enabling policy enforcement for existing users](/docs/Registry?topic=Registry-user#existing_users).
{: tip}

Using {{site.data.keyword.registrylong_notm}} tokens is deprecated.
{: deprecated}

For more information about IAM, see [What is {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}?](/docs/account?topic=account-iamoverview#iamoverview)

For more information about enabling policies for {{site.data.keyword.registrylong_notm}}, see [Defining user access role policies](/docs/Registry?topic=Registry-user#user).

Policies enable access to be granted at different levels. Some of the options include the following access levels:

* Access to the service in your account
* Access to a specific resource within the service
* Access to all IAM-enabled services in your account
* Access to resources within a resource group

After you define the scope of the access policy, you assign a role. Review the following tables that outline what actions each role allows within the {{site.data.keyword.registrylong_notm}} service.

For more information about assigning user roles in the UI, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

Try out the tutorial [Tutorial: Granting access to {{site.data.keyword.registrylong_notm}} resources](/docs/Registry?topic=Registry-iam_access#iam_access).
{: tip}

## Platform management roles
{: #platform_management_roles}

The following table details actions that are mapped to platform management roles. Platform management roles enable users to perform tasks on service resources at the platform level, for example assign user access for the service, and create or delete service IDs.

| Platform management role | Description of actions | Example actions |
|-----------------|-----------------|-----------------|
| Viewer | Not supported | |
| Editor | Not supported | |
| Operator | Not supported | |
| Administrator | Configure access for other users.<br/><br/>Configure registry tokens (deprecated).<br/><br/>Apply pull secrets to clusters. | For more information about assigning user roles in the UI, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).<br/><br/>List, retrieve, and remove registry tokens (deprecated).<br/><br/>To create clusters in {{site.data.keyword.containerlong_notm}} that have pull secrets to access images in {{site.data.keyword.registrylong_notm}}, you must have the Administrator role. To use the [`ibmcloud ks cluster pull-secret-apply`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_pull_secret_apply) command to configure pull secrets for an existing cluster, you must have the Administrator role. For more information, see [Preparing to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare). |
{: caption="Table 1. IAM user roles and actions" caption-side="top"}

Using {{site.data.keyword.registrylong_notm}} tokens is deprecated.
{: deprecated}

For {{site.data.keyword.registrylong_notm}}, the following actions exist:

| Action| Operation on service | Role | Status |
|-----------------|-----------------|--------------|
| `container-registry.registrytoken.delete` | [`ibmcloud cr token-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_rm) Remove one or more specified tokens. | Administrator | Deprecated |
| `container-registry.registrytoken.get` | [`ibmcloud cr token-get`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_get) Retrieve the specified token from the registry. | Administrator | Deprecated |
| `container-registry.registrytoken.list` | [`ibmcloud cr token-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_list) Display all tokens that exist for your {{site.data.keyword.cloud_notm}} account. | Administrator | Deprecated |
{: caption="Table 2. Platform actions and operations for configuring {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Service access roles
{: #service_access_roles}

The following table details actions that are mapped to service access roles. Service access roles enable users access to {{site.data.keyword.registrylong_notm}} as well as the ability to call the {{site.data.keyword.registrylong_notm}} API.

| Service access role | Description of actions | Example actions|
|-----------------|-----------------|-----------------|
| Reader | The Reader role can view information. | View, inspect, and pull images.<br/><br/>View and analyze namespaces.<br/><br/>View quotas.<br/><br/>View vulnerability reports.<br/><br/>View image signatures.<br/><br/>View retention policies.<br/><br/>View the contents of the trash. <br/><br/> View the contents of the manifest for an image.<br/><br/>List Vulnerability Advisor security exemption policies and types of security exemptions. |
| Writer | The Writer role can edit information. | Build, push, delete, and restore images.<br/><br/>View quotas.<br/><br/>Sign images.<br/><br/>Set and run retention policies.<br/><br/>Delete all untagged images in your {{site.data.keyword.registrylong_notm}} account. |
| Manager | The Manager role can perform all actions. | View, inspect, pull, build, push, delete, and restore images.<br/><br/>View, add, analyze, and remove namespaces.<br/><br/>Assign namespaces to resource groups.<br/><br/>View and set quotas.<br/><br/>View vulnerability reports.<br/><br/>View and create image signatures.<br/><br/>Review and change pricing plans.<br/><br/>Enable IAM policy enforcement.<br/><br/>List, add, and remove Vulnerability Advisor security issue exemption policies.<br/><br/>List types of security exemptions<br/><br/>Set and run retention policies.<br/><br/>View the contents of the trash.<br/><br/>Restore images.<br/><br/> View the contents of the manifest for an image.<br/><br/>Prevent or allow image pulls or pushes over public network connections for your account.<br/><br/>Check whether the use of public connections is prevented for image pushes or pulls in your account.<br/><br/>Delete all untagged images in your {{site.data.keyword.registrylong_notm}} account. |
{: caption="Table 3. IAM service access roles and actions" caption-side="top"}

For the following {{site.data.keyword.registrylong_notm}} commands, you must have at least one of the specified roles as shown in the following tables. To create a policy that allows access to {{site.data.keyword.registrylong_notm}}, you must create a policy where the following criteria apply.

* The service name is `container-registry`.
* The service instance is empty.
* The region is the region that you want to grant access to, or is empty to give access to all regions.

### Access roles for configuring {{site.data.keyword.registrylong_notm}}
{: #access_roles_configure}

To grant a user permission to configure your {{site.data.keyword.registrylong_notm}} in your account, you must create a policy that grants one or more of the roles in the following table. When you create your policy, you must not specify a `resource type` or `resource`. Policies for configuring {{site.data.keyword.registrylong_notm}} must not be set at a resource group level.

For example, run the following `ibmcloud iam user-policy-create` command. Where `<user_email>` is the user's email address, `<region>` is the region, and `<roles>` is the role, or roles, that you want the user to have.

```
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <region> --roles <roles>
```
{: pre}

The following table details actions that are mapped to operations on the service and to the service access roles for configuring {{site.data.keyword.registrylong_notm}}.

| Action | Operation on service | Role |
|-----------------------|---------------------|--------------|
| `container-registry.auth.get` | [`ibmcloud cr private-only`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only) Check whether the use of public connections is prevented for image pushes or pulls in your account. | Manager |
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) Enable IAM policy enforcement.<br/><br/>[`ibmcloud cr private-only`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only) Prevent or allow image pulls or pushes over public network connections for your account. | Manager |
| `container-registry.exemption.list` | [`ibmcloud cr exemption-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list) List your Vulnerability Advisor exemption policies for security issues.<br/><br/>[`ibmcloud cr exemption-types`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types) List the types of security issues that you can exempt. | Reader, Manager |
| `container-registry.exemption.manager` | [`ibmcloud cr exemption-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add) Create a Vulnerability Advisor exemption policy for a security issue.<br/><br/>[`ibmcloud cr exemption-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm) Delete a Vulnerability Advisor exemption policy for a security issue. | Manager |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add) Create a namespace.<br/><br/>[`ibmcloud cr namespace-assign`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_namespace_assign) Assign a namespace to a resource group. | Manager |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm) Remove a namespace. | Manager |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan) Display your pricing plan. | Manager |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade) Upgrade to the standard plan. | Manager |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota) Display your current quotas for traffic and storage, and usage information against those quotas. | Reader, Writer, Manager |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set) Modify the specified quota. | Manager |
| `container-registry.settings.get` | [`ibmcloud cr platform-metrics`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics) Get registry service settings for the targeted account, such as whether platform metrics are enabled. | Reader, Writer, Manager |
| `container-registry.settings.set` | [`ibmcloud cr platform-metrics`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics) Update registry service settings for the targeted account, such as enabling platform metrics. | Manager |
{: caption="Table 4. Service actions and operations for configuring {{site.data.keyword.registrylong_notm}}" caption-side="top"}

### Access roles for using {{site.data.keyword.registrylong_notm}}
{: #access_roles_using}

To grant a user permission to access {{site.data.keyword.registrylong_notm}} content in your account, you must create a policy that grants one or more of the roles in the following table. When you create your policy, you can restrict access to a specific namespace by specifying the resource type `namespace` and the namespace name as the resource. If you don't specify a `resource-type` and a `resource`, the policy grants access to all resources in the account. Alternatively, if your namespace is within a resource group, permission can be granted by using an access policy on that resource group.

For example, use the following command, where `<user_email>` is the user's email address, `<region>` is the region, `<roles>` is the role, or roles, that you want the user to have, and `<namespace_name>` is the name of the namespace:

```
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <region> --roles <roles> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

The following table details actions that are mapped to operations on the service and to the service access roles for using {{site.data.keyword.registrylong_notm}}.

The [`ibmcloud cr build`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) command is deprecated from 6 October 2020. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead. For more information, see the [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecating-container-builds){: external} blog post.
{: deprecated}

| Action | Operation on service | Role | Status |
|---------------------|-------------------|-----------|-----------|
| `container-registry.image.build` | [`ibmcloud cr build`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) Build a container image. | Writer, Manager | Deprecated |
| `container-registry.image.delete` | `docker trust revoke` Delete the signature for a container image.<br/><br/>[`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged) Delete all untagged images in your {{site.data.keyword.registrylong_notm}} account.<br/><br/>[`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) Delete one or more container images.<br/><br/>[`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) Remove a tag, or tags, from each specified container image in {{site.data.keyword.registrylong_notm}}.<br/><br/>[`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria.<br/><br/>[`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) Clean up your namespaces by retaining only container images that meet your criteria. | Writer, Manager<br/><br/>To run `ibmcloud cr retention-run` and `ibmcloud cr retention-policy-set` you must have Manager, or  both Reader and Writer. | |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) Display details about a specific container image. <br/><br/>[`ibmcloud cr manifest-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect) View the contents of the manifest for an image. | Reader, Manager | |
| `container-registry.image.list` | [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) List all your container images, including untagged images.<br/><br/>[`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) List your tagged container images.<br/><br/>[`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged) Delete all untagged images in your {{site.data.keyword.registrylong_notm}} account.<br/><br/>[`ibmcloud cr trash-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list) Display the container images that are in the trash. | Reader, Manager | |
| `container-registry.image.pull` | `docker pull` Pull a container image.<br/><br/>`docker trust inspect` Inspect the signature for a container image.<br/><br/>[`ibmcloud cr image-tag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) Create a new container image that refers to a source image.<br/><br/> [`ibmcloud cr vulnerability-assessment`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va) View a vulnerability assessment report for your container image. | Reader, Writer, Manager | |
| `container-registry.image.push` | `docker push` Push a container image.<br/><br/>`docker trust sign` Sign a container image.<br/><br/>[`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) Restore a deleted container image from the trash.<br/><br/>[`ibmcloud cr image-tag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) Create a new container image that refers to a source image. | Writer, Manager | |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list) List your namespaces. | Reader, Manager | |
| `container-registry.retention.analyze` | [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria.<br/><br/>[`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) Clean up your namespaces by retaining only container images that meet your criteria. | Reader, Manager<br/><br/>To run `ibmcloud cr retention-run` and `ibmcloud cr retention-policy-set` you must have Manager, or both Reader and Writer. | |
| `container-registry.retention.get` | View the image retention policy for a namespace by using the API, see [{{site.data.keyword.registrylong_notm}} API](https://{DomainName}/apidocs/container-registry). | Reader, Manager | |
| `container-registry.retention.set` | [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria. | Writer, Manager | |
| `container-registry.retention.list` | [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list) List the image retention policies for your account. | Reader, Manager | |
{: caption="Table 5. Service actions and operations for using {{site.data.keyword.registrylong_notm}}" caption-side="top"}
