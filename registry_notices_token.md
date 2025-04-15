---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, registry tokens,

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Registry token creation is discontinued from 1 July 2019
{: #registry_notices_token}

To facilitate the migration to IAM and the new `icr.io` domains, {{site.data.keyword.registrylong}} will not allow the creation of registry tokens from 1 July 2019.
{: shortdesc}

The original announcement was published on 12 June 2019.
{: note}

Recently, the new [{{site.data.keyword.registryshort}}](https://www.ibm.com/products/container-registry){: external} `icr.io` domain names were introduced. With this change, it was announced that an IAM API key, rather than a registry token, needs to be stored in an image pull secret so that you can pull images from the new registry domains. In accordance with this change, and to facilitate migration to the new domains, the creation of registry tokens is discontinued on 1 July 2019.

New clusters are deployed that have both pull secrets that access `bluemix.net` domains with a registry token and pull secrets that access `icr.io` domains with an IAM API key. Moving forward, all new clusters will be deployed with IAM API key pull secrets only, and you are unable to create new registry tokens with `ibmcloud cr token-add`. These changes mean that new clusters must pull images from the `icr.io` domains. Registry tokens are deprecated and anyone with questions about registry tokens must consult IAM.

## What you need to know about this change
{: #registry_notices_token_affect}

Existing registry tokens continue to provide access to {{site.data.keyword.registryshort}} by using the deprecated `bluemix.net` domain names. You can continue to use existing registry tokens to access these domains without interruption.

However, the old domains and registry tokens will be discontinued as well. To prepare yourself for this event, set up your clusters to pull images from the `icr.io` domains. This action has two effects. You migrate away from the deprecated `bluemix.net` domains while simultaneously migrating from registry tokens to IAM API keys.

## How you benefit from this change
{: #registry_notices_token_benefit}

With IAM API keys, you can add IAM policies for more fine-grained control over access. For example, you can create IAM access policies to restrict permissions to specific registry namespaces so that a cluster can pull images from those namespaces only.
