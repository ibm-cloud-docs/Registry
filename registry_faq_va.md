---

copyright:
  years: 2025
lastupdated: "2025-10-16"

keywords: commands, questions, registry, Vulnerability Advisor, frequently asked questions, image, package manager, security notices, version of a package, notify security status, vulnerabilities

subcollection: Registry

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for Vulnerability Advisor
{: #registry_faq_va}

Frequently asked questions for the Vulnerability Advisor component of {{site.data.keyword.registrylong}}.
{: shortdesc}

For frequently asked questions about {{site.data.keyword.registryshort}}, see [FAQ for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_faq).

## How do I manage any vulnerabilities?
{: #faq_va_vuln}
{: faq}

You can use the Vulnerability Advisor component of {{site.data.keyword.registrylong_notm}} to manage image security and vulnerabilities.

For more information, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui).

## How can I view all of the vulnerabilities?
{: #faq_va_vuln_view}
{: faq}

To view all the vulnerabilities that are found by the Vulnerability Advisor component of {{site.data.keyword.registrylong_notm}}, you need to access the dashboard. The dashboard provides an overview and assessment of the security for an image. The dashboard displays details about any vulnerable packages and nonsecure container or app configurations.

Encrypted images are not scanned by Vulnerability Advisor.
{: note}

To see the vulnerabilities in an image and address any vulnerabilities before you deploy the image, complete the following steps:
1. Log in to the {{site.data.keyword.cloud_notm}} console.
2. Navigate to {{site.data.keyword.registryshort_notm}} by clicking the **Navigation menu** icon and selecting **Container Registry**.
3. View a list of your images along with their security status by clicking **Images**.
4. If you see any issues, click the **Issues by type** tab to see the Vulnerabilities table. The Vulnerabilities table displays the Vulnerability ID, policy status, affected packages, and resolution steps for each issue.
5. To get more information about a specific issue, expand the corresponding row, which shows a summary of the issue along with a link to the vendor security notice.
6. Complete the corrective action for each issue and then rebuild the image.

For more information, see [Reviewing a vulnerability report](/docs/Registry?topic=Registry-va_index&interface=ui&locale=en#va_reviewing) and [About Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui&locale=en#about).

## How much does Vulnerability Advisor cost?
{: #faq_va_cost}
{: faq}

The cost of Vulnerability Advisor is built into the pricing for {{site.data.keyword.registrylong_notm}}. For more information, see [Billing for storage and pull traffic](/docs/Registry?topic=Registry-registry_overview#registry_billing_traffic).

## Can images from other registries be scanned by Vulnerability Advisor?
{: #faq_va_reg}
{: faq}

Vulnerability Advisor scans images from {{site.data.keyword.registrylong_notm}} only.

## How is a Vulnerability Advisor scan triggered?
{: #faq_va_trigger_scan}
{: faq}

For more information about how the scanning of an image by the Vulnerability Advisor component of {{site.data.keyword.registrylong_notm}} is triggered, see [Vulnerable packages](/docs/Registry?topic=Registry-va_index&interface=ui#packages).

## Why doesn't my image scan in Vulnerability Advisor v4?
{: #faq_va_v4_scan}
{: faq}

If your image isn't being scanned by the Vulnerability Advisor component of {{site.data.keyword.registrylong_notm}}, check that it has a [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag). In Vulnerability Advisor version 4, images are scanned only if they have a tag.

## Why doesn't a new image scan in Vulnerability Advisor?
{: #faq_va_new_scan_error}
{: faq}

If you get the vulnerability report immediately after you add the image to the [registry](#x2064940){: term}, you might receive the following error, where `<imagename>` is the name of your image:

```txt
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://cloud.ibm.com/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support
```
{: screen}

You receive this message because the images are scanned asynchronously to the requests for results, and the scanning process takes a while to complete. During normal operation, the scan completes within the first few minutes after you add the image to the registry. The time that it takes to complete depends on variables like the proportions of the image and the amount of traffic that the registry is receiving.

If you get this message as part of a build pipeline and you see this error regularly, try adding some retry logic that contains a short pause.

If you still see unacceptable performance, contact support, see [Getting help and support for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-help-and-support).

## How often are the security notices updated in Vulnerability Advisor?
{: #faq_va_update_security_notice}
{: faq}

Security notices for Vulnerability Advisor are loaded from the vendors' operating system sites approximately every 12 hours.

## How do I get notified about the security status of an image?
{: #faq_va_security_status}
{: faq}

You can see the security status of your images within the Vulnerability Advisor dashboard. You cannot set up notifications.

## Which version of a package is installed in my image?
{: #faq_va_package_version}
{: faq}

To determine the version of a package that is installed in your image, use the relevant package manager command for your operating system.

### Alpine package manager commands
{: #faq_va_package_version_alpine}

On Alpine, to determine the version of a package that is installed in your image, you can use the following commands, where `PACKAGE_NAME` is the name of your package.

- To list the metadata for a specific installed package, run the following command:

    ```txt
    apk info PACKAGE_NAME
    ```
    {: pre}

- To list all installed packages and their versions, run the following command:

    ```txt
    apk list
    ```
    {: pre}

### Debian and Ubuntu package manager commands
{: #faq_va_package_version_debian_ubuntu}

On Debian and Ubuntu, to determine the version of a package that is installed in your image, you can use the following commands, where `PACKAGE_NAME` is the name of your package.

- To list the metadata for a specific installed package, run either of the following commands:

    ```txt
    apt show PACKAGE_NAME
    ```
    {: pre}

    ```txt
    dpkg-query -l PACKAGE_NAME
    ```
    {: pre}

- To list all installed packages and their versions, run either of the following commands:

    ```txt
    apt list
    ```
    {: pre}

    ```txt
    dpkg-query -W
    ```
    {: pre}

### {{site.data.keyword.redhat_notm}} and CentOS package manager commands
{: #faq_va_package_version_redhat_centos}

On {{site.data.keyword.redhat_openshift_full}} and CentOS, to determine the version of a package that is installed in your image, you can use the following commands, where `PACKAGE_NAME` is the name of your package.

- To list the metadata for a specific installed package, run either of the following commands:

    ```txt
    rpm -qi PACKAGE_NAME
    ```
    {: pre}

    ```txt
    yum info PACKAGE_NAME
    ```
    {: pre}

- To list all installed packages and their versions, run either of the following commands:

    ```txt
    rpm -qa
    ```
    {: pre}

    ```txt
    yum list installed
    ```
    {: pre}

## Does Vulnerability Advisor have versions?
{: #faq_va_versions}
{: faq}

Vulnerability Advisor version 4 is the only version available. For more information, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui).
