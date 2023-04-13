---

copyright:
  years: 2023
lastupdated: "2023-04-13"

keywords: error, registry, access, unauthorized, error, code engine, unauthorized

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting an `Unauthorized` error when I'm using {{site.data.keyword.codeengineshort}}?
{: #troubleshoot-unauthorized-ce}
{: troubleshoot}
{: support}

You are trying to access {{site.data.keyword.registrylong}} but are getting an `Unauthorized` error.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get the following message. You might see this error message if you are using {{site.data.keyword.codeenginefull_notm}}.
{: tsSymptoms}

`Status code 401 Unauthorized`

You are trying to access {{site.data.keyword.registryshort}} by using {{site.data.keyword.codeenginefull_notm}} and you don't have the correct credentials.
{: tsCauses}

If you are accessing {{site.data.keyword.registryshort}} through {{site.data.keyword.codeengineshort}}, confirm that {{site.data.keyword.codeengineshort}} is using a pull secret with a valid API key. For more information, see [Add registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce).
{: tsResolve}
