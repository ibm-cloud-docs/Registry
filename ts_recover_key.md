---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-29"

keywords: troubleshooting, support, help, errors, problems, ts, registry, keys, lost keys, recover lost keys, root keys, repo keys, repository keys

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:term: .term}
{:external: target="_blank" .external}
{:troubleshoot: data-hd-content-type='troubleshoot'}

# How do I recover lost or compromised keys?
{: #troubleshoot-recover-key}
{: troubleshoot}
{: support}

Recovering lost or compromised keys for {{site.data.keyword.registrylong}}.
{: shortdesc}

{: tsSymptoms}
When you're using [trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent), you can't manage trusted images any more because your signing keys are lost or compromised.

{: tsCauses}
Your repository or root key is lost or compromised.

{: tsResolve}
Your options for recovering lost or affected keys depend on the type of key: repository or root.

- For [repository keys](#troubleshoot-recover-key-repo), you can generate a new set of signing keys for the repository.
- For [root keys](#troubleshoot-recover-key-root), you can request that the repository is deleted and create a new repository.

## Repository keys
{: #troubleshoot-recover-key-repo}

If your repository key is lost or compromised, generate a new set of signing keys for your repository.
{: shortdesc}

The only signing role that you can rotate is `targets`, which is the repository admin. If other roles are affected, generate new keys for those roles, remove the old ones, and add the new ones as signers.
{:tip}

Before you begin, retrieve the root key passphrase that you created when you first [pushed a signed image](/docs/Registry?topic=Registry-registry_trustedcontent#trustedcontent_push).

1. Install the CLI version of the [Notary project](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli){: external}.

2. [Set up your trusted content environment](/docs/Registry?topic=Registry-registry_trustedcontent#trustedcontent_setup).

3. Create an IAM API key:

   ```
   ibmcloud iam api-key-create notary-auth --file notary-auth
   ```
   {: pre}

4. Set NOTARY_AUTH:

   ```
   export NOTARY_AUTH="iamapikey:$(jq -r .apikey notary-auth)"
   ```
   {: pre}

5. Rotate your keys so that content that was signed with those keys is no longer trusted. Use the trust server variable that you set up in Step 2, and replace`<image>` with the image whose repository key is affected.

   ```
   notary -s "$DOCKER_CONTENT_TRUST_SERVER" -d ~/.docker/trust key rotate <image> targets
   ```
   {: pre}

6. If prompted, enter the root key passphrase. Then, enter a new root key passphrase for the new repository key when prompted.

7. [Push a signed image](/docs/Registry?topic=Registry-registry_trustedcontent#trustedcontent_push) that uses the new signing keys.

8. (Optional) When you've finished, if you want to revoke your API key, run the following command:

    ```
    ibmcloud iam api-key-delete notary-auth
    ```
    {:pre}

## Root keys
{: #troubleshoot-recover-key-root}

If your root key is lost or compromised, you can't update any trusted content repositories that used that root key.
{: shortdesc}

You can [delete the namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_remove) that have repositories that use the affected root key, which deletes your images and trust data.

If the namespace contains repositories with unaffected root keys, such as a namespace for production images, you might want to delete only the trust data associated with the affected root key. Open a support ticket.

1. Contact {{site.data.keyword.cloud}} support, see [Using the Support Center](/docs/get-support?topic=get-support-using-avatar). Include a brief description of your issue, the account ID, and a list of the namespaces that contain the image repositories with affected root keys.

2. After {{site.data.keyword.cloud_notm}} addresses the issue, delete the Docker Content Trust repository on your local computer.

   - Linux and Mac directory: `~/.docker/trust/private` and `~/.docker/trust/tuf`

   - Windows directory: `%HOMEPATH%\.docker\trust\private` and `%HOMEPATH%\.docker\trust\tuf`

   Because the root key is affected, this step deletes all signing keys, including for other trust servers.
   {:tip}

3. If you use [{{site.data.keyword.cloud_notm}} Image Enforcement](/docs/Registry?topic=Registry-security_enforce#security_enforce) in your {{site.data.keyword.containershort_notm}} cluster, restart each image enforcement pod. To trigger Kubernetes to do a rolling restart of the pods automatically, you can change some metadata on the pod. For example, [target your Kubernetes CLI to your cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) and modify the deployment.

   ```
   kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
   ```
   {: pre}

4. Generate trusted content repositories.

    - If you want to create new trusted content, [push new signed images](/docs/Registry?topic=Registry-registry_trustedcontent#trustedcontent_push).

    - If you don't want to change the previous trusted content, add a signature to the most recent images in the registry.

      ```
      docker trust sign <image>:<tag>
      ```
      {: pre}
