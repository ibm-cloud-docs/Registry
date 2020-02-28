---

copyright:
  years: 2019, 2020
lastupdated: "2020-02-28"

keywords: logging, logs, platform services logs,

subcollection: registry

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

# {{site.data.keyword.la_full_notm}} platform services logs
{: #registry_logs}

{{site.data.keyword.registrylong}} generates platform services logs that are displayed in your LogDNA instances.
{: shortdesc}

For information about how to configure LogDNA instances to receive platform services logs, see [Configuring IBM Cloud service logs](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-config_svc_logs).

Most of the time when you work with {{site.data.keyword.registrylong_notm}} you are pushing, pulling, or managing images. These interactions output results that either you or your automation, tools, or runtime receive, therefore {{site.data.keyword.registrylong_notm}} doesn't generate platform logs for them. {{site.data.keyword.at_full_notm}} provides a comprehensive list of events for auditing these interactions, see [Activity Tracker events](/docs/Registry?topic=registry-at_events).

{{site.data.keyword.registrylong_notm}} generates platform services logs that are displayed in your LogDNA instances for the following specific cases:

- When {{site.data.keyword.registrylong_notm}} runs scheduled retention policies for namespaces in your account
- When {{site.data.keyword.registrylong_notm}} calculates your account's registry traffic and average storage usage per hour for a region

## Where to look for {{site.data.keyword.la_full_notm}} logs
{: #registry_logs_region}

The [region](/docs/Registry?topic=registry-registry_overview#registry_regions) in which an {{site.data.keyword.registrylong_notm}} or a Vulnerability Advisor log entry is available corresponds to the region of the {{site.data.keyword.registrylong_notm}} that generated the log, except for `ap-south`. Logs for `ap-south` show in `Tokyo (jp-tok)`.

The following table shows the location of {{site.data.keyword.la_full_notm}}.

| Region for your account's registry | Domain name of your registry | Location of {{site.data.keyword.la_full_notm}} logs |
|-----------------|-----------------|-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="Table 1. Location of {{site.data.keyword.la_full_notm}} logs" caption-side="top"}

The following table shows the location of global registry {{site.data.keyword.la_full_notm}} logs.

| Registry | Global registry | Location of {{site.data.keyword.la_full_notm}} logs |
|-----------------|-----------------|-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 2. Location of global registry {{site.data.keyword.la_full_notm}} logs" caption-side="top"}
