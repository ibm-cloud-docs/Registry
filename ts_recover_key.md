---

copyright:
  years: 2017, 2021
lastupdated: "2021-08-06"

keywords: troubleshooting, support, help, errors, problems, ts, registry, keys, lost keys, recover lost keys, root keys, repo keys, repository keys

subcollection: Registry

content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note .note}
{:note: .note}
{:note:.deprecated}
{:objectc data-hd-programlang="objectc"}
{:objectc: .ph data-hd-programlang='Objective C'}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# How do I recover lost or compromised keys?
{: #troubleshoot-recover-key}
{: troubleshoot}
{: support}

Recovering lost or compromised keys for {{site.data.keyword.registrylong}}.
{: shortdesc}

When you're using [trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent), you can't manage trusted images anymore because your signing keys are lost or compromised.
{: tsSymptoms}

Your repository or root key is lost or compromised.
{: tsCauses}

Your options for recovering lost or affected keys depend on the type of key: repository or root.
{: tsResolve}

- For [repository keys](#troubleshoot-recover-key-repo), you can generate a new set of signing keys for the repository.
- For [root keys](#troubleshoot-recover-key-root), you can request that the repository is deleted and create a new repository.

## Repository keys
{: #troubleshoot-recover-key-repo}

If your repository key is lost or compromised, generate a new set of signing keys for your repository.
{: shortdesc}

The Notary v1 service is deprecated. It is being removed from {{site.data.keyword.registrylong_notm}} on 31 August 2021. As an alternative approach, {{site.data.keyword.registrylong_notm}} supports the [Red Hat Signing](https://www.redhat.com/en/blog/container-image-signing){: external} model. For more information, see [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig).
{: deprecated}

The only signing role that you can rotate is `targets`, which is the repository admin. If other roles are affected, generate new keys for those roles, remove the old ones, and add the new ones as signers.
{:tip}

Before you begin, retrieve the root key passphrase that you created when you first [pushed a signed image](/docs/Registry?topic=Registry-registry_trustedcontent#trustedcontent_push).

1. Install the CLI version of the [Notary project](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli){: external}.

2. [Set up your trusted content environment](/docs/Registry?topic=Registry-registry_trustedcontent#trustedcontent_setup).

3. Create an IAM API key.

   ```
   ibmcloud iam api-key-create notary-auth --file notary-auth
   ```
   {: pre}

4. Set the `NOTARY_AUTH`.

   ```
   export NOTARY_AUTH="iamapikey:$(jq -r .apikey notary-auth)"
   ```
   {: pre}

5. Rotate your keys so that content that was signed with those keys is no longer trusted. Use the trust server variable that you set up in Step 2, and replace `<image>` with the image whose repository key is affected.

   ```
   notary -s "$DOCKER_CONTENT_TRUST_SERVER" -d ~/.docker/trust key rotate <image> targets
   ```
   {: pre}

6. If prompted, enter the root key passphrase. Then, enter a new root key passphrase for the new repository key when prompted.

7. [Push a signed image](/docs/Registry?topic=Registry-registry_trustedcontent#trustedcontent_push) that uses the new signing keys.

8. (Optional) When you finish, if you want to revoke your API key, run the following command.

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

   - Linux&reg; and macOS directory `~/.docker/trust/private` and `~/.docker/trust/tuf`

   - Windows&reg; directory `%HOMEPATH%\.docker\trust\private` and `%HOMEPATH%\.docker\trust\tuf`

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
