---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-29"

keywords: troubleshooting, support, help, errors, problems, ts, registry, adding a namespace fails

subcollection: Registry

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:term: .term}
{:external: target="_blank" .external}
{:troubleshoot: data-hd-content-type='troubleshoot'}

# Why can't I add a namespace?
{: #troubleshoot-add-namespace}
{: troubleshoot}
{: support}

Setting up a namespace fails in {{site.data.keyword.registrylong}}.
{: shortdesc}

{: tsSymptoms}
When you run `ibmcloud cr namespace-add`, you are unable to set your entered value as the namespace.

{: tsCauses}
The following alternatives are possible causes:

- You entered a namespace value that is already being used by another {{site.data.keyword.cloud}} organization.
- A namespace was recently deleted and you are reusing its name. If the namespace that was deleted contained many resources, the deletion might not yet be fully processed by {{site.data.keyword.registrylong_notm}}.
- You used invalid characters in the namespace value.

{: tsResolve}
You can fix this problem in the following ways:

- Follow any instructions that are in the returned error message.
- Check that you entered a valid namespace:
  - Your namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region.
  - Your namespace must be 4 - 30 characters long.
  - Your namespace must start and end with a letter or number.
  - Your namespace must contain lowercase letters, numbers, hyphens (-), and underscores (_) only.
- Choose a different value for your namespace.
- If you are re-creating a namespace that was deleted, and it contained many images, try again later.
