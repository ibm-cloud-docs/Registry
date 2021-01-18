---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, log in, login fails

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

# Why can't I log in to {{site.data.keyword.registrylong_notm}}?
{: #troubleshoot-login}
{: troubleshoot}
{: support}

Logging in to {{site.data.keyword.registrylong}} fails.
{: shortdesc}

{: tsSymptoms}
The `ibmcloud cr login` command fails.

{: tsCauses}
The following alternatives are possible causes:

- The `container-registry` CLI plug-in is out of date and needs updating.
- Docker is not installed on your local computer, or is not running.
- Your {{site.data.keyword.cloud_notm}} login credentials have expired.

{: tsResolve}
You can fix this problem in the following ways:

- Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
- Ensure that Docker is installed on your computer. If it is already installed, restart the Docker daemon.
- Rerun the `ibmcloud login` command to refresh your {{site.data.keyword.cloud_notm}} login credentials.
