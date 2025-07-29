---

copyright:
  years: 2021, 2025
lastupdated: "2025-07-29"

keywords: Virtual private endpoint, VPE, vpc, private, service, endpoint gateway, gateway, endpoint

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using VPEs for VPC to privately connect to {{site.data.keyword.registryshort_notm}}
{: #registry_vpe}

You can use {{site.data.keyword.cloud}} virtual private endpoints (VPE) for Virtual Private Cloud (VPC) to connect to {{site.data.keyword.registrylong}} from your VPC network by using the IP addresses of your choice, which are allocated from a subnetwork within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all [availability zones](#x7018171){: term} of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud_notm}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addresses within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

If you have an {{site.data.keyword.vpc_short}} instance and you want to connect the VPC instance to {{site.data.keyword.registrylong_notm}} for your {{site.data.keyword.registryshort_notm}} services, you can create a VPE gateway for your VPC to access {{site.data.keyword.registrylong_notm}} within your VPC network. Any connections to {{site.data.keyword.registrylong_notm}} that originate from within the VPC automatically go through the {{site.data.keyword.registryshort_notm}} VPE gateway, if one exists. For more information, see [Getting started with Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started).

When you connect to {{site.data.keyword.registryshort_notm}} from the {{site.data.keyword.cloud_notm}} console, you must go through a browser in your VPC to ensure that the connection goes through the {{site.data.keyword.registryshort_notm}} VPE gateway.
{: important}

For more information about other {{site.data.keyword.cloud_notm}} VPE services, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).

## Before you begin
{: #registry_vpe_prereqs}

Before you target a VPE for {{site.data.keyword.registryshort_notm}}, you must complete the following tasks.

- Ensure that a Virtual Private Cloud is created, see [Getting started with Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started).
- Make a plan for your virtual private endpoints, see [Planning for virtual private endpoint gateways](/docs/vpc?topic=vpc-planning-considerations).
- Ensure that correct access controls are set for your VPE, see [Configuring ACLs and security groups for use with endpoint gateways](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways).
- Understand the limitations of having a VPE, see [Virtual private endpoint limitations](/docs/vpc?topic=vpc-limitations-vpe).
- Understand how to view details about a VPE, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

## Virtual private endpoints
{: #registry_vpe_endpoints}

The table lists {{site.data.keyword.registrylong_notm}} private endpoints that are supported from the following VPC regions:

- Dallas (`us-south`)
- Frankfurt (`eu-de`)
- London (`eu-gb`)
- Madrid (`eu-es`)
- Montreal (`ca-mon`)
- Osaka (`jp-osa`)
- Sao Paulo (`br-sao`)
- Sydney (`au-syd`)
- Tokyo (`jp-tok`)
- Toronto (`ca-tor`)
- Washington (`us-east`)

You can create a VPE gateway for your local {{site.data.keyword.registryshort_notm}} service only. You can pull images from any other {{site.data.keyword.registryshort_notm}} region by using the public domains, such as `uk.icr.io`. For more information about mapping the region name to the domain, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).
{: important}

## Setting up a VPE for {{site.data.keyword.registrylong_notm}}
{: #registry_vpe_endpoint_setup}

When you create a VPE gateway by using the CLI or API, you must specify the [cloud resource name (CRN)](#x9494304){: term} of the region that you want to connect to {{site.data.keyword.registryshort_notm}}. Review the following table for the available regions and CRNs to use to create your VPE gateway.

You can create VPE gateways in these locations:  `au-syd`, `br-sao`, `ca-mon`, `ca-tor`, `eu-de`, `eu-es`, `eu-gb`, `jp-osa`, `jp-tok`, `us-south`, and `us-east` (global registry).

| Registry region | Region that was formerly known as | Cloud resource name (CRN) |
|-----------------|----------------------------------|---------------------------|
| `au-syd` | `ap-south` | `crn:v1:bluemix:public:container-registry:au-syd:::endpoint:au.icr.io` |
| `br-sao` | Not applicable | `crn:v1:bluemix:public:container-registry:br-sao:::endpoint:br.icr.io` |
| `ca-mon` | Not applicable | `crn:v1:bluemix:public:container-registry:ca-mon:::endpoint:ca2.icr.io` |
| `ca-tor` | Not applicable | `crn:v1:bluemix:public:container-registry:ca-tor:::endpoint:ca.icr.io` |
| `eu-de` | `eu-central` | `crn:v1:bluemix:public:container-registry:eu-de:::endpoint:de.icr.io` |
| `eu-es` | Not applicable | `crn:v1:bluemix:public:container-registry:eu-es:::endpoint:es.icr.io` |
| `eu-gb` | `uk-south` | `crn:v1:bluemix:public:container-registry:eu-gb:::endpoint:uk.icr.io` |
| `jp-osa` | Not applicable | `crn:v1:bluemix:public:container-registry:jp-osa:::endpoint:jp2.icr.io` |
| `jp-tok` | `ap-north` | `crn:v1:bluemix:public:container-registry:jp-tok:::endpoint:jp.icr.io` |
| `us-south` | Not applicable | `crn:v1:bluemix:public:container-registry:us-south:::endpoint:us.icr.io` |
| Global `us-east` | Not applicable | `crn:v1:bluemix:public:container-registry:us-east:::endpoint:icr.io` |
{: caption="Region availability and cloud resource names (CRNs) for connecting {{site.data.keyword.registryshort_notm}} over private {{site.data.keyword.cloud_notm}} networks" caption-side="bottom"}
{: #table_registry_vpe}

You can pull images from any other {{site.data.keyword.registryshort_notm}} region by using the public domains, such as `uk.icr.io`. For more information about mapping the region name to the domain, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

### Configuring an endpoint gateway
{: #registry_endpoint-gateway-servicename}

To configure a VPE gateway, complete the following steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users. For more information, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).
2. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.registrylong_notm}} that you want to be privately available to the VPC. To create the VPE gateway by using the CLI, run the following command, where `CRN` is the CRN of the target region as shown in the [Region availability and cloud resource names (CRNs) for connecting {{site.data.keyword.registryshort_notm}} over private {{site.data.keyword.cloud_notm}} networks](#table_registry_vpe) table, `VPC_ID` is the ID of the VPC, and `MY_NAME` is the name of the new endpoint gateway.

    ```txt
    ibmcloud is endpoint-gateway-create --target CRN --vpc-id VPC_ID --name MY_NAME
    ```
    {: pre}

3. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
4. View the created VPE gateways associated with the {{site.data.keyword.registrylong_notm}}. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.registrylong_notm}} instance privately through it.
