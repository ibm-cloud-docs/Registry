---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notifications, notifications, registry, changes, ip address

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Changes to private IP addresses for {{site.data.keyword.registryshort}} from 15 December 2022
{: #registry_notices_ip_address}

The {{site.data.keyword.registrylong}} private IP addresses that were replaced on 5 July 2022 are being decommissioned on 15 December 2022.
{: shortdesc}

The original announcement was published on 2 November 2022.
{:  note}

## What you need to know about this change
{: #registry_notices_ip_address_know}

IP addresses for accessing {{site.data.keyword.registryshort}} over the private network changed on 5 July 2022, see [{{site.data.keyword.registryshort}} private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network). You continue to be able to use these old IP addresses, but they are due to be decommissioned on 15 December 2022. After this date, you will not be able to access {{site.data.keyword.registryshort}} by using these IP addresses.

{{site.data.keyword.containerlong_notm}} cluster workers are configured so that you can access {{site.data.keyword.registryshort}} over the private network even when the public domain is used. This process caches the DNS result on worker startup and is not refreshed until a cluster worker is reloaded, replaced, or rebooted. If you have not reloaded, replaced, or rebooted the cluster workers since 5 July 2022, it is likely that they still refer to the old {{site.data.keyword.registryshort}} private IP addresses. If these workers are not reloaded or replaced, they will not function correctly after the old {{site.data.keyword.registryshort}} IP addresses are decommissioned.

If you have any other custom configuration that uses the old {{site.data.keyword.registryshort}} private IP addresses and you do not update your configuration to use the new {{site.data.keyword.registryshort}} IP addresses, you might have a problem with accessing {{site.data.keyword.registryshort}} over the private network. For more information, see [Permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-firewall#firewall_private_container_registry).

## What actions you need to take
{: #registry_notices_ip_address_actions}

Any cluster workers that you have not reloaded, replaced, or rebooted since 5 July 2022 must be reloaded or replaced before 15 December 2022. For more information about how to reload workers for classic clusters, see [`ibmcloud ks worker reload`](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_reload). For more information about how to replace workers for VPC clusters, see [`ibmcloud ks worker replace`](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace). You can also reboot affected workers but this action is not recommended due to the risks associated with rebooting. For more information about rebooting workers, see [`ibmcloud ks worker reboot`](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_reboot).

If you have any other custom configuration that uses the old {{site.data.keyword.registryshort}} private IP addresses, such as for firewall rules or Calico policies, you must update your configuration to use the new {{site.data.keyword.registryshort}} IP addresses and remove the old IP addresses. Both the old and new private IP addresses are documented in the {{site.data.keyword.containerlong_notm}} documentation. For more information, see [Permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-firewall#firewall_private_container_registry).

The {{site.data.keyword.containerlong_notm}} [Calico policy samples](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies){: external} will be updated to remove the old IP addresses on 15 December 2022. If you use these samples, ensure that you pull in the most recent samples after this date.

## Original announcement
{: #registry_notices_ip_address_announce}

The original announcement was published on 2 November 2022.
