---

copyright:
  years: 2017, 2025
lastupdated: "2025-10-17"

keywords: registry, namespace, value, characters, delete

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I add a namespace in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-add-namespace}
{: troubleshoot}
{: support}

Setting up a namespace fails in {{site.data.keyword.registrylong}}.
{: shortdesc}

When you run `ibmcloud cr namespace-add`, you are unable to set your entered value as the namespace.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- **Scenario A.** You used invalid characters in the namespace value.
- **Scenario B.** You entered a namespace value that is already being used by another {{site.data.keyword.cloud_notm}} organization.
- **Scenario C.** A namespace was recently deleted and you're reusing its name. If the namespace that was deleted contained many resources, the deletion might not yet be fully processed by {{site.data.keyword.registryshort}}.
- **Scenario D.** You might not have the correct permissions for creating a namespace.

You can fix these problems in the following ways:
{: tsResolve}

Follow any instructions that are in the returned error message. If that is not successful, or no instructions are provided, try the following options:

- **Scenario A.** Check that you entered a valid namespace:
    - Your namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region.
    - Your namespace must be 4 - 30 characters long.
    - Your namespace must start and end with a letter or number.
    - Your namespace must contain lowercase letters, numbers, hyphens (-), and underscores (_) only.
- **Scenario B.** Choose a different value for your namespace.
- **Scenario C.** If you're re-creating a namespace that was deleted, and it contained many images, try again later.
- **Scenario D.** - Ensure that you have the Manager role in the {{site.data.keyword.registryshort_notm}} service at the account level for adding, assigning, and removing namespaces. See [Why aren't I authorized to access a specified resource in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-namespace-auth) for assistance.

For more information about namespaces, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan).
