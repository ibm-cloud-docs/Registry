---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, billing, untagged images

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort}} to bill for storage used by untagged images from 1 February 2022
{: #registry_notices_billing}

Starting 1 February 2022, {{site.data.keyword.registrylong}} will bill for the storage that is used by untagged images.
{: shortdesc}

The original announcement was published on 2 November 2021.
{: note}

## What are untagged images?
{: #registry_notices_billing_untagged_image}

Untagged images are images in the registry that don’t have a tag. You can create untagged images in several ways, for example, by pushing different images consecutively by using the same tag.

## Do I have any untagged images?
{: #registry_notices_billing_untagged_image_own}

To find out whether you have any untagged images, list your images by running the [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) command. Untagged images have a hyphen (-) in the **Tags** column.

## Do I need untagged images?
{: #registry_notices_billing_untagged_image_need}

If you have active containers that are running untagged images, you need the untagged images. If you delete untagged images that are in use, you can cause problems with scaling or if you have an automated restart. For this situation to be a problem, you deployed by referencing the image by digest or your image reference might be mutated by a webhook service, for example, Portieris.

## How does this change affect me?
{: #registry_notices_billing_affect}

If you have many untagged images, you might see an increase in the bill for [{{site.data.keyword.registrylong_notm}}](https://www.ibm.com/products/container-registry){: external}. You can mitigate this cost by deleting any untagged images that you do not require.

## How can I remove untagged images?
{: #registry_notices_billing_untagged_image_remove}

You can remove untagged images individually, collectively, or by using retention policies.

-  To remove untagged images individually, run the following command, where `REPOSITORY` is your repository and `DIGEST` is your digest:

    `ibmcloud cr image-rm REPOSITORY@sha256:DIGEST`

    For more information, see [Deleting images from your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).
- To remove untagged images collectively, you can use the [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged) command. For more information, see [Clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged).
- To use retention policies to remove images, including untagged images, see [Cleaning up your namespaces in {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_retention).

## Original announcement
{: #registry_notices_billing_announce}

The original announcement was published on 2 November 2021.
