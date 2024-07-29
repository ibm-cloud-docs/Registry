---

copyright:
  years: 2024
lastupdated: "2024-07-29"

keywords: IBM Cloud Container Registry notices, notices, DCT, docker content trust, Notary v1, signing images, Red Hat signing

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using Notary v1 for signing images in {{site.data.keyword.registryshort}} is deprecated from 8 July 2021
{: #registry_notices_notaryv1}

The Notary v1 service is being deprecated immediately and it is being removed from {{site.data.keyword.registrylong}} on 31 August 2021.
{: shortdesc}

[Notary v1](https://github.com/notaryproject/notary){: external} is the server side of [Docker Content Trust (DCT)](https://docs.docker.com/engine/security/trust/){: external}. DCT did not have widespread adoption in the community or in the {{site.data.keyword.registrylong_notm}} customer base.

As an alternative approach, {{site.data.keyword.registrylong_notm}} supports the [{{site.data.keyword.redhat_notm}} container image signing](https://www.redhat.com/en/blog/container-image-signing){: external} model, see [Signing images by using {{site.data.keyword.redhat_notm}} signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig) for implementation details.

## Original announcement
{: #registry_notices_notaryv1_announce}

The original announcement was published on 8 July 2021.
