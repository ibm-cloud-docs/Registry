---

copyright:
  years: 2019, 2025
lastupdated: "2025-04-14"

keywords: IBM Cloud Container Registry release notes, change, January, February, March, April, May, June, July, August, September, October, November, December, registry, images, vulnerability advisor, what's new, whats new, what is new

subcollection: Registry

content-type: release-note

---


{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.registryshort}}
{: #registry_release_notes}

What's new in {{site.data.keyword.registrylong}} and Vulnerability Advisor. The changes are grouped by date.
{: shortdesc}

## 14 February 2025
{: #registry-14feb2025}
{: release-note}

Access {{site.data.keyword.registrylong_notm}} by using trusted profiles {: #14feb2025_trustprof}
:   You can use trusted profiles to grant different {{site.data.keyword.cloud_notm}} identities access to {{site.data.keyword.registrylong_notm}} resources in your account. Automatically grant federated users access to your account with conditions based on SAML attributes from your corporate directory.

    For more information, see [Accessing {{site.data.keyword.registryshort_notm}} by using trusted profiles](/docs/Registry?topic=Registry-registry_access_trusted_profiles).

## 9 December 2024
{: #registry-09dec2024}
{: release-note}

Content delivery network (CDN) is enabled for users that pull {{site.data.keyword.registrylong_notm}} images from global (`icr.io`) over a public network {: #09dec2024_cdn}
:   To ensure continued worldwide performance for global registry (`icr.io`) in {{site.data.keyword.registrylong_notm}}, a content delivery network (CDN) is now enabled.

## 26 June 2024
{: #registry-26jun2024}
{: release-note}

Firewall changes from 4 September 2024 for users that pull {{site.data.keyword.registrylong_notm}} images from global (`icr.io`) {: #26jun2024_firewall}
:   To ensure continued worldwide performance for global registry (`icr.io`) in {{site.data.keyword.registrylong}}, a content delivery network (CDN) is being enabled that means that you might have to adjust your firewall settings. If you need to adjust your firewall settings, you must adjust them by 4 September 2024.

    For more information, see [Important firewall changes from 4 September 2024 for users that pull {{site.data.keyword.registrylong_notm}} images from global (`icr.io`)](/docs/Registry?topic=Registry-registry_notices_firewall).

## 15 March 2024
{: #registry-15mar2024}
{: release-note}

New region in Madrid {: #15mar2024_madrid}
:   A new region in Madrid, Spain is available. The new region is `eu-es` and the domain name is `es.icr.io`. For more information, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

## 13 November 2023
{: #registry-13nov2023}
{: release-note}

Discontinuation of Vulnerability Advisor version 3 {: #13nov2023_va3}
:   Vulnerability Advisor version 3 is discontinued.

    For more information about how to update to Vulnerability Advisor version 4, see [Vulnerability Advisor version 3 is being discontinued on 13 November 2023](/docs/Registry?topic=Registry-registry_notices_va_v3).

## 11 October 2023
{: #registry-11oct2023}
{: release-note}

Vulnerability Advisor version 3 is discontinued from 13 November 2023 {: #registry-11oct2023_v3}
:   Vulnerability Advisor version 3 is being discontinued on 13 November 2023. If you have version 3 set as the default, you must update to Vulnerability Advisor version 4 by 13 November 2023. If you are already using version 4, no action is required.

    For more information about how to update to version 4, see [Vulnerability Advisor version 3 is being discontinued on 13 November 2023](/docs/Registry?topic=Registry-registry_notices_va_v3).

## 24 July 2023
{: #registry-24jul2023}
{: release-note}

Added the option to output several {{site.data.keyword.registrylong_notm}} commands in JSON format {: #registry-24jul2023_json_option}
:   The following {{site.data.keyword.registrylong_notm}} commands now have an output option for JSON format:

    - `ibmcloud cr exemption-add`
    - `ibmcloud cr exemption-list`
    - `ibmcloud cr exemption-types`
    - `ibmcloud cr image-list`
    - `ibmcloud cr namespace-list`
    - `ibmcloud cr plan`
    - `ibmcloud cr quota`
    - `ibmcloud cr retention-policy-list`

    For more information about the {{site.data.keyword.registrylong_notm}} commands, see [{{site.data.keyword.registrylong_notm}} CLI](/docs/Registry?topic=Registry-containerregcli)

The `--json` option for {{site.data.keyword.registrylong_notm}} commands is deprecated {: #registry-24jul2023_json}
:   The `--json` option is replaced with the `--output json` option in the following commands:

    - `ibmcloud cr image-digests`
    - `ibmcloud cr image-prune-untagged`
    - `ibmcloud cr image-retention-run`
    - `ibmcloud cr trash-list`

    For more information about the {{site.data.keyword.registrylong_notm}} commands, see [{{site.data.keyword.registrylong_notm}} CLI](/docs/Registry?topic=Registry-containerregcli)

## 19 June 2023
{: #registry-19jun2023}
{: release-note}

Vulnerability Advisor version 3 is deprecated from 19 June 2023 {: #registry-19jun2023_v3}
:   For more information about how to update to version 4, see [Update Vulnerability Advisor to version 4 by 19 June 2023](/docs/Registry?topic=Registry-registry_notices_va_v4).

## 19 May 2023
{: #registry-19may2023}
{: release-note}

Update Vulnerability Advisor to version 4 by 19 June 2023 {: #19may2023_va_v4}
:   The Vulnerability Advisor component of {{site.data.keyword.registrylong}} is being updated.

    Vulnerability Advisor version 3 is being deprecated as the default on 19 June 2023. From 19 June 2023, the default will be Vulnerability Advisor version 4. If you have version 3 set as the default, you can continue to use version 3 until the end of support date. An end of support date is not available yet.

    For more information, see [Update Vulnerability Advisor to version 4 by 19 June 2023](/docs/Registry?topic=Registry-registry_notices_va_v4).

## 26 April 2023
{: #registry-26apr2023}
{: release-note}

Using Portieris to block the deployment of images with issues is deprecated. {: #26apr2023_portieris}
:   The use of Portieris to block the deployment of images with issues that are found by Vulnerability Advisor is deprecated.

## 11 November 2022
{: #registry-11nov2022}
{: release-note}

Change to virtual private endpoints {: #11nov2022_vpe}
:   Virtual private endpoints are changing.

    On 11 November 2022, virtual private endpoints (VPEs) for {{site.data.keyword.registrylong_notm}} are being updated and the existing VPE version is being deprecated on 15 December 2022. If you use {{site.data.keyword.registryshort_notm}} VPE gateways, you must create new VPE gateways and remove your VPE gateways that were created before 11 November 2022 at the earliest opportunity so that you pick up these changes. VPE gateways that were created before 11 November 2022 are deprecated and will not work after 15 December 2022.

    If you create a new {{site.data.keyword.registryshort}} VPE gateway after 11 November 2022 and also use {{site.data.keyword.iamshort}} (IAM) [restricted IP address lists](/docs/account?topic=account-ips&interface=ui), you must ensure that your restricted IP address list contains the Cloud Service Endpoint (CSE) source IP addresses of the VPCs in which your {{site.data.keyword.registryshort}} VPE gateways exist. This requirement is related to a previous change to how {{site.data.keyword.registryshort}} works over the private network that the new VPE version also uses, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network).

    For more information, see [Changes to {{site.data.keyword.registryshort}} VPE gateways from 11 November 2022](/docs/Registry?topic=Registry-registry_notices_vpe).

## 2 November 2022
{: #registry-2nov2022}
{: release-note}

Changes to private IP addresses from 15 December 2022 {: #2nov2022_ip}
:  The {{site.data.keyword.registrylong_notm}} private IP addresses that were replaced on 5 July 2022 are being decommissioned on 15 December 2022.

    IP addresses for accessing {{site.data.keyword.registryshort}} over the private network changed on 5 July 2022, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network). You continue to be able to use these old IP addresses, but they are due to be decommissioned on 15 December 2022. After this date, you will not be able to access {{site.data.keyword.registryshort}} by using these IP addresses.

    For more information, see [Changes to private IP addresses from 15 December 2022](/docs/Registry?topic=Registry-registry_notices_ip_address).

## 15 September 2022
{: #registry-15sep2022}
{: release-note}

{{site.data.keyword.registryshort}} plug-in 1.0.0 is available {: #15sep2022_v1}
:   A new version, version 1.0.0, of the {{site.data.keyword.registryshort}} CLI plug-in is available. To update the version of your {{site.data.keyword.registryshort}} CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).

    Version 1.0.0 includes [Vulnerability Advisor 4](/docs/Registry?topic=Registry-registry_release_notes#15sep2022_va_version_4).

    In version 1.0.0, the `ibmcloud cr image-list` and `ibmcloud cr image-digests` commands no longer include security status by default. To include security status, you can either add the `--va` option to the command, or use the [`ibmcloud cr va`](/docs/Registry?topic=Registry-containerregcli#bx_cr_va) command to query the security status for an individual image.

    For more information, see [{{site.data.keyword.registryshort}} CLI stops returning security status results in lists by default from version 1.0.0](/docs/Registry?topic=Registry-registry_notices_lists).

All releases of {{site.data.keyword.registryshort}} plug-in 0.1 are deprecated {: #15sep2022_v0}
:   All releases of version 0.1 of the {{site.data.keyword.registryshort}} CLI plug-in are deprecated. You can continue to use releases of version 0.1, but version 1.0.0 is available for you to use. Version 0.1 will continue to be updated with any required updates until 15 September 2023. To update the version of your CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).

Vulnerability Advisor 4 is available from {{site.data.keyword.registryshort}} plug-in 1.0.0 {: #15sep2022_va_version_4}
:   From {{site.data.keyword.registryshort}} plug-in 1.0.0, you can choose whether to use Vulnerability Advisor version 3 or version 4 to run your commands. Vulnerability Advisor 4 is available from version 1.0.0 of the {{site.data.keyword.registryshort}} plug-in. Vulnerability Advisor 3 is the default.

    If you want to continue to use version 3, you don't need to do anything.

    If you want to use version 4 to run the `ibmcloud cr va`, `ibmcloud cr image-list`, or `ibmcloud cr image-digests` commands, see [Setting the version of Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui#va_set_version).

    For more information about Vulnerability Advisor, see [About Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui#about). For more information about Vulnerability Advisor API 4, see [Vulnerability Advisor 4 for {{site.data.keyword.registrylong_notm}}](https://{DomainName}/apidocs/vulnerability-advisor).

New commands for setting and checking the Vulnerability Advisor version are available from {{site.data.keyword.registryshort}} plug-in 1.0.0 {: #15sep2022_va_version_commands}
:   From {{site.data.keyword.registryshort}} plug-in 1.0.0, you can use new commands to check and set Vulnerability Advisor versions.

    If you want to continue to use version 3, you don't need to do anything.

    If you want to use version 4, you can set the version by running the [`ibmcloud cr va-version-set`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set) command.

    For more information about setting the version by using the `ibmcloud cr va-version-set` command, see [`ibmcloud cr va-version-set`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set) and [Setting the version of Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui#va_set_version).

    To find out which version of Vulnerability Advisor that you're running, see [`ibmcloud cr va-version`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version).

## 3 August 2022
{: #registry-03aug2022}
{: release-note}

The CLI stops returning security status results in lists by default from version 1.0.0 {: #03aug2022_list}
:   From {{site.data.keyword.registrylong_notm}} CLI plug-in version 1.0.0, when you use the [`ibmcloud cr image-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) and [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) commands to list images, they return Vulnerability Advisor security status results only if you use the `--va` option.

    If you want to continue to receive security status with your lists, prepare to upgrade by adding the new `--va` option to your commands.

    For more information, see [{{site.data.keyword.registryshort}} CLI stops returning security status results in lists by default from version 1.0.0](/docs/Registry?topic=Registry-registry_notices_lists).

## 8 July 2022
{: #registry-08jul2022}
{: release-note}

Context-based restrictions {: #08jul2022_cbr}
:   You can use context-based restrictions to define and enforce access restrictions for {{site.data.keyword.cloud_notm}} resources based on the network location of access requests.

    For more information, see [Protecting {{site.data.keyword.registryshort}} resources with context-based restrictions](/docs/Registry?topic=Registry-registry-cbr&interface=ui).

## 5 July 2022
{: #registry-05jul2022}
{: release-note}

Change to {{site.data.keyword.registryshort}} private IP addresses in all regions {: #05jul2022_private_network}
:   If you're using {{site.data.keyword.iamshort}} (IAM) restricted IP address lists and you are connecting to {{site.data.keyword.registryshort}} over the private network, your lists of allowed IP addresses must now include the private subnet and IP addresses of your own hosts. The {{site.data.keyword.registrylong_notm}} private IP addressees also changed. This change also affects you if you have allowlists or a firewall rule.

    For more information, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network) and [Using IAM IP address access restrictions](/docs/Registry?topic=Registry-registry_iam_ip).

All accounts require IAM access policies {: #05jul2022_iam}
:   To access {{site.data.keyword.registrylong_notm}}, you must be using {{site.data.keyword.iamshort}} (IAM) access policies. You must ensure that you are using IAM access policies to manage access to the {{site.data.keyword.registryshort}} service.

    Policy-free authorization is discontinued in the following {{site.data.keyword.registryshort}} regions:

    - `au-syd`
    - `eu-de`
    - `eu-gb`
    - `jp-tok`
    - `us-south`

    For more information about mapping the region name to the domain, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

    Other regions are unaffected because they already require IAM access policies for all accounts.

    For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy) and [Defining IAM access policies](/docs/Registry?topic=Registry-user).

## 23 June 2022
{: #registry-23jun2022}
{: release-note}

Change to {{site.data.keyword.registryshort}} private IP addresses in the following regions only: `br-sao`, `ca-tor` {: #23jun2022_private_network}
:   If you're using {{site.data.keyword.iamshort}} (IAM) restricted IP address lists and you're connecting to {{site.data.keyword.registryshort}} over the private network in the `br-sao` and `ca-tor` regions, your lists of allowed IP addresses must now include the private subnet and IP addresses of your own hosts. The {{site.data.keyword.registrylong_notm}} private IP addressees also changed. This change also affects you if you have allowlists or a firewall rule. Other regions are not affected yet.

    For more information, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network) and [Using IAM IP address access restrictions](/docs/Registry?topic=Registry-registry_iam_ip).

## 20 April 2022
{: #registry-20apr2022}
{: release-note}

{{site.data.keyword.registryshort}} private IP addresses are changing from 23 June 2022 {: #20apr2022_private_network}
:   By 23 June 2022, if you're using {{site.data.keyword.iamshort}} (IAM) restricted IP address lists and you're connecting to {{site.data.keyword.registryshort}} over the private network, you must update your lists of allowed IP addresses to include the private subnet and IP addresses of your own hosts. The {{site.data.keyword.registrylong_notm}} private IP addressees are also changing, which might require updates to your firewall configuration.

    For more information, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network).

## 1 March 2022
{: #registry-01mar2022}
{: release-note}

Amendment to the minimum supported Docker version for {{site.data.keyword.registryshort}} {: #01mar2022_docker}
:   From 1 March 2022, the minimum version of Docker Engine that is supported by {{site.data.keyword.registryshort}} is v17.07, or later.

## 9 February 2022
{: #registry-09feb2022}
{: release-note}

All accounts will require IAM access policies from 5 July 2022 {: #09feb2022_iam}
:   From 5 July 2022, to access {{site.data.keyword.registrylong_notm}}, you must be using {{site.data.keyword.iamshort}} (IAM) access policies. If you started to use {{site.data.keyword.registryshort}} before the availability of [IAM API key policies in {{site.data.keyword.registryshort}}](#registry-25feb2019) in February 2019, you must now ensure that you're using IAM access policies to manage access to the {{site.data.keyword.registryshort}} service.

    Policy-free authorization will be discontinued in the following {{site.data.keyword.registryshort}} regions:

    - `au-syd`
    - `eu-de`
    - `eu-gb`
    - `jp-tok`
    - `us-south`

    For more information about mapping the region name to the domain, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

    Other regions are unaffected because they already require IAM access policies for all accounts.

    For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy) and [Defining IAM access policies](/docs/Registry?topic=Registry-user).

## 2 February 2022
{: #registry-02feb2022}
{: release-note}

Replication of exemption policies between {{site.data.keyword.IBM_notm}} regions is discontinued {: #02feb2022_exemption}
:   From 2 February 2022, all regions require separate exemption policy management. Exemption policies are used to exclude any matching vulnerabilities or configuration issues from Vulnerability Advisor reports. You can set an exemption policy by running the [`ibmcloud cr exemption-add`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add) command, see [Setting organizational exemption policies](/docs/Registry?topic=Registry-va_index&interface=ui#va_managing_policy).

    For more information, see [{{site.data.keyword.registryshort_notm}} is ending exemption synchronization across regions on 31 January 2022](/docs/Registry?topic=Registry-registry_notices_exemptions).

## 1 February 2022
{: #registry-01feb2022}
{: release-note}

Storage that is used by untagged images is being charged for {: #01feb2022_billing}
:   From 1 February 2022, {{site.data.keyword.registrylong_notm}} is charging for the storage that is used by [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images. To reduce the amount that you're charged, you can [clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged). You can also [free up used storage and change service plans or quota limits to stay within given quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup).

    For more information, see [{{site.data.keyword.registryshort_notm}} to bill for storage used by untagged images from 1 February 2022](/docs/Registry?topic=Registry-registry_notices_billing).

## 17 January 2022
{: #registry-17jan2022}
{: release-note}

View the activity tracker auditing events for {{site.data.keyword.redhat_notm}} signing {: #17jan2022_sig}
:   You can view the activity tracker auditing events for [{{site.data.keyword.redhat_notm}} Signing](https://www.redhat.com/en/blog/container-image-signing){: external} operations.

    For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).
## 27 June 2017
{: #registry-27jun2017}
{: release-note}

Introducing {{site.data.keyword.registrylong_notm}} {: #27jun2017_ga}
:   {{site.data.keyword.registrylong_notm}} is available as a service in {{site.data.keyword.cloud_notm}}. [{{site.data.keyword.registryshort}}](https://www.ibm.com/products/container-registry){: external} provides a multi-tenant private image registry that you can use to store and share your container images with users in your {{site.data.keyword.cloud_notm}} account.

    For more information about how to use {{site.data.keyword.registryshort}}, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started).
