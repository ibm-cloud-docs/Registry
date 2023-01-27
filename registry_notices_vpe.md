---

copyright:
  years: 2022
lastupdated: "2023-01-27"

keywords: IBM Cloud Container Registry notifications, notifications, registry, changes, vpe

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Changes to {{site.data.keyword.registryshort_notm}} VPE gateways from 11 November 2022
{: #registry_notices_vpe}

If you're using an {{site.data.keyword.registrylong}} virtual private endpoint (VPE) gateway that was created before 11 November 2022, you must re-create your VPE gateway before 15 December 2022. If you use {{site.data.keyword.iamshort}} restricted IP address lists and {{site.data.keyword.registryshort}} VPE gateways, you must also update your restricted IP address lists.
{: shortdesc}

## What you need to know about this change
{: #registry_notices_vpe_know}

On 11 November 2022, virtual private endpoints (VPEs) for {{site.data.keyword.registrylong_notm}} are being updated and the existing VPE version is being deprecated on 15 December 2022. If you use {{site.data.keyword.registryshort}} VPE gateways, you must create new VPE gateways and remove your VPE gateways that were created before 11 November 2022 at the earliest opportunity so that you pick up these changes. VPE gateways that were created before 11 November 2022 are deprecated and will not work after 15 December 2022.

If you create a new {{site.data.keyword.registryshort}} VPE gateway after 11 November 2022 and also use {{site.data.keyword.iamshort}} (IAM) [restricted IP address lists](/docs/account?topic=account-ips&interface=ui), you must ensure that your restricted IP address list contains the Cloud Service Endpoint (CSE) source IP addresses of the VPCs in which your {{site.data.keyword.registryshort}} VPE gateways exist. This requirement is related to a previous change to how {{site.data.keyword.registryshort}} works over the private network that the new VPE version also uses, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network).

## How you benefit from this change
{: #registry_notices_vpe_benefit}

{{site.data.keyword.registryshort}} VPEs are being updated so that they can access all {{site.data.keyword.registryshort}} service regions by using a single VPE gateway. Previously, a {{site.data.keyword.registryshort}} VPE gateway provided access to {{site.data.keyword.registryshort}} only in the region in which the VPC and VPE gateway existed. If a user wanted to access another {{site.data.keyword.registryshort}} region, they had to use the private registry domain names (for example, `private.us.icr.io`) and required extra VPC configuration for these domains.

With the new VPE version, VPC users can privately access all {{site.data.keyword.registryshort}} regions by using a single {{site.data.keyword.registryshort}} VPE gateway that uses a public domain name (for example, `us.icr.io`) regardless of the region in which the VPE gateway exists and without having to provide extra configuration.

Additionally, the new version of the VPE is in line with previous changes to private networking within {{site.data.keyword.registryshort}} where the real source IP addresses of requests to the {{site.data.keyword.registryshort}} are now maintained.

Previously, when connections came in over private networks, including through VPE gateways, the source IP addresses that you saw in {{site.data.keyword.at_full_notm}} and that were configured for IAM restricted IP address lists, were documented {{site.data.keyword.registryshort}} IP addresses, see [Permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-firewall#firewall_private_container_registry).

When you connect to {{site.data.keyword.registryshort}} now, the real IP address of your VPC [Cloud service endpoint source addresses](/docs/vpc?topic=vpc-vpc-behind-the-curtain#cse-source-addresses) is maintained in a request, which means that IAM restricted IP lists can be configured to specifically allow requests from your VPC, which improves security.

## Understanding if you are impacted by this change
{: #registry_notices_vpe_impact}

You are affected by this change if you are using a {{site.data.keyword.registryshort}} VPE gateway that was created before 11 November 2022. VPE gateways created before this date can be identified by differences in their target CRN. You can find the target CRN of a VPE gateway by viewing the VPE gateway details in the {{site.data.keyword.cloud_notm}} console (GUI) or CLI, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway&interface=ui).

VPE gateways that were created before 11 November 2022 are in the format:

`crn:v1:bluemix:public:container-registry:<cloud-region>:::endpoint:vpe.<cloud-region>.container-registry.cloud.ibm.com`

VPE gateways that are created after 11 November 2022 are in the format:

`crn:v1:bluemix:public:container-registry:<cloud-region>:::endpoint:<registry-region-domain>`

For a list of updated {{site.data.keyword.registryshort}} VPE CRNs, see [Setting up a VPE for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_vpe&interface=ui#registry_vpe_endpoint_setup).

If you are using a {{site.data.keyword.registryshort}} VPE gateway that was created before 11 November 2022 and also maintain IAM restricted IP address lists, you must change your restricted IP address list to contain your VPC Cloud Service Endpoint source addresses.

## What actions you need to take
{: #registry_notices_vpe_actions}

If you use a {{site.data.keyword.registryshort}} VPE gateway that was created before 11 November 2022
:   You must re-create your {{site.data.keyword.registryshort}} VPE gateway before 15 December 2022. If you don't re-create your VPE gateway, the VPE gateway will not connect to {{site.data.keyword.registryshort}} after that date.

    To replace the VPE gateway, complete the following steps:

    1. Create a new VPE gateway for {{site.data.keyword.registryshort}} in the required VPC, see [Creating an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=ui). If you’re using the CLI, you might want to refer to the {{site.data.keyword.registryshort}} VPE CRNs. For more information, see [Setting up a VPE for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_vpe&interface=ui#registry_vpe_endpoint_setup).

    2. Remove the VPE gateway that was created before 11 November 2022, see [Deleting an endpoint gateway](/docs/vpc?topic=vpc-vpe-deleting-ui-cli-api&interface=ui).

If you use a {{site.data.keyword.registryshort}} VPE gateway that was created before 11 November 2022 and you use IAM restricted IP address lists
:   You must re-create your {{site.data.keyword.registryshort}} VPE gateway and update your IAM restricted IP address lists before 15 December 2022. If you don't re-create your VPE gateway and update your IP address lists, the VPE gateway will not connect to {{site.data.keyword.registryshort}} after that date.

    To replace the VPE gateway and update your IAM restricted IP address lists, complete the following steps:

    1. Update your IAM restricted IP address lists to access the [Cloud service endpoint source addresses](/docs/vpc?topic=vpc-vpc-behind-the-curtain#cse-source-addresses) of your VPC. You can find the CSEs by viewing the details of your VPC in either the {{site.data.keyword.cloud_notm}} console or CLI.

    2. Create a new VPE gateway for {{site.data.keyword.registryshort}} in the required VPC, see [Creating an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=ui). If you’re using the CLI, you might want to refer to the {{site.data.keyword.registryshort}} VPE CRNs. For more information, see [Setting up a VPE for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_vpe&interface=ui#registry_vpe_endpoint_setup).

    3. Remove the VPE gateway that was created before 11 November 2022, see [Deleting an endpoint gateway](/docs/vpc?topic=vpc-vpe-deleting-ui-cli-api&interface=ui).
