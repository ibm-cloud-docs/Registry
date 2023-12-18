---

copyright:
  years: 2021, 2023
lastupdated: "2023-12-18"

keywords: registry, login, push, pull, iam session, iam

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the {{site.data.keyword.registryshort}} login keep expiring?
{: #troubleshoot-login-expire}
{: troubleshoot}
{: support}

Logging in to {{site.data.keyword.registrylong}} by using the [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login) command is subject to IAM login session limits.
{: shortdesc}

Pushes and pulls to the registry fail after a period of inactivity. The following example is a typical scenario:
{: tsSymptoms}

1. You log in by using the `ibmcloud cr login` command, and then you push or pull an image.
2. You don't run any other commands for a length of time that is longer than the IAM session inactivity limit.
3. Without logging in again, you try to push or pull an image and the command fails.

When you log in by using the `ibmcloud cr login` command, you are subject to the IAM session limits, see [Setting limits for login sessions](/docs/account?topic=account-iam-work-sessions).
{: tsCauses}

You can mitigate the issue by taking one of the following actions:
{: tsResolve}

- Log in by using an IAM [API key](#x8051010){: term} because this key is not subject to the IAM session expiry, see [Using Docker to authenticate with an API key](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth_docker).
- Change the IAM login session limits to better suit your needs, see [Setting limits for login sessions](/docs/account?topic=account-iam-work-sessions). The longer you set the limits, the longer your {{site.data.keyword.registrylong_notm}} login lasts for.
