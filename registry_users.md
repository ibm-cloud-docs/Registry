---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-24"

keywords: user access policies, access policies, policies, policy enforcement, user access, roles, account, users, resources, namespace

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}


# Defining IAM access policies for {{site.data.keyword.registryshort_notm}}
{: #user}

As an administrator, you can define {{site.data.keyword.iamlong}} (IAM) access policies to create different levels of access for different users in {{site.data.keyword.registrylong}}. For example, you can authorize some users to view quotas and other users to set quotas.
{: shortdesc}

You must define IAM [access policies](#x2853407){: term} for every user that works with {{site.data.keyword.registrylong_notm}}. The scope of an IAM access policy is based on the user's role or roles that determine the actions that they are allowed to do. Some roles are predefined, but custom roles can be defined.

To find out more about IAM access policies, see [{{site.data.keyword.cloud_notm}} IAM roles](/docs/account?topic=account-userroles).

You can assign {{site.data.keyword.registryshort}} namespaces to a [resource group](/docs/account?topic=account-rgs) and scope access policies to that group, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan). However, you can still define access policies that are scoped to individual {{site.data.keyword.registryshort}} namespaces or to all namespaces that are owned by the account.

## Creating policies
{: #create}
{: help}
{: support}

Before you begin, complete the following tasks:

- Decide on the roles that each user needs and on which resources in {{site.data.keyword.registrylong_notm}}, see [IAM roles](/docs/Registry?topic=Registry-iam#iam). You can create multiple policies, for example, you can grant write access on a resource but grant read access only on another resource. Policies are additive, which means that a global read policy and a resource-scoped write policy grants both read and write access on that resource.

- [Invite users to an account](/docs/account?topic=account-iamuserinv&interface=ui#invite-users-access).

    If you want users to create clusters in {{site.data.keyword.containerlong_notm}}, ensure that you assign the {{site.data.keyword.registrylong_notm}} Administrator role to those users, and don't assign a resource group. For more information, see [Preparing your account to create clusters](/docs/containers?topic=containers-clusters).
    {: tip}

To create policies for {{site.data.keyword.registrylong_notm}}, the service name field must be `container-registry`.

If you want to access resources, you must assign roles to users or service IDs. If you want to grant access to everything, don't specify a resource type or a resource. If you want to grant access to a specific namespace, specify the resource type as `namespace` and use the namespace name as the resource.

- To create a policy for users, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).
- To create a policy for service IDs, run the `ibmcloud iam service-policy-create` command or use the {{site.data.keyword.cloud_notm}} console to bind roles to your service IDs. To create policies, you must have the Administrator role. You automatically have the Administrator role on your own account. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids#serviceids) and [Managing access to resources](/docs/account?topic=account-assign-access-resources).

For an example of useful access policies for {{site.data.keyword.registrylong_notm}}, see [Granting access to {{site.data.keyword.registryshort}} resources tutorial](/docs/Registry?topic=Registry-iam_access).
{: tip}

## Setting up region-based policies for IAM
{: #create_region_policy_iam}

For all regions other than global you can use the region field when you create a rule. So for example, in the CLI for `us-south` you use the `--region us-south` option. However, because global is a geography and not a region you must omit the `--region`option and add `geography=global` into the `--attributes` field.

### Region-based user policies
{: #create_region_policy_user}

The following example shows the command for creating a user policy to assign a role to a user in `us-south`, where `USER_ID` is the user ID (`name@example.com`) and `ROLES` is the role or roles that you want to allocate:

```txt
ibmcloud iam user-policy-create USER_ID --roles ROLES --service-name container-registry --region us-south
```
{: pre}

The following example shows the command for creating a user policy to assign a role to a user in `global`, where `USER_ID` is the user ID (`name@example.com`) and `ROLES` is the role or roles that you want to allocate:

```txt
ibmcloud iam user-policy-create USER_ID --roles ROLES --service-name container-registry --attributes "geography=global"
```
{: pre}

### Region-based service ID policies
{: #create_region_policy_service}

The following example shows the command for creating a service ID policy in `us-south`, where `SERVICE_ID` is the service ID and `ROLES` is the role or roles that you want to allocate:

```txt
ibmcloud iam service-policy-create SERVICE_ID --roles ROLES --service-name container-registry --region us-south
```
{: pre}

The following example shows the command for creating a service ID policy in `global`, where `SERVICE_ID` is the service ID and `ROLES` is the role or roles that you want to allocate:

```txt
ibmcloud iam service-policy-create SERVICE_ID --roles ROLES --service-name container-registry --attributes "geography=global"
```
{: pre}
