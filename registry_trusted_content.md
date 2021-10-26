---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-26"

keywords: Docker Content Trust, keys, trusted content, signing, signing images, repository keys, trust, revoking trust, signing key, 

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Signing images for trusted content
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools.
{: shortdesc}

You can use either {{site.data.keyword.redhat_full}} Signatures or Docker Content Trust and Notary to sign your images.

 The Notary v1 service is deprecated. It is being removed from {{site.data.keyword.registrylong_notm}} on 31 August 2021. {{site.data.keyword.registrylong_notm}} supports the [Red Hat Signing](https://www.redhat.com/en/blog/container-image-signing){: external} model. For more information, see [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures](#registry_trustedcontent_red_hat_sig).
{: deprecated}

- [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures](#registry_trustedcontent_red_hat_sig)
- [Signing images for trusted content by using Docker Content Trust and Notary - deprecated](#registry_trustedcontent_dct_notary)

## Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures
{: #registry_trustedcontent_red_hat_sig}

You can use various tools to create [{{site.data.keyword.redhat_notm}} Signatures](https://www.redhat.com/en/blog/container-image-signing){: external} for your images. You can store your signed images for trusted content by using the {{site.data.keyword.redhat_notm}} Signatures extension API, which is supported by {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

You can use the following tools to create {{site.data.keyword.redhat_notm}} signatures:

- [Skopeo](#registry_trustedcontent_red_hat_sig_skopeo)
- [Podman](#registry_trustedcontent_red_hat_sig_podman)
- [OpenShift CLI](#registry_trustedcontent_red_hat_sig_oc)
- [Atomic](#registry_trustedcontent_red_hat_sig_atomic)

### Using skopeo to sign images
{: #registry_trustedcontent_red_hat_sig_skopeo}
{: help}
{: support}

To use [skopeo](https://github.com/containers/skopeo){: external} to sign your images, you must create a private [GNU Privacy Guard (GnuPG or GPG)](https://gnupg.org/){: external} identity and then run the `skopeo` command:

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

### Using atomic to sign images
{: #registry_trustedcontent_red_hat_sig_atomic}

See [Atomic CLI Reference](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/html/cli_reference/index){: external}.

## Signing images for trusted content by using Docker Content Trust and Notary - deprecated
{: #registry_trustedcontent_dct_notary}

To sign images for trusted content by using Docker Content Trust and Notary, you must have Docker version 18.03 or later. You can learn more by reviewing the [Docker Content Trust](https://docs.docker.com/engine/security/trust/content_trust/){: external} and the [Notary project](https://github.com/notaryproject/notary){: external} documentation.
{: shortdesc}

The Notary v1 service is deprecated. It is being removed from {{site.data.keyword.registrylong_notm}} on 31 August 2021. {{site.data.keyword.registrylong_notm}} supports the [Red Hat Signing](https://www.redhat.com/en/blog/container-image-signing){: external} model. For more information, see [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures](#registry_trustedcontent_red_hat_sig).
{: deprecated}

When you push your image with trusted content enabled, your Docker client also pushes a signed metadata object into the {{site.data.keyword.cloud_notm}} trust server. When you pull a tagged image when Docker Content Trust is enabled, your Docker client contacts the trust server to establish the latest signed version of the tag that you requested, verifies the content signature, and downloads the signed image.

An image name is made up of a repository and a tag. When you are using trusted content, each repository uses a unique signing key. Each tag within a repository uses the key that belongs to the repository. If you have multiple teams publishing content, each to their own repository within your {{site.data.keyword.registrylong_notm}} namespaces, each team can use their own keys to sign their content so that you can verify that each image is produced by the appropriate team.

A repository can contain both signed and unsigned content. If Docker Content Trust is enabled, you can access the signed content in a repository, even if other unsigned content is alongside it.

Images have separate signatures for old (`registry.bluemix.net`) and new (`icr.io`) domain names. Existing signatures work when the image is pulled from the old domain name. If you want to pull signed content from the new domain name, you must sign the image on the new domain name, `icr.io`, see [Signing an image for the new domain name](#trustedcontent_resign).
{: note}

Docker Content Trust uses a trust on first use (TOFU) security model. The repository key is pulled from the trust server when you pull a signed image from a repository for the first time. That key is used to verify images from that repository in the future. You must verify that you trust either the trust server or the image and its publisher before you pull the repository for the first time. If the trust information in the server is compromised and an image hasn't been pulled from the repository before, your Docker client might pull the compromised information from the trust server. If the trust data is compromised after you pull the image for the first time, on subsequent pulls, your Docker client fails to verify the compromised data and doesn't pull the image. For more information about how to inspect trust data for an image, see [Viewing signed images](#trustedcontent_viewsigned).

For more information about the TOFU security model, see [The Update Framework](https://theupdateframework.github.io/){: external}.

### Setting up your trusted content environment
{: #trustedcontent_setup}
{: help}
{: support}

By default, Docker Content Trust is disabled. Before you log in to {{site.data.keyword.registrylong_notm}} and start working with signed images, you must enable the Content Trust environment.
{: shortdesc}

1. Enable the Docker Content Trust environment variable by running one of the following commands.

    On Linux&reg; or macOS.

    ```sh
    export DOCKER_CONTENT_TRUST=1
    ```
    {: pre}

    On Windows&reg;.

    ```sh
    set DOCKER_CONTENT_TRUST=1
    ```
    {: pre}

2. Log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```sh
    ibmcloud login [--sso]
    ```
    {: pre}

    If you have a federated ID, use `ibmcloud login --sso` to log in. Enter your username and use the provided URL in your CLI output to retrieve your one-time passcode. If you have a federated ID, the login fails without the `--sso` and succeeds with the `--sso` option.
    {: tip}

3. Target the region that you want to use. If you don't know the region name, you can run the command without the region and choose one.

    ```sh
    ibmcloud cr region-set <region>
    ```
    {: pre}

4. Log in to {{site.data.keyword.registrylong_notm}}.

    ```sh
    ibmcloud cr login
    ```
    {: pre}

5. Export the environment variable command into your command line, where `<registry_DNS>` is your registry domain name. To find out about the available {{site.data.keyword.registrylong_notm}} domain names, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

    ```sh
    export DOCKER_CONTENT_TRUST_SERVER=https://<registry_DNS>:4443
    ```
    {: pre}

Now you are ready to push, pull, and manage trusted, signed images.

During your session with Docker Content Trust enabled, if you want to do an operation with trusted content disabled (such as to pull an unsigned image), use the `--disable-content-trust` option with the command.
{: tip}

### Pushing a signed image
{: #trustedcontent_push}
{: help}
{: support}

When you first push a signed image, Docker automatically creates a pair of signing keys (the root and repository keys). To sign an image in a repository where signed images have previously been pushed, you must load the correct signing key for the repository onto the computer that is pushing the image.
{: shortdesc}

Before you begin, [set up your registry namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).

1. [Set up your trusted content environment](#trustedcontent_setup).

2. [Push your image](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pushing). The tag is mandatory for trusted content. You see the following message:

    ```sh
    Signing and pushing image metadata.
    ```
    {: screen}

3. The first time that you push a signed image to a new repository, the command creates two signing keys, the root key and repository key, and stores them in your local computer. Enter and save secure passphrases for each key, and then [back up your keys](#trustedcontent_backupkeys). Backing up your keys is critical because your recovery options are limited, see [How do I recover lost or compromised keys?](/docs/Registry?topic=Registry-troubleshoot-recover-key)

    This action is only required the first time that you push a signed repository.
    {: tip}

### Pulling a signed image
{: #trustedcontent_pull}
{: help}
{: support}

The first time that you pull a signed image with Docker Content Trust enabled, your Docker client recognizes the signature as trusted. The Docker client pulls the most recent signed version of the image that you specify. Unsigned images or untrusted content is not pulled.
{: shortdesc}

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Pull your image. Replace `<source_image>` with the repository of the image and `<tag>` with the tag of the image that you want to use, such as `latest`. To list available images to pull, run `ibmcloud cr image-list`.

    ```sh
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Specify the tag when you push or pull a signed image. The `latest` tag defaults only when content trust is disabled.
    {: tip}

### Signing an image for the new domain name
{: #trustedcontent_resign}
{: help}
{: support}

To sign the image for the new domain name, `icr.io`, you must pull, tag, and push the image.
{: shortdesc}

1. Pull your signed image from the old domain name. Replace `<source_image>` with the repository of the image and `<tag>` with the tag of the image that you want to use, such as `latest`. To list available images to pull, run `ibmcloud cr image-list`.

    ```sh
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Specify the tag when you push or pull a signed image. The `latest` tag defaults only when content trust is disabled.
    {: tip}

2. Run the `docker tag` command for the new domain name. Replace `<old_domain_name>` with your old domain name, `<new_domain_name>` with your new domain name, `<repository>` with the name of your repository, and `<tag>` with the name of your tag.

    ```sh
    docker tag <old_domain_name>/<repository>:<tag> <new_domain_name>/<repository>:<tag>
    ```
    {: pre}

3. Push your image by using the new domain name, see [Push Docker images to your namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pushing). The tag is mandatory for trusted content. You see the following message:

    ```sh
    Signing and pushing image metadata.
    ```
    {: screen}

### Managing trusted content
{: #trustedcontent_managetrust}

By using `docker trust` commands, you can view who signed images and revoke trust content status. To run `docker trust` commands, you must have Docker 18.03 or later.
{: shortdesc}

#### Viewing signed images
{: #trustedcontent_viewsigned}
{: help}
{: support}

You can review signed versions of an image repository or tag, including information about the key ID and signer.
{: shortdesc}

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Review the tag, digest, and signer information for each image.

    (Optional) Specify the tag, `<tag>`, to see information about that version of the image.

    ```sh
    docker trust inspect --pretty <image>:<tag>
    ```
    {: pre}

#### Revoking trust
{: #trustedcontent_revoketrust}
{: help}
{: support}

You can revoke the trusted content status of an image.
{: shortdesc}

Before you begin, retrieve the repository key passphrase that you saved when you [first pushed the trusted repository](#trustedcontent_push). If you need to identify which key is used for the trusted image, use the `docker view` [command](#trustedcontent_viewsigned).

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Remove all trusted metadata for the image repository. Enter your repository key passphrase when prompted.

    (Optional) Specify a tag to revoke trusted metadata only for that version of the image.

    ```sh
    docker trust revoke <image>:<tag>
    ```
    {: pre}

3. Verify that trust was revoked in the list of trusted content.

    (Optional) If you want to verify revoked content for a tagged image, include the tag.

    ```sh
    docker trust inspect --pretty <image>:<tag>
    ```
    {: pre}

    You see the following message:

    ```sh
    No signatures or cannot access <image>:<tag>
    ```
    {: screen}

### Backing up signing keys
{: #trustedcontent_backupkeys}
{: help}
{: support}

When you first push a signed image to a new repository, Docker Content Trust creates two signing keys, the root and repository keys, and stores them in a directory on your local computer.

- On Linux&reg; and macOS `~/.docker/trust/private`

- On Windows&reg; `%HOMEPATH%\.docker\trust\private`

If you changed your Docker configuration directory, look for the `trust` subdirectory there.
{: tip}

You must back up all your keys, and especially the root key. If a key is lost or compromised, your recovery options are limited, see [How do I recover lost or compromised keys?](/docs/Registry?topic=Registry-troubleshoot-recover-key)

To back up your keys, see [Docker Content Trust documentation](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys){: external}.

### Managing trusted signers
{: #trustedcontent_signers}

You can add and remove signers from signing images in a repository.
{: shortdesc}

#### Adding signers to a trusted repository
{: #trustedcontent_addsigners}
{: help}
{: support}

To allow other users to sign images in a repository, add the signing keys for those users to that repository.
{: shortdesc}

Before you begin, complete the following tasks.

- Image signers must have permission to push images to the namespace.
- Repository owners and signers must have Docker 18.03 or later installed.
- Create a trusted content repository by [pushing a signed image](#trustedcontent_push). Repository owners must have the repository admin keys for the repository available in the Docker trust folder on their local computer. If you don't have the repository admin key, contact the owner to do this task for you.

When you add a signer, you can no longer use the repository admin key to sign images in that repository. You must hold the private key for one of the approved signers to sign. To retain the ability to sign images after you add a signer, follow these instructions again to generate and add a signer role for yourself.
{: tip}

To share signing keys, complete the following steps.

1. If the new signer doesn't have a key pair, a key pair must be generated and loaded.

    1. Generate the key. You can enter any name for `<NAME>`. The name that you select is visible when someone inspects trust on the repository. Work with the repository owner to meet any naming conventions that might be used by the organization and to select a name that is identifiable for that signer.

        ```sh
        docker trust key generate <NAME>
        ```
        {: pre}

    2. Enter a passphrase for the private key. A public key (`.pub`) is generated, and the corresponding private key is automatically loaded into the Docker trust configuration.

    3. The new signer must send the repository owner the public key.

2. The repository owner must add the signer's key to the repository.

    1. [Set up the trusted content environment](#trustedcontent_setup).

    2. Add the signer's key to the repository.

        ```sh
        docker trust signer add --key <NAME>.pub <NAME> <repository>
        ```
        {: pre}

3. The signer can set up their environment and sign an image.

    1. [Set up the trusted content environment](#trustedcontent_setup).

    2. The signer must sign an image. When prompted, enter the passphrase for the private key.

        ```sh
        docker trust sign <repository>:<tag>
        ```
        {: pre}

4. To verify that the signer was added, see [Viewing signed images](#trustedcontent_viewsigned).

#### Removing a signer from a repository
{: #trustedcontent_removesigner}
{: help}
{: support}

If you no longer want a signer to be able to sign images in your repository, you can remove them as a signer.
{: shortdesc}

Before you begin, repository owners and signers must have Docker 18.03 or later installed.

If you remove a signer, the trust server does not trust their signed versions of the image. To ensure that the image can be pulled after the signer is removed, make sure that the most recent version of the image isn't signed by the signer that you're removing. If the most recent version of the image is signed by the signer that you're removing, push an update to the image and sign it by using your key before you continue.
{: tip}

To remove a signer, complete the following steps.

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Remove the signer by running the following command.

    ```sh
    docker trust signer remove <NAME> <repository>
    ```
    {: pre}

3. To verify that the signer was removed, view the trust data for the image and verify that the signer is no longer listed. For more information about viewing trust data, see [Viewing signed images](#trustedcontent_viewsigned).


