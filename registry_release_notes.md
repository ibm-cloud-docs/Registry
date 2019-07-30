---

copyright:
  years: 2019
lastupdated: "2019-07-25"

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

Use these release notes to learn about the latest changes to {{site.data.keyword.registrylong}} and Vulnerability Advisor. The changes are grouped by date.
{:shortdesc}

## 25 July 2019
{: #25jul2019}

- **{{site.data.keyword.at_full_notm}} available for {{site.data.keyword.registrylong_notm}}**

  Use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud}}.

  For more information, see [Activity Tracker events](/docs/services/Registry?topic=registry-at_events#at_events).

## 01 July 2019
{: #01jul2019}

- **`ibmcloud cr token-add` command is no longer available**

  The `ibmcloud cr token-add` command is discontinued. You can't add registry tokens in either the CLI or the API anymore.

## 27 June 2019
{: #27jun2019}

- **Container Scanner is no longer available**

  The Container Scanner is discontinued. Vulnerability Advisor will continue to scan images that are pushed to {{site.data.keyword.registrylong_notm}}.

## 13 June 2019
{: #13jun2019}

- **Remove tags from images**

  Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}.

  To remove a specific tag from an image and leave the underlying image and any other tags in place, use the [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) command. If you want to delete the underlying image, and all of its tags, use the [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command instead.

  For more information, see [Removing tags from images in your private {{site.data.keyword.cloud_notm}} repository](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag).

## 13 May 2019
{: #13may2019}

- **End of support for Container Scanner**

  Container Scanner is now deprecated and is no longer usable.

  For more information, see [Installing the Container Scanner (deprecated)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).

## 2 April 2019
{: #2apr2019}

- **General Availability of Container Image Security Enforcement**

  Use Container Image Security Enforcement to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) is properly applied to the image.

  For more information, see [Enforcing container image security](/docs/services/Registry?topic=registry-security_enforce#security_enforce).

## 14 March 2019
{: #14mar2019}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} available for {{site.data.keyword.registrylong_notm}}**

  Use the {{site.data.keyword.cloudaccesstraillong_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud}}.

  For more information, see [Activity Tracker events](/docs/services/Registry?topic=registry-at_events#at_events).

## 25 February 2019
{: #25feb2019}

- **New DNS names**

  {{site.data.keyword.registrylong_notm}} is adopting new domain names. The new domain names are available in the console and the CLI. You can use the new `icr.io` domain names now. The existing `registry.bluemix.net` domain names are deprecated, but you can continue to use them for the time being, an end of support date will be announced later. For more information, see [Regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions) and [Introducing New IBM Cloud Container Registry Domain Names ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  If you are using content trust then, because signatures apply to the whole image name including the domain name, you must add new signatures so that you can consume content trust under the new domain name. For more information about signing images, see [Signing images for trusted content](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).

- **IAM API key pull secrets for {{site.data.keyword.containerlong_notm}} clusters**

  The new cluster image pull secrets for the `icr.io` domains are authorized by using an IAM API key, therefore, if you want more control over access to your {{site.data.keyword.registrylong_notm}} resources, you can add IAM policies. For example, you can change the API key policies in the cluster's pull secret so that images are pulled from a certain registry region or namespace only.
  
  For more information, see [Understanding how your cluster is authorized to pull images from {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).

- **New region in ap-north**

  A new region is available in `ap-north`. You can use the new region by using the domain name `jp.icr.io`.
  
  For more information, see [Regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## 21 Feb 2019
{: #21feb2019}

- **Automating access to your namespaces**

  Using tokens to automate pushing and pulling Docker images to and from your namespaces is deprecated. You must now use API keys to automate access to your {{site.data.keyword.registrylong_notm}} namespaces so that you can push and pull images.

  For more information, see [Automating access to your namespaces by using API keys](/docs/services/Registry?topic=registry-registry_access#registry_api_key).

## 8 January 2019
{: #8jan2019}

- **End of support for Vulnerability Advisor API version 2**

  Vulnerability Advisor’s API version 2 is deprecated and is no longer usable. Use version 3 of the API, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/container-registry/va).

  For more information, see [Vulnerability Advisor v2 API Deprecation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/).

## 4 October 2018
{: #4oct2018}

- **Managing user access**

  Use {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) to control access by users in your account to {{site.data.keyword.registrylong_notm}}. When IAM policies are enabled for your account in {{site.data.keyword.registrylong_notm}}, every user that accesses the {{site.data.keyword.registrylong_notm}} service in your account must be assigned an access policy with an IAM user role defined. That policy determines what role the user has within the context of the service, and what actions the user can perform.

  For more information, see [Managing user access with {{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam), [Defining user access role policies](/docs/services/Registry?topic=registry-user#user), and [Tutorial: Granting access to IBM Cloud Container Registry resources](/docs/services/Registry?topic=registry-iam_access#iam_access).

## 7 August 2018
{: #7aug2018}

- **Exemption policies available in Vulnerability Advisor**

  If you want to manage the security of an {{site.data.keyword.cloud_notm}} organization, you can use your policy setting to determine whether an issue is exempt or not. You can choose to use Container Image Security Enforcement to ensure that deployment is allowed only from images that contain no security issues after accounting for any issues that are exempted by your policy.

  For more information, see [Setting organizational exemption policies](/docs/services/Registry?topic=va-va_index#va_managing_policy).

## 25 July 2018
{: #25jul2018}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} available for Vulnerability Advisor**

  Use the {{site.data.keyword.cloudaccesstrailfull_notm}} service to track how users and applications interact with the {{site.data.keyword.registrylong_notm}} service in {{site.data.keyword.cloud}}.

  For more information, see [Activity Tracker events](/docs/services/Registry?topic=registry-at_events#at_events).
  
## 12 July 2018
{: #12jul2018}

- **Vulnerability Advisor API version 3**

  Version 3 of the API changes the behavior of the API endpoints that are used to list exemptions. You should check that your use of the API does not rely on the behavior of version 2.

  For more information, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/container-registry/va).

## 31 May 2018
{: #31may2018}

- **Use Helm for Passport Advantage images**

  Import {{site.data.keyword.IBM_notm}} software that is downloaded from [IBM Passport Advantage Online for customers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/passportadvantage/pao_customer.html) and packaged for use with Helm into your {{site.data.keyword.registrylong_notm}} namespace.

  For more information, see [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).

## 21 March 2018
{: #21mar2018}

- **Container Scanner**

  Container Scanner enables Vulnerability Advisor to report any problems found in running containers that are not present in the container's base image.

  For more information, see [Installing the Container Scanner](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).

## 16 March 2018
{: #16mar2018}

- **Container Image Security Enforcement beta**

  Use Container Image Security Enforcement beta to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) is properly applied to the image.

  For more information, see [Enforcing container image security](/docs/services/Registry?topic=registry-security_enforce#security_enforce).

## 20 February 2018
{: #20feb2018}

- **Trusted content**

  {{site.data.keyword.registrylong_notm}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools.

  For more information, see [Signing images for trusted content](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).

## 6 November 2017
{: #6nov2017}

- **Global registry**

  A global registry is available, it has no region included in its name (`icr.io`). Only public images that are provided by IBM are hosted in this registry.

  For more information, see [Global registry](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## 29 September 2017
{: #29sep2017}

- **Build Docker images**

  The `ibmcloud cr build` command is now available for running container builds. You can build a Docker image directly in {{site.data.keyword.cloud_notm}} or create your own Docker image on your local computer and upload (push) it to your namespace in {{site.data.keyword.registrylong_notm}}.

  For more information, see [Building Docker images to use them with your namespace](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) and [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).

## 24 August 2017
{: #24aug2017}

- **Graphical User Interface released**

  The {{site.data.keyword.registrylong_notm}} graphical user interface is available in the Catalog, see [Container Registry ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/catalog/registry).

## 27 June 2017
{: #27jun2017}

- **General availability of {{site.data.keyword.registrylong_notm}}**

  {{site.data.keyword.registrylong_notm}} is generally available as a service in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.registrylong_notm}} supports {{site.data.keyword.containerlong_notm}}.

  For more information about {{site.data.keyword.containerlong_notm}}, see [Getting started tutorial](/docs/containers?topic=containers-getting-started).
