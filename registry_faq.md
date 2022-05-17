---

copyright:
  years: 2018, 2022
lastupdated: "2022-05-17"

keywords: public images, commands, questions, registry, Vulnerability Advisor, frequently asked questions, namespace, tool, image, digest, access, region, package manager, security notices, version of a package

subcollection: Registry

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# Frequently asked questions about {{site.data.keyword.registryshort_notm}}
{: #registry_faq}

Frequently asked questions (FAQs) about {{site.data.keyword.registrylong}}.
{: shortdesc}

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

## How many namespaces can you have?
{: #faq_namespace}
{: faq}

You can have 100 registry [namespaces](x2031005){: term} in each region.

## Do images in the trash count toward my quota?
{: #faq_trash}
{: faq}

Images that are in the trash don't count toward your quota.

## How do I find the image digest?
{: #faq_digest}
{: faq}

You can find the long format of the image [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) by running one of the following commands. The digest is displayed in the **Digest** column of the CLI.

When you are using the digest to identify an image, always use the long format.
{: note}

- Run the [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) command:

    ```txt
    ibmcloud cr image-digests
    ```
    {: pre}

- Run the [`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) command:

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

To find the digests for your images, run the [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) command. You can refer to an image by using a combination of the **Repository** and **Digest** columns, for example, `repository@digest`.

## How do you use access control?
{: #faq_access_control}
{: faq}

You can create {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) policies to control access to your namespaces in {{site.data.keyword.registrylong_notm}}. For more information, see [Granting access to {{site.data.keyword.registrylong_notm}} resources tutorial](/docs/Registry?topic=Registry-iam_access) and [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).

## How can I share an image with many users?
{: #faq_share_image}
{: faq}

You can create an {{site.data.keyword.cloud_notm}} account and invite all the users to it. They can then all have access to any [namespace](x2031005){: term} that is created in the account. You can create a subset of the users and set an IAM access policy to differentiate access at the namespace level. Users can be members of many accounts, but you can't give access outside the account, that is, you can't share a namespace to multiple accounts. 

For more information, see [Defining IAM access policies](/docs/Registry?topic=Registry-user).

## Do I have any untagged images?
{: #faq_untagged_image_1}
{: faq}

To find out whether you have any [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, list your images by running the [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) command. Untagged images have a hyphen (-) in the **Tags** column.

## Do I need untagged images?
{: #faq_untagged_image_2}
{: faq}

If you have active containers that are running [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, you must retain the untagged images. If you delete untagged images that are in use, you can cause problems with scaling or automated restarts. Deleting untagged images might cause a problem in the following circumstances:

- The image was deployed by referencing the image by using the digest.
- The image reference was mutated by a webhook service, such as [Portieris](/docs/Registry?topic=Registry-security_enforce_portieris).

## What regions are available?
{: #faq_regions}
{: faq}

To find out about the regions that are available for {{site.data.keyword.registrylong_notm}}, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## How much does Vulnerability Advisor cost?
{: #faq_va_cost}
{: faq}

The cost of Vulnerability Advisor is built into the pricing for {{site.data.keyword.registrylong_notm}}. For more information, see [Billing for storage and pull traffic](/docs/Registry?topic=Registry-registry_overview#registry_billing_traffic).

## Can images from other registries be scanned?
{: #faq_va_reg}
{: faq}

Vulnerability Advisor scans images from {{site.data.keyword.registrylong_notm}} only.

## How is a Vulnerability Advisor scan triggered?
{: #faq_va_trigger_scan}
{: faq}

For more information about how the scanning of an image is triggered, see [Vulnerable packages](/docs/Registry?topic=va-va_index#packages).

## Why doesn't a new image scan?
{: #faq_va_new_scan_error}
{: faq}

If you get the vulnerability report immediately after you add the image to the [registry](x2064940){: term}, you might receive the following error:

```txt
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://cloud.ibm.com/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support
```
{: screen}

You receive this message because the images are scanned asynchronously to the requests for results, and the scanning process takes a while to complete. During normal operation, the scan completes within the first few minutes after you add the image to the registry. The time that it takes to complete depends on variables like the image size and the amount of traffic that the registry is receiving.

If you get this message as part of a build pipeline and you see this error regularly, try adding some retry logic that contains a short pause.

If you still see unacceptable performance, contact support, see [Getting help and support for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-ts_index#gettinghelp).

## How often are the security notices updated?
{: #faq_va_update_security_notice}
{: faq}

Security notices for Vulnerability Advisor are loaded from the vendors' operating system sites approximately every 12 hours.

## Which version of a package is installed in my image?
{: #faq_va_package_version}
{: faq}

To determine the version of a package that is installed in your image, use the relevant package manager command for your operating system.

### Alpine package manager commands
{: #faq_va_package_version_alpine}

On Alpine, to determine the version of a package that is installed in your image, you can use the following commands, where `<package_name>` is the name of your package.

- To list the metadata for a specific installed package, run the following command:

    ```txt
    apk info <package_name>
    ```
    {: pre}

- To list all installed packages and their versions, run the following command:

    ```txt
    apk list
    ```
    {: pre}

### Debian and Ubuntu package manager commands
{: #faq_va_package_version_debian_ubuntu}

On Debian and Ubuntu, to determine the version of a package that is installed in your image, you can use the following commands, where `<package_name>` is the name of your package.

- To list the metadata for a specific installed package, run either of the following commands:

    ```txt
    apt show <package_name>
    ```
    {: pre}

    ```txt
    dpkg-query -l <package_name>
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

### Red Hat and CentOS package manager commands
{: #faq_va_package_version_redhat_centos}

On {{site.data.keyword.redhat_notm}} and CentOS, to determine the version of a package that is installed in your image, you can use the following commands, where `<package_name>` is the name of your package.

- To list the metadata for a specific installed package, run either of the following commands:

    ```txt
    rpm -qi <package_name>
    ```
    {: pre}

    ```txt
    yum info <package_name>
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


