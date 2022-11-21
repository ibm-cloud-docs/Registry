---

copyright:
  years: 2017, 2022
lastupdated: "2022-06-13"

keywords: error, registry, manifest version, manifest version error, tag, image, the manifest version for this image is not supported for tagging

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get a manifest version error?
{: #troubleshoot-manifest-error-version}
{: troubleshoot}
{: support}

You get a manifest version error when you try to tag your image in {{site.data.keyword.registrylong}}: `The manifest version for this image is not supported for tagging.`
{: shortdesc}

You tried to tag your image, but you receive the following error message: `The manifest version for this image is not supported for tagging. To upgrade to a supported manifest version, pull and push this image by using Docker version 17.07 or later, then run the 'ibmcloud cr image-tag' command again.`
{: tsSymptoms}

The manifest version is not supported.
{: tsCauses}

To resolve the problem, complete the following steps:
{: tsResolve}

1. Upgrade to a supported version of Docker, see [Support for Docker](/docs/Registry?topic=Registry-registry_overview#docker).

2. Pull the image that you tried to tag by running the following command, where `<source_image>` is your source image name:

    ```txt
    docker pull <source_image>
    ```
    {: pre}

3. To upgrade the manifest version, push the image by running the following command:

    ```txt
    docker push <source_image>
    ```
    {: pre}

4. Tag the image by running the `ibmcloud cr image-tag` command, see [Creating new images that refer to a source image](/docs/Registry?topic=Registry-registry_images_#registry_images_source).


