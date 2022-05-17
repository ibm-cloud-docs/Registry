---

copyright:
  years: 2017, 2022
lastupdated: "2022-05-17"

keywords: error, registry, not a registered command, registered command, cr, command, ibmcloud cr

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does a `cr` command fail saying that it's not registered?
{: #troubleshoot-login-error}
{: troubleshoot}
{: support}

You can't run any {{site.data.keyword.registrylong}} `ibmcloud cr` commands, they are failing with the message: `'cr' is not a registered command. See 'ibmcloud help'`.
{: shortdesc}

You're trying to run an `ibmcloud cr` command, but you receive an error message similar to one of the following error messages:
{: tsSymptoms}

```txt
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

```txt
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: screen}

The `container-registry` CLI plug-in is not installed.
{: tsCauses}

Install the `container-registry` CLI plug-in, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).
{: tsResolve}


