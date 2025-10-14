---

copyright:
  years: 2024, 2025
lastupdated: "2025-10-14"

keywords: IBM Cloud Container Registry notices, notices, IBM Bluemix Container Registry, available, ga

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort_notm}} is available from 27 June 2017
{: #registry_notices_ibcr}

The registry has been a part of {{site.data.keyword.containerlong_notm}} since its inception in June 2015. {{site.data.keyword.IBM_notm}} announced that the {{site.data.keyword.registrylong}} is live as a separate offering within the {{site.data.keyword.cloud_notm}} platform.
{: shortdesc}

The original announcement was published on 28 June 2017.
{: note}

The registry is your location to safely store and share [Docker](https://docs.docker.com/reference/cli/docker/){: external} images in a multi-tenant, highly available, and scalable private image registry that is hosted and managed by {{site.data.keyword.IBM_notm}}. [Get started](/docs/Registry?topic=Registry-getting-started) by setting up your own image namespace and push Docker images to your namespace.

By using {{site.data.keyword.registrylong_notm}}, you can also take advantage of the capabilities that are provided by Vulnerability Advisor. Vulnerability Advisor introspects every layer in each image before a live container is instantiated from an image, which ensures security insight to your environment.

Each {{site.data.keyword.cloud_notm}} account has a free tier so that you can store 500 MB of private Docker images without charge. After that tier, you pay a flat rate for each GB to store images and use Vulnerability Advisor capabilities. Inbound traffic, as a result of pushing images to your registry, is free. Outbound traffic from the registry is free up to 5 GB per month and then it is a rate for each GB. Existing users of the registry have 30 days to migrate to the new service plan. After 30 days, users are automatically migrated. Users who use more than 500 MB of storage cannot push more images to the registry without upgrading to a paid plan or removing existing images first.
