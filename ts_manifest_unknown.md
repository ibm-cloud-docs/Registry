---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-25"

keywords: error, registry, manifest unknown, manifest, manifest unknown error

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get a manifest unknown error in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-manifest-unknown}
{: troubleshoot}
{: support}

You get a `manifest unknown` error when you try to pull an image in {{site.data.keyword.registrylong}}.
{: shortdesc}

You're trying to pull an image, but you receive the following manifest error message: `manifest unknown`
{: tsSymptoms}

The manifest does not exist in the registry.
{: tsCauses}

To resolve the problem, try the following options:
{: tsResolve}

- Check that the image name is correct.
- Check that you're pointing at the correct {{site.data.keyword.registryshort}} region by running the [`ibmcloud cr region`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region) command.
