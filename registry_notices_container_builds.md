---

copyright:
  years: 2024
lastupdated: "2024-07-29"

keywords: IBM Cloud Container Registry notices, notices, container builds

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort}} is deprecating container builds - act by 6 September 2021
{: #registry_notices_container_builds}

The container build capability of {{site.data.keyword.registrylong}} is deprecated and is being replaced by {{site.data.keyword.contdelivery_full}} capabilities. You must take action by 6 September 2021.
{: shortdesc}

The `ibmcloud cr build` command, which builds an image in {{site.data.keyword.cloud_notm}} and pushes it to [{{site.data.keyword.registryshort}}](https://www.ibm.com/products/container-registry){: external}, is now deprecated. To build images and push them to {{site.data.keyword.registryshort}} from the command line, a tool like [Docker](https://docs.docker.com/engine/reference/commandline/cli/){: external} can be used instead.

## What you need to know about this change
{: #registry_notices_container_builds_know}

It is common to use the `ibmcloud cr build` command in a DevOps pipeline. In [{{site.data.keyword.contdelivery_short}}](https://www.ibm.com/products/continuous-delivery){: external}, you can use either [Classic pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-deliverypipeline_about) or [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-tekton-pipelines) to build container images, but you must update existing pipelines to replace the `ibmcloud cr build` command.

The {{site.data.keyword.registryshort}} job type in a Classic pipeline uses the `ibmcloud cr build` command from the job's build script. Several of the toolchain templates use this script to build container images. An alternative, which uses [moby buildkit](https://github.com/moby/buildkit){: external} instead of the `ibmcloud cr build` command, is under development. This alternative will be available before the `ibmcloud cr build` command is removed from {{site.data.keyword.registryshort}}. Detailed instructions for migrating your pipeline will be available then. For more information about building container images, including migration steps when they are available, see [Building container images](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images).

The {{site.data.keyword.contdelivery_short}} service also provides several Tekton tasks that you can reference from your Tekton pipelines to build container images. If you use the `ibmcloud cr build` command directly or reference the provided [`icr-cr-build`](https://github.com/open-toolchain/tekton-catalog/blob/master/container-registry/README.md#icr-cr-build){: external} task, you can migrate to one of three other [Tekton](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) tasks to build container images.

## What actions you must take by 6 September 2021
{: #registry_notices_container_builds_action}

By 6 September 2021, users of {{site.data.keyword.registrylong_notm}} will need to add the `–accept-deprecation` option to the `ibmcloud cr build` command. The new option is available in the container-registry plug-in version 0.1.543 and will be required for continued operation from 6 September 2021 onward. {{site.data.keyword.registrylong_notm}} container build service will have an end of service date of 5 October 2021.

## Learn more
{: #registry_notices_container_builds_learn}

For more information about migrating your existing pipelines, see the {{site.data.keyword.contdelivery_short}} documentation about [building container images](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images), or [get started with the {{site.data.keyword.contdelivery_short}} service](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started).

## Original announcement
{: #registry_notices_container_builds_announce}

The original announcement that this notification mirrors is [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/blog/announcement/ibm-cloud-container-registry-deprecating-container-builds/){: external} and it was published on 6 October 2020.
