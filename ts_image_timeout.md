---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-25"

keywords: registry, list, images, timeout, account

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is it timing out when I list images in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-image-timeout}
{: troubleshoot}
{: support}

Listing images times out in {{site.data.keyword.registrylong}}.
{: shortdesc}

The request timed out while you attempted to list your images in the {{site.data.keyword.cloud_notm}} console, CLI, or API.
{: tsSymptoms}

The most likely cause of the timeout is that the account has many images. The vulnerability reports can't be displayed because the targeted account contains more images than Vulnerability Advisor can process.
{: tsCauses}

You can run the [`ibmcloud cr image-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) command with the `--restrict` option to reduce the scope of the list and increase performance. Alternatively, if you don't want to fetch vulnerability reports, use the `--no-va` option. For help with managing the number of images, see [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).
{: tsResolve}
