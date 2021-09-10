---

copyright:
  years: 2018, 2021
lastupdated: "2021-09-09"

keywords: user access role policies, access policies, policies, policy enforcement, user access, role policies, roles, 

subcollection: Registry

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Defining access role policies
{: #user}

As an administrator, you can define access policies for your registry to create different levels of access for different users. For example, you can authorize certain users to set quotas while other users can view only quotas.
{: shortdesc}

You must define access policies for every user that works with {{site.data.keyword.registrylong}}. The scope of an access policy is based on the user's role or roles that determine the actions that they are allowed to do. Some policies are pre-defined, but others can be customized.

If you started to use {{site.data.keyword.registrylong_notm}} before 4 October 2018, you must enable policy enforcement for each region so that you can use {{site.data.keyword.iamlong}} (IAM) access role policies to manage access to the {{site.data.keyword.registrylong_notm}} service. If you do not enable this policy, any user in the account can manage registry resources. For more information, see [Enabling policy enforcement for existing users](#existing_users).
{: tip}

To find out more about {{site.data.keyword.iamlong}} (IAM) access role policies, see [IAM access](/docs/account?topic=account-userroles).

From version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan). However, you can still set permissions for the namespace at the account level or in the namespace itself.

## Creating policies
{: #create}
{: help}
{: support}

If you want to control access to resources, you must assign roles to users or service IDs. Access to {{site.data.keyword.registrylong_notm}} resources can be granted to the namespace resource by name, the resource group, or the entire service, that is, all namespaces in the account.

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

If you’re an existing user, you must enable policy enforcement. If you started to use {{site.data.keyword.registrylong_notm}} after 4 October 2018, you don’t need to do anything to enable IAM policies. Policies are enforced automatically for invited users and Service IDs.

To enable policy enforcement, you must run the `ibmcloud cr iam-policies-enable` command once in each region.
{: important}

1. [Create policies](#create) for your users and service IDs.

2. To enable policy enforcement, run the [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) command.

    You must have the Manager role on the account so that you can run the `ibmcloud cr iam-policies-enable` command. You automatically have Manager role in your own account.
    {: tip}

3. To verify that IAM policies are enabled, run [`ibmcloud cr iam-policies-status`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_status).


