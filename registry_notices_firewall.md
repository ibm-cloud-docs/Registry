---

copyright:
  years: 2024
lastupdated: "2024-07-25"

keywords: IBM Cloud Container Registry notices, firewall, cdn, domain-based firewall, domains, icr.io, notices, content delivery network

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Important firewall changes from 4 September 2024 for users that pull {{site.data.keyword.registryshort}} images from global (`icr.io`)
{: #registry_notices_firewall}

To ensure continued worldwide performance for global registry (`icr.io`) in {{site.data.keyword.registrylong}}, a content delivery network (CDN) is being enabled that means that you might have to adjust your firewall settings. If you need to adjust your firewall settings, you must adjust them by 4 September 2024.
{: shortdesc}

## What you need to know about this change
{: #registry_notices_firewall_know}

If you use domain-based firewall rules, you must add the following domains. The domains accommodate future changes that might issue a redirect for certain requests such as an image layer download for traffic optimization. Regional registries are not impacted. For more information about regional registries, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

## What actions you must take by 4 September 2024
{: #registry_notices_firewall_actions}

If you use a public network to access the global instance of {{site.data.keyword.registryshort}} by using the domain `icr.io`, you must add the following domains to your firewall rules by 4 September 2024:

- `dd0.icr.io`
- `dd2.icr.io`
- `dd4.icr.io`
- `dd6.icr.io`

If you are located in China, you must also allow the following domains by 4 September 2024:

- `dd1-icr.ibm-zh.com`
- `dd3-icr.ibm-zh.com`
- `dd5-icr.ibm-zh.com`
- `dd7-icr.ibm-zh.com`

For more information about {{site.data.keyword.registryshort}} public access and firewall rules, see [Accessing {{site.data.keyword.registryshort}} through a firewall](/docs/Registry?topic=Registry-registry_firewall).
