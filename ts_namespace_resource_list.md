---

copyright:
  years: 2021
lastupdated: "2021-09-10"

keywords: troubleshooting, support, help, errors, problems, ts, registry, namespaces, resource list

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why don't all of my namespaces show up in the **Resource list** page in the {{site.data.keyword.cloud_notm}} console?
{: #troubleshoot-namespace-resource-list}
{: troubleshoot}
{: support}

My {{site.data.keyword.registrylong}} namespaces don't all show up in the {{site.data.keyword.cloud_notm}} **Resource list** page in the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

When you view your namespaces in the {{site.data.keyword.cloud_notm}} **Resource list** page, they don't all show up.
{: tsSymptoms}

Only namespaces that are assigned to resource groups show in the {{site.data.keyword.cloud_notm}} **Resource list** page.
{: tsCauses}

Namespaces created in version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, are created in the resource group that you specify. If you don't specify a resource group, and a resource group isn't targeted, the default resource group is used.

Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the {{site.data.keyword.cloud_notm}} console before 29 July 2020, aren't assigned to resource groups.

If you want to see all of your namespaces in the {{site.data.keyword.cloud_notm}} **Resource list** page, you must assign each namespace to a resource group, see [Assigning existing namespaces to resource groups](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_assign).
{: tsResolve}


