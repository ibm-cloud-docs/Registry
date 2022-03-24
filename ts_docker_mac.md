---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-24"

keywords: troubleshoot, error, problem, registry, docker login, mac, credentials, error saving credentials, error storing credentials, user name or passphrase you entered is not correct

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is Docker login on my Mac failing?
{: #troubleshoot-docker-mac}
{: troubleshoot}
{: support}

When you're using {{site.data.keyword.registrylong}}, Docker login fails on a Mac with the following message `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct'`.
{: shortdesc}

You receive the following error message when you try to run the [`ibmcloud cr login`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_login) command on a Mac:
{: tsSymptoms}

```txt
Error saving credentials: error storing credentials - err: exit status 1, out: 
'The user name or passphrase you entered is not correct.'
```
{: screen}

Docker for Mac has a problem that prevents your credentials from being stored in the macOS keychain.
{: tsCauses}

You might be able to resolve the problem by restarting your Mac. If the restart doesn't solve the problem, you can disable the storage of logins in your Mac keychain:
{: tsResolve}

1. In your menu, click the **Docker** icon, select **Preferences**.
2. Clear the **Securely store Docker logins in macOS keychain** checkbox.


