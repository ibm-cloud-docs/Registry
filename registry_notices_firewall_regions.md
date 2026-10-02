---

copyright:
  years: 2026
lastupdated: "2026-10-02"

keywords: IBM Cloud Container Registry notices, firewall, cdn, domain-based firewall, domains, icr.io, notices, content delivery network, regions

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Firewall changes from 18 March 2026 for users that pull {{site.data.keyword.registryshort}} images from regional instances
{: #registry_notices_firewall_regions}

To ensure continued performance for regional instances of {{site.data.keyword.registrylong}}, a content delivery network (CDN) was enabled on 18 March 2026. If you use domain-based firewall rules to access regional registry instances, you must ensure that your rules include the required domains.
{: shortdesc}

The original announcement was published on 20 January 2026.
{: note}

## What you need to know about this change
{: #registry_notices_firewall_regions_know}

If you use domain-based firewall rules, you must add the following domains. The domains accommodate future changes that might issue a redirect for certain requests such as an image layer download for traffic optimization.

## Required firewall domains
{: #registry_notices_firewall_regions_actions}

If you use a public network to access {{site.data.keyword.registrylong_notm}}, your firewall rules must include the following domains:

| Local {{site.data.keyword.registryshort_notm}} region | Domain name |
| ----------------------------------------------------- | ----------- |
| `au-syd` | `dd0.au.icr.io` |
| `br-sao` | `dd0.br.icr.io` |
| `ca-mon` | `dd0.ca2.icr.io` |
| `ca-tor` | `dd0.ca.icr.io` |
| `eu-de` | `dd0.de.icr.io` |
| `eu-es` | `dd0.es.icr.io` |
| `eu-gb` | `dd0.uk.icr.io` |
| `jp-osa` | `dd0.jp2.icr.io` |
| `jp-tok` | `dd0.jp.icr.io` |
| `us-south` | `dd0.us.icr.io` |
{: caption="Add these domains to your firewall rules for {{site.data.keyword.registryshort_notm}}" caption-side="bottom"}
{: #table_registry_firewall_domains_notice}

For more information about {{site.data.keyword.registryshort}} public access and firewall rules, see [Accessing {{site.data.keyword.registryshort}} through a firewall](/docs/Registry?topic=Registry-registry_firewall).
