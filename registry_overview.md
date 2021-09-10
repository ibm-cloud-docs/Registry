---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-10"

keywords: private Docker images, scalable private image registry, regions, plans, billing, registry, service plans, quotas, costs, domain names, Docker, global registry, registry, elements, components

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.registrylong_notm}}
{: #registry_overview}

Use {{site.data.keyword.registrylong}} to store and access private container images in a highly available and scalable architecture.
{: shortdesc}

{{site.data.keyword.registrylong_notm}} provides a multi-tenant, highly available, scalable, and encrypted private image registry that is hosted and managed by {{site.data.keyword.IBM}}. You can use {{site.data.keyword.registrylong_notm}} by setting up your own image namespace and pushing container images to your namespace.

![Image showing how you can interact with IBM Cloud Container Registry.](images/registry_architecture1.svg "Image showing how you can interact with {{site.data.keyword.registrylong_notm}}. {{site.data.keyword.registrylong_notm}} contains both private and public repositories, and APIs to interact with the service. Your local Docker client can pull and push images to and from your private repositories in the registry, and can pull public repositories. The {{site.data.keyword.cloud_notm}} web UI (console) interacts with the {{site.data.keyword.registrylong_notm}} API to list images. The {{site.data.keyword.registrylong_notm}} CLI interacts with the API to list, create, inspect, and remove images, as well as other administrative functions. Your local Docker client can also pull and push images from your local image store to other registries."){: caption="Figure 1. How {{site.data.keyword.registrylong_notm}} interacts with your Docker images" caption-side="bottom"}

A Docker image is the basis for every container that you create. An image is created from a Dockerfile, which is a file that contains instructions to build the image. A Dockerfile might reference build artifacts in its instructions that are stored separately, such as an app, the app's configuration, and its dependencies. Images are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry). By using {{site.data.keyword.registrylong_notm}}, only users with access to your {{site.data.keyword.cloud_notm}} account can access your images.

When you push images to {{site.data.keyword.registrylong_notm}}, you benefit from the built-in Vulnerability Advisor features that scan for potential security issues and vulnerabilities. Vulnerability Advisor checks for vulnerable packages in specific Docker base images, and known vulnerabilities in app configuration settings. When vulnerabilities are found, information about the vulnerability is provided. You can use this information to resolve security issues so that containers are not deployed from vulnerable images.

Review the following table to find an overview of benefits of using {{site.data.keyword.registrylong_notm}}.

| Benefit | Description |
|---------|-------------|
| Highly available and scalable private registry. | Set up your own image namespace in a multi-tenant, highly available, scalable, encrypted private registry that is hosted and managed by {{site.data.keyword.IBM_notm}}.  \n  \n Store your private Docker images and share them with users in your {{site.data.keyword.cloud_notm}} account. |
| Image security compliance with Vulnerability Advisor. | Benefit from automatic scanning of images in your namespace.  \n  \n Review recommendations that are specific to the operating system to fix potential vulnerabilities and protect your containers from being compromised. |
| Quota limits for storage and pull traffic. | Benefit from free storage and pull traffic to your private images until you reach your free quota.  \n  \n Set custom quota limits for the amount of storage and pull traffic per month to avoid exceeding your preferred payment level. |
{: caption="Table 1. {{site.data.keyword.registrylong_notm}} benefits" caption-side="top"}

## Service plans
{: #registry_plans}

You can choose between the free or standard {{site.data.keyword.registrylong_notm}} service plans to store your Docker images and make these images available to users in your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

The {{site.data.keyword.registrylong_notm}} service plan determines the amount of storage and pull traffic that you can use for your private images. The service plan is associated with your {{site.data.keyword.cloud_notm}} account, and limits for storage and image pull traffic apply to all namespaces that you set up in your account.

Service plans are scoped to the specific registry instance (one of the regional registries or the global registry) that you are currently working with. Plan settings must all be managed separately for your account in each registry instance. For more information, see [Regions](#registry_regions).
{: note}

The following table shows available {{site.data.keyword.registrylong_notm}} service plans and their characteristics. For more information about how billing works and what happens when you exceed service plan limits, see [Quota limits and billing in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).

| Characteristics | Free | Standard |
|-----------------|------|----------|
| Description. | Try out {{site.data.keyword.registrylong_notm}} to store and share your Docker images. This plan is the default service plan when you set up your first namespace in {{site.data.keyword.registrylong_notm}}. | Benefit from unlimited storage and pull traffic usage to manage the Docker images for all namespaces in your {{site.data.keyword.cloud_notm}} account. |
| Amount of storage for images. | 500 MB | Unlimited |
| Pull traffic. | 5 GB per month | Unlimited |
| Billing. | If you exceed your storage or pull traffic limits, you cannot push or pull images to and from your namespace. For more information, see [Quota limits and billing in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing). | **Storage**. You are charged by Gigabyte-Months of usage. The first 0.5 GB-Months are free. Then, you are charged as stated in the offering details page, see [{{site.data.keyword.registryshort_notm}}](https://cloud.ibm.com/registry/catalog).  \n  \n **Pull traffic**. You are charged by Gigabyte usage per month. The first 5 GB are free. Then, you are charged as stated in the offering details page, see [{{site.data.keyword.registryshort_notm}}](https://cloud.ibm.com/registry/catalog). If you exceed your storage or pull traffic limits, you can't push or pull images to and from your namespace. For more information about storage, pull traffic, and the cost estimator, see [Quota limits and billing in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing). |
{: caption="Table 2. {{site.data.keyword.registrylong_notm}} plans" caption-side="top"}

## Quota limits and billing
{: #registry_plan_billing}

Find information and examples for how the billing process and quota limits work in {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

Every image is built from a number of layers that each represent an incremental change from the base image. When you push or pull an image, the amount of storage and pull traffic that is needed for each layer is added to your monthly usage. Identical layers are automatically shared between images in your {{site.data.keyword.cloud_notm}} account and are reused when you create other images. The storage for each identical layer is charged only once, regardless of how many images in your account reference the layer. Layers that are only referenced by deleted images in the trash are not charged.

Quota limits and billing are scoped to the specific registry instance (one of the regional registries or the global registry) that you are currently working with. Quota settings must be managed separately for your account in each registry instance. For more information, see [Regions](#registry_regions).
{: note}

The following example is for pushing images:
:   You push an image to your namespace that is based on the Ubuntu image. The Ubuntu image contains several layers. Because you do not have these layers in your account yet, the amount of storage that these layers require is added to your monthly usage.

    Later, you create a second image that is based on the Ubuntu image. You change the Ubuntu base image, such as by adding more commands or files to your Dockerfile. Each change represents a new image layer. When you push the second image, {{site.data.keyword.registrylong_notm}} recognizes that all layers of the base Ubuntu image are already stored in your account. You are not charged for storing these layers a second time, even if you pushed your image to another namespace. {{site.data.keyword.registrylong_notm}} determines the size of all new layers and adds the amount of storage to your monthly usage.

### Billing for storage and pull traffic
{: #registry_billing_traffic}

Depending on the service plan that you choose, you are charged for the storage and pull traffic that you use per month in each region.
{: shortdesc}

#### Storage
{: #registry_billing_traffic_storage}

Every {{site.data.keyword.registrylong_notm}} service plan comes with a certain amount of storage that you can use to store your Docker images in the namespaces of your {{site.data.keyword.cloud_notm}} account. If you are on the standard plan, you are charged by GB-Months of usage. The first 0.5 GB-Months are free. If you are on the free plan, you can store your images in {{site.data.keyword.registrylong_notm}} for free until you reach the quota limits for the free plan. A GB-Month is an average of 1 GB of storage for a month (730 hours).
{: shortdesc}

The following example is for the standard plan:
:   You use 5 GB for exactly half the month and then you push several images to your namespace and use 10 GB for the rest of the month. Your monthly usage is calculated as shown in the following example:

    (5 GB x 0.5 (months)) + (10 GB x 0.5 (months)) = 2.5 + 5 = 7.5 GB-Months

    In the standard plan, the first 0.5 GB-Months are free, so you get charged for 7 GB-Months (7.5 GB-Months - 0.5 GB-Months).

#### Pull traffic
{: #registry_billing_traffic_pull_traffic}

Every {{site.data.keyword.registrylong_notm}} service plan includes a certain amount of free pull traffic to your private images that are stored in your namespace. Pull traffic is the bandwidth that you use when you pull a layer of an image from your namespace to your local computer. If you are on the standard plan, you are charged by GB of usage per month. The first 5 GB each month is free. If you are on the free plan, you can pull images from your namespace until you reach the quota limit for the free plan.
{: shortdesc}

The following example is for the standard plan:
:   In the month, you pulled images that contain layers with a total size of 14 GB. Your monthly usage is calculated as shown in the following example:

    In the standard plan, the first 5 GB per month is free, so you get charged for 9 GB (14 GB - 5 GB).

### Quota limits for storage and pull traffic
{: #registry_quota_limits}

Depending on the service plan that you choose, you can push and pull images to and from your namespace until you reach your plan-specific or custom quota limits for each region.
{: shortdesc}

#### Storage
{: #registry_quota_limits_storage}

When you reach or exceed the quota limits for your plan, you can't push any images to the namespaces in your {{site.data.keyword.cloud_notm}} account until you complete one of the following tasks.

- [Free up space by removing images](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup) from your namespaces.
- [Upgrade to the standard plan](#registry_plan_upgrade).
- If you set quota limits for storage in your free or standard plan, you can also [increase this quota limit](/docs/Registry?topic=Registry-registry_quota#registry_quota_set) to enable the pushing of new images again.

The following example is for the standard plan:
:   Your current quota limit for storage is set to 1 GB. All private images that are stored in the namespaces of your {{site.data.keyword.cloud_notm}} account already use 900 MB of this storage. You have 100 MB storage available until you reach your quota limit. One user wants to push an image with a size of 2 GB on the local computer. Because the quota limit is not yet reached, {{site.data.keyword.registrylong_notm}} allows the user to push this image.

    After the push, {{site.data.keyword.registrylong_notm}} determines the actual size of the image in your namespace, which can vary from the size on your local computer, and checks whether the limit for storage is reached. In this example, the storage usage increases from 900 MB by 2 GB. With your current quota limit set to 1 GB, {{site.data.keyword.registrylong_notm}} prevents you from pushing more images to the namespace.

#### Pull traffic
{: #registry_quota_limits_pull_traffic}

When you reach or exceed the quota limits for your plan, you can't pull any images from the namespaces in your {{site.data.keyword.cloud_notm}} account until you complete one of the following tasks.

- Wait for the next billing period to start.
- [Upgrade to the standard plan](#registry_plan_upgrade).
- [Increase your quota limits for pull traffic](/docs/Registry?topic=Registry-registry_quota#registry_quota_set).

The following example is for the standard plan:
:   In the month, your quota limit for pull traffic is set to 5 GB. You already pulled images from your namespaces and used 4.5 GB of this pull traffic. You have 0.5 GB pull traffic available until you reach your quota limit. One user wants to pull an image from your namespace with a size of 1 GB. Because the quota limit is not yet reached, {{site.data.keyword.registrylong_notm}} allows the user to pull this image.

    After the image is pulled, {{site.data.keyword.registrylong_notm}} determines the bandwidth that you used during the pull and checks whether the limit for pull traffic is reached. In this example, the pull traffic usage increases from 4.5 GB to 5.5 GB. With your current quota limit set to 5 GB, {{site.data.keyword.registrylong_notm}} prevents you from pulling images from your namespace.

### Cost
{: #registry_cost}

You can see the costs of {{site.data.keyword.registrylong_notm}} in the pricing plans section of the offering details page, see [{{site.data.keyword.registryshort_notm}}](https://cloud.ibm.com/registry/catalog).
{: shortdesc}

## Upgrading your service plan
{: #registry_plan_upgrade}
{: help}
{: support}

You can upgrade your service plan to benefit from unlimited storage and pull traffic usage to manage the Docker images for all namespaces in your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

If you want to find out what service plan you have for the registry region that you're targeting, run the `ibmcloud cr plan` command.
{: tip}

To upgrade your service plan, complete the following steps.

1. Log in to {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

    If you have a federated ID, use `ibmcloud login --sso` to log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your username and use the provided URL in your CLI output to retrieve your one-time passcode. If you have a federated ID, the login fails without the `--sso` and succeeds with the `--sso` option.
    {: tip}

2. Target the region for which you want to upgrade the plan.

    ```
    ibmcloud cr region-set
    ```
    {: pre}

    For more information, see [`ibmcloud cr region-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) and [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

3. Upgrade to the standard plan.

    ```
    ibmcloud cr plan-upgrade standard
    ```
    {: pre}

    If you have an {{site.data.keyword.cloud_notm}} lite plan, you must upgrade to an {{site.data.keyword.cloud_notm}} Pay-as-you-go or Subscription account before you run `ibmcloud cr plan-upgrade`.
    {: tip}

    For more information, see [`ibmcloud cr plan-upgrade`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade).

## Find out more about the elements that are used in {{site.data.keyword.registrylong_notm}}
{: #overview_elements}

Information about the elements that are used in {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

To learn more about Docker-specific terms, see [Docker glossary](https://docs.docker.com/glossary/){: external}.

### Container image
{: #overview_elements_container_image}

A file system and its execution parameters that are used within a container runtime to create a container. The file system consists of a series of layers, which are combined at run time, that are created as the container image is built by successive updates. The container image does not retain state as the container runs.

Container images are stored in a repository that is stored in a namespace.

### Dockerfile
{: #overview_elements_dockerfile}

A Dockerfile is a text file that contains instructions to build a Docker image.

Typically, a container image is built upon a base image that contains a base operating system, such as Ubuntu. You can incrementally change the base image with your Dockerfile instructions to define the environment that the app needs to run. Every change to the base image describes a new layer of the image, and you can make multiple changes in a single Dockerfile line. The instructions in a Dockerfile also might reference build artifacts that are stored separately, such as an app, the app's configuration, and its dependencies. For more information about Dockerfile, see [Dockerfile reference](https://docs.docker.com/engine/reference/builder/){: external}.

### Docker V2 container images
{: #overview_elements_dockerv2_images}

A container image that is compliant with the [Docker: Image Manifest V2, Schema 2](https://docs.docker.com/registry/spec/manifest-v2-2/){: external} specification.

The media type for Docker Image Manifest V2, Schema 2 is `application/vnd.docker.distribution.manifest.v2+json` and the media type for the manifest list is `application/vnd.docker.distribution.manifest.list.v2+json`. A Docker V2 container image is a type of OCI container image. For more information about support for Docker, see [Docker](/docs/Registry?topic=Registry-registry_overview#docker).

### OCI container images
{: #overview_elements_oci_images}

A container image that is compliant with the [OCI Image Format](https://github.com/opencontainers/image-spec){: external} specification.

The media type for OCI container images is `application/vnd.oci.image.manifest.v1+json`.

### Registry
{: #overview_elements_registry}

A public or private container image storage and distribution service.

Storage is provided for OCI container images (also known as Docker container images). OCI container images can be accessed or "pulled" by OCI clients that use the appropriate registry domain name. Container images can be accessed by anyone (public images) or access can be limited to a group (private images). {{site.data.keyword.registrylong_notm}} provides a multi-tenant, highly available, private image registry that is hosted and managed by {{site.data.keyword.IBM_notm}}. You can use the registry by adding a namespace that is private to your account and then push images to your namespace.

### Registry namespace
{: #overview_elements_namespace}

A collection of repositories that store your container images in {{site.data.keyword.registrylong_notm}}. The registry namespace is associated with your {{site.data.keyword.cloud_notm}} account. You can have multiple registry namespaces in an account.

A registry namespace is made up of one or more repositories.

When you set up your own namespace in {{site.data.keyword.registrylong_notm}}, the namespace is appended to the registry URL, `<region>.icr.io/my_namespace`. The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Every user in your {{site.data.keyword.cloud_notm}} account can view and work with images that are stored in your registry namespace.

You can have 100 namespaces in each region.
{: note}

From version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, when you create a namespace, it is created in the resource group that you specify so that you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. If you don't specify a resource group, and a resource group isn't targeted, the default resource group is used.

Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the {{site.data.keyword.cloud_notm}} console before 29 July 2020 aren't created in resource groups. If you have an existing namespace that is not in a resource group, you can assign the namespace to a resource group and then set permissions for that namespace at the resource group level. For more information about resource groups, see [Assigning existing namespaces to resource groups](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_assign).

Namespaces that are assigned to a resource group show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.

### Repository
{: #overview_elements_repository}

A collection of related container images in the container registry that are distinguished by tag or digest only.

Repository is often used interchangeably with container image, but a repository potentially holds multiple tagged variants of a container image.

A repository stores container images, and is itself stored in a registry namespace.

### Tag
{: #overview_elements_tag}

A label that you can reassign that identifies container images within a repository.

You can use tags to distinguish different versions of the same base image within a repository. When you run a Docker command and do not specify the tag of a repository image, then the image tagged `latest` is used by default.

### Untagged image
{: #overview_elements_untagged}

An image that has no tag is an untagged image. Images that are untagged can be referenced by using the digest reference format `<repository>@<digest>` as opposed to the tag reference format `<repository>:<tag>`. Untagged images are typically the result of an image that is pushed with a pre-existing `<repository>:<tag>` combination. In this case, the tag is overwritten and the original image becomes untagged.

You can view untagged images by using the [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) command, and clean up untagged images by using the [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged) command.

## Regions
{: #registry_regions}

The default instance of {{site.data.keyword.registrylong_notm}} is the global registry. The global registry doesn't include a region in its domain name (`icr.io`).
{: shortdesc}

Use the global instance of the registry unless you have a specific requirement, for example, data sovereignty, to store your data in a particular region. In which case, you can use {{site.data.keyword.registrylong_notm}} in [local regions](#registry_regions_local).

All registry artifacts are scoped to the specific registry instance (one of the regional registries or the global registry) that you are currently working with. For example, namespaces, images, quota settings, and plan settings must all be managed separately for your account in each registry instance.

### Global registry
{: #registry_regions_global}

A global registry is available. The global registry doesn't have a region included in its name (`icr.io`). In addition to hosting user namespaces and images, this registry also hosts public images that are provided by {{site.data.keyword.IBM_notm}}.
{: shortdesc}

The global instance of {{site.data.keyword.registrylong_notm}} is available by using the domain names that are shown in the following table.

| Registry | Domain name | Private domain name | Deprecated domain name |
|----------|-------------|----------------------|-----------------------|
| Global | `icr.io` | `private.icr.io` | `registry.bluemix.net` |
{: caption="Table 3. Domain name for the global registry" caption-side="top"}

To learn about connecting to {{site.data.keyword.registrylong_notm}} by using the private domain names, see [Using private network connections for image pushes and pulls](/docs/Registry?topic=Registry-registry_private#registry_private_images).

The existing `bluemix.net` domain names are deprecated, but you can continue to use them for the moment. An end of support date is not available yet.
{: deprecated}

#### Targeting the global registry
{: #registry_regions_global_target}

You can target the global registry by running the [`ibmcloud cr region-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) command.
{: shortdesc}

1. To target the global registry, run the following command.

    ```
    ibmcloud cr region-set global
    ```
    {: pre}

2. To log your local Docker daemon into the global registry, run the `ibmcloud cr login` command.

### Local regions
{: #registry_regions_local}

Regional instances of {{site.data.keyword.registrylong_notm}} are available by using the domain names that are shown in the following table.
{: shortdesc}

| Local registry region | Domain name | Private domain name | Deprecated domain name |
|-----------------------|-------------|---------------------|------------------------|
| `ap-north` | `jp.icr.io` | `private.jp.icr.io` | Not applicable |
| `ap-south` | `au.icr.io` | `private.au.icr.io` | `registry.au-syd.bluemix.net` |
| `br-sao` | `br.icr.io` | `private.br.icr.io` | Not applicable |
| `ca-tor` | `ca.icr.io` | `private.ca.icr.io` | Not applicable |
| `eu-central` | `de.icr.io` | `private.de.icr.io` | `registry.eu-de.bluemix.net` |
| `jp-osa` | `jp2.icr.io` | `private.jp2.icr.io` | Not applicable |
| `uk-south` | `uk.icr.io` | `private.uk.icr.io` | `registry.eu-gb.bluemix.net` |
| `us-south` | `us.icr.io` | `private.us.icr.io` | `registry.ng.bluemix.net` |
{: caption="Table 4. Domain names for local regions" caption-side="top"}

To learn about connecting to {{site.data.keyword.registrylong_notm}} by using the private domain names, see [Using private network connections for image pushes and pulls](/docs/Registry?topic=Registry-registry_private#registry_private_images).

The existing `bluemix.net` domain names are deprecated, but you can continue to use them for the moment. An end of support date is not available yet.
{: deprecated}

#### Targeting a local region
{: #registry_regions_local_target}
{: help}
{: support}

If you want to use a region other than your local region, you can target the region that you want to access by running the [`ibmcloud cr region-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) command. You can run the command with no options to get a list of available regions, or you can specify the region as an option.
{: shortdesc}

1. To run the command with options, replace `<region>` with the name of the [region](#registry_regions_local).

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

    For example, to target the `eu-central` region, run the following command.

    ```
    ibmcloud cr region-set eu-central
    ```
    {: pre}

2. To log your local Docker daemon into the registry so that you can push or pull images, run the `ibmcloud cr login` command.

## Support for Docker
{: #docker}

{{site.data.keyword.registrylong_notm}} supports Docker Engine V1.12.6, or later.

Docker is required only if you want to push or pull images.

Docker V2 Schema 2 images are supported. Manifest lists are also supported. For more information, see [Docker: Image Manifest Version 2, Schema 2](https://docs.docker.com/registry/spec/manifest-v2-2/){: external}.

Docker V2 Schema 1 images are discontinued and you can't push them to {{site.data.keyword.registrylong_notm}} anymore.
{: note}


