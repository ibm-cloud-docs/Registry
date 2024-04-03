---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-03"

keywords: error, iam, access denied, access, insufficient scope, scope

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting errors about insufficient scope?
{: #troubleshoot-scope}
{: troubleshoot}
{: support}

You have a valid IAM API key or OAuth token, but you still get `Access denied` errors about insufficient scope in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get the following message:
{: tsSymptoms}

`Insufficient scope`

You might see this message if you are trying to access {{site.data.keyword.registryshort}} by using a client such as Docker. The following alternatives are possible causes:
{: tsCauses}

- **Scenario A.** The API key that is used to access {{site.data.keyword.registryshort}} has insufficient permissions.
- **Scenario B.** Context-based restriction rules are in place.

You can fix this problem in the following ways:
{: tsResolve}

- **Scenario A.** Confirm that the API key that you are using has suitable permissions for the resource that you are trying to access. Contact the owner of the resource for help. For more information, see [Managing IAM access](/docs/Registry?topic=Registry-iam&interface=ui).

- **Scenario B.** Check whether context-based restriction rules are in place. If so, these rules prevent you from accessing resources outside the defined allowed contexts. Adjust the allowed context or rerun your pull from within an allowed context. For more information, see [Protecting {{site.data.keyword.registryshort}} resources with context-based restrictions](/docs/Registry?topic=Registry-registry-cbr&interface=ui).

    To confirm whether a context-based restriction rule caused the `Access denied` error, check {{site.data.keyword.at_full_notm}} for the resource that is being accessed. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor#enabled-access).
    {: tip}
