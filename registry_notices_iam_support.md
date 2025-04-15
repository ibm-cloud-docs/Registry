---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, iam, support, access policies, iam policies, policies

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort_notm}} supports IAM access policies
{: #registry_notices_iam_support}

As from 4 October 2018, {{site.data.keyword.registrylong}} supports {{site.data.keyword.iamshort}} (IAM) access policies. You can configure IAM policies to control the actions that your users can do.
{: shortdesc}

The original announcement was published on 4 October 2018.
{: note}

If you used {{site.data.keyword.registryshort_notm}} before 4 October 2018, policies are not enforced until you manually enable them. When IAM policy enforcement is enabled, users that order clusters must have the Administrator role on both {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.registryshort_notm}}.

You can use the `ibmcloud cr iam-policies-enable` command to opt in to fine-grained access control by using IAM. New users are opted in automatically.

For more information, see [Defining IAM access policies for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-user).

## Original announcement
{: #registry_notices_iam_support_announce}

The original announcement was published on 4 October 2018.
