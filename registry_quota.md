---

copyright:
  years: 2017, 2022
lastupdated: "2022-02-08"

keywords: quota limits, custom quota limits, pull traffic, quotas, storage, free up space, decrease storage,

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Managing quota limits for storage and pull traffic
{: #registry_quota}

You can limit the amount of storage and pull traffic that can be used in your {{site.data.keyword.cloud}} account by setting and managing custom quota limits.
{: shortdesc}

## Setting quota limits for storing and pulling images
{: #registry_quota_set}
{: help}
{: support}

You can limit the amount of storage and pull traffic to your private images by setting your own quota limits.
{: shortdesc}

When you upgrade to the {{site.data.keyword.registrylong_notm}} standard plan, you benefit from unlimited amount of storage and pull traffic to your private images. To avoid exceeding your preferred payment level, you can set individual quotas for the amount of storage and pull traffic. Quota limits are applied to all namespaces that you set up in {{site.data.keyword.registrylong_notm}}. If you are using the free service plan, you can also set custom quotas within your free amount of storage and pull traffic.

To set a quota, complete the following steps.

1. Log in to {{site.data.keyword.cloud_notm}}.

    ```txt
    ibmcloud login
    ```
    {: pre}

2. Review your current quota limits for storage and pull traffic.

    ```txt
    ibmcloud cr quota
    ```
    {: pre}

    Your output looks similar to the following example.

    ```txt
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

3. Change the quota limit for storage and pull traffic. To change the pull traffic usage, specify the **traffic** option and replace `<traffic_quota>` with the value in megabytes that you want to set for the pull traffic quota. If you want to change the amount of storage in your account, specify the **storage** option and replace `<storage_quota>` with the value in megabytes that you want to set.

    If you are on the free plan, you cannot set your quota to an amount that exceeds the free tier. The free tier allowance for storage is 512 MB and traffic is 5120 MB.
    {: tip}

    ```txt
    ibmcloud cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    Example to set your quota limit for storage to 600 megabytes, and the pull traffic to 7000 megabytes:

    ```txt
    ibmcloud cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}

## Reviewing quota limits and usage for storing and pulling images
{: #registry_quota_get}
{: help}
{: support}

You can review your quota limits and check your current storage and pull traffic usage for your account.
{: shortdesc}

1. Log in to {{site.data.keyword.cloud_notm}}.

    ```txt
    ibmcloud login
    ```
    {: pre}

2. Review your current quota limits for storage and pull traffic.

    ```txt
    ibmcloud cr quota
    ```
    {: pre}

    Your output looks similar to the following example.

    ```txt
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

## Freeing up used storage and changing service plans or quota limits to stay within given quota limits
{: #registry_quota_freeup}
{: help}
{: support}

If you exceed the quota limits that are set for your {{site.data.keyword.cloud_notm}} account, you can free up storage and change your service plan or quota limits so that you can continue pushing and pulling images to and from your namespace.
{: shortdesc}

To free up image storage in your {{site.data.keyword.cloud_notm}} account, complete the following steps.

Depending on the size of the image, it might take a while for the image to be removed and for the storage to be available.
{: note}

1. To list all images by [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest), both [tagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) and [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged), in all your namespaces of your {{site.data.keyword.cloud_notm}} account, run the following command. Combine the content of the **Repository** column and the **Digest** column to create the image name in the format `repository@digest`.

    ```txt
    ibmcloud cr image-digests
    ```
    {: pre}

2. You can remove images individually, collectively, or by using retention policies.

   - To remove images individually from your namespace, use the [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command. Replace `<image_name>` with the name of the image that you want to remove. The name must be in the format `repository@digest` or `repository:tag`. If a tag is not specified in the image name, the image that is tagged `latest` is deleted by default. Deleted images are stored in the trash for 30 days. Images that are in the trash don't count toward your quota.

        You can remove both tagged and untagged images by using the format `repository@digest`. You can remove tagged images only by using the format `repository:tag`.
        {: note}

        ```txt
        ibmcloud cr image-rm <image_name>
        ```
        {: pre}

   - To remove untagged images collectively from your namespace, use the [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged) command, see [Clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged).

   - To use retention policies, see [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).

3. Review your storage quota usage.

    ```txt
    ibmcloud cr quota
    ```
    {: pre}

4. To reduce your pull traffic usage, you must wait until the next billing period.

    To continue pulling images from your namespaces, choose between the following options.

    - Wait until the next billing cycle starts.
    - If you have a free plan, [upgrade to the standard service plan](/docs/Registry?topic=Registry-registry_overview#registry_plan_upgrade).
    - If you already have a standard plan, [set new quota limits for the pull traffic](#registry_quota_set).


