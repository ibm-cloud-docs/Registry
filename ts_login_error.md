---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, log in, login fails, not a registered command, registered command, command fails

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

# Why are all the {{site.data.keyword.registrylong_notm}} commands failing?
{: #troubleshoot-login-error}
{: troubleshoot}
{: support}

You can't run any {{site.data.keyword.registrylong}} `ibmcloud cr` commands, they are failing with the message: `'cr' is not a registered command. See 'ibmcloud help'`.
{: shortdesc}

{: tsSymptoms}
You're trying to run an `ibmcloud cr` command, but you receive an error message similar to one of the following error messages:

```
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

```
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

{: tsCauses}
The `container-registry` CLI plug-in is not installed.

{: tsResolve}
Install the `container-registry` CLI plug-in, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).
