---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-20"

keywords: user access role policies, access policies, policies, policy enforcement, user access, role policies, roles, 

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

# Defining access role policies
{: #user}

As an administrator, you can define access policies for your registry to create different levels of access for different users. For example, you can authorize certain users to set quotas while other users can only view quotas.
{: shortdesc}

You must define access policies for every user that works with {{site.data.keyword.registrylong}}. The scope of an access policy is based on a user's defined role or roles that determine the actions that they are allowed to do. Some policies are pre-defined, but others can be customized.

If you started to use {{site.data.keyword.registrylong_notm}} before 4 October 2018, you must enable policy enforcement for each region so that you can use {{site.data.keyword.iamlong}} (IAM) access role policies to manage access to the {{site.data.keyword.registrylong_notm}} service. If you do not enable this policy, any user in the account can manage registry resources. For more information, see [Enabling policy enforcement for existing users](#existing_users).
{: tip}

To find out more about {{site.data.keyword.iamlong}} (IAM) access role policies, see [IAM access](/docs/account?topic=account-userroles).

## Creating policies
{: #create}

If you want to control access to resources, you must assign roles to users or service IDs. Access to {{site.data.keyword.registrylong_notm}} resources can be granted to the namespace resource by name, or the entire service, that is, all namespaces in the account.

If you want to grant access to everything, don't specify a resource type or a resource. If you want to grant access to a specific namespace, specify the resource type as `namespace` and use the namespace name as the resource.

You cannot organize and assign access to registry namespaces in resource groups.
{: note}

Before you begin, complete the following tasks:

- Decide what roles each user needs and on which resources in {{site.data.keyword.registrylong_notm}}, see [IAM roles](/docs/Registry?topic=Registry-iam#iam). Take into consideration that you can create multiple policies, for example, you can grant write access on a resource but only grant read access on another resource, and grant no access on another resource. Policies are additive, which means that a global read policy and a resource-scoped write policy grants both read and write access on that resource.

- [Invite users to an account](/docs/account?topic=account-iamuserinv#iamuserinv).

  If you want users to be able to create clusters in {{site.data.keyword.containerlong_notm}}, ensure that you assign the {{site.data.keyword.registrylong_notm}} Administrator role to those users and do not assign a resource group, see [Preparing to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare).
  {: tip}

To create policies for {{site.data.keyword.registrylong_notm}}, the service name field must be `container-registry`.

- To create a policy for users, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).
- To create a policy for service IDs, run the `ibmcloud iam service-policy-create` command or use the GUI to bind roles to your service IDs. To create policies, you must have the Administrator role. You automatically have the Administrator role on your own account. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids#serviceids) and [Managing access to resources](/docs/account?topic=account-assign-access-resources).

## Enabling policy enforcement for existing users
{: #existing_users}

For users provisioned after 4 October 2018, IAM policies are enabled by default. For users provisioned before 4 October 2018, after you create your policies, you must enable policy enforcement so that your policies take effect.

To enable policy enforcement, you must run the `ibmcloud cr iam-policies-enable` command once in each region.
{: important}

1. [Create policies](#create) for your users and service IDs.

2. To enable policy enforcement, run the [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) command.

    You must have the Manager role on the account so that you can run the `ibmcloud cr iam-policies-enable` command. You automatically have Manager role in your own account.
    {: tip}

3. To verify that IAM policies are enabled, run [`ibmcloud cr iam-policies-status`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_status).
