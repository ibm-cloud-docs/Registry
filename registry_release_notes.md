---

copyright:
  years: 2019
lastupdated: "2019-10-18"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

subcollection: registry

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

# Release notes
{: #registry_release_notes}

Learn about the latest changes to {{site.data.keyword.registrylong}} and Vulnerability Advisor. The changes are grouped by date.
{:shortdesc}

## 14 October 2019
{: #14oct2019}

<dl>
  <dt>`ibmcloud cr manifest-inspect` command is available</dt>
  <dd>The `ibmcloud cr manifest-inspect` command displays the contents of the manifest for an image.

  For more information, see [`ibmcloud cr manifest-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect).</dd>
</dl>

## 23 September 2019
{: #23sep2019}

<dl>
  <dt>You can create retention policies for your images. Image retention policies retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.</dt>
  <dd>The following commands are available for you to use to create retention policies so that you can manage your images:
  
  <ul>
    <li>The [`ibmcloud cr retention-policy-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set) command sets up a policy for retaining images for each repository within a namespace.</li>
    <li>The [`ibmcloud cr retention-policy-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list) command lists the image retention policies for your account. </li>
  </ul>
  
  For more information, see [Retaining images](/docs/services/Registry?topic=registry-registry_retention).</dd>
</dl>

<dl>
  <dt>You can restore deleted images from the trash. All deleted images are stored in the trash for 30 days.</dt>
  <dd>The following commands are available for you to use to restore images:
  
  <ul>
    <li>The [`ibmcloud cr trash-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list) command displays all images in the trash in your {{site.data.keyword.cloud_notm}} account. Images remain in the trash for 30 days after they've been deleted.</li>
    <li>The [`ibmcloud cr image-restore`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command restores a deleted image from the trash.</li>
  </ul>
  
  For more information, see [Listing images in the trash](/docs/services/Registry?topic=registry-registry_images_#registry_images_list_trash) and [Restoring images](/docs/services/Registry?topic=registry-registry_images_#registry_images_restore).</dd>
</dl>

## 1 August 2019
{: #01aug2019}

<dl>
  <dt>`ibmcloud cr retention-run` command is available</dt>
  <dd>The `ibmcloud cr retention-run` command cleans up your namespaces by retaining images for each repository within a namespace in {{site.data.keyword.registrylong_notm}} by applying specified criteria. All other images in the namespace are deleted.
  
  For more information, see [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) and [Retaining images](/docs/services/Registry?topic=registry-registry_retention).</dd>
</dl>

## 25 July 2019
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.at_full_notm}} available for {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud_notm}}.

  For more information, see [Activity Tracker events](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>

## 1 July 2019
{: #1jul2019}

<dl>
  <dt>`ibmcloud cr token-add` command is no longer available</dt>
  <dd>The `ibmcloud cr token-add` command is discontinued. You can't add registry tokens in either the CLI or the API anymore.</dd>
</dl>

## 27 June 2019
{: #27jun2019}

<dl>
  <dt>Container Scanner is no longer available</dt>
  <dd>The Container Scanner is discontinued. Vulnerability Advisor still scans images that are pushed to {{site.data.keyword.registrylong_notm}}.</dd>
</dl>

## 13 June 2019
{: #13jun2019}

<dl>
  <dt>Remove tags from images</dt>
  <dd>Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}.

  To remove a specific tag from an image and leave the underlying image and any other tags in place, use the [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) command. If you want to delete the underlying image, and all of its tags, use the [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command instead.

  For more information, see [Removing tags from images in your private {{site.data.keyword.cloud_notm}} repository](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag).</dd>
</dl>

## 13 May 2019
{: #13may2019}

<dl>
  <dt>End of support for Container Scanner</dt>
  <dd>Container Scanner is now deprecated and is no longer usable.

  For more information, see [Installing the Container Scanner (deprecated)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 2 April 2019
{: #2apr2019}

<dl>
  <dt>General Availability of Container Image Security Enforcement</dt>
  <dd>Use Container Image Security Enforcement to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) is properly applied to the image.

  For more information, see [Enforcing container image security](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 14 March 2019
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} available for {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Use the {{site.data.keyword.cloudaccesstraillong_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud_notm}}.

  For more information, see [Activity Tracker events](/docs/services/Registry?topic=registry-at_events#at_events).
</dd>
</dl>

## 25 February 2019
{: #25feb2019}

<dl>
  <dt>New domain names</dt>
  <dd>{{site.data.keyword.registrylong_notm}} is adopting new domain names. The new domain names are available in the console and the CLI. You can use the new `icr.io` domain names now. The existing `registry.bluemix.net` domain names are deprecated, but you can continue to use them until the end of support date. An end of support date is not available yet. For more information, see [Regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions) and [Introducing New IBM Cloud Container Registry Domain Names ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  Signatures apply to the whole image name, which includes the domain name. If you are using content trust, you must add new signatures so that you can consume content trust under the new domain name. For more information about signing images, see [Signing images for trusted content](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

<dl>
  <dt>IAM API key pull secrets for {{site.data.keyword.containerlong_notm}} clusters</dt>
  <dd>The new cluster image pull secrets for the `icr.io` domains are authorized by using an {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) API key. Therefore, if you want more control over access to your {{site.data.keyword.registrylong_notm}} resources, you can add IAM policies. For example, you can change the API key policies in the cluster's pull secret so that images are pulled from a certain registry region or namespace only.
  
  For more information, see [Understanding how your cluster is authorized to pull images from {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).</dd>
</dl>

<dl>
  <dt>New region in ap-north</dt>
  <dd>A new region is available in `ap-north`. You can use the new region by using the domain name `jp.icr.io`.
  
  For more information, see [Regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions).</dd>
</dl>

## 21 February 2019
{: #21feb2019}

<dl>
  <dt>Automating access to your namespaces</dt>
  <dd>Using tokens to automate pushing and pulling Docker images to and from your namespaces is deprecated. You must now use API keys to automate access to your {{site.data.keyword.registrylong_notm}} namespaces so that you can push and pull images.

  For more information, see [Automating access to your namespaces by using API keys](/docs/services/Registry?topic=registry-registry_access#registry_api_key).</dd>
</dl>

## 8 January 2019
{: #8jan2019}

 <dl>
  <dt>End of support for Vulnerability Advisor API version 2</dt>
  <dd>Vulnerability Advisor’s API version 2 is deprecated and is no longer usable. Use version 3 of the API, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/container-registry/va).

  For more information, see [Vulnerability Advisor v2 API Deprecation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/).</dd>
</dl>

## 4 October 2018
{: #4oct2018}

<dl>
  <dt>Managing user access</dt>
  <dd>Use {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) to control access by users in your account to {{site.data.keyword.registrylong_notm}}. When IAM policies are enabled for your account in {{site.data.keyword.registrylong_notm}}, every user that accesses the service in your account must be assigned an access policy with an IAM user role defined. That policy determines what role the user has within the context of the service, and what actions the user can perform.

  For more information, see [Managing user access with {{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam), [Defining user access role policies](/docs/services/Registry?topic=registry-user#user), and [Tutorial: Granting access to IBM Cloud Container Registry resources](/docs/services/Registry?topic=registry-iam_access#iam_access).</dd>
</dl>

## 7 August 2018
{: #7aug2018}

<dl>
  <dt>Exemption policies available in Vulnerability Advisor</dt>
  <dd>If you want to manage the security of an {{site.data.keyword.cloud_notm}} organization, you can use your policy setting to determine whether an issue is exempt or not. You can use Container Image Security Enforcement to ensure that deployment is allowed only from images that contain no security issues after accounting for any issues that are exempted by your policy.

  For more information, see [Setting organizational exemption policies](/docs/services/Registry?topic=va-va_index#va_managing_policy).</dd>
</dl>

## 25 July 2018
{: #25jul2018}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} available for Vulnerability Advisor</dt>
  <dd>Use the {{site.data.keyword.cloudaccesstrailfull_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud_notm}}.

  For more information, see [Activity Tracker events](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>
  
## 12 July 2018
{: #12jul2018}

<dl>
  <dt>Vulnerability Advisor API version 3</dt>
  <dd>Version 3 of the API changes the behavior of the API endpoints that are used to list exemptions. You must check that your use of the API does not rely on the behavior of version 2.

  For more information, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/container-registry/va).</dd>
</dl>

## 31 May 2018
{: #31may2018}

<dl>
  <dt>Use Helm for Passport Advantage images</dt>
  <dd>Import {{site.data.keyword.IBM_notm}} software that is downloaded from [IBM Passport Advantage Online for customers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/passportadvantage/pao_customer.html) and packaged for use with Helm into your {{site.data.keyword.registrylong_notm}} namespace.

  For more information, see [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).</dd>
</dl>

## 21 March 2018
{: #21mar2018}

<dl>
  <dt>Container Scanner</dt>
  <dd>Container Scanner enables Vulnerability Advisor to report any problems that are found in running containers that are not present in the container's base image.

  For more information, see [Installing the Container Scanner](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 16 March 2018
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement beta</dt>
  <dd>Use Container Image Security Enforcement beta to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) is properly applied to the image.

  For more information, see [Enforcing container image security](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 20 February 2018
{: #20feb2018}

<dl>
  <dt>Trusted content</dt>
  <dd>{{site.data.keyword.registrylong_notm}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools.

  For more information, see [Signing images for trusted content](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

## 6 November 2017
{: #6nov2017}

<dl>
  <dt>Global registry</dt>
  <dd>A global registry is available. It has no region included in its domain name (`icr.io`). Only public images that are provided by {{site.data.keyword.IBM_notm}} are hosted in this registry.

  For more information, see [Global registry](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).</dd>
</dl>

## 29 September 2017
{: #29sep2017}

<dl>
  <dt>Build Docker images</dt>
  <dd>The `ibmcloud cr build` command is now available for running container builds. You can build a Docker image directly in {{site.data.keyword.cloud_notm}} or create your own Docker image on your local computer and upload (push) it to your namespace in {{site.data.keyword.registrylong_notm}}.

  For more information, see [Building Docker images to use them with your namespace](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) and [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).</dd>
</dl>

## 24 August 2017
{: #24aug2017}

<dl>
  <dt>Graphical user interface released</dt>
  <dd>The {{site.data.keyword.registrylong_notm}} graphical user interface is available in the catalog, see [Container Registry ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/catalog/registry).</dd>
</dl>

## 27 June 2017
{: #27jun2017}

<dl>
  <dt>General availability of {{site.data.keyword.registrylong_notm}}</dt>
  <dd>{{site.data.keyword.registrylong_notm}} is generally available as a service in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.registrylong_notm}} supports {{site.data.keyword.containerlong_notm}}.

  For more information about {{site.data.keyword.containerlong_notm}}, see [Getting started with {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-getting-started).</dd>
</dl>
