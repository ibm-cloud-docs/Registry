---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-05"

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

The reference documentation for {{site.data.keyword.registrylong_notm}} is available in the {{site.data.keyword.cloud_notm}} documentation. For more information, see [About {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_overview) and [{{site.data.keyword.registryshort}} CLI](/docs/Registry?topic=Registry-containerregcli).

## How do I set up the {{site.data.keyword.registryshort}} CLI?
{: #faq_setup_cli}
{: faq}

To set up the {{site.data.keyword.registrylong_notm}} command-line interface (CLI), use the following steps:
1. Ensure that the {{site.data.keyword.cloud_notm}} CLI is installed. To verify that it is installed, run the `ibmcloud help` command.
2. Install the `container-registry` CLI plug-in by running the command `ibmcloud plugin install container-registry`.
3. Log in to {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command.
4. Verify the installation by checking the current version of the `container-registry` CLI plug-in with the command `ibmcloud plugin list`.

Now you can use the {{site.data.keyword.registrylong_notm}} CLI to manage your registry and its resources for your {{site.data.keyword.cloud_notm}} account.

For more information, see [Setting up the {{site.data.keyword.registryshort}} CLI and namespace](/docs/Registry?topic=Registry-registry_setup_cli_namespace) and [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started).

## Why isn't `ibmcloud cr` a known command?
{: #faq_cr_unknown}
{: faq}

If you receive a message that says that `ibmcloud cr` isn't a registered command, the `container-registry` CLI plug-in either isn't installed or it's not up to date. See [Why do {{site.data.keyword.registryshort_notm}} (`ibmcloud cr`) commands fail with a message that they're not registered?](/docs/Registry?topic=Registry-troubleshoot-login-error) for assistance.

If you have issues with an unregistered command, it is likely that you don't have the most recent version of the plug-in. For more information about how to update the {{site.data.keyword.registryshort}} CLI, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).

## How do I configure my firewall to allow connections to {{site.data.keyword.registryshort}}?
{: #faq_firewall}
{: faq}

You can use a [Layer 7 firewall](https://nordlayer.com/learn/firewall/layer-7/){: external} with the domains that are listed in [Accessing {{site.data.keyword.registryshort}} through a firewall](/docs/Registry?topic=Registry-registry_firewall) or use a [virtual private network (VPN)](/docs/iaas-vpn?topic=iaas-vpn-getting-started).

## What is the name of my namespace?
{: #faq_namespace_2}
{: faq}

To find out the names of your namespaces, run the [`ibmcloud cr namespace-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list) command.

You can also use the API to list your namespaces by using the `GET /api/v1/namespaces` method.

For more information about namespaces, see [Registry namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace). To plan your namespaces, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan).

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

The error message `You are not authorized to access the specified resource.` indicates that you lack the necessary user permissions for working with namespaces.

See [Why aren't I authorized to access a specified resource in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-namespace-auth) for assistance.

## Why am I unable to create a namespace?
{: #faq_namespace_create}
{: faq}

If you're having problems when you try to add a namespace in {{site.data.keyword.registryshort_notm}}, it could be one of the following causes:

- Invalid characters are included in the namespace.
- The namespace is already in use.
- You're reusing a namespace that was deleted recently.
- You don't have the correct permissions to create a namespace.

See [Why can't I add a namespace in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-add-namespace) for assistance.

## How do I obtain image pull credentials for {{site.data.keyword.registryshort}}?
{: #faq_credentials}
{: faq}

For long-lived credentials, you want an API key that is associated with a service ID or user ID that has IAM reader permission on the namespace that contains the image. A user API key is associated with a user and their access policies. A service ID API key has its own access policies. You can create service ID API keys and user API keys manually in the {{site.data.keyword.cloud_notm}} console and in the CLI. For more information about API keys, see [Understanding API keys](/docs/account?topic=account-manapikey).

For security reasons, the API key is only available to be copied or downloaded at the time of creation. If the API key is lost, you must create a new API key.
{: tip}

You can create user API keys and service ID API keys in the {{site.data.keyword.cloud_notm}} console, the command-line interface (CLI), the API, and in Terraform. For more information about creating API keys, see [Managing user API keys](/docs/account?topic=account-userapikey&interface=ui) and [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys&interface=ui).

For more information about how to access {{site.data.keyword.registryshort}}, see [Accessing {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_access).

## How do I list image names?
{: #faq_list_images}
{: faq}

To list all the images in your {{site.data.keyword.cloud_notm}} account, you can run the `ibmcloud cr images` command, which displays all tagged images in your {{site.data.keyword.cloud_notm}} account with a truncated digest. If you want to list all your images with the complete digest, including untagged images, run the `ibmcloud cr image-digests` command. The image name is in either the format `repository@digest` or `repository:tag`. The values for repository, digest, and tag are returned when you run the commands.

For more information, see [`ibmcloud cr image-list` (`ibmcloud cr images`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) and [`ibmcloud cr image-digests` (`ibmcloud cr digests`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests).

## How do you list public images?
{: #faq_list_public_images}
{: faq}

To list public images, run the following `ibmcloud` commands to target the global registry and list the public images that are provided by {{site.data.keyword.IBM_notm}}:

1. Set the region to global by running the `ibmcloud cr region-set` command and entering `global` as the region.

```sh
ibmcloud cr region-set global
```
{: pre}

2. List the public images by running the `ibmcloud cr images` command with the `--include-ibm` option.

```sh
ibmcloud cr images --include-ibm
```
{: pre}

## Why are requests to {{site.data.keyword.registryshort}} timing out while I'm using the {{site.data.keyword.cloud_notm}} CLI?
{: #faq_requests_timeout}
{: faq}

The timeout issue when you are using the {{site.data.keyword.cloud_notm}} CLI with {{site.data.keyword.registryshort}} might be due to having many images in the account. To resolve this situation, you can use the `ibmcloud cr image-list` command with the `--restrict` option to narrow down the scope of the list and improve performance. Alternatively, if vulnerability reports are not needed, use the `ibmcloud cr image-list` command with the `--no-va` option. To manage the number of images, consider cleaning up your namespaces. For more information, see [Cleaning up your namespaces in {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_retention).

If you're following the [getting started instructions](/docs/Registry?topic=Registry-getting-started), the instructions assume that you're in your own account with permission to do everything. If you're a member of an account that is owned and administered by someone else, you might not have the correct permissions to configure and operate the registry service. Ask your administrator to add you to an existing access policy, or create an access policy that gives you the correct service access role for working with {{site.data.keyword.registryshort}}. For more information, see [Why can't I get started with {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-get-started) for assistance.

If {{site.data.keyword.registryshort}} commands fail with an error that states that they're not registered, install the `container-registry` CLI plug-in. Additionally, ensure that the `ibmcloud` CLI plug-in and the `container-registry` CLI plug-in are both up to date. If you want to use all the available commands and options, you must keep your CLIs current. To check the current version of your CLI plug-ins, run the `ibmcloud plugin list` command. See [Why isn't `ibmcloud cr` a known command?](#faq_cr_unknown) for assistance.

## How do I add multiple tags to a container image?
{: #faq_tags}
{: faq}

To add multiple tags to a container image you can use the `ibmcloud cr image-tag` command, but you need to run the command for each tag that you want to add. For example, if your image is named `us.icr.io/birds/bluebird:1` and you want to add the tags `latest` and `peck`, you must run the following commands:

```sh
ibmcloud cr image-tag us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

```sh
ibmcloud cr image-tag us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:peck
```
{: pre}

After you run these commands, the image has three tags `1`, `latest`, and `peck`.

## What tools can I use to build and push images?
{: #faq_tools}
{: faq}

You can use Docker and non-Docker tools to build and push images to the registry. You can use non-Docker tools that support [OCI container image](#x9860419){: term} format and protocol. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).

## How do I log in to {{site.data.keyword.registryshort}} with Podman?
{: #faq_login_podman}
{: faq}

To log in to {{site.data.keyword.registrylong_notm}} by using Podman, you can use the following command `podman login DOMAIN_NAME -u iamapikey -p PASSWORD`. Replace `DOMAIN_NAME` with your domain name, for example `icr.io`, and replace `PASSWORD` with your IAM API key.

If you prefer not to use an API key, you can use the following command to log in with a user refresh token `ibmcloud cr login --client podman`.

For more information, see [Using Podman to authenticate with the registry](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth_example_other_podman), [Using Podman to authenticate with the registry by using trusted profiles](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_apikey_auth_podman), and [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login).

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

You can run either of the following commands to get the long form of the image digest:

- Run the [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) command:

    ```sh
    ibmcloud cr image-digests
    ```
    {: pre}

- Run the [`ibmcloud cr image-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) command with the `--no-trunc` option:

    ```sh
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

See [Why can't I push or pull a Docker image when I use {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-push-pull-docker) for assistance.

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

## Can I share a {{site.data.keyword.registryshort}} namespace across {{site.data.keyword.cloud_notm}} accounts?
{: #faq_share_namespace}
{: faq}

You can't share a {{site.data.keyword.registryshort}} (`icr.io`) namespace across {{site.data.keyword.cloud_notm}} accounts. A namespace is owned by a single {{site.data.keyword.cloud_notm}} account and cannot be shared with multiple accounts.

## Can I push images on a different account to the one that is running the build pipeline?
{: #faq_push_image_diff_account}
{: faq}

You can push images to {{site.data.keyword.registrylong_notm}} on a different {{site.data.keyword.cloud_notm}} account than the one that is running the build pipeline by using the following steps.

 1. Create an API key in the target {{site.data.keyword.cloud_notm}} account with the necessary access policies to allow pushing images to the required namespace.
 2. Store the API key and the target namespace in your build pipeline configuration.
 3. Modify your build pipeline script to use the API key and target namespace when you are pushing images to {{site.data.keyword.registryshort}}. This action causes your build pipeline to authenticate and to push images to the specified namespace in the target {{site.data.keyword.cloud_notm}} account.

 For more information, see [Pushing images by using an API key](/docs/Registry?topic=Registry-registry_images_#registry_api_key_push_image) and [Accessing {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_access).

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

## How do I do a dry run to check what untagged images are going to be removed by the `ibmcloud cr image-prune-untagged` command?
{: #faq_untagged_image_prune}
{: faq}

You can't do a dry run of the [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged) command. But you can view your untagged images by running the [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) command. You can then check that you do want to remove these untagged images before you run the `ibmcloud cr image-prune-untagged` command.

## How do I restore an image that I removed by accident?
{: #faq_image_restore}
{: faq}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command and restore a selected image by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command. Images are stored in the trash for 30 days.

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

## How do I change the region or registry?
{: #faq_region_registry}
{: faq}

To change the region and the registry, you must log in to {{site.data.keyword.cloud_notm}} and use the [`ibmcloud cr region-set REGION`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set) command, which sets the `container-registry` CLI plug-in to target the specified regional registry.

For example, to change the registry to `uk.icr.io`, which is in the region `eu-gb`, complete the following steps.

1. Log in to {{site.data.keyword.cloud_notm}} by using the following command.

```sh
ibmcloud login
```
{: pre}

2. Run the `ibmcloud cr region-set` command to set the region and registry by entering `eu-gb` as the region:

```sh
ibmcloud cr region-set eu-gb
```
{: pre}

You can also use the name of the registry (for example, `uk.icr.io`) or the former name of the region (for example, `uk-south` instead of `eu-gb`).
{: tip}

You get the following response:

```txt
The region is set to 'uk-south', the registry is 'uk.icr.io'.
```
{: screen}

To find out more about the regions that are available for {{site.data.keyword.registrylong_notm}}, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## How do I get the `docker pull` command to return the most recent version?
{: #faq_docker_pull}
{: faq}

To find the most recent image, run the `ibmcloud cr image-list` command rather than the `docker pull` command. To make it easier to find the most recent image, define a different sequential tag for your images every time, and do not rely on the `latest` tag.

See [Why can't I pull the newest image by using the `latest` tag in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-docker-latest) for assistance.

## Why do my pods fail with an `ImagePullBackOff` error?
{: #faq_imagepullbackoff}
{: faq}

The error is likely to be caused by one of the following situations:

- Your cluster uses an API key that is stored in an image pull secret to authorize the cluster to pull images from {{site.data.keyword.registrylong_notm}}.
- The image with the specific tag does not exist in the repository.

To fix the error, check for the following potential causes.

- Check that you're using the correct name and tag for the image.
- Check that your pull traffic and storage quotas are large enough.
- Check whether you have an image pull secret in your namespace.

For more information, see [Why do images fail to pull from registry with ImagePullBackOff or authorization errors?](/docs/Registry?topic=Registry-ts-app-image-pull) for assistance.

## Why am I getting an exceeded quota error?
{: #faq_quota_error}
{: faq}

You exceeded the image storage or pull traffic quota for your account for the current month. To resolve this issue, you can either review your quota limits and increase them as necessary, or if you're on the Lite plan, upgrade to the standard plan.

For more information, see [Why am I getting errors about my quota in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-quota) and [Staying within quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup).
