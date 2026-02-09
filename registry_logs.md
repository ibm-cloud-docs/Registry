---

copyright:
  years: 2019, 2026
lastupdated: "2026-02-09"

keywords: platform services logs for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry logs, IBM Cloud Container Registry security, analyzing logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry logs, IBM Cloud Container Registry logs, logs, region

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Logging for {{site.data.keyword.registryshort_notm}}
{: #registry_logs}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.registrylong}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems.
{: shortdesc}

{{site.data.keyword.logs_routing_full_notm}} is a platform service. You can use {{site.data.keyword.logs_routing_full_notm}} to route the platform logs in your account to your choice of destination by configuring a tenant that defines where the platform logs are sent. For more information, see [About Logs Routing](/docs/logs-router?topic=logs-router-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on platform logs that are generated in your account and routed by {{site.data.keyword.logs_routing_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where platform logs are generated
{: #log-locations}

{{site.data.keyword.registrylong_notm}} generates platform logs that are displayed in your logging instances. The following tables list the locations where the automatic collection of {{site.data.keyword.registryshort_notm}} service logs is enabled.

| Locations in Americas | Are platform services logs available? |
| --------------------- | ------------------------------------- |
| `Dallas (us-south)` | [Yes]{: tag-green} |
| `Sao Paulo (br-sao)` | [Yes]{: tag-green} |
| `Montreal (ca-mon)` | [Yes]{: tag-green} |
| `Toronto (ca-tor)` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Americas locations" caption-side="bottom"}
{: #table_registry_logs_service_americas}

| Locations in Asia Pacific | Are platform services logs available? |
| ------------------------- | ------------------------------------- |
| `Chennai-Airtel (in-che)` | [Yes]{: tag-green} |
| `Osaka (jp-osa)` | [Yes]{: tag-green} |
| `Sydney (au-syd)` | [Yes]{: tag-green} |
| `Tokyo (jp-tok)` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Asia-Pacific locations" caption-side="bottom"}
{: #table_registry_logs_service_ap}

| Locations in Europe | Are platform services logs available? |
| ------------------- | ------------------------------------- |
| `Frankfurt (eu-de)` | [Yes]{: tag-green} |
| `London (eu-gb)` | [Yes]{: tag-green} |
| `Madrid (eu-es)` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service logs in the Europe locations" caption-side="bottom"}
{: #table_registry_logs_service_europe}

| Location for Global | Are platform services logs available? |
| ------------------- | ------------------------------------- |
| `Global` | [Yes]{: tag-green} |
{: caption="The automatic collection of {{site.data.keyword.registryshort_notm}} service logs for Global" caption-side="bottom"}
{: #table_registry_logs_service_global}

For more information about where to see {{site.data.keyword.registryshort_notm}} service logs if you're using {{site.data.keyword.logs_routing_full_notm}}, see [Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}](#lr-locations).

## Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}
{: #lr-locations}

{{site.data.keyword.registryshort}} sends logs by {{site.data.keyword.logs_routing_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington DC (`us-east`) | Montreal (`ca-mon`) | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
| ------------------- | ---------------------- | ------------------- | ------------------ | -------------------- |
| [Yes]{: tag-green} | [Yes]{: tag-green} (`global`) | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where platform logs are sent in Americas locations" caption-side="top"}
{: #logr-table-1}
{: tab-title="Americas"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Chennai-Airtel (`in-che`) | Tokyo (`jp-tok`) | Sydney (`au-syd`) | Osaka (`jp-osa`) |
| ------------------ | ---------------- | ----------------- | ---------------- |
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where platform logs are sent in Asia-Pacific locations" caption-side="top"}
{: #logr-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`) | London (`eu-gb`) | Madrid (`eu-es`) |
| ------------------- | ---------------- | ---------------- |
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where platform logs are sent in Europe locations" caption-side="top"}
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

For information about fields included in every platform log, see [Fields that are included in platform logs](/docs/logs-router?topic=logs-router-about-platform-logs#about-platform-logs-2).

The following fields are included in the log record.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `logSourceCRN` | Required | Defines the account and flow log instance where the log is published. |
| `saveServiceCopy` | Required | Defines whether IBM saves a copy of the record for operational purposes. |
| `message` | Required | Description of the log that is generated. |
{: caption="Log record fields" caption-side="bottom"}
{: #table_at_log_records}



## Log messages
{: #log_messages}

An example of a billing log in the `message.message` field is:

```text
For the period starting 2026-01-07 06:00:00 +0000 UTC, and ending 2026-01-07 07:00:00 +0000 UTC, this account used 0.00GB traffic, and used an average of 157.90GB storage
```
{: screen}

## Analyzing {{site.data.keyword.registryshort}} logs
{: #cloud-logs}

You can use the following queries to analyze {{site.data.keyword.registryshort}} logs:

- A Lucene query for {{site.data.keyword.registryshort}} platform logs: `message.serviceName:"container\-registry"`
- A DataPrime query for {{site.data.keyword.registryshort}} platform logs: `filter $d.message.serviceName ~ 'container-registry'`
