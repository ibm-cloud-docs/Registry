---

copyright:
  years: 2019, 2023
lastupdated: "2023-12-18"

keywords: retention, delete images, retain images, clean up, retention policies, delete images, keep all images, namespace, images, policy, repository, trash

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Cleaning up your namespaces
{: #registry_retention}

You can clean up your [namespace](#x2031005){: term} by choosing to retain only the most recent images in each repository in that namespace in {{site.data.keyword.registrylong}}.
{: shortdesc}

You can also choose whether to delete or retain your untagged images.

You can detect and delete old images from all the repositories in a namespace by running a one-off command, `ibmcloud cr retention-run`, or by setting a scheduled policy by running the `ibmcloud cr retention-policy-set` command. You can choose the number of images that you want to keep in each repository in a namespace, all other images are automatically deleted. Both options keep the most recent images. The age of the image is determined by when the image was created, not when it was pushed to the [registry](#x2064940){: term}. The number of images that are kept is the same for each repository in that namespace.

When you run the [`ibmcloud cr retention-run`](#retention_images) and [`ibmcloud cr retention-policy-set`](#retention_policy_set) commands, a list of images to delete is shown, and you must confirm that you want to delete those images. After you run the `ibmcloud cr retention-policy-set` command the first time, the policy runs automatically and deletes any images that meet the criteria that are specified in the policy. Deleted images are stored in the trash for 30 days.

If you want to check what's in the trash, run the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-registry_images_#registry_images_list_trash) command. You can restore images from the trash by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-registry_images_#registry_images_restore) command.

If you want to check your policies, you can run the [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list) command.

If you want to cancel a policy, [update the retention policy so that it keeps all your images](#retention_policy_keep).

You can also clean up your namespace by [deleting your untagged images](#retention_images_untagged).

## Planning retention
{: #retention_plan}

The [`ibmcloud cr retention-run`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run) and [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set) commands operate on a per-namespace basis. If you have multiple namespaces in your pipeline, you can apply different retention criteria for each namespace to best suit your requirements.

Consider a typical delivery pipeline with development, staging, and production environments. As code is delivered, continuous integration and continuous deployment pushes images into the registry and then deploys them straight to your development environment. After testing, some builds from development are promoted to staging, and then potentially onto production. In this scenario, the rate of image change is fastest in development and slowest in production. If all your environments pull images from the same namespace, it can be difficult to choose an appropriate number of images to retain due to this difference in velocity.

A good approach is to deliver all images into a development namespace, for example, `project-development`, and then to use the [`ibmcloud cr image-tag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_tag) command to tag the image into a different namespace when it is promoted to a higher stage of the pipeline. In the previous example, you can have three namespaces: development, `project-development`, staging, `project-staging`, and production, `project-production`. When you are promoting from development to staging, images are tagged from the `project-development` namespace into the `project-staging` namespace, and the images from the `project-staging` namespace are used for deployment. Similarly, when you are promoting from staging to production, images are tagged from the `project-staging` namespace into the `project-production` namespace, and the `project-production` namespace images are used in the production deployment.

You gain the following advantages by using this technique:

- You can choose different retention settings for development, staging, and production namespaces.
- You minimize the chances of accidentally removing an image that might be in use in your staging or production environments, when compared with using a single namespace for all images.
- You can use different [IAM](/docs/Registry?topic=Registry-iam) policies. For example, you can have more restrictive access to production images.
- You can sign production images, but leave development and staging images unsigned.

## Clean up your namespaces to keep a set number of images
{: #retention_images}
{: help}
{: support}

Use the `ibmcloud cr retention-run` command to clean up a namespace by retaining a specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.

You can choose whether to exclude untagged images from the clean-up process.

The [`ibmcloud cr retention-run`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run) command lists the images to delete and gives you the option to cancel before deletion.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command and restore a selected image by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command.
{: tip}

To reduce the number of images in each repository within your namespace by using the CLI, complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. Choose the registry in which you want to clean up your images by running the following command and selecting the appropriate region:

    ```txt
    ibmcloud cr region-set
    ```
    {: pre}

3. To retain the most recent images and delete the others, run one the following commands:

    - If you want to clean up both tagged and untagged images, run the following command:

        ```txt
        ibmcloud cr retention-run --images <image_count> <namespace>
        ```
        {: pre}

        Where `<image_count>` is the number of images that you want to retain for each repository within your namespace, `<namespace>`.

    - If you want to clean up tagged images only and retain all untagged images, run the following command:

        ```txt
        ibmcloud cr retention-run --retain-untagged --images <image_count> <namespace>
        ```
        {: pre}

        Where `<image_count>` is the number of images that you want to retain for each repository within your namespace, `<namespace>`.

    If an image that you're expecting to see doesn't show in the list that is produced, see [Why doesn't the retention command show all the images?](/docs/Registry?topic=Registry-troubleshoot-image-list-retention) for assistance.
    {: tip}

4. Verify that the images were deleted by running the following command, and check that the images do not show in the list.

    ```txt
    ibmcloud cr image-list
    ```
    {: pre}

    If listing images times out, see [Why is it timing out when I list images?](/docs/Registry?topic=Registry-troubleshoot-image-timeout) for assistance.
    {: tip}

## Set a retention policy for your namespaces
{: #retention_policy_set}
{: help}
{: support}

You can set a retention policy for your namespaces to retain only images that meet your criteria. The retention policy runs automatically to clean up your namespaces.

You can choose whether to exclude untagged images from the clean-up process.

You can use the [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set) command to set a policy that retains a specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted and moved to the trash. When you set a policy it runs immediately, then it runs daily. You can set only one policy in each namespace.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If you delete an image in error, you can restore the image by using the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) and [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) commands.
{: tip}

To set a policy and immediately move your deleted images to the trash, complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. Choose the registry in which you want to clean up your images by running the following command and selecting the appropriate region:

    ```txt
    ibmcloud cr region-set
    ```
    {: pre}

3. To set a policy that retains the most recent images and deletes the others, run one of the following commands:

    - If you want to clean up both tagged and untagged images, run the following command:

        ```txt
        ibmcloud cr retention-policy-set --images <image_count> <namespace>
        ```
        {: pre}

        Where `<image_count>` is the number of images that you want to retain for each repository within your namespace, `<namespace>`.

        A list of images to delete is displayed.

    - If you want to clean up tagged images only and retain all untagged images, run the following command:

        ```txt
        ibmcloud cr retention-policy-set --retain-untagged --images <image_count> <namespace>
        ```
        {: pre}

        Where `<image_count>` is the number of images that you want to retain for each repository within your namespace, `<namespace>`.

        A list of images to delete is displayed.

4. Review the list of images. To run the policy and delete the images, confirm that you want to set the policy.

    If you don't want to delete those images, choose `No`. The policy is not set and the images are not deleted.
    {: tip}

5. Verify that the images were deleted by running the following command, and check that the images show in the list.

    ```txt
    ibmcloud cr trash-list
    ```
    {: pre}

6. Verify that the policy is set by running the [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list) command, and check that the policy that you set for the namespace retains the required number of images. If you set the policy to retain all untagged images, ensure that the **`Retain all untagged`** column has the value `true`.

    ```txt
    ibmcloud cr retention-policy-list
    ```
    {: pre}

## Update a retention policy to keep all your images
{: #retention_policy_keep}
{: help}
{: support}

All namespaces have a default policy that keeps all images. You can return a policy to the default state.

You can use the [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set) command to set the policy back to the default state by running the following command, where `<namespace>` is your namespace:

```txt
ibmcloud cr retention-policy-set --images All <namespace>
```
{: pre}

## Clean up your namespaces by deleting untagged images
{: #retention_images_untagged}
{: help}
{: support}

You can clean up your namespace and reduce your bills by deleting your [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images in the namespace and optionally output the results in JSON format.

If you want to delete your untagged images and output the results in JSON format, run the following [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged) command, where `<namespace>` is your namespace:

```txt
ibmcloud cr image-prune-untagged [--force | -f [--output json]] --restrict <namespace>
```
{: pre}
