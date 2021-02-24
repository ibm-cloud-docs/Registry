---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-24"

keywords: troubleshooting, support, help, errors, problems, ts, registry, firewall, custom firewall

subcollection: Registry

content-type: troubleshoot

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
{:troubleshoot: data-hd-content-type='troubleshoot'}

# Why can't I access the registry through a custom firewall?
{: #troubleshoot-firewall}
{: troubleshoot}
{: support}

Accessing {{site.data.keyword.registrylong}} fails when you have a custom firewall.
{: shortdesc}

{: tsSymptoms}
You set up an extra firewall in your development environment with custom settings for inbound and outbound network traffic. When you try to access {{site.data.keyword.registrylong_notm}}, the connection fails.

{: tsCauses}
Your custom firewall requires certain network groups to be opened for inbound and outbound network traffic to allow communication to and from the registry.

{: tsResolve}
Allow your cluster to access infrastructure resources and services from behind a firewall, see [Allowing the cluster to access infrastructure resources and other services](/docs/containers?topic=containers-firewall#firewall_outbound).

For INBOUND connectivity to your computer, allow incoming network traffic from the source network groups to the destination public IP address of your computer.

For OUTBOUND connectivity from your computer, use the same network groups and allow outgoing network traffic from the source public IP address of your computer to the network groups.
