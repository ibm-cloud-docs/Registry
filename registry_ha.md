---

copyright:
  years: 2018, 2021
lastupdated: "2021-09-09"

keywords: load balancing, back ups, HA for IBM Cloud Container Registry, DR for IBM Cloud Container Registry, high availability for IBM Cloud Container Registry, disaster recovery for IBM Cloud Container Registry, failover for IBM Cloud Container Registry

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
{:release-note: data-hd-content-type='release-note'}
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


# Understanding high availability and disaster recovery for {{site.data.keyword.registryshort_notm}}
{: #ha-dr}

The {{site.data.keyword.registrylong}} service is a highly available, regional, service.
{: shortdesc}

- In each supported region, traffic is load balanced across registry infrastructure in multiple availability zones, with no single point of failure.
- Data that is stored in {{site.data.keyword.registrylong_notm}} is replicated and it is also backed up regularly.
- If you're worried about the availability of your images if an entire region is unavailable, you can choose to push your images to multiple registries.

    You might also choose to push your images to multiple registries in case you accidentally delete or overwrite your images.

    For more information about regions, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

For more information about service availability, see [Service Level Agreements](/docs/overview?topic=overview-slas).

## Frequently asked questions about high availability and disaster recovery
{: #ha-dr_faq}

Review the following FAQs about high availability and disaster recovery.
{: shortdesc}

### Does the service replicate the data?
{: #ha-dr_replicate_data}

All customer data in {{site.data.keyword.registrylong_notm}} is replicated and backed up. Backups include service and policy settings and image data, but not vulnerability results, which can be reconstructed. All data, including vulnerability results, is replicated within each region so that the loss of a single availability zone is tolerated transparently. Regular point-in-time backups are used by {{site.data.keyword.IBM_notm}} to restore the content if the data is corrupted. Extra backups are created in other regions with compatible privacy policies that are used by {{site.data.keyword.IBM_notm}} to restore the service in a disaster situation.

The following table shows the backup locations.

| Environment | Active location | Backup location |
|-------------|-----------------|-----------------|
| `ap-north` | `jp-tok` | `au-syd` |
| `ap-south` | `au-syd` | `jp-tok` |
| `br-sao` | `br-sao` | `us-south` |
| `ca-tor` | `ca-tor` | `us-east` (service and policy settings)  \n  \n `ca-mon` (images) |
| `eu-de` | `eu-de` | `eu-gb` |
| `eu-gb` | `eu-gb` | `eu-de` |
| `global` | `us-east` | `us-south` |
| `jp-osa` | `jp-osa` | `jp-tok` |
| `us-south` | `us-south` | `us-east` |
{: caption="Table 1. Backup locations" caption-side="top"}

### Are users required to replicate the data?
{: #ha-dr_client}

You're not expected to replicate your images. However, you can create a service instance in another {{site.data.keyword.registrylong_notm}} region. You can also choose from a range of tools, including pushing to multiple locations from your development pipeline, and the use of replication tools, such as [`skopeo copy`](https://github.com/containers/skopeo/blob/main/docs/skopeo-copy.1.md){: external}. {{site.data.keyword.IBM_notm}} doesn't replicate service instances.

### What data is backed-up or replicated?
{: #ha-dr_backup}

The image data and service and policy settings are backed up by {{site.data.keyword.IBM_notm}}.

### Does {{site.data.keyword.cloud_notm}} replicate the service?
{: #ha-dr_service}

{{site.data.keyword.IBM_notm}} doesn't make replicas of your data available in any region other than the region where you stored it. High availability is achieved by running the service in three data centers in each region.

### Are users required to replicate the service?
{: #ha-dr_service_replicate}

You're not required to replicate your data into another region, but you can do it yourself by using tools such as [`skopeo copy`](https://github.com/containers/skopeo/blob/main/docs/skopeo-copy.1.md){: external}.


