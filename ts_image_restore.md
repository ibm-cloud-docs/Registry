---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-23"

keywords: troubleshoot, error, problem, registry, restoring images, trash, image, tag, tagged image, digest

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# When I'm restoring an image, I get an error saying that the tagged image exists
{: #troubleshoot-image-restore}
{: troubleshoot}
{: support}

You want to restore an image from the {{site.data.keyword.registrylong}} trash, but you get a 409 error: `The tagged image already exists. You can restore this image by using the digest.`
{: shortdesc}

You receive the following error message when you run the [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command: `The tagged image already exists. You can restore this image by using the digest.`
{: tsSymptoms}

An image with the same name exists in your live repository. You can't overwrite a live image with an image that is in the trash.
{: tsCauses}

Remove the tag from the existing image in your live repository by running the [`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) command. You can then restore the required image from the trash by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command with the option `<repo>@<digest>`, which restores the digest and its tags to the live repository. For more information, see [Restoring images by digest](/docs/Registry?topic=Registry-registry_images_#registry_images_restore_digest).
{: tsResolve}


