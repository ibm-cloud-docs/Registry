---

copyright:
  years: 2019, 2024
lastupdated: "2024-07-02"

keywords: platform services logs for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry logs, IBM Cloud Container Registry security, analyzing logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry logs, IBM Cloud Container Registry logs, logs, region

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}# Analyzing logs for {{site.data.keyword.registryshort_notm}}
{: #registry_logs}

{{site.data.keyword.registrylong}} generates platform services logs that are displayed in your logging instances.
{: shortdesc}

As of 28 March 2024, the {{site.data.keyword.la_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.la_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Logging is the same for both services. For information about migrating from {{site.data.keyword.la_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro). For more information about using {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.registrylong_notm}}, see [Logging for {{site.data.keyword.registryshort_notm}}(/docs/Registry?topic=Registry-logging)].
{: deprecated}

For more information about how to configure logging instances to receive platform services logs, see [Configuring {{site.data.keyword.cloud_notm}} platform logs](/docs/log-analysis?topic=log-analysis-config_svc_logs). For more information about {{site.data.keyword.loganalysislong_notm}}, see [Getting started with {{site.data.keyword.loganalysislong_notm}}](/docs/log-analysis?topic=log-analysis-getting-started).

Most of the time when you work with {{site.data.keyword.registrylong_notm}} you're pushing, pulling, or managing images. These interactions output results that either you or your automation, tools, or runtime receive; {{site.data.keyword.registrylong_notm}} doesn't generate platform logs for them. {{site.data.keyword.at_full_notm}} provides a comprehensive list of events for auditing these interactions, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

{{site.data.keyword.registrylong_notm}} generates platform services logs that are displayed in your logging instances for the following specific cases:

- When {{site.data.keyword.registrylong_notm}} runs scheduled retention policies for namespaces in your account.
- When {{site.data.keyword.registrylong_notm}} calculates your account's registry traffic and average storage usage per hour for a region.

## Locations of platform services logs
{: #registry_logs_locations}

{{site.data.keyword.registrylong_notm}} generates platform logs that are displayed in your logging instances. The following tables list the locations where the automatic collection of {{site.data.keyword.registryshort_notm}} service logs is enabled.

| Locations in Americas | Are platform services logs available? |
|-----------------------|---------------------------------------|
| `Dallas (us-south)` | Yes |
| `Sao Paulo (br-sao)` | Yes |
| `Toronto (ca-tor)` | Yes |
{: caption="Table 1. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Americas locations" caption-side="bottom"}
{: #table_registry_logs_service_americas}

| Locations in Asia Pacific | Are platform services logs available? |
|---------------------------|---------------------------------------|
| `Osaka (jp-osa)` | Yes |
| `Sydney (au-syd)` | Yes |
| `Tokyo (jp-tok)` | Yes |
{: caption="Table 2. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Asia Pacific locations" caption-side="bottom"}
{: #table_registry_logs_service_ap}

| Locations in Europe | Are platform services logs available? |
|---------------------|---------------------------------------|
| `Frankfurt (eu-de)` | Yes |
| `London (eu-gb)` | Yes |
| `Madrid (eu-es)` | Yes |
{: caption="Table 3. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Europe locations" caption-side="bottom"}
{: #table_registry_logs_service_europe}

| Location for Global | Are platform services logs available? |
|---------------------|---------------------------------------|
| `Global` | Yes |
{: caption="Table 4. The automatic collection of {{site.data.keyword.registryshort_notm}} service logs for Global" caption-side="bottom"}
{: #table_registry_logs_service_global}

For more information about where to see {{site.data.keyword.registryshort_notm}} service logs, see [Where to look for {{site.data.keyword.la_full_notm}} logs](#registry_logs_region).

For more information about the locations where {{site.data.keyword.cloud_notm}} services are enabled to send platform logs to {{site.data.keyword.la_full_notm}}, see [{{site.data.keyword.cloud_notm}} services that generate {{site.data.keyword.la_full_notm}} logs by location](/docs/log-analysis?topic=log-analysis-cloud_services_locations).

## Where to look for {{site.data.keyword.la_full_notm}} logs
{: #registry_logs_region}

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
