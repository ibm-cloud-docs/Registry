---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, user access role policies, access policies, policies, policy enforcement,

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

# Defining user access role policies
{: #user access}

As an administrator, you can define access policies for your registry to create different levels of access for different users. For example, you can authorize certain users to set quotas while other users can only view quotas.
{: shortdesc}

You must define access policies for every user that works with {{site.data.keyword.registrylong}}. The scope of an access policy is based on a user's defined role or roles that determine the actions that they are allowed to perform. Some policies are pre-defined, but others can be customized.

If you started to use {{site.data.keyword.registrylong_notm}} before 4 October 2018, you must enable policy enforcement before your policies can take effect, see [Enabling policy enforcement for existing users](#existing_users).
{: tip}

To find out more about {{site.data.keyword.iamlong}} (IAM) access role policies, see [{{site.data.keyword.iamshort}}](/docs/iam?topic=iam-iamoverview#iamoverview).

## Creating policies
{: #create}

If you want to control access to resources, you must assign roles to users or service IDs. Access to {{site.data.keyword.registrylong_notm}} resources can be granted to the namespace resource by name, or the entire service, that is, all namespaces in the account.

If you want to grant access to everything, don't specify a resource type or a resource. If you want to grant access to a specifc namespace, specify the resource type as `namespace` and use the namespace name as the resource.

**Before you begin**

- Decide what roles each user needs and on which resources in {{site.data.keyword.registrylong_notm}}, see [IAM roles](/docs/services/Registry?topic=registry-iam#iam). Take into consideration that you can create multiple policies, for example, you can grant write access on a resource but only grant read access on another resource, and grant no access on another resource. Policies are additive, which means that a global read policy and a resource-scoped write policy grants both read and write access on that resource.

- [Invite users and assign access](/docs/iam?topic=iam-iamuserinv#iamuserinv).

  If you want users to be able to create clusters in {{site.data.keyword.containerlong_notm}}, ensure that you assign the {{site.data.keyword.registrylong_notm}} Administrator role to those users and do not assign a resource group, see [Preparing to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare).
  {: tip}

To create policies for {{site.data.keyword.registrylong_notm}}, the service name field must be `container-registry`.

- To create a policy for users, see [Managing access to resources](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).
- To create a policy for service IDs, run the `ibmcloud iam service-policy-create` command or use the GUI to bind roles to your service IDs. To create policies, you must have the Administrator role. You automatically have the Administrator role on your own account. For more information, see [Creating and working with service IDs](/docs/iam?topic=iam-serviceids#serviceids) and [Managing service ID access policies](/docs/iam?topic=iam-serviceidpolicy#serviceidpolicy).

## Enabling policy enforcement for existing users
{: #existing_users}

For users provisioned after 4 October 2018, IAM policies are enabled by default. For users provisioned before 4 October 2018, after you create your policies, you must enable policy enforcement so that your policies take effect.

1. [Create policies](#create) for your users and service IDs.

2. To enable policy enforcement, run the [`bx cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) command.

    You must have the Manager role on the account so that you can run the `ibmcloud cr iam-policies-enable` command. You automatically have Manager role in your own account.
    {: tip}
