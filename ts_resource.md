---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-25"

keywords: error, iam, access denied, access, resource,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting errors for a resource in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-resource}
{: troubleshoot}
{: support}

You're trying to access a specific resource in {{site.data.keyword.registrylong}}, but you get an `Access denied` error message that says that you are not authorized to access that resource.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get the following message:
{: tsSymptoms}

`You are not authorized to access the specified resource.`

The following alternatives are possible causes:
{: tsCauses}

- **Scenario A.** The API key that is used to access {{site.data.keyword.registryshort}} has insufficient permissions.
- **Scenario B.** Context-based restriction rules are in place.

You can fix this problem in the following ways:
{: tsResolve}

- **Scenario A.** Confirm that the API key that you are using has suitable permissions for the resource that you are trying to access. Contact the owner of the resource for help. For more information, see [Managing IAM access](/docs/Registry?topic=Registry-iam&interface=ui).

- **Scenario B.** Check whether context-based restriction rules are in place. If so, these rules prevent you from accessing resources outside the defined allowed contexts. Adjust the allowed context or rerun your pull from within an allowed context. For more information, see [Protecting {{site.data.keyword.registryshort}} resources with context-based restrictions](/docs/Registry?topic=Registry-registry-cbr&interface=ui).

    To confirm whether a context-based restriction rule caused the `Access denied` error, check {{site.data.keyword.at_full_notm}} or {{site.data.keyword.logs_full_notm}} for the resource that is being accessed. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor#enabled-access).
    {: tip}

    As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For more information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
    {: deprecated}
