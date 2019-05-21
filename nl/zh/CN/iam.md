---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: IBM Cloud Container Registry, user access, Identity and Access Management, policies, user roles, access policies, platform management roles, service access roles, access roles,

subcollection: registry

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

# 使用 Identity and Access Management 管理用户访问权
{: #iam}

您帐户中的用户对 {{site.data.keyword.registrylong}} 的访问权通过 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) 进行控制。
{: shortdesc}

如果在 {{site.data.keyword.registrylong_notm}} 中为帐户启用了 IAM 策略，那么必须使用定义的 IAM 用户角色，为帐户中访问 {{site.data.keyword.registrylong_notm}} 服务的每个用户分配访问策略。该策略确定用户在服务的上下文中具有的角色，以及用户可以执行的操作。{{site.data.keyword.registrylong_notm}} 中的每个操作都会映射到一个或多个 [IAM 用户角色](/docs/iam?topic=iam-userroles)。

仅当您使用 IAM 登录到 {{site.data.keyword.registrylong_notm}} 时，才会强制实施 IAM 策略。如果使用其他方法（例如，注册表令牌）登录到 {{site.data.keyword.registrylong_notm}}，那么不会强制实施策略。如果要针对用于自动化的某个标识限制对一个或多个名称空间的访问，请考虑使用 IAM 服务标识，而不使用注册表令牌。有关服务标识的更多信息，请参阅[创建和使用服务标识](/docs/iam?topic=iam-serviceids#serviceids)。

有关 IAM 的更多信息，请参阅 [IBM Cloud 访问和管理](/docs/iam?topic=iam-iamoverview#iamoverview)。

有关为 {{site.data.keyword.registrylong_notm}} 启用策略的信息，请参阅[定义用户访问角色策略](/docs/services/Registry?topic=registry-user#user)。

策略允许在不同级别授予访问权。其中一些选项包含以下访问级别：

* 对帐户中服务的访问权
* 对服务中特定资源的访问权
* 对帐户中所有启用 IAM 的服务的访问权

在定义访问策略的作用域后，可以分配角色。请查看下列各表，其中概述了每个角色在 {{site.data.keyword.registrylong_notm}} 服务中所允许的操作。

有关在 UI 中分配用户角色的信息，请参阅[管理 IAM 访问权](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)。

请尝试[教程：授予对 {{site.data.keyword.registrylong_notm}} 资源的访问权](/docs/services/Registry?topic=registry-iam_access#iam_access)。
{: tip}

## 平台管理角色
{: #platform_management_roles}

下表详细描述了映射到平台管理角色的操作。平台管理角色支持用户在平台级别对服务资源执行任务，例如为用户分配对服务的访问权以及创建或删除服务标识。

|平台管理角色|操作描述|示例操作|
|:-----------------|:-----------------|:-----------------|
|查看者|不支持| |
|编辑者|不支持| |
|操作员|不支持| |
|管理员| <ul><li>为其他用户配置访问权</li><li>配置注册表令牌</li><li>创建集群</li></ul> | <ul><li>有关在 UI 中分配用户角色的信息，请参阅[管理 IAM 访问权](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)。</li><li>添加、列出、检索和除去注册表令牌</li><li>要在 {{site.data.keyword.containerlong_notm}} 中创建集群，必须将 {{site.data.keyword.registrylong_notm}} 的“管理员”角色分配给用户；请参阅[准备创建集群](/docs/containers?topic=containers-clusters#cluster_prepare)。</li></ul> |
{: caption="表 1. IAM 用户角色和操作" caption-side="top"}

对于 {{site.data.keyword.registrylong_notm}}，存在以下操作：

|操作|服务上的操作|角色
|:-----------------|:-----------------|:--------------|
|`container-registry.registrytoken.create`|[`ibmcloud cr token-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_add)：添加可用于控制对注册表的访问权的令牌。|管理员|
|`container-registry.registrytoken.delete`|[`ibmcloud cr token-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_rm)：除去一个或多个指定的令牌。|管理员|
|`container-registry.registrytoken.get`|[`ibmcloud cr token-get`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_get)：从注册表中检索指定的令牌。|管理员|
|`container-registry.registrytoken.list`|[`ibmcloud cr token-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_list)：显示 {{site.data.keyword.cloud_notm}} 帐户存在的所有令牌。|管理员|
{: caption="表 2. 用于配置 {{site.data.keyword.registrylong_notm}} 的平台操作" caption-side="top"}

## 服务访问角色
{: #service_access_roles}

下表详细描述了映射到服务访问角色的操作。通过服务访问角色，用户可以访问 {{site.data.keyword.registrylong_notm}}，并且有能力调用 {{site.data.keyword.registrylong_notm}} API。

|服务访问角色 |操作描述|示例操作|
|:-----------------|:-----------------|:-----------------|
|读取者|“读取者”角色可以查看信息。| <ul><li>查看、检查和拉出映像</li><li>查看名称空间</li><li>查看配额</li><li>查看漏洞报告</li><li>查看映像签名</li></ul>|
|写入者|“写入者”角色可以编辑信息。|<ul><li>构建、推送和删除映像</li><li>查看配额</li><li>对映像签名</li><li>添加和除去名称空间</li></ul> |
|管理者|“管理者”角色可以执行所有操作。| <ul><li>查看、检查、拉出、构建、推送和删除映像</li><li>查看、添加和除去名称空间</li><li>查看和设置配额</li><li>查看漏洞报告</li><li>查看和创建映像签名</li><li>复查和更改价格套餐</li><li>启用 IAM 策略强制实施</li><li>管理漏洞顾问程序豁免</li></ul> |
{: caption="表 3. IAM 服务访问角色和操作" caption-side="top"}

 对于以下 {{site.data.keyword.registrylong_notm}} 命令，您必须至少具有其中一个指定的角色，如下列各表中所示。要创建允许访问 {{site.data.keyword.registrylong_notm}} 的策略，您必须创建服务名称为 `container-registry` 的策略，服务实例为空，并且区域是您要授权访问的区域，或者为空以授予对所有区域的访问权。

### 用于配置 {{site.data.keyword.registrylong_notm}} 的访问角色
{: #access_roles_configure}

要授予用户在帐户中配置 {{site.data.keyword.registrylong_notm}} 的许可权，您必须创建授予下表中一个或多个角色的策略。创建策略时，不能指定 `resource type` 或 `resource`。

**示例**

```
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

|操作|服务上的操作|角色
|:-----------------|:-----------------|:--------------|
|`container-registry.auth.set`|[`ibmcloud cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable)：启用 IAM 策略强制实施。|管理者|
|`container-registry.exemption.manager`| <ul><li>[`ibmcloud cr exemption-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add)：为安全问题创建豁免。</li><li>[`ibmcloud cr exemption-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list)：列出对安全问题的豁免。</li><li>[`ibmcloud cr exemption-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm)：删除对安全问题的豁免。</li><li>[`ibmcloud cr exemption-types`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types)：列出可以豁免的安全问题的类型。</li></ul> |管理者|
|`container-registry.plan.get`|[`ibmcloud cr plan`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan)：显示价格套餐。|管理者|
|`container-registry.plan.set`|[`ibmcloud cr plan-upgrade`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade)：升级为标准套餐。|管理者|
|`container-registry.quota.get`|[`ibmcloud cr quota`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota)：显示流量和存储的当前配额以及这些配额的使用情况信息。|读取者、写入者和管理者|
|`container-registry.quota.set`|[`ibmcloud cr quota-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set)：修改指定的配额。|管理者|
{: caption="表 4. 用于配置 {{site.data.keyword.registrylong_notm}} 的服务操作" caption-side="top"}

### 使用 {{site.data.keyword.registrylong_notm}} 的访问角色
{: #access_roles_using}

要授予用户访问帐户中 {{site.data.keyword.registrylong_notm}} 内容的许可权，您必须创建授予下表中一个或多个角色的策略。创建策略时，可以通过将资源类型 `namespace` 和特定名称空间的名称指定为资源，从而限制对该名称空间的访问。如果未指定 `resource-type` 和 `resource`，那么策略将授予对帐户中所有资源的访问权。

您无法组织资源组中的注册表名称空间，以及分配对这些名称空间的访问权。
{: note}

**示例**

```
ibmcloud iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Reader> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

|操作|服务上的操作|角色
|:-----------------|:-----------------|:--------------|
|`container-registry.image.build`|[`ibmcloud cr build`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build)：构建容器映像。|写入者、管理者|
|`container-registry.image.delete`| <ul><li> [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm)：删除一个或多个映像。</li><li>`docker trust revoke`：删除签名。</li></ul> |写入者、管理者|
|`container-registry.image.inspect`|[`ibmcloud cr image-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect)：显示有关特定映像的详细信息。|读取者、管理者|
|`container-registry.image.list`|[`ibmcloud cr image-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list)：列出容器映像。|读取者、管理者|
|`container-registry.image.pull`| <ul><li>`docker pull`：拉出映像。</li><li>`docker trust inspect`：检查签名。</li></ul> |读取者、写入者和管理者|
|`container-registry.image.push`| <ul><li>`docker push`：推送映像。</li><li>`docker trust sign`：对映像签名。</li><li>[`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load)：将从 [IBM Passport Advantage Online for customers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/passportadvantage/pao_customer.html) 下载并已打包与 Helm 配合使用的 IBM 软件导入到 {{site.data.keyword.registrylong_notm}} 名称空间。</li></ul> |写入者、管理者|
|`container-registry.image.tag`|[`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag)：创建引用源映像的新映像。源映像和目标映像必须位于同一区域中。|对于源映像，为读取者、写入者或管理者；对于目标映像，为写入者或管理者|
|`container-registry.image.vulnerabilities`|[`ibmcloud cr vulnerability-assessment`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va)：查看映像的漏洞评估报告。|读取者、管理者|
|`container-registry.namespace.create`|[`ibmcloud cr namespace-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add)：添加名称空间。|写入者、管理者|
|`container-registry.namespace.delete`|[`ibmcloud cr namespace-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm)：除去名称空间。|写入者、管理者|
|`container-registry.namespace.list`|[`ibmcloud cr namespace-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list)：显示名称空间。|读取者、管理者|
{: caption="表 5. 使用 {{site.data.keyword.registrylong_notm}} 的服务操作" caption-side="top"}
