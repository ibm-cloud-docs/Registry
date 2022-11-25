---

copyright:
  years: 2018, 2022
lastupdated: "2022-11-25"

keywords: policies, role, access policies, platform management roles, service access roles, access roles, access, IAM access for IBM Cloud Container Registry, permissions for IBM Cloud Container Registry, iam for IBM Cloud Container Registry, roles for IBM Cloud Container Registry, actions for IBM Cloud Container Registry, assigning access for IBM Cloud Container Registry, manager, reader, writer, actions, access group

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Managing IAM access for {{site.data.keyword.registryshort_notm}}
{: #iam}

Access to {{site.data.keyword.registrylong}} for users in your account is controlled by {{site.data.keyword.iamlong}} (IAM).
{: shortdesc}

Every user that accesses the {{site.data.keyword.registrylong_notm}} service in your account must be assigned an IAM [access policy](x2853407){: term} with an IAM role. A user can also be a member of an [access group](/docs/account?topic=account-groups) with assigned IAM access policies that grant an IAM role. Review the following roles, actions, and more to help determine the best way to assign access to {{site.data.keyword.registryshort}}.

The IAM access policy that you assign to users in your account determines the actions that a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by {{site.data.keyword.registryshort}} as operations that are allowed to be performed on the service. Each action is mapped to an [IAM platform or service role](/docs/account?topic=account-userroles) that you can assign to a user.

If a specific role and its actions don't fit the use case that you're looking to address, you can [create a custom role](/docs/account?topic=account-custom-roles#custom-access-roles) and pick the actions to include.
{: tip}

IAM access policies are enforced only when you use IAM to log in to {{site.data.keyword.registryshort}}. If you want to restrict user access to one or more [namespaces](x2031005){: term} for an ID that you are using for automation, use an IAM service ID. For more information about service IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids#serviceids).

From version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, you can set permissions so that you can configure access to resources within a namespace at the [resource group](x2161955){: term} level. For more information, see [User permissions for working with namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan_perm).

For more information about IAM, see [How {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} works](/docs/account?topic=account-iamoverview#iamoverview).

For more information about enabling policies for {{site.data.keyword.registryshort}}, see [Defining IAM access policies](/docs/Registry?topic=Registry-user#user).

Policies enable access to be granted at different levels. Some options include the following access levels:

- Access to the service in your account
- Access to a specific resource within the service
- Access to all IAM-enabled services in your account
- Access to resources within a resource group

After you define the scope of the IAM access policy, you assign a role.

Review the following tables that outline the actions that each role allows within the {{site.data.keyword.registryshort}} service. Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access to the service, create or delete instances, and bind instances to applications. Service access roles enable users access to {{site.data.keyword.registryshort}} and the ability to call the {{site.data.keyword.registryshort}} API. For more information about the exact actions that are mapped to each role, see [IAM roles and actions for {{site.data.keyword.registryshort}}](/docs/account?topic=account-iam-service-roles-actions#container-registry).

For more information about assigning user roles in the UI, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

Try out the tutorial [Granting access to {{site.data.keyword.registryshort}} resources tutorial](/docs/Registry?topic=Registry-iam_access#iam_access).
{: tip}

## Context-based restrictions
{: #iam_cbr}

{{site.data.keyword.registryshort}} also supports context-based restrictions. You can use context-based restrictions to define and enforce access restrictions for {{site.data.keyword.cloud_notm}} resources based on the network location of access requests. These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. 

For more information, see [What are context-based restrictions?](/docs/account?topic=account-context-restrictions-whatis).

For an example of how to set up context-based restrictions, see the context-based restrictions tutorial [Leveraging context-based restrictions to secure your resources](/docs/account?topic=account-context-restrictions-tutorial).

When you set up context-based restrictions, the restrictions apply to everything for the selected service in the account unless you select a subset of resources. To set up your own context-based restrictions for {{site.data.keyword.registryshort_notm}}, when you're creating a rule, in the **Select your resources** section, select **Container Registry**. {{site.data.keyword.registryshort}} supports the following subset of resources: `resource type = namespace` and `resource id = YOUR_IMAGE_NAMESPACE`, where `YOUR_IMAGE_NAMESPACE` is the namespace of your image.

## Platform management roles
{: #platform_management_roles}

The following table details actions that are mapped to platform management roles. Platform management roles enable users to perform tasks on service resources at the platform level, for example assign user access for the service, and create or delete service IDs.

| Platform management roles | Description of actions | Example actions |
|--------------------------|------------------------|-----------------|
| Viewer | Not supported | |
| Editor | Not supported | |
| Operator | Not supported | |
| Administrator | Configure access for other users.  \n  \n Apply pull secrets to clusters. | For more information about assigning user roles in the UI, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).  \n  \n To create clusters in {{site.data.keyword.containerlong_notm}} that have pull secrets to access images in {{site.data.keyword.registryshort}}, you must have the Administrator role. To use the [`ibmcloud ks cluster pull-secret apply`](/docs/containers?topic=containers-kubernetes-service-cli#cs_cluster_pull_secret_apply) command to configure the pull secrets for an existing cluster, you must have the Administrator role. For more information, see [Preparing to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare). |
{: caption="Table 1. IAM user roles and actions" caption-side="bottom"}

## Service access roles
{: #service_access_roles}

The following table details actions that are mapped to service access roles. Service access roles give users access to {{site.data.keyword.registryshort}} as well as the ability to call the {{site.data.keyword.registryshort}} API.

| Service access role | Description of actions | Example actions|
|---------------------|------------------------|----------------|
| Reader | The Reader role can view information. | View, inspect, and pull images.  \n  \n View and analyze namespaces.  \n  \n View quotas.  \n  \n View vulnerability reports.  \n  \n View image signatures.  \n  \n View retention policies.  \n  \n View the contents of the trash.  \n  \n View the contents of the manifest for an image.  \n  \n List Vulnerability Advisor security exemption policies and types of security exemptions. |
| Writer | The Writer role can edit information. | Push, delete, and restore images.  \n  \n View quotas.  \n  \n Sign images.  \n  \n Set and run retention policies.  \n  \n Delete all untagged images in your {{site.data.keyword.registryshort}} account. |
| Manager | The Manager role can perform all actions. | View, inspect, pull, push, delete, and restore images.  \n  \n View, add, analyze, and remove namespaces.  \n  \n Assign namespaces to resource groups.  \n  \n View and set quotas.  \n  \n View vulnerability reports.  \n  \n View and create image signatures.  \n  \n Review and change pricing plans.  \n  \n Enable IAM access policy enforcement.  \n  \n List, add, and remove Vulnerability Advisor security issue exemption policies.  \n  \n List types of security exemptions.  \n  \n Set and run retention policies.  \n  \n View the contents of the trash.  \n  \n Restore images.  \n  \n  View the contents of the manifest for an image.  \n  \n Prevent or allow image pulls or pushes over public network connections for your account.  \n  \n Check whether the use of public connections is prevented for image pushes or pulls in your account.  \n  \n Delete all untagged images in your {{site.data.keyword.registryshort}} account. |
{: caption="Table 2. IAM service access roles and actions" caption-side="bottom"}

For the following {{site.data.keyword.registryshort}} commands, you must have at least one of the specified roles as shown in the following tables. To create a policy that allows access to {{site.data.keyword.registryshort}}, you must create a policy where the following criteria apply.

- The service name is `container-registry`.
- The service instance is empty.
- The region is the region that you want to grant access to, or is empty to give access to all regions.

### Access roles for configuring {{site.data.keyword.registryshort}}
{: #access_roles_configure}

To grant a user permission to configure {{site.data.keyword.registryshort}} in your account, you must create a policy that grants one or more of the roles in the following table. When you create your policy, you must not specify a `resource type` or `resource`. Policies for configuring {{site.data.keyword.registryshort}} must not be set at a resource group level.

For example, run the following `ibmcloud iam user-policy-create` command. Where `<user_email>` is the user's email address, `<region>` is the region, and `<roles>` is the role, or roles, that you want the user to have.

```txt
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <region> --roles <roles>
```
{: pre}

The following table details actions that are mapped to operations on the service and to the service access roles for configuring {{site.data.keyword.registryshort}}.

| Action | Operation on service | Role |
|--------|----------------------|------|
| `container-registry.auth.get` | [`ibmcloud cr private-only`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only) Check whether the use of public connections is prevented for image pushes or pulls in your account. | Manager |
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) Enable IAM access policy enforcement.  \n  \n [`ibmcloud cr private-only`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only) Prevent or allow image pulls or pushes over public network connections for your account. | Manager |
| `container-registry.exemption.list` | [`ibmcloud cr exemption-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list) List your Vulnerability Advisor exemption policies for security issues.  \n  \n [`ibmcloud cr exemption-types`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types) List the types of security issues that you can exempt. | Reader, Manager |
| `container-registry.exemption.manager` | [`ibmcloud cr exemption-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add) Create a Vulnerability Advisor exemption policy for a security issue.  \n  \n [`ibmcloud cr exemption-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm) Delete a Vulnerability Advisor exemption policy for a security issue. | Manager |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add) Create a namespace.  \n  \n [`ibmcloud cr namespace-assign`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_namespace_assign) Assign a namespace to a resource group. | Manager |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm) Remove a namespace. | Manager |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan) Display your pricing plan. | Manager |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade) Upgrade to the standard plan. | Manager |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota) Display your current quotas for traffic and storage, and usage information against those quotas. | Reader, Writer, Manager |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set) Modify the specified quota. | Manager |
| `container-registry.settings.get` | [`ibmcloud cr platform-metrics`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics) Get registry service settings for the targeted account, such as whether platform metrics are enabled. | Reader, Writer, Manager |
| `container-registry.settings.set` | [`ibmcloud cr platform-metrics`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics) Update registry service settings for the targeted account, such as enabling platform metrics. | Manager |
{: caption="Table 3. Service actions and operations for configuring {{site.data.keyword.registryshort}}" caption-side="bottom"}

### Access roles for using {{site.data.keyword.registryshort}}
{: #access_roles_using}

To grant a user permission to access {{site.data.keyword.registryshort}} content in your account, you must create a policy that grants one or more of the roles in the following table. When you create your policy, you can restrict access to a specific namespace by specifying the resource type `namespace` and the namespace name as the resource. If you don't specify a `resource-type` and a `resource`, the policy grants access to all resources in the account. Alternatively, if your namespace is within a resource group, permission can be granted by using an IAM access policy on that resource group.

For example, use the following command to create a user policy. Where `<user_email>` is the user's email address, `<region>` is the region, `<roles>` is the role, or roles, that you want the user to have, and `<namespace_name>` is the name of the namespace.

```txt
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <region> --roles <roles> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

The following table details actions that are mapped to operations on the service and to the service access roles for using {{site.data.keyword.registryshort}}.

| Action | Operation on service | Role | Status |
|--------|----------------------|------|--------|
| `container-registry.image.delete` | `docker trust revoke` Delete the signature for a container image.  \n  \n [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged) Delete all untagged images in your {{site.data.keyword.registryshort}} account.  \n  \n [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) Delete one or more container images.  \n  \n [`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) Remove a tag, or tags, from each specified container image in {{site.data.keyword.registryshort}}.  \n  \n [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria.  \n  \n [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) Clean up your namespaces by retaining only container images that meet your criteria. | Writer, Manager  \n  \n To run `ibmcloud cr retention-run` and `ibmcloud cr retention-policy-set` you must have Manager, or both Reader and Writer. | |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) Display details about a specific container image.  \n  \n [`ibmcloud cr manifest-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect) View the contents of the manifest for an image. | Reader, Manager | |
| `container-registry.image.list` | [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) List all your container images, including untagged images.  \n  \n [`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) List your tagged container images.  \n  \n [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged) Delete all untagged images in your {{site.data.keyword.registryshort}} account.  \n  \n [`ibmcloud cr trash-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list) Display the container images that are in the trash. | Reader, Manager | |
| `container-registry.image.pull` | `docker pull` Pull a container image.  \n  \n `docker trust inspect` Inspect the signature for a container image.  \n  \n [`ibmcloud cr image-tag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) Create a container image that refers to a source image.  \n  \n [`ibmcloud cr vulnerability-assessment`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va) View a vulnerability assessment report for your container image. | Reader, Writer, Manager | |
| `container-registry.image.push` | `docker push` Push a container image.  \n  \n `docker trust sign` Sign a container image.  \n  \n [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) Restore a deleted container image from the trash.  \n  \n [`ibmcloud cr image-tag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) Create a container image that refers to a source image. | Writer, Manager | |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list) List your namespaces. | Reader, Manager | |
| `container-registry.retention.analyze` | [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria.  \n  \n [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) Clean up your namespaces by retaining only container images that meet your criteria. | Reader, Manager  \n  \n To run `ibmcloud cr retention-run` and `ibmcloud cr retention-policy-set` you must have Manager, or both Reader and Writer. | |
| `container-registry.retention.get` | View the image retention policy for a namespace by using the API, see [{{site.data.keyword.registrylong_notm}} API](/apidocs/container-registry). | Reader, Manager | |
| `container-registry.retention.set` | [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) Set a policy to clean up your namespaces by retaining only container images that meet your criteria. | Writer, Manager | |
| `container-registry.retention.list` | [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list) List the image retention policies for your account. | Reader, Manager | |
{: caption="Table 4. Service actions and operations for using {{site.data.keyword.registryshort}}" caption-side="bottom"}

## Assigning access to {{site.data.keyword.registryshort}} in the console
{: #registry_iam_assign-access-console}
{: ui}

You can use one of the following options to assign access in the console:

- Access policies per user. You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For more information about the steps to assign IAM access, see [Managing access to resources](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console).
- Access groups. Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as required from the group to control their access. You manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag).

## Assigning access to {{site.data.keyword.registryshort}} in the CLI
{: #registry_iam_assign-access-cli}
{: cli}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the CLI](/docs/account?topic=account-assign-access-resources&interface=cli#access-resources-cli). The following example shows a command for assigning the `Manager` role for {{site.data.keyword.registryshort}}:

Use `container-registry` for the service name.
{: tip}

```bash
ibmcloud iam user-policy-create <user@example.com> --service-name container-registry --roles Manager
```
{: pre}

## Assigning access to {{site.data.keyword.registryshort}} by using the API
{: #registry_iam_assign-access-api}
{: api}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the API](/docs/account?topic=account-assign-access-resources&interface=api#access-resources-api) or [Create a policy](/apidocs/iam-policy-management#create-policy) in the API docs. Role cloud resource names (CRN) in the following table are used to assign access with the API.

| Role name | Role CRN |
|-----------|----------|
| Administrator  | `crn:v1:bluemix:public:container-registry::::serviceRole:Administrator` |
| Reader         | `crn:v1:bluemix:public:container-registry::::serviceRole:Reader`        |
| Writer         | `crn:v1:bluemix:public:container-registry::::serviceRole:Writer`        |
| Manager        | `crn:v1:bluemix:public:container-registry::::serviceRole:Manager`       |
{: caption="Table 5. Role ID values for API use" caption-side="bottom"}

The following example is for assigning the `Manager` role for {{site.data.keyword.registryshort}}:

Use `container-registry` for the service name, and refer to the Role ID values table to ensure that you're using the correct value for the CRN.
{: tip}

```curl 
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{
  "type": "access",
  "description": "Manager role for Container Registry",
  "subjects": [
    {
      "attributes": [
        {
          "name": "iam_id",
          "value": "IBMid-123453user"
        }
      ]
    }'
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:container-registry::::serviceRole:Manager"
    }
  ],
  "resources":[
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "$ACCOUNT_ID"
        },
        {
          "name": "serviceName",
          "value": "container-registry"
        }
      ]
    }
  ]
}
```
{: curl}
{: codeblock}

```java
SubjectAttribute subjectAttribute = new SubjectAttribute.Builder()
      .name("iam_id")
      .value("IBMid-123453user")
      .build();

PolicySubject policySubjects = new PolicySubject.Builder()
      .addAttributes(subjectAttribute)
      .build();

PolicyRole policyRoles = new PolicyRole.Builder()
      .roleId("crn:v1:bluemix:public:container-registry::::serviceRole:Manager")
      .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
      .name("accountId")
      .value("ACCOUNT_ID")
      .operator("stringEquals")
      .build();

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
      .name("serviceName")
      .value("container-registry")
      .operator("stringEquals")
      .build();

PolicyResource policyResources = new PolicyResource.Builder()
      .addAttributes(accountIdResourceAttribute)
      .addAttributes(serviceNameResourceAttribute)
      .build();

CreatePolicyOptions options = new CreatePolicyOptions.Builder()
      .type("access")
      .subjects(Arrays.asList(policySubjects))
      .roles(Arrays.asList(policyRoles))
      .resources(Arrays.asList(policyResources))
      .build();

Response<Policy> response = service.createPolicy(options).execute();
Policy policy = response.getResult();

System.out.println(policy);
```
{: java}
{: codeblock}
   
```javascript
const policySubjects = [
  {
    attributes: [
      {
        name: 'iam_id',
        value: 'IBMid-123453user',
      },
    ],
  },
];
const policyRoles = [
  {
    role_id: 'crn:v1:bluemix:public:container-registry::::serviceRole:Manager',
  },
];
const accountIdResourceAttribute = {
  name: 'accountId',
  value: 'ACCOUNT_ID',
  operator: 'stringEquals',
};
const serviceNameResourceAttribute = {
  name: 'serviceName',
  value: 'container-registry',
  operator: 'stringEquals',
};
const policyResources = [
  {
    attributes: [accountIdResourceAttribute, serviceNameResourceAttribute]
  },
];
const params = {
  type: 'access',
  subjects: policySubjects,
  roles: policyRoles,
  resources: policyResources,
};

iamPolicyManagementService.createPolicy(params)
  .then(res => {
    examplePolicyId = res.result.id;
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
policy_subjects = PolicySubject(
  attributes=[SubjectAttribute(name='iam_id', value='IBMid-123453user')])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:container-registry::::serviceRole:Manager')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value='ACCOUNT_ID')
service_name_resource_attribute = ResourceAttribute(
  name='serviceName', value='container-registry')
policy_resources = PolicyResource(
  attributes=[account_id_resource_attribute,
        service_name_resource_attribute])

policy = iam_policy_management_service.create_policy(
  type='access',
  subjects=[policy_subjects],
  roles=[policy_roles],
  resources=[policy_resources]
).get_result()

print(json.dumps(policy, indent=2))
```
{: python}
{: codeblock}

```go
subjectAttribute := &iampolicymanagementv1.SubjectAttribute{
  Name:  core.StringPtr("iam_id"),
  Value: core.StringPtr("IBMid-123453user"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
  Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
  RoleID: core.StringPtr("crn:v1:bluemix:public:container-registry::::serviceRole:Manager"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("accountId"),
  Value:    core.StringPtr("ACCOUNT_ID"),
  Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceName"),
  Value:    core.StringPtr("container-registry"),
  Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
  Attributes: []iampolicymanagementv1.ResourceAttribute{
    *accountIDResourceAttribute, *serviceNameResourceAttribute}
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
  "access",
  []iampolicymanagementv1.PolicySubject{*policySubjects},
  []iampolicymanagementv1.PolicyRole{*policyRoles},
  []iampolicymanagementv1.PolicyResource{*policyResources},
)

policy, response, err := iamPolicyManagementService.CreatePolicy(options)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(policy, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}

## Assigning access to {{site.data.keyword.registryshort}} by using Terraform
{: #registry_iam_assign-access-terraform}
{: terraform}

The following example is for assigning the `Manager` role for {{site.data.keyword.registryshort}}:

Use `container-registry` for the service name.
{: tip}

```terraform
resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@example.com"
  roles  = ["Manager"]

  resources {
    service = "container-registry"
  }
}
```
{: codeblock}

For more information, see [ibm_iam_user_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_policy){: external} in the Terraform documentation.



