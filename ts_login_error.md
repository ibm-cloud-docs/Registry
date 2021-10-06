---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-06"

keywords: troubleshooting, support, help, errors, problems, ts, registry, log in, login fails, not a registered command, registered command, command fails

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do all the {{site.data.keyword.registrylong_notm}} commands fail?
{: #troubleshoot-login-error}
{: troubleshoot}
{: support}

You can't run any {{site.data.keyword.registrylong}} `ibmcloud cr` commands, they are failing with the message: `'cr' is not a registered command. See 'ibmcloud help'`.
{: shortdesc}

You're trying to run an `ibmcloud cr` command, but you receive an error message similar to one of the following error messages:
{: tsSymptoms}

```sh
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

```sh
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

The `container-registry` CLI plug-in is not installed.
{: tsCauses}

Install the `container-registry` CLI plug-in, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).
{: tsResolve}


