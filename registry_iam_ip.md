---

copyright:
  years: 2021, 2025
lastupdated: "2025-10-14"

keywords: access restrictions, IP addresses, access, public, private, network

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using IAM IP address access restrictions in {{site.data.keyword.registryshort_notm}}
{: #registry_iam_ip}

You can enable IAM IP address access restrictions when you're using {{site.data.keyword.registrylong}}.
{: shortdesc}

To enable IAM IP address access restrictions, you must ensure that the {{site.data.keyword.iamshort}} (IAM) access list is configured so that the {{site.data.keyword.registryshort}} OAuth service can still function. The OAuth service is used to authenticate image pulls and pushes in {{site.data.keyword.registryshort}}.

You must ensure that the IP addresses of any computers that can originate pulls and pushes are added to the IAM IP address access list, see [Allowing specific IP addresses](/docs/account?topic=account-ips).

## Granting access if you are using a public network
{: #registry_iam_ip_public}

If you're using {{site.data.keyword.registrylong_notm}} over a public network, you must ensure that the Public IP addresses of any computers that can originate pulls and pushes are added to the IAM IP allowlist.

## Granting access if you are using a private network
{: #registry_iam_ip_private}

If you're using {{site.data.keyword.registrylong_notm}} in one of the following scenarios, you must add the private IP addresses of any computers that can originate pulls and pushes to the allowlist.

- You're using one of the private (`private.*`) domains, for example `private.us.icr.io`.
- You're using an {{site.data.keyword.containerlong_notm}} cluster in a configuration that automatically talks to the registry over a private connection. For more information, see [Private network connection to `icr.io` registries](/docs/containers?topic=containers-registry#cluster_registry_auth_private).
