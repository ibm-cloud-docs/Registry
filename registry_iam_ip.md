---

copyright:
  years: 2021
lastupdated: "2021-10-06"

keywords: 

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using IAM IP address access restrictions with {{site.data.keyword.registrylong_notm}}
{: #registry_iam_ip}

If you want to enable [IAM IP address access restrictions](/docs/account?topic=account-ips) when you're using {{site.data.keyword.registrylong}}, you must ensure that the {{site.data.keyword.iamshort}} (IAM) allowlist is configured so that the {{site.data.keyword.registrylong_notm}} OAuth service, which is used to authenticate image pulls and pushes, can still function.

## Granting access if you are using {{site.data.keyword.registrylong_notm}} over the public network
{: #registry_iam_ip_public}

If you're using the registry over the public network, you must ensure that the IP addresses of any computers that can originate pulls and pushes are added to the IAM IP allowlist.

## Granting access if you are using {{site.data.keyword.registrylong_notm}} over the private network
{: #registry_iam_ip_private}

If you're using the registry in one of the following scenarios, you must add the registry's own private IP addresses for the appropriate region to the allowlist. You can find these IP addresses in [Permit worker nodes to communicate with {{site.data.keyword.registrylong}}](/docs/containers?topic=containers-firewall#firewall_private_container_registry) in the {{site.data.keyword.containerlong_notm}} documentation.

- You're using one of the `private.*` domains, for example, `private.us.icr.io`.
- You're using an {{site.data.keyword.containerlong_notm}} cluster in a [configuration](/docs/containers?topic=containers-registry#cluster_registry_auth_private) that automatically talks to the registry over a private connection.

This action is required for private connections because the source IP address that {{site.data.keyword.registrylong}} receives is the IP address of the {{site.data.keyword.cloud_notm}} service endpoint and not the IP from where the request originated.
{: note}


