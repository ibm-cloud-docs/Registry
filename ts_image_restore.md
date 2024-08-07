---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-25"

keywords: error, registry, restore, trash, image, tag, tagged image, digest, tagged image already exists, restore this image by using the digest, CRT0500E

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get an error when I'm restoring an image in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-image-restore}
{: troubleshoot}
{: support}

You want to restore an image from the {{site.data.keyword.registrylong}} trash, but you get a 409 error: `CRT0500E The tagged image already exists. You can restore this image by using the digest.`
{: shortdesc}

You receive the following error message when you run the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command: `CRT0500E The tagged image already exists. You can restore this image by using the digest. For more information, see troubleshooting: https://cloud.ibm.com/docs/Registry?topic=Registry-ts_index#ts_image_restore`
{: tsSymptoms}

An image with the same name exists in your live repository. You can't overwrite a live image with an image that is in the trash.
{: tsCauses}

Remove the [tag](#x2040924){: term} from the existing image in your live repository by running the [`ibmcloud cr image-untag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_untag) command. You can then restore the required image from the trash by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command with the option `<repo>@<digest>`, which restores the digest and its tags to the live repository. For more information, see [Restoring images by digest](/docs/Registry?topic=Registry-registry_images_#registry_images_restore_digest).
{: tsResolve}
