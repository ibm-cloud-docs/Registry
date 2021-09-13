---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-13"

keywords: troubleshooting, support, help, errors, problems, ts, registry, listing images times out,

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does listing images  in the {{site.data.keyword.cloud_notm}} console timeout?
{: #troubleshoot-image-timeout}
{: troubleshoot}
{: support}

Listing images in the {{site.data.keyword.registrylong}} {{site.data.keyword.cloud_notm}} console times out.
{: shortdesc}

The request timed out while you attempted to list your images in the {{site.data.keyword.cloud_notm}} console.
{: tsSymptoms}

The {{site.data.keyword.cloud_notm}} console timed out while it was trying to list all your images. The most likely cause of the timeout is that the account has many images. For help with managing the number of images see, [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).
{: tsCauses}

You can run the [`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) command to see all the images in the account because the CLI does not have a timeout. Also, consider adding the `--restrict` and  `--no-va` options to reduce the scope of the list and increase performance.
{: tsResolve}


