---

copyright:
  years: 2023, 2024
lastupdated: "2024-07-23"

keywords: IBM Cloud Container Registry notices, vulnerability advisor, change, update, actions, sdk, code, api, cli, version 4, version 3

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Update Vulnerability Advisor to version 4 by 19 June 2023
{: #registry_notices_va_v4}

The Vulnerability Advisor component of {{site.data.keyword.registrylong}} is being updated. From 19 June 2023, Vulnerability Advisor version 3 will be replaced as the default by Vulnerability Advisor version 4.
{: shortdesc}

Vulnerability Advisor version 3 is being deprecated as the default on 19 June 2023. From 19 June 2023, the default will be Vulnerability Advisor version 4. If you have version 3 set as the default, you can continue to use version 3 until the end of support date. An end of support date is not available yet.

## What you need to know about this change
{: #notices_va_v4_change}

If you use the {{site.data.keyword.cloud_notm}} console to access Vulnerability Advisor, no action is required. The {{site.data.keyword.cloud_notm}} console is automatically updated to Vulnerability Advisor version 4.

If you use the {{site.data.keyword.cloud_notm}} CLI and you want to use version 4 as the default, you must update the {{site.data.keyword.registryshort}} CLI plug-in to version 1.0.0, or later, by 19 June 2023. Updating the {{site.data.keyword.registryshort}} CLI plug-in to 1.0.0, or later, enables the `ibmcloud cr va` command and the `--va` option on the `ibmcloud cr images` and `ibmcloud cr digests` commands to work with Vulnerability Advisor version 4.

On 19 June 2023, when the default changes to Vulnerability Advisor version 4, the {{site.data.keyword.registryshort}} CLI automatically starts to use this version unless the `ibmcloud cr va-version-set v3` command was run, in which case Vulnerability Advisor version 3 continues to be used. You can use the `ibmcloud cr va-version` command to determine which Vulnerability Advisor version is in use and the `ibmcloud cr va-version-set v4` command to switch to Vulnerability Advisor version 4. When Vulnerability Advisor version 3 reaches its end of support date, any {{site.data.keyword.registryshort}} CLI commands that access Vulnerability Advisor version 3 cease to work. An end of support date is not available yet.

If you use the Vulnerability Advisor REST API to access Vulnerability Advisor, you must update your client call from `/va/api/v3` APIs to `/va/api/v4` APIs.

If you use one of the Vulnerability Advisor version 3 SDKs to access Vulnerability Advisor, you must update to the Vulnerability Advisor version 4 SDK.

Any exemptions that you previously defined continue to work. However, the security notice value that comes back in Vulnerability Advisor version 4 might not be the same as for Vulnerability Advisor version 3 because different sources of data are used. Therefore, if the returned value isn't the same as for Vulnerability Advisor version 3, you might have to update any existing exemptions that specify a security notice. {{site.data.keyword.redhat_full}} security notices are unaffected. Exemptions that are defined by CVE value are also unaffected.

Differences in Vulnerability Advisor version 4 behavior are documented in [About Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui#about).

## What actions you must take by 19 June 2023
{: #notices_va_v4_action}

You can choose whether to update to use version 4, the default, or to continue to use version 3, which is deprecated.

- If you want to use Vulnerability Advisor version 4 as the default, update the following items as described in [What you need to know about this change](#notices_va_v4_change):

    - The {{site.data.keyword.registryshort}} CLI plug-in and, if you have explicitly run the `ibmcloud cr va-version-set v3` command previously, run the following command.

        ```txt
        ibmcloud cr va-version-set v4
        ```
        {: pre}

    - Any code that calls Vulnerability Advisor version 3 either through the API or through the SDK.
    - You might have to update any existing exemptions that specify a security notice.

- If you want to continue to use Vulnerability Advisor version 3, run the following command:

    ```txt
    ibmcloud cr va-version-set v3
    ```
    {: pre}

## Original announcement
{: #registry_notices_announce}

The original announcement was published on 19 May 2023.
