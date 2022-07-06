---

copyright:
  years: 2022
lastupdated: "2022-07-06"

keywords: registry, resource, authorized, namespace, create a namespace, permissions

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get "You are not authorized to access the specified resource" when I create a namespace?
{: #troubleshoot-namespace-auth}
{: troubleshoot}
{: support}

When you try to create a namespace in {{site.data.keyword.registrylong}}, you get the following error message: `You are not authorized to access the specified resource`.
{: shortdesc}

You try to create a namespace, but you get the following error message: `You are not authorized to access the specified resource`.
{: tsSymptoms}

You don't have the right user permissions for working with namespaces. To add, assign, and remove namespaces, you must have the Manager role in the {{site.data.keyword.registryshort}} service at the account level. If you have the Manager role on the resource group, or resource groups, that is not sufficient, it must be at the account level.
{: tsCauses}

You must ensure that you are assigned the Manager role at the account level. For more information, see [User permissions for working with namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan_perm).
{: tsResolve}


