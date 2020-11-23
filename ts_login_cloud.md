---

copyright:
  years: 2017, 2020
lastupdated: "2020-11-23"

keywords: troubleshooting, support, help, errors, problems, ts, registry, log in, login fails

subcollection: Registry

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

# Why do I get a failure message when I run any command in {{site.data.keyword.registrylong_notm}}?
{: #troubleshoot-login-cloud}
{: troubleshoot}
{: support}

You can't run any commands in {{site.data.keyword.registrylong}}, even though you are logged in to {{site.data.keyword.cloud_notm}}. You get the following message: `FAILED You are not logged in to IBM Cloud`.
{: shortdesc}

{: tsSymptoms}
All `ibmcloud cr` commands fail.

{: tsCauses}
The `container-registry` CLI plug-in is out of date and needs updating.

{: tsResolve}
Upgrade to the most recent version of the `container-registry` CLI plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
