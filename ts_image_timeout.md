---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-14"

keywords: troubleshooting, support, help, errors, problems, ts, registry, listing images times out,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does listing images timeout?
{: #troubleshoot-image-timeout}
{: troubleshoot}
{: support}

Listing images times out.
{: shortdesc}

The request timed out while you attempted to list your images in the {{site.data.keyword.cloud_notm}} console, CLI, or API.
{: tsSymptoms}

The most likely cause of the timeout is that the account has many images. The vulnerability reports can't be displayed because the targeted account contains more images than Vulnerability Advisor can process.
{: tsCauses}

You can run the [`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) command with the `--restrict` option to reduce the scope of the list and increase performance. Alternatively, if you don't want to fetch vulnerability reports, use the `--no-va` option. For help with managing the number of images see, [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).
{: tsResolve}


