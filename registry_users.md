---

copyright:
  years: 2018, 2022
lastupdated: "2022-07-06"

keywords: user access policies, access policies, policies, policy enforcement, user access, roles, account, users, resources, namespace

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Defining IAM access policies for {{site.data.keyword.registryshort_notm}}
{: #user}

As an administrator, you can define {{site.data.keyword.iamlong}} (IAM) access policies for your registry to create different levels of access for different users in {{site.data.keyword.registrylong}}. For example, you can authorize certain users to set quotas while other users can view only quotas.
{: shortdesc}

From 5 July 2022, all accounts require {{site.data.keyword.iamshort}} (IAM) access policies. If you started to use {{site.data.keyword.registryshort_notm}} before the availability of [IAM API key policies in {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_release_notes#registry-25feb2019) in February 2019, you must ensure that you are using IAM access policies to manage access to the {{site.data.keyword.registrylong_notm}} service. For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy).
{: important}

You must define IAM [access policies](x2853407){: term} for every user that works with {{site.data.keyword.registrylong_notm}}. The scope of an IAM access policy is based on the user's role or roles that determine the actions that they are allowed to do. Some policies are pre-defined, but others can be customized.

If you started to use {{site.data.keyword.registrylong_notm}} before 4 October 2018, you must enable policy enforcement for each region so that you can use IAM access policies to manage access to the {{site.data.keyword.registrylong_notm}} service. If you do not enable this policy, any user in the account can manage registry resources. For more information, see [Enabling policy enforcement for existing users](#existing_users).
{: tip}

To find out more about IAM access policies, see [{{site.data.keyword.cloud_notm}} IAM roles](/docs/account?topic=account-userroles).

From version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan). However, you can still set permissions for the namespace at the account level or in the namespace itself.

## Creating policies
{: #create}
{: help}
{: support}

If you want to control access to resources, you must assign roles to users or service IDs. Access to {{site.data.keyword.registrylong_notm}} resources can be granted to the namespace resource by name, the [resource group](x2161955){: term}, or the entire service, that is, all namespaces in the account.

If you want to grant access to everything, don't specify a resource type or a resource. If you want to grant access to a specific namespace, specify the resource type as `namespace` and use the namespace name as the resource.

Before you begin, complete the following tasks:

- Decide what roles each user needs and on which resources in {{site.data.keyword.registrylong_notm}}, see [IAM roles](/docs/Registry?topic=Registry-iam#iam). You can create multiple policies, for example, you can grant write access on a resource but grant read access only on another resource, and grant no access on another resource. Policies are additive, which means that a global read policy and a resource-scoped write policy grants both read and write access on that resource.

- [Invite users to an account](/docs/account?topic=account-iamuserinv#iamuserinv).

    If you want users to create clusters in {{site.data.keyword.containerlong_notm}}, ensure that you assign the {{site.data.keyword.registrylong_notm}} Administrator role to those users and don't assign a resource group. For more information, see [Preparing to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare).
    {: tip}

To create policies for {{site.data.keyword.registrylong_notm}}, the service name field must be `container-registry`.

- To create a policy for users, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).
- To create a policy for service IDs, run the `ibmcloud iam service-policy-create` command or use the {{site.data.keyword.cloud_notm}} console to bind roles to your service IDs. To create policies, you must have the Administrator role. You automatically have the Administrator role on your own account. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids#serviceids) and [Managing access to resources](/docs/account?topic=account-assign-access-resources).

## Enabling policy enforcement for existing users
{: #existing_users}
{: help}
{: support}

If you’re an existing user, you must enable policy enforcement. If you started to use {{site.data.keyword.registrylong_notm}} after 4 October 2018, you don’t need to do anything to enable IAM access policies. Policies are enforced automatically for invited users and Service IDs.

To enable policy enforcement, you must run the `ibmcloud cr iam-policies-enable` command once in each region.
{: important}

1. [Create policies](#create) for your users and service IDs.

2. To enable policy enforcement, run the [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) command.

    You must have the Manager role on the account so that you can run the `ibmcloud cr iam-policies-enable` command. You automatically have Manager role in your own account.
    {: tip}

3. To verify that IAM access policies are enabled, run [`ibmcloud cr iam-policies-status`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_status).


