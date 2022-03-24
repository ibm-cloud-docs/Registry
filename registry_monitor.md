---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-24"

keywords: IBM Cloud, observability, registry, monitoring, metrics, pull traffic, storage usage, storage quota, monitor, locations, attributes

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring metrics for {{site.data.keyword.registrylong_notm}}
{: #registry_monitor}

You can use {{site.data.keyword.mon_full}} to monitor platform metrics of {{site.data.keyword.registrylong}} usage for your account and to create alerts based on these metrics.
{: shortdesc}

Platform metrics for {{site.data.keyword.registryshort}} must be enabled in each {{site.data.keyword.registryshort}} region that you want to monitor, see [Enabling metrics for {{site.data.keyword.registryshort}}](#registry_enable_platform_metrics).

## Enabling metrics for {{site.data.keyword.registryshort_notm}}
{: #registry_enable_platform_metrics}

You must enable {{site.data.keyword.registryshort_notm}} metrics in each region that you want to see metrics.
{: note}

You can create a {{site.data.keyword.mon_short}} instance in the region that you want to monitor and enable platform metrics for it. Alternatively, you can enable platform metrics on an existing {{site.data.keyword.mon_short}} instance in that region.

Complete the following steps to create and configure platform metrics for {{site.data.keyword.registryshort_notm}}.

1. Create and configure an {{site.data.keyword.mon_full_notm}} instance that is configured with platform metrics in the region that you want to monitor, see [Getting started with {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

   For more information about the locations where {{site.data.keyword.registryshort_notm}} is enabled for monitoring, see [Locations](#registry_monitor_locations).

2. Log in to {{site.data.keyword.cloud_notm}}.

    ```txt
    ibmcloud login
    ```
    {: pre}

3. Target the [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) where you want to enable metrics by running the [`ibmcloud cr region-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) command. Replace `<region>` with the name of the [region](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

    ```txt
    ibmcloud cr region-set <region>
    ```
    {: pre}

4. Check whether metrics are already enabled for your account by running the following [`ibmcloud cr platform-metrics`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics) command. This command also displays the registry that the result applies to.

    ```txt
    ibmcloud cr platform-metrics --status
    ```
    {: pre}

5. Enable platform metrics by running the following `ibmcloud cr platform-metrics` command. It can take up to 30 minutes for your metrics to become effective.

    ```txt
    ibmcloud cr platform-metrics --enable
    ```
    {: pre}

    If you want to target a different [region](/docs/Registry?topic=Registry-registry_overview#registry_regions), run the [`ibmcloud cr region-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) command.

## Locations
{: #registry_monitor_locations}

You can configure one monitoring instance in each region to collect platform metrics for {{site.data.keyword.registrylong_notm}}. The following tables list the locations where metrics can be collected if you enable collection of {{site.data.keyword.registryshort_notm}} service metrics in that region.

{{site.data.keyword.registrylong_notm}} global registry metrics are available through the monitoring `Washington (us-east)` instance.
{: note}

| Locations in Americas | Platform metrics available |
|-----------------------|---------------------------------|
| `Dallas (us-south)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `Sao Paulo (br-sao)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `Toronto (ca-tor)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `Washington (us-east)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
{: caption="Table 1. The automatic collection of {{site.data.keyword.registryshort_notm}} service metrics in Americas locations" caption-side="bottom"}

| Locations in Asia Pacific | Platform metrics available |
|---------------------------|---------------------------------|
| `Osaka (jp-osa)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `Sydney (au-syd)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `Tokyo (jp-tok)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
{: caption="Table 2. The automatic collection of {{site.data.keyword.registryshort_notm}} service metrics in Asia Pacific locations" caption-side="bottom"}

| Locations in Europe | Platform metrics available |
|---------------------|---------------------------------|
| `Frankfurt (eu-de)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `London (eu-gb)` | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
{: caption="Table 3. The automatic collection of {{site.data.keyword.registryshort_notm}} service metrics in Europe locations" caption-side="bottom"}

For more information about the locations where {{site.data.keyword.cloud_notm}} services are enabled to send metrics to {{site.data.keyword.mon_full_notm}}, see [{{site.data.keyword.cloud_notm}} services by location](/docs/monitoring?topic=monitoring-cloud_services_locations).

## Viewing metrics
{: #registry_view_metrics}

To monitor {{site.data.keyword.registryshort_notm}} metrics, you must start the {{site.data.keyword.mon_short}} UI instance that is enabled for platform metrics in the region where you are using {{site.data.keyword.registryshort_notm}}.
{: important}

### Starting the Monitoring UI from the Observability page
{: #registry_view_metrics_opt2}

To start the Monitoring UI from the Observability page, complete the following steps:

1. [Start the Monitoring UI](/docs/monitoring?topic=monitoring-launch).
2. Select **DASHBOARDS**.
3. In the **Default Dashboards** section, expand **IBM**.
4. Choose the {{site.data.keyword.registryshort_notm}} dashboard from the list. Available dashboards are **Container Registry Usage** and **Container Registry Quota Usage**. For more information about predefined dashboards, see [Predefined dashboards](#registry_dashboards_dictionary).

Next, change the scope or make a copy of the Default dashboard so that you can monitor your account in {{site.data.keyword.registryshort_notm}}. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards).

## Predefined dashboards
{: #registry_dashboards_dictionary}

The following table outlines the predefined monitoring dashboards that you can use to monitor {{site.data.keyword.registryshort_notm}} metrics.

| Dashboard name        | Description    | Default dashboard |
|-----------------------|----------------|-------------------|
| {{site.data.keyword.registryshort_notm}} Usage | A dashboard that you can use to visualize the traffic usage and storage usage. Traffic usage is the sum of bytes from image pulls from your {{site.data.keyword.registryshort_notm}} namespaces in the current billing period. Storage usage is the sum of bytes of images in your {{site.data.keyword.registryshort_notm}} namespaces. | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| {{site.data.keyword.registryshort_notm}} Quota Usage | A dashboard that you can use to visualize the traffic usage and storage usage and compare the data to your quotas, if set. Visible only to those accounts that have finite quotas. The **Container Registry Quota Usage** dashboard is available only if you enable metrics and you have both a storage and a traffic quota set. | |
{: caption="Table 4. Predefined dashboards" caption-side="bottom"}

The predefined dashboards can't be changed. You can copy any predefined dashboard so that you can change it to suit your requirements. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards).
{: important}

When you start your dashboard, some metrics might display a `Data Load Error` warning icon. This warning is because more time is required to create the data. When data is available, the warning sign goes away and the metric is populated. You might also need to change the resolution period.
{: note}

## Metrics
{: #metrics}

| Metric Name | Information |
|-------------|-------------|
| [`Pull Traffic`](#ibm_containerregistry_pull_traffic) | The account's pull traffic in the current month. |
| [`Pull Traffic Quota`](#ibm_containerregistry_pull_traffic_quota) | The account's pull traffic quota. |
| [`Storage Quota`](#ibm_containerregistry_storage_quota) | The account's storage quota. |
| [`Storage`](#ibm_containerregistry_storage) | The account's storage usage. |
{: caption="Table 5. Metrics available by plan names" caption-side="bottom"}

### `Pull Traffic`
{: #ibm_containerregistry_pull_traffic}

The account's pull traffic in the current month.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 6. Pull Traffic metric metadata" caption-side="bottom"}

### `Pull Traffic Quota`
{: #ibm_containerregistry_pull_traffic_quota}

The account's pull traffic quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 7. Pull Traffic Quota metric metadata" caption-side="bottom"}

### `Storage Quota`
{: #ibm_containerregistry_storage_quota}

The account's storage quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 8. Storage Quota metric metadata" caption-side="bottom"}

### `Storage Used`
{: #ibm_containerregistry_storage}

The account's storage usage.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 9. Storage metric metadata" caption-side="bottom"}


