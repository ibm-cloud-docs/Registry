---

copyright:
  years: 2018, 2021
lastupdated: "2021-12-17"

keywords: public images, commands, questions, registry, FAQ, Vulnerability Advisor, frequently asked questions, FAQs,

subcollection: Registry

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# Frequently asked questions (FAQs)
{: #registry_faq}

Frequently asked questions about {{site.data.keyword.registrylong}}.
{: shortdesc}

## How do you list public images?
{: #faq_list_public_images}
{: faq}

To list public images, run the following `ibmcloud` commands to target the global registry and list the public images that are provided by {{site.data.keyword.IBM}}:

```sh
ibmcloud cr region-set global
```
{: pre}

```sh
ibmcloud cr images --include-ibm
```
{: pre}

## Can you use non-Docker tools to build my images and push them to the registry?
{: #faq_tools}
{: faq}

Yes, if the tool supports [OCI container image](#x9860419){: term} format and protocol. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).

## Is there a limit to the number of namespaces you can have?
{: #faq_namespace}
{: faq}

You can have 100 registry namespaces in each region.

## Do images in the trash count toward my quota?
{: #faq_trash}
{: faq}

Images that are in the trash don't count toward your quota.

## How do you use access control with {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}?
{: #faq_access_control}
{: faq}

You can create {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) policies to control access to your namespaces in {{site.data.keyword.registrylong_notm}}. For more information, see [Granting access to {{site.data.keyword.registrylong_notm}} resources tutorial](/docs/Registry?topic=Registry-iam_access) and [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).

## What regions are available for {{site.data.keyword.registrylong_notm}}?
{: #faq_regions}
{: faq}

To find out about the regions that are available, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## How much does Vulnerability Advisor cost?
{: #faq_va_cost}
{: faq}

The cost of Vulnerability Advisor is built into the pricing for {{site.data.keyword.registrylong_notm}}. For more information, see [Billing for storage and pull traffic](/docs/Registry?topic=Registry-registry_overview#registry_billing_traffic).

## Does Vulnerability Advisor scan images from other registries?
{: #faq_va_reg}
{: faq}

Vulnerability Advisor scans images from {{site.data.keyword.registrylong_notm}} only.

## How is a Vulnerability Advisor scan triggered?
{: #faq_va_trigger_scan}
{: faq}

For more information about how the scanning of an image is triggered, see [Vulnerable packages](/docs/Registry?topic=va-va_index#packages).

## Why have I received a scan not found error message for a newly added image?
{: #faq_va_new_scan_error}
{: faq}

If you get the vulnerability report immediately after you add the image to the registry, you might receive the following error:

```sh
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://cloud.ibm.com/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support
```
{: screen}

You receive this message because the images are scanned asynchronously to the requests for results, and the scanning process takes a while to complete. During normal operation, the scan completes within the first few minutes after you add the image to the registry. The time that it takes to complete depends on variables like the image size and the amount of traffic that the registry is receiving.

If you get this message as part of a build pipeline and you see this error regularly, try adding some retry logic that contains a short pause.

If you still see unacceptable performance, contact support, see [Getting help and support for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-ts_index#gettinghelp).

## How often are the security notices updated?
{: #faq_va_update_security_notice}
{: faq}

Security notices for Vulnerability Advisor are loaded from the vendors' operating system sites approximately every 12 hours.


