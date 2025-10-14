---

copyright:
  years: 2017, 2025
lastupdated: "2025-10-14"

keywords: error, registry, manifest type, tag, image, the manifest type for this image is not supported for tagging, CRI0302E

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get a manifest type error when I tag my image in {{site.data.keyword.registryshort}}?
{: #troubleshoot-manifest-error-type}
{: troubleshoot}
{: support}

When you try to tag your image in {{site.data.keyword.registrylong}}, you get a manifest type error: `CRI0302E The manifest type for this image is not supported for tagging.`
{: shortdesc}

You tried to tag your image, but you received the following manifest error message: `CRI0302E The manifest type for this image is not supported for tagging. To find out about supported manifest types, see https://cloud.ibm.com/docs/Registry?topic=Registry-ts_index#ts_manifest_error_type`
{: tsSymptoms}

The manifest type is not supported.
{: tsCauses}

To resolve the problem, complete the following steps:
{: tsResolve}

1. Pull the image that you tried to tag by running the following command, where `SOURCE_IMAGE` is your source image name:

    ```txt
    docker pull SOURCE_IMAGE
    ```
    {: pre}

2. Tag your local copy of the image that you pulled in the previous step by running the following command, where `TARGET_IMAGE` is your new image name:

    ```txt
    docker tag SOURCE_IMAGE TARGET_IMAGE
    ```
    {: pre}

3. Push the image that you tagged in the previous step by running the following command:

    ```txt
    docker push TARGET_IMAGE
    ```
    {: pre}
