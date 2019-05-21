---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

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

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

您可以使用在 `container-registry` CLI 插件中提供的 {{site.data.keyword.registrylong}} CLI 来管理 {{site.data.keyword.cloud_notm}} 帐户的注册表及其资源。
{: shortdesc}

**先决条件**

* 安装 [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。使用 {{site.data.keyword.cloud_notm}} CLI 运行命令的前缀为 `ibmcloud`。
* 在运行注册表命令之前，请使用 `ibmcloud login` 命令登录到 {{site.data.keyword.cloud_notm}}，以生成访问令牌并对会话进行认证。

在命令行中，`ibmcloud` CLI 和 `container-registry` CLI 插件更新可用时会通知您。请确保使 CLI 保持最新，以便可以使用所有可用的命令和标志。

如果要查看 `container-registry` CLI 插件的当前版本，请运行 `ibmcloud plugin list`。

要了解如何使用 {{site.data.keyword.registrylong_notm}} CLI，请参阅 [{{site.data.keyword.registrylong_notm}} 入门](/docs/services/Registry?topic=registry-getting-started#getting-started)。

有关某些命令所需的 IAM 平台和服务访问角色的更多信息，请参阅[使用 Identity and Access Management 管理用户访问权](/docs/services/Registry?topic=registry-iam#iam)。

不要将个人信息放入容器映像、名称空间名称、描述字段（例如，注册表令牌）或任何映像配置数据（例如，映像名称或映像标签）中。
{:tip}

## `ibmcloud cr api`
{: #bx_cr_api}

返回有关对其运行命令的注册表 API 端点的详细信息。

```
ibmcloud cr api
```
{: codeblock}

**先决条件**

无

## `ibmcloud cr build`
{: #bx_cr_build}

在 {{site.data.keyword.registrylong_notm}} 中构建 Docker 映像。

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
<dt>`DIRECTORY`</dt>
<dd>构建上下文的位置，包含 Dockerfile 和必备文件。如果在工作目录设置为构建上下文的存储位置时运行命令，那么可以用句点 (.) 替换 `DIRECTORY`.</dd>
<dt>`--no-cache`</dt>
<dd>（可选）如果指定此项，那么在此构建中不会使用先前构建中的高速缓存映像层。</dd>
<dt>`--pull`</dt>
<dd>（可选）如果指定此项，那么即使构建主机上已存在具有匹配标记的映像，也仍然会拉出基本映像。</dd>
<dt>`--quiet`, `-q`</dt>
<dd>（可选）如果指定此项，将禁止构建输出，除非发生错误。</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>（可选）以“`KEY=VALUE`”格式指定其他构建自变量。通过包含此参数多次可以指定多个构建自变量。指定与 Dockerfile 中的密钥相匹配的 ARG 行时，每个构建自变量的值都可用作环境变量。</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>（可选）如果对多个构建使用相同的文件，那么可以选择指向其他 Dockerfile 的路径。指定 Dockerfile 相对于构建上下文的位置。如果未指定此项，缺省值为 `PATH/Dockerfile`，其中 PATH 是构建上下文的根目录。</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>要构建的映像的全名，包含注册表 URL 和名称空间。</dd>
</dl>

**示例**

构建一个不使用先前构建的构建高速缓存的 Docker 映像，其中构建输出已禁止，标记为 *`us.icr.io/birds/bluebird:1`*，并且目录是您的工作目录。

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

为安全问题创建豁免。您可以为安全问题创建应用于不同作用域的豁免。作用域可以是帐户、名称空间、存储库或标记。

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**命令选项**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>要将帐户设置为作用域，请使用“`*`”作为值。要将名称空间、存储库或标记设置为作用域，请输入下列其中一种格式的值：`namespace`、`namespace/repository` 或 `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>要豁免的安全问题的类型。要查找有效的问题类型，请运行 `ibmcloud cr exemption-types`。
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>要豁免的安全问题的标识。要找到问题标识，运行`ibmcloud cr va <image>`，其中 `<image>` 是映像的名称，并使用 **Vulnerability ID** 或 **Configuration Issue ID** 列中的相关值。
</dd>
</dl>

**示例**

针对 `us.icr.io/birds/bluebird` 存储库中的所有映像，为标识为 `CVE-2018-17929` 的 CVE 创建 CVE 豁免。 

```
bmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

针对标识为 `CVE-2018-17929` 的 CVE 创建帐户范围的 CVE 豁免。

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

为标记为 `us.icr.io/birds/bluebird:1` 的单个映像的问题 `application_configuration:nginx.ssl_protocols` 创建配置问题豁免。

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

列出安全问题的豁免。

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**命令选项**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>（可选）仅列出应用于此作用域的豁免。 要将名称空间、存储库或标记设置为作用域，请输入下列其中一种格式的值：`namespace`、`namespace/repository` 或 `namespace/repository:tag`
</dd>
</dl>

**示例**

列出适用于 *`birds/bluebird`* 存储库中映像的所有安全问题豁免。输出包括帐户范围的豁免、作用域限定为 *`birds`* 名称空间的豁免，以及作用域限定为 *`birds/bluebird`* 存储库的豁免，但不包括作用域限定为 *`birds/bluebird`* 存储库中特定标记的任何豁免。

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

删除安全问题的豁免。要查看现有豁免，请运行 `ibmcloud cr exemption-list`。

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**命令选项**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>要将帐户设置为作用域，请使用“`*`”作为值。要将名称空间、存储库或标记设置为作用域，请输入下列其中一种格式的值：`namespace`、`namespace/repository` 或 `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>要除去的安全问题豁免的问题类型。要查找豁免的问题类型，请运行 `ibmcloud cr exemption-list`。</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>要除去的安全问题豁免的标识。要查找豁免的问题标识，请运行 `ibmcloud cr exemption-list`。</dd>
</dl>

**示例**

针对 `us.icr.io/birds/bluebird` 存储库中的所有映像，为标识为 `CVE-2018-17929` 的 CVE 删除 CVE 豁免。

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

删除标识为 `CVE-2018-17929` 的 CVE 的帐户范围的 CVE 豁免。

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

为标记为 `us.icr.io/birds/bluebird:1` 的单个映像的问题 `application_configuration:nginx.ssl_protocols` 删除配置问题豁免。

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

列出可以豁免的安全问题的类型。

```
ibmcloud cr exemption-types
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

如果是使用 IAM 认证，那么此命令将启用细颗粒度授权。有关更多信息，请参阅[使用 Identity and Access Management 管理用户访问权](/docs/services/Registry?topic=registry-iam#iam)和[定义用户访问角色策略](/docs/services/Registry?topic=registry-user#user)。

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

显示目标 {{site.data.keyword.registryshort_notm}} 帐户的 IAM 策略状态。有关更多信息，请参阅[使用 Identity and Access Management 管理用户访问权](/docs/services/Registry?topic=registry-iam#iam)和[定义用户访问角色策略](/docs/services/Registry?topic=registry-user#user)。

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

显示有关特定映像的详细信息。

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
<dt>`--format FORMAT`</dt>
<dd>（可选）使用 Go 模板来设置输出元素的格式。

有关更多信息，请参阅[对 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)。

</dd>
<dt>`IMAGE`</dt>
<dd>要获取其报告的映像的名称。可以通过在命令中列出每个映像（各名称之间用一个空格分隔）来检查多个映像。

<p>要查找映像的名称，请运行 `ibmcloud cr image-list`。将**存储库**和**标记**列的内容组合在一起，以创建格式为 `repository:tag` 的映像名称。如果未在映像名称中指定标记，那么会检查标记为 `latest` 的映像。</p>

</dd>
</dl>

**示例**

使用格式化伪指令 *`"{{ .Config.ExposedPorts }}"`* 来显示有关映像 *`us.icr.io/birds/bluebird:1`* 的已公开端口的详细信息。

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

显示 {{site.data.keyword.cloud_notm}} 帐户中的所有映像。

映像名称是**存储库**和**标记**列的内容组合，格式为 `repository:tag`。
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
<dt>`--no-trunc`</dt>
<dd>（可选）不截断映像摘要。</dd>
<dt>`--format FORMAT`</dt>
<dd>（可选）使用 Go 模板来设置输出元素的格式。

有关更多信息，请参阅[对 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)。

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>（可选）将列出每个映像，格式为 `repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>（可选）将输出限制为仅显示指定名称空间或名称空间和存储库中的映像。</dd>
<dt>`--include-ibm`</dt>
<dd>（可选）在输出中包含 {{site.data.keyword.IBM_notm}} 提供的公用映像。不使用此选项时，缺省情况下仅列出专用映像。</dd>
</dl>

**示例**

以 `repository:tag` 格式显示 *`birds`* 名称空间中的映像，而不截断映像摘要。

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

从 {{site.data.keyword.registrylong_notm}} 中删除一个或多个指定的映像。

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**

<dl>
<dt>`IMAGE`</dt>
<dd>要删除的映像的名称。可以通过在命令中列出每个映像（各名称之间用一个空格分隔）来同时删除多个映像。`IMAGE` 的格式必须为 `repository:tag`，例如：`us.icr.io/namespace/image:latest`

<p>要查找映像的名称，请运行 `ibmcloud cr image-list`。将**存储库**和**标记**列的内容组合在一起，以创建格式为 `repository:tag` 的映像名称。如果未在映像名称中指定标记，那么缺省情况下会删除标记为 `latest` 的映像。</p>

</dd>
</dl>

**示例**
删除映像 `us.icr.io/birds/bluebird:1`。

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

在 {{site.data.keyword.registrylong_notm}} 中创建引用源映像 SOURCE_IMAGE 的新映像 TARGET_IMAGE。源映像和目标映像必须位于同一区域中。

要查找映像的名称，请运行 `ibmcloud cr image-list`。将**存储库**和**标记**列的内容组合在一起，以创建格式为 `repository:tag` 的映像名称。
{: tip}

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>源映像的名称。`SOURCE_IMAGE` 的格式必须为 `repository:tag`，例如：`us.icr.io/namespace/image:latest`

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>目标映像的名称。`TARGET_IMAGE` 的格式必须为 `repository:tag`，例如：`us.icr.io/namespace/image:latest`

</dd>
</dl>

**示例**

向映像 `us.icr.io/birds/bluebird:1` 添加另一个标记引用 `latest`。

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

将映像 `us.icr.io/birds/bluebird:peck` 复制到同一名称空间 `birds/pigeon` 中的其他存储库。

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

将映像 `us.icr.io/birds/bluebird:peck` 复制到您有权访问的另一个名称空间 `animals` 中。

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

显示登录到的注册表的名称和帐户。

```
ibmcloud cr info
```
{: codeblock}

**先决条件**

无

## `ibmcloud cr login`
{: #bx_cr_login}

此命令针对注册表运行 `docker login` 命令。需要运行 `docker login` 命令后，才能对注册表运行 `docker push` 或 `docker pull` 命令。无需运行此命令就可运行其他 `ibmcloud cr` 命令。如果未安装 Docker，那么此命令将返回错误消息。

```
ibmcloud cr login
```
{: codeblock}

**先决条件**

无

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

选择名称空间的名称，然后将其添加到 {{site.data.keyword.cloud_notm}} 帐户。

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
<dt>`NAMESPACE`</dt>
<dd>要添加的名称空间。名称空间在同一区域的所有 {{site.data.keyword.cloud_notm}} 帐户中必须唯一。名称空间必须具有 4 到 30 个字符，并且只能包含小写字母、数字、连字符和下划线。名称空间必须以字母或数字开头和结尾。
  
<p>  
<strong>提示</strong>：不要将个人信息放入名称空间名称中。
</p>
  
</dd>
</dl>

**示例**

创建名称为 *`birds`* 的名称空间。

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

显示 {{site.data.keyword.cloud_notm}} 帐户拥有的所有名称空间。

```
ibmcloud cr namespace-list
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

从 {{site.data.keyword.cloud_notm}} 帐户中除去名称空间。除去名称空间时，将删除此名称空间中的映像。

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
<dt>`NAMESPACE`</dt>
<dd>要除去的名称空间。</dd>
<dt>`--force`, `-f`</dt>
<dd>（可选）强制命令运行，而不显示用户提示。</dd>
</dl>

**示例**

除去名称空间 *`birds`*。

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

显示您的价格套餐。

```
ibmcloud cr plan
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

升级到标准套餐。

有关套餐的信息，请参阅[注册表套餐](/docs/services/Registry?topic=registry-registry_overview#registry_plans)。

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**命令选项**
<dl>
<dt>`PLAN`</dt>
<dd>（可选）要升级为的价格套餐的名称。如果未指定 `PLAN`，缺省值为 `standard`。</dd>
</dl>

**示例**

升级为标准价格套餐。

```
    ibmcloud cr plan-upgrade standard
    ```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

将已从 [IBM Passport Advantage Online for customers ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/passportadvantage/pao_customer.html) 下载并已打包与 Helm 配合使用的 {{site.data.keyword.IBM_notm}} 软件导入到 {{site.data.keyword.registrylong_notm}} 名称空间。

容器映像会推送到专用 {{site.data.keyword.registryshort_notm}} 名称空间。Helm chart 会写入从中运行命令的目录中所创建的 `ppa-import` 目录。（可选）可以使用 [Chart Museum 开放式源代码项目 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 来托管 Helm chart。

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>从 IBM Passport Advantage 下载的压缩文件的路径。</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>其中一个名称空间。压缩文件中的容器映像会推送到此名称空间。要列出名称空间，请运行 `ibmcloud cr namespace-list`。</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>（可选）您的 [Chart Museum ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 唯一资源标识。</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>（可选）您的 [Chart Museum ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 用户名。</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>（可选）您的 [Chart Museum ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 密码。</dd>
</dl>

**示例**

在 {{site.data.keyword.registrylong_notm}} 名称空间 *`birds`* 中导入 IBM 软件并将其打包以与 Helm 配合使用，其中压缩文件的路径为 *`downloads/compressed_file.tgz`*。

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

显示流量和存储的当前配额以及这些配额的使用情况信息。

```
ibmcloud cr quota
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

修改指定的配额。

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[配置 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_configure)。

**命令选项**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>（可选）将流量配额更改为指定的值（以兆字节为单位）。如果您无权设置流量，或者如果设置的值超过当前价格套餐，那么操作会失败。</dd>
<dt>`--storage STORAGE`</dt>
<dd>（可选）将存储配额更改为指定的值（以兆字节为单位）。如果您无权设置存储配额，或者如果设置的值超过当前价格套餐，那么操作会失败。</dd>
</dl>

**示例**

将拉出流量的配额限制设置为 *7000* 兆字节，并将存储量设置为 *600* 兆字节。

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

显示目标区域和注册表。

```
ibmcloud cr region
```
{: codeblock}

**先决条件**

无

有关更多信息，请参阅[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)。

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

设置 {{site.data.keyword.registrylong_notm}} 命令的目标区域。要列出可用的区域，请运行不带任何参数的命令。

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**先决条件**

无

**命令选项**
<dl>
<dt>`REGION`</dt>
<dd>（可选）目标区域的名称，例如 `us-south`。

有关更多信息，请参阅[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)。

</dd>
</dl>

**示例**

将美国南部区域设定为目标。

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-add`
{: #bx_cr_token_add}

添加可用于控制对注册表的访问权的令牌。

```
ibmcloud cr token-add [--description DESCRIPTION] [--quiet | -q] [--non-expiring] [--readwrite]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**命令选项**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>（可选）指定此值作为运行 `ibmcloud cr token-list` 时显示的令牌描述。如果令牌是由 {{site.data.keyword.containerlong_notm}} 自动创建的，那么描述会设置为 Kubernetes 集群名称。在这种情况下，除去集群时会自动除去该令牌。
  
<p> 
  <strong>提示</strong>：不要将个人信息放入令牌描述中。
</p>

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>（可选）仅显示令牌，不显示任何周围的文本。</dd>
<dt>`--non-expiring`</dt>
<dd>（可选）创建具有不会到期的访问权的令牌。未设置此参数时，缺省情况下令牌的访问权将在 24 小时后到期。</dd>
<dt>`--readwrite`</dt>
<dd>（可选）创建用于授予读写访问权的令牌。不使用此选项时，缺省情况下访问权为只读。</dd>
</dl>

**示例**

为不会到期且具有读/写访问权的令牌添加描述 *Token for my account*。

```
ibmcloud cr token-add --description "Token for my account" --non-expiring --readwrite
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

从注册表中检索指定的令牌。

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**命令选项**
<dl>
<dt>`TOKEN`</dt>
<dd>要检索的令牌的唯一标识。要列出令牌，请运行 `ibmcloud cr token-list`。</dd>
</dl>

**示例**

检索令牌 *10101010-101x-1x10-x1xx-x10xx10xxx10*。

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

显示 {{site.data.keyword.cloud_notm}} 帐户存在的所有令牌。

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**命令选项**
<dl>
<dt>`--format FORMAT`</dt>
<dd>（可选）使用 Go 模板来设置输出元素的格式。

有关更多信息，请参阅[对 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)。

</dd>
</dl>

**示例**

使用格式化伪指令 *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`* 来显示所有只读标记。

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
{: pre}

此示例生成以下格式的输出：

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

除去一个或多个指定的注册表令牌。

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[平台管理角色](/docs/services/Registry?topic=registry-iam#platform_management_roles)。

**命令选项**
<dl>
<dt>`TOKEN`</dt>
<dd>TOKEN 可以是令牌本身，也可以是令牌的唯一标识，如 `ibmcloud cr token-list` 中所示。可以指定多个令牌，并且令牌之间必须以一个空格分隔。</dd>
<dt>`--force`, `-f`</dt>
<dd>（可选）强制命令运行，而不显示用户提示。</dd>
</dl>

**示例**

除去令牌 *10101010-101x-1x10-x1xx-x10xx10xxx10*。

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

查看映像的漏洞评估报告。

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**先决条件**

要了解有关必需许可权的信息，请参阅[使用 {{site.data.keyword.registrylong_notm}} 的访问角色](/docs/services/Registry?topic=registry-iam#access_roles_using)。

**命令选项**
<dl>
<dt>`IMAGE`</dt>
<dd>要获取其报告的映像的名称。此报告指示该映像是否具有任何已知的包漏洞。可以通过在命令中列出每个映像（各名称之间用一个空格分隔）来同时请求多个映像的报告。

<p>要查找映像的名称，请运行 `ibmcloud cr image-list`。将**存储库**和**标记**列的内容组合在一起，以创建格式为 `repository:tag` 的映像名称。如果未在映像名称中指定标记，那么报告会评估标记为 `latest` 的映像。</p>

<p>支持以下操作系统：

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

有关更多信息，请参阅[使用漏洞顾问程序管理映像安全性](/docs/services/va?topic=va-va_index)。

</dd>
<dt>`--extended`, `-e`</dt>
<dd>（可选）命令输出显示有关有漏洞包的修订的其他信息。</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>（可选）命令输出限制为仅显示漏洞。</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>（可选）命令输出限制为仅显示配置问题。</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>（可选）命令输出以所选格式返回。缺省格式为 `text`。支持以下格式：

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**示例**

查看映像的标准漏洞评估报告。

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

以 JSON 格式查看映像 `us.icr.io/birds/bluebird:1` 的漏洞评估报告，此报告仅显示漏洞。

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
