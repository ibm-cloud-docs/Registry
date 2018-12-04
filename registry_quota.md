---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-28"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Managing quota limits for storage and pull traffic
{: #registry_quota}

You can limit the amount of storage and pull traffic that can be used in your {{site.data.keyword.Bluemix}} account by setting and managing custom quota limits.
{:shortdesc}


## Setting quota limits for storing and pulling images
{: #registry_quota_set}

You can limit the amount of storage and pull traffic to your private images by setting your own quota limits.
{:shortdesc}

When you upgrade to the {{site.data.keyword.registryshort_notm}} standard plan, you benefit from unlimited amount of storage and pull traffic to your private images. To avoid exceeding your preferred payment level, you can set individual quotas for the amount of storage and pull traffic. Quota limits are applied to all namespaces that you set up in {{site.data.keyword.registrylong_notm}}. If you are using the free service plan, you can also set custom quotas within your free amount of storage and pull traffic.

To set a quota:

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Review your current quota limits for storage and pull traffic.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Your output looks similar to the following.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

3.  Change the quota limit for storage and pull traffic. To change the pull traffic usage, specify the **traffic** option and replace _&lt;traffic_quota&gt;_ with the value in megabytes that you want to set for the pull traffic quota. If you want to change the amount of storage in your account, specify the **storage** option and replace _&lt;storage_quota&gt;_ with the value in megabytes that you want to set.

    If you are on the free plan, you cannot set your quota to an amount that exceeds the free tier. The free tier allowance for storage is 512 MB and traffic is 5120 MB.
    {:tip}

    ```
    ibmcloud cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    Example to set your quota limit for storage to 600 megabytes, and the pull traffic to 7000 megabytes:

    ```
    ibmcloud cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}


## Reviewing quota limits and usage for storing and pulling images
{: #registry_quota_get}

You can review your quota limits and check your current storage and pull traffic usage for your account.
{:shortdesc}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Review your current quota limits for storage and pull traffic.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Your output looks similar to the following.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}


## Freeing up used storage and changing service plans or quota limits to stay within given quota limits
{: #registry_quota_freeup}

If you exceeded your quota limits that are set for your {{site.data.keyword.Bluemix_notm}} account, you can free up storage and change your service plan or quota limits to continue pushing and pulling images to and from your namespace.
{:shortdesc}

To free up image storage in your {{site.data.keyword.Bluemix_notm}} account:

1.  List all images in all your namespaces of your {{site.data.keyword.Bluemix_notm}} account.

    ```
    ibmcloud cr images
    ```
    {: pre}

2.  Remove an image from your namespace. Replace _&lt;image_name&gt;_ with the name of the image that you want to remove.

    ```
    ibmcloud cr image-rm <image_name>
    ```
    {: pre}

    Depending on the size of the image, it might take a while for the image to be removed and for the storage to be available.
    {:tip}

3.  Review your storage quota usage.

    ```
    ibmcloud cr quota
    ```
    {: pre}

4. You cannot reduce your pull traffic usage in a billing period.
   {:tip}

    To continue pulling images from your namespaces, choose between the following options.

    -   Wait until the next billing cycle starts.
    -   If you have a free plan, [upgrade to the standard service plan](registry_overview.html#registry_plan_upgrade).
    -   If you already have a standard plan, [set new quota limits for the pull traffic](#registry_quota_set).
