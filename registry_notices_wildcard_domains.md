---

copyright:
  years: 2023
lastupdated: "2023-06-19"

keywords: IBM Cloud Container Registry notices, wildcard, domain, firewall

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Upcoming public networking changes for {{site.data.keyword.registryshort}}
{: #registry_notices_wildcard_domains}

Users that use the public network to access {{site.data.keyword.registrylong}} are advised to use a wildcard domain, such as `*.icr.io`, in their firewalls rules. The use of a wildcard domain accommodates future changes that might issue a redirect for certain requests such as an image layer download for traffic optimization.

This advice is a change from existing advice that states that you must allow only the public domain of the {{site.data.keyword.registryshort}} that you are using.
{: note}
