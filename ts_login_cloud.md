---

copyright:
  years: 2017, 2024
lastupdated: "2024-01-12"

keywords: registry, fail, command, container-registry, CLI, plug-in, you are not logged in to IBM Cloud, failed, CRC0016E

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do commands fail saying that I'm not logged in?
{: #troubleshoot-login-cloud}
{: troubleshoot}
{: support}

You are logged in to {{site.data.keyword.cloud_notm}} but you can't run any commands in {{site.data.keyword.registrylong}}. You get the following message: `CRC0016E FAILED You are not logged in to IBM Cloud`.
{: shortdesc}

All `ibmcloud cr` commands fail with the message: `CRC0016E FAILED You are not logged in to IBM Cloud`.
{: tsSymptoms}

The `container-registry` CLI plug-in is out of date and needs updating.
{: tsCauses}

Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
{: tsResolve}
