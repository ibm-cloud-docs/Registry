---

copyright:
  years: 2017, 2025
lastupdated: "2025-01-20"

keywords: registry, delete, image, tag, ibmcloud cr image-rm

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do all the tags get deleted when I delete an image in {{site.data.keyword.registryshort}}?
{: #troubleshoot-image-rm}
{: troubleshoot}
{: support}

You tried to delete an image from {{site.data.keyword.registrylong}} by using the `ibmcloud cr image-rm` command and all the [tags](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) that referred to that image got deleted too.
{: shortdesc}

You deleted an image by using the `ibmcloud cr image-rm` command and all the tags within the same repository that reference the image also got deleted.
{: tsSymptoms}

Where multiple tags exist for the same image [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) within a repository, the [`ibmcloud cr image-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm) command removes the underlying image and all its tags. If the same image exists in a different repository or namespace, then that copy of the image is not removed.
{: tsCauses}

If you want to remove a tag from an image, but leave the underlying image and any other tags, use the [`ibmcloud cr image-untag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_untag) command. For more information, see [Removing tags from images in your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_untag) and [Deleting images from your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).
{: tsResolve}
