---

copyright:
  years: 2024
lastupdated: "2024-10-09"

keywords: IBM Cloud Container Registry notices, domain names, notices

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Introducing new {{site.data.keyword.registryshort}} domain names from 25 February 2019
{: #registry_notices_domain_names}

From 25 February 2019, {{site.data.keyword.registrylong}} is adopting new domain names to align with the rebranding of {{site.data.keyword.cloud_notm}} for a better user experience.

You can now use IAM policies for more control over access to your registry resources. The new domain names are shown by location in the following table:

| Existing domain name | New domain name |
|----------------------|-----------------|
| `registry.ng.bluemix.net` | `us.icr.io` |
| `registry.eu-gb.bluemix.net` | `uk.icr.io` |
| `registry.eu-de.bluemix.net` | `de.icr.io` |
| `registry.au-syd.bluemix.net` | `au.icr.io` |
| `registry.bluemix.net` | `icr.io` |
| Not applicable | `jp.icr.io` |
{: caption="New domain names" caption-side="bottom"}
{: #table_registry_domain_names_new}

The new domain names are available in the console and the CLI beginning 25 February 2019. You can use the new `icr.io` domain names now. The existing `bluemix.net` domain names are deprecated, but you can continue to use them. An end of support date is not available yet.

## What you need to know about this change
{: #registry_notices_domain_names_know}

This change affects containers that run images from {{site.data.keyword.registryshort}}. To pull {{site.data.keyword.registryshort}} images for your deployments in [{{site.data.keyword.containerlong_notm}}](https://www.ibm.com/products/kubernetes-service){: external} clusters, your clusters must be authorized to pull from the domain name that the image uses:

- Existing clusters have pull secrets that use a registry token to authorize access to images from the `bluemix.net` domain name for the global registry and the regional registry from the region that the cluster is in. To pull images from the new `icr.io` domain name, you must act now.
- New clusters have pull secrets for both registry token access to `bluemix.net` domains as well as IAM API keys for access to `icr.io` domains. By default, you can pull images from the new `icr.io` domain in any registry region.

## How you benefit from this change
{: #registry_notices_domain_names_benefit}

This new method uses an API key to authorize pulling images from the registry. Because the new `icr.io` domains are authorized by using an IAM API key, you can add IAM policies if you want more control over access. For example, you can change the API key policies in the cluster’s pull secret to pull images from only a certain registry region or namespace.

## Original announcement
{: #registry_notices_domain_names_announce}

The original announcement that this notification mirrors is [Introducing New {{site.data.keyword.registrylong_notm}} Domain Names](https://www.ibm.com/blog/announcement/introducing-new-ibm-cloud-container-registry-domain-names/){: external} and it was published on 25 February 2019.
