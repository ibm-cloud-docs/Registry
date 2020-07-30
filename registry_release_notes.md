---

copyright:
  years: 2019, 2020
lastupdated: "2020-07-30"

keywords: changelog, release notes, changes, user access, DNS names, regions, releases,

subcollection: Registry

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
{:term: .term}
{:external: target="_blank" .external}

# Release notes
{: #registry_release_notes}

Learn about the latest changes to {{site.data.keyword.registrylong}} and Vulnerability Advisor. The changes are grouped by date.
{:shortdesc}

## 30 July 2020
{: #30jul2020}

### New access roles required for Vulnerability Advisor exemption policies
{: #30jul2020exemption}

If you want to manage your Vulnerability Advisor exemption policies for security issues, you might have to update your access role depending on the task that you want to complete.

For more information, see [Access roles for configuring IBM Cloud Container Registry](/docs/Registry?topic=Registry-iam#access_roles_configure).

## 29 July 2020
{: 29jul2020}

### You can set permissions so that access to resources within a namespace can be configured at the resource group level
{: #29jul2020_resource_group}

Namespaces are created in resource groups so that access to resources within a namespace can be configured at the resource group level. If a namespace isn't already in a resource group, you can assign the namespace to a resource group.
{: shortdesc}

- Namespaces created in version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the GUI on or after 29 July 2020, are created in a resource group that you specify so that, if you want to, you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. However, you can still set permissions for the namespace at the account level or in the namespace itself. For more information, see [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add) and [`ibmcloud cr namespace-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add).

- Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the GUI before 29 July 2020 aren't assigned to resource groups. If you want to assign an existing namespace to a resource group so that access to resources within a namespace can be configured at the resource group level, see [Assigning existing namespaces to resource groups](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_assign) and [`ibmcloud cr namespace-assign`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_namespace_assign).

- You can find out which namespaces are assigned to resource groups and which are unassigned by running the [`ibmcloud cr namespace-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list) command with the `-v` flag.

## 13 July 2020
{: #13jul2020}

### To work with namespaces, you must have the Manager role at the account level
{: #13jul2020_manager}

If you want to add or remove namespaces, you must have the Manager role, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## 24 June 2020
{: #24jun2020}

### Restoring all tags for a digest in a repository is now an option
{: #24jun2020_tags}

When you want to restore an image, you have the option to restore either by tag or by digest. Restoring by digest restores the digest and all of its tags in the repository that aren't already in the live repository. You can restore an image by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command.

For more information, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

## 18 May 2020
{: #18may2020}

### Retaining untagged images is now an option when you clean up your namespaces
{: #18may2020_untagged}

Retention policies now include untagged images by default when calculating what to retain. A new `retain-untagged` option for the [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) and [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) commands allows you to keep all untagged images and delete only tagged images. You can view the value of `retain-untagged` for each retention policy by running the [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list) command.

For more information, see [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).

## 30 April 2020
{: #30apr2020}

### `ibmcloud cr image-prune-untagged` command is available
{: #30apr2020_prune}

The `ibmcloud cr image-prune-untagged` command deletes all [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images in your {{site.data.keyword.registrylong_notm}} account.

For more information, see [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged) and [Clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged).

## 16 April 2020
{: #16apr2020}

### You can use private network connections to securely route your data in {{site.data.keyword.registrylong_notm}}
{: #16apr2020_private_network}

If you use cloud-based services for production workloads, you can use a secure private connection so that you ensure that you adhere to any compliance regulations. You can use {{site.data.keyword.cloud_notm}} service endpoints to connect to {{site.data.keyword.cloud_notm}} services over the {{site.data.keyword.cloud_notm}} private network.

For more information, see [Securing your connection to {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_private) and [{{site.data.keyword.registrylong_notm}} architecture and workload](/docs/Registry?topic=Registry-registry_architecture).

### `ibmcloud cr private-only` command is available
{: #16apr2020_private}

The `ibmcloud cr private-only` command enables you to prevent image pulls or pushes over public network connections for your account.

For more information, see [`ibmcloud cr private-only`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only).

## 3 February 2020
{: #3feb2020}

### Using {{site.data.keyword.registrylong_notm}} tokens is deprecated
{: #3feb2020_tokens}

From 12 August 2020, UAA and registry tokens will no longer be accepted for authentication.

For more information, see [Announcing End of IBM Cloud Container Registry Support for Registry and UAA Tokens](https://www.ibm.com/cloud/blog/announcements/announcing-end-of-ibm-cloud-container-registry-support-for-registry-and-uaa-tokens){: external)}.

## 31 January 2020
{: #31jan2020}

### `ibmcloud cr image-digests` command is available
{: #31jan2020_digests}

The `ibmcloud cr image-digests` command displays all images in your account, including untagged images.

For more information, see [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests).

## 4 December 2019
{: #4dec2019}

### Support for {{site.data.keyword.openshiftlong_notm}} signatures is available
{: #4dec2019_signatures}

{{site.data.keyword.registrylong_notm}} now supports {{site.data.keyword.openshiftlong}} signatures.

For more information, see [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig).

## 25 October 2019
{: #25oct2019}

### {{site.data.keyword.la_full_notm}} platform services logs are available
{: #25oct2019_logs}

{{site.data.keyword.registrylong_notm}} generates platform services logs that are displayed in your LogDNA instances.

For more information, see [{{site.data.keyword.la_full_notm}} platform services logs](/docs/Registry?topic=Registry-registry_logs).

## 14 October 2019
{: #14oct2019}

### `ibmcloud cr manifest-inspect` command is available
{: #14oct2019_manifest}

The `ibmcloud cr manifest-inspect` command displays the contents of the manifest for an image.

For more information, see [`ibmcloud cr manifest-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect).

## 23 September 2019
{: #23sep2019}

### You can create retention policies for your images
{: #23sep2019_retention_policy}

Image retention policies retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.

The following commands are available for you to use to create retention policies so that you can manage your images:

- The [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) command sets up a policy for retaining images for each repository within a namespace.
- The [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list) command lists the image retention policies for your account.
  
For more information, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

### You can restore deleted images from the trash.
{: #23sep2019_restore_trash}

All deleted images are stored in the trash for 30 days.

The following commands are available for you to use to restore images:

- The [`ibmcloud cr trash-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list) command displays all images in the trash in your {{site.data.keyword.cloud_notm}} account. Images remain in the trash for 30 days after they've been deleted.
- The [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command restores a deleted image from the trash.

For more information, see [Listing images in the trash](/docs/Registry?topic=Registry-registry_images_#registry_images_list_trash) and [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

## 1 August 2019
{: #01aug2019}

### `ibmcloud cr retention-run` command is available
{: #01aug2019_retention}

The `ibmcloud cr retention-run` command cleans up your namespaces by retaining images for each repository within a namespace in {{site.data.keyword.registrylong_notm}} by applying specified criteria. All other images in the namespace are deleted.

For more information, see [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) and [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## 25 July 2019
{: #25jul2019}

### {{site.data.keyword.at_full_notm}} available for {{site.data.keyword.registrylong_notm}}
{: #25jul2019_at}

Use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud_notm}}.

For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

## 1 July 2019
{: #1jul2019}

### `ibmcloud cr token-add` command is no longer available
{: #1jul2019_token_add}

The `ibmcloud cr token-add` command is discontinued. You can't add registry tokens in either the CLI or the API anymore.

## 27 June 2019
{: #27jun2019}

### Container Scanner is no longer available
{: #27jun2019_cs}

The Container Scanner is discontinued. Vulnerability Advisor still scans images that are pushed to {{site.data.keyword.registrylong_notm}}.

## 13 June 2019
{: #13jun2019}

### Remove tags from images
{: #13jun2019_tags}

Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}. To remove a specific tag from an image and leave the underlying image and any other tags in place, use the [`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) command. If you want to delete the underlying image, and all of its tags, use the [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command instead.

For more information, see [Removing tags from images in your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_untag).

## 13 May 2019
{: #13may2019}

### End of support for Container Scanner
{: #13may2019_cs}

Container Scanner is now deprecated and is no longer usable.

## 2 April 2019
{: #2apr2019}

### General Availability of Container Image Security Enforcement
{: #2apr2019_cise}

Use Container Image Security Enforcement to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/Registry?topic=Registry-registry_trustedcontent) is properly applied to the image.

For more information, see [Enforcing container image security](/docs/Registry?topic=Registry-security_enforce#security_enforce).

## 14 March 2019
{: #14mar2019}

### {{site.data.keyword.cloudaccesstrailfull_notm}} available for {{site.data.keyword.registrylong_notm}}
{: #14mar2019_at}

Use the {{site.data.keyword.cloudaccesstraillong_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud_notm}}.

For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

## 25 February 2019
{: #25feb2019}

### New domain names
{: #25feb2019_dns}

{{site.data.keyword.registrylong_notm}} is adopting new domain names. The new domain names are available in the console and the CLI. You can use the new `icr.io` domain names now. The existing `registry.bluemix.net` domain names are deprecated, but you can continue to use them until the end of support date. An end of support date is not available yet.

For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions) and [Introducing New IBM Cloud Container Registry Domain Names](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names){: external}.

Signatures apply to the whole image name, which includes the domain name. If you are using content trust, you must add new signatures so that you can consume content trust under the new domain name.

For more information about signing images, see [Signing images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent).

### IAM API key pull secrets for {{site.data.keyword.containerlong_notm}} clusters
{: #25feb2019_secrets}

The new cluster image pull secrets for the `icr.io` domains are authorized by using an {{site.data.keyword.iamlong}} (IAM) API key. Therefore, if you want more control over access to your {{site.data.keyword.registrylong_notm}} resources, you can add IAM policies. For example, you can change the API key policies in the cluster's pull secret so that images are pulled from a certain registry region or namespace only.

For more information, see [Understanding how to authorize your cluster to pull images from a registry](/docs/containers?topic=containers-registry#cluster_registry_auth).

### New region in ap-north
{: #25feb2019_ap-north}

A new region is available in `ap-north`. You can use the new region by using the domain name `jp.icr.io`.

For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## 21 February 2019
{: #21feb2019}

### Automating access to your namespaces
{: #21feb2019_access}

Using tokens to automate pushing and pulling Docker images to and from your namespaces is deprecated. You must now use API keys to automate access to your {{site.data.keyword.registrylong_notm}} namespaces so that you can push and pull images.

For more information, see [Automating access to your namespaces by using API keys](/docs/Registry?topic=Registry-registry_access#registry_access_user_apikey).

## 8 January 2019
{: #8jan2019}

### End of support for Vulnerability Advisor API version 2
{: #8jan2019_va2}

Vulnerability Advisor’s API version 2 is deprecated and is no longer usable. Use version 3 of the API, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}}](https://cloud.ibm.com/apidocs/container-registry/va){: external}.

For more information, see [Vulnerability Advisor v2 API Deprecation](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/){: external}.

## 4 October 2018
{: #4oct2018}

### Managing user access
{: #4oct2018_access}

Use {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) to control access by users in your account to {{site.data.keyword.registrylong_notm}}. When IAM policies are enabled for your account in {{site.data.keyword.registrylong_notm}}, every user that accesses the service in your account must be assigned an access policy with an IAM user role defined. That policy determines what role the user has within the context of the service, and what actions the user can perform.

For more information, see [Managing user access with {{site.data.keyword.iamshort}}](/docs/Registry?topic=Registry-iam#iam), [Defining user access role policies](/docs/Registry?topic=Registry-user#user), and [Tutorial: Granting access to IBM Cloud Container Registry resources](/docs/Registry?topic=Registry-iam_access#iam_access).

## 7 August 2018
{: #7aug2018}

### Exemption policies available in Vulnerability Advisor
{: #7aug2018_exemption}

If you want to manage the security of an {{site.data.keyword.cloud_notm}} organization, you can use your policy setting to determine whether an issue is exempt or not. You can use Container Image Security Enforcement to ensure that deployment is allowed only from images that contain no security issues after accounting for any issues that are exempted by your policy.

For more information, see [Setting organizational exemption policies](/docs/Registry?topic=va-va_index#va_managing_policy).

## 25 July 2018
{: #25jul2018}

### {{site.data.keyword.cloudaccesstrailfull_notm}} available for Vulnerability Advisor
{: #25jul2018_at}

Use the {{site.data.keyword.cloudaccesstrailfull_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud_notm}}.

For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

## 12 July 2018
{: #12jul2018}

### Vulnerability Advisor API version 3
{: #12jul2018_va3}

Version 3 of the API changes the behavior of the API endpoints that are used to list exemptions. You must check that your use of the API does not rely on the behavior of version 2.

For more information, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}}](https://cloud.ibm.com/apidocs/container-registry/va){: external}.

## 31 May 2018
{: #31may2018}

### Use Helm for Passport Advantage images
{: #31may2018_helm}

Import {{site.data.keyword.IBM_notm}} software that is downloaded from [IBM Passport Advantage Online for customers](https://www.ibm.com/software/passportadvantage/pao_customer.html){: external} and packaged for use with Helm into your {{site.data.keyword.registrylong_notm}} namespace.

For more information, see [`ibmcloud cr ppa-archive-load`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).

## 21 March 2018
{: #21mar2018}

### Container Scanner
{: #21mar2018_cs}

Container Scanner enables Vulnerability Advisor to report any problems that are found in running containers that are not present in the container's base image.

## 16 March 2018
{: #16mar2018}

### Container Image Security Enforcement beta
{: #16mar2018_cise}

Use Container Image Security Enforcement beta to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/Registry?topic=Registry-registry_trustedcontent) is properly applied to the image.

For more information, see [Enforcing container image security](/docs/Registry?topic=Registry-security_enforce#security_enforce).

## 20 February 2018
{: #20feb2018}

### Trusted content
{: #20feb2018_tc}

{{site.data.keyword.registrylong_notm}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools.

For more information, see [Signing images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent).

## 6 November 2017
{: #6nov2017}

### Global registry
{: #6nov2017_global}

A global registry is available. It has no region included in its domain name (`icr.io`). Only public images that are provided by {{site.data.keyword.IBM_notm}} are hosted in this registry.

For more information, see [Global registry](/docs/Registry?topic=Registry-registry_overview#registry_regions_global).

## 29 September 2017
{: #29sep2017}

### Build Docker images
{: #29sep2017_docker}

The `ibmcloud cr build` command is now available for running container builds. You can build a Docker image directly in {{site.data.keyword.cloud_notm}} or create your own Docker image on your local computer and upload (push) it to your namespace in {{site.data.keyword.registrylong_notm}}.

For more information, see [Building Docker images to use them with your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_creating) and [`ibmcloud cr build`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).

## 24 August 2017
{: #24aug2017}

### Graphical user interface released
{: #24aug2017_gui}

The {{site.data.keyword.registrylong_notm}} graphical user interface is available in the catalog, see [Container Registry](https://cloud.ibm.com/kubernetes/catalog/registry){: external}.

## 27 June 2017
{: #27jun2017}

### General availability of {{site.data.keyword.registrylong_notm}}
{: #27jun2017_ga}

{{site.data.keyword.registrylong_notm}} is generally available as a service in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.registrylong_notm}} supports {{site.data.keyword.containerlong_notm}}.

For more information about {{site.data.keyword.containerlong_notm}}, see [Getting started with {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-getting-started).
