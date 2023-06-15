---

copyright:
  years: 2023
lastupdated: "2023-06-15"

keywords: IBM Cloud Container Registry notices, wildcard, domain, firewall

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Upcoming public networking changes for {{site.data.keyword.registryshort}}
{: #registry_notices_wildcard_domains}

Customers using the public network to access {{site.data.keyword.registrylong}} should use a wildcard domain such as `*.icr.io` in their firewalls rules. This is to accommodate future changes that may issue a redirect for certain requests such as an image layer download for traffic optimisation.

This is a change from existing advice which states you must allow only the public domain of the {{site.data.keyword.registryshort}} you are using.
{: note}

