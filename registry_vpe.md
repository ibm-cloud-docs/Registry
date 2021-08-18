---

copyright:
  years: 2021
lastupdated: "2021-08-18"

keywords: Virtual private endpoint, VPE

subcollection: Registry

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.registrylong_notm}}
{: #registry_vpe}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC enables you to connect to {{site.data.keyword.registryshort_notm}} from your VPC network by using the IP addresses of your choosing, allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

If you have an [{{site.data.keyword.vpc_full}} (VPC) instance](/docs/vpc?topic=vpc-getting-started) and want to connect the VPC instance to {{site.data.keyword.registrylong_notm}} for your {{site.data.keyword.registryshort_notm}} services, you can create a virtual private endpoint (VPE) for your VPC to access {{site.data.keyword.registrylong_notm}} within your VPC network.

To connect to {{site.data.keyword.registrylong_notm}} by using a virtual private endpoint, you must use the {{site.data.keyword.registryshort_notm}} API or CLI. The {{site.data.keyword.registryshort_notm}} page of the {{site.data.keyword.cloud_notm}} console must be accessed from a browser in your VPC.
{: note}

You must ensure that the canonical domain name for the registry [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) (for example, `us.icr.io` in `us-south`) resolves to the IP address of the VPE gateway. This action ensures that the image name, which starts with the hostname, is consistent. You can ensure consistency by creating container hostmap entries or configuring the `kube` Domain Name System (DNS).

For more information about other {{site.data.keyword.cloud_notm}} VPE services, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).

## Before you begin
{: #registry_vpe_prereqs}

Before you target a virtual private endpoint for {{site.data.keyword.registryshort_notm}}, you must complete the following tasks.

- Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
- Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
- Ensure that [correct access controls](/docs/vpc?topic=vpc-vpe-configuring-acls) are set for your virtual private endpoint.
- Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe) of having a virtual private endpoint.
- Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

## Virtual private service endpoints
{: #registry_vpe_endpoints}

The table lists {{site.data.keyword.registrylong_notm}} private endpoints that are supported from the following VPC regions:

- Dallas (`us-south`)
- Frankfurt (`eu-de`)
- London (`eu-gb`)
- Osaka (`jp-osa`)
- Sydney (`au-syd`)
- Tokyo (`jp-tok`)
- Toronto (`ca-tor`)
- Washington (`us-east`)

You can create a VPE gateway for your local {{site.data.keyword.registryshort_notm}} service only. This restriction is a known limitation, if you want to connect to {{site.data.keyword.registrylong_notm}} in another region, you must enable classic access, see [Creating a classic access VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure#create-a-classic-access-vpc) and use hostnames, such as `private.uk.icr.io`.
{: important}

## Setting up a VPE for {{site.data.keyword.registrylong_notm}}
{: #registry_vpe_endpoint_setup}

When you create a VPE gateway by using the [CLI](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-cli) or [API](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-api), you must specify the Cloud Resource Name (CRN) of the region that you want to connect to {{site.data.keyword.registryshort_notm}}. Review the following table for the available regions and CRNs to use to create your VPE gateway.

You can create VPE gateways in the following locations: `ap-north`, `ap-south`, `ca-tor`, `eu-central`, `jp-osa`, `uk-south`, `us-south`, and `us-east` (global registry).

| Registry region | Cloud Resource Name (CRN) |
|-----------------|-----------------|
| `ap-north` | `crn:v1:bluemix:public:container-registry:jp-tok:::endpoint:vpe.jp-tok.container-registry.cloud.ibm.com` |
| `ap-south` | `crn:v1:bluemix:public:container-registry:au-syd:::endpoint:vpe.au-syd.container-registry.cloud.ibm.com` |
| `ca-tor` | `crn:v1:bluemix:public:container-registry:ca-tor:::endpoint:vpe.ca-tor.container-registry.cloud.ibm.com` |
| `eu-central` | `crn:v1:bluemix:public:container-registry:eu-de:::endpoint:vpe.eu-de.container-registry.cloud.ibm.com` |
| `jp-osa` | `crn:v1:bluemix:public:container-registry:jp-osa:::endpoint:vpe.jp-osa.container-registry.cloud.ibm.com` |
| `uk-south` | `crn:v1:bluemix:public:container-registry:eu-gb:::endpoint:vpe.eu-gb.container-registry.cloud.ibm.com` |
| `us-south` | `crn:v1:bluemix:public:container-registry:us-south:::endpoint:vpe.us-south.container-registry.cloud.ibm.com` |
| Global `us-east` | `crn:v1:bluemix:public:container-registry:us-east:::endpoint:vpe.us-east.container-registry.cloud.ibm.com` |
{: caption="Table 1. Region availability and Cloud Resource Names for connecting {{site.data.keyword.registryshort_notm}} over {{site.data.keyword.cloud_notm}} private networks." caption-side="top"}

If you want to connect to {{site.data.keyword.registrylong_notm}} in another region, you must use hostnames, such as `private.uk.icr.io`. For more information about {{site.data.keyword.registryshort_notm}} private networks, see [Securing your connection to Container Registry](/docs/Registry?topic=Registry-registry_private).

### Configuring an endpoint gateway
{: #registry_endpoint-gateway-servicename}

To configure a virtual private endpoint gateway, follow these steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users. For more information, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).
2. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.registrylong_notm}} that you want to be privately available to the VPC. To create the VPE gateway by using the CLI, run the following command, where `<CRN>` is the CRN of the target region as shown in Table 1.

    ```
    ibmcloud is endpoint-gateway-create --target <CRN> --vpc-id <VPC-ID> --name myname
    ```
    {: pre}

3. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
4. View the created VPE gateways associated with the {{site.data.keyword.registrylong_notm}}. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.registrylong_notm}} instance privately through it.


