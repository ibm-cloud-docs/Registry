---

copyright:
  years: 2022, 2023
lastupdated: "2023-12-18"

keywords: change log, cli, versions, change log for Container Registry CLI, updates to Container Registry CLI

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort}} CLI change log
{: #registry_cli_change_log}

In this change log, you can learn about the most recent changes, improvements, and updates for the {{site.data.keyword.registrylong}} CLI.
{: shortdesc}

For more information about how to update the {{site.data.keyword.registryshort}} CLI, see [Updating the container-registry CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).

Version 0.1 of the {{site.data.keyword.registryshort}} CLI is deprecated, see [All releases of {{site.data.keyword.registryshort}} plug-in 0.1 are deprecated](/docs/Registry?topic=Registry-registry_release_notes#15sep2022_v0).
{: deprecated}

## Version 1.3.5
{: #cli-change-logv1-135}

Version 1.3.5 of the CLI was released on 18 December 2023.

This release has the following changes:

- Vulnerability remediation for PVR0478945.
- Updated translations.

## Version 1.3.4
{: #cli-change-logv1-134}

Version 1.3.4 of the CLI was released on 14 November 2023.

This release has the following changes:

- Improved the error message for the [`ibmcloud cr va-version-set`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set) command.
- Updated translations.

## Version 1.3.1
{: #cli-change-logv1-131}

Version 1.3.1 of the CLI was released on 31 August 2023.

This release has the following changes:

- Adds a `--force` option to the [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=Registry-containerregcli&locale=en#bx_cr_retention_policy_set) command so that you can immediately apply and run the policy without user prompts.
- Vulnerability remediation for the CVE with the ID `CVE-2023-3978`.

## Version 1.2.2
{: #cli-change-logv1-122}

Version 1.2.2 of the CLI was released on 24 July 2023.

This release has the following changes:

- Added a JSON output option, `--output json` or `-o json`, to several commands.
- [Deprecated]{: tag-deprecated} The `--json` option is deprecated and is replaced with the `--output json` option.
- Updated translations.

For more information about the commands for which the JSON format option is available, see [JSON output option added to several {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=Registry-registry_release_notes#registry-24jul2023).

## Version 1.1.0
{: #cli-change-logv1-110}

Version 1.1.0 of the CLI was released on 7 July 2023.

This release has the following changes:

- Fixes a Vulnerability Advisor versioning defect that affected some commands.

## Version 1.0.11
{: #cli-change-logv1-1011}

Version 1.0.11 of the CLI was released on 19 June 2023.

This release has the following changes:

- The backup default Vulnerability Advisor version is now version 4.
- Vulnerability remediations.
- Updated translations.

## Version 1.0.8
{: #cli-change-logv1-108}

Version 1.0.8 of the CLI was released on 5 April 2023.

This release has the following changes:

- Vulnerability remediations.
- Updated translations.
- Updated error messages.

## Version 0.1.587
{: #cli-change-log-01587}

Version 0.1.587 of the CLI was released on 26 January 2023.

This release has the following changes:

- Vulnerability remediations.

## Version 1.0.6
{: #cli-change-logv1-106}

Version 1.0.6 of the CLI was released on 25 January 2023.

This release has the following changes:

- Vulnerability remediations.

## Version 1.0.5
{: #cli-change-logv1-105}

Version 1.0.5 of the CLI was released on 5 December 2022.

This release has the following changes:

- Vulnerability remediations.
- Updated translations.
- You can install and uninstall the container-registry plug-in by using the `cr` alias.

## Version 0.1.585
{: #cli-change-log-01585}

Version 0.1.585 of the CLI was released on 5 December 2022.

This release has the following changes:

- Vulnerability remediations.

## Version 1.0.2
{: #cli-change-logv1-102}

Version 1.0.2 of the CLI was released on 19 October 2022.

This release has the following changes:

- Minor bug fixes.
- Vulnerability remediations.
- Updated translations.

## Version 0.1.584
{: #cli-change-log-01584}

Version 0.1.584 of the CLI was released on 19 October 2022.

This release has the following changes:

- Updated translations.

## Version 1.0.1
{: #cli-change-logv1-101}

Version 1.0.1 of the CLI was released on 23 September 2022.

This release has the following changes:

- Vulnerability remediations.
- Updated translations.

## Version 0.1.583
{: #cli-change-log-01583}

Version 0.1.583 of the CLI was released on 23 September 2022.

This release has the following changes:

- Vulnerability remediations.
- Updated translations.

## Version 1.0.0
{: #cli-change-logv1-100}

Version 1.0.0 of the CLI was released on 15 September 2022.

This release has the following changes:

- Vulnerability Advisor v4 is now available, see [Vulnerability Advisor 4 is available from {{site.data.keyword.registryshort}} plug-in 1.0.0](/docs/Registry?topic=Registry-registry_release_notes#15sep2022_va_version_4).
- Image and digest list output no longer includes security status by default. You can either add the `--va` argument to include security status for all the listed images, or you can use the `ibmcloud cr va` command to query security status for an individual image.

## Version 0.1.582
{: #cli-change-log-01582}

Version 0.1.582 of the CLI was released on 15 September 2022.

This release has the following changes:

- Vulnerability remediations.
