---

copyright:
  years: 2023
lastupdated: "2023-03-29"

keywords: error, iam, access denied, access, private network,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting `Access denied` errors over a private network?
{: #troubleshoot-private}
{: troubleshoot}
{: support}

You have a valid IAM API key or OAuth token, but you still get `Access denied` errors over a private network in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get the following message:
{: tsSymptoms}

`You must access this account over the private network.`

You attempted to access {{site.data.keyword.registryshort}} over the public network, but the account is set to allow only private network traffic.
{: tsCauses}

Check the account settings for private only traffic. If private-only traffic is enabled, ensure that you're accessing {{site.data.keyword.registryshort}} from the private network. For more information, see [Using private network connections](/docs/Registry?topic=Registry-registry_private#registry_private_images).
{: tsResolve}
