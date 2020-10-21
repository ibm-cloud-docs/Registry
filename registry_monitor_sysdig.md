---

copyright:
  years: 2020
lastupdated: "2020-10-21"

keywords: IBM Cloud, observability, registry, monitoring, supertenant, Sysdig, metrics

subcollection: Registry

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}
{:term: .term}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Monitoring metrics for {{site.data.keyword.registrylong_notm}}
{: #registry_monitor_sysdig}

{{site.data.keyword.mon_full}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}

## Platform metrics overview
{: #registry_platform_metrics}

You can configure one instance only of the {{site.data.keyword.mon_full_notm}} service in each region to collect platform metrics.

* To use platform metrics, you must set up {{site.data.keyword.mon_full_notm}}, see [Getting started tutorial for {{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started).
* To configure the Sysdig instance, you must set the *platform metrics* configuration setting, see [Enabling Platform Metrics](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-platform_metrics_enabling).
* If a Sysdig instance in a region is already enabled to collect platform metrics, metrics from Sysdig-enabled services are collected automatically and available for monitoring through this instance. For more information about Sysdig-enabled services, see [Cloud services](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-cloud_services).
* For information about the locations where {{site.data.keyword.registryshort_notm}} is enabled for Sysdig, see [Container services](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-cloud_services_locations#cloud_services_locations_container).

To monitor platform metrics, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where {{site.data.keyword.registryshort_notm}} is provisioned.
{: important}

## Enabling platform metrics by using the {{site.data.keyword.registryshort_notm}} CLI
{: #registry_enable_platform_metrics}

Complete the following steps to configure platform metrics:

1. Log in to {{site.data.keyword.cloud_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

2. Log in to {{site.data.keyword.registryshort_notm}}:

   ```
   ibmcloud cr login
   ```
   {: pre}

2. To enable platform metrics, run the following command:

   ```
   ibmcloud cr platform-metrics --enable
   ```
   {: pre}

## Viewing metrics
{: #registry_view_metrics}

To monitor {{site.data.keyword.registryshort_notm}} metrics, you must launch the Sysdig web UI instance that is enabled for platform metrics in the region where you are using {{site.data.keyword.registryshort_notm}}.
{: important}

### Launching the Sysdig web UI from the Observability page
{: #registry_view_metrics_opt2}

To launch the Sysdig web UI from the *Observability* page, complete the following steps:

1. [Launch the Sysdig web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch).
2. Select **DASHBOARDS**.
3. In the **Default Dashboards** section, expand **IBM**.
4. Choose the {{site.data.keyword.registryshort_notm}} dashboard from the list.

Next, change the scope or make a copy of the *Default* dashboard so that you can monitor your account in {{site.data.keyword.registryshort_notm}}.

## Monitoring {{site.data.keyword.registryshort_notm}}
{: #registry_monitor_service}

Consider the following tasks when you monitor your account in the {{site.data.keyword.registryshort_notm}} service:

| Task                                      | Predefined alert | What to look for  |
|-------------------------------------------|------------------|-------------------|
| Monitor how the storage usage compares to the storage quota of your account. | {{site.data.keyword.registryshort_notm}} Storage Near Quota | When your storage quota is reached, you can't push image's namespaces that are owned by your account until you free up space by removing images, upgrade to the standard plan, or increase your custom quota limit. [Learn more](#registry_task1). |
| Monitor how the pull traffic usage compares to the pull traffic quota of your account. | {{site.data.keyword.registryshort_notm}} Traffic Near Quota | When your pull traffic quota is reached, you can't pull images from namespaces that are owned by your account for the remainder of the current billing period. Wait for the next billing period to start, upgrade to the standard plan, or increase your traffic quota. [Learn more](#registry_task2). |
{: caption="Table 1. Pre-defined alerts" caption-side="top"}

----
### Monitor the storage usage and quota
{: #registry_task1}

#### Description
{: #task1-pr}

{{site.data.keyword.registryshort_notm}} records the storage usage of your account, which increases and decreases as images are pushed to, or deleted from, a namespace that is owned by your account.
Your account has either a plan-specific or custom storage quota that determines the amount of storage that you can use to store your Docker images in the namespaces of your {{site.data.keyword.cloud_notm}} account. This alert notifies you when 80% of this quota is reached.
When this quota is reached, images can't be pushed to namespaces that are owned by the account until you either free up space or upgrade to the standard plan. If you set quota limits for storage in your free or standard plan, you can also increase this quota limit to enable you to push new images again. For more information, see [Service plans](/docs/Registry?topic=Registry-registry_overview#registry_plans).

#### User action
{: #registry_task1-action}

Monitor the storage usage by using the {{site.data.keyword.registryshort_notm}} dashboard and, if the quota is near to being reached, minimize storage usage. To help to minimize your storage usage, you can configure retention policies for each namespace to automatically delete images after a specific criteria is met. For more information, see [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).

If the alert is triggered regularly, consider upgrading to the standard plan or adjusting the storage quotas for your account. For more information, see [Managing quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_quota).

----
### Monitor the pull traffic usage and quota
{: #registry_task2}

#### Description
{: #registry_task2-pr}

{{site.data.keyword.registryshort_notm}} records pull traffic usage of your account, which increases when images that belong to namespaces in your account are pulled by using the public network. Your account has either a plan-specific or custom pull traffic quota that determines the amount of pull traffic that you can use in one billing period. When you reach or exceed the quota limits for your plan, you can't pull any images from the namespaces in your {{site.data.keyword.cloud_notm}} account until you either wait for the next billing period to start, upgrade to the standard plan, or increase your quota limits for pull traffic. For more information, see [Service plans](/docs/Registry?topic=Registry-registry_overview#registry_plans).

#### User action
{: #registry_task2-action}

Monitor the pull traffic of your account by using the {{site.data.keyword.registryshort_notm}} dashboard. If the alert triggers regularly, consider upgrading to the standard plan or adjusting the storage quotas for your account. For more information, see [Managing quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_quota).

You can also consider using {{site.data.keyword.registryshort_notm}} over a private network connection because pull traffic is not charged for image pulls that use private connections. For more information, see [Using private network connections for image pushes and pulls](/docs/Registry?topic=Registry-registry_private#registry_private_images).

----

## {{site.data.keyword.registryshort_notm}} Predefined Dashboards
{: #registry_dashboards_dictionary}

The following table outlines the pre-defined Sysdig dashboards that you can use to monitor {{site.data.keyword.registryshort_notm}} metrics:

| Dashboard name        | Description    |
|-----------------------|----------------|
| `{{site.data.keyword.registryshort_notm}}` | Dashboard visualizing important {{site.data.keyword.registryshort_notm}} metrics. |
{: caption="Table 2. Pre-defined dashboards" caption-side="top"}

The *Default* dashboard can't be changed. You can copy the dashboard so that you can make changes to suit your requirements.
{: important}

When you start your dashboard, some metrics might display a `Data Load Error` warning icon. This warning is because not enough time has elapsed to create the data. When data is available, the warning sign goes away and the metric is populated.
{: note}

## Predefined alerts
{: #registry_default_alerts}

The following table outlines the pre-defined alerts that are available in Sysdig.

| Alert Name                                 | Description |
|--------------------------------------------|-------------|
| {{site.data.keyword.registryshort_notm}} Storage Near Quota | This alert notifies you when the storage usage of your account reaches 80% of the storage quota. To manage your usage, consider using the actions described in [Monitoring {{site.data.keyword.registryshort_notm}}](#registry_monitor_service). |
| {{site.data.keyword.registryshort_notm}} Traffic Near Quota | This alert notifies you when the traffic usage of your account reaches 80% of the traffic quota. To prevent the quota being reached, consider using the actions described in [Monitoring {{site.data.keyword.registryshort_notm}}](#registry_monitor_service). |
{: caption="Table 3. Pre-defined alerts" caption-side="top"}

## Metrics available by Service Plan
{: #metrics-by-plan}

| Metric Name |
|-----------|
| [Pull Traffic](#ibm_containerregistry_pull_traffic) |
| [Pull Traffic Quota](#ibm_containerregistry_pull_traffic_quota) |
| [Storage Quota](#ibm_containerregistry_storage_quota) |
| [Storage Used](#ibm_containerregistry_storage) |
{: caption="Table 4: Metrics Available by Plan Names" caption-side="top"}

### Pull Traffic
{: #ibm_containerregistry_pull_traffic}

The account's pull traffic in the current month.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 5: Pull Traffic metric metadata" caption-side="top"}

### Pull Traffic Quota
{: #ibm_containerregistry_pull_traffic_quota}

The account's pull traffic quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 6: Pull Traffic Quota metric metadata" caption-side="top"}

### Storage Quota
{: #ibm_containerregistry_storage_quota}

The account's storage quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 7: Storage Quota metric metadata" caption-side="top"}

### Storage Used
{: #ibm_containerregistry_storage}

The account's storage usage.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 8: Storage Used metric metadata" caption-side="top"}

## Attributes for Segmentation
{: #attributes}

### Global Attributes
{: #global-attributes}

The following attributes are available for segmenting all of the metrics that are listed in [Metrics available by Service Plan](#metrics-by-plan).

| Attribute | Attribute Name | Attribute Description | Applicable to {{site.data.keyword.registryshort_notm}} metrics |
|-----------|----------------|-----------------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type has a value of `public`, `dedicated`, or `local`. | Yes |
| `Location` | `ibm_location` | The location of the monitored resource. This location can be a region, data center, or global. | Yes |
| `Resource` | `ibm_resource` | The resource that is being measured by the service, typically an identifying name or GUID. | No |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created. | No |
| `Resource Type` | `ibm_resource_type` | The type of resource that is being measured by the service. | No |
| `Service name` | `ibm_service_name` | The name of the service that is generating this metric. | Yes |
| `Scope` | `ibm_scope` | The scope is the account, organization, or space GUID that is associated with this metric. | Yes |
{: caption="Table 9. Attributes for segmenting metrics" caption-side="top"}

### Additional Attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes as described in [Metrics available by Service Plan](#metrics-by-plan). For segmentation options, see the individual metrics.

| Attribute | Attribute Name | Attribute Description | Applicable to {{site.data.keyword.registryshort_notm}} metrics |
|-----------|----------------|-----------------------|-----------------------|
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. | No |
| `Service instance name` | `ibm_service_instance_name` | The service instance name provides the user-provided name of the service instance. The name might not be a unique value depending on the name provided by the user. | No |
{: caption="Table 10. Attributes for segmenting attributes" caption-side="top"}
