---

copyright:
  years: 2017, 2021
lastupdated: "2021-11-25"

keywords: Docker Content Trust, keys, trusted content, signing, signing images, repository keys, trust, revoking trust, signing key, 

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Signing images for trusted content
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools.
{: shortdesc}

You can use {{site.data.keyword.redhat_full}} Signatures to sign your images.

The Notary v1 service for signing images in {{site.data.keyword.registrylong_notm}} is discontinued from 1 November 2021.

## Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures
{: #registry_trustedcontent_red_hat_sig}

You can use various tools to create [{{site.data.keyword.redhat_notm}} Signatures](https://www.redhat.com/en/blog/container-image-signing){: external} for your images. You can store your signed images for trusted content by using the {{site.data.keyword.redhat_notm}} Signatures extension API, which is supported by {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

You can use the following tools to create {{site.data.keyword.redhat_notm}} signatures:

- [Skopeo](#registry_trustedcontent_red_hat_sig_skopeo)
- [Podman](#registry_trustedcontent_red_hat_sig_podman)
- [OpenShift CLI](#registry_trustedcontent_red_hat_sig_oc)

### Using Skopeo to sign images
{: #registry_trustedcontent_red_hat_sig_skopeo}
{: help}
{: support}

To use [Skopeo](https://github.com/containers/skopeo){: external} to sign your images, you must create a private [GNU Privacy Guard (GnuPG or GPG)](https://gnupg.org/){: external} identity and then run the `skopeo` command:

1. To create a GnuPG identity, run the following command.

    ```sh
    gpg --generate-key
    ```
    {: pre}

2. Push and sign the image at the same time by using the GnuPG identity to sign the image. Where `<your_email>` is the email address that you used to sign up for GnuPG, `<repository:tag>` is your repository and tag, and `<image>` is the name of your image in the format `<region><namespace><repository:tag>`, where `<region>` is the name of your region and `<namespace>` is the name of your namespace.

    ```sh
    skopeo --insecure-policy copy --sign-by <your_email> docker-daemon:<repository:tag> docker://<image>
    ```
    {: pre}

    For example, where `user@email.com` is your GnuPG email address, `bluebird:build1` is your repository and tag, and `us.icr.io/birds/bluebird:build1` is the name of your image.

    ```sh
    skopeo --insecure-policy copy --sign-by user@email.com docker-daemon:bluebird:build1 docker://us.icr.io/birds/bluebird:build1
    ```
    {: pre}

    On macOS, if you get the error `“FATA[0015] Error writing signatures: mkdir /var/lib/atomic: permission denied”`, override the internal default for registry configuration so that the correct signature storage is used by running the command with the  `--registries.d` option.

    ```sh
    skopeo --registries.d . --insecure-policy copy --sign-by user@email.com docker-daemon:us.icr.io/birds/bluebird:build1 docker://us.icr.io/birds/bluebird:build1
    ```
    {: pre}

On Linux&reg; and macOS, the default configuration for the tools is to store the signatures locally. Storing signatures locally can lead to signature verification failure because the signature is not in the registry. To fix this problem, you can modify or delete the configuration file. On Linux&reg;, the configuration is saved in `/etc/containers/registries.d/default.yaml`. On macOS, the configuration file is saved in `/usr/local/etc/containers/registries.d/default.yaml`.
{: tip}

### Using Podman to sign images
{: #registry_trustedcontent_red_hat_sig_podman}

See [Podman](https://podman.io/){: external}.

### Using OpenShift CLI to sign images
{: #registry_trustedcontent_red_hat_sig_oc}

See [OpenShift CLI](https://docs.openshift.com/container-platform/3.11/admin_guide/image_signatures.html){: external}. The OpenShift CLI uses the `oc` command.


