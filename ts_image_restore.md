---

copyright:
  years: 2017, 2021
lastupdated: "2021-08-05"

keywords: troubleshooting, support, help, errors, problems, ts, registry, restoring images, restoring images from the trash, trash

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

# When I'm restoring an image, why do I get an error that says that the tagged image exists?
{: #troubleshoot-image-restore}
{: troubleshoot}
{: support}

You want to restore an image from the {{site.data.keyword.registrylong}} trash, but you get a 409 error: `The tagged image already exists. You can restore this image by using the digest.`
{: shortdesc}

{: tsSymptoms}
You receive the following error message when you run the [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command: `The tagged image already exists. You can restore this image by using the digest.`
