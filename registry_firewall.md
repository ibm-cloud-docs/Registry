---

copyright:
  years: 2024
lastupdated: "2024-05-29"

keywords: IBM Cloud Container Registry, firewall, access, communicate, domains, subdomains, traffic, allowlist

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Accessing {{site.data.keyword.registryshort}} through a firewall
{: #registry_firewall}

To permit worker nodes to communicate with {{site.data.keyword.registrylong}}, allow outgoing network traffic from the worker nodes to {{site.data.keyword.registrylong_notm}} [regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).
{: shortdesc}

If you are using {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong}}, by default the connection to {{site.data.keyword.registryshort}} is private. Therefore, you don't need to allow public access to {{site.data.keyword.registryshort}}. For more information about private connectivity, see [Private network connection to `icr.io` registries](/docs/containers?topic=containers-registry#cluster_registry_auth_private).
{: note}

You can configure your firewall to allow connections to {{site.data.keyword.registryshort}} by using a [Layer 7 firewall](https://nordlayer.com/learn/firewall/layer-7/){: external} with the domains listed in the following table.

When you access {{site.data.keyword.registrylong_notm}} over the public internet, you must not have any allowlist restrictions that are based on IP addresses in place. If you have any concerns about opening your allowlist, you can configure private access to {{site.data.keyword.registrylong_notm}} by using the private {{site.data.keyword.cloud_notm}} network, see [Securing your connection to Container Registry](/docs/Registry?topic=Registry-registry_private). Note that IP address lists are not provided because they can change frequently.
{: important}

In addition to the following regional subdomains, you must also allow traffic from your worker nodes to port `443` on all subdomains of `icr.io` in case of redirection to other subdomains for delivery optimization. You must allow `TCP port 443 FROM <each_worker_node_publicIP> TO *.icr.io`, where `<each_worker_node_publicIP>` is the public IP address for each worker node. If you use the deprecated domain names, you must allow those domains too.

| Region | Registry address  |
|---------------|-------------|
| Global | `icr.io` Deprecated: `registry.bluemix.net` |
| AP North | `jp.icr.io` |
| AP South | `au.icr.io` Deprecated: `registry.au-syd.bluemix.net` |
| EU Central | `de.icr.io` Deprecated: `registry.eu-de.bluemix.net` |
| Madrid | `es.icr.io` |
| Osaka | `jp2.icr.io` |
| Sao Paolo | `br.icr.io` |
| Toronto | `ca.icr.io` |
| UK South | `uk.icr.io` Deprecated: `registry.eu-gb.bluemix.net` |
| US South | `us.icr.io` Deprecated: `registry.ng.bluemix.net` |
{: caption="Table 1. Addresses for {{site.data.keyword.registryshort}} traffic" caption-side="bottom"}
{: #table_registry_traffic_addresses}
