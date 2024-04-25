---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-25"

keywords: error, iam, access denied, access, private network,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting errors about using a private network in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-private}
{: troubleshoot}
{: support}

You have a valid IAM API key or OAuth token, but you still get an `Access denied` error over a private network in {{site.data.keyword.registrylong}}: `Private-only access is enabled on this account, but this request was over the public network.`
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get the following message:
{: tsSymptoms}

`Private-only access is enabled on this account, but this request was over the public network. You must access this account over the private network`

You attempted to access {{site.data.keyword.registryshort}} over the public network, but the account is set to allow only private network traffic.
{: tsCauses}

Check the account settings for private only traffic. If private-only traffic is enabled, ensure that you are accessing {{site.data.keyword.registryshort}} from the private network. For more information, see [Using private network connections](/docs/Registry?topic=Registry-registry_private#registry_private_images).
{: tsResolve}
