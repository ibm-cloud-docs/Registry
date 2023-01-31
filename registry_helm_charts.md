---

copyright:
  years: 2022
lastupdated: "2023-01-31"

keywords: helm, charts, private repository, trash, recycle bin, restoring charts, helm chart, registry, namespace, cli, tags, images, helm repository

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using Helm charts
{: #registry_helm_charts}

You can securely store and share Helm charts with other users in {{site.data.keyword.registrylong}}.
{: shortdesc}

## OCI support for Helm charts
{: #registry_helm_charts_oci}

The [Open Container Initiative (OCI)](https://opencontainers.org){: external} released [Open Container Initiative Distribution Specification v1.0.0](https://specs.opencontainers.org/distribution-spec/?v=v1.0.0){: external} in September 2021. This specification supports other artifact types in addition to container images. One of the [artifact types that is supported](https://github.com/opencontainers/artifacts/blob/main/artifact-authors.md#defining-oci-artifact-types){: external} is the [Helm chart](https://helm.sh/docs/topics/charts/){: external}.

[Helm v3.8.0](https://github.com/helm/helm/releases/tag/v3.8.0){: external} provides support to store and work with charts in OCI registries, as an alternative to [Helm chart repositories](https://helm.sh/docs/topics/chart_repository/){: external}. For more information, see the [Helm Registries documentation](https://helm.sh/docs/topics/registries/){: external}.

## Adding Helm charts to your namespace
{: #registry_helm_charts_add}
{: help}
{: support}

You can securely store and share Helm charts with other users by adding charts to your [namespace](x2031005){: term} in {{site.data.keyword.registrylong_notm}}.

Every Helm chart that you want to add to your namespace must exist on your local computer first. You can either download (pull) a chart from another repository to your local computer, or build your own chart by using the [`helm create`](https://helm.sh/docs/helm/helm_create/){: external} command. To add a chart to your namespace, you must upload (push) the local chart to your namespace in {{site.data.keyword.registrylong_notm}}.

Do not put personal information in your charts (for example, in namespace names or description fields) or in any chart or chart configuration data (for example, chart names or chart labels).
{: important}

### Pulling charts from another registry or Helm repository
{: #registry_helm_charts_pull}
{: help}
{: support}

You can pull (download) a chart from any private or public [registry](x2064940){: term} source or Helm repository, and then tag it for later use in {{site.data.keyword.registrylong_notm}}.

![Pull a chart from a private or public registry or Helm repository to your computer.](images/images_pull.svg "You can pull a chart from {{site.data.keyword.registrylong_notm}} or from any private or public registry source or Helm repository to your local computer."){: caption="Figure 1. Pulling charts from another registry" caption-side="bottom"}

Before you begin, complete the following tasks.

- [Install the CLI](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) to work with your namespace.
- [Set up your own namespace in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_setup).
- Install the latest release of [Helm CLI](https://github.com/helm/helm/releases){: external} to work with charts.

1. Download the Helm chart to your local computer.

    - From the OCI registry:

        ```txt
        helm pull oci://<registry/<my_namespace>/<chart_name> --version <chart_version>
        ```
        {: pre}

        Example, where `<registry>` is `localhost:5000`, `my_namespace` is `helm-charts`, `chart_name` is `mychart`, and `<chart_version>` is `0.1.0`:

        ```txt
        helm pull oci://localhost:5000/helm-charts/mychart --version 0.1.0
        ```
        {: pre}

    - From a Helm repository:

        ```txt
        helm pull <chart URL | repo/chartname> --version <chart_version>
        ```
        {: pre}

        Example, where `<repo/chartname>` is `ibm-charts/ibm-istio` and `<chart_version>` is `1.2.2`.

        You can add the repo alias by using the [`helm repo add`](https://helm.sh/docs/helm/helm_repo_add/){: external} command.
        {: tip}

        ```txt
        helm pull ibm-charts/ibm-istio  --version 1.2.2
        ```
        {: pre}

    If you get an `unauthorized: authentication required` or a `denied: requested access to the resource is denied` message, run the [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login) command.
    {: tip}

After you pull a chart for your [namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace), you can upload (push) the chart from your local computer to your namespace.

### Pushing Helm charts to your namespace
{: #registry_helm_charts_push}
{: help}
{: support}

You can push (upload) a chart to your namespace in {{site.data.keyword.registrylong_notm}} to store and share your chart with other users.

![Push a chart from your computer to {{site.data.keyword.registrylong_notm}}.](images/images_push.svg "You can push (upload) a chart from your local computer to your namespace in {{site.data.keyword.registrylong_notm}} to store and share your chart with other users."){: caption="Figure 2. Pushing charts to your namespace" caption-side="bottom"}

Before you begin, complete the following tasks.

- [Install the CLI](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) to work with your namespace.
- [Set up your own namespace in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_setup).
- Install the latest release of [Helm CLI](https://github.com/helm/helm/releases){: external} to work with charts.
- [Pull](#registry_helm_charts_pull) or [create](https://helm.sh/docs/chart_template_guide/getting_started/){: external} a chart on your local computer. If you create a chart, you must save the chart as an archive by using the [`helm package`](https://helm.sh/docs/helm/helm_package/){: external} command.

To upload (push) a chart, complete the following steps:

1. Log in to the CLI by running the [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login) command.

    ```txt
    ibmcloud cr login
    ```
    {: pre}

    You must log in if you pull a chart from your private {{site.data.keyword.registrylong_notm}}.
    {: tip}

2. To view all namespaces that are available in your account, run the [`ibmcloud cr namespace-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list) command.
3. Upload the chart to your namespace.

    ```txt
    helm push <my_chart_package> oci://<region>.icr.io/<my_namespace>
    ```
    {: pre}

    Example, where `<my_chart_package>` is `mychart-0.1.0.tgz`, `region` is `uk`, and `<my_namespace>` is `helm-charts`:

    ```txt
    helm push mychart-0.1.0.tgz oci://uk.icr.io/helm-charts
    ```
    {: pre}

    If you get an `unauthorized: authentication required` or a `denied: requested access to the resource is denied` message, run the `ibmcloud cr login` command.
    {: tip}

After you push your chart to {{site.data.keyword.registrylong_notm}}, you can [install the Helm chart to the cluster in {{site.data.keyword.containerlong_notm}}](#registry_helm_charts_install).

### Copying charts between registries
{: #registry_helm_charts_copy}
{: help}
{: support}

You can pull a chart from a registry in one region and push it to a registry in another region so that you can share the chart with users in both regions.

![Copying charts between registries.](images/images_copy.svg "You can pull a chart from a registry in one region and push it to a registry in another region."){: caption="Figure 3. Copying charts between registries" caption-side="bottom"}

Before you begin, complete the following tasks.

- [Install the CLI](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) to work with your namespace.
- [Set up your own namespace in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_setup).
- Install the latest release of [Helm CLI](https://github.com/helm/helm/releases){: external} to work with charts.

To copy a chart between two registries, complete the following steps:

1. [Pull a chart from a registry](#registry_helm_charts_pull).
2. [Push the chart to another registry](#registry_helm_charts_push). Make sure that you use the correct domain name for the new region that you're targeting.

After you copy your chart, you can [install the Helm chart to the cluster in {{site.data.keyword.containerlong_notm}}](#registry_helm_charts_install).

### Installing a Helm chart to the cluster
{: #registry_helm_charts_install}
{: help}
{: support}

You can install a Helm chart to the cluster in {{site.data.keyword.containerlong_notm}} directly from the registry. Follow the instructions in the Helm chart `README`, and use the full registry reference to the chart and chart version for installation.

```txt
helm install <release_name> oci://<region>.icr.io/<my_namespace>/<chart_name> --version <chart_version>
```
{: pre}

Example, where `<release_name>` is `myrelease`, `region` is `uk`, `<my_namespace>` is `helm-charts`, `<chart_name>` is `mychart`, and `<chart_version>` is `0.1.0`:

```txt
helm install myrelease oci://uk.icr.io/helm-charts/mychart --version 0.1.0
```
{: pre}

## Deleting charts from your private repository
{: #registry_helm_charts_remove}
{: help}
{: support}

You can delete unwanted charts from your private {{site.data.keyword.cloud_notm}} [repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository) by using either the {{site.data.keyword.cloud_notm}} console or the CLI.

If you want to delete a private repository and its associated charts, see [Deleting a private repository and any associated charts](#registry_helm_charts_repo_remove).

Deleting a chart that is being used by an existing deployment might cause a Helm upgrade, rollback, or delete to fail.
{: important}

If you want to restore a deleted chart, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command and restore a selected chart by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command. You can use these commands because Helm charts are a supported artifact type in OCI.
{: tip}

Where multiple [tags](#x2040924){: term} exist for the same chart digest within a repository, the [`ibmcloud cr image-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm) command removes the underlying chart and all its tags. If the same chart exists in a different repository or namespace, that copy of the chart is not removed.
{: tip}

A tag must always match the chart's semantic version, which means that a `latest` tag isn't used.
{: tip}

### Deleting charts from your private repository in the CLI
{: #registry_helm_charts_remove_cli}
{: help}
{: support}

You can delete unwanted charts and all their tags from your private {{site.data.keyword.cloud_notm}} repository by using the CLI.

Deleting a chart that is being used by an existing deployment might cause a Helm upgrade, rollback, or delete to fail.
{: important}

If you want to restore a deleted chart, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command and restore a selected chart by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command.
{: tip}

To delete a chart by using the CLI, complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. To delete a chart, run the following command, where `CHART` is the name of the chart that you want to remove, in the format `repository@digest` or `repository:tag`. Unlike images, a tag must be specified because the `latest` tag doesn't exist because a tag must always match the chart's semantic version. You can delete multiple charts by listing each private {{site.data.keyword.cloud_notm}} registry path in the command with a space between each path.

    ```txt
    ibmcloud cr image-rm CHART
    ```
    {: pre}

    To find the names of your charts, run `ibmcloud cr image-list`. The registry stores different artifact types that include Helm charts and container images. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`. To identify your chart by digest, run the `ibmcloud cr image-digests` command. Combine the content of the **Repository** column (`repository`) and the **Digest** column (`digest`) separated by an at (`@`) symbol to create the image name in the format `repository@digest`.
    {: tip}

3. Verify that the chart was deleted by running the following command, and check that the chart does not show in the list.

    ```txt
    ibmcloud cr image-list
    ```
    {: pre}

### Deleting charts from your private repository in the console
{: #registry_helm_charts_remove_gui}
{: help}
{: support}

You can delete unwanted charts and all their tags from your private {{site.data.keyword.cloud_notm}} repository by using the {{site.data.keyword.cloud_notm}} console.

Deleting a chart that is being used by an existing deployment might cause a Helm upgrade, rollback, or delete to fail.
{: important}

If you want to restore a deleted chart, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command and restore a selected chart by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command.
{: tip}

To delete a chart by using the {{site.data.keyword.cloud_notm}} console, complete the following steps.

1. Log in to the {{site.data.keyword.cloud_notm}} console [https://cloud.ibm.com/login](https://cloud.ibm.com/login){: external} with your IBMid.
2. If you have multiple {{site.data.keyword.cloud_notm}} accounts, select the account and region that you want to use from the account menu.
3. Click the **Navigation menu** icon, then click **Container Registry**.
4. Click **Images**. A list of your charts (and images if they exist) is displayed. The registry stores different artifact types that include Helm charts and container images.
5. In the row that contains the chart that you want to delete, select the checkbox.
6. Click **Delete Image**.

## Listing charts in the trash
{: #registry_helm_charts_list_trash}
{: help}
{: support}

You can list deleted charts that are in the trash and see when they expire.

To find out which charts are in the trash, you can use the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command. Charts are stored in the trash for 30 days.

To list the charts in the trash, complete the following steps.

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. List the charts in the trash by running the following command.

    ```txt
    ibmcloud cr trash-list
    ```
    {: pre}

3. List only the charts in the trash for the namespace that you're interested in by running the following command, where `<namespace>` is your namespace.

    ```txt
    ibmcloud cr trash-list --restrict <namespace>
    ```
    {: pre}

## Restoring charts
{: #registry_helm_charts_restore}
{: help}
{: support}

You can restore charts from the trash. Deleted charts are stored in the trash for 30 days.

You can restore a chart from the trash by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command. To find out which charts are in the trash, run the [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list) command.

You can restore charts by running the [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore) command. You can use the following options:

- `<repo>@<digest>`, which restores the digest and all its tags in the repository that aren't already in the live repository, see [Restoring charts by digest](#registry_helm_charts_restore_digest).
- `<repo>:<tag>`, which restores the tag, see [Restoring charts by tag](#registry_helm_charts_restore_tag).

### Restoring charts by digest
{: #registry_helm_charts_restore_digest}
{: help}
{: support}

When you restore a chart by digest, the digest is moved from the trash into your live repository, and all the tags for that digest in the repository are restored.

To restore a chart by digest from the trash, complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. List the charts in the trash by running the following command.

    ```txt
    ibmcloud cr trash-list
    ```
    {: pre}

    A table is displayed that shows the items in the trash. The table shows the digest, the days until expiry, and the tags for that digest.

3. Note the digest for the chart that you want to restore.
4. Run the following command to restore the chart to your repository. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, and `<digest>` is the digest of the chart that you want to restore.

    ```txt
    ibmcloud cr image-restore <dns>/<namespace>/<repo>@<digest>
    ```
    {: pre}

    If some tags aren't restored, see [Why aren't all tags restored when I restore by digest?](/docs/Registry?topic=Registry-troubleshoot-image-restore-digest).
    {: tip}

    In your live repository, you can pull the chart by digest. If you run the [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) command, the chart shows in the output.
    {: tip}

### Restoring charts by tag
{: #registry_helm_charts_restore_tag}
{: help}
{: support}

When you restore a chart by tag, only that specific tag is moved out of the trash into your live repository.

To restore a chart by tag from the trash, complete the following steps.

1. Log in to {{site.data.keyword.cloud_notm}} by running the `ibmcloud login` command.
2. List the charts in the trash by running the following command.

    ```txt
    ibmcloud cr trash-list
    ```
    {: pre}

    A table is displayed that shows the items in the trash. The table shows the digest, the days until expiry, and the tags for that digest.

3. For the chart that you want to restore, make a note of the digest up to, but not including, the at sign (`@`). This part of the digest is `<dns>/<namespace>/<repo>`, where `<dns>` is the domain name, `<namespace>` is the namespace, and `<repo>` is the repository.
4. For the chart that you want to restore, make a note of the tag, `<tag>`.
5. Run the following command to restore the chart to your repository, where `<dns>/<namespace>/<repo>` is the name of the chart that you want to restore and `<tag>` is the tag.

    ```txt
    ibmcloud cr image-restore <dns>/<namespace>/<repo>:<tag>
    ```
    {: pre}

    In your live repository, you can pull the chart by tag.

    If you run the `ibmcloud cr trash-list` command, the digest and any other tags show in the output, but the tag is no longer displayed.
    {: tip}

## Deleting a private repository and any associated charts
{: #registry_helm_charts_repo_remove}
{: help}
{: support}

You can delete private repositories that are no longer required, and any associated charts, by using the {{site.data.keyword.cloud_notm}} console.

When you delete a repository, all charts in that repository are deleted. This action can't be undone.
{: important}

Before you begin, you must back up any charts that you want to keep.
{: tip}

To delete a private repository by using the {{site.data.keyword.cloud_notm}} console, complete the following steps.

1. Log in to the {{site.data.keyword.cloud_notm}} console [https://cloud.ibm.com/login](https://cloud.ibm.com/login){: external} with your IBMid.
2. If you have multiple {{site.data.keyword.cloud_notm}} accounts, select the account and region that you want to use from the account menu.
3. Click the **Navigation menu** icon, then click **Container Registry**.
4. Click **Repositories**. A list of your private repositories is displayed.
5. In the row that contains the private repository that you want to delete, select the checkbox.

    Ensure that the correct repository is selected because this action can't be undone.
    {: important}

6. Click **Delete Repository**.
