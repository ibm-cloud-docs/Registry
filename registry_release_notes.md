---

copyright:
  years: 2019
lastupdated: "2019-02-12"

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

# Release notes for {{site.data.keyword.registrylong_notm}}
{: #registry_release_notes}

The following features and changes to the {{site.data.keyword.registrylong}} service are available.

## 21 February 2019
{: 21February2019}

- **New DNS names**
  {{site.data.keyword.registrylong_notm}} is adopting new domain names to align with the rebranding of {{site.data.keyword.cloud_notm}} for a better user experience.
  
  The new domain names are available in the console and the CLI from `<DATE>`. You can use the new `icr.io` domain names now. The existing `bluemix.net` domain names are deprecated, but you can continue to use them for the time being, an end of support date will be announced later.
  [For more information, see Regions)](/docs/services/Registry/registry_overview.html#registry_regions).
- **User access**
  Because the new `icr.io` domains are authorized by using an IAM API key, if you want more control over access to your {{site.data.keyword.registrylong_notm}} resources, you can add IAM policies. For example, you can change the API key policies in the cluster's pull secret so that images are pulled from a certain registry region or namespace only. For more information, see (default pull secrets link).
  
