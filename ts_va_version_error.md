---

copyright:
  years: 2023
lastupdated: "2023-12-15"

keywords: error, va, vulnerability advisor, v3, version 3, version 4, invalid version, CRC0589E

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get an error about an invalid version of Vulnerability Advisor being specified?
{: #troubleshoot-va-version-error}
{: troubleshoot}
{: support}

You tried to set Vulnerability Advisor to an invalid version, for example, version 3 in {{site.data.keyword.registrylong}}. Version 3 is discontinued. For example, `CRC0589E Invalid Vulnerability Advisor version v3 specified.`
{: shortdesc}

When you try to set the version of Vulnerability Advisor to version 3 `v3`, you get the following message.
{: tsSymptoms}

```txt
$ ibmcloud cr va-version-set v3
FAILED
CRC0589E Invalid Vulnerability Advisor version v3 specified. Specify a valid version or, to list the available versions, re-run the command with no parameters. See https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-va-version-error
```
{: screen}

You are trying to use a discontinued version of Vulnerability Advisor.
{: tsCauses}

Version 3 of Vulnerability Advisor is discontinued from 13 November 2023. Vulnerability Advisor version 4 is now the default. You must update to Vulnerability Advisor version 4.
{: tsResolve}

To update to version 4, run the following command.

```txt
ibmcloud cr va-version-set v4
```
{: pre}

For more information about how to update to Vulnerability Advisor version 4, see [Vulnerability Advisor version 3 is being discontinued on 13 November 2023](/docs/Registry?topic=Registry-registry_notices_va_v3). For more information about the versions of Vulnerability Advisor, see [Does Vulnerability Advisor have versions?](/docs/Registry?topic=Registry-registry_faq#faq_va_versions) and [Setting the Vulnerability Advisor version](/docs/Registry?topic=Registry-va_index&interface=ui#va_set_version).
