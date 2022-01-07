---

copyright:
  years: 2017, 2022
lastupdated: "2022-01-07"

keywords: troubleshooting, support, help, errors, problems, ts, registry, listing images, retention, distroless images

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why doesn't an image show on the list that is produced by the `ibmcloud cr retention-run` command?
{: #troubleshoot-image-list-retention}
{: troubleshoot}
{: support}

An image doesn't show in the list that is produced by the {{site.data.keyword.registrylong}} `ibmcloud cr retention-run` command.
{: shortdesc}

You ran the [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) command and an image that you're expecting to view in the list is not displayed.
{: tsSymptoms}

You might have a [distroless](https://github.com/GoogleContainerTools/distroless){: external} image. Some distroless images don't have a creation date. The `ibmcloud cr retention-run` command deletes the oldest images, and therefore requires a creation date.
{: tsCauses}

You can delete the image manually by running the [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command, see [Deleting images from your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).
{: tsResolve}

To check the creation date of an image, you can run the [`ibmcloud cr image-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) command. If the image doesn't have a creation date, the date is shown in the `ibmcloud cr image-inspect` output as `1970-01-01` and the image is excluded from the results for `ibmcloud cr retention-run`.
{: tip}


