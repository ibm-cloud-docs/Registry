---

copyright:
  years: 2017, 2023
lastupdated: "2023-09-13"

keywords: Docker, trusted content, signing, signing images, repository keys, trust, revoking trust, signing key, skopeo, podman, Red Hat signatures, sign images, images, signatures, cli

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Signing images for trusted content
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace.
{: shortdesc}

By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools.

You can use {{site.data.keyword.redhat_full}} signatures to sign your images.

## Signing images by using {{site.data.keyword.redhat_notm}} signatures
{: #registry_trustedcontent_red_hat_sig}

You can use various tools to create [{{site.data.keyword.redhat_notm}} signatures](https://www.redhat.com/en/blog/container-image-signing){: external} for your images. You can store your signed images for trusted content by using the {{site.data.keyword.redhat_notm}} signatures extension API, which is supported by {{site.data.keyword.registrylong_notm}}.

You can use the following tools to create {{site.data.keyword.redhat_notm}} signatures:

- [Skopeo](#registry_trustedcontent_red_hat_sig_skopeo)
- [Podman](#registry_trustedcontent_red_hat_sig_podman)
- [{{site.data.keyword.redhat_openshift_notm}} CLI](#registry_trustedcontent_red_hat_sig_oc)

### Using Skopeo to sign images
{: #registry_trustedcontent_red_hat_sig_skopeo}
{: help}
{: support}

To use [Skopeo](https://github.com/containers/skopeo){: external} to sign your images, you must create a private [GNU Privacy Guard (GnuPG or GPG)](https://gnupg.org/){: external} identity and then run the `skopeo` command.

The following example doesn't include Skopeo authentication.
{: note}

1. To create a GnuPG identity, run the following command.

    ```txt
    gpg --generate-key
    ```
    {: pre}

2. Push and sign the image at the same time by using the GnuPG identity to sign the image. Where `<your_email>` is the email address that you used to sign up for GnuPG, `<repository:tag>` is your repository and tag, and `<image>` is the name of your image in the format `<region><namespace><repository:tag>`, where `<region>` is the name of your region and `<namespace>` is the name of your namespace.

    To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`. If the list images command times out, see [Why is it timing out when I list images?](/docs/Registry?topic=Registry-troubleshoot-image-timeout) for assistance.
    {: tip}

    ```txt
    skopeo --insecure-policy copy --sign-by <your_email> docker-daemon:<repository:tag> docker://<image>
    ```
    {: pre}

    For example, where `user@email.com` is your GnuPG email address, `bluebird:build1` is your repository and tag, and `us.icr.io/birds/bluebird:build1` is the name of your image.

    ```txt
    skopeo --insecure-policy copy --sign-by user@email.com docker-daemon:bluebird:build1 docker://us.icr.io/birds/bluebird:build1
    ```
    {: pre}

    [macOS]{: tag-macos} On macOS, if you get the error `Error copying image to the remote destination: Error writing signatures: mkdir /var/lib/containers/sigstore: permission denied`, override the internal default for registry configuration so that the correct signature storage is used by running the command with the `--registries.d` option.
    {: tip}

    ```txt
    skopeo --registries.d . --insecure-policy copy --sign-by user@email.com docker-daemon:us.icr.io/birds/bluebird:build1 docker://us.icr.io/birds/bluebird:build1
    ```
    {: pre}

[Linux]{: tag-linux} [macOS]{: tag-macos} On Linux&reg; and macOS, the default configuration for the tools is to store the signatures locally. Storing signatures locally can lead to signature verification failure because the signature is not in the registry. To fix this problem, you can modify or delete the configuration file. On Linux&reg;, the configuration is saved in `/etc/containers/registries.d/default.yaml`. On macOS, the configuration file is saved in `/usr/local/etc/containers/registries.d/default.yaml`. On macOS, when Skopeo is installed by using the [Homebrew](https://brew.sh/){: external} package manager, the configuration file might be at `/opt/homebrew/Cellar/etc/containers/registries.d/default.yaml` for Apple silicon, or `/usr/local/Cellar/etc/containers/registries.d/default.yaml` for Intel.
{: tip}

### Using Podman to sign images
{: #registry_trustedcontent_red_hat_sig_podman}

You can use Podman to sign images. For more information, see [Podman](https://podman.io/){: external}.

### Signing images by using the {{site.data.keyword.redhat_openshift_notm}} CLI
{: #registry_trustedcontent_red_hat_sig_oc}

You can sign your images by using the {{site.data.keyword.redhat_openshift_notm}} CLI. For more information, see [{{site.data.keyword.redhat_openshift_notm}} CLI](https://docs.openshift.com/container-platform/3.11/admin_guide/image_signatures.html){: external}. The {{site.data.keyword.redhat_openshift_full}} CLI uses the `oc` command.
