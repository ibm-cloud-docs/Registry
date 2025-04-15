---

copyright:
  years: 2023, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, vulnerability advisor, change, update, actions, sdk, code, api, cli, version 4, version 3

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Vulnerability Advisor version 3 is being discontinued on 13 November 2023
{: #registry_notices_va_v3}

The version of the Vulnerability Advisor component of {{site.data.keyword.registrylong}} has been updated. Vulnerability Advisor version 4 is now the default. Vulnerability Advisor version 3 is already [deprecated](/docs/Registry?topic=Registry-registry_notices_va_v4) and is discontinued from 13 November 2023. If you are still using version 3, you must update to Vulnerability Advisor version 4 by 13 November 2023. If you are already using version 4, no action is required.
{: shortdesc}

The original announcement was published on 11 October 2023.
{: note}

## What you need to know about this change
{: #notices_va_v3_change}

If you use the {{site.data.keyword.cloud_notm}} console to access Vulnerability Advisor, no action is required. The {{site.data.keyword.cloud_notm}} console is automatically updated to Vulnerability Advisor version 4.

If you use the {{site.data.keyword.cloud_notm}} CLI, you must update the `container-registry` CLI plug-in to version 1.0.0, or later, by 13 November 2023. Updating the `container-registry` CLI plug-in to 1.0.0, or later, enables the `ibmcloud cr va` command and the `--va` option on the `ibmcloud cr images` and `ibmcloud cr digests` commands to work with Vulnerability Advisor version 4. On 13 November 2023, any {{site.data.keyword.registryshort}} CLI commands that access Vulnerability Advisor version 3 cease to work.

If you have explicitly run the `ibmcloud cr va-version-set v3` command previously, you must set the version to version 4.

If you use the Vulnerability Advisor REST API to access Vulnerability Advisor, you must update your client call from `/va/api/v3` APIs to `/va/api/v4` APIs.

You must be using version 1.0.0, or later, of the SDK.

Any exemptions that you previously defined for version 3 continue to work. However, the security notice value that comes back in Vulnerability Advisor version 4 might not be the same as for Vulnerability Advisor version 3 because different sources of data are used. Therefore, if the returned value isn't the same as for Vulnerability Advisor version 3, you might have to update any existing exemptions that specify a security notice. Exemptions that are defined by CVE value are unaffected.

Differences in Vulnerability Advisor version 4 behavior are documented in [About Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui#about).

## What actions you must take by 13 November 2023
{: #notices_va_v3_action}

To update to Vulnerability Advisor version 4, complete the following steps:

1. Ensure that you are using version 1.0.0, or later, of the `container-registry` CLI plug-in. To update the plug-in, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).

2. If required, set the Vulnerability Advisor version to version 4 by running the following command:

    ```txt
    ibmcloud cr va-version-set v4
    ```
    {: pre}

3. If required, update any existing exemptions that specify a security notice.

4. Update any code to reference the version 4 APIs.

5. Ensure that you are using version 1.0.0, or later, of the SDK, see [`container-registry-go-sdk`](https://github.com/IBM/container-registry-go-sdk/releases){: external}.
