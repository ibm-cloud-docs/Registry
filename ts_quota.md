---

copyright:
  years: 2023
lastupdated: "2023-03-29"

keywords: error, iam, access denied, access, quota, pull traffic quota, image storage quota

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting `Access denied` errors about my quota?
{: #troubleshoot-quota}
{: troubleshoot}
{: support}

You have a valid IAM API key or OAuth token, but you still get `Access denied` errors about your quota in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get one of the following messages:
{: tsSymptoms}

- `Your account has exceeded its pull traffic quota for the current month.`
- `Your account has exceeded its image storage quota for the current month.`

You exceeded your image storage quota or pull traffic quota.
{: tsCauses}

Review your quota limits and increase them as necessary. However, if you do increase your quota, your costs increase. For more information, see [Managing quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_quota#registry_quota_get).
{: tsResolve}
