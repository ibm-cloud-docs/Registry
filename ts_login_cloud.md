---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-10"

keywords: troubleshooting, support, help, errors, problems, ts, registry, log in, login fails

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get a failure message when I run any command in {{site.data.keyword.registrylong_notm}}?
{: #troubleshoot-login-cloud}
{: troubleshoot}
{: support}

You can't run any commands in {{site.data.keyword.registrylong}}, even though you are logged in to {{site.data.keyword.cloud_notm}}. You get the following message: `FAILED You are not logged in to IBM Cloud`.
{: shortdesc}

All `ibmcloud cr` commands fail.
{: tsSymptoms}

The `container-registry` CLI plug-in is out of date and needs updating.
{: tsCauses}

Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
{: tsResolve}


