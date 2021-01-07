---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-07"

keywords: troubleshooting, support, help, errors, problems, ts, registry, listing images times out, IBM Cloud console, console

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

# Why does listing images in the {{site.data.keyword.cloud_notm}} console time out?
{: #troubleshoot-image-timeout}
{: troubleshoot}
{: support}

Listing images in the {{site.data.keyword.registrylong}} {{site.data.keyword.cloud_notm}} console times out.
{: shortdesc}

{: tsSymptoms}
The request timed out while you attempted to list your images in the {{site.data.keyword.cloud_notm}} console.

{: tsCauses}
The {{site.data.keyword.cloud_notm}} console timed out while trying to list all your images. The most likely cause of the timeout is that the account has a very large number of images. For help with managing the number of images see, [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).

{: tsResolve}
You can run the [`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) command to see all the images in the account because the CLI does not have a timeout. Also consider using the `--restrict` option to reduce the scope of the list and increase performance.
