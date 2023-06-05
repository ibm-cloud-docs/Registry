---

copyright:
  years: 2023
lastupdated: "2023-06-05"

keywords: error, iam, access denied, access policy, policy, access,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting `Access denied` errors?
{: #troubleshoot-access-denied}
{: troubleshoot}
{: support}

You have a valid IAM API key or OAuth token, but you still get `Access denied` errors in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get one of the following messages.

`You are not authorized to access the specified resource.`
:   For more information, see [Why am I getting `Access denied` errors for a resource](/docs/Registry?topic=Registry-troubleshoot-resource)?

`Insufficient scope`
:    You might see this message if you are trying to access {{site.data.keyword.registryshort}} by using a client such as Docker. For more information, see [Why am I getting `Access denied` errors about insufficient scope](/docs/Registry?topic=Registry-troubleshoot-scope)?

`Your account has exceeded its pull traffic quota for the current month.`
:   For more information, see [Why am I getting `Access denied` errors about my quota](/docs/Registry?topic=Registry-troubleshoot-quota)?

`Your account has exceeded its image storage quota for the current month.`
:   For more information, see [Why am I getting `Access denied` errors about my quota](/docs/Registry?topic=Registry-troubleshoot-quota)?

`You must access this account over the private network.`
:   For more information, see [Why am I getting `Access denied` errors over a private network](/docs/Registry?topic=Registry-troubleshoot-private)?

`Status code 403 Forbidden`
: You might see this message if you are using {{site.data.keyword.codeenginefull_notm}}. For more information, see [Why am I getting a `Forbidden` error when I'm using {{site.data.keyword.codeengineshort}}](/docs/Registry?topic=Registry-troubleshoot-forbidden-ce)?

`ImagePullBackoff`
:   You might see this status when you start containers in Kubernetes. For more information, see [Why do images fail to pull from registry with `ImagePullBackOff` or authorization errors](/docs/Registry?topic=Registry-ts-app-image-pull)?
