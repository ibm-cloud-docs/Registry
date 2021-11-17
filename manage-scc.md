---

copyright:
  years: 2021
lastupdated: "2021-11-17"

keywords: Security and compliance for {{site.data.keyword.registrylong_notm}}, security for {{site.data.keyword.registrylong_notm}}, compliance for {{site.data.keyword.registrylong_notm}},

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance with {{site.data.keyword.registrylong_notm}}
{: #manage-security-compliance}

{{site.data.keyword.registrylong}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

- Monitor for controls and goals that are applicable to {{site.data.keyword.registrylong_notm}}.
- Define rules for {{site.data.keyword.registrylong_notm}} that can help to standardize resource configuration.


## Monitoring security and compliance posture with {{site.data.keyword.registrylong_notm}}
{: #monitor-container-registry}

As a security or compliance focal, you can use the {{site.data.keyword.registrylong_notm}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All the goals for {{site.data.keyword.registrylong_notm}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, see [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).


### Available goals for {{site.data.keyword.registrylong_notm}}
{: #container-registry-available-goals}

You can choose from the following goals:

- Check whether {{site.data.keyword.registryshort_notm}} access is managed only by IAM access groups. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} has at least `#` service IDs with the IAM manager role. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} has at least `#` users with the IAM manager role. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} has no more than `#` service IDs with the IAM administrator role. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} is enabled with {{site.data.keyword.mon_full_notm}}. For more information, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor).
- Check whether {{site.data.keyword.registryshort_notm}} IAM access controls are configured for the account. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} image pushes and pulls take place only over private endpoints. For more information, see [Securing your connection to {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_private).
- Check whether {{site.data.keyword.registryshort_notm}} has no more than `#` users with the IAM administrator role. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether security insights sends alerts for critical, high, or medium vulnerabilities for images in {{site.data.keyword.registryshort_notm}}. For more information, see [Leveraging default services](/docs/security-advisor?topic=security-advisor-setup-services).

## Gaining security insight with {{site.data.keyword.registrylong_notm}}
{: #container-registry-security_insight}

With {{site.data.keyword.compliance_short}}, you can gain insight into potential issues through built-in security capabilities. By default, {{site.data.keyword.registryshort_notm}} is an integrated service. {{site.data.keyword.compliance_short}} gathers and presents information that is related to security so that all your security alerts are displayed in one place.

To learn more about how you can use security insights, see [Monitoring vulnerabilities in container images](/docs/security-advisor?topic=security-advisor-setup-services#setup-images).


