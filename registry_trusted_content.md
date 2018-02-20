---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Signing images for trusted content
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tooling. To use this feature, you must have Docker version 1.11 or later. You can learn more by reviewing the [Docker Content Trust](https://docs.docker.com/engine/security/trust/content_trust/) and [the Notary project](https://github.com/theupdateframework/notary) documentation.
{:shortdesc}

When you push your image with trusted content enabled, your Docker client also pushes a signed metadata object into the {{site.data.keyword.Bluemix_notm}} trust server. When pulling a tagged image with Docker Content Trust enabled, your Docker client contacts the trust server to establish the latest signed version of the tag that you requested, verifies the content signature, and downloads the signed image.

An image name is made up of a repository and a tag. When using trusted content, each repository uses a unique signing key. Each tag within a repository uses the key that belongs to the repository. If you have multiple teams publishing content, each to their own repository within your {{site.data.keyword.registrylong_notm}} namespaces, each team can use their own keys to sign their content, so that you can verify that each image is produced by the appropriate team.

A repository can contain both signed and unsigned content. If you push an update to a tag while trusted content is disabled and then pull it with trusted content enabled, Docker Content Trust uses a "trust on first use" model. The repository key is pulled from the trust server as well as the signed metadata the first time that you pull a repository. To ensure the security of your repository, ensure that you trust the signature of an image before you pull a signed image.

## Setting up your trusted content environment
{: #trustedcontent_setup}

By default, Docker Content Trust is disabled. Enable the Content Trust environment before logging in to {{site.data.keyword.registrylong_notm}} and working with signed images.
{:shortdesc}

1.  Enable the Docker Content Trust environment variable in your terminal.

    For Linux or Mac:

    ```
    export DOCKER_CONTENT_TRUST=1
    ```
    {: codeblock}

    For Windows:

    ```
    set DOCKER_CONTENT_TRUST=1
    ```
    {: codeblock}

2.  Log in to the {{site.data.keyword.Bluemix_notm}} CLI.

    ```
    bx login [--sso]
    ```
    {: pre}

    **Note:** If you have a federated ID, use `bx login --sso` to log in. Enter your user name and use the provided URL in your CLI output to retrieve your one-time passcode. You know you have a federated ID when the login fails without the `--sso` and succeeds with the `--sso` option.

3.  Target the region that you want to use. If you don't know the region name, you can run the command without the region and choose one.

    ```
    bx cr region-set <region>
    ```
    {: pre}

4.  Log in to {{site.data.keyword.registrylong_notm}}.

    ```
    bx cr login
    ```
    {: pre}

    The output instructs you to export the Docker Content Trust environment variable. For example:

    ```
    user:~ user$ bx cr login
    Logging in to 'registry.ng.bluemix.net'...
    Logged in to 'registry.ng.bluemix.net'.

    To set up your Docker client with content trust, export the following environment variable:
    export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
    {: screen}

5.  Copy and paste the environment variable command in your terminal. For example:

    ```
    export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
    {: pre}


Now you are ready to push, pull, and manage trusted, signed images.

During your session with Docker Content Trust enabled, if you want to perform an operation with trusted content disabled (such as to pull an unsigned image), use the `--disable-content-trust` flag with the command.
{: tip}

## Pushing a signed image
{: #trustedcontent_push}

When you first push a signed image, Docker automatically creates a pair of signing keys: root and repository. To sign an image in a repository where signed images have been pushed before, you must have the correct repository signing key loaded on the machine that is pushing the image.
{:shortdesc}

Before you begin, [set up your registry namespace](index.html#registry_namespace_add).

1.  [Set up your trusted content environment](#trustedcontent_setup).

2.  [Push your image](index.html#registry_images_pushing). The tag is mandatory for trusted content. In the command output you see, "Signing and pushing image metadata."

3.  **First time pushing a signed repository.** When you push a signed image to a new repository, the command creates two signing keys, root key and repository key, and stores them in your local machine. Enter and save secure passphrases for each key, and then [back up your keys](#trustedcontent_backupkeys). Backing up your keys is critical because your [recovery options](ts_index.html#ts_recoveringtrustedcontent) are limited.


## Pulling a signed image
{: #trustedcontent_pull}

The first time that you pull a signed image with Docker Content Trust enabled, your Docker client recognizes the signature as trusted. The Docker client pulls the most recent signed version of the image that you specify. It does not pull unsigned images or untrusted content.
{:shortdesc}


1.  [Set up your trusted content environment](#trustedcontent_setup).

2.  Pull your image. Replace _&lt;source_image&gt;_ with the repository of the image and _&lt;tag&gt;_ with the tag of the image that you want to use, such as _latest_. To list available images to pull, run `bx cr image-list`.

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Specify the tag when you push or pull a signed image. The `latest` tag only defaults when content trust is disabled.
    {: tip}

## Managing trusted content
{: #trustedcontent_managetrust}

Using `docker trust` commands, you can view who signed images, as well as revoke trust content status. To run `docker trust` commands, you need Docker 17.12 or later.
{:shortdesc}

### Viewing signed images
{: #trustedcontent_viewsigned}

You can review signed versions of an image repository or tag, including information on the key ID and signer.
{:shortdesc}

1.  [Set up your trusted content environment](#trustedcontent_setup).

2.  Review the tag, digest, and signer information for each image. **Optional**: Specify the _&lt;tag&gt;_ to see information for that version of the image.

    ```
    docker trust view <image>:<tag>
    ```
    {: pre}

### Revoking trust
{: #trustedcontent_revoketrust}

You can revoke the trusted content status of an image.
{:shortdesc}

Before you begin, retrieve the repository key passphrase that you saved when you [first pushed the trusted repository](#trustedcontent_push). If you need to identify which key is used for the trusted image, use the `docker view` [command](#trustedcontent_viewsigned).

1.  [Set up your trusted content environment](#trustedcontent_setup).

2.  Remove all trusted metadata for the image repository. Enter your repository key passphrase when prompted. **Optional**: Specify a tag to revoke trusted metadata only for that version of the image.

    ```
    docker trust revoke <image>:<tag>
    ```
    {: pre}

3.  Verify that trust was revoked in the list of trusted content. **Optional**: Include the tag if you want to verify revoked content for a tagged image.

    ```
    $ docker trust view <image>:<tag>

    No signatures for <image>:<tag>
    ```
    {: codeblock}

## Backing up signing keys
{: #trustedcontent_backupkeys}

When you first push a signed image to a new repository, Docker Content Trust creates two signing keys, root key and repository key, and stores them on your local machine:

*  Linux and Mac directory: `~/.docker/trust/private`

*  Windows directory: `%HOMEPATH%\.docker\trust\private`

   If you changed your Docker configuration directory, look for the `trust` subdirectory there.
   {: tip}

You must back up all your keys, and especially the root key. If a key is lost or compromised, your [recovery options](ts_index.html#ts_recoveringtrustedcontent) are limited.

To back up your keys, consult the [Docker Content Trust documentation](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys).
