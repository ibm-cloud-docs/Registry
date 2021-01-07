---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-06"

keywords: troubleshooting, support, help, errors, problems, ts, registry, adding images to the registry, passport advantage, ppa, IBM images, ppa import, helm charts

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

# Why can't I add other {{site.data.keyword.IBM_notm}} images to the registry?
{: #troubleshoot-ppa}
{: troubleshoot}
{: support}

You're unable to add other {{site.data.keyword.IBM}} images to {{site.data.keyword.registrylong}}.
{: shortdesc}

{: tsSymptoms}
When you try to import content that you used in other {{site.data.keyword.IBM_notm}} products, such as {{site.data.keyword.cloud}} Private, you are not able to store your images and other licensed software from [{{site.data.keyword.IBM_notm}} Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external} in the registry.

{: tsCauses}
Software packages such as images and Helm charts from {{site.data.keyword.IBM_notm}} Passport Advantage must be imported to the registry with the [`ibmcloud cr ppa-archive-load`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load) command.

{: tsResolve}
Before you begin to import a product from {{site.data.keyword.IBM_notm}} Passport Advantage, complete the following tasks:

1. Log in to {{site.data.keyword.cloud_notm}} by running `ibmcloud login [--sso]`.
2. Log in to {{site.data.keyword.registrylong_notm}} by running `ibmcloud cr login`.
3. [Target the `kubectl` CLI](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) to your cluster.
4. If you have not already set up Helm in your cluster, [set up Helm in your cluster now](/docs/containers?topic=containers-helm#helm).
5. If you want to share the charts within your organization, you can install the [Chart Museum open source project](https://github.com/helm/charts/tree/master/stable/chartmuseum){: external}.

## Importing {{site.data.keyword.IBM_notm}} Passport Advantage products to use in {{site.data.keyword.cloud_notm}}
{: #troubleshoot-ppa-import}

Importing images to use in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

1. Obtain the compressed file that you want to import from [{{site.data.keyword.IBM_notm}} Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}.

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

   If you want to upload Helm charts from the {{site.data.keyword.IBM_notm}} Passport Advantage archive to a chart museum, include the following options in the command: `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
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
