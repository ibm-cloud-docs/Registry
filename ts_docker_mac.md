---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-16"

keywords: troubleshooting, support, help, errors, problems, ts, registry, docker login, mac, docker login fails on a mac

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

# Why does Docker login fail on my Mac?
{: #troubleshoot-docker-mac}
{: troubleshoot}
{: support}

When you're using {{site.data.keyword.registrylong}}, Docker login fails on a Mac with the message: `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`
{: shortdesc}

{: tsSymptoms}
You receive the following error message when you try to run the `ibmcloud cr login` command on a Mac: `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`

{: tsCauses}
Docker for Mac has a problem that prevents your credentials from being stored in the macOS keychain.

{: tsResolve}
You might be able to resolve the problem by rebooting your Mac. If rebooting your Mac doesn't work, you can disable the storage of logins in your Mac keychain:

1. In your menu, click the **Docker** icon, select **Preferences**.
2. Clear the **Securely store Docker logins in macOS keychain** checkbox.
