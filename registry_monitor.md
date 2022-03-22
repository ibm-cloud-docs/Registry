---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-22"

keywords: IBM Cloud, observability, registry, monitoring, metrics, pull traffic, storage usage, storage quota, monitor, locations, attributes

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring metrics for {{site.data.keyword.registrylong_notm}}
{: #registry_monitor}

You can use {{site.data.keyword.mon_full}} to monitor the metrics for {{site.data.keyword.registrylong}}.
{: shortdesc}

{{site.data.keyword.mon_full}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, [DevOps](x5784896){: term} teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.

## Platform metrics overview
{: #registry_platform_metrics}

You can configure one instance only of the {{site.data.keyword.mon_full_notm}} service in each region to collect platform metrics.

- To use platform metrics, you must set up {{site.data.keyword.mon_full_notm}}, see [Getting started tutorial for {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).
- To configure the monitoring instance, you must set the platform metrics configuration setting, see [Enabling Platform Metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).
- If a monitoring instance in a region is already enabled to collect platform metrics, metrics are collected automatically and available for monitoring through this instance. For more information about monitoring-enabled services, see [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).
- For more information about the locations where {{site.data.keyword.registryshort_notm}} is enabled for monitoring, see [Container services](/docs/monitoring?topic=monitoring-cloud_services_locations#cloud_services_locations_container).

To monitor platform metrics, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where {{site.data.keyword.registryshort_notm}} is provisioned.
{: important}

## Enabling platform metrics by using the {{site.data.keyword.registryshort_notm}} CLI
{: #registry_enable_platform_metrics}

Complete the following steps to configure platform metrics:

1. Log in to {{site.data.keyword.cloud_notm}}.

    ```txt
    ibmcloud login
    ```
    {: pre}

2. To enable platform metrics, run the following command:

    ```txt
    ibmcloud cr platform-metrics --enable
    ```
    {: pre}

## Viewing metrics
{: #registry_view_metrics}

To monitor {{site.data.keyword.registryshort_notm}} metrics, you must start the Monitoring UI instance that is enabled for platform metrics in the region where you are using {{site.data.keyword.registryshort_notm}}.
{: important}

### Starting the Monitoring UI from the Observability page
{: #registry_view_metrics_opt2}

To start the Monitoring UI from the Observability page, complete the following steps:

1. [Start the Monitoring UI](/docs/monitoring?topic=monitoring-launch).
2. Select **DASHBOARDS**.
3. In the **Default Dashboards** section, expand **IBM**.
4. Choose the {{site.data.keyword.registryshort_notm}} dashboard from the list.

Next, change the scope or make a copy of the Default dashboard so that you can monitor your account in {{site.data.keyword.registryshort_notm}}.

## {{site.data.keyword.registryshort_notm}} predefined dashboards
{: #registry_dashboards_dictionary}

The following table outlines the predefined monitoring dashboards that you can use to monitor {{site.data.keyword.registryshort_notm}} metrics.

| Dashboard name        | Description    |
|-----------------------|----------------|
| {{site.data.keyword.registryshort_notm}} | Dashboard visualizing important {{site.data.keyword.registryshort_notm}} metrics. |
| {{site.data.keyword.registryshort_notm}} Quota Usage | Dashboard visualizing important {{site.data.keyword.registryshort_notm}} metrics compared to quotas, if set. Visible only to those accounts that have finite quotas. |
{: caption="Table 1. Predefined dashboards" caption-side="bottom"}

The Default dashboard can't be changed. You can copy the dashboard so that you can change it to suit your requirements.
{: important}

When you start your dashboard, some metrics might display a `Data Load Error` warning icon. This warning is because more time is required to create the data. When data is available, the warning sign goes away and the metric is populated.
{: note}

## Metrics available by service plan
{: #metrics-by-plan}

| Metric Name |
|-----------|
| [`Pull Traffic`](#ibm_containerregistry_pull_traffic) |
| [`Pull Traffic Quota`](#ibm_containerregistry_pull_traffic_quota) |
| [`Storage Quota`](#ibm_containerregistry_storage_quota) |
| [`Storage Used`](#ibm_containerregistry_storage) |
{: caption="Table 2. Metrics available by plan names" caption-side="bottom"}

### `Pull Traffic`
{: #ibm_containerregistry_pull_traffic}

The account's pull traffic in the current month.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 3. Pull Traffic metric metadata" caption-side="bottom"}

### `Pull Traffic Quota`
{: #ibm_containerregistry_pull_traffic_quota}

The account's pull traffic quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 4. Pull Traffic Quota metric metadata" caption-side="bottom"}

### `Storage Quota`
{: #ibm_containerregistry_storage_quota}

The account's storage quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 5. Storage Quota metric metadata" caption-side="bottom"}

### `Storage Used`
{: #ibm_containerregistry_storage}

The account's storage usage.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 6. Storage Used metric metadata" caption-side="bottom"}

## Attributes for segmentation
{: #attributes}

### Global Attributes
{: #global-attributes}

The following attributes are available for segmenting all the metrics that are listed in [Metrics available by service plan](#metrics-by-plan).

| Attribute | Attribute Name | Attribute Description | Applicable to {{site.data.keyword.registryshort_notm}} metrics |
|-----------|----------------|-----------------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type has a value of `public`. | Yes |
| `Location` | `ibm_location` | The location of the monitored resource. This location can be a region, data center, or global. | Yes |
| `Resource` | `ibm_resource` | The resource that is being measured by the service, which is typically an identifying name or [globally unique identifier (GUID)](x2390455){: term}. | No |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created. | No |
| `Resource Type` | `ibm_resource_type` | The type of resource that is being measured by the service. | No |
| `Service name` | `ibm_service_name` | The name of the service that is generating this metric. | Yes |
| `Scope` | `ibm_scope` | The scope is the account, organization, or space GUID that is associated with this metric. | Yes |
{: caption="Table 7. Attributes for segmenting metrics" caption-side="bottom"}

### Other Attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes as described in [Metrics available by service plan](#metrics-by-plan). For segmentation options, see the individual metrics.

| Attribute | Attribute Name | Attribute Description | Applicable to {{site.data.keyword.registryshort_notm}} metrics |
|-----------|----------------|-----------------------|-----------------------|
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. | No |
| `Service instance name` | `ibm_service_instance_name` | The service instance name provides the user-provided name of the service instance. The name might not be a unique value because the name depends on the name that is provided by the user. | No |
{: caption="Table 8. Attributes for segmenting attributes" caption-side="bottom"}


