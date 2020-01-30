---

copyright:
  years: 2017, 2020
lastupdated: "2020-01-30"

keywords: troubleshooting, support, help, errors, error messages, failure, fails, lost keys, firewall, Docker manifest errors, problems, ts, registry,

subcollection: registry

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

# Troubleshooting
{: #ts_index}

Here are the answers to common troubleshooting questions about using {{site.data.keyword.registrylong}}.
{:shortdesc}

## Getting help and support for {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

If you have problems or questions when you are using {{site.data.keyword.registrylong_notm}}, you can get help by searching for information or by asking questions through a forum. You can also open an {{site.data.keyword.IBM}} support ticket.

When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.registrylong_notm}} development team.

- If you have technical questions about developing or deploying an app with {{site.data.keyword.registrylong_notm}}, post your question on [Stack Overflow](https://stackoverflow.com/search?q=+ibm-cloud+container-registry){: external} and tag your question with `ibm-cloud` and `container-registry`.
- For questions about the service and getting started instructions, use the [IBM Developer Answers](https://developer.ibm.com/answers/topics/container-registry.html){: external} forum. Include the `ibm-cloud` and `container-registry` tags.

See [Using the Support Center](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) for more details about using the forums.

For information about opening an {{site.data.keyword.IBM_notm}} support ticket, or about support levels and ticket severities, see [How do I get the support I need?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support)

## Logging in to {{site.data.keyword.registrylong_notm}} fails
{: #ts_login}

You can't log in to {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
The `ibmcloud cr login` command fails.

{: tsCauses}
The following alternatives are possible causes:

- The `container-registry` CLI plug-in is out of date and needs updating.
- Docker is not installed on your local computer, or is not running.
- Your {{site.data.keyword.cloud_notm}} login credentials have expired.

{: tsResolve}
You can fix this problem in the following ways:

- Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).
- Ensure that Docker is installed on your computer. If it is already installed, restart the Docker daemon.
- Rerun the `ibmcloud login` command to refresh your {{site.data.keyword.cloud_notm}} login credentials.

## Running any command for {{site.data.keyword.registrylong_notm}} fails with `FAILED You are not logged in to IBM Cloud.`
{: #ts_login_cloud}

You can't run any commands in {{site.data.keyword.registrylong_notm}}, even though you are logged in to {{site.data.keyword.cloud_notm}}.

{: tsSymptoms}
All `ibmcloud cr` commands fail.

{: tsCauses}
The `container-registry` CLI plug-in is out of date and needs updating.

{: tsResolve}
Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).

## {{site.data.keyword.registrylong_notm}} commands fail with `'cr' is not a registered command. See 'ibmcloud help'.`
{: #ts_login_error}

You can't run a `ibmcloud cr` command because `cr` is not a registered `ibmcloud` command.

{: tsSymptoms}
You see an error message similar to one of the following error messages:

```
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

```
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

{: tsCauses}
The `container-registry` CLI plug-in is not installed.

{: tsResolve}
Install the `container-registry` CLI plug-in, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## The `ibmcloud cr build` command fails
{: #ts_build_fails}

{: tsSymptoms}
The build command fails.

{: tsCauses}
The server might be down or there might be issues with your Dockerfile.

{: tsResolve}
To find out what the cause is, run `docker build` locally with the appropriate [`docker build` options](https://docs.docker.com/engine/reference/commandline/build/){: external}:

```
docker build --no-cache .
```
{:  pre}

- If the local build doesn't work, check for issues with your Dockerfile.
- If the local build works, [contact {{site.data.keyword.cloud_notm}} support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).

## Setting up a namespace fails
{: #ts_problem}

{: tsSymptoms}
When you run `ibmcloud cr namespace-add`, you are unable to set your entered value as the namespace.

{: tsCauses}
The following alternatives are possible causes:

- You entered a namespace value that is already being used by another {{site.data.keyword.cloud_notm}} organization.
- A namespace was recently deleted and you are reusing its name. If the namespace that was deleted contained many resources, the deletion might not yet be fully processed by {{site.data.keyword.registrylong_notm}}.
- You used invalid characters in the namespace value.

{: tsResolve}
You can fix this problem in the following ways:

- Follow any instructions that are in the returned error message.
- Check that you entered a valid namespace:
  - Your namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region.
  - Your namespace must be 4 - 30 characters long.
  - Your namespace must start and end with a letter or number.
  - Your namespace must contain lowercase letters, numbers, hyphens (-), and underscores (_) only.
- Choose a different value for your namespace.
- If you are re-creating a namespace that was deleted, and it contained many images, try again later.

## Push or pull of a Docker image fails
{: #ts_pushpull}

{: tsSymptoms}
When you run commands to push or pull Docker images, you receive an error message. The error message varies depending on the root cause. Potential error messages might be:

```
You have exceeded your storage quota. Delete one or more images,
or review your storage quota and pricing plan
```
{: screen}

```
You have exceeded your pull traffic quota for the current month.
Review your pull traffic quota and pricing plan
```
{: screen}

```
unauthorized: authentication required
```
{: screen}

```
denied: requested access to the resource is denied
```
{: screen}

{: tsCauses}
The following alternatives are possible causes:

- Docker is not installed.
- The Docker client is not logged in to {{site.data.keyword.registrylong_notm}}.
- Your {{site.data.keyword.cloud_notm}} access token might have expired.
- You exceeded the quota limit for storage or pull traffic that is set for your {{site.data.keyword.cloud_notm}} account.

{: tsResolve}
You can fix this problem in the following ways:

- [Ensure that Docker is installed on your computer](/docs/Registry?topic=registry-getting-started#gs_registry_cli_install).
- Check your Docker installation path.
- Log in to {{site.data.keyword.cloud_notm}} by running `ibmcloud login`. Then, log in to the {{site.data.keyword.registrylong_notm}} CLI by running `ibmcloud cr login`.
- [Review quota limits and usage for storing and pulling Docker images in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-registry_quota#registry_quota_get).

## Unable to pull the most recent image using the `latest` tag
{: #ts_docker_latest}

{: tsSymptoms}
You are trying to run the command `docker pull`, but it returned a version of your image that is not the most recent version built.

{: tsCauses}
The `latest` tag is applied by default to reference an image when you run Docker commands without specifying the tag value. The `latest` tag is applied to the most recent `docker build` or `docker tag` command that was run without a tag value explicitly set. Therefore, it's possible to run `docker` commands out-of-order or to explicitly set tags on some images, and the `latest` tag to refer to a build that is not the most recent.

{: tsResolve}
It is generally better to explicitly define a different sequential tag for your images every time, and not rely on the `latest` tag.

## Unable to add other IBM images to the registry
{: #ts_ppa}

{: tsSymptoms}
When you try to import content that you used in other IBM products, such as {{site.data.keyword.cloud_notm}} Private, you are not able to store your images and other licensed software from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external} in the registry.

{: tsCauses}
Software packages such as images and Helm charts from IBM Passport Advantage must be imported to the registry with the `ibmcloud cr ppa-archive-load` command.

{: tsResolve}
Before you begin to import a product from IBM Passport Advantage, complete the following tasks:

1. Log in to {{site.data.keyword.cloud_notm}} by running `ibmcloud login [--sso]`.
2. Log in to {{site.data.keyword.registrylong_notm}} by running `ibmcloud cr login`.
3. [Target the `kubectl` CLI](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) to your cluster.
4. If you have not already set up Helm in your cluster, [set up Helm in your cluster now](/docs/containers?topic=containers-helm#helm).
5. If you want to share the charts within your organization, you can install the [Chart Museum open source project](https://github.com/helm/charts/tree/master/stable/chartmuseum){: external}. For instructions, see this [developerWorks recipe](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/){: external}.

### Importing IBM Passport Advantage products for use in {{site.data.keyword.cloud_notm}}
{: #ts_ppa_import}

1. Obtain the compressed file that you want to import from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}.

2. Target the region that you want to use. If you don't know the region name, run the command without the region and then choose a region.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

3. Import the compressed archive file. Specify the path to the compressed file and the registry namespace that you want to push the images to.

   ```
   ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
   ```
   {: pre}

   This command expands the compressed file, loads any contained images into your local Docker client, and then pushes the images to the namespace in your registry.

   If you want to upload Helm charts from the IBM Passport Advantage archive to a chart museum, include the following options in the command: `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
   {: tip}

   The following message is an example of the output from the command:

   ```
   user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
   Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
   Found 1 image(s) and 1 chart(s) to import.
   Importing 'iib-prod:10.0.0.10' and pushing it to 'us.icr.io/mynamespace/iib-prod:10.0.0.10'...
   Loaded image: iib-prod:10.0.0.10
   The push refers to repository [us.icr.io/mynamespace/iib-prod]
   1ecda25d51a8: Preparing
   369bf331939e: Preparing
   ...
   369bf331939e: Pushed
   1ecda25d51a8: Pushed
   10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

   Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

   OK
   ```
   {: screen}

4. If the compressed files contain Helm charts, these charts are placed in an archive directory called `ppa-import` that is created in your current working directory. Open the directory to get the name of the Helm chart, `<helm_chart>`, and then inspect its values.

   ```
   helm inspect values ppa-import/charts/<helm_chart>.tgz
   ```
   {: pre}

   If you uploaded charts to a chart museum in the previous step, you can use `helm inspect` to inspect the chart in chart museum.
   {: tip}

5. Configure the Helm chart,`<helm_chart>`, according to the values that are output by the `helm inspect values` command.

6. Deploy the Helm chart, `<helm_chart>`, by using the `helm install` command. You can override values in the chart as required by using the `--set` option.

   ```
   helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
   ```
   {: pre}

## I used the `ibmcloud cr image-rm` command to delete an image and all the tags that referenced that image got deleted too
{: #ts_image-rm}

{: tsSymptoms}
You deleted an image by using the `ibmcloud cr image-rm` command and all the tags within the same repository that referenced the image also got deleted.

{: tsCauses}
Where multiple tags exist for the same image digest within a repository, the [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command removes the underlying image and all its tags. If the same image exists in a different repository or namespace, that copy of the image is not removed.

{: tsResolve}
If you want to remove a tag from an image, but leave the underlying image and any other tags, use the [`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) command. For more information, see [Removing tags from images in your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=registry-registry_images_#registry_images_untag) and [Deleting images from your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=registry-registry_images_#registry_images_remove).

## An image does not show in the list produced by the `ibmcloud cr retention-run` command
{: #ts_image_list}

{: tsSymptoms}
You ran the [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) command and an image that you're expecting to see in the list is not displayed.

{: tsCauses}
You might have a distroless image. Some distroless images don't have a creation date. The `ibmcloud cr retention-run` command deletes the oldest images, and therefore requires a creation date.

{: tsResolve}
You can delete the image manually by running the [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) command, see [Deleting images from your private IBM Cloud repository](/docs/Registry?topic=registry-registry_images_#registry_images_remove).

To check the creation date of an image, you can run the [`ibmcloud cr image-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) command. If the image doesn't have a creation date, the date is shown in the `ibmcloud cr image-inspect` output as `1970-01-01` and the image is excluded from the results for `ibmcloud cr retention-run`.
{: tip}

## You want to restore an image from the trash, but you get a 409 error: `The tagged image already exists. You can restore this image by using the digest.`
{: #ts_image_restore}

{: tsSymptoms}
You receive the following error message when you run the [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore) command: `The tagged image already exists. You can restore this image by using the digest.`

{: tsCauses}
An image with the same name exists in your live repository. You can't overwrite a live image with an image that is in the trash.

{: tsResolve}
You can restore this image by restoring by digest and then, if required, you can use the `ibmcloud cr image-tag` command to tag the image, see [Restoring images by digest](/docs/Registry?topic=registry-registry_images_#registry_images_restore_digest).

## Accessing the registry with a custom firewall fails
{: #ts_firewall}

{: tsSymptoms}
You set up an additional firewall in your development environment with custom settings for inbound and outbound network traffic. When trying to access {{site.data.keyword.registrylong_notm}}, the connection fails.

{: tsCauses}
Your custom firewall requires certain network groups to be opened for inbound and outbound network traffic to allow communication to and from the registry.

{: tsResolve}
Let your cluster access infrastructure resources and services from behind a firewall, see [Allowing the cluster to access infrastructure resources and other services](/docs/containers?topic=containers-firewall#firewall_outbound).

For INBOUND connectivity to your computer, allow incoming network traffic from the source network groups to the destination public IP address of your computer.

For OUTBOUND connectivity from your computer, use the same network groups and allow outgoing network traffic from the source public IP address of your computer to the network groups.

## Recovering lost or compromised keys
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
When using [trusted content](/docs/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent), you can no longer manage trusted images because your signing keys are lost or compromised.

{: tsCauses}
Your repository or root key is lost or compromised.

{: tsResolve}
Your options for recovering lost or affected keys depend on the type of key: repository or root:

- For [repository keys](#trustedcontent_lostrepokey), you can generate a new set of signing keys for the repository.
- For [root keys](#trustedcontent_lostrootkey), you can request that the repository is deleted and create a new repository.

### Repository keys
{: #trustedcontent_lostrepokey}

If your repository key is lost or compromised, generate a new set of signing keys for your repository.
{:shortdesc}

The only signing role that you can rotate is `targets`, which is the repository admin. If other roles are affected, generate new keys for those roles, remove the old ones, and add the new ones as signers.
{:tip}

Before you begin, retrieve the root key passphrase that you created when you first [pushed a signed image](/docs/Registry?topic=registry-registry_trustedcontent#trustedcontent_push).

1. Install the CLI version of the [Notary project](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli){: external}.

2. [Set up your trusted content environment](/docs/Registry?topic=registry-registry_trustedcontent#trustedcontent_setup).

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

7. [Push a signed image](/docs/Registry?topic=registry-registry_trustedcontent#trustedcontent_push) that uses the new signing keys.

8. (Optional) When you've finished, if you want to revoke your API key, run the following command:

    ```
    ibmcloud iam api-key-delete notary-auth
    ```
    {:pre}

### Root keys
{: #trustedcontent_lostrootkey}

If your root key is lost or compromised, you can't update any trusted content repositories that used that root key.
{:shortdesc}

You can [delete the namespaces](/docs/Registry?topic=registry-registry_setup_cli_namespace#registry_remove) that have repositories that use the affected root key, which deletes your images and trust data.

If the namespace contains repositories with unaffected root keys, such as a namespace for production images, you might want to delete only the trust data associated with the affected root key. Open a support ticket.

1. [Contact {{site.data.keyword.cloud_notm}} support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support). Include a brief description of your issue, the account ID, and a list of the namespaces that contain the image repositories with affected root keys.

2. After {{site.data.keyword.cloud_notm}} addresses the issue, delete the Docker Content Trust repository on your local computer.

   - Linux and Mac directory: `~/.docker/trust/private` and `~/.docker/trust/tuf`

   - Windows directory: `%HOMEPATH%\.docker\trust\private` and `%HOMEPATH%\.docker\trust\tuf`

   Because the root key is affected, this step deletes all signing keys, including for other trust servers.
   {:tip}

3. If you use [{{site.data.keyword.cloud_notm}} Image Enforcement](/docs/Registry?topic=registry-security_enforce#security_enforce) in your {{site.data.keyword.containershort_notm}} cluster, restart each image enforcement pod. To trigger Kubernetes to do a rolling restart of the pods automatically, you can change some metadata on the pod. For example, [target your Kubernetes CLI to your cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) and modify the deployment.

   ```
   kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
   ```
   {: pre}

4. Generate trusted content repositories.

    - If you want to create new trusted content, [push new signed images](/docs/Registry?topic=registry-registry_trustedcontent#trustedcontent_push).

    - If you don't want to change the previous trusted content, add a signature to the most recent images in the registry.

      ```
      docker trust sign <image>:<tag>
      ```
      {: pre}

## The installation of Container Image Security Enforcement fails with `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists`
{: #ts_install_cise_fail}

{: tsSymptoms}
Your installation of Container Image Security Enforcement failed and you received the following message:

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
The previous installation failed and the subsequent uninstallation did not remove every Kubernetes job that is associated with the installation.

{: tsResolve}
Remove the remaining Kubernetes jobs by running the following command:

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}

## Pods do not restart after all your workers have been down
{: #ts_pods}

{: tsSymptoms}
Pods do not restart after all your cluster workers have been down. Container Image Security Enforcement is deployed. The cluster workers are showing as healthy, but nothing is scheduled.

{: tsCauses}
By default, Container Image Security Enforcement adds a fail closed admission webhook. If all Container Image Security Enforcement pods are down, the pods are not available to approve their own recovery.

{: tsResolve}
To recover the cluster when it's in this state, you must change the webhook configuration to make it fail open instead of closed.

You must have sufficient role-based access control (RBAC) privileges to use the following verbs:

- `GET`
- `PATCH`

on these resources:

- `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
- `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration`

For more information about RBAC, see [Authorizing users with custom Kubernetes RBAC roles](/docs/containers?topic=containers-users#rbac) and [Kubernetes - Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/){: external}.

Complete the following steps to change the webhook configuration to make it fail open instead of closed, and then, when at least one Container Image Security Enforcement pod is running, restore the webhook configuration so that it fails closed:

1. Update `MutatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Change `failurePolicy` to `Ignore`, save, and close.

2. Update `ValidatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Change `failurePolicy` to `Ignore`, save, and close.

3. Wait for some Container Image Security Enforcement pods to start. You can check whether the pods have started by running the following command until you see the **STATUS** column for at least one pod is displaying `Running`:

   ```
   kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
   ```
   {: pre}

4. When at least one Container Image Security Enforcement pod is running, update `MutatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Change `failurePolicy` to `Fail`, save, and close.

5. Update `ValidatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Change `failurePolicy` to `Fail`, save, and close.

## Manifest error: `The manifest type for this image is not supported for tagging.`
{: #ts_manifest_error_type}

{: tsSymptoms}
You tried to tag your image, but you receive the following error message: `The manifest type for this image is not supported for tagging.`

{: tsCauses}
The manifest type is not supported.

{: tsResolve}
To resolve the problem, complete the following steps:

1. Pull the image that you tried to tag by running the following command, where `<source_image>` is your source image name:

   ```
   docker pull <source_image>
   ```
   {: pre}

2. Tag your local copy of the image that you pulled in the previous step by running the following command, where `<target_image>` is your new image name:

   ```
   docker tag <source_image> <target_image>
   ```
   {: pre}

3. Push the image that you tagged in the previous step by running the following command:

   ```
   docker push <target_image>
   ```
   {: pre}

## Manifest error: `The manifest version for this image is not supported for tagging.`
{: #ts_manifest_error_version}

{: tsSymptoms}
You tried to tag your image, but you receive the following error message: `The manifest version for this image is not supported for tagging. To upgrade to a supported manifest version, pull and push this image by using Docker version 1.12 or later, then run the 'ibmcloud cr image-tag' command again.`

{: tsCauses}
The manifest version is not supported.

{: tsResolve}
To resolve the problem, complete the following steps:

1. Upgrade to Docker Engine version 1.12 or later.

2. Pull the image that you tried to tag by running the following command, where `<source_image>` is your source image name:

   ```
   docker pull <source_image>
   ```
   {: pre}

3. To upgrade the manifest version, push the image by running the following command:

   ```
   docker push <source_image>
   ```
   {: pre}

4. Tag the image by running the `ibmcloud cr image-tag` command, see [Creating new images that refer to a source image](/docs/Registry?topic=registry-registry_images_#registry_images_source).

## Docker login fails on a Mac: `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`
{: #ts_docker_mac}

{: tsSymptoms}
You receive the following error message when you try to run the `ibmcloud cr login` command on a Mac: `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`

{: tsCauses}
There is a problem with Docker for Mac that prevents your credentials from being stored in the macOS keychain.

{: tsResolve}
You might be able to resolve the problem by rebooting your Mac. If rebooting your Mac doesn't work, you can disable the storage of logins in your Mac keychain:

1. In your menu, click the **Docker** icon, select **Preferences**.
2. Clear the **Securely store Docker logins in macOS keychain** check box.
