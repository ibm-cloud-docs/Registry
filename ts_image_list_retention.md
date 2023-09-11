---

copyright:
  years: 2017, 2023
lastupdated: "2023-09-11"

keywords: registry, image, retention, distroless, list, creation date

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why doesn't the retention command show all the images?
{: #troubleshoot-image-list-retention}
{: troubleshoot}
{: support}

An image doesn't show in the list that is produced by the {{site.data.keyword.registrylong}} `ibmcloud cr retention-run` command.
{: shortdesc}

You ran the [`ibmcloud cr retention-run`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run) command and an image that you're expecting to view in the list is not displayed.
{: tsSymptoms}

You might have a [distroless](https://github.com/GoogleContainerTools/distroless){: external} image. Some distroless images don't have a creation date.  The `ibmcloud cr retention-run` command deletes the oldest images, and therefore requires a creation date.
{: tsCauses}

You can delete the image manually by running the [`ibmcloud cr image-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm) command, see [Deleting images from your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).
{: tsResolve}

To check the creation date of an image, you can run the [`ibmcloud cr image-inspect`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_inspect) command. If the image doesn't have a creation date, the date is shown in the `ibmcloud cr image-inspect` output as `1970-01-01`, and the image is excluded from the results for `ibmcloud cr retention-run`.
{: tip}
