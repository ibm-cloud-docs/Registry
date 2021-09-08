---

copyright:
  years: 2021
lastupdated: "2021-09-03"

keywords: Responsibilities

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


# Understanding your responsibilities when you are using {{site.data.keyword.registryshort_notm}}
{: #registry_responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.registrylong}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.registrylong_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

## Incident and operations management
{: #incident-and-ops}

Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, recovery, and full state backup and recovery.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|------|-------------------------------------------------|-----------------------|
| Data incidents. | It is the responsibility of {{site.data.keyword.IBM_notm}} to inform you if your data is lost. |  |
| Ensure that the application is available. | It is the responsibility of {{site.data.keyword.IBM_notm}} to inform you if the application is not available. | |
| Track events. | It is the responsibility of {{site.data.keyword.IBM_notm}} to ensure that {{site.data.keyword.cloudaccesstraillong_notm}} is tracking events. | It is your responsibility to monitor events by using {{site.data.keyword.cloudaccesstraillong_notm}} to ensure that your application is being accessed only by users with the right authority. It is also your responsibility to ensure that an {{site.data.keyword.cloudaccesstrailshort}} instance is set up to receive events. For more information, see [Auditing the events for Container Registry](/docs/Registry?topic=Registry-at_events). |
{: row-headers}
{: caption="Table 1. Responsibilities for incident and operations" caption-side="top"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or {{site.data.keyword.IBM_notm}} might be responsible for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Change management
{: #change-management}

Change management includes tasks such as deployment, configuration, upgrades, patching, configuration changes, and deletion.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|------|-------------------------------------------------|-----------------------|
| Provisioning. | It is the responsibility of {{site.data.keyword.IBM_notm}} to provision the service. | |
| Deprovisioning. | It is the responsibility of {{site.data.keyword.IBM_notm}} to deprovision the service. | |
| Update package versions. | | It is your responsibility to update package versions inside container images. You can use Vulnerability Advisor to identify the required updates. For more information, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index). |
{: row-headers}
{: caption="Table 2. Responsibilities for change management" caption-side="top"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or {{site.data.keyword.IBM_notm}} might be responsible for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Identity and access management
{: #iam-responsibilities}

Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|------|-------------------------------------------------|-----------------------|
| Authentication | It is the responsibility of {{site.data.keyword.IBM_notm}} to implement authentication. | |
| Process access policies | It is the responsibility of {{site.data.keyword.IBM_notm}} to ensure that the policies are processed. | |
| Set up access policies | | It is your responsibility to set up access policies. For more information, see [Creating policies](/docs/Registry?topic=Registry-user#create). |
| Access to back-end resources | It is the responsibility of {{site.data.keyword.IBM_notm}} to access to back-end resources. | |
| Access to namespaces | | It is your responsibility to set up access to namespaces. For more information, see [Automating access to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_access).|
{: row-headers}
{: caption="Table 3. Responsibilities for identity and access management" caption-side="top"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or {{site.data.keyword.IBM_notm}} might be responsible for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Security and regulation compliance
{: #security-compliance}

Security and regulation compliance includes tasks such as security controls implementation and compliance certification.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|------|-------------------------------------------------|-----------------------|
| Secure confidential information. | | It is your responsibility to make sure that no confidential information is put into your images. |
| Ensure that the service instance is secure. | It is the responsibility of {{site.data.keyword.IBM_notm}} to ensure the security of the service instance. | |
{: row-headers}
{: caption="Table 4. Responsibilities for security and regulation compliance" caption-side="top"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or {{site.data.keyword.IBM_notm}} might be responsible for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Disaster recovery
{: #disaster-recovery}

Disaster recovery includes tasks such as providing dependencies on disaster recovery sites, provision disaster recovery environments, data and configuration backup, replicating data and configuration to the disaster recovery environment, and failover on disaster events. For more information, see [Understanding high availability and disaster recovery for Container Registry](/docs/Registry?topic=Registry-ha-dr).

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|------|-------------------------------------------------|-----------------------|
| Copy your data to another region. | | It is your responsibility to copy the data to another region. For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).|
| Restore the contents of the data in a single region. | It is the responsibility of {{site.data.keyword.IBM_notm}} to restore the contents of the data in a single region. | |
{: row-headers}
{: caption="Table 5. Responsibilities for disaster recovery" caption-side="top"}
{: summary="The rows are read from left to right. The first column describes the task that a the customer or {{site.data.keyword.IBM_notm}} might be responsible for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

