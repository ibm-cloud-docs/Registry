---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-30"

keywords: IBM Cloud, registry, monitoring, metrics, pull traffic, storage usage, storage quota, monitor, locations, dashboard, storage, region, platform metrics

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring metrics for {{site.data.keyword.registryshort_notm}}
{: #registry_monitor}

You can use {{site.data.keyword.mon_full}} to monitor platform metrics of {{site.data.keyword.registrylong}} usage for your account and to create alerts based on these metrics.
{: shortdesc}

Platform metrics for {{site.data.keyword.registryshort_notm}} must be enabled in each {{site.data.keyword.registryshort_notm}} region that you want to monitor, see [Enabling metrics for {{site.data.keyword.registryshort}}](#registry_enable_platform_metrics). For more information about {{site.data.keyword.monitoringlong_notm}}, see [{{site.data.keyword.monitoringshort}} in {{site.data.keyword.cloud_notm}}](/docs/monitoring?topic=monitoring-about-monitor).

## Enabling metrics for {{site.data.keyword.registryshort_notm}}
{: #registry_enable_platform_metrics}

You must enable {{site.data.keyword.registryshort_notm}} metrics in each region that you want to see metrics.
{: note}

You can create a {{site.data.keyword.mon_short}} instance in the region that you want to monitor and enable platform metrics for it. Alternatively, you can enable platform metrics on an existing {{site.data.keyword.mon_short}} instance in that region.

Complete the following steps to create and configure platform metrics for {{site.data.keyword.registryshort_notm}}.

1. Create and configure an {{site.data.keyword.mon_full_notm}} instance that is configured with platform metrics in the region that you want to monitor, see [Getting started with {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

   For more information about the locations where {{site.data.keyword.registryshort_notm}} is enabled for monitoring, see [Locations of platform metrics](#registry_monitor_locations).

2. Log in to {{site.data.keyword.cloud_notm}}.

    ```txt
    ibmcloud login
    ```
    {: pre}

3. Target the [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) where you want to enable metrics by running the [`ibmcloud cr region-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set) command. Replace `<region>` with the name of the [region](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).

    ```txt
    ibmcloud cr region-set <region>
    ```
    {: pre}

4. Check whether metrics are already enabled for your account by running the following [`ibmcloud cr platform-metrics`](/docs/Registry?topic=Registry-containerregcli#ic_cr_platform_metrics) command. This command also displays the registry that the result applies to.

    ```txt
    ibmcloud cr platform-metrics --status
    ```
    {: pre}

5. Enable platform metrics by running the following `ibmcloud cr platform-metrics` command. It can take up to 30 minutes for your metrics to become effective.

    ```txt
    ibmcloud cr platform-metrics --enable
    ```
    {: pre}

    If you want to target a different [region](/docs/Registry?topic=Registry-registry_overview#registry_regions), run the [`ibmcloud cr region-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set) command.

## Locations of platform metrics
{: #registry_monitor_locations}

You can configure one monitoring instance in each region to collect platform metrics for {{site.data.keyword.registrylong_notm}}. The following tables list the locations where metrics can be collected if you enable collection of {{site.data.keyword.registryshort_notm}} service metrics in that region.

| Locations in Americas | Platform metrics available |
|-----------------------|----------------------------|
| `Dallas (us-south)` | Yes |
| `Sao Paulo (br-sao)` | Yes |
| `Toronto (ca-tor)` | Yes |
{: caption="Table 1. The automatic collection of {{site.data.keyword.registryshort_notm}} service metrics in Americas locations" caption-side="bottom"}
{: #table_registry_monitor_collect_service_metrics_americas}

| Locations in Asia Pacific | Platform metrics available |
|---------------------------|----------------------------|
| `Osaka (jp-osa)` | Yes |
| `Sydney (au-syd)` | Yes |
| `Tokyo (jp-tok)` | Yes |
{: caption="Table 2. The automatic collection of {{site.data.keyword.registryshort_notm}} service metrics in Asia Pacific locations" caption-side="bottom"}
{: #table_registry_monitor_collect_service_metrics_ap}

| Locations in Europe | Platform metrics available |
|---------------------|----------------------------|
| `Frankfurt (eu-de)` | Yes |
| `London (eu-gb)` | Yes |
| `Madrid (eu-es)` | Yes |
{: caption="Table 3. The automatic collection of {{site.data.keyword.registryshort_notm}} service metrics in Europe locations" caption-side="bottom"}
{: #table_registry_monitor_collect_service_metrics_europe}

| Location for Global | Platform metrics available |
|---------------------|----------------------------|
| `Global` | Yes |
{: caption="Table 4. The automatic collection of {{site.data.keyword.registryshort_notm}} service metrics for Global" caption-side="bottom"}
{: #table_registry_monitor_collect_service_metrics_global}

For more information about where to see {{site.data.keyword.registryshort_notm}} metrics, see [Where to look for metrics](#registry_monitor_ui).

For more information about the locations where {{site.data.keyword.cloud_notm}} services are enabled to send metrics to {{site.data.keyword.mon_full_notm}}, see [{{site.data.keyword.cloud_notm}} services by location](/docs/monitoring?topic=monitoring-cloud_services_locations).

## Where to look for metrics
{: #registry_monitor_ui}

### {{site.data.keyword.mon_short}} metrics
{: #registry_monitor_ui_at}

The [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) in which a {{site.data.keyword.registryshort}} or a Vulnerability Advisor metric is available corresponds to the region of the {{site.data.keyword.registryshort}} that generated the metric.

The following table shows the location of {{site.data.keyword.mon_short}} metrics.

| Region for your account's registry | Domain name of your registry | Location of {{site.data.keyword.mon_short}} metrics |
|------------------------------------|------------------------------|-----------------------------------------------------|
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
| `ap-south` | `au.icr.io` | `Sydney (au-syd)` |
| `br-sao` | `br.icr.io` | `Sao Paulo (br-sao)` |
| `ca-tor` | `ca.icr.io` | `Toronto (ca-tor)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `eu-es` | `es.icr.io` | `Madrid (eu-es)` |
| `jp-osa` | `jp2.icr.io` | `Osaka (jp-osa)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
{: caption="Table 5. Location of {{site.data.keyword.mon_short}} metrics" caption-side="bottom"}
{: #table_registry_monitor_metrics_location}

The following table shows the location of global registry {{site.data.keyword.mon_short}} metrics.

| Registry | Global registry | Location of {{site.data.keyword.at_full_notm}} metrics |
|----------|-----------------|--------------------------------------------------------|
| `Global` | `icr.io` | `Washington (us-east)` |
{: caption="Table 6. Location of global registry {{site.data.keyword.mon_short}} metrics" caption-side="bottom"}
{: #table_registry_monitor_metrics_location_global}

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

| Dashboard name | Description | Default dashboard |
|----------------|-------------|-------------------|
| {{site.data.keyword.registryshort_notm}} Usage | A dashboard that you can use to visualize the traffic usage and storage usage. Traffic usage is the sum of bytes from image pulls from your {{site.data.keyword.registryshort_notm}} namespaces in the current billing period. Storage usage is the sum of bytes of images in your {{site.data.keyword.registryshort_notm}} namespaces. | Yes |
| {{site.data.keyword.registryshort_notm}} Quota Usage | A dashboard that you can use to visualize the traffic usage and storage usage and compare the data to your quotas, if set. Visible only to those accounts that have finite quotas. The **Container Registry Quota Usage** dashboard is available only if you enable metrics and you have both a storage and a traffic quota set. | No |
{: caption="Table 7. Predefined dashboards" caption-side="bottom"}
{: #table_registry_monitor_dashboards_predefined}

The predefined dashboards can't be changed. You can copy any predefined dashboard so that you can change it to suit your requirements. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards).
{: important}

When you start your dashboard, some metrics might display a `Data Load Error` warning icon. This warning is because more time is required to create the data. When data is available, the warning sign goes away, and the metric is populated. You might also need to change the resolution period.
{: note}

## Platform metrics
{: #metrics}

| Metric Name | Information |
|-------------|-------------|
| [`Pull Traffic`](#ibm_containerregistry_pull_traffic) | The account's pull traffic in the current month. |
| [`Pull Traffic Quota`](#ibm_containerregistry_pull_traffic_quota) | The account's pull traffic quota. |
| [`Storage Quota`](#ibm_containerregistry_storage_quota) | The account's storage quota. |
| [`Storage`](#ibm_containerregistry_storage) | The account's storage usage. |
{: caption="Table 8. Metrics available by plan names" caption-side="bottom"}
{: #table_registry_monitor_metrics_plan}

### `Pull Traffic`
{: #ibm_containerregistry_pull_traffic}

The account's pull traffic in the current month.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 9. Pull Traffic metric metadata" caption-side="bottom"}
{: #table_registry_monitor_metrics_pull_traffic}

### `Pull Traffic Quota`
{: #ibm_containerregistry_pull_traffic_quota}

The account's pull traffic quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_pull_traffic_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 10. Pull Traffic Quota metric metadata" caption-side="bottom"}
{: #table_registry_monitor_metrics_pull_traffic_quota}

### `Storage Quota`
{: #ibm_containerregistry_storage_quota}

The account's storage quota.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage_quota`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 11. Storage Quota metric metadata" caption-side="bottom"}
{: #table_registry_monitor_metrics_storage_quota}

### `Storage`
{: #ibm_containerregistry_storage}

The account's storage usage.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_containerregistry_storage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
{: caption="Table 12. Storage metric metadata" caption-side="bottom"}
{: #table_registry_monitor_metrics_storage}
