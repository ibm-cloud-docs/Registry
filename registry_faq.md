---

copyright:
  years: 2018, 2019
lastupdated: "2019-12-10"

keywords: public images, commands, questions, registry, FAQ, Vulnerability Advisor, frequently asked questions, FAQs,

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
{:term: .term}

# Frequently asked questions (FAQs)
{: #registry_faq}

Frequently asked questions about {{site.data.keyword.registrylong}}.
{: shortdesc}

## How do you list public images?
{: #faq_list_public_images}
{: faq}

To list public images, run the following `ibmcloud` commands to target the global registry and list the public images that are provided by {{site.data.keyword.IBM}}:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Can you use non-docker tools to build my images and push them to the registry?
{: #faq_tools}
{: faq}

Yes, if the tool supports OCI image format and protocol.

## How do you use access control with {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}?
{: #faq_access_control}
{: faq}

You can create {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) policies to control access to your namespaces in {{site.data.keyword.registrylong_notm}}. For more information, see [Tutorial: Granting access to {{site.data.keyword.registrylong_notm}} resources](/docs/services/Registry?topic=registry-iam_access) and [Managing user access with Identity and Access Management](/docs/services/Registry?topic=registry-iam).

## What regions are available for {{site.data.keyword.registrylong_notm}}?
{: #faq_regions}
{: faq}

You can host images in [local regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local). IBM hosted public images are available in the [Global registry](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## Why have I received a scan not found error message for a newly added image?
{: #faq_va_new_scan_error}
{: faq}

If you get the vulnerability report immediately after you add the image to the registry, you might receive the following error:

```
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://cloud.ibm.com/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support
```
{: screen}

You receive this message because the images are scanned asynchronously to the requests for results, and the scanning process takes a while to complete. During normal operation, the scan completes within the first few minutes after you add the image to the registry. The time that it takes to complete depends on variables like the image size and the amount of traffic that the registry is receiving.

If you get this message as part of a build pipeline and you see this error regularly, try adding some retry logic that contains a short pause.

If you still see unacceptable performance, contact support, see [Getting help and support for {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-ts_index#gettinghelp).

## How is a Vulnerability Advisor scan triggered?
{: #faq_va_trigger_scan}
{: faq}

The scanning of an image is triggered in one of the following ways:

- If a new image is pushed to the registry.
- If the last scan is more than 7 days ago, the image is queued for rescanning, which might take some time to complete.
- If a new security notice is released for a package that is installed in the image, the image is queued for rescanning, which might take some time to complete. Rescans that are triggered by the release of new security notices are available for Ubuntu and Debian images only.

## How often are the security notices updated?
{: #faq_va_update_security_notice}
{: faq}

Security notices for Vulnerability Advisor are loaded from the vendors' operating system sites approximately every 12 hours.
