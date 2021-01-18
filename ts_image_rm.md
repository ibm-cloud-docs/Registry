---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, deleting images, deleting tags, tags

subcollection: Registry

content-type: troubleshoot

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

# I used the `ibmcloud cr image-rm` command to delete an image, why did all the tags get deleted too?
{: #troubleshoot-image-rm}
{: troubleshoot}
{: support}

You tried to delete an image from {{site.data.keyword.registrylong}} and all the tags that referenced that image got deleted too.
{: shortdesc}

{: tsSymptoms}
You deleted an image by using the `ibmcloud cr image-rm` command and all the tags within the same repository that referenced the image also got deleted.

{: tsCauses}
Where multiple tags exist for the same image digest within a repository, the [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command removes the underlying image and all its tags. If the same image exists in a different repository or namespace, that copy of the image is not removed.

{: tsResolve}
If you want to remove a tag from an image, but leave the underlying image and any other tags, use the [`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) command. For more information, see [Removing tags from images in your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_untag) and [Deleting images from your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).
