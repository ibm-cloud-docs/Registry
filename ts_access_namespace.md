---

copyright:
  years: 2023
lastupdated: "2023-02-06"

keywords: registry, namespace, access, image, scope

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I access a namespace?
{: #troubleshoot-access-namespace}
{: troubleshoot}
{: support}

Pushing an image fails with the message `insufficient scope` when you are using {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to push an image, you receive the message `insufficient scope`.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- You are using an incorrect credential.
- You have insufficient or incorrect IAM policies.

You can fix this problem in the following ways:
{: tsResolve}

- Check that you're using the correct credential, such as the user ID or the service ID.
- Check that you have an appropriate IAM policy. For more information about IAM policies, see [Managing IAM access for Container Registry](/docs/Registry?topic=Registry-iam&interface=ui).
