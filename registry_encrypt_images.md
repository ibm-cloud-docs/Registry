---

copyright:
  years: 2020,
lastupdated: "2020-08-28"

keywords: encryption, decryption, security, encrypted images, public-private key pairs,

subcollection: Registry

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
{:term: .term}
{:external: target="_blank" .external}

# Encrypting images for content confidentiality in {{site.data.keyword.registrylong_notm}}
{: #registry_encrypt}

You can protect the confidentiality of your {{site.data.keyword.registrylong_notm}} images, and ensure that untrusted hosts can't run the images.
{: shortdesc}

Create an encrypted image so that people without the private key can't access the content. Create the encrypted image by using an RSA public-private key pair to encrypt and decrypt the image. A public key is not a secret and anyone can use it to encrypt an image. A private key is a secret and only users with that private key can use it to decrypt the image.

Encryption is supported in {{site.data.keyword.registrylong_notm}} and complies with the following standards:

* [opencontainers/image-spec](https://github.com/opencontainers/image-spec){: external}
* [opencontainers/artifacts](https://github.com/opencontainers/artifacts/pull/15){: external}

For more information about encrypting images, see:

* [Advancing container image security with encrypted container images](https://developer.ibm.com/articles/advancing-image-security-encrypted-container-images/){: external}
* [Webinar: Advancing image security and compliance through Container Image Encryption!](https://www.youtube.com/watch?v=dYXhAxxPkqA){: external}

## Before you begin
{: #registry_encrypt_prereqs}

* Complete the instructions in [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).
* Ensure that you have the most recent version of the `container-registry` CLI plug-in for the {{site.data.keyword.cloud_notm}} CLI, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
* Ensure that you have a private namespace to push your encrypted image to, see [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).
* Install [Buildah version 1.15](https://buildah.io/releases/2020/06/27/Buildah-version-v1.15.0.html){: external}, or later, so that you can build encrypted images. Buildah works in the Linux environment only. As an alternative to Linux, you can use a virtual machine or Docker image to run Buildah to build images.
* Install [Podman](https://podman.io/).

## Step 1: Create the public-private key pair
{: #registry_encrypt_create}

Create a public-private key pair by using OpenSSL commands.

1. Create a work directory, for example, `<user_keys>`, in which to store the keys and change to that directory:

   ```
   mkdir <user_keys>; cd <user_keys>
   ```
   {: pre}

2. Use OpenSSL to create a private key, where `<user>` is the name for your key's identity:

   ```
   openssl genrsa --out <user>Private.pem
   ```
   {: pre}

   You can protect your private keys and manage data encryption from one central location by using {{site.data.keyword.keymanagementservicelong_notm}}. You can add existing cryptographic keys to {{site.data.keyword.keymanagementservicelong_notm}} by using the {{site.data.keyword.keymanagementserviceshort}} dashboard. For more information, see [Bringing your encryption keys to the cloud](/docs/key-protect?topic=key-protect-importing-keys) and [Importing your own keys](/docs/key-protect?topic=key-protect-getting-started-tutorial#import-keys).
   {: tip}

3. Create a public key:

   ```
   openssl rsa -in <user>Private.pem -pubout -out <user>Pub.pem
   ```
   {: pre}

4. List the keys to ensure that they are created:

   ```
   ls -l
   ```
   {: pre}

5. Display the keys:

   ```
   cat *.pem
   ```
   {: pre}

6. To use this key pair to encrypt images, display the public key by running the following `cat` command, and then copy the public key to somewhere that your build infrastructure can access it:

   ```
   cat <user>Pub.pem
   ```
   {: pre}

   You get a response similar to the following output:

   ```
   -----BEGIN PUBLIC KEY-----
   MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAv8Ny7dCWQ8Pdq1ddYSwk
   QOCB3lUEZVEyj9StX3jnISF/rxIsUZzJfbOrQN0fGkm+1sCCtltgQdztTjito8Fh
   DGflqQBSmV40XP3iZnNUJDrHuAol463Z/BuxxFXL3ry6rTosLGfrRwdQjxp8RSsn
   WyIIO2rmcqXZYe4SCtiMjMejLlTIDWLIMdYL3d6hA4DpgDLoh6EPmhKMVVwRt5b0
   ew5eMLcDuq6ButOM5yv4zYVHNrajY41NK+abSlFb6wzMg2AUDiC/MxV1LRq6mpyZ
   GJllx3LS1M1j7fDO3pmh/M0X7yD/4RgHwFaW4/4CQBw3fyxrOv0pZzZay+o
   -----END PUBLIC KEY-----
   ```
   {: screen}

## Step 2: Encrypt the image
{: #registry_encrypt_image}

Encrypt the image by using the public key and then build a container image by using a Dockerfile.

1. Go to the directory where you store your apps, for example, `<my_app>`.

   ```
   cd <my_app>
   ```
   {: pre}

2. Create the Dockerfile by running the following command:

   ```
   cat << EOF >> Dockerfile
   FROM nginx:latest
   RUN echo "some secret" > /secret-file
   EOF
   ```
   {: pre}

3. Use Buildah to create an unencrypted image by running the following commands, where `<namespace>` is your namespace:

   ```
   buildah bud -t us.icr.io/<namespace>/<my_app> .
   ```
   {: pre}

   `us.icr.io/<namespace>/<my_app>` is committed to the local image store.

4. Encrypt the image by using the public key and upload the image to the registry by running the following commands and by specifying the JSON Web Encryption (`jwe`) protocol to encrypt the image, where `<user_keys>/<user>Pub.pem` is the encryption key:

   ```
   buildah push --encryption-key jwe:..<user_keys>/<user>Pub.pem us.icr.io/<namespace>/<my_app>
   ```
   {: pre}

   Buildah version 1.15, or later, uses Docker’s login credentials to authenticate, if these credentials don't work or you want to use an API key, you can supply the `—-creds <user_name>` option, where `<user_name>` is the username. If you use the `—-creds <user_name>` the option, when requested, type in the password of the registry credential.
   {: tip}

   You get a response telling you that the manifest is written to the image destination, which is the registry.

5. Check in your registry to make sure that the image is there.

## Step 3: Pull and decrypt the image
{: #registry_encrypt_pull}

Pull the image from the registry and decrypt it by using the private key.

1. To ensure that you are pulling from the registry and that you are not using the local cache, remove the image locally:

   ```
   buildah rmi -f us.icr.io/<namespace>/<my_app>
   ```
   {: pre}

2. (Optional) You can try to pull the image without providing the decryption key to confirm that the image can't be decrypted:

   ```
   buildah pull us.icr.io/<namespace>/<my_app>
   ```
   {: pre}

   The output contains a message similar to the following message:

   ```
   ...<truncated>...
   Error decrypting layer sha256:ab4ea03582e08a8e8fc35b778cc6f1a1fa797469fa9cc61cee85f703b316bb12: missing private key needed for decryption
   ERRO exit status 125
   ```
   {: screen}

3. Use Buildah to pull the image with the decryption key, where `<user_keys>/<user>Private.pem` is the decryption key and `us.icr.io/<namespace>/<my_app>` is the registry:

   ```
   buildah pull --decryption-key ../<user_keys>/<user>Private.pem us.icr.io/<namespace>/<my_app>
   ```
   {: pre}

   The encrypted image is retrieved from the registry, decrypted, and stored in the local image store.

4. Confirm that the image is stored by running Podman:

   ```
   podman run -it us.icr.io/<namespace>/<my_app> /bin/bash
   ```
   {: pre}

## Next steps
{: #registry_encrypt_next}

You can run encrypted images in [{{site.data.keyword.containerlong_notm}}](https://{DomainName}/kubernetes/registry/main/private){: external}, however, it is currently unsupported. You can use this technology preview, [Encrypted Images Key Syncer Helm Operator](https://operatorhub.io/operator/enc-key-sync){: external}.
{: note}
