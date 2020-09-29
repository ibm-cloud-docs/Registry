---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-29"

keywords: troubleshooting, support, help, errors, problems, ts, registry, restoring images, restoring images from the trash by digest, trash, restoring tags

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

# When I'm restoring an image from the trash by digest, why aren't some of the tags restored?
{: #troubleshoot-image-restore-digest}
{: troubleshoot}
{: support}

You want to restore an image by digest from the {{site.data.keyword.registrylong}} trash, but some of the tags weren't restored.
{: shortdesc}

{: tsSymptoms}
You run the [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command, but the tags were not restored. If all of the tags were unsuccessful, the digest shows in the live repository, but it is untagged. You can see the digest if you run [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests), but not if you run [`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list).

{: tsCauses}
The tags that were not restored already exist in your live repository. You can't overwrite a tag with a tag that is in the trash.

{: tsResolve}
Untag the existing image in your live repository by running the [`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) command. You can then restore the required image from the trash by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command with the option `<repo>@<digest>`, which restores the digest and its tags to the live repository. For more information, see [Restoring images by digest](/docs/Registry?topic=Registry-registry_images_#registry_images_restore_digest). Alternatively, you can run the [`ibmcloud cr image-tag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) command and use the restored digest as the source image.

In your live repository, you can pull the image by digest. If you run the [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) command, the image shows in the output.
{: tip}
