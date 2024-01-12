---

copyright:
  years: 2017, 2024
lastupdated: "2024-01-12"

keywords: error, registry, push, Docker image, pull, Docker image, quota, pricing plan, pull traffic, storage quota

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I push or pull a Docker image?
{: #troubleshoot-push-pull-docker}
{: troubleshoot}
{: support}

When you're using {{site.data.keyword.registrylong}}, pushing or pulling a Docker image fails. You might receive various messages, for example, about being over quota or invalid credentials.
{: shortdesc}

When you run commands to push or pull Docker images, you receive an error message. The error message varies depending on the root cause. The following error messages are potential error messages that you might receive:
{: tsSymptoms}

```txt
Your account has exceeded its image storage quota for the current month. See https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-quota
```
{: screen}

```txt
Your account has exceeded your pull traffic quota for the current month. See https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-quota
```
{: screen}

```txt
unauthorized: authentication required
```
{: screen}

```txt
You are not authorized to access the specified resource.
```
{: screen}

```txt
An error occurred when authenticating your request with IBM Cloud. Clear your browser cookies, log in to IBM Cloud, and try your request again.
```
{: screen}

The following alternatives are possible causes:
{: tsCauses}

- Docker is not installed.
- The Docker client is not logged in to {{site.data.keyword.registrylong_notm}}.
- Your {{site.data.keyword.cloud_notm}} [access token](#x2113001){: term} expired.
- You exceeded the quota limit for storage or pull traffic that is set for your {{site.data.keyword.cloud_notm}} account.
- You're on a free plan and you need to upgrade to a standard plan.

You can fix this problem in the following ways:
{: tsResolve}

- [Ensure that Docker is installed on your computer](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install).
- Check your Docker installation path.
- Log in to {{site.data.keyword.cloud_notm}} by running `ibmcloud login`. Then, log in to the {{site.data.keyword.registrylong_notm}} CLI by running [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login).
- [Review quota limits and usage](/docs/Registry?topic=Registry-registry_quota#registry_quota_get). For more information, see [Staying within quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup).
- Upgrade to a standard plan. For more information, see [Upgrading your service plan](/docs/Registry?topic=Registry-registry_overview#registry_plan_upgrade).
