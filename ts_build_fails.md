---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-10"

keywords: troubleshooting, support, help, errors, problems, ts, registry, build, build fails

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the `ibmcloud cr build` command fail?
{: #troubleshoot-build-fails}
{: troubleshoot}
{: support}

The {{site.data.keyword.registrylong}} build command fails.
{: shortdesc}

The `ibmcloud cr build` build command fails.
{: tsSymptoms}

The server might be down or issues might exist in your Dockerfile.
{: tsCauses}

To find out what the cause is, run `docker build` locally with the appropriate [`docker build` options](https://docs.docker.com/engine/reference/commandline/build/){: external}:
{: tsResolve}

```
docker build --no-cache .
```
{:  pre}

- If the local build doesn't work, check for issues with your Dockerfile.
- If the local build works, contact {{site.data.keyword.cloud}} support, see [Using the Support Center](/docs/get-support?topic=get-support-using-avatar).

The [`ibmcloud cr build`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) command is deprecated from 6 October 2020. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead. For more information, see the [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecating-container-builds){: external} blog post.
{: deprecated}


