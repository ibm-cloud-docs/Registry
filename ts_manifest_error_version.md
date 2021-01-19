---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, image not supported, manifest version, tagging image fails

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

# Why am I getting a manifest version error when I try to tag my image?
{: #troubleshoot-manifest-error-version}
{: troubleshoot}
{: support}

You get a manifest version error when you try to tag your image in {{site.data.keyword.registrylong}}: `The manifest version for this image is not supported for tagging.`
{: shortdesc}

{: tsSymptoms}
You tried to tag your image, but you receive the following error message: `The manifest version for this image is not supported for tagging. To upgrade to a supported manifest version, pull and push this image by using Docker version 1.12 or later, then run the 'ibmcloud cr image-tag' command again.`

{: tsCauses}
The manifest version is not supported.

{: tsResolve}
To resolve the problem, complete the following steps:

1. Upgrade to Docker Engine version 1.12 or later.

2. Pull the image that you tried to tag by running the following command, where `<source_image>` is your source image name:

   ```
   docker pull <source_image>
   ```
   {: pre}

3. To upgrade the manifest version, push the image by running the following command:

   ```
   docker push <source_image>
   ```
   {: pre}

4. Tag the image by running the `ibmcloud cr image-tag` command, see [Creating new images that refer to a source image](/docs/Registry?topic=Registry-registry_images_#registry_images_source).
