---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-25"

keywords: error, registry, push, Docker image, pull, Docker image, quota, pricing plan, pull traffic, storage quota

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I push or pull a Docker image when I'm using {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-push-pull-docker}
{: troubleshoot}
{: support}

When you're using {{site.data.keyword.registrylong}}, pushing or pulling a Docker image fails. You might receive various messages, for example, about being over quota or invalid credentials.
{: shortdesc}

When you run commands to push or pull Docker images, you receive an error message. The error message varies depending on the root cause. The following error messages are potential error messages that you might receive:
{: tsSymptoms}

- **Scenario A.** `unauthorized: authentication required`
- **Scenario B.** `denied: You are not authorized to access the specified resource.`
- **Scenario C.** `unauthorized: An error occurred when authenticating your request with IBM Cloud. Clear your browser cookies, log in to IBM Cloud, and try your request again.`
- **Scenario D.** `Your account has exceeded its pull traffic quota for the current month.`, see [Why am I getting errors about my quota?](/docs/Registry?topic=Registry-troubleshoot-quota) for assistance.
- **Scenario E.** `Your account has exceeded its image storage quota for the current month.`, see [Why am I getting errors about my quota?](/docs/Registry?topic=Registry-troubleshoot-quota) for assistance.

The following alternatives are possible causes:
{: tsCauses}

For scenarios A, B, and C:

- Docker is not installed.
- The Docker client is not logged in to {{site.data.keyword.registrylong_notm}}.
- Your {{site.data.keyword.cloud_notm}} [access token](#x2113001){: term} expired.

You can fix this problem in the following ways:
{: tsResolve}

For scenarios A, B, and C:

- [Ensure that Docker is installed on your computer](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install).
- Check your Docker installation path.
- Log in to {{site.data.keyword.cloud_notm}} by running `ibmcloud login`. Then, log in to the {{site.data.keyword.registrylong_notm}} CLI by running [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login).
