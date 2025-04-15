---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, container builds, end of support, eos, ibmcloud cr build

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Support for the {{site.data.keyword.registryshort}} container build service ends on 5 October 2021
{: #registry_notices_cont_builds_eos}

As announced on 6 October 2020, the end of support for the {{site.data.keyword.registrylong}} container build service is 5 October 2021.
{: shortdesc}

The original announcement was published on 3 September 2021.
{: note}

## What you need to know
{: #registry_notices_cont_builds_eos_what}

Container builds that use the `ibmcloud cr build` CLI command or the API will stop working on 5 October 2021.

## What actions you need to take
{: #registry_notices_cont_builds_eos_action}

As of 6 September 2021, you must add the `--accept-deprecation` option to any container builds that use the `ibmcloud cr build` command. The `--accept-deprecation` option is available in the container-registry plug-in version v0.1.543. After 6 September 2021, container-registry plug-in version 0.1.543 is required for all container builds.

On or before the end of support date of 5 October 2021, you must replace the build mechanism for any container builds that use the `ibmcloud cr build` command or the build API. For more information, see [{{site.data.keyword.registryshort}} is deprecating container builds - act by 6 September 2021](/docs/Registry?topic=Registry-registry_notices_container_builds).

Changes effective on 05 October 2021.
