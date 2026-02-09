---

copyright:
  years: 2019, 2026
lastupdated: "2026-02-09"

keywords: IBM Cloud Container Registry release notes, change, January, February, March, April, May, June, July, August, September, October, November, December, registry, images, vulnerability advisor, what's new, whats new, what is new

subcollection: Registry

content-type: release-note

---


{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.registryshort}}
{: #registry_release_notes}

What's new in {{site.data.keyword.registrylong}} and Vulnerability Advisor? The changes are grouped by date.
{: shortdesc}

## 9 February 2026
{: #registry-09feb2026}
{: release-note}

New region in India {: #09feb2026_chennai}
:   A new region in India, Chennai - Airtel, is available. The new region is `in-che` and the domain name is `in.icr.io`. You can target the new region in the {{site.data.keyword.cloud_notm}} console or in the command-line interface (CLI) by running `ibmcloud cr region-set in-che`. For more information, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

## 29 July 2025
{: #registry-29jul2025}
{: release-note}

New region in Canada {: #29jul2025_montreal}
:   A new region in Montreal, Canada is available. The new region is `ca-mon` and the domain name is `ca2.icr.io`. You can target the new region in the {{site.data.keyword.cloud_notm}} console or in the command-line interface (CLI) by running `ibmcloud cr region-set ca-mon`. For more information, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

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

    For more information about the {{site.data.keyword.registrylong_notm}} commands, see [{{site.data.keyword.registrylong_notm}} CLI](/docs/Registry?topic=Registry-containerregcli).

The `--json` option for {{site.data.keyword.registrylong_notm}} commands is deprecated {: #registry-24jul2023_json}
:   The `--json` option is replaced with the `--output json` option in the following commands:

    - `ibmcloud cr image-digests`
    - `ibmcloud cr image-prune-untagged`
    - `ibmcloud cr image-retention-run`
    - `ibmcloud cr trash-list`

    For more information about the {{site.data.keyword.registrylong_notm}} commands, see [{{site.data.keyword.registrylong_notm}} CLI](/docs/Registry?topic=Registry-containerregcli).

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

## 27 June 2017
{: #registry-27jun2017}
{: release-note}

Introducing {{site.data.keyword.registrylong_notm}} {: #27jun2017_ga}
:   {{site.data.keyword.registrylong_notm}} is available as a service in {{site.data.keyword.cloud_notm}}. [{{site.data.keyword.registryshort}}](https://www.ibm.com/products/container-registry){: external} provides a multi-tenant private image registry that you can use to store and share your container images with users in your {{site.data.keyword.cloud_notm}} account.

    For more information about how to use {{site.data.keyword.registryshort}}, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started).
