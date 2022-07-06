---

copyright:
  years: 2021, 2022
lastupdated: "2022-07-06"

keywords: Security and compliance for {{site.data.keyword.registrylong_notm}}, security for {{site.data.keyword.registrylong_notm}}, compliance for {{site.data.keyword.registrylong_notm}}, managing security and compliance for container registry, monitoring security and compliance for container registry, goals, container registry, security insight, security, compliance, registry, user access

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance for {{site.data.keyword.registryshort_notm}}
{: #manage-security-compliance}

{{site.data.keyword.registrylong}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

- Monitor for controls and goals that are applicable to {{site.data.keyword.registryshort}}.
- Define rules for {{site.data.keyword.registryshort}} that can help to standardize resource configuration.


## Monitoring security and compliance posture
{: #monitor-container-registry}

As a security or compliance focal, you can use the {{site.data.keyword.registryshort}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All the goals for {{site.data.keyword.registryshort}} are added to the {{site.data.keyword.cloud_notm}} Control Library profile, but can also be mapped to other profiles.
{: note}

To start monitoring your resources, see [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).


### Available goals for {{site.data.keyword.registryshort}}
{: #container-registry-available-goals}

You can choose from the following goals:

- Check whether {{site.data.keyword.registryshort_notm}} access is managed only by IAM [access groups](x2160811){: term}. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} has at least `#` service IDs with the IAM manager role. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} has at least `#` users with the IAM manager role. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} has no more than `#` service IDs with the IAM administrator role. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).
- Check whether {{site.data.keyword.registryshort_notm}} is enabled with {{site.data.keyword.mon_full_notm}}. For more information, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor).
- Check whether {{site.data.keyword.registryshort_notm}} IAM access controls are configured for the account. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam). From 5 July 2022, IAM access controls are always configured for the account. For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy).
- Check whether {{site.data.keyword.registryshort_notm}} image pushes and pulls take place only over private endpoints. For more information, see [Securing your connection to {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_private).
- Check whether {{site.data.keyword.registryshort_notm}} has no more than `#` users with the IAM administrator role. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).

## Governing {{site.data.keyword.registryshort}} resource configuration
{: #govern-container-registry}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} dashboard to define [configuration rules](#x3084914){: term} for {{site.data.keyword.registryshort}}.

Configuration rules are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the data that you can use to create a rule for {{site.data.keyword.registryshort}}, review the following table.

You can restrict your rule to a specific registry instance by specifying either the `registry` or `region` target attributes. For example, to restrict your rule to the registry instance in `us-south`, you can use the `string_equals` *operator* to require that either the *target attribute* `registry` matches the *value* `us.icr.io`, or the *target attribute* `region` matches the *value* `us-south`.

| Resource kind | Property | Operator | Value | Description |
|---------------|----------|----------|-------|-------------|
| *Service* | *`iam_authz`* | *`is_true`* | Not applicable | Enables role-based authorization for authenticating with {{site.data.keyword.iamlong}}. From 5 July 2022, this value is always true. For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy). |
| *Service* | *`private_only`* | *`is_true`*  \n *`is_false`* | Not applicable | Restricts the account so that it can push and pull images by using private connections only. |
| *Service* | *`platform_metrics`* | *`is_true`*  \n *`is_false`* | Not applicable | Publishes {{site.data.keyword.registryshort}} platform metrics. |
{: caption="Table 1. Rule properties for {{site.data.keyword.registryshort}}" caption-side="bottom"}

For example, use the following rule if you want *`private_only`* to be true, but only in the `us-south` registry.

```txt
{
    "target": {
        "service_name": "container-registry",
        "resource_kind": "service",
        "additional_target_attributes": [
            {
                "name": "registry",
                "operator": "string_equals",
                "value": "us.icr.io"
            }
        ]
    },
    "required_config": {
        "description": "IBM Cloud Container Registry account-level regional settings",
        "and": [
            {
                "property": "private_only",
                "operator": "is_true"
            }
        ]
    }
}
```
{: codeblock}

To learn more about configuration rules, see [What is Configuration Governance?](/docs/security-compliance?topic=security-compliance-what-is-governance)


