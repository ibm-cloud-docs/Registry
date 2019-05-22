---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-22"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, 

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
{:faq: data-hd-content-type='faq'}

# Frequently asked questions (FAQs)
{: #registry_faq}

Frequently asked questions about {{site.data.keyword.registrylong}}.
{: shortdesc}

## How do I list public images?
{: #faq_list_public_images}
{: faq}

To list public images, run the following `ibmcloud` commands to target the global registry and list the IBM-provided public images:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Can I use non-docker tools to build my images and push them to the registry?
{: #faq_tools}
{: faq}

No, only tools that build Docker v2 image formats are supported. For more information, see [Docker: Image Manifest V 2, Schema 2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.docker.com/registry/spec/manifest-v2-2/).

The FAQs below are in staging only at the moment.
{: tip}

## How do I use access control with IAM?
{: #faq_access_control}
{: faq}

You can create {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) policies to control access to your namespaces in {{site.data.keyword.registrylong_notm}}. For more information, see [Tutorial: Granting access to {{site.data.keyword.registrylong_notm}} resources](/docs/services/Registry?topic=registry-iam_access) and [Managing user access with Identity and Access Management](/docs/services/Registry?topic=registry-iam).

## What regions are available for {{site.data.keyword.registrylong_notm}}?
{: #faq_regions}
{: faq}

You can host images in [local regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local). IBM hosted public images are available in the [Global registry](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## How do I update the Container Scanner when it is flagged with vulnerabilities?
{: #faq_va_update_scan_flag}
{: faq}

To update the version of the Container Scanner that is running in a cluster, use Helm in the same way as for the installation, but with the `–upgrade` flag. For more information, see [Configure the Helm Chart](/docs/services/Registry?topic=va-va_index#va_install_container_scanner_helm).

For example:

```
helm install -f config.yaml --name=<myscanner> ibm/ibmcloud-container-scanner -upgrade
```
{: pre}

## Why have I received a scan not found error message for a newly added image?
{: #faq_va_new_scan_error}
{: faq}

If you get the vulnerability report immediately after adding the image to the registry, you might receive the following error:

```
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

You receive this message because the images are scanned asynchronously to the requests for results, and the scanning process takes a while to complete. During normal operation, the scan completes between 30 seconds and 5 minutes after you've added the image to the registry, depending on variables like the image size and the amount of traffic that the registry is receiving.

If you get this message as part of a build pipeline and you see this error regularly, try adding some retry logic that contains a short pause.

If you still see unacceptable performance, contact support, see [Getting help and support for {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-ts_index#gettinghelp).

## How is a Vulnerability Advisor scan triggered?
{: #faq_va_trigger_scan}
{: faq}

The scanning of an image is triggered in one of the following ways:

- If a new image is pushed to the registry, a priority request is issued to rescan the image.
- If the image has not been scanned for 7 days, a background request is issued to rescan the image, which might take some time to complete.
- If a new security notice is released for a package installed in the image, a background request is issued to rescan the image, which might take some time to complete.
  Rescans that are triggered by the release of new security notices are available for Ubuntu and Debian images only.
  {:tip}

## How often are the security notices updated?
{: #faq_va_update_security_notice}
{: faq}

Security notices for Vulnerbaility Advisor are loaded from the vendors' operating system sites approximately every 12 hours.

## Does Vulnerability Advisor have versions?
{: #faq_va_versions}
{: faq}

No. However, a version number is baked into the API, but this version is the version of the JSON that is returned.

The different components (for example, the API, scanning tools, and database) are all updated independently. Given that the scans happen asynchronously to the requests for results, the set of components that give a result is variable. However, each scan does contain a timestamp that can be used to work out the components used for the scan.</staging>
