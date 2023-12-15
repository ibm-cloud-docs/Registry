---

copyright:
  years: 2023
lastupdated: "2023-12-15"

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

When you try to access {{site.data.keyword.registryshort}}, you get one of the following messages.
{: tsSymptoms}

- `Your account has exceeded its pull traffic quota for the current month.`
- `Your account has exceeded its image storage quota for the current month.`

The following alternatives are possible causes:
{: tsCauses}

- A. You exceeded your image storage quota or pull traffic quota.
- B. You're on a free plan and you need to upgrade to a standard plan.

You can fix this problem in the following ways:
{: tsResolve}

- A. Review your quota limits and increase them as necessary. However, increasing your quota does increase your costs. For more information, see [Managing quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_quota#registry_quota_get) and [Staying within quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup).
- B. Upgrade to a standard plan. For more information, see [Upgrading your service plan](/docs/Registry?topic=Registry-registry_overview&interface=ui#registry_plan_upgrade).
