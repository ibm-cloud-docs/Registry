---

copyright:
  years: 2023
lastupdated: "2023-03-29"

keywords: error, registry, access, error, code engine, forbidden

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting a `Forbidden` error when I'm using {{site.data.keyword.codeengineshort}}?
{: #troubleshoot-forbidden-ce}
{: troubleshoot}
{: support}

You're trying to access {{site.data.keyword.registrylong}} but you're getting a `Forbidden` error.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get the following message. You might see this error message if you're using {{site.data.keyword.codeenginefull_notm}}.
{: tsSymptoms}

`Status code 403 Forbidden`

No token is sent, which means that you're trying to access a private namespace but you didn't send any credentials.
{: tsCauses}

If you're accessing {{site.data.keyword.registryshort}} through {{site.data.keyword.codeengineshort}}, confirm that {{site.data.keyword.codeengineshort}} is using a pull secret with a valid API key. For more information, see [Add registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce).
{: tsResolve}
