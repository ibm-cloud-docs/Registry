---

copyright:
  years: 2023
lastupdated: "2023-02-07"

keywords: registry, slow, performance, image, pull

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is pulling images slow?
{: #troubleshoot-pull-performance}
{: troubleshoot}
{: support}

Pulling an image is slow from {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to pull an image, it takes a long time.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- You are using a large image.
- You are pulling your image over a long distance.
- You have a poor connection.

You can fix this problem in the following ways:
{: tsResolve}

- Make your image smaller.
- Store and pull your images in the same location.
- If you're using {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.redhat_openshift_full}} Container Platform, you can pull images over the private network to get a faster speed.
