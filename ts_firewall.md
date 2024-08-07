---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-02"

keywords: registry, firewall, custom firewall, network, network traffic

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I access {{site.data.keyword.registryshort_notm}} through a custom firewall?
{: #troubleshoot-firewall}
{: troubleshoot}
{: support}

Accessing {{site.data.keyword.registrylong}} fails when you have a custom firewall.
{: shortdesc}

You have a supplementary firewall in your development environment with custom settings for inbound and outbound network traffic. When you try to access {{site.data.keyword.registrylong_notm}}, the connection fails.
{: tsSymptoms}

Your custom firewall requires certain network groups to be open for inbound and outbound network traffic to allow communication to and from the registry.
{: tsCauses}

Allow your cluster to access infrastructure resources and services from behind a firewall, see [Allowing the cluster to access infrastructure resources and other services](/docs/containers?topic=containers-firewall#firewall_outbound).
{: tsResolve}

For INBOUND connectivity to your computer, allow incoming network traffic from the source network groups to the destination public IP address of your computer.

For OUTBOUND connectivity from your computer, use the same network groups and allow outgoing network traffic from the source public IP address of your computer to the network groups.
