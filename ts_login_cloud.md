---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-27"

keywords: troubleshoot, error, problem, registry, fail, command, container-registry, CLI, plug-in, you are not logged in to IBM Cloud, failed

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do the {{site.data.keyword.registryshort_notm}} commands fail saying that I'm not logged in?
{: #troubleshoot-login-cloud}
{: troubleshoot}
{: support}

You can't run any commands in {{site.data.keyword.registrylong}}, even though you are logged in to {{site.data.keyword.cloud_notm}}. You get the following message: `FAILED You are not logged in to IBM Cloud`.
{: shortdesc}

All `ibmcloud cr` commands fail with the message: `FAILED You are not logged in to IBM Cloud`.
{: tsSymptoms}

The `container-registry` CLI plug-in is out of date and needs updating.
{: tsCauses}

Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
{: tsResolve}


