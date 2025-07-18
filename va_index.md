---

copyright:
  years: 2017, 2025
lastupdated: "2025-06-27"

keywords: Image security, Vulnerability Advisor, security, registry, vulnerabilities, containers, registry, container registry, portieris, reviewing a vulnerability report, organizational exemption policies, exemption policies, vulnerable packages, data, exemptions, policy, vulnerability report, security issues

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Managing image security with Vulnerability Advisor
{: #va_index}

Vulnerability Advisor is provided as part of {{site.data.keyword.registrylong}}. Vulnerability Advisor checks the security status of container images that are provided by {{site.data.keyword.IBM_notm}}, third parties, or added to your organization's registry namespace.
{: shortdesc}

Vulnerability Advisor provides security management for [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started). Vulnerability Advisor generates a security status report that includes suggested fixes and best practices.

When you add an image to a namespace, the image is automatically scanned by Vulnerability Advisor to detect security issues and potential vulnerabilities. If security issues are found, instructions are provided to help fix the reported vulnerability.

Any issues that are found by Vulnerability Advisor result in a verdict that indicates that it is not advisable to deploy this image. If you choose to deploy the image, any containers that are deployed from the image include known issues that might be used to attack or otherwise compromise the container. The verdict is adjusted based on any exemptions that you specified.

Fixing the security issues that are reported by Vulnerability Advisor can help you to secure your {{site.data.keyword.cloud_notm}} infrastructure.

Using Portieris to block the deployment of images with issues that are found by Vulnerability Advisor is deprecated.
{: deprecated}

## About Vulnerability Advisor
{: #about}

Vulnerability Advisor provides functions to help you to secure your images.

The following functions are available in version 4:

- Scans images for issues.
- Creates an evaluation report that is based on security practices that are specific to {{site.data.keyword.containerlong_notm}}.
- Supplies instructions about how to fix a reported [vulnerable package](#packages) in its reports.
- Applies exemption policies to reports at an account, [namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace), [repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository), or [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) level to mark when issues that are flagged do not apply to your use case.

The **Security status** column in the **Images** tab of the {{site.data.keyword.registryshort}} dashboard displays the number of issues that are associated with each image. To find out more about the issues, click the link in the **Security status** column.

The Vulnerability Advisor dashboard provides an overview and assessment of the security for an image. If you want to find out more about the Vulnerability Advisor dashboard, see [Reviewing a vulnerability report](#va_reviewing).

Encrypted images aren't scanned by Vulnerability Advisor.
{: note}

### Data protection
{: #about_data_protection}

To scan images and containers in your account for security issues, Vulnerability Advisor collects, stores, and processes the following information:

- Free-form fields, including IDs, descriptions, and image names (registry, namespace, repository name, and image tag)
- Metadata about the file modes and creation timestamps of the configuration files
- The content of system and application configuration files in images and containers
- Installed packages and libraries (including their versions)

Do not put personal information into any field or location that Vulnerability Advisor processes, as identified in the preceding list.
{: important}

Scan results, aggregated at a data center level, are processed to produce anonymized metrics to operate and improve the service.

In version 4, the image is indexed when it is first pushed to {{site.data.keyword.registryshort}} registry, and that index report is stored in the database. When Vulnerability Advisor is queried, the image index report is retrieved, and a vulnerability assessment is produced. This action happens dynamically every time Vulnerability Advisor is queried. Therefore, no pregenerated scan result exists that requires deleting. However, the image index report is deleted within 30 days of the deletion of the image from the registry.

## Types of vulnerabilities
{: #types}

### Vulnerable packages
{: #packages}

Vulnerability Advisor checks for vulnerable packages in images that are using supported operating systems and provides a link to any relevant security notices about the vulnerability.

Packages that contain known vulnerability issues are displayed in the scan results. The possible vulnerabilities are updated daily by using the published security notices for the Docker image types that are listed in the following table. Typically, for a vulnerable package to pass the scan, a later version of the package is required that includes a fix for the vulnerability. The same package can list multiple vulnerabilities, and in this case, a single package update can address multiple vulnerabilities.

Vulnerability Advisor returns vulnerabilities only when a package fix is published by the distributor. Declared vulnerabilities that aren't fixed yet, or are not going to be fixed, are not reported by Vulnerability Advisor. Therefore, if Vulnerability Advisor does not report any vulnerabilities, there might still be a risk in the image.

For version 4, the image is indexed the first time that it is pushed. Thereafter, the vulnerability assessment is calculated every time Vulnerability Advisor is queried about that image. Images are scanned only if they have a tag.

The following tables show the supported Docker base images that Vulnerability Advisor checks for vulnerable packages.

Vulnerability Advisor supports only releases of platforms that are currently supported by the vendor of that platform.
{: important}

| Docker base image | Supported versions | Source of security notices |
|-------------------|--------------------|----------------------------|
| Alpine | All stable versions with vendor security support. Edge is also supported. | [Alpine SecDB database](https://secdb.alpinelinux.org/){: external}. |
| Debian | All stable versions with vendor security support.  \n  \n CVEs on binary packages that are associated with the Debian source package `linux`, such as `linux-libc-dev`, are not reported. Most of these binary packages are kernel and kernel modules, which are not run in container images. | [Debian Security Bug Tracker](https://security-tracker.debian.org/tracker/){: external}. |
| GoogleContainerTools distroless | All stable versions with vendor security support. | [GoogleContainerTools distroless](https://github.com/GoogleContainerTools/distroless){: external} |
| Red Hat&reg; Enterprise Linux&reg; (RHEL) | RHEL/UBI 7, RHEL/UBI 8, and RHEL/UBI 9 | [{{site.data.keyword.redhat_notm}} Security Data API](https://docs.redhat.com/en/documentation/red_hat_security_data_api/1.0/html/red_hat_security_data_api/index){: external}. |
| Ubuntu | All stable versions with vendor security support. | [Ubuntu CVE Tracker](https://launchpad.net/ubuntu-cve-tracker){: external}. |
{: caption="Supported Docker base images that Vulnerability Advisor 4 checks for vulnerable packages" caption-side="bottom"}
{: #table_registry_vpe_docker_images}

If you are using an image that is based on an Operating System Distribution in the preceding table, but at a version that is unsupported by the vendor and has no security feed data available, for example, Debian 10 or earlier, Vulnerability Advisor might report `No issues` for your image.
{: note}

### Configuration issues
{: #app_configurations}

Configuration issues are not supported in Vulnerability Advisor version 4.

## Setting the version of Vulnerability Advisor
{: #va_set_version}

To retrieve results from version 4, run the following [`ibmcloud cr va-version-set`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set) command. The only valid value is `v4`.

```txt
ibmcloud cr va-version-set v4
```
{: pre}

Alternatively, you can set an environment variable `va_version`, and specify the Vulnerability Advisor version that you want to use. The only valid value is `v4`.

If you try to set an invalid version of Vulnerability Advisor, you get en error, see [Why do I get an error about an invalid version of Vulnerability Advisor being specified?](/docs/Registry?topic=Registry-troubleshoot-va-version-error) for assistance.
{: tip}

## Reviewing a vulnerability report
{: #va_reviewing}

Before you deploy an image, you can review its Vulnerability Advisor report for details about any vulnerable packages and nonsecure container or app settings.

You can also check whether the image is compliant with organizational policies.

If you don't address any discovered issues, those issues can impact the security of containers that are using that image. If you use enforcement in your container runtime environment, you might be prevented from deploying that image unless all issues are exempted by your policy.

If your image does not meet the requirements that are set by your organization's policy, you must configure the image to meet those requirements before you can deploy it. For more information about how to view and change the organization policy, see [Setting organizational exemption policies](#va_managing_policy).
{: requirement}

### Reviewing a vulnerability report by using the console
{: #va_reviewing_gui}
{: help}
{: support}
{: ui}

You can review the security of the Docker images that are stored in your namespaces in {{site.data.keyword.registryshort}} by using the {{site.data.keyword.cloud_notm}} console.

1. Log in to {{site.data.keyword.cloud_notm}}.
2. Click the **Navigation menu** icon, then click **Container Registry**.
3. Click **Images**. A list of your images and the security status of each image is displayed in the **Images** table.
4. To see the report for the image that is tagged `latest`, click the row for that image. The **Image details** tab opens showing the data for that image. If no `latest` tag exists in the repository, the most recent image is used.
5. If the **Security status** column shows any issues, to find out about the issues, click the **Issues by type** tab. The **Vulnerabilities** table is displayed.

    - **Vulnerabilities** table. This table shows the Vulnerability ID for each issue, the policy status for that issue, the affected packages and how to resolve the issue. To see more information about that issue, expand the row. A summary of that issue is displayed that contains a link to the vendor security notice for that issue. Lists packages that contain known vulnerability issues.

        The list is updated daily by using published security notices for the Docker image types that are listed in [Types of vulnerabilities](#types). Typically, for a vulnerable package to pass the scan, a later version of the package is required that includes a fix for the vulnerability. The same package can list multiple vulnerabilities and in this case, a single package update can correct multiple issues. Click the security notice code to view more information about the package and for steps to update the package.

6. Complete the corrective action for each issue shown in the report, and rebuild the image.

### Reviewing a vulnerability report by using the CLI
{: #va_registry_cli}
{: help}
{: support}
{: cli}

You can review the security of Docker images that are stored in your namespaces in {{site.data.keyword.registrylong_notm}} by using the CLI.

1. List the images in your {{site.data.keyword.cloud_notm}} account. A list of all images is returned, independent of the namespace where they are stored.

    ```txt
    ibmcloud cr image-list
    ```
    {: pre}

2. Check the status in the **SECURITY STATUS** column.
    - `No Issues` No security issues were found.
    - `<X> Issues` The potential security issues or vulnerabilities that are found, where `<X>` is the number of issues.
    - `Scanning` The image is being scanned and the final vulnerability status is not determined.
    - `Unsupported OS` The scan found no supported operating system (OS) distribution.

3. To view the details for the status, review the Vulnerability Advisor report by running the following command. Where `REGION` is the region, `MY_NAMESPACE` is your namespace, `MY_IMAGE` is your image, and `TAG` is your tag.

    ```txt
    ibmcloud cr va REGION.icr.io/MY_NAMESPACE/MY_IMAGE:TAG
    ```
    {: pre}

## Setting organizational exemption policies
{: #va_managing_policy}

If you want to manage the security of an {{site.data.keyword.cloud_notm}} organization, you can use your policy setting to determine whether an issue is exempt or not.

You can deploy containers from any image regardless of security status.

To find out more about the required permissions for working with exemptions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

Using Portieris to block the deployment of images with issues that are found by Vulnerability Advisor is deprecated.
{: deprecated}

### Setting exemption policies by using the console
{: #va_managing_policy_gui}
{: help}
{: support}
{: ui}

If you are using the {{site.data.keyword.cloud_notm}} console, you can set a [namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace), [repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository), or [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) as the scope of the exemption policy. If you want to use the [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) as the scope, you must use the CLI, see [Setting organizational exemption policies by using the CLI](/docs/Registry?topic=Registry-va_index&interface=cli#va_managing_policy_cli).
{: note}

If you want to set exemptions from the policy by using the {{site.data.keyword.cloud_notm}} console, complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}}. You must be logged in to see Vulnerability Advisor in the {{site.data.keyword.cloud_notm}} console.
2. Click the **Navigation menu** icon, then click **Container Registry**.
3. Click **Settings**.
4. In the **Security policy exemptions** section, click **Create**.
5. Select the issue type.
6. Enter the issue ID.

    You can find this information in your [vulnerability report](#va_reviewing). The **Vulnerability ID** column contains the ID to use for CVE or security notice issues.
    {: tip}

7. Select the registry namespace, repository, image, and tag that you want the exemption to apply to.
8. Click **Create**.

You can also edit and remove exemptions by hovering over the relevant row and clicking the **open and close list of options** icon.

### Setting exemption policies by using the CLI
{: #va_managing_policy_cli}
{: help}
{: support}
{: cli}

If you are using the CLI, you can set a [namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace), [repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository), [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest), or [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) as the scope of the exemption policy.
{: note}

If you want to set exemptions from the policy by using the CLI, you can run the following commands:

- To create an exemption for a security issue, run the [`ibmcloud cr exemption-add`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add) command.
- To list your exemptions for security issues, run the [`ibmcloud cr exemption-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_list) command.
- To list the types of security issues that you can exempt, run the [`ibmcloud cr exemption-types`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_types) command.
- To delete an exemption for a security issue, run the [`ibmcloud cr exemption-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_rm) command.

For more information about the commands, you can use the `--help` option when you run the command.
