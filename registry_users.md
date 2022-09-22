---

copyright:
  years: 2018, 2022
lastupdated: "2022-09-22"

keywords: user access policies, access policies, policies, policy enforcement, user access, roles, account, users, resources, namespace

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Defining IAM access policies for {{site.data.keyword.registryshort_notm}}
{: #user}

As an administrator, you can define {{site.data.keyword.iamlong}} (IAM) access policies to create different levels of access for different users in {{site.data.keyword.registrylong}}. For example, you can authorize certain users to set quotas while other users can only view quotas.
{: shortdesc}

From 5 July 2022, all accounts require {{site.data.keyword.iamshort}} (IAM) access policies. If you started to use {{site.data.keyword.registryshort_notm}} before the availability of [IAM API key policies in {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_release_notes#registry-25feb2019) in February 2019, you must ensure that you are using IAM access policies to manage access to the {{site.data.keyword.registrylong_notm}} service. For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy).
{: important}

You must define IAM [access policies](x2853407){: term} for every user that works with {{site.data.keyword.registrylong_notm}}. The scope of an IAM access policy is based on the user's role or roles that determine the actions that they are allowed to do. Some roles are predefined, but custom roles can be defined.

To find out more about IAM access policies, see [{{site.data.keyword.cloud_notm}} IAM roles](/docs/account?topic=account-userroles).

From version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, you can assign {{site.data.keyword.registryshort}} namespaces to a [resource group](/docs/account?topic=account-rgs) and scope access policies to that group, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan). However, you can still define access policies that are scoped to individual {{site.data.keyword.registryshort}} namespaces or to all namespaces that are owned by the account.

## Creating policies
{: #create}
{: help}
{: support}

Before you begin, complete the following tasks:

- Decide what roles each user needs and on which resources in {{site.data.keyword.registrylong_notm}}, see [IAM roles](/docs/Registry?topic=Registry-iam#iam). You can create multiple policies, for example, you can grant write access on a resource but grant read access only on another resource. Policies are additive, which means that a global read policy and a resource-scoped write policy grants both read and write access on that resource.

- [Invite users to an account](/docs/account?topic=account-iamuserinv#iamuserinv).

    If you want users to create clusters in {{site.data.keyword.containerlong_notm}}, ensure that you assign the {{site.data.keyword.registrylong_notm}} Administrator role to those users and don't assign a resource group. For more information, see [Preparing to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare).
    {: tip}

To create policies for {{site.data.keyword.registrylong_notm}}, the service name field must be `container-registry`.

If you want to access resources, you must assign roles to users or service IDs. If you want to grant access to everything, don't specify a resource type or a resource. If you want to grant access to a specific namespace, specify the resource type as `namespace` and use the namespace name as the resource.

- To create a policy for users, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).
- To create a policy for service IDs, run the `ibmcloud iam service-policy-create` command or use the {{site.data.keyword.cloud_notm}} console to bind roles to your service IDs. To create policies, you must have the Administrator role. You automatically have the Administrator role on your own account. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids#serviceids) and [Managing access to resources](/docs/account?topic=account-assign-access-resources).

For an example of useful access policies for {{site.data.keyword.registrylong_notm}}, see the [Granting access to {{site.data.keyword.registryshort}} resources tutorial](/docs/Registry?topic=Registry-iam_access).
{: tip}


