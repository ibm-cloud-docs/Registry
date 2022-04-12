---

copyright:
  years: 2021, 2022
lastupdated: "2022-04-12"

keywords: access restrictions, IP addresses, access, public, private, network

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using IAM IP address access restrictions
{: #registry_iam_ip}

You can enable [IAM IP address access restrictions](/docs/account?topic=account-ips) when you're using {{site.data.keyword.registrylong}}.
{: shortdesc}

To enable IAM IP address access restrictions, you must ensure that the {{site.data.keyword.iamshort}} (IAM) [allowlist](x3954001){: term} is configured so that the {{site.data.keyword.registryshort}} OAuth service can still function. The OAuth service is used to authenticate image pulls and pushes in {{site.data.keyword.registryshort}}.

## Granting access if you are using a public network
{: #registry_iam_ip_public}

If you're using {{site.data.keyword.registrylong_notm}} over a public network, you must ensure that the IP addresses of any computers that can originate pulls and pushes are added to the IAM IP allowlist.

## Granting access if you are using a private network
{: #registry_iam_ip_private}

If you're using {{site.data.keyword.registrylong_notm}} in one of the following scenarios, you must add the registry's own private IP addresses for the appropriate region to the allowlist. For more information about these IP addresses, see [Permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-firewall#firewall_private_container_registry).

- You're using one of the `private.*` domains, for example, `private.us.icr.io`.
- You're using an {{site.data.keyword.containerlong_notm}} cluster in a [configuration](/docs/containers?topic=containers-registry#cluster_registry_auth_private) that automatically talks to the registry over a private connection.

This action is required for private connections because the source IP address that {{site.data.keyword.registryshort}} receives is the IP address of the {{site.data.keyword.cloud_notm}} service endpoint and not the IP from where the request originated.
{: note}


