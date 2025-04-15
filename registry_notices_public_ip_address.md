---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, public IP address, IP addresses

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Changes to the public IP addresses for {{site.data.keyword.registryshort}} from 13 September 2021
{: #registry_notices_public_ip_address}

From 13 September 2021, {{site.data.keyword.registrylong}} is changing the public IP address ranges that are used to serve images and API requests. Furthermore, the IP address ranges are not being published anymore.
{: shortdesc}

The original announcement was published on 18 August 2021.
{: note}

## What you need to know:
{: #registry_notices_public_ip_address_know}

Any public internet-facing firewall rules that are based on published IP address ranges will stop working after 13 September 2021. If you have these rules, you must remove them.

## What actions you need to take
{: #registry_notices_public_ip_address_action}

If you connect to {{site.data.keyword.registryshort}} by using the public internet and you have your own firewalls that have rules that allow access that is based on previously published IP address ranges, you must remove them. You do not need to change rules that are based on the use of domain names.

If you are concerned about removing firewall restrictions, consider the use of rules that are based on domain names or you can adopt private networking. For more information, see [Securing your connection to {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_private).

## When the changes take effect
{: #registry_notices_public_ip_address_change}

The changes take effect from 13 September 2021.

## Original announcement
{: #registry_notices_public_ip_address_announce}

The original announcement was published on 18 August 2021.
