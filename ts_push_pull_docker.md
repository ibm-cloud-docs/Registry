---

copyright:
  years: 2017, 2022
lastupdated: "2022-04-13"

keywords: error, registry, push, Docker image, pull, Docker image, quota, pricing plan, pull traffic, storage quota

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I push or pull a Docker image?
{: #troubleshoot-push-pull-docker}
{: troubleshoot}
{: support}

Pushing or pulling a Docker image fails when you are using {{site.data.keyword.registrylong}}.
{: shortdesc}

When you run commands to push or pull Docker images, you receive an error message. The error message varies depending on the root cause. The following error messages are potential error messages that you might receive:
{: tsSymptoms}

```txt
You have exceeded your storage quota. Delete one or more images,
or review your storage quota and pricing plan
```
{: screen}

```txt
You have exceeded your pull traffic quota for the current month.
Review your pull traffic quota and pricing plan
```
{: screen}

```txt
unauthorized: authentication required
```
{: screen}

```txt
denied: requested access to the resource is denied
```
{: screen}

The following alternatives are possible causes:
{: tsCauses}

- Docker is not installed.
- The Docker client is not logged in to {{site.data.keyword.registrylong_notm}}.
- Your {{site.data.keyword.cloud_notm}} [access token](x2113001){: term} expired.
- You exceeded the quota limit for storage or pull traffic that is set for your {{site.data.keyword.cloud_notm}} account.

You can fix this problem in the following ways:
{: tsResolve}

- [Ensure that Docker is installed on your computer](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install).
- Check your Docker installation path.
- Log in to {{site.data.keyword.cloud_notm}} by running `ibmcloud login`. Then, log in to the {{site.data.keyword.registrylong_notm}} CLI by running [`ibmcloud cr login`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_login).
- [Review quota limits and usage](/docs/Registry?topic=Registry-registry_quota#registry_quota_get).


