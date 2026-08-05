---

copyright:
  years: 2023, 2026
lastupdated: "2026-08-04"

keywords: registry, slow, performance, image, pull

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting slow image pulls in IBM Cloud registry
{: #troubleshoot-pull-performance}
{: troubleshoot}
{: support}

Pulling an image is slow from {{site.data.keyword.registrylong}}.
{: shortdesc}

When you try to pull an image, it takes a long time.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- **Scenario A.** You are using a large image.
- **Scenario B.** You are pulling your image over a long distance.
- **Scenario C.** You have a poor connection.

You can fix this problem in the following ways:
{: tsResolve}

- **Scenario A.** Reduce the size of your image.
- **Scenario B.** Store and pull your images in the same location.
- **Scenario C.** If you are using {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.redhat_openshift_full}} Container Platform, you can pull images over the private network to get a faster speed.
