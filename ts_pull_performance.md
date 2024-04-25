---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-25"

keywords: registry, slow, performance, image, pull

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is pulling images in {{site.data.keyword.registryshort_notm}} slow?
{: #troubleshoot-pull-performance}
{: troubleshoot}
{: support}

Pulling an image is slow from {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to pull an image, it takes a long time.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- **Scenario A.** You're using a large image.
- **Scenario B.** You're pulling your image over a long distance.
- **Scenario C.** You have a poor connection.

You can fix this problem in the following ways:
{: tsResolve}

- **Scenario A.** Reduce the size of your image.
- **Scenario B.** Store and pull your images in the same location.
- **Scenario C.** If you're using {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.redhat_openshift_full}} Container Platform, you can pull images over the private network to get a faster speed.
