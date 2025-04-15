---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, Exemption Synchronization, replicate exemptions, exemptions, regions

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.registryshort}} is ending exemption synchronization across regions on 31 January 2022
{: #registry_notices_exemptions}

Beginning 31 January 31 2022, Vulnerability Advisor for {{site.data.keyword.registrylong}} will no longer replicate exemptions between {{site.data.keyword.cloud_notm}} regions.
{: shortdesc}

The original announcement was published on 20 December 2021.
{: note}

## What are exemptions?
{: #registry_notices_exemptions_desc}

Exemptions are policies that exclude any matching vulnerabilities or configuration issues from [Vulnerability Advisor](https://cloud.ibm.com/apidocs/vulnerability-advisor){: external} reports. Exemptions are typically used when the issues are checked and found to be irrelevant to the account. The exemption status is displayed in the vulnerability report for any images that are within the policy’s scope.

For more information, see [Setting organizational exemption policies](/docs/Registry?topic=Registry-va_index&interface=ui#va_managing_policy).

## What is the current behavior?
{: #registry_notices_exemptions_behavior}

In some [{{site.data.keyword.registrylong_notm}}](https://www.ibm.com/products/container-registry){: external} regions, exemptions are replicated for consistency. You can manage exemptions in one of these regions, and the settings for that region apply to all the regions that allow replication of exemptions. In all other regions, exemptions must be managed separately in each region and apply only in the region where the exemption is set.

## Which regions currently replicate exemptions?
{: #registry_notices_exemptions_replicate}

Exemptions are currently replicated in the following {{site.data.keyword.cloud_notm}} regions:

- `au-syd` (formerly known as `ap-south`)
- `eu-de` (formerly known as `eu-central`)
- `eu-gb` (formerly known as `uk-south`)
- `jp-tok` (formerly known as `ap-north`)
- `us-south`
- `Global`

All other regions require separate exemption management.

## Do I have any exemptions?
{: #registry_notices_exemptions_own}

To find out whether you have any exemptions in a particular region, set the region by running [`ibmcloud cr region-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set) and then run the [`ibmcloud cr exemption-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_list) command.

## How does this change affect me?
{: #registry_notices_exemptions_affect}

Beginning 31 January 2022, all regions will require separate exemption management. Any existing exemptions created before this date in the replicated regions are still present after this date. However, any changes from this date must be performed in each region where you want the change to take effect.

## Original announcement
{: #registry_notices_exemptions_announce}

The original announcement was published on 20 December 2021.
