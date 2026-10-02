---

copyright:
  years: 2024, 2026
lastupdated: "2026-10-02"

keywords: IBM Cloud Container Registry notices, firewall, cdn, domain-based firewall, domains, icr.io, notices, content delivery network

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Important firewall changes from 4 September 2024 for users that pull {{site.data.keyword.registryshort}} images from global (`icr.io`)
{: #registry_notices_firewall}

To ensure continued worldwide performance for global registry (`icr.io`) in {{site.data.keyword.registrylong}}, a content delivery network (CDN) was enabled on 4 September 2024. If you use domain-based firewall rules to access the global registry, you must ensure that your rules include the required domains.
{: shortdesc}

The original announcement was published on 1 July 2024.
{: note}

## What you need to know about this change
{: #registry_notices_firewall_know}

If you use domain-based firewall rules, you must add the following domains. The domains accommodate future changes that might issue a redirect for certain requests such as an image layer download for traffic optimization. Regional registries are not impacted. For more information about regional registries, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## Required firewall domains
{: #registry_notices_firewall_actions}

If you use a public network to access the global instance of {{site.data.keyword.registryshort}} by using the domain `icr.io`, your firewall rules must include the following domains:

- `dd0.icr.io`
- `dd2.icr.io`

If you are located in China, you must also allow the following domains:

- `dd1-icr.ibm-zh.com`
- `dd3-icr.ibm-zh.com`

For more information about {{site.data.keyword.registryshort}} public access and firewall rules, see [Accessing {{site.data.keyword.registryshort}} through a firewall](/docs/Registry?topic=Registry-registry_firewall).
