---

copyright:
  years: 2021
lastupdated: "2021-04-30"

keywords: 

subcollection: Registry

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:term: .term}
{:external: target="_blank" .external}

# Using IAM IP address access restrictions with {{site.data.keyword.registrylong_notm}}
{: #registry_iam_ip}

If you want to enable [IAM IP address access restrictions](/docs/account?topic=account-ips) when you're using {{site.data.keyword.registrylong}}, you must ensure that the {{site.data.keyword.iamshort}} (IAM) allowlist is configured so that the {{site.data.keyword.registrylong_notm}} OAuth service, which is used to authenticate image pulls and pushes, can still function.

The deprecated [`ibmcloud cr image-build`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) command can't be used in combination with IAM IP allowlists.
{: note}

## Granting access if you are using {{site.data.keyword.registrylong_notm}} over the public network
{: #registry_iam_ip_public}

If you're using the registry over the public network, you must ensure that the IP addresses of any computers that can originate pulls and pushes are added to the IAM IP allowlist.

## Granting access if you are using {{site.data.keyword.registrylong_notm}} over the private network
{: #registry_iam_ip_private}

If you're using the registry in one of the following scenarios, you must add the registry's own private IP addresses for the appropriate region to the allowlist. You can find these IP addresses in step 6 of [Opening required ports in a private firewall](/docs/containers?topic=containers-firewall#firewall_private) in the {{site.data.keyword.containerlong_notm}} documentation.

- You're using one of the `private.*` domains, for example, `private.us.icr.io`.
- You're using an {{site.data.keyword.containerlong_notm}} cluster in a [configuration](/docs/containers?topic=containers-registry#cluster_registry_auth_private) that automatically talks to the registry over a private connection.

This action is required for private connections because the source IP address that {{site.data.keyword.registrylong}} receives is the IP address of the {{site.data.keyword.cloud_notm}} service endpoint and not the IP from where the request originated.
{: note}
