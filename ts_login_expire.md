---

copyright:
  years: 2021
lastupdated: "2021-04-09"

keywords: troubleshooting, support, help, errors, problems, ts, registry, login expire

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

# Why does the {{site.data.keyword.registrylong_notm}} login keep expiring?
{: #troubleshoot-login-expire}
{: troubleshoot}
{: support}

Logging in to {{site.data.keyword.registrylong}} by using the `ibmcloud cr login` command is subject to IAM login session limits.
{: shortdesc}

{: tsSymptoms}
Pushes and pulls to the registry fail after a period of inactivity. The following example is a typical scenario:

1. You log in by using the `ibmcloud cr login` command, and then you push or pull an image.
2. You don't run any other commands for a length of time that is longer than the IAM session inactivity limit.
3. Without logging in again, you try to push or pull an image and the command fails.

{: tsCauses}
When you log in by using the `ibmcloud cr login` command, you are subject to the IAM session limits, see [Setting limits for login sessions](/docs/account?topic=account-iam-work-sessions).

{: tsResolve}
You can mitigate the issue by taking one of the following actions:

- Log in by using an IAM API key because this key is not subject to the IAM session expiry, see [Using Docker to authenticate with an API key](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth_docker).
- Change the IAM login session limits to better suit your needs, see [Setting limits for login sessions](/docs/account?topic=account-iam-work-sessions). The longer you set the limits, the longer your {{site.data.keyword.registrylong_notm}} login lasts for.
