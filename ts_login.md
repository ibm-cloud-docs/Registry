---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-05"

keywords: registry, log in, login fails, container-registry, CLI plug-in, login credentials, Docker

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I log in to {{site.data.keyword.registryshort}}?
{: #troubleshoot-login}
{: troubleshoot}
{: support}

Logging in to {{site.data.keyword.registrylong}} fails.
{: shortdesc}

The [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login) command fails.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- **Scenario A.** The `container-registry` CLI plug-in is out of date and needs updating.
- **Scenario B.** Docker is not installed on your local computer, or is not running.
- **Scenario C.** Your {{site.data.keyword.cloud_notm}} login credentials expired.

You can fix this problem in the following ways:
{: tsResolve}

- **Scenario A.** Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
- **Scenario B.** Ensure that Docker is installed on your computer. If it is already installed, restart the Docker daemon.
- **Scenario C.** Rerun the `ibmcloud login` command to refresh your {{site.data.keyword.cloud_notm}} login credentials.
