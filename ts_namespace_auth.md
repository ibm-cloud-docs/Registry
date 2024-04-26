---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-26"

keywords: registry, resource, authorized, namespace, create a namespace, permissions

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why aren't I authorized to access a specified resource in {{site.data.keyword.registryshort}}?
{: #troubleshoot-namespace-auth}
{: troubleshoot}
{: support}

You aren't authorized to create a namespace in {{site.data.keyword.registrylong}}.
{: shortdesc}

You try to create a namespace, but you receive the following error message:
{: tsSymptoms}

`You are not authorized to access the specified resource.`

You don't have the correct user permissions for working with namespaces. To add, assign, and remove namespaces, you must have the Manager role in the {{site.data.keyword.registryshort}} service at the account level. If you have the Manager role on the resource group, or resource groups, it is not sufficient, the Manager role must be at the account level.
{: tsCauses}

You must ensure that you are assigned the Manager role at the account level. For more information, see [User permissions for working with namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan_perm).
{: tsResolve}
