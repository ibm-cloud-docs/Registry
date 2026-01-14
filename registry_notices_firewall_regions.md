---

copyright:
  years: 2026
lastupdated: "2026-01-14"

keywords: IBM Cloud Container Registry notices, firewall, cdn, domain-based firewall, domains, icr.io, notices, content delivery network, regions

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Important firewall changes from 18 March 2026 for users that pull {{site.data.keyword.registryshort}} images from regional instances
{: #registry_notices_firewall_regions}

To ensure continued performance for regional instances of {{site.data.keyword.registrylong}}, a content delivery network (CDN) is being enabled that means that you might have to adjust your firewall settings. If you need to adjust your firewall settings, you must adjust them by 18 March 2026.
{: shortdesc}

The original announcement was published on 14 January 2026.
{: note}

## What you need to know about this change
{: #registry_notices_firewall_regions_know}

If you use domain-based firewall rules, you must add the following domains. The domains accommodate future changes that might issue a redirect for certain requests such as an image layer download for traffic optimization.

## What actions you must take by 18 March 2026
{: #registry_notices_firewall_regions_actions}

If you use a public network to access {{site.data.keyword.registrylong_notm}}, you must add the following domains to your firewall rules by 18 March 2026:

{{registry_firewall.md#table_registry_firewall_domains}}

For more information about {{site.data.keyword.registryshort}} public access and firewall rules, see [Accessing {{site.data.keyword.registryshort}} through a firewall](/docs/Registry?topic=Registry-registry_firewall).
