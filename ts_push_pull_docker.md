---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, pushing a Docker image fails, pulling a Docker image fails, exceeded quota,

subcollection: Registry

content-type: troubleshoot

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

# Why can't I push or pull a Docker image?
{: #troubleshoot-push-pull-docker}
{: troubleshoot}
{: support}

Pushing or pulling a Docker image fails.
{: shortdesc}

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
- The Docker client is not logged in to {{site.data.keyword.registrylong}}.
- Your {{site.data.keyword.cloud}} access token might have expired.
- You exceeded the quota limit for storage or pull traffic that is set for your {{site.data.keyword.cloud_notm}} account.

{: tsResolve}
You can fix this problem in the following ways:

- [Ensure that Docker is installed on your computer](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install).
- Check your Docker installation path.
- Log in to {{site.data.keyword.cloud_notm}} by running `ibmcloud login`. Then, log in to the {{site.data.keyword.registrylong_notm}} CLI by running `ibmcloud cr login`.
- [Review quota limits and usage for storing and pulling Docker images in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_quota#registry_quota_get).
