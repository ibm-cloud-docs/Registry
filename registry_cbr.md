---

copyright:
  years: 2023
lastupdated: "2023-11-14"

keywords: IBM Cloud Container Registry, context-based restrictions, CBR, access

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Protecting {{site.data.keyword.registryshort}} resources with context-based restrictions
{: #registry-cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to {{site.data.keyword.registrylong}} resources can be controlled with context-based restrictions and identity and access management (IAM) policies.
{: shortdesc}

These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Because both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. See [What are context-based restrictions?](/docs/account?topic=account-context-restrictions-whatis) for more information.

A user must have the Administrator role on the {{site.data.keyword.registryshort}} service to create, update, or delete rules. A user must also have either the Editor or Administrator role for context-based restrictions to create, update, or delete network zones. A user with the Viewer role for the context-based restrictions can add network zones to a rule.
{: note}

Any {{site.data.keyword.at_full_notm}} or audit log events generated come from the context-based restrictions, not {{site.data.keyword.registryshort}}. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).

{{site.data.keyword.registryshort}} is a service that is integrated with context-based restrictions. For more information, see [Services that are integrated with context-based restrictions](/docs/account?topic=account-context-restrictions-whatis&interface=cli#cbr-adopters).

To find out how to protect your {{site.data.keyword.registryshort}} resources with context-based restrictions, see the [Leveraging context-based restrictions to secure your resources](/docs/account?topic=account-context-restrictions-tutorial) tutorial.

## How {{site.data.keyword.registryshort}} integrates with context-based restrictions
{: #registry-cbr_overview}

You can create context-based restrictions for {{site.data.keyword.registrylong_notm}} resources or for specific APIs. With context-based restrictions, you can protect resources, see [Protecting specific resources](#registry-cbr_protect).

## Protecting specific resources
{: #registry-cbr_protect}

When you set up context-based restrictions, the restrictions apply to everything for the selected service in the account unless you select a subset of resources. {{site.data.keyword.registryshort}} supports the following subset of resources: `resource type = namespace` and `resource id = YOUR_IMAGE_NAMESPACE`, where `YOUR_IMAGE_NAMESPACE` is the namespace of your image. For more information about rules, see [Creating rules](/docs/account?topic=account-context-restrictions-create&interface=ui#context-restrictions-create-rules).

For example, if your image is in the format `uk.icr.io/<my_project>/<my_image>:latest`, where `<my_project>` is the name of your project and `<my_image>` is the name of the image, the attribute types are as shown in the following table.

| Attribute type | Operator | Value |
|----------------|----------|-------|
| `Region` | `string equals` | `London`|
| `Resource Type` | `string equals` | `namespace` |
| `Resource Name` | `string equals` | `<my_project>` |
{: caption="Table 1. Example attribute types" caption-side="bottom"}

The **Resource Name** value is a namespace, as shown by the [`ibmcloud cr namespace-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list) command.

## Limitations
{: #registry-cbr_limitations}

Context-based restrictions protect only the actions that are associated with the [{{site.data.keyword.registrylong_notm}} API](/apidocs/container-registry) and the [Vulnerability Advisor 4 for {{site.data.keyword.registrylong_notm}} API](/apidocs/vulnerability-advisor). Actions that are associated with the following platform APIs are not protected by context-based restrictions. Reference the API docs for the specific action IDs.

- [Resource Instance APIs](/apidocs/resource-controller/resource-controller#list-resource-instances)
- [Resource Keys APIs](/apidocs/resource-controller/resource-controller#list-resource-keys)
- [Resource Bindings APIs](/apidocs/resource-controller/resource-controller#list-resource-bindings)
- [Resource Aliases APIs](/apidocs/resource-controller/resource-controller#list-resource-aliases)
- [IAM Policy APIs](/apidocs/iam-policy-management#list-policies)
- [Global Search APIs](/apidocs/search)
- Global Tagging [Attach](/apidocs/tagging#attach-tag) and [Detach](/apidocs/tagging#detach-tag) APIs
- [Context-based Restriction Rule APIs](/apidocs/context-based-restrictions#create-rule)
- [Secrets Manager APIs](/apidocs/secrets-manager/secrets-manager-v2)

## Creating rules
{: #registry-cbr_create_rules}

Define restrictions to {{site.data.keyword.registryshort}} resources by creating rules.

### Creating rules in the {{site.data.keyword.cloud_notm}} console
{: #registry-cbr_rules_ui}
{: ui}

To create rules in the {{site.data.keyword.cloud_notm}} console, see [Creating rules](/docs/account?topic=account-context-restrictions-create&interface=ui#context-restrictions-create-rules). When you are asked to select a service, select **Container Registry**. You can protect all resources, or specific resources, see [Protecting specific resources](#registry-cbr_protect).

The following attribute types for specific resources are available in the {{site.data.keyword.cloud_notm}} console:

- `Region`
- `Resource Type`
- `Resource Name`

### Creating rules by using the CLI
{: #registry-cbr_rules_cli}
{: cli}

1. To create rules from the CLI, [install the context-based restrictions CLI plug-in](/docs/cli?topic=cli-cbr-plugin#install-cbr-plugin).
2. You can use the [`ibmcloud cbr rule-create` command](/docs/account?topic=account-cbr-plugin#cbr-cli-rule-create-command) to create rules for context-based restrictions. For more information, see [Creating rules by using the CLI](/docs/account?topic=account-context-restrictions-create&interface=cli#context-restrictions-create-rules-cli).

The following example creates a rule that targets the Container Registry service and allows access to your namespace `my_namespace` only over the private network in `us-south`.

```txt
ibmcloud cbr rule-create --description 'Only allow access to my_namespace over the private network' --service-name container-registry --context-attributes endpointType=private --resource-attributes resourceType=namespace,resource=my_namespace --region=us-south
```
{: pre}

### Creating rules by using the API
{: #registry-cbr_rules_api}
{: api}

To create rules in the API, see the [API docs](/apidocs/context-based-restrictions#create-rule) and [Creating rules by using the API](/docs/account?topic=account-context-restrictions-create&interface=api#context-restrictions-create-rules-api).

After you create a rule, it might take up to 10 minutes to before you can update that rule due to IAM TTL response caching.
{: note}
