---

copyright:
  years: 2018, 2025
lastupdated: "2025-04-23"

keywords: public images, commands, questions, registry, Vulnerability Advisor, frequently asked questions, namespace, tool, image, digest, access, region, package manager, security notices, version of a package

subcollection: Registry

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for {{site.data.keyword.registryshort_notm}}
{: #registry_faq}

Frequently asked questions for {{site.data.keyword.registrylong}}.
{: shortdesc}

For frequently asked questions about Vulnerability Advisor, see [FAQ for Vulnerability Advisor](/docs/Registry?topic=Registry-registry_faq_va).

## Where is the reference documentation for {{site.data.keyword.registryshort}}?
{: #faq_ref_docs}
{: faq}

The reference documentation for {{site.data.keyword.registrylong_notm}} is available in the {{site.data.keyword.cloud_notm}} documentation. For more information, see [About {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_overview) and [{{site.data.keyword.registrylong_notm}} CLI](/docs/Registry?topic=Registry-containerregcli).

## How do I set up the {{site.data.keyword.registryshort}} CLI?
{: #faq_setup_cli}
{: faq}

To set up the {{site.data.keyword.registrylong_notm}} CLI, use the following steps:
1. Ensure that the {{site.data.keyword.cloud_notm}} CLI is installed.
2. Install the `container-registry` CLI plug-in by running the command `ibmcloud plugin install container-registry`.
3. Log in to {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command.
4. Verify the installation by checking the current version of the `container-registry` CLI plug-in with the command `ibmcloud plugin list`.

Now you can use the {{site.data.keyword.registrylong_notm}} CLI to manage your registry and its resources for your {{site.data.keyword.cloud_notm}} account.

For more information, see [Setting up the {{site.data.keyword.registryshort}} CLI and namespace](/docs/Registry?topic=Registry-registry_setup_cli_namespace) and [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started).

## How do I configure my firewall to allow connections to {{site.data.keyword.registryshort}}?
{: #faq_firewall}
{: faq}

You can use a [Layer 7 firewall](https://nordlayer.com/learn/firewall/layer-7/){: external} with the domains listed in [Accessing {{site.data.keyword.registryshort}} through a firewall](/docs/Registry?topic=Registry-registry_firewall) or use a [virtual private network (VPN)](/docs/iaas-vpn?topic=iaas-vpn-getting-started).

## How many namespaces can you have?
{: #faq_namespace}
{: faq}

You can have 100 registry namespaces in each region.

## Can I rename a namespace?
{: #faq_namespace_rename}
{: faq}

You can't rename a [namespace](#x2031005){: term}. If you want to change the name of the namespace, you must create a namespace with the new name and transfer its data. To transfer its data, you can copy the contents of the existing namespace into the namespace that you created.

If you don't want to transfer data manually, you can create a script for this action by using the [`ibmcloud cr image-tag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_tag) command. For example, you can use the following script, where `OLD_NAMESPACE` is the existing namespace and `NEW_NAMESPACE` is the namespace that you created:

```txt
IMAGES=$(icr images --restrict OLD_NAMESPACE --format "{{ .Repository }}:{{ .Tag }}")

for i in $IMAGES ; do
   new=$(echo $i | sed "s|/OLD_NAMESPACE/|/NEW_NAMESPACE/|1")
   ibmcloud cr image-tag $i $new
done
```
{: codeblock}

## Why don't I have authorization to create a namespace?
{: #faq_auth_namespace}
{: faq}

You are not authorized to create a namespace in {{site.data.keyword.registrylong_notm}}. The error message `You are not authorized to access the specified resource.` indicates that you lack the necessary user permissions for working with namespaces. To add, assign, and remove namespaces, you must have the Manager role in the {{site.data.keyword.registryshort}} service at the account level. If you have the Manager role on the resource group, or resource groups, it is not sufficient; the Manager role must be at the account level.

For more information, see [Why aren't I authorized to access a specified resource in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-namespace-auth) and [User permissions for working with namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan_perm).

## How do I list image names?
{: #faq_list_images}
{: faq}

To list all the images in your {{site.data.keyword.cloud_notm}} account, you can run the `ibmcloud cr images` command, which displays all tagged images in your {{site.data.keyword.cloud_notm}} account with a truncated digest. If you want to list all your images with the complete digest, including untagged images, run the `ibmcloud cr image-digests` command. The image name is in either the format `repository@digest` or `repository:tag`. The values for repository, digest, and tag are returned when you run the commands.

For more information, see [`ibmcloud cr image-list` (`ibmcloud cr images`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) and [`ibmcloud cr image-digests` (`ibmcloud cr digests`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests).

## How do you list public images?
{: #faq_list_public_images}
{: faq}

To list public images, run the following `ibmcloud` commands to target the global registry and list the public images that are provided by {{site.data.keyword.IBM_notm}}:

```txt
ibmcloud cr region-set global
```
{: pre}

```txt
ibmcloud cr images --include-ibm
```
{: pre}

## What tools can I use to build and push images?
{: #faq_tools}
{: faq}

You can use Docker and non-Docker tools to build and push images to the registry. You can use non-Docker tools that support [OCI container image](#x9860419){: term} format and protocol. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).

## Do images in the trash count toward my quota?
{: #faq_trash}
{: faq}

Images that are in the trash don't count toward your quota.

## How do I find the image digest?
{: #faq_digest}
{: faq}

You can find the long format of the image [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) by running one of the following commands. The digest is displayed in the **Digest** column of the CLI.

When you're using the digest to identify an image, always use the long format.
{: note}

- Run the [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) command:

    ```txt
    ibmcloud cr image-digests
    ```
    {: pre}

- Run the [`ibmcloud cr image-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) command:

    ```txt
    ibmcloud cr image-list --no-trunc
    ```
    {: pre}

    If you run the `ibmcloud cr image-list` command without the `--no-trunc` option, you see the truncated format of the digest.
    {: note}

## How do I use digests to work with images?
{: #faq_digest_use}
{: faq}

The [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) identifies an image by using the `sha256` hash of the [image manifest](/docs/Registry?topic=Registry-registry_overview#overview_elements_manifest).

To find the digests for your images, run the [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) command. You can refer to an image by using a combination of the content of the **Repository** column (`repository`) and the **Digest** column (`digest`) separated by an at (`@`) symbol to create the image name in the format `repository@digest`.

## Why can't I push the image into {{site.data.keyword.registryshort}}?
{: #faq_push_images}
{: faq}

You might have issues when you are pulling or pushing images to {{site.data.keyword.registryshort}} because of various reasons such as exceeding the image storage or pull traffic quota, or invalid credentials. To resolve this issue, log in to {{site.data.keyword.cloud_notm}} and the {{site.data.keyword.registrylong_notm}} CLI, review quota limits and usage, and consider upgrading to a standard plan if you are on a free plan.

For more information, see [Why can't I push or pull a Docker image when I use {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-push-pull-docker) for assistance.

## How do I list images that are more than a year old?
{: #faq_images_year_old}
{: faq}

[Linux]{: tag-linux} [macOS]{: tag-macos} On Linux&reg; and macOS, if you want to list all images, both tagged and untagged that were created more than a year ago, you can run the following command:

```txt
year=$(($(date +%s) - 31556952))
ibmcloud cr digests --format '{{ if (lt .Created '$year')}}{{.Repository}}:{{.Digest}}{{end}}'
```
{: pre}

## How do you use access control?
{: #faq_access_control}
{: faq}

You can create {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) policies to control access to your namespaces in {{site.data.keyword.registrylong_notm}}. For more information, see [Granting access to {{site.data.keyword.registrylong_notm}} resources tutorial](/docs/Registry?topic=Registry-iam_access) and [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).

## How can I share access to an image?
{: #faq_share_image}
{: faq}

To access an image, a user must be a member of the {{site.data.keyword.cloud_notm}} account that owns the images. After the user is added to the account, appropriate IAM policies must be created to assign access.

For more information, see [Defining IAM access policies](/docs/Registry?topic=Registry-user).

## Do I have any untagged images?
{: #faq_untagged_image_1}
{: faq}

To find out whether you have any [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, list your images by running the [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) command. Untagged images have a hyphen (-) in the **Tags** column.

## Do I need untagged images?
{: #faq_untagged_image_2}
{: faq}

If you have active containers that are running [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, you must retain the untagged images. If you delete untagged images that are in use, you can cause problems with scaling or automated restarts. Deleting untagged images might cause a problem in the following circumstances:

- The image was deployed by using the digest as the reference. For example, {{site.data.keyword.codeenginefull_notm}} does resolve and use an image digest when it is serving applications, see [Deploying app workloads from images in a public registry](/docs/codeengine?topic=codeengine-deploy-app&interface=ui).
- The image reference was mutated by a webhook service, such as [Portieris](/docs/Registry?topic=Registry-security_enforce_portieris).

## What are eligible images?
{: #faq_eligible_image}
{: faq}

If you're cleaning up images by using retention policies, only eligible images are cleaned up. Images that are always retained are [Cloud Native Buildpacks](https://buildpacks.io/){: external} and [Google distroless](https://github.com/GoogleContainerTools/distroless){: external} images with the build date set to a specific constant rather than the real build time or with no build timestamp at all, and manifest lists. Images that are always retained are not eligible images.

The images that are not eligible are still displayed, but they do not count toward the total number of images that is set in the retention policy and are not removed.

Images created before `2013-01-19T00:13:39Z` are excluded from retention policy evaluation.

For more information, see [Planning retention](/docs/Registry?topic=Registry-registry_retention#retention_plan).

## What regions are available?
{: #faq_regions}
{: faq}

To find out more about the regions that are available for {{site.data.keyword.registrylong_notm}}, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## How do I get the `docker pull` command to return the most recent version?
{: #faq_docker_pull}
{: faq}

To find the most recent image, run the `ibmcloud cr image-list` command rather than the `docker pull` command. To make it easier to find the most recent image, define a different sequential tag for your images every time, and do not rely on the latest tag.

For more information, see [Why can't I pull the newest image by using the latest tag in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-docker-latest) for assistance.

## Why do my pods fail with an `ImagePullBackOff` error?
{: #faq_imagepullbackoff}
{: faq}

Your cluster uses an API key that is stored in an image pull secret to authorize the cluster to pull images from {{site.data.keyword.registrylong_notm}}, or the image with the specific tag does not exist in the repository. To fix it, make sure that you're using the correct name and tag for the image, that you have enough pull traffic and storage quota, and that you have an image pull secret in your namespace.

For more information, see [Why do images fail to pull from registry with ImagePullBackOff or authorization errors?](/docs/Registry?topic=Registry-ts-app-image-pull) for assistance.

## Why am I getting an exceeded quota error?
{: #faq_quota_error}
{: faq}

You exceeded your image storage or pull traffic quota for the current month. This means that you used more quota than your account allows for the month. To resolve this issue, you can either review your quota limits and increase them as necessary, or if you're on the lite plan upgrade to the standard plan.

For more information, see [Why am I getting errors about my quota in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-quota) and [Staying within quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup).
