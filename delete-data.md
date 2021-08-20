---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-20"

keywords: PHI, data, data encryption in IBM Cloud Container Registry, data storage for IBM Cloud Container Registry, personal data in IBM Cloud Container Registry, data deletion for IBM Cloud Container Registry, data in IBM Cloud Container Registry, data security in IBM Cloud Container Registry

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


# Managing your data in {{site.data.keyword.registrylong_notm}}
{: #delete-data}

Information about your data and how it is stored.
{: shortdesc}

The {{site.data.keyword.cloud}} platform provides layered security controls across network and infrastructure. {{site.data.keyword.cloud_notm}} provides a group of security services that can be used by application developers to secure their mobile and web apps. For more information, see [How do I know that my data is safe?](/docs/overview?topic=overview-security)

## How your data is stored
{: #data-storage}

### Image data
{: #data-storage_image}

Image data is stored in {{site.data.keyword.cos_full_notm}}, which is encrypted at rest, and encrypted in transit between {{site.data.keyword.registrylong_notm}} and {{site.data.keyword.cos_full_notm}}. For more information about {{site.data.keyword.cos_full_notm}}, see [About IBM Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage).

Data that is stored in {{site.data.keyword.registrylong_notm}} is backed up regularly. For more information, see [High availability and disaster recovery](/docs/Registry?topic=Registry-ha-dr).

### Scanning data
{: #data-storage_va}

To scan images and containers in your account for security issues, {{site.data.keyword.registrylong_notm}} collects, stores, and processes the following information:

- Free-form fields, including IDs, descriptions, and image names (registry, namespace, repository name, and image tag)
- Metadata about the file modes and creation timestamps of the configuration files
- The content of system and application configuration files in images and containers
- Installed packages and libraries (including their versions)

Scan results, aggregated at a data center level, are processed to produce anonymized metrics to operate and improve the service. Scan results are deleted 30 days after they are generated. For more information, see [Data protection](/docs/Registry?topic=va-va_index#about_data_protection).

Do not put personal information into any field or location that {{site.data.keyword.registrylong_notm}} processes, as identified in the preceding list.
{: important}

## Deleting your data
{: #data-delete}

You can delete your {{site.data.keyword.registrylong_notm}} namespaces, images, and private repositories.

### Deleting the service
{: #data-delete_service}

When an {{site.data.keyword.cloud_notm}} account is canceled or removed, the resource instances that track the account's usage of {{site.data.keyword.registrylong_notm}} are deleted. As part of that action all namespaces, and the images that they contain, are removed in accordance with the data retention policy.

The {{site.data.keyword.registrylong_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.registrylong_notm}} service description, which you can find in the Service Description for {{site.data.keyword.cloud_notm}} in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).

### Deleting namespaces
{: #data-delete_namespaces}

If you no longer require a registry namespace, you can remove the namespace from your {{site.data.keyword.cloud_notm}} account. Deleting a namespace removes all images, trash, and trust information that is contained in the namespace. For more information, see [Removing namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_remove).

### Deleting images
{: #data-delete_images}

You can delete unwanted images from your private repository by using either the {{site.data.keyword.cloud_notm}} console or the CLI. For more information, see [Deleting images from your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).

You can clean up your namespace by choosing to retain only the most recent images in each repository in that namespace in {{site.data.keyword.registrylong_notm}}. You can detect and delete old images from all the repositories in a namespace by running a one-off command, `ibmcloud cr retention-run`, or by setting a scheduled policy by running the `ibmcloud cr retention-policy-set` command. For more information, see [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).

### Deleting private repositories
{: #data-delete_private_repo}

You can delete private repositories that are no longer required, and any associated images, by using the {{site.data.keyword.cloud_notm}} console. For more information, see [Deleting a private repository and any associated images](/docs/Registry?topic=Registry-registry_images_#registry_repo_remove).

## Restoring deleted data
{: #data-restore}

You can restore images from the trash by digest or by tag.

You can restore an image from the trash by running the `ibmcloud cr image-restore` command. To find out which images are in the trash, run the `ibmcloud cr trash-list` command. Images are stored in the trash for 30 days. For more information, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).


