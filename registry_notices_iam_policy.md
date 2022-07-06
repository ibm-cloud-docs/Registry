---

copyright:
  years: 2022
lastupdated: "2022-07-06"

keywords: IBM Cloud Container Registry notices, iam access policies, access policies, changes, prepare, iam, policy, region

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# IAM access policies are required from 5 July 2022
{: #registry_notices_iam_policy}

From 5 July 2022, to access {{site.data.keyword.registrylong}} you must be using {{site.data.keyword.iamshort}} (IAM) access policies.
{: shortdesc}

If you started to use {{site.data.keyword.registryshort}} before the availability of [IAM API key policies in {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#registry-25feb2019) in February 2019, you must ensure that you are using IAM access policies to manage access to the {{site.data.keyword.registrylong_notm}} service.
{: important}

Policy-free authorization is being discontinued in the following {{site.data.keyword.registryshort}} regions:

- `us-south (us.icr.io)`
- `uk-south (uk.icr.io)`
- `eu-central (de.icr.io)`
- `ap-south (au.icr.io)`
- `ap-north (jp.icr.io)`

Other regions are unaffected because they already require IAM access policies for all accounts.

## What are the changes?
{: #notices_iam_policy_change}

Before 7 June 2019, all account users had full access to the images and settings that are associated with the account. Accounts that use {{site.data.keyword.registryshort}} for the first time since 7 June 2019 are required to have IAM access policies and other accounts optionally require them. From 5 July 2022, all accounts require IAM access policies.

By default, account owners already have appropriate policies that give them full access to {{site.data.keyword.registryshort}}. If policy-free authorization is in use, any other account user IDs and service IDs must be granted appropriate policies so that they can continue to access images and settings.

## Check whether these changes affect you
{: #notices_iam_policy_affect}

To check whether policy-free authorization is in effect, run the [`ibmcloud cr iam-policies-status`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_status) command. If the CLI reports that `IAM policy enforcement is disabled`, you must [prepare for the changes](#notices_iam_policy_prepare).

The policy status setting is specific to each {{site.data.keyword.registryshort}} region. Check every region in which you have {{site.data.keyword.registryshort}} namespaces by running the [`ibmcloud cr region-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) command.

## Prepare for the changes
{: #notices_iam_policy_prepare}

If the changes affect you, you must create IAM [access policies](/docs/Registry?topic=Registry-user) that apply to each service ID and user ID that accesses images in your {{site.data.keyword.registryshort}} namespaces, or accesses {{site.data.keyword.registryshort}} settings that are associated with your account and region.

1. Identify each service ID and user ID that accesses your {{site.data.keyword.registryshort}} images and settings. You can use [{{site.data.keyword.at_full_notm}}](/docs/Registry?topic=Registry-at_events) to help find this information.
2. For each access that is identified in the previous step, [create an IAM access policy](/docs/Registry?topic=Registry-iam_access) that allows the correct access. You can also use access groups to apply policies to IDs.
3. (Optional) If you want to upgrade the account to use IAM access policy authorization at a more convenient time, rather than on the date of the change, run the [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) command.

    This change cannot be reversed.
    {: important}

    This change applies to the currently targeted region only. Remember to check all regions where you have {{site.data.keyword.registryshort}} namespaces.

## What if I did not make the changes in time?
{: #notices_iam_policy_unprepared}

To recover any access that is lost, follow the steps in [Prepare for the changes](#notices_iam_policy_prepare).


