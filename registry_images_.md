---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Adding images to your namespace
{: #registry_images_}

You can securely store and share Docker images with other users by adding images to your namespace in {{site.data.keyword.registrylong}}.
{:shortdesc}

Every image that you want to add to your namespace must exist on your local machine first. You can either download (pull) an image from another repository to your local machine, or build your own image from a Dockerfile by using the Docker `build` command. To add an image to your namespace, you must upload (push) the local image to your namespace in {{site.data.keyword.registrylong_notm}}.


## Pulling images from another registry
{: #registry_images_pulling}

You can pull (download) an image from any private or public registry source, and then tag it for later use in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}



Before you begin:

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in {{site.data.keyword.registrylong_notm}}](registry_setup_cli_namespace.html#registry_namespace_add).
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `bx login`, `bx cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `bx login` command again.


Download the image, see [Pull an image](index.html#registry_images_pulling) in the Getting Started documentation.

  **Tip:** If you get an "unauthorized: authentication required" or a "denied: requested access to the resource is denied" message, run the `bx cr login` command.


After you pull an image and tag it for your namespace, you can upload (push) the image from your local machine to your namespace.

## Pushing Docker images to your namespace
{: #registry_images_pushing}

You can push (upload) an image to your namespace in {{site.data.keyword.registrylong_notm}} to securely store and share your image with other users.
{:shortdesc}



Before you begin:

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry](registry_setup_cli_namespace.html#registry_namespace_add).
- [Pull](#registry_images_pulling) or [build](#registry_images_creating) an image on your local machine and tag the image with your namespace information.
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `bx login`, `bx cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `bx login` command again.


To upload (push) an image, follow these steps.

1. Log in to the CLI:

  ```
  bx cr login
  ```
  {: pre}

  **Note:** You must log in if you pull an image from your private {{site.data.keyword.registrylong_notm}}.

2. To view all namespaces that are available in your account, run the `bx cr namespace-list` command.
3. [Upload the image to your namespace.](index.html#registry_images_pushing)

  **Tip:** If you get an "unauthorized: authentication required" or a "denied: requested access to the resource is denied" message, run the `bx cr login` command.


After you push your image to your private registry, you can:

- [Manage security with Vulnerability Advisor](../va/va_index.html) to find information about potential security issues and vulnerabilities.
- [Create a cluster and use this image to deploy a container](../../containers/container_index.html) to the cluster in {{site.data.keyword.containerlong_notm}}.

## Copying images between registries
{: #registry_images_copying}

You can pull an image from a registry in one region and push it to a registry in another region so that you can share the image with users in both regions.
{:shortdesc}



Before you begin:

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry](registry_setup_cli_namespace.html#registry_namespace_add).
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `bx login`, `bx cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `bx login` command again.


To copy an image between two registries, follow these steps.

1. [Pull an image from a registry](#registry_images_pulling).
2. [Push the image to another registry](#registry_images_pushing). Make sure that you use the correct domain name for the new region you're targeting.

After you copied your image, you can:

- [Managing image security with Vulnerability Advisor](../va/va_index.html) to find information about potential security issues and vulnerabilities.
- [Create a cluster and use this image to deploy a container](../../containers/container_index.html) to the cluster in {{site.data.keyword.containerlong_notm}}.

## Building Docker images to use them with your namespace
{: #registry_images_creating}

You can build a Docker image directly in {{site.data.keyword.Bluemix_notm}} or create your own Docker image on your local machine and upload (push) it to your namespace in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Before you begin:

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry](registry_setup_cli_namespace.html#registry_namespace_add).
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `bx login`, `bx cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `bx login` command again.


A Docker image is the basis for every container that you create. An image is created from a Dockerfile, which is a file that contains instructions to build the image. A Dockerfile might reference build artifacts in its instructions that are stored separately, such as an app, the app's configuration, and its dependencies.

If you want to take advantage of {{site.data.keyword.Bluemix_notm}} compute resources and internet connection or Docker is not installed on your workstation, build your image directly in {{site.data.keyword.Bluemix_notm}}. If you need to access resources in your build that are on servers that are behind your firewall, build your image locally.

To build your own Docker image, complete the following steps:

1. Create a local directory where you want to store the build context. The build context contains your Dockerfile and related build artifacts, such as the app code. Navigate to this directory in a command line window.
2. Create a Dockerfile.
  1. Create a Dockerfile in your local directory.

    ```
    touch Dockerfile
    ```
    {: pre}

  2. Use a text editor to open the Dockerfile. At a minimum, you must add the base image to build your image from. Replace _&lt;source_image&gt;_ and _&lt;tag&gt;_ with the image repository and tag that you want to use. If you are using an image from another private registry, define the full path to the image in this private registry.

    ```
    FROM <source_image>:<tag>
    ```
    {: pre}

    Example to create a Dockerfile that is based on the public {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty (ibmliberty) image:

    ```
    FROM registry.<region>.bluemix.net/ibmliberty:latest
    LABEL description="This is my test Dockerfile"
    EXPOSE 9080
    ```
    {: pre}

    This example adds a label to the image metadata and exposes port 9080. For more Dockerfile instructions that you can use, see the [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/).

3. Decide on a name for your image. The image name must be in the following format:

  ```
  registry.<region>.bluemix.net/<my_namespace>/<repo_name>:<tag>
  ```
  {: pre}

  where _&lt;my_namespace&gt;_ is your namespace information, _&lt;repo_name&gt;_ is the name of your repository, and _&lt;tag&gt;_ is the version that you want to use for your image. To find your namespace, run the `bx cr namespace-list` command.

4. Take note of the path to the directory that contains your Dockerfile. If you run the commands in the following steps while your working directory is set to where your build context is stored, you can replace _&lt;directory&gt;_ with a period (.).
5. Choose to either build your image directly in {{site.data.keyword.Bluemix_notm}} or build and test your image locally before you push it to {{site.data.keyword.Bluemix_notm}}.
  - To build the image directly in {{site.data.keyword.Bluemix_notm}}, run the following command:

    ```
    bx cr build -t <image_name> <directory>
    ```
    {: pre}

    where _&lt;image_name&gt;_ is the name of your image and _&lt;directory&gt;_ is the path to the directory.

    For more information about the `bx cr build` command, see [{{site.data.keyword.registrylong_notm}} CLI](../../cli/plugins/registry/index.html#containerregcli).

  - To build and test your image locally before you push it to {{site.data.keyword.Bluemix_notm}}, complete the following steps:
    1. Build the image from your Dockerfile on your local machine and tag it with your image name.

      ```
      docker build -t <image_name> <directory>
      ```
      {: pre}

      where _&lt;image_name&gt;_ is the name of your image and _&lt;directory&gt;_ is the path to the directory.

    2. Optional: Test your image on your local machine before you push it to your namespace.

      ```
      docker run <image_name>
      ```
      {: pre}

      Replace _&lt;image_name&gt;_ with the name of your image.

    3. After you create your image and tag it for your namespace, [you can push your image to your namespace private registry](#registry_images_pushing).

To use Vulnerability Advisor to check the security of your image, see [Managing image security with Vulnerability Advisor](../va/va_index.html).

## Removing images from your private {{site.data.keyword.Bluemix_notm}} images registry
{: #registry_images_remove}

You can remove unwanted images from your private image registry.
{:shortdesc}

Before you begin, remove any containers that are using the image.

Public {{site.data.keyword.IBM_notm}} images cannot be removed from your private {{site.data.keyword.Bluemix_notm}} registry, and do not count towards your quota.

1. Log in to {{site.data.keyword.Bluemix_notm}} by running the `bx login` command.
2. To remove an image, run the following command:

  ```
  bx cr image-rm IMAGE
  ```
  {: pre}

  Where _IMAGE_ is the full {{site.data.keyword.Bluemix_notm}} registry path to the image that you want to remove, in the format `namespace/image:tag`.

  If a tag is not specified in the image path, the image tagged `latest` is deleted by default. You can delete multiple images by listing each private {{site.data.keyword.Bluemix_notm}} registry path in the command with a space between each path.

  **Tip:** You can run the `bx cr namespace-list` command to retrieve your namespace value.

3. Verify that the image was removed by running the following command, and check that the image does not appear in the list.

  ```
  bx cr image-list
  ```
  {: pre}
