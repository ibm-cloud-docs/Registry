---

copyright:
  years: 2021
lastupdated: "2021-05-10"

keywords: Virtual private endpoint, VPE

subcollection: Registry

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:term: .term}
{:external: target="_blank" .external}

# Using a virtual private endpoint for {{site.data.keyword.vpc_short}}
{: #registry_vpe}

If you have an [{{site.data.keyword.vpc_full}} (VPC) instance](/docs/vpc?topic=vpc-getting-started) and want to connect the VPC instance to {{site.data.keyword.registrylong_notm}} for your {{site.data.keyword.registryshort_notm}} services, you can create a virtual private endpoint (VPE) for your VPC to access {{site.data.keyword.registrylong_notm}} within your VPC network.
{: shortdesc}

You can configure the VPE to use the IP addresses of your choice, which are allocated from a subnet within your VPC. Virtual private endpoints are bound to a [VPE gateway](/docs/vpc?topic=vpc-about-vpe) and serve as an intermediary that enables your workload in VPC to connect to the private endpoints in {{site.data.keyword.registrylong_notm}}.

To connect to {{site.data.keyword.registrylong_notm}} by using a virtual private endpoint, you must use the {{site.data.keyword.registryshort_notm}} API or CLI. The {{site.data.keyword.registryshort_notm}} page of the {{site.data.keyword.cloud_notm}} console must be accessed through the public network from your VPC.
{: note}

You must ensure that the canonical domain name for the registry [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) (for example, `us.icr.io` in `us-south`) resolves to the IP address of the VPE gateway. This action ensures that the image name, which starts with the hostname, is consistent. You can ensure consistency by creating container host-map entries or configuring the `kube` Domain Name System (DNS).

For more information about other {{site.data.keyword.cloud_notm}} VPE services, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).

## Before you begin
{: #egistry_vpe_prereqs}

Before you target a virtual private endpoint for {{site.data.keyword.registryshort_notm}}, you must complete the following tasks.

- Ensure that a [Virtual Private Cloud is provisioned](/docs/vpc?topic=vpc-getting-started){: external}.
- Ensure that [virtual private endpoints are planned](/docs/vpc?topic=vpc-planning-considerations){: external}.
- Ensure that [correct access controls](/docs/vpc?topic=vpc-vpe-configuring-acls){:external} are set for your virtual private endpoint.
- Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe){: external} of having a virtual private endpoint.
- Ensure that a VPE gateway is [created](/docs/vpc?topic=vpc-ordering-endpoint-gateway){: external} and understand how to
  [access](/docs/vpc?topic=vpc-accessing-vpe-after-setup){: external} a VPE gateway.
- Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway){: external} about
  a virtual private endpoint.

## Virtual private service endpoints
{: #egistry_vpe_endpoints}

The table lists {{site.data.keyword.registrylong_notm}} private endpoints that are supported from the following VPC regions:

- Dallas (`us-south`)
- Frankfurt (`eu-de`)
- London (`eu-gb`)
- Osaka (`jp-osa`)
- Sydney (`au-syd`)
- Tokyo (`jp-tok`)
- Washington (`us-east`)

You can create a VPE gateway for your local {{site.data.keyword.registryshort_notm}} service only. You can create VPE gateways in the following locations: `us-south`, `us-east` (global registry), `uk-south`, `eu-central`, `ap-south`, `ap-north`, and `jp-osa`.
{: important}

When you create a VPE gateway by using the [CLI](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-cli) or [API](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-api), you must specify the Cloud Resource Name (CRN) of the region that you want to connect to {{site.data.keyword.registryshort_notm}}. If you use the {{site.data.keyword.registryshort_notm}} page of the {{site.data.keyword.cloud_notm}} console to create the VPE gateway, choose the relevant service name and region and the gateway is created for you.

To create the VPE gateway by using the CLI, run the following command, where `<CRN>` is the CRN of the target region as shown in the following table.

```
ibmcloud is endpoint-gateway-create --target <CRN> --vpc-id <VPC-ID> --name myname
```
{: pre}

| Registry region | Cloud Resource Name (CRN) |
|-----------------|-----------------|
| `ap-north` | `crn:v1:bluemix:public:container-registry:jp-tok:::endpoint:vpe.jp-tok.container-registry.cloud.ibm.com` |
| `ap-south` | `crn:v1:bluemix:public:container-registry:au-syd:::endpoint:vpe.au-syd.container-registry.cloud.ibm.com` |
| `eu-central` | `crn:v1:bluemix:public:container-registry:eu-de:::endpoint:vpe.eu-de.container-registry.cloud.ibm.com` |
| `jp-osa` | `crn:v1:bluemix:public:container-registry:jp-osa:::endpoint:vpe.jp-osa.container-registry.cloud.ibm.com` |
| `uk-south` | `crn:v1:bluemix:public:container-registry:eu-gb:::endpoint:vpe.eu-gb.container-registry.cloud.ibm.com` |
| `us-south` | `crn:v1:bluemix:public:container-registry:us-south:::endpoint:vpe.us-south.container-registry.cloud.ibm.com` |
| Global `us-east` | `crn:v1:bluemix:public:container-registry:us-east:::endpoint:vpe.us-east.container-registry.cloud.ibm.com` |
{: caption="Table 1. Cloud Resource Names for connecting {{site.data.keyword.registryshort_notm}} over {{site.data.keyword.cloud_notm}} private networks." caption-side="top"}

If you want to connect to {{site.data.keyword.registrylong_notm}} in another region, you must use hostnames, such as `private.uk.icr.io`. For more information about {{site.data.keyword.registryshort_notm}} private networks, see [Securing your connection to Container Registry](/docs/Registry?topic=Registry-registry_private).
