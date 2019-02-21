---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, vulnerability of images, security of images, security issues

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

# Monitoring the vulnerability of images
{: #registry_ui}

You can view information about potential vulnerabilities, and the security of images in the {{site.data.keyword.registrylong}} public and private repositories by using the {{site.data.keyword.Bluemix_notm}} console.
{:shortdesc}

The **Security Status** column shows you the following information about the image:

- `Secure` No security issues were found.
- `Vulnerable` Security or configuration issues were found and must be addressed before you can deploy the image.
- `Incomplete` The scan is not complete. The scan might still be running or the image’s operating system might not be compatible. Wait and try the scan again. If the scan still does not complete, push the image again to start a new scan. Images with incomplete scans are not blocked for deployment.
- `Unsupported OS` The operating system in the image is not supported.

To view the graphical user interface, use the following steps:

1. Log in to the {{site.data.keyword.cloud_notm}} console ([https://cloud.ibm.com/login ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login)) with your IBMid.
2. If you have multiple {{site.data.keyword.Bluemix_notm}} accounts, select the account and region that you want to use from the account menu.
3. Click **Catalog**.
4. Select the **Containers** category and click the **Container Registry** tile.
5. To view information about images in your private repositories, click **Images**. A list of images in your private repositories and the security status for each image is displayed.
6. To find out more information about the potential vulnerabilities, including the tags and the image digest, click the row for the image in the table. The **Image Details** tab opens.
7. To find out about the issues by type, click the **Issues by Type** tab.
8. To find out about the associated containers, click the **Associated Containers** tab.

To find out more about what the information in the security report means, see [Managing image security with Vulnerability Advisor](/docs/services/va/va_index.html).
