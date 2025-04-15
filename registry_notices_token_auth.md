---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, registry tokens, authentication

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort}} discontinues registry tokens for authentication on 19 August 2021
{: #registry_notices_token_auth}

From 19 August 2021, any {{site.data.keyword.registrylong}} pulls that use registry tokens stop working, including pulls from [{{site.data.keyword.containerlong_notm}}](https://www.ibm.com/products/kubernetes-service){: external} and [{{site.data.keyword.openshiftlong}}](https://www.ibm.com/products/openshift){: external}. Any {{site.data.keyword.registryshort}} pushes that use registry tokens from CI pipelines also stop working.
{: shortdesc}

The original announcement was published on 28 May 2021.
{: note}

The [discontinuation of registry tokens as an authentication mechanism](/docs/Registry?topic=Registry-registry_notices_token) for {{site.data.keyword.registrylong_notm}} was announced in June 2019 as {{site.data.keyword.registryshort}} moved to a more secure IAM API key approach. This announcement is also aligned to the `icr.io` domain name changes. A further announcement was issued in February 2020 about [{{site.data.keyword.registryshort}} not accepting registry tokens for authentication](/docs/Registry?topic=Registry-registry_notices_uaa_token).

## What actions you must take by 19 August 2021
{: #registry_notices_token_auth_action}

You must automate access to your {{site.data.keyword.registryshort}} namespaces so that you can push and pull images by using {{site.data.keyword.iamlong}} (IAM) by 19 August 2021.

## Learn more
{: #registry_notices_token_auth_learn}

For more information about how to automate access to your {{site.data.keyword.registryshort}} namespaces see the following topics.

- [Automating access by using IAM](/docs/Registry?topic=Registry-registry_access)
- [{{site.data.keyword.containerlong_notm}} and {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-registry)
- [{{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#openshift_iccr)

## Original announcement
{: #registry_notices_token_auth_announce}

The original announcement was published on 28 May 2021.
