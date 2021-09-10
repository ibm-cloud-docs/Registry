---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-10"

keywords: troubleshooting, support, help, errors, problems, ts, registry, image not supported, manifest type, tagging image fails

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting a manifest type error when I try to tag my image?
{: #troubleshoot-manifest-error-type}
{: troubleshoot}
{: support}

You get a manifest type error when you try to tag your image in {{site.data.keyword.registrylong}}: `The manifest type for this image is not supported for tagging.`
{: shortdesc}

You tried to tag your image, but you receive the following manifest error message: `The manifest type for this image is not supported for tagging.`
{: tsSymptoms}

The manifest type is not supported.
{: tsCauses}

To resolve the problem, complete the following steps:
{: tsResolve}

1. Pull the image that you tried to tag by running the following command, where `<source_image>` is your source image name:

    ```
    docker pull <source_image>
    ```
    {: pre}

2. Tag your local copy of the image that you pulled in the previous step by running the following command, where `<target_image>` is your new image name:

    ```
    docker tag <source_image> <target_image>
    ```
    {: pre}

3. Push the image that you tagged in the previous step by running the following command:

    ```
    docker push <target_image>
    ```
    {: pre}


