---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, listing images, retention

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

# Why is an image missing from the list that is produced by the `ibmcloud cr retention-run` command?
{: #troubleshoot-image-list-retention}
{: troubleshoot}
{: support}

An image doesn't show in the list that is produced by the {{site.data.keyword.registrylong}} `ibmcloud cr retention-run` command.
{: shortdesc}

{: tsSymptoms}
You ran the [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) command and an image that you're expecting to see in the list is not displayed.

{: tsCauses}
You might have a distroless image. Some distroless images don't have a creation date. The `ibmcloud cr retention-run` command deletes the oldest images, and therefore requires a creation date.

{: tsResolve}
You can delete the image manually by running the [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command, see [Deleting images from your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).

To check the creation date of an image, you can run the [`ibmcloud cr image-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) command. If the image doesn't have a creation date, the date is shown in the `ibmcloud cr image-inspect` output as `1970-01-01` and the image is excluded from the results for `ibmcloud cr retention-run`.
{: tip}
