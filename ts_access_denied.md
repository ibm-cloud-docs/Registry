---

copyright:
  years: 2023, 2024
lastupdated: "2024-02-13"

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

- `You are not authorized to access the specified resource`, see [Why am I getting `Access denied` errors for a resource?](/docs/Registry?topic=Registry-troubleshoot-resource) for assistance.

- `Insufficient scope`, you might see this message if you are trying to access {{site.data.keyword.registryshort}} by using a client such as Docker, see [Why am I getting `Access denied` errors about insufficient scope?](/docs/Registry?topic=Registry-troubleshoot-scope) for assistance.

- `Your account has exceeded its pull traffic quota for the current month.`, see [Why am I getting `Access denied` errors about my quota?](/docs/Registry?topic=Registry-troubleshoot-quota) for assistance.

- `Your account has exceeded its image storage quota for the current month.`, see [Why am I getting `Access denied` errors about my quota?](/docs/Registry?topic=Registry-troubleshoot-quota) for assistance.

- `You must access this account over the private network`, see [Why am I getting `Access denied` errors  over a private network?](/docs/Registry?topic=Registry-troubleshoot-private) for assistance.

- `Status code 403 Forbidden`, you might see this message if you are using {{site.data.keyword.codeenginefull_notm}}, see [Why am I getting a `Forbidden` error when I'm using {{site.data.keyword.codeengineshort}}?](/docs/Registry?topic=Registry-troubleshoot-forbidden-ce) for assistance.

- `ImagePullBackoff`, you might see this status when you start containers in Kubernetes, see [Why do images fail to pull from registry with `ImagePullBackOff` or authorization errors?](/docs/Registry?topic=Registry-ts-app-image-pull) for assistance.
