---

copyright:
  years: 2019, 2021
lastupdated: "2021-04-06"

keywords: platform services logs for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry logs, IBM Cloud Container Registry security, analyzing logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry logs, IBM Cloud Container Registry logs,

subcollection: Registry

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:term: .term}
{:external: target="_blank" .external}

# Analyzing logs for {{site.data.keyword.registryshort_notm}}
{: #registry_logs}

{{site.data.keyword.registrylong}} generates platform services logs that are displayed in your logging instances.
{: shortdesc}

For more information about how to configure logging instances to receive platform services logs, see [Configuring IBM Cloud service logs](/docs/log-analysis?topic=log-analysis-config_svc_logs).

Most of the time when you work with {{site.data.keyword.registrylong_notm}} you are pushing, pulling, or managing images. These interactions output results that either you or your automation, tools, or runtime receive; {{site.data.keyword.registrylong_notm}} doesn't generate platform logs for them. {{site.data.keyword.at_full_notm}} provides a comprehensive list of events for auditing these interactions, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

{{site.data.keyword.registrylong_notm}} generates platform services logs that are displayed in your logging instances for the following specific cases:

- When {{site.data.keyword.registrylong_notm}} runs scheduled retention policies for namespaces in your account.
- When {{site.data.keyword.registrylong_notm}} calculates your account's registry traffic and average storage usage per hour for a region.

## Where to look for {{site.data.keyword.la_full_notm}} logs
{: #registry_logs_region}

The [region](/docs/Registry?topic=Registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor log entry is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} that generated the log, except for `ap-south` and `jp-osa`. Logs for `ap-south` and `jp-osa` show in `Tokyo (jp-tok)`.

The following table shows the location of {{site.data.keyword.la_full_notm}} logs.

| Region for your account's registry | Domain name of your registry | Location of {{site.data.keyword.la_full_notm}} logs |
|-----------------|-----------------|-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
| `jp-osa` | `jp2.icr.io` | `Tokyo (jp-tok)` |
{: caption="Table 1. Location of {{site.data.keyword.la_full_notm}} logs" caption-side="top"}

The following table shows the location of global registry {{site.data.keyword.la_full_notm}} logs.

| Registry | Global registry | Location of {{site.data.keyword.la_full_notm}} logs |
|-----------------|-----------------|-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 2. Location of global registry {{site.data.keyword.la_full_notm}} logs" caption-side="top"}
