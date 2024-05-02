---

copyright:
  years: 2023, 2024
lastupdated: "2024-05-02"

keywords: error, cosign, Podman, pulling, image

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why have I got a problem pulling an image with `cosign` when I use Podman in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-cosign-podman}
{: troubleshoot}
{: support}

You're having problems when you try to pull an image when you're using [`cosign`](https://github.com/sigstore/cosign){: external} with [Podman](https://podman.io/){: external} in {{site.data.keyword.registrylong}}.
{: shortdesc}

You are getting the following error when you try to pull an image and you're using `cosign` with Podman: `UNAUTHORIZED: Authorization required.`
{: tsSymptoms}

You might need to log in to `cosign` manually.
{: tsCauses}

You can fix this problem in the following way:
{: tsResolve}

Use the following command to log in to `cosign`, where `<registry>` is your registry and `<your_api_key>` is your API key.

```txt
cosign login <registry> -u iamapikey -p <your_api_key>
```
{: pre}
