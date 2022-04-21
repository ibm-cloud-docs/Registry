---

copyright:
  years: 2022
lastupdated: "2022-04-21"

keywords: IBM Cloud Container Registry notices, iam, IP address list, restricted IP address, change, private network, change, impact, actions, know

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Update IAM restricted IP address lists by 23 May 2022
{: #registry_notices_iam_private_network}

By 23 May 2022, if you're connecting to {{site.data.keyword.registrylong}} over the private network and you're using {{site.data.keyword.iamshort}} (IAM) restricted IP address lists, you must change your IAM restricted IP list.
{: shortdesc}

## What you need to know
{: #registry_notices_iam_private_network_know}

From 23 May 2022, when connections are made to {{site.data.keyword.registrylong_notm}}, the real source IP of the request will be used. Previously, when connections came in over private networks, the source IP addresses that you saw in {{site.data.keyword.at_full_notm}} and that were configured for [IAM restricted IP address lists](/docs/account?topic=account-ips) were documented [{{site.data.keyword.registryshort}} IP addresses](/docs/containers?topic=containers-firewall#firewall_private_container_registry).

This change is required because of a security improvement to {{site.data.keyword.registrylong_notm}}. Instead of adding the {{site.data.keyword.registrylong_notm}} private IP addresses to your allowed IP list, you must add the private subnet and IP addresses of your own hosts, for example, worker nodes in an {{site.data.keyword.containerlong_notm}} cluster.

If you don't make the [appropriate updates](#registry_notices_iam_pivate_network_action) before this change happens on 23 May 2022, your requests to {{site.data.keyword.registryshort}} might fail to be authorized.
{: important}

## How you benefit from this change
{: #registry_notices_iam_pivate_network_benefit}

This change increases security for any {{site.data.keyword.registrylong_notm}} users that use private connections and IAM restricted IP address lists. After the change, you must configure the restricted IP address list to allow the private subnet and IP addresses of your own host. This change means that you can ensure {{site.data.keyword.registryshort}} OAuth requests originate only from hosts that you own.

If you use {{site.data.keyword.at_full_notm}}, you can see the true source IP address in any audit logs, where previously you saw a private {{site.data.keyword.registryshort}} owned IP.

## Understanding if you are impacted
{: #registry_notices_iam_pivate_network_impact}

You are accessing {{site.data.keyword.registryshort}} over the private network if one of the following statements is true:

- You're using one of the `private.*` domains, for example, `private.us.icr.io`.
- You're using an {{site.data.keyword.containerlong_notm}} cluster in a [configuration](/docs/containers?topic=containers-registry#cluster_registry_auth_private) that automatically talks to the registry over a private connection.
- You are accessing {{site.data.keyword.registryshort}} through a virtual private cloud (VPC) Virtual Private Endpoint Gateway (VPE Gateway).

## What actions you need to take
{: #registry_notices_iam_pivate_network_action}

You must take the appropriate actions before 23 May 2022. If you don’t make the appropriate updates, your requests to push and pull from {{site.data.keyword.registryshort}} might fail.
{: important}

By 23 May 2022, if you access {{site.data.keyword.registryshort}} over the private network and maintain a list of restricted IP addresses in IAM, you must update your IAM restricted IP address list to include any IP addresses or subnets of hosts in your account that make requests to {{site.data.keyword.registryshort}}. These IP addresses and subnets are in addition to the current {{site.data.keyword.registryshort}} [private IP addresses](/docs/containers?topic=containers-firewall#firewall_private_container_registry). 

After 27 May 2022, you can remove the existing {{site.data.keyword.registryshort}} private IP addresses from your allowed IP list.

For more information about connecting to {{site.data.keyword.registryshort}} over the private network, see [Securing your connection to Container Registry](/docs/Registry?topic=Registry-registry_private).


