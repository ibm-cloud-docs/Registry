---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, iam, IP address list, restricted IP address, change, private network, actions

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022
{: #registry_notices_iam_private_network}

By 23 June 2022, if you connect to {{site.data.keyword.registrylong}} over the private network and you use {{site.data.keyword.iamshort}} (IAM) restricted IP address lists, you must change your IAM restricted IP list. This change also affects you if you have allowlists or a firewall rule.
{: shortdesc}

The original announcement was published on 7 April 2022.
{: note}

On 23 June 2022, only the `br-sao` and `ca-tor` regions changed. The remaining regions changed on 5 July 2022. This change was originally due to take place on 23 May 2022 but was delayed.
{: note}

## What you need to know about this change
{: #registry_notices_iam_private_network_know}

From 5 July 2022 (23 June 2022 for the `br-sao` and `ca-tor` regions), when connections are made to {{site.data.keyword.registryshort}}, the real source IP of the request is used. Previously, when connections came in over private networks, the source IP addresses that you saw in the activity tracker auditing events and that were configured for [IAM restricted IP address lists](/docs/account?topic=account-ips) were documented {{site.data.keyword.registryshort}} [IP addresses](/docs/containers?topic=containers-firewall#firewall_private_container_registry).

This change improves the security of {{site.data.keyword.registrylong_notm}}. With this change, you can configure real, account specific, private client IP addresses in IAM restricted IP lists, instead of the documented list of shared IP addresses. You must now allow private subnet and IP addresses of your own hosts (for example, worker nodes in a classic {{site.data.keyword.containerlong_notm}} cluster or the egress IP of a VPC network).

As part of this change, the {{site.data.keyword.registryshort}} private IP addresses also altered; therefore, updates to your firewall configuration might be required.

If you use [Calico](https://www.tigera.io/project-calico/){: external}, the samples are updated to take account of the change.

You must not remove the {{site.data.keyword.registryshort}} private IP addresses from your IAM restricted IP list until an announcement advises you to do so.
{: important}

You must take the [appropriate actions](#registry_notices_iam_pivate_network_action) before this change happens on 23 June 2022, otherwise your requests to {{site.data.keyword.registryshort}} might fail to be authorized.
{: important}

## How you benefit from this change
{: #registry_notices_iam_pivate_network_benefit}

This change increases security for any {{site.data.keyword.registryshort}} users that use private connections and IAM restricted IP address lists. After the change, you must configure the restricted IP address list to allow the private subnet and IP addresses of your own host. This change means that you can ensure that {{site.data.keyword.registryshort}} OAuth requests originate only from hosts that you own.

If you use {{site.data.keyword.atracker_full_notm}}, you can see the true source IP address in any audit logs, where previously you saw a {{site.data.keyword.registryshort}} owned IP that was private.

## Understanding if you are impacted by this change
{: #registry_notices_iam_pivate_network_impact}

You are impacted if you are accessing {{site.data.keyword.registryshort}} over the private network.

You are accessing {{site.data.keyword.registryshort}} over the private network if one of the following statements is true:

- You use one of the `private.*` domains, for example `private.us.icr.io`.
- You use an {{site.data.keyword.containerlong_notm}} cluster in a [configuration](/docs/containers?topic=containers-registry#cluster_registry_auth_private) that automatically talks to the registry over a private connection.
- You access {{site.data.keyword.registryshort}} through a virtual private cloud (VPC) virtual private endpoint gateway (VPE gateway).
- You use the {{site.data.keyword.registryshort}} private IP addresses for configuring network access, for example, in firewalls or Access Control Lists (ACL).

If any of the previous statements is true when this change takes effect, then the IP addresses in the activity tracker auditing events change, but you don't need to do anything unless you are also using IAM IP address access restrictions.

## What actions you need to take
{: #registry_notices_iam_pivate_network_action}

You must take the appropriate actions before 23 June 2022. If you don’t make the appropriate updates, your requests to push and pull from {{site.data.keyword.registryshort}} might fail.
{: important}

Depending on which of the following scenarios you fit, take the appropriate action.

You access {{site.data.keyword.registryshort}} over the private network and maintain a list of restricted IP addresses in IAM.
:   You must update your IAM restricted IP address list to include any IP addresses or subnets of hosts in your account that make requests to {{site.data.keyword.registryshort}}. You must keep the current {{site.data.keyword.registryshort}} private IP addresses in your restricted IP list until an announcement indicates it is safe to remove them. For more information about how to update a restricted IP address list, see [Allowing specific IP addresses](/docs/account?topic=account-ips) in the {{site.data.keyword.iamshort}} (IAM) documentation.

Your firewalls are configured with the {{site.data.keyword.registryshort}} private IP addresses.
:   You must include the new private IP addresses in your firewall configuration. For more information about connecting to {{site.data.keyword.registryshort}} over the private network, see [Securing your connection to {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_private).

For more information about the new and current {{site.data.keyword.registryshort}} private IP addresses, see the following topics:

- For {{site.data.keyword.containerlong_notm}}, see [Permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-firewall#firewall_private_container_registry).
- For {{site.data.keyword.openshiftlong}}, see [Permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-firewall#firewall_private_container_registry).
