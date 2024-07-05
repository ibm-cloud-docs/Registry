---

copyright:
  years: 2019, 2024
lastupdated: "2024-07-05"

keywords: platform services logs for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry logs, IBM Cloud Container Registry security, analyzing logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry logs, IBM Cloud Container Registry logs, logs, region

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Logging for {{site.data.keyword.registryshort_notm}}
{: #registry_logs}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.registrylong}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems.
{: shortdesc}

You can use {{site.data.keyword.logs_routing_full_notm}}, a platform service, to route platform logs in your account to a destination of your choice by configuring a tenant that defines where platform logs are sent. For more information, see [About Logs Routing](/docs/logs-router?topic=logs-router-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on platform logs that are generated in your account and routed by {{site.data.keyword.logs_routing_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

As of 28 March 2024, the {{site.data.keyword.la_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.la_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Logging is the same for both services. For information about migrating from {{site.data.keyword.la_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

## Locations where platform logs are generated
{: #log-locations}

{{site.data.keyword.registrylong_notm}} generates platform logs that are displayed in your logging instances. The following tables list the locations where the automatic collection of {{site.data.keyword.registryshort_notm}} service logs is enabled.

| Locations in Americas | Are platform services logs available? |
|-----------------------|---------------------------------------|
| `Dallas (us-south)` | [Yes]{: tag-green} |
| `Sao Paulo (br-sao)` | [Yes]{: tag-green} |
| `Toronto (ca-tor)` | [Yes]{: tag-green} |
{: caption="Table 1. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Americas locations" caption-side="bottom"}
{: #table_registry_logs_service_americas}

| Locations in Asia Pacific | Are platform services logs available? |
|---------------------------|---------------------------------------|
| `Osaka (jp-osa)` | [Yes]{: tag-green} |
| `Sydney (au-syd)` | [Yes]{: tag-green} |
| `Tokyo (jp-tok)` | [Yes]{: tag-green} |
{: caption="Table 2. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Asia Pacific locations" caption-side="bottom"}
{: #table_registry_logs_service_ap}

| Locations in Europe | Are platform services logs available? |
|---------------------|---------------------------------------|
| `Frankfurt (eu-de)` | [Yes]{: tag-green} |
| `London (eu-gb)` | [Yes]{: tag-green} |
| `Madrid (eu-es)` | [Yes]{: tag-green} |
{: caption="Table 3. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Europe locations" caption-side="bottom"}
{: #table_registry_logs_service_europe}

| Location for Global | Are platform services logs available? |
|---------------------|---------------------------------------|
| `Global` | [Yes]{: tag-green} |
{: caption="Table 4. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs for Global" caption-side="bottom"}
{: #table_registry_logs_service_global}

For more information about where to see {{site.data.keyword.registryshort_notm}} service logs if you are using {{site.data.keyword.la_full_notm}}, see [Locations where logs are sent to {{site.data.keyword.la_full_notm}}](#la-legacy-locations).

For more information about where to see {{site.data.keyword.registryshort_notm}} service logs if you are using {{site.data.keyword.logs_routing_full_notm}}, see [Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}](#lr-locations).

## Locations where logs are sent to {{site.data.keyword.la_full_notm}}
{: #la-legacy-locations}

As of 28 March 2024, the {{site.data.keyword.la_full_notm}} service is deprecated.
{: deprecated}

The [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor log entry is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} that generated the log, except for `ap-south`. Logs for `ap-south` show in `Tokyo (jp-tok)`.

The following table shows the location of {{site.data.keyword.la_full_notm}} logs.

| Region for your account's registry | Domain name of your registry | Location of {{site.data.keyword.la_full_notm}} logs |
|------------------------------------|------------------------------|-----------------------------------------------------|
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
| `br-sao` | `br.icr.io` | `Sao Paulo (br-sao)` |
| `ca-tor` | `ca.icr.io` | `Toronto (ca-tor)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `eu-es` | `es.icr.io` | `Madrid (eu-es)` |
| `jp-osa` | `jp2.icr.io` | `Osaka (jp-osa)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
{: caption="Table 5. Location of {{site.data.keyword.la_full_notm}} logs" caption-side="bottom"}
{: #table_registry_logs_location}

The following table shows the location of global registry {{site.data.keyword.la_full_notm}} logs.

| Registry | Global registry | Location of {{site.data.keyword.la_full_notm}} logs |
|----------|-----------------|-----------------------------------------------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 6. Location of global registry {{site.data.keyword.la_full_notm}} logs" caption-side="bottom"}
{: #table_registry_logs_location_global}

## Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}
{: #lr-locations}

{{site.data.keyword.registryshort}} sends logs by {{site.data.keyword.logs_routing_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`) | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|------------------------|--------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} (`global`) | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Table 7. Regions where platform logs are sent in Americas locations" caption-side="top"}
{: #logr-table-1}
{: tab-title="Americas"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`) | Sydney (`au-syd`) | Osaka (`jp-osa`) |
|------------------|-------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Table 7. Regions where platform logs are sent in Asia Pacific locations" caption-side="top"}
{: #logr-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`) | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------|------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Table 7. Regions where platform logs are sent in Europe locations" caption-side="top"}
{: #logrr-table-3}
{: tab-title="Europe"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

## Platform logs that are generated
{: #log-platform}

{{site.data.keyword.registrylong_notm}} generates platform services logs that are displayed in your logging instances for the following specific cases:

- When {{site.data.keyword.registrylong_notm}} runs scheduled retention policies for namespaces in your account.
- When {{site.data.keyword.registrylong_notm}} calculates your account's registry traffic and average storage usage per hour for a region.

## Viewing logs
{: #log-viewing}

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For more information about launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation](/docs/cloud-logs?topic=cloud-logs-instance-launch).

## Fields by log type
{: #log-fields}

For information about fields included in every platform log, see [Fields for platform logs](/docs/logs-router?topic=logs-router-about-platform-logs#platform_reqd).

The following fields are included in the log record.

| Field             | Type       | Description             |
|-------------------|------------|-------------------------|
| `logSourceCRN`    | Required   | Defines the account and flow log instance where the log is published. |
| `saveServiceCopy` | Required   | Defines whether IBM saves a copy of the record for operational purposes. |
| `message`         | Required   | Description of the log that is generated. |
{: caption="Table 8. Log record fields" caption-side="bottom"}
{: #table_at_log_records}
