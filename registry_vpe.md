---

copyright:
  years: 2021, 2022
lastupdated: "2022-02-11"

keywords: Virtual private endpoint, VPE

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.registrylong_notm}}
{: #registry_vpe}

You can use {{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC to connect to {{site.data.keyword.registryshort_notm}} from your VPC network by using the IP addresses of your choice, which is allocated from a subnetwork within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all [availability zones](x7018171){: term} of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

If you have an [{{site.data.keyword.vpc_full}} (VPC) instance](/docs/vpc?topic=vpc-getting-started) and want to connect the VPC instance to {{site.data.keyword.registrylong_notm}} for your {{site.data.keyword.registryshort_notm}} services, you can create a virtual private endpoint (VPE) for your VPC to access {{site.data.keyword.registrylong_notm}} within your VPC network.

To connect to {{site.data.keyword.registrylong_notm}} by using a virtual private endpoint, you must use the {{site.data.keyword.registryshort_notm}} API or CLI. The {{site.data.keyword.registryshort_notm}} page of the {{site.data.keyword.cloud_notm}} console must be accessed from a browser in your VPC.
{: note}

You must ensure that the canonical [domain name](/docs/Registry?topic=Registry-registry_overview#overview_elements_domain_name) for the registry [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) (for example, `us.icr.io` in `us-south`) resolves to the IP address of the VPE gateway. This action ensures that the image name, which starts with the hostname, is consistent. You can ensure consistency by creating container hostmap entries or configuring the `kube` Domain Name System (DNS).

For more information about other {{site.data.keyword.cloud_notm}} VPE services, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).

## Before you begin
{: #registry_vpe_prereqs}

Before you target a virtual private endpoint for {{site.data.keyword.registryshort_notm}}, you must complete the following tasks.

- Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
- Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
- Ensure that [correct access controls](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways) are set for your virtual private endpoint.
- Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe) of having a virtual private endpoint.
- Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

## Virtual private service endpoints
{: #registry_vpe_endpoints}

The table lists {{site.data.keyword.registrylong_notm}} private endpoints that are supported from the following VPC regions:

- Dallas (`us-south`)
- Frankfurt (`eu-de`)
- London (`eu-gb`)
- Osaka (`jp-osa`)
- Sao Paulo (`br-sao`)
- Sydney (`au-syd`)
- Tokyo (`jp-tok`)
- Toronto (`ca-tor`)
- Washington (`us-east`)

You can create a VPE gateway for your local {{site.data.keyword.registryshort_notm}} service only. This restriction is a known limitation, if you want to connect to {{site.data.keyword.registrylong_notm}} in another region, you must enable classic access, see [Creating a classic access VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure#create-a-classic-access-vpc) and use hostnames, such as `private.uk.icr.io`.
{: important}

## Setting up a VPE for {{site.data.keyword.registrylong_notm}}
{: #registry_vpe_endpoint_setup}

When you create a VPE gateway by using the [CLI](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-cli) or [API](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-api), you must specify the [cloud resource name (CRN)](x9494304){: term} of the region that you want to connect to {{site.data.keyword.registryshort_notm}}. Review the following table for the available regions and CRNs to use to create your VPE gateway.

You can create VPE gateways in the following locations: `ap-north`, `ap-south`, `br-sao`, `ca-tor`, `eu-central`, `jp-osa`, `uk-south`, `us-south`, and `us-east` (global registry).

| Registry region | Cloud resource name (CRN) |
|-----------------|-----------------|
| `ap-north` | `crn:v1:bluemix:public:container-registry:jp-tok:::endpoint:vpe.jp-tok.container-registry.cloud.ibm.com` |
| `ap-south` | `crn:v1:bluemix:public:container-registry:au-syd:::endpoint:vpe.au-syd.container-registry.cloud.ibm.com` |
| `br-sao` | `crn:v1:bluemix:public:container-registry:br-sao:::endpoint:vpe.br-sao.container-registry.cloud.ibm.com` |
| `ca-tor` | `crn:v1:bluemix:public:container-registry:ca-tor:::endpoint:vpe.ca-tor.container-registry.cloud.ibm.com` |
| `eu-central` | `crn:v1:bluemix:public:container-registry:eu-de:::endpoint:vpe.eu-de.container-registry.cloud.ibm.com` |
| `jp-osa` | `crn:v1:bluemix:public:container-registry:jp-osa:::endpoint:vpe.jp-osa.container-registry.cloud.ibm.com` |
| `uk-south` | `crn:v1:bluemix:public:container-registry:eu-gb:::endpoint:vpe.eu-gb.container-registry.cloud.ibm.com` |
| `us-south` | `crn:v1:bluemix:public:container-registry:us-south:::endpoint:vpe.us-south.container-registry.cloud.ibm.com` |
| Global `us-east` | `crn:v1:bluemix:public:container-registry:us-east:::endpoint:vpe.us-east.container-registry.cloud.ibm.com` |
{: caption="Table 1. Region availability and cloud resource names for connecting {{site.data.keyword.registryshort_notm}} over {{site.data.keyword.cloud_notm}} private networks" caption-side="bottom"}

If you want to connect to {{site.data.keyword.registrylong_notm}} in another region, you must use hostnames, such as `private.uk.icr.io`. For more information about {{site.data.keyword.registryshort_notm}} private networks, see [Securing your connection to Container Registry](/docs/Registry?topic=Registry-registry_private).

### Configuring an endpoint gateway
{: #registry_endpoint-gateway-servicename}

To configure a virtual private endpoint gateway, follow these steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users. For more information, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).
2. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.registrylong_notm}} that you want to be privately available to the VPC. To create the VPE gateway by using the CLI, run the following command, where `<CRN>` is the CRN of the target region as shown in Table 1.

    ```txt
    ibmcloud is endpoint-gateway-create --target <CRN> --vpc-id <VPC-ID> --name myname
    ```
    {: pre}

3. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
4. View the created VPE gateways associated with the {{site.data.keyword.registrylong_notm}}. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.registrylong_notm}} instance privately through it.


