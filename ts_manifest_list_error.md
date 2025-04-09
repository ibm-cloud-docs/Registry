---

copyright:
  years: 2021, 2025
lastupdated: "2025-04-09"

keywords: error, registry, tag, manifest list, oci image index, manifest, manifest list invalid error, image, repository, CRI0304E

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get a manifest list invalid error in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-manifest-list-error}
{: troubleshoot}
{: support}

When you try to tag your manifest list or OCI Image Index in {{site.data.keyword.registrylong}}, you get a manifest list invalid error.`CRI0304E The manifest list or OCI index that you are tagging references an image that doesn't exist`
{: shortdesc}

You get the following manifest list invalid error when you try to [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) your [manifest](/docs/Registry?topic=Registry-registry_overview#overview_elements_manifest) list or OCI Image Index in {{site.data.keyword.registrylong_notm}}: `CRI0304E The manifest list or OCI index that you are tagging references an image that doesn't exist, see https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-manifest-list-error`.
{: tsSymptoms}

Manifest lists and OCI Image Indexes contain a list of references to different images, where each image is for a different architecture. When you tag a manifest list or OCI Image Index, {{site.data.keyword.registryshort}} tries to copy the referenced images. When you get this error message, it indicates that one of those referenced images was not found in the registry.
{: tsCauses}

To understand how to fix this issue, you must work out what images are referenced in the manifest list or OCI Image Index by running the following command, where `SOURCE_IMAGE` is your source image name:
{: tsResolve}

```txt
ibmcloud cr manifest-inspect SOURCE_IMAGE
```
{: pre}

The output of which is similar to this output:

```txt
{
    "schemaVersion": 2,
    "mediaType": "application/vnd.docker.distribution.manifest.list.v2+json",
    "manifests": [
        {
            "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
            "size": 528,
            "digest": "sha256:865b0c35e6da393b8e80b7e3799f777572399a4cff047eb02a81fa6e7a48ed4b",
            "platform": {
                "architecture": "amd64",
                "os": "linux"
            }
        },
        {
            "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
            "size": 538,
            "digest": "sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc",
            "platform": {
                "architecture": "ppc64le",
                "os": "linux"
            }
        }
    ]
}
```
{: screen}

For this output to be valid, the images, with the [digests](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) from the previous output, must exist in the same repository as the manifest list or OCI index that you are trying to tag. To confirm whether one of the images is missing, you can run the following command. Replace `<src_repo>` with the name of your namespace and repository in the format `mynamespace/myrepo`.

```txt
ibmcloud cr digests --restrict <src_repo>
```
{: pre}

For example, if you run the following command:

```txt
ibmcloud cr  digests --restrict mynamespace/myrepo
```
{: pre}

You get the following response:

```txt
Listing images...

Repository                  Digest                                                                    Tags   Type                                 Created       Size     Security status
icr.io/mynamespace/myrepo   sha256:865b0c35e6da393b8e80b7e3799f777572399a4cff047eb02a81fa6e7a48ed4b   -      Docker Image Manifest V2, Schema 2   4 days ago    1.8 MB   -
icr.io/mynamespace/myrepo   sha256:a08e18417cec86f570be496b8bde1350dd986fc354d091b44d6a536570c26193   list   Docker Manifest List                 -             433 B    -

OK
```
{: screen}

In the previous example, you can see that only one image is in the same repository as the manifest list `sha256:865b0c35e6da393b8e80b7e3799f777572399a4cff047eb02a81fa6e7a48ed4b` and therefore, the manifest list is referencing another image `sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc` that does not currently exist in the repository.

You can resolve this issue by using one of the following options, following on from the previous example.

- If the missing image exists elsewhere in the registry, you can use the [`ibmcloud cr image-tag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_tag) command to move the image to the same repository.

    1. To detect if the missing digest exists elsewhere in the registry, run the following command.

        ```txt
        ibmcloud cr digests --format '{{if eq .Digest "sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc"}}{{.Repository}}@{{.Digest}}{{end}}'
        icr.io/myrepo2/image2@sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc
        ```
        {: pre}

    2. If the previous command returns an image, you can copy it to the same repository as the manifest list.

        ```txt
        ibmcloud cr image-tag icr.io/mynamespace/myrepo2@sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc icr.io/mynamespace/myrepo:ppc64le
        ```
        {: pre}

- If the missing image was deleted in the last 30 days, you can restore it from the trash.

    1. Detect if the image exists in trash by running the following command.

        ```txt
        ibmcloud cr trash-list --restrict mynamespace
        ```
        {: pre}

        You receive the following response:

        ```txt
        Listing the contents of the trash...

        Digest                                                                                              Days until expiry   Tags
        icr.io/mynamespace/myrepo@sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc   30                  ppc64le


        OK
        ```
        {: screen}

    2. If the image does exist in trash, you can restore it by running the following command.

        ```txt
        ibmcloud cr image-restore icr.io/mynamespacemyrepo@sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc
        ```
        {: pre}

        You receive the following response:

        ```txt
        Restoring digest 'icr.io/mynamespace/myrepo@sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc' ...

        Successfully restored digest 'icr.io/mynamespace/myrepo@sha256:1d71e323557502cc78ee6c237331a09b0c33ba59c14e5f683da3b1c6218779cc'
        Successfully restored tags: ppc64le

        OK
        ```
        {: screen}

- If you have a local copy of the image, you can push it back to the registry. For more information, see [Pushing Docker images to your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_pushing_namespace).
