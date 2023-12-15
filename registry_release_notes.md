---

copyright:
  years: 2019, 2023
lastupdated: "2023-12-15"

keywords: IBM Cloud Container Registry release notes, change, January, February, March, April, May, June, July, August, September, October, November, December, registry, images, vulnerability advisor

subcollection: Registry

content-type: release-note

---


{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.registryshort}}
{: #registry_release_notes}

Learn about the changes to {{site.data.keyword.registrylong}} and Vulnerability Advisor. The changes are grouped by date.
{: shortdesc}

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

JSON output option added to several {{site.data.keyword.registrylong_notm}} commands {: #registry-24jul2023_json_option}
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

    If you want to use version 4 to run the `ibmcloud cr va`, `ibmcloud cr image-list`, or `ibmcloud cr image-digests` commands, see [Setting the Vulnerability Advisor version](/docs/Registry?topic=Registry-va_index&interface=ui#va_set_version).

    For more information about Vulnerability Advisor, see [About Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui#about). For more information about Vulnerability Advisor API 4, see [Vulnerability Advisor 4 for {{site.data.keyword.registrylong_notm}}](https://{DomainName}/apidocs/vulnerability-advisor).

New commands for setting and checking the Vulnerability Advisor version are available from {{site.data.keyword.registryshort}} plug-in 1.0.0 {: #15sep2022_va_version_commands}
:   From {{site.data.keyword.registryshort}} plug-in 1.0.0, you can use new commands to check and set Vulnerability Advisor versions.

    If you want to continue to use version 3, you don't need to do anything.

    If you want to use version 4, you can set the version by running the [`ibmcloud cr va-version-set`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set) command.

    For more information about setting the version by using the `ibmcloud cr va-version-set` command, see [`ibmcloud cr va-version-set`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set) and [Setting the Vulnerability Advisor version](/docs/Registry?topic=Registry-va_index&interface=ui#va_set_version).

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
:   If you are using {{site.data.keyword.iamshort}} (IAM) restricted IP address lists and you are connecting to {{site.data.keyword.registryshort}} over the private network, your lists of allowed IP addresses must now include the private subnet and IP addresses of your own hosts. The {{site.data.keyword.registrylong_notm}} private IP addressees also changed. This change also affects you if you have allowlists or a firewall rule.

    For more information, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network) and [Using IAM IP address access restrictions](/docs/Registry?topic=Registry-registry_iam_ip).

All accounts require IAM access policies {: #05jul2022_iam}
:   To access {{site.data.keyword.registrylong_notm}}, you must be using {{site.data.keyword.iamshort}} (IAM) access policies. You must ensure that you are using IAM access policies to manage access to the {{site.data.keyword.registryshort}} service.

    Policy-free authorization is discontinued in the following {{site.data.keyword.registryshort}} regions:

    - `us-south (us.icr.io)`
    - `uk-south (uk.icr.io)`
    - `eu-central (de.icr.io)`
    - `ap-south (au.icr.io)`
    - `ap-north (jp.icr.io)`

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

    - `us-south (us.icr.io)`
    - `uk-south (uk.icr.io)`
    - `eu-central (de.icr.io)`
    - `ap-south (au.icr.io)`
    - `ap-north (jp.icr.io)`

    Other regions are unaffected because they already require IAM access policies for all accounts.

    For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy) and [Defining IAM access policies](/docs/Registry?topic=Registry-user).

## 2 February 2022
{: #registry-02feb2022}
{: release-note}

Replication of exemption policies between {{site.data.keyword.IBM_notm}} regions is discontinued {: #02feb2022_exemption}
:   From 2 February 2022, all regions require separate exemption policy management. Exemption policies are used to exclude any matching vulnerabilities or configuration issues from Vulnerability Advisor reports. You can set an exemption policy by running the [`ibmcloud cr exemption-add`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add) command, see [Setting organizational exemption policies](/docs/Registry?topic=Registry-va_index&interface=ui#va_managing_policy).

    For more information, see [{{site.data.keyword.registrylong_notm}} Is Ending Exemption Synchronization Across Regions](https://www.ibm.com/blog/announcement/ibm-cloud-container-registry-is-ending-exemption-synchronization-across-regions/){: external}.

## 1 February 2022
{: #registry-01feb2022}
{: release-note}

Storage that is used by untagged images is being charged for {: #01feb2022_billing}
:   From 1 February 2022, {{site.data.keyword.registrylong_notm}} is charging for the storage that is used by [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images. To reduce the amount that you're charged, you can [clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged). You can also [free up used storage and change service plans or quota limits to stay within given quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup).

    For more information, see [Starting 1 February 2022, {{site.data.keyword.registrylong_notm}} will be billing for the storage that is used by untagged images](https://www.ibm.com/blog/announcement/ibm-cloud-container-registry-to-bill-for-storage-used-by-untagged-images/){: external}.

## 17 January 2022
{: #registry-17jan2022}
{: release-note}

View {{site.data.keyword.at_full_notm}} events for {{site.data.keyword.redhat_notm}} signing {: #17jan2022_sig}
:   You can view {{site.data.keyword.at_short}} events for [{{site.data.keyword.redhat_notm}} Signing](https://www.redhat.com/en/blog/container-image-signing){: external} operations.

    For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

## 7 December 2021
{: #registry-07dec2021}
{: release-note}

Define configuration rules for {{site.data.keyword.registryshort}} {: #07dec2021_gov}
:   As a security or compliance focal, you can use the **Govern resources** section of the {{site.data.keyword.compliance_short}} dashboard to define [configuration rules](#x3084914){: term} for {{site.data.keyword.registryshort}}.

    For more information, see [Managing security and compliance for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-manage-security-compliance).

## 1 November 2021
{: #registry-01nov2021}
{: release-note}

Using Notary v1 for signing images is discontinued {: #01nov2021_notary}
:   The Notary v1 service that supports [Docker Content Trust](https://docs.docker.com/engine/security/trust/){: external} and `docker trust` commands in {{site.data.keyword.registryshort}} is discontinued from 1 November 2021.

    {{site.data.keyword.registryshort}} supports the [{{site.data.keyword.redhat_notm}} Signing](https://www.redhat.com/en/blog/container-image-signing){: external} model. For more information, see [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig).

## 5 October 2021
{: #registry-05oct2021}
{: release-note}

{{site.data.keyword.registryshort}} container builds are discontinued {: #05oct2021_build}
:   The `ibmcloud cr build` command is discontinued from 5 October 2021. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead.

    For more information, see [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/blog/announcement/ibm-cloud-container-registry-deprecating-container-builds/){: external}.

## 2 September 2021
{: #registry-02sep2021}
{: release-note}

Namespaces that are assigned to a resource group show in the Resource list page {: #02sep2021_resource_list}
:   Namespaces that are assigned to a resource group show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console. For more information, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan).

## 30 August 2021
{: #registry-30aug2021}
{: release-note}

New region in Brazil {: #30aug2021_brazil}
:   A new region in Sao Paulo, Brazil is available. The new region is `br-sao` and the domain name is `br.icr.io`. For more information, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

## 19 August 2021
{: #registry-19aug2021}
{: release-note}

Using registry tokens is discontinued {: #19aug2021_remove_tokens}
:   From 19 August 2021, registry tokens are no longer accepted for authentication. For more information, see [{{site.data.keyword.registrylong_notm}} Deprecates Registry Tokens for Authentication](https://www.ibm.com/blog/announcement/ibm-cloud-container-registry-deprecates-registry-tokens-for-authentication/){: external}.

## 9 August 2021
{: #registry-09aug2021}
{: release-note}

The `ibmcloud cr login` command logs you into the `<region>.icr.io` registry domain only {: #09aug2021_bmx}
:   From version 0.1.541 of the {{site.data.keyword.registryshort_notm}} CLI, the `ibmcloud cr login` command logs you in to the `<region>.icr.io` registry domain only, where `<region>` is your [region](/docs/Registry?topic=Registry-registry_overview#registry_regions). If you want to log in to the deprecated domain, `registry.<region>.bluemix.net`, use `docker login`, see [Authentication](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth).

## 8 July 2021
{: #registry-08jul2021}
{: release-note}

Using Notary v1 for signing images is deprecated {: #08jul2021_notary}
:   The Notary v1 service for signing images is deprecated. It is being removed from {{site.data.keyword.registryshort}} on 31 August 2021.

    As an alternative approach, {{site.data.keyword.registryshort}} supports the [{{site.data.keyword.redhat_notm}} Signing](https://www.redhat.com/en/blog/container-image-signing){: external} model. For more information, see [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig).

## 21 June 2021
{: #registry-21jun2021}
{: release-note}

Global registry {: #21jun2021_global}
:   The global registry (`icr.io`) is now available for hosting user images and namespaces. Previously the global registry hosted only public images that are provided by {{site.data.keyword.IBM_notm}}. For more information, see [Global registry](/docs/Registry?topic=Registry-registry_overview#registry_regions_global).

## 10 May 2021
{: #registry-10may2021}
{: release-note}

New region in Canada {: #10may2021_canada}
:   A new region in Toronto, Canada is available. The new region is `ca-tor` and the domain name is `ca.icr.io`. For more information, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

## 4 May 2021
{: #registry-04may2021}
{: release-note}

The `ibmcloud cr ppa-archive-load` command is discontinued {: #04may2021_ppa}
:   The `ibmcloud cr ppa-archive-load` command is discontinued. Containerized software is distributed in {{site.data.keyword.cloud_notm}} Paks, see [{{site.data.keyword.cloud_notm}} Paks](https://www.ibm.com/cloud-paks){: external}. To run {{site.data.keyword.cloud_notm}} Paks on {{site.data.keyword.openshiftlong_notm}}, see [Adding Cloud Paks](/docs/openshift?topic=openshift-openshift_cloud_paks). For more information about setting up your {{site.data.keyword.containerlong_notm}} cluster to pull entitled software, see [Setting up a cluster to pull entitled software](/docs/containers?topic=containers-registry#secret_entitled_software).

## 18 February 2021
{: #registry-18feb2021}
{: release-note}

Increase the performance of the `ibmcloud cr image-list` and `ibmcloud cr image-digests` commands by using the `--no-va` option {: #18feb2021_no-va}
:   If you don't need the security status (Vulnerability Advisor) results as part of the output of the [`ibmcloud cr image-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) or [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) commands, you can use the `--no-va` option to increase performance.

## 15 February 2021
{: #registry-15feb2021}
{: release-note}

New region in Japan {: #15feb2021_japan}
:   A new region in Japan is available. The new region is `jp-osa` and the domain name is `jp2.icr.io`. For more information, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

## 19 November 2020
{: #registry-19nov2020}
{: release-note}

You can use Portieris to enforce container image security {: #19nov2020_portieris}
:   With effect from 19 November 2020, Container Image Security Enforcement is deprecated. To enforce container image security, you can use [Portieris](https://github.com/IBM/portieris){: external}. You can use Portieris to control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/Registry?topic=Registry-registry_trustedcontent) is properly applied to the image.

    For more information, see [Enforcing container image security by using Portieris](/docs/Registry?topic=Registry-security_enforce_portieris).

## 21 October 2020
{: #registry-21oct2020}
{: release-note}

Find out about the usage on your account by using platform metrics {: #21oct2020_metrics}
:   You can use the [`ibmcloud cr platform-metrics`](/docs/Registry?topic=Registry-containerregcli#ic_cr_platform_metrics) command to enable and disable platform metrics, and to find out whether you have platform metrics set up on your account.

    For more information, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor).

## 6 October 2020
{: #registry-06oct2020}
{: release-note}

{{site.data.keyword.registryshort}} container builds are deprecated {: #06oct2020_build}
:   The `ibmcloud cr build` command, which builds an image in {{site.data.keyword.cloud_notm}} and pushes it to {{site.data.keyword.registryshort_notm}}, is deprecated from 6 October 2020. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead.

    For more information, see [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/blog/announcement/ibm-cloud-container-registry-deprecating-container-builds/){: external}.

## 27 August 2020
{: #registry-27aug2020}
{: release-note}

Setting exemption policies by digest {: #27aug2020_digest}
:   When you want to set up an exemption policy, you can set the scope by namespace, repository, digest, or tag. You can set an exemption policy by running the [`ibmcloud cr exemption-add`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add) command.

    For more information, see [Setting organizational exemption policies](/docs/Registry?topic=Registry-va_index&interface=ui#va_managing_policy).

## 12 August 2020
{: #registry-12aug2020}
{: release-note}

Using UAA tokens is discontinued {: #12aug2020_tokens}
:   From 12 August 2020, UAA tokens are no longer accepted for authentication. At the moment, registry tokens continue to be accepted, but their use is deprecated.

    For more information, see [Announcing End of {{site.data.keyword.registrylong_notm}} Support for UAA Tokens](https://www.ibm.com/blog/announcement/announcing-end-of-ibm-cloud-container-registry-support-for-uaa-tokens/){: external}.

## 30 July 2020
{: #registry-30jul2020}
{: release-note}

New access roles are required for Vulnerability Advisor exemption policies {: #30jul2020_exemption}
:   If you want to manage your Vulnerability Advisor exemption policies for security issues, depending on the task that you want to complete, you might have to update your access role.

    For more information, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## 29 July 2020
{: #registry-29jul2020}
{: release-note}

You can set permissions so that access to resources within a namespace can be configured at the resource group level {: #29jul2020_resource_group}
:   Namespaces are created in resource groups so that access to resources within a namespace can be configured at the resource group level. If a namespace isn't already in a resource group, you can assign the namespace to a resource group.

    - Namespaces created in version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, are created in a resource group that you specify so that you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. However, you can still set permissions for the namespace at the account level or in the namespace itself. For more information, see [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add) and [`ibmcloud cr namespace-add`](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_add).

    - Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the {{site.data.keyword.cloud_notm}} console before 29 July 2020 aren't assigned to resource groups. You can assign an existing namespace to a resource group so that you can configure access to resources within a namespace at the resource group level. For more information, see [Assigning existing namespaces to resource groups](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_assign) and [`ibmcloud cr namespace-assign`](/docs/Registry?topic=Registry-containerregcli#ic_cr_namespace_assign).

    - You can find out which namespaces are assigned to resource groups and which are unassigned by running the [`ibmcloud cr namespace-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list) command with the `-v` option.

## 13 July 2020
{: #registry-13jul2020}
{: release-note}

To work with namespaces, you must have the Manager role at the account level {: #13jul2020_manager}
:   If you want to add or remove namespaces, you must have the Manager role, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## 24 June 2020
{: #registry-24jun2020}
{: release-note}

Restoring all tags for a digest in a repository is now an option {: #24jun2020_tags}
:   When you want to restore an image, you can restore either by tag or by digest. Restoring by digest restores the digest and all its tags in the repository that aren't already in the live repository. You can restore an image by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command.

    For more information, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

## 18 May 2020
{: #registry-18may2020}
{: release-note}

Retaining untagged images is now an option when you clean up your namespaces {: #18may2020_untagged}
:   Retention policies now include untagged images by default when they calculate what to retain. You can use the `retain-untagged` option for the [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set) and [`ibmcloud cr retention-run`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run) commands to keep all untagged images and delete only tagged images. You can view the value of `retain-untagged` for each retention policy by running the [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list) command.

    For more information, see [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).

## 30 April 2020
{: #registry-30apr2020}
{: release-note}

`ibmcloud cr image-prune-untagged` command is available {: #30apr2020_prune}
:   The `ibmcloud cr image-prune-untagged` command deletes all [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images in your {{site.data.keyword.registryshort}} account.

    For more information, see [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged) and [Clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged).

## 16 April 2020
{: #registry-16apr2020}
{: release-note}

You can use private network connections to securely route your data in {{site.data.keyword.registryshort}} {: #16apr2020_private_network}
:   If you use cloud-based services for production workloads, you can use a secure private connection so that you can ensure that you adhere to any compliance regulations. You can use {{site.data.keyword.cloud_notm}} service endpoints to connect to {{site.data.keyword.cloud_notm}} services over the private {{site.data.keyword.cloud_notm}} network.

    For more information, see [Securing your connection to {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_private) and [{{site.data.keyword.registrylong_notm}} architecture and workload](/docs/Registry?topic=Registry-registry_architecture).

`ibmcloud cr private-only` command is available {: #16apr2020_private}
:   You can use the `ibmcloud cr private-only` command to prevent image pulls or pushes over public network connections for your account.

    For more information, see [`ibmcloud cr private-only`](/docs/Registry?topic=Registry-containerregcli#ic_cr_private_only).

## 3 February 2020
{: #registry-3feb2020}
{: release-note}

Using {{site.data.keyword.registryshort}} tokens is deprecated {: #3feb2020_tokens}
:   The use of UAA and {{site.data.keyword.registryshort}} tokens is deprecated. From 12 August 2020, UAA tokens are not accepted for authentication.

    For more information, see [Announcing End of {{site.data.keyword.registrylong_notm}} Support for UAA Tokens](https://www.ibm.com/blog/announcement/announcing-end-of-ibm-cloud-container-registry-support-for-uaa-tokens/){: external}.

## 31 January 2020
{: #registry-31jan2020}
{: release-note}

`ibmcloud cr image-digests` command is available {: #31jan2020_digests}
:   The `ibmcloud cr image-digests` command displays all images in your account, including untagged images.

    For more information, see [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests).

## 4 December 2019
{: #registry-4dec2019}
{: release-note}

Support for {{site.data.keyword.redhat_notm}} signatures is available {: #4dec2019_signatures}
:   {{site.data.keyword.registryshort}} now supports {{site.data.keyword.redhat_notm}} signatures.

    For more information, see [Signing images for trusted content by using {{site.data.keyword.redhat_full}} signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig).

## 25 October 2019
{: #registry-25oct2019}
{: release-note}

{{site.data.keyword.la_full_notm}} platform services logs are available {: #25oct2019_logs}
:   {{site.data.keyword.registryshort}} generates platform services logs that are displayed in your logging instances.

    For more information, see [{{site.data.keyword.la_full_notm}} platform services logs](/docs/Registry?topic=Registry-registry_logs).

## 14 October 2019
{: #registry-14oct2019}
{: release-note}

`ibmcloud cr manifest-inspect` command is available {: #14oct2019_manifest}
:   The `ibmcloud cr manifest-inspect` command displays the contents of the manifest for an image.

    For more information, see [`ibmcloud cr manifest-inspect`](/docs/Registry?topic=Registry-containerregcli#bx_cr_manifest_inspect).

## 23 September 2019
{: #registry-23sep2019}
{: release-note}

You can create retention policies for your images {: #23sep2019_retention_policy}
:   Image retention policies retain the specified number of images for each repository within a namespace in {{site.data.keyword.registryshort}}. All other images in the namespace are deleted.

    The following commands are available for you to use to create retention policies so that you can manage your images:

    - The [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set) command sets up a policy for retaining images for each repository within a namespace.
    - The [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list) command lists the image retention policies for your account.

    For more information, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

You can restore deleted images from the trash {: #23sep2019_restore_trash}
:   All deleted images are stored in the trash for 30 days.

    The following commands are available for you to use to restore images:

    - The [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command displays all images in the trash in your {{site.data.keyword.cloud_notm}} account. Images remain in the trash for 30 days after deletion.
    - The [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command restores a deleted image from the trash.

    For more information, see [Listing images in the trash](/docs/Registry?topic=Registry-registry_images_#registry_images_list_trash) and [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

## 1 August 2019
{: #registry-01aug2019}
{: release-note}

`ibmcloud cr retention-run` command is available {: #01aug2019_retention}
:   The `ibmcloud cr retention-run` command cleans up your namespaces by retaining images for each repository within a namespace in {{site.data.keyword.registryshort}} by applying specified criteria. All other images in the namespace are deleted.

    For more information, see [`ibmcloud cr retention-run`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run) and [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## 25 July 2019
{: #registry-25jul2019}
{: release-note}

{{site.data.keyword.at_full_notm}} available for {{site.data.keyword.registryshort}} {: #25jul2019_at}
:   Use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with the {{site.data.keyword.registryshort}} service in {{site.data.keyword.cloud_notm}}.

    For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

## 1 July 2019
{: #registry-1jul2019}
{: release-note}

`ibmcloud cr token-add` command is no longer available {: #1jul2019_token_add}
:   The `ibmcloud cr token-add` command is discontinued. You can't add registry tokens in either the CLI or the API anymore.

## 27 June 2019
{: #registry-27jun2019}
{: release-note}

Container Scanner is no longer available {: #27jun2019_cs}
:   The Container Scanner is discontinued. Vulnerability Advisor still scans images that are pushed to {{site.data.keyword.registryshort}}.

## 13 June 2019
{: #registry-13jun2019}
{: release-note}

Remove tags from images {: #13jun2019_tags}
:   Remove a tag, or tags, from each specified image in {{site.data.keyword.registryshort}}. To remove a specific tag from an image and leave the underlying image and any other tags in place, use the [`ibmcloud cr image-untag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_untag) command. If you want to delete the underlying image, and all its tags, use the [`ibmcloud cr image-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm) command instead.

    For more information, see [Removing tags from images in your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_untag).

## 13 May 2019
{: #registry-13may2019}
{: release-note}

End of support for Container Scanner {: #13may2019_cs}
:   Container Scanner is now deprecated and is no longer usable.

## 2 April 2019
{: #registry-2apr2019}
{: release-note}

General Availability of Container Image Security Enforcement {: #2apr2019_cise}
:   Use Container Image Security Enforcement to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/Registry?topic=Registry-registry_trustedcontent) is properly applied to the image.

## 14 March 2019
{: #registry-14mar2019}
{: release-note}

{{site.data.keyword.cloudaccesstrailfull_notm}} available for {{site.data.keyword.registryshort}} {: #14mar2019_at}
:   Use the {{site.data.keyword.cloudaccesstraillong_notm}} service to track how users and applications interact with the {{site.data.keyword.registryshort}} service in {{site.data.keyword.cloud_notm}}.

    For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

## 25 February 2019
{: #registry-25feb2019}
{: release-note}

New domain names {: #25feb2019_dns}
:   {{site.data.keyword.registryshort}} is adopting new domain names. The new domain names are available in the {{site.data.keyword.cloud_notm}} console and the CLI. You can use the new `icr.io` domain names now. The existing `registry.bluemix.net` domain names are deprecated, but you can continue to use them until the end of support date. An end of support date is not available yet.

    For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions) and [Introducing New {{site.data.keyword.registrylong_notm}} Domain Names](https://www.ibm.com/blog/announcement/introducing-new-ibm-cloud-container-registry-domain-names/){: external}.

    Signatures apply to the whole image name, which includes the domain name. If you're using content trust, you must add new signatures so that you can use content trust under the new domain name.

    For more information about signing images, see [Signing images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent).

Adding IAM API key policies to control access to resources {: #25feb2019_secrets}
:   The new cluster image pull secrets for the `icr.io` domains are authorized by using an {{site.data.keyword.iamshort}} (IAM) API key. Therefore, if you want more control over access to your {{site.data.keyword.registryshort}} resources, you can add IAM access policies. For example, you can change the API key policies in the cluster's pull secret so that images are pulled from a certain registry region or namespace only.

    For more information, see [Understanding how to authorize your cluster to pull images from a registry](/docs/containers?topic=containers-registry#cluster_registry_auth).

New region in ap-north {: #25feb2019_ap-north}
:   A new region is available in `ap-north`. You can use the new region by using the domain name `jp.icr.io`.

    For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## 21 February 2019
{: #registry-21feb2019}
{: release-note}

Automating access to your namespaces {: #21feb2019_access}
:   Using tokens to automate pushing and pulling Docker images to and from your namespaces is deprecated. You must now use API keys to automate access to your {{site.data.keyword.registryshort}} namespaces so that you can push and pull images.

    For more information, see [Creating a user API key manually](/docs/Registry?topic=Registry-registry_access#registry_access_user_apikey_create).

## 8 January 2019
{: #registry-8jan2019}
{: release-note}

End of support for Vulnerability Advisor API version 2 {: #8jan2019_va2}
:   Vulnerability Advisor’s API version 2 is deprecated and is no longer usable. Use version 3 of the API, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}}](/apidocs/vulnerability-advisor).

## 4 October 2018
{: #registry-4oct2018}
{: release-note}

Managing user access {: #4oct2018_access}
:   Use {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) to control access by users in your account to {{site.data.keyword.registryshort}}. When IAM access policies are enabled for your account in {{site.data.keyword.registryshort}}, every user that accesses the service in your account must be assigned an IAM [access policy](x2853407){: term} with an IAM user role defined. That policy determines the role that the user has within the context of the service, and what actions the user can perform.

    For more information, see [Managing IAM access with {{site.data.keyword.iamshort}}](/docs/Registry?topic=Registry-iam#iam), [Defining IAM access policies](/docs/Registry?topic=Registry-user#user), and [Granting access to {{site.data.keyword.registryshort}} resources tutorial](/docs/Registry?topic=Registry-iam_access#iam_access).

## 7 August 2018
{: #registry-7aug2018}
{: release-note}

Exemption policies available in Vulnerability Advisor {: #7aug2018_exemption}
:   If you want to manage the security of an {{site.data.keyword.cloud_notm}} organization, you can use your policy setting to determine whether an issue is exempt or not. You can use Portieris to ensure that deployment is allowed only from images that contain no security issues after accounting for any issues that are exempted by your policy.

    For more information, see [Setting organizational exemption policies](/docs/Registry?topic=Registry-va_index&interface=ui#va_managing_policy).

## 25 July 2018
{: #registry-25jul2018}
{: release-note}

{{site.data.keyword.cloudaccesstrailfull_notm}} available for Vulnerability Advisor {: #25jul2018_at}
:   Use the {{site.data.keyword.cloudaccesstrailfull_notm}} service to track how users and applications interact with the {{site.data.keyword.registryshort}} service in {{site.data.keyword.cloud_notm}}.

    For more information, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

## 12 July 2018
{: #registry-12jul2018}
{: release-note}

Vulnerability Advisor API version 3 {: #12jul2018_va3}
:   Version 3 of the API changes the behavior of the API endpoints that are used to list exemptions. You must check that your use of the API does not rely on the behavior of version 2.

    For more information, see [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}}](/apidocs/vulnerability-advisor).

## 31 May 2018
{: #registry-31may2018}
{: release-note}

Use Helm for Passport Advantage images {: #31may2018_helm}
:   Import {{site.data.keyword.IBM_notm}} software that is downloaded from [IBM Passport Advantage Online for customers](https://www.ibm.com/software/passportadvantage/pao_customer.html){: external} and packaged for use with Helm into your {{site.data.keyword.registryshort}} namespace.

## 21 March 2018
{: #registry-21mar2018}
{: release-note}

Container Scanner {: #21mar2018_cs}
:   Container Scanner enables Vulnerability Advisor to report any problems that are found in running containers that are not present in the container's base image.

## 16 March 2018
{: #registry-16mar2018}
{: release-note}

Container Image Security Enforcement beta {: #16mar2018_cise}
:   Use Container Image Security Enforcement beta to verify your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}. You can control where images are deployed from, enforce Vulnerability Advisor policies, and ensure that [content trust](/docs/Registry?topic=Registry-registry_trustedcontent) is properly applied to the image.

## 20 February 2018
{: #registry-20feb2018}
{: release-note}

Trusted content {: #20feb2018_tc}
:   {{site.data.keyword.registryshort}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools.

    For more information, see [Signing images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent).

## 6 November 2017
{: #registry-6nov2017}
{: release-note}

Global registry {: #6nov2017_global}
:   A global registry is available. The global registry domain name doesn't include a region (`icr.io`). Only public images that are provided by {{site.data.keyword.IBM_notm}} are hosted in this registry.

    For more information, see [Global registry](/docs/Registry?topic=Registry-registry_overview#registry_regions_global).

## 29 September 2017
{: #registry-29sep2017}
{: release-note}

Build Docker images {: #29sep2017_docker}
:   The `ibmcloud cr build` command is now available for running container builds. You can build a Docker image directly in {{site.data.keyword.cloud_notm}} or create your own Docker image on your local computer and upload (push) it to your namespace in {{site.data.keyword.registryshort}}.

    For more information, see [Building Docker images to use them with your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_creating).

## 24 August 2017
{: #registry-24aug2017}
{: release-note}

Graphical user interface released {: #24aug2017_gui}
:   The {{site.data.keyword.registrylong_notm}} graphical user interface is available in the catalog, see [{{site.data.keyword.registryshort_notm}}](https://cloud.ibm.com/registry/catalog).

## 27 June 2017
{: #registry-27jun2017}
{: release-note}

Introducing {{site.data.keyword.registrylong_notm}} {: #27jun2017_ga}
:   {{site.data.keyword.registrylong_notm}} is available as a service in {{site.data.keyword.cloud_notm}}. [{{site.data.keyword.registryshort}}](https://www.ibm.com/products/container-registry){: external} provides a multi-tenant private image registry that you can use to store and share your container images with users in your {{site.data.keyword.cloud_notm}} account.

    For more information about how to use {{site.data.keyword.registryshort}}, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started).
