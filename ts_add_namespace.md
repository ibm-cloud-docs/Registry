---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-23"

keywords: troubleshoot, error, problem, registry, namespace, add,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# I can't add a namespace
{: #troubleshoot-add-namespace}
{: troubleshoot}
{: support}

Setting up a namespace fails in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you run `ibmcloud cr namespace-add`, you are unable to set your entered value as the namespace.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- You entered a namespace value that is already being used by another {{site.data.keyword.cloud}} organization.
- A namespace was recently deleted and you are reusing its name. If the namespace that was deleted contained many resources, the deletion might not yet be fully processed by {{site.data.keyword.registrylong_notm}}.
- You used invalid characters in the namespace value.

You can fix this problem in the following ways:
{: tsResolve}

- Follow any instructions that are in the returned error message.
- Check that you entered a valid namespace:
    - Your namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region.
    - Your namespace must be 4 - 30 characters long.
    - Your namespace must start and end with a letter or number.
    - Your namespace must contain lowercase letters, numbers, hyphens (-), and underscores (_) only.
- Choose a different value for your namespace.
- If you are re-creating a namespace that was deleted, and it contained many images, try again later.


