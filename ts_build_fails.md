---

copyright:
  years: 2017, 2020
lastupdated: "2020-10-13"

keywords: troubleshooting, support, help, errors, problems, ts, registry, build, build fails

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

# Why is the `ibmcloud cr build` command failing?
{: #troubleshoot-build-fails}
{: troubleshoot}
{: support}

The {{site.data.keyword.registrylong}} build command fails.
{: shortdesc}

{: tsSymptoms}
The `ibmcloud cr build` build command fails.

{: tsCauses}
The server might be down or there might be issues with your Dockerfile.

{: tsResolve}
To find out what the cause is, run `docker build` locally with the appropriate [`docker build` options](https://docs.docker.com/engine/reference/commandline/build/){: external}:

```
docker build --no-cache .
```
{:  pre}

- If the local build doesn't work, check for issues with your Dockerfile.
- If the local build works, contact {{site.data.keyword.cloud}} support, see [Using the Support Center](/docs/get-support?topic=get-support-using-avatar).

The [`ibmcloud cr build`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) command is deprecated from 6 October 2020. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead. For more information, see [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecating-container-builds){: external}.
{: deprecated}
