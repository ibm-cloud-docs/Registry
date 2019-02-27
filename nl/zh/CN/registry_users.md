---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 定义用户访问角色策略
{: #user access}

作为管理员，您可以为注册表定义访问策略，以便为不同用户创建不同级别的访问权。例如，您可以授权某些用户设置配额，授权其他用户只能查看配额。
{: shortdesc}

必须为使用 {{site.data.keyword.registrylong}} 的每个用户定义访问策略。访问策略的作用域基于用户的已定义角色，这些角色将确定允许用户执行的操作。某些策略是预定义策略，但其他策略可以进行定制。

如果您在 2018 年 10 月 4 日之前就开始使用 {{site.data.keyword.registrylong_notm}}，那么必须启用策略强制实施才能使策略生效，请参阅[为现有用户启用策略强制实施](#existing_users)。
{: tip}

要了解有关 {{site.data.keyword.iamlong}} (IAM) 访问角色策略的更多信息，请参阅 [{{site.data.keyword.iamshort}}](/docs/iam/index.html#iamoverview)。

## 创建策略
{: #create}

如果要控制对资源的访问权，您必须向用户或服务标识分配角色。对 {{site.data.keyword.registrylong_notm}} 资源的访问权可以按名称授予名称空间资源，也可以授予整个服务（即帐户中的所有名称空间）。

如果要授予对所有内容的访问权，那么不要指定资源类型或资源。如果要授予对特定名称空间的访问权，请将资源类型指定为 `namespace`，然后将该名称空间的名称用作资源。

**开始之前**

- 决定每个用户需要的角色以及这些角色是针对 {{site.data.keyword.registrylong_notm}} 中的哪些资源；请参阅 [IAM 角色](/docs/services/Registry/iam.html#iam)。请考虑您可以创建多个策略的情况；例如，可以授予对某个资源的写访问权，但仅授予对另一资源的读访问权，并且不授予对另一资源的访问权。策略是可叠加的，这意味着全局读策略和作用域限定为资源的写策略会授予对该资源的读和写访问权。

- [邀请用户和分配访问权](/docs/iam/iamuserinv.html#iamuserinv)。

  如果您希望用户能够在 {{site.data.keyword.containerlong_notm}} 中创建集群，请确保为这些用户分配 {{site.data.keyword.registrylong_notm}}“管理员”角色，而不要分配资源组；请参阅[准备创建集群](/docs/containers/cs_clusters.html#cluster_prepare)。
  {: tip}

要为 {{site.data.keyword.registrylong_notm}} 创建策略，“服务名称”字段必须为 `container-registry`。

- 要为用户创建策略，请参阅[管理对资源的访问权](/docs/iam/mngiam.html#iammanidaccser)。
- 要为服务标识创建策略，请运行 `ibmcloud iam service-policy-create` 命令或使用 GUI 将角色绑定到服务标识。要创建策略，您必须具有“管理员”角色。您在自己的帐户上会自动具有“管理员”角色。有关更多信息，请参阅[创建和使用服务标识](/docs/iam/serviceid.html#serviceids)以及[管理服务标识访问策略](/docs/iam/serviceidaccess.html#serviceidpolicy)。

## 为现有用户启用策略强制实施
{: #existing_users}

对于在 2018 年 10 月 4 日之后供应的用户，缺省情况下已启用 IAM 策略。对于在 2018 年 10 月 4 日之前供应的用户，在创建策略后，必须启用策略强制实施，才能使策略生效。

1. 为用户和服务标识[创建策略](#create)。

2. 要启用策略强制实施，请运行 [`bx cr iam-policies-enable`](/docs/services/Registry/registry_cli.html#bx_cr_iam_policies_enable) 命令。

    您必须在帐户上具有“管理者”角色，才能运行 `ibmcloud cr iam-policies-enableibmcloud cr iam-policies-enable` 命令。您在自己的帐户中会自动具有“管理者”角色。
    {: tip}
