---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, va, v2, deprecation, vulnerability advisor

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Vulnerability Advisor version 2 API is being discontinued on 8 January 2019
{: #registry_notices_va_v2_dep}

Version 2 of the {{site.data.keyword.registrylong}} Vulnerability Advisor API will be discontinued on 8 January 2019. You must update any automation to use version 3 of the API.
{: shortdesc}

The original announcement was published on 4 December 2018.
{: note}

Vulnerability Advisor is a component of the {{site.data.keyword.registrylong_notm}} offering, which scans Docker images that are stored in your registry for known vulnerabilities and configuration issues.

## What is changing?
{: #registry_notices_va_v2_dep_change}

Effective 8 January 2019, version 2 of Vulnerability Advisor’s API will be discontinued and will no longer be usable. You must start to use version 3 of the API as soon as possible.

## End of support Date: 8 January 2019
{: #registry_notices_va_v2_dep_eos}

- All existing API calls that use version 2 continue to work until the end of support.
- Any API call that uses version 2 after the end of support fails.
- Before the end of support, update any automation to use version 3 of the API.
