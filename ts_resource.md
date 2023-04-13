---

copyright:
  years: 2023
lastupdated: "2023-04-13"

keywords: error, iam, access denied, access, resource,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting `Access denied` errors for a resource?
{: #troubleshoot-resource}
{: troubleshoot}
{: support}

You have a valid IAM API key or OAuth token, but you still get `Access denied` errors for a specific resource in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get the following message:
{: tsSymptoms}

`You are not authorized to access the specified resource.`

The following alternatives are possible causes:
{: tsCauses}

- The API key that is used to access {{site.data.keyword.registryshort}} has insufficient permissions.
- Context-based restriction rules are in place.

You can fix this problem in the following ways:
{: tsResolve}

- Confirm that the API key that you are using has suitable permissions for the resource that you are trying to access. Contact the owner of the resource for help. For more information, see [Managing IAM access](/docs/Registry?topic=Registry-iam&interface=ui).

- Check whether context-based restriction rules are in place. If so, these rules prevent you from accessing resources outside the defined allowed contexts. Adjust the allowed context or rerun your pull from within an allowed context. For more information, see [Context-based restrictions](/docs/Registry?topic=Registry-iam&interface=ui#iam_cbr).

    To confirm whether a context-based restriction rule caused the `Access denied` error, check {{site.data.keyword.at_full_notm}} for the resource that is being accessed. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor#enabled-access).
    {: tip}
