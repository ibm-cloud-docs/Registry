---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Signing images for trusted content
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} provides trusted content technology so that you can sign images to ensure the integrity of images in your registry namespace. By pulling and pushing signed images, you can verify that your images were pushed by the correct party, such as your continuous integration (CI) tools. To use this feature, you must have Docker version 18.03 or later. You can learn more by reviewing the [Docker Content Trust ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.docker.com/engine/security/trust/content_trust/) and the [Notary project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/theupdateframework/notary) documentation.
{:shortdesc}

When you push your image with trusted content enabled, your Docker client also pushes a signed metadata object into the {{site.data.keyword.Bluemix_notm}} trust server. When pulling a tagged image with Docker Content Trust enabled, your Docker client contacts the trust server to establish the latest signed version of the tag that you requested, verifies the content signature, and downloads the signed image.

An image name is made up of a repository and a tag. When you are using trusted content, each repository uses a unique signing key. Each tag within a repository uses the key that belongs to the repository. If you have multiple teams publishing content, each to their own repository within your {{site.data.keyword.registrylong_notm}} namespaces, each team can use their own keys to sign their content so that you can verify that each image is produced by the appropriate team.

A repository can contain both signed and unsigned content. If you have Docker Content Trust enabled, you can access the signed content in a repository, even if there is other unsigned content alongside it.

Docker Content Trust uses a "trust on first use" security model. The repository key is pulled from the trust server when you  pull a signed image from a repository for the first time, and that key is used to verify images from that repository in the future. You must verify that you trust either the trust server or the image and its publisher before pulling the repository for the first time. If the trust information in the server is compromised and you haven't pulled an image from the repository before, your Docker client might pull the compromised information from the trust server. If the trust data is compromised after you pull the image for the first time, on subsequent pulls, your Docker client fails to verify the compromised data and does not pull the image. For more information about how to inspect trust data for an image, see [Viewing signed images](#trustedcontent_viewsigned).

For more information about the "trust on first use" security model, see [The Update Framework (TUF) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://theupdateframework.github.io/).

## Setting up your trusted content environment
{: #trustedcontent_setup}

By default, Docker Content Trust is disabled. Enable the Content Trust environment before logging in to {{site.data.keyword.registrylong_notm}} and working with signed images.
{:shortdesc}

1. Enable the Docker Content Trust environment variable in your terminal.

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

2. Log in to the {{site.data.keyword.Bluemix_notm}} CLI.

   ```
   ibmcloud login [--sso]
   ```
   {: pre}

   If you have a federated ID, use `ibmcloud login --sso` to log in. Enter your user name and use the provided URL in your CLI output to retrieve your one-time passcode. You know you have a federated ID when the login fails without the `--sso` and succeeds with the `--sso` option.
   {: tip}

3. Target the region that you want to use. If you don't know the region name, you can run the command without the region and choose one.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

4. Log in to {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

   The output instructs you to export the Docker Content Trust environment variable.

   **Example**

   ```
   user:~ user$ ibmcloud cr login
   Logging in to 'registry.ng.bluemix.net'...
   Logged in to 'registry.ng.bluemix.net'.

   To set up your Docker client with content trust,
   export the following environment variable:
   export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
   ```
   {: screen}

5. Copy and paste the environment variable command in your terminal. For example:

   ```
   export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
   ```
   {: pre}

Now you are ready to push, pull, and manage trusted, signed images.

During your session with Docker Content Trust enabled, if you want to do an operation with trusted content disabled (such as to pull an unsigned image), use the `--disable-content-trust` flag with the command.
{: tip}

## Pushing a signed image
{: #trustedcontent_push}

When you first push a signed image, Docker automatically creates a pair of signing keys: root and repository. To sign an image in a repository where signed images have been pushed before, you must have the correct repository signing key loaded on the machine that is pushing the image.
{:shortdesc}

Before you begin, [set up your registry namespace](/docs/services/Registry/index.html#registry_namespace_add).

1. [Set up your trusted content environment](#trustedcontent_setup).

2. [Push your image](/docs/services/Registry/index.html#registry_images_pushing). The tag is mandatory for trusted content. In the command output you see:

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

3. **First time pushing a signed repository.** When you push a signed image to a new repository, the command creates two signing keys, root key and repository key, and stores them in your local machine. Enter and save secure passphrases for each key, and then [back up your keys](#trustedcontent_backupkeys). Backing up your keys is critical because your [recovery options](/docs/services/Registry/ts_index.html#ts_recoveringtrustedcontent) are limited.

## Pulling a signed image
{: #trustedcontent_pull}

The first time that you pull a signed image with Docker Content Trust enabled, your Docker client recognizes the signature as trusted. The Docker client pulls the most recent signed version of the image that you specify. Unsigned images or untrusted content are not pulled.
{:shortdesc}

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Pull your image. Replace `<source_image>` with the repository of the image and `<tag>` with the tag of the image that you want to use, such as _latest_. To list available images to pull, run `ibmcloud cr image-list`.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    Specify the tag when you push or pull a signed image. The `latest` tag only defaults when content trust is disabled.
    {: tip}

## Managing trusted content
{: #trustedcontent_managetrust}

By using `docker trust` commands, you can view who signed images and revoke trust content status. To run `docker trust` commands, you must have Docker 18.03 or later.
{:shortdesc}

### Viewing signed images
{: #trustedcontent_viewsigned}

You can review signed versions of an image repository or tag, including information about the key ID and signer.
{:shortdesc}

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Review the tag, digest, and signer information for each image.

   (Optional) Specify the tag, `<tag>`, to see information about that version of the image.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### Revoking trust
{: #trustedcontent_revoketrust}

You can revoke the trusted content status of an image.
{:shortdesc}

Before you begin, retrieve the repository key passphrase that you saved when you [first pushed the trusted repository](#trustedcontent_push). If you need to identify which key is used for the trusted image, use the `docker view` [command](#trustedcontent_viewsigned).

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Remove all trusted metadata for the image repository. Enter your repository key passphrase when prompted.

   (Optional) Specify a tag to revoke trusted metadata only for that version of the image.

   ```
   docker trust revoke <image>:<tag>
   ```
   {: pre}

3. Verify that trust was revoked in the list of trusted content.

   (Optional) If you want to verify revoked content for a tagged image, include the tag.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   Output from the previous command:

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## Backing up signing keys
{: #trustedcontent_backupkeys}

When you first push a signed image to a new repository, Docker Content Trust creates two signing keys, the root key and repository key, and stores them on your local machine:

- Linux and Mac directory: `~/.docker/trust/private`

- Windows directory: `%HOMEPATH%\.docker\trust\private`

   If you changed your Docker configuration directory, look for the `trust` subdirectory there.
   {: tip}

You must back up all your keys, and especially the root key. If a key is lost or compromised, your [recovery options](/docs/services/Registry/ts_index.html#ts_recoveringtrustedcontent) are limited.

To back up your keys, consult the [Docker Content Trust documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys).

## Managing trusted signers
{: #trustedcontent_signers}

You can add and remove signers from signing images in a repository.
{:shortdesc}

### Adding signers to a trusted repository
{: #trustedcontent_addsigners}

To allow other users to sign images in a repository, add the signing keys for those users to that repository.
{:shortdesc}

**Before you begin**

- Image signers must have permission to push images to the namespace.
- Repository owners and additional signers must have Docker 18.03 or later installed.
- Create a trusted content repository by [pushing a signed image](#trustedcontent_push). Repository owners must have the repository admin keys for the repository available in the Docker trust folder on their local machine. If you do not have the repository admin key, contact the owner to do this task for you.

When you add a signer, you can no longer use the repository admin key to sign images in that repository. You must hold the private key for one of the approved signers to sign. To retain the ability to sign images after adding a signer, follow these instructions again to generate and add a signer role for yourself.
{:tip}

To share signing keys:

1. If the new signer has not generated a key pair yet, a key pair must be generated and loaded.
  
    a. Generate the key. You can enter any name for `<NAME>`, however, the name you select is visible when someone inspects trust on the repository. Work with the repository owner to meet any naming conventions that might be used by the organization and to select a name that is identifiable for that signer.

      ```
      docker trust key generate <NAME>
      ```
      {: pre}
  
    b. Enter a passphrase for the private key. A public key (`.pub`) is generated, and the corresponding private key is automatically loaded into the Docker trust configuration.
  
    c. The new signer must send the repository owner the public key.

2. The repository owner must add the signer's key to the repository.

    a. [Set up the trusted content environment](#trustedcontent_setup).

    b. Add the signer's key to the repository.

      ```
      docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}

3. The signer can set up their environment and sign an image.

    a. [Set up the trusted content environment](#trustedcontent_setup).

    b. The signer must sign an image. When prompted, enter the passphrase for the private key.

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4. To verify that the signer was added, see [Viewing signed images](#trustedcontent_viewsigned).

### Removing a signer from a repository
{: #trustedcontent_removesigner}

If you no longer want a signer to be able to sign images in your repository, you can remove them as a signer.
{:shortdesc}

Before you begin, repository owners and additional signers must have Docker 18.03 or later installed.

If you remove a signer, the trust server does not trust their signed versions of the image. To ensure that the image can be pulled after removing the signer, make sure that the signer has not signed the most recent version of the image before continuing. If the signer has signed the most recent version of the image, push an update to the image and sign it by using your key before continuing.
{:tip}

To remove a signer:

1. [Set up your trusted content environment](#trustedcontent_setup).

2. Remove the signer.

   ```
   docker trust signer remove <NAME> <repository>
   ```
   {: pre}

3. To verify that the signer was removed, view the trust data for the image and verify that the signer is no longer listed. For more information about viewing trust data, see [Viewing signed images](#trustedcontent_viewsigned).
