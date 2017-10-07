---

copyright:
  years: 2017
lastupdated: "2017-10-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Getting started with {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}} provides a multi-tenant private image registry that you can use to safely store and share your Docker images with users in your {{site.data.keyword.Bluemix_notm}} account.

The {{site.data.keyword.Bluemix_notm}} console includes a brief Quick Start. To find out more about how to use the {{site.data.keyword.Bluemix_notm}} console, see [Viewing information about images in the {{site.data.keyword.Bluemix_notm}} console](registry_ui.html).


## Install the {{site.data.keyword.registrylong_notm}} CLI
{: #registry_cli_install}

1.  Install the [{{site.data.keyword.Bluemix_notm}} CLI](http://clis.ng.bluemix.net/ui/home.html) so that you can run the {{site.data.keyword.Bluemix_notm}}bx commands.
2.  Install the container-registry plug-in:

    ```
    bx plugin install container-registry -r {{site.data.keyword.Bluemix_notm}}
    ```
    {: pre}

3.  [Install the Docker CLI](https://www.docker.com/community-edition#/download). For Windows 8, or OS X Yosemite 10.10.x or earlier, install [Docker Toolbox](https://www.docker.com/products/docker-toolbox) instead.

## Set up a namespace
{: #registry_namespace_add}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Add a namespace to create your own image repository. Replace &lt;my_namespace&gt; with your preferred namespace.

    ```
    bx cr namespace-add <my_namespace>
    ```
    {: pre}


## Pull images from another registry to your local machine to use them in {{site.data.keyword.registrylong_notm}}
{: #registry_images_pulling}

1.  Log in to the CLI:

    ```
    bx cr login
    ```
    {: pre}

    **Note:** You must log in if you pull an image from your private {{site.data.keyword.registrylong_notm}}.

2.  Download (*pull*) the image to your local machine. Replace &lt;source_image&gt; with the repository of the image and &lt;tag&gt; with the tag of the image that you want to use, e.g., latest.

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Example:

    ```
    docker pull hello-world:latest
    ```
    {: pre}

3.  Tag the image.Replace &lt;source_image&gt; with the repository and &lt;tag&gt; with the tag of your local image that you pulled earlier. Define the repository and tag of the image that you want to use in your namespace by replacing &lt;new_image_repo&gt; and &lt;new_tag&gt;.

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    Example:

    ```
    docker tag hello-world:latest registry.<region>.bluemix.net/my_namespace/hw_repo:1
    ```
    {: pre}


## Push Docker images to your namespace in {{site.data.keyword.registrylong_notm}}
{: #registry_images_pushing}

1.  Upload (push) the image to your namespace. Replace &lt;my_namespace&gt; with the namespace where you want to upload your image, and &lt;image_repo&gt; and &lt;tag&gt; with the repository and the tag of the image that you chose when you tagged the image.

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    Example:

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/hw_repo:1
    ```
    {: pre}

2.  Verify that the image was pushed successfully by running the following command.

    ```
    bx cr image-list
    ```
    {: pre}


Good work! You set up a namespace in {{site.data.keyword.registrylong_notm}} and pushed your first image to your namespace.

**What's next?**

-   [Managing image security with Vulnerability Advisor](../va/va_index.html).
-   [Review your service plans and usage](registry_overview.html#registry_plans)
-   [Store and manage more images in your namespace](registry_images_.html).
-   [Create and deploy a container from your image to a Kubernetes cluster](../../containers/cs_cluster.html).

