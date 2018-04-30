---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-30"

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
{:shortdesc}

The {{site.data.keyword.Bluemix_notm}} console includes a brief Quick Start. To find out more about how to use the {{site.data.keyword.Bluemix_notm}} console, see [Monitoring the vulnerability of images](registry_ui.html).

Do not put personal information in your container images, namespace names, description fields (for example, in registry tokens), or in any image configuration data (for example, image names or image labels).
{:tip}



## Install the {{site.data.keyword.registrylong_notm}} CLI
{: #registry_cli_install}

1.  Install the [{{site.data.keyword.Bluemix_notm}} CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://clis.ng.bluemix.net/ui/home.html) so that you can run the {{site.data.keyword.Bluemix_notm}} **bx** commands.
2.  Install the container-registry plug-in:

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}


## Set up a namespace
{: #registry_namespace_add}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Add a namespace to create your own image repository. Replace _&lt;my_namespace&gt;_ with your preferred namespace.

    ```
    bx cr namespace-add <my_namespace>
    ```
    {: pre}

3.  To ensure that your namespace is created, run the `bx cr namespace-list` command.

    ```
    bx cr namespace-list
    ```
    {: pre}


## Pull images from another registry to your local machine
{: #registry_images_pulling}

1.  [Install the Docker CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.docker.com/community-edition#/download). For Windows 8, or OS X Yosemite 10.10.x or earlier, install [Docker Toolbox ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.docker.com/products/docker-toolbox) instead.

2.  Log in to the CLI:

    ```
    bx cr login
    ```
    {: pre}

    **Note:** You must log in if you pull an image from your private {{site.data.keyword.registrylong_notm}}.

3.  Download (_pull_) the image to your local machine. Replace _&lt;source_image&gt;_ with the repository of the image and _&lt;tag&gt;_ with the tag of the image that you want to use, e.g., _latest_.

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Example, where _&lt;source_image&gt;_ is `hello-world` and _&lt;tag&gt;_ is `latest`:

    ```
    docker pull hello-world:latest
    ```
    {: pre}

4.  Tag the image. Replace _&lt;source_image&gt;_ with the repository and _&lt;tag&gt;_ with the tag of your local image that you pulled earlier. Replace _&lt;region&gt;_ with the name of your [region](registry_overview.html#registry_regions). Replace _&lt;my_namespace&gt;_ with the namespace that you created in [Set up a namespace](index.html#registry_namespace_add). Define the repository and tag of the image that you want to use in your namespace by replacing _&lt;new_image_repo&gt;_ and _&lt;new_tag&gt;_.

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    Example, where _&lt;source_image&gt;_ is `hello-world`, _&lt;tag&gt;_ is `latest`, _&lt;region&gt;_ is `eu-gb`, _&lt;my_namespace&gt;_ is `Namespace1`, _&lt;new_image_repo&gt;_ is `hw_repo`, and _&lt;new_tag&gt;_ is `1`:

    ```
    docker tag hello-world:latest registry.eu-gb.bluemix.net/Namespace1/hw_repo:1
    ```
    {: pre}


## Push Docker images to your namespace
{: #registry_images_pushing}

1.  Upload (_push_) the image to your namespace. Replace _&lt;my_namespace&gt;_ with the namespace that you created in [Set up a namespace](index.html#registry_namespace_add), and _&lt;image_repo&gt;_ and _&lt;tag&gt;_ with the repository and the tag of the image that you chose when you tagged the image.

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    Example, where _&lt;region&gt;_ is `eu-gb`, _&lt;my_namespace&gt;_ is `Namespace1`, _&lt;image_repo&gt;_ is `hw_repo`, and _&lt;tag&gt;_ is `1`:

    ```
    docker push registry.eu-gb.bluemix.net/Namespace1/hw_repo:1
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
