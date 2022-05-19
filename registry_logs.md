---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-18"

keywords: platform services logs for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, logging for IBM Cloud Container Registry, IBM Cloud Container Registry logs, IBM Cloud Container Registry security, analyzing logs for IBM Cloud Container Registry, viewing IBM Cloud Container Registry logs, IBM Cloud Container Registry logs, logs, region

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Analyzing logs for {{site.data.keyword.registryshort_notm}}
{: #registry_logs}

{{site.data.keyword.registrylong}} generates platform services logs that are displayed in your logging instances.
{: shortdesc}

For more information about how to configure logging instances to receive platform services logs, see [Configuring {{site.data.keyword.cloud_notm}} service logs](/docs/log-analysis?topic=log-analysis-config_svc_logs).

Most of the time when you work with {{site.data.keyword.registrylong_notm}} you are pushing, pulling, or managing images. These interactions output results that either you or your automation, tools, or runtime receive; {{site.data.keyword.registrylong_notm}} doesn't generate platform logs for them. {{site.data.keyword.at_full_notm}} provides a comprehensive list of events for auditing these interactions, see [Auditing events for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-at_events).

{{site.data.keyword.registrylong_notm}} generates platform services logs that are displayed in your logging instances for the following specific cases:

- When {{site.data.keyword.registrylong_notm}} runs scheduled retention policies for namespaces in your account.
- When {{site.data.keyword.registrylong_notm}} calculates your account's registry traffic and average storage usage per hour for a region.

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
| `jp-osa` | `jp2.icr.io` | `Osaka (jp-osa)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
{: caption="Table 1. Location of {{site.data.keyword.la_full_notm}} logs" caption-side="bottom"}

The following table shows the location of global registry {{site.data.keyword.la_full_notm}} logs.

| Registry | Global registry | Location of {{site.data.keyword.la_full_notm}} logs |
|----------|-----------------|-----------------------------------------------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Table 2. Location of global registry {{site.data.keyword.la_full_notm}} logs" caption-side="bottom"}


