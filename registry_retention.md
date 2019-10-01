---

copyright:
  years: 2019,
lastupdated: "2019-10-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

subcollection: registry

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


# Retaining images
{: #registry_retention}

You can decide whether to delete or retain images.
{: shortdesc}

## Planning retention
{: #retention_plan}

The [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) and [`ibmcloud cr retention-policy-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) commands operate on a per-namespace basis, therefore if you have multiple namespaces in your pipeline, you can apply different retention criteria for each namespace to best suit your requirements.

Consider a typical delivery pipeline with development, staging, and production environments. As code is delivered, continuous integration and continuous deployment pushes images into the registry and then deploys them straight to your development environment. After testing, some builds from development are promoted to staging, and then potentially onto production. In this scenario, the rate of image change is fastest in development and slowest in production. If all of your environments pull images from the same namespace, it can be difficult to choose an appropriate number of images to retain due to this difference in velocity.

A good approach is to deliver all images into a development namespace, for example, `project-development`, and then to use the [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) command to tag the image into a different namespace when it is promoted to a higher stage of the pipeline. In the previous example, you can have three namespaces: development, `project-development`, staging, `project-staging`, and production, `project-production`. When you are promoting from development to staging, images are tagged from the `project-development` namespace into the `project-staging` namespace, and the images from the `project-staging` namespace are used for deployment. Similarly, when you are promoting from staging to production, images are tagged from the `project-staging` namespace into the `project-production` namespace, and the `project-production` namespace images are used in the production deployment.

You gain the following advantages by using this technique:

* You can choose different retention settings for development, staging, and production namespaces.
* You minimise the chances of accidentally removing an image that might be in use in your staging or production environments, when compared with using a single namespace for all images.
* You can use different [IAM](/docs/services/Registry?topic=registry-iam) policies. For example, you can have more restrictive access to production images.
* You can sign production images, but leave development and staging images unsigned.

## Clean up your namespaces by retaining only images that meet your criteria
{: #retention_images}

Use the `ibmcloud cr retention-run` command to clean up a namespace by retaining a specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.
{:shortdesc}

The [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) command lists the images that will be deleted and gives you the option to cancel before deletion.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list) command and restore a selected image by running the  [`ibmcloud cr image-restore`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command.
{: tip}

To reduce the number of images in each repository within your namespace by using the CLI, complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. Choose the registry in which you want to clean up your images by running the following command and selecting the appropriate region:

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. To retain some images and delete the others, run the following command:

   ```
  ibmcloud cr retention-run --images <image_count> <namespace>
   ```
   {: pre}

   Where `<image_count>` is the number of images that you want to retain for each repository within your namespace, `<namespace>`.

3. Verify that the images were deleted by running the following command, and check that the images do not show in the list.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

## Set a retention policy for your namespaces to retain only images that meet your criteria
{: #retention_policy_set}

You can set a retention policy that runs automatically to clean up your namespaces.
{:shortdesc}

You can use the [`ibmcloud cr retention-policy-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) command to set a policy that retains a specified number of images in a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted and moved to the trash. When you set a policy it runs immediately, subsequently it runs on a daily basis. You can set only one policy in each namespace.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If you delete an image in error, you can restore the image by using the [`ibmcloud cr trash-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list) and [`ibmcloud cr image-restore`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) commands.
{: tip}

To set a policy and immediately move your deleted images to the trash, complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. Choose the registry in which you want to clean up your images by running the following command and selecting the appropriate region:

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. To set a policy, run the following command:

   ```
   ibmcloud cr retention-policy-set --images <image_count> <namespace>
   ```
   {: pre}

   Where `<image_count>` is the number of images that you want to retain for each repository within your namespace, `<namespace>`.

   A list of images to delete is displayed. 

4. Review the list of images. To run the policy and delete the images, confirm that you want to set the policy. 

   If you don't want to delete those images, choose `No`. The policy is not set and the images are not deleted.
   {: tip}
  
5. Verify that the images were deleted by running the following command, and check that the images show in the list.

   ```
   ibmcloud cr trash-list
   ```
   {: pre}

6. Verify that the policy is set by running the [`ibmcloud cr retention-policy-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list) command, and check that policy that you set for the namespace retains the required number of images:

   ```
   ibmcloud cr retention-policy-list
   ```
   {: pre}

## Updating a retention policy so that it keeps all your images
{: #retention_policy_keep}

All namespaces have a default policy that keeps all images. You can return a policy to the default state.
{:shortdesc}

You can use the [`ibmcloud cr retention-policy-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) command to set the policy back to the default state by running the following command, where `<namespace>` is your namespace:

  ```
  ibmcloud cr retention-policy-set --images All <namespace>
  ```
  {: pre}
