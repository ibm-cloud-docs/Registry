---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-21"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

您可以使用在 container-registry 插件中提供的 {{site.data.keyword.registrylong}} CLI 来管理 {{site.data.keyword.Bluemix_notm}} 帐户的注册表及其资源。
{: shortdesc}

**先决条件**
* 在运行注册表命令之前，请使用 `ibmcloud login` 命令登录到 {{site.data.keyword.Bluemix_notm}}，以生成访问令牌并对会话进行认证。

要了解如何使用 {{site.data.keyword.registrylong_notm}} CLI，请参阅 [{{site.data.keyword.registrylong_notm}} 入门](index.html)。

不要将个人信息放入容器映像、名称空间名称、描述字段（例如，注册表令牌）或任何映像配置数据（例如，映像名称或映像标签）中。
{:tip}


<table summary="管理 {{site.data.keyword.registrylong_notm}}">
<caption>表 1. 用于管理 {{site.data.keyword.registrylong_notm}} 的命令
</caption>
 <thead>
 <th colspan="5">用于管理注册表的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[`ibmcloud cr api
](#bx_cr_api)</td>
 <td>[`ibmcloud cr build`](#bx_cr_build)</td>
 <td>[`ibmcloud cr exemption-add`](#bx_cr_exemption_add)</td>
 <td>[`ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)](#bx_cr_exemption_list)</td>
 <td>[`ibmcloud cr exemption-rm`](#bx_cr_exemption_rm)</td>
 </tr>
 <tr>
 <td>[`ibmcloud cr exemption-types
](#bx_cr_exemption_types)</td>
 <td>[`ibmcloud cr info
](#bx_cr_info)</td>
 <td>[`ibmcloud cr image-inspect`](#bx_cr_image_inspect)</td>
 <td>[`ibmcloud cr image-list` (`ibmcloud cr images`)](#bx_cr_image_list)</td>
 <td>[`ibmcloud cr image-rm`](#bx_cr_image_rm)</td>
  </tr>
 <tr>
 <td>[`    ibmcloud cr login
    ](#bx_cr_login)</td>
 <td>[`ibmcloud cr namespace-add`](#bx_cr_namespace_add)</td>
 <td>[`ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)](#bx_cr_namespace_list)</td>
 <td>[`ibmcloud cr namespace-rm`](#bx_cr_namespace_rm)</td>
 <td>[`ibmcloud cr plan`](#bx_cr_plan)</td>
 </tr>
 <tr>
 <td>[`ibmcloud cr plan-upgrade`](#bx_cr_plan_upgrade)</td>
 <td>[`ibmcloud cr ppa-archive-load`](#bx_cr_ppa_archive_load)</td>
 <td>[`ibmcloud cr quota`](#bx_cr_quota)</td>
 <td>[`ibmcloud cr quota-set`](#bx_cr_quota_set)</td>
 <td>[`ibmcloud cr region`](#bx_cr_region)</td>
 </tr><tr>
 <td>[`ibmcloud cr region-set`](#bx_cr_region_set)</td>
 <td>[`ibmcloud cr token-add`](#bx_cr_token_add)</td>
 <td>[`ibmcloud cr token-get`](#bx_cr_token_get)</td>
 <td>[`ibmcloud cr token-list` (`ibmcloud cr tokens`)](#bx_cr_token_list)</td>
 <td>[`ibmcloud cr token-rm`](#bx_cr_token_rm)</td>
  </tr><tr>
  <td>[`ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)](#bx_cr_va)</td>
 </tr>
 </tbody></table>



## `ibmcloud cr api
`
{: #bx_cr_api}

返回有关对其运行命令的注册表 API 端点的详细信息。

```
ibmcloud cr api
```
{: codeblock}


## `ibmcloud cr build`
{: #bx_cr_build}

在 {{site.data.keyword.registrylong_notm}} 中构建 Docker 映像。

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**参数**
<dl>
<dt>`DIRECTORY`</dt>
<dd>构建上下文的位置，包含 Dockerfile 和必备文件。</dd>
<dt>`--no-cache`</dt>
<dd>（可选）如果指定此项，那么在此构建中不会使用先前构建中的高速缓存映像层。</dd>
<dt>`--pull`</dt>
<dd>（可选）如果指定此项，那么即使构建主机上已存在具有匹配标记的映像，也仍然会拉出基本映像。</dd>
<dt>`--quiet`, `-q`</dt>
<dd>（可选）如果指定此项，将禁止构建输出，除非发生错误。</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>（可选）以“KEY=VALUE”格式指定其他构建自变量。通过包含此参数多次可以指定多个构建自变量。指定与 Dockerfile 中的密钥相匹配的 ARG 行时，每个构建自变量的值都可用作环境变量。</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>（可选）如果对多个构建使用相同的文件，那么可以选择指向其他 Dockerfile 的路径。指定 Dockerfile 相对于构建上下文的位置。如果未指定此项，缺省值为 `PATH/Dockerfile`，其中 PATH 是构建上下文的根目录。</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>要构建的映像的全名，包含注册表 URL 和名称空间。</dd>
</dl>


## `ibmcloud cr info
`
{: #bx_cr_info}

显示登录到的注册表的名称和帐户。

```
ibmcloud cr info
```
{: codeblock}


## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

为安全问题创建豁免。您可以为安全问题创建应用于不同作用域的豁免。作用域可以是帐户、名称空间、存储库或标记。 

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**参数**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>要将帐户设置为作用域，请使用“`*`”作为值。要将名称空间、存储库或标记设置为作用域，请输入下列其中一种格式的值：`namespace`、`namespace/repository` 或 `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>要豁免的安全问题的类型。要查找有效的问题类型，请运行 `ibmcloud cr exemption-types`。
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>要豁免的安全问题的标识。要查找问题标识，请运行 `ibmcloud cr va <image>`，其中 *&lt;image&gt;* 是映像的名称，并使用 **Vulnerability ID** 或 **Configuration Issue ID** 列中的相关值。
</dd>
</dl>


## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

列出安全问题的豁免。 

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**参数**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>（可选）仅列出应用于此作用域的豁免。 要将名称空间、存储库或标记设置为作用域，请输入下列其中一种格式的值：`namespace`、`namespace/repository` 或 `namespace/repository:tag`
</dd>
</dl>


## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

删除安全问题的豁免。要查看现有豁免，请运行 `ibmcloud cr exemption-list`。

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**参数**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>要将帐户设置为作用域，请使用“`*`”作为值。要将名称空间、存储库或标记设置为作用域，请输入下列其中一种格式的值：`namespace`、`namespace/repository` 或 `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>要除去的安全问题豁免的问题类型。要查找豁免的问题类型，请运行 `ibmcloud cr exemption-list`。</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>要除去的安全问题豁免的标识。要查找豁免的问题标识，请运行 `ibmcloud cr exemption-list`。</dd>
</dl>


## `ibmcloud cr exemption-types
`
{: #bx_cr_exemption_types}

列出可以豁免的安全问题的类型。

```
ibmcloud cr exemption-types
```
{: codeblock}


## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

显示有关特定映像的详细信息。

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**参数**
<dl>
<dt>`--format FORMAT`</dt>
<dd>（可选）使用 Go 模板来设置输出元素的格式。

有关更多信息，请参阅[对 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤](registry_cli_reference.html#registry_cli_listing)。

</dd>
<dt>`IMAGE`</dt>
<dd>要获取其报告的映像的名称。可以通过在命令中列出每个映像（各名称之间用一个空格分隔）来检查多个映像。

<p>要查找映像的名称，请运行 `ibmcloud cr image-list`。将**存储库**和**标记**列的内容组合在一起，以创建格式为 `repository:tag` 的映像名称。如果未在映像名称中指定标记，那么会检查标记为 `latest` 的映像。</p>

</dd>
</dl>


## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

显示 {{site.data.keyword.Bluemix_notm}} 帐户中的所有映像。

映像名称是<strong>存储库</strong>和<strong>标记</strong>列的内容组合，格式为 `repository:tag`。
{:tip}

```
 ibmcloud cr image-list [--no-trunc] [--format FORMAT] [-q, --quiet] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**参数**
<dl>
<dt>`--no-trunc`</dt>
<dd>（可选）不截断映像摘要。</dd>
<dt>`--format FORMAT`</dt>
<dd>（可选）使用 Go 模板来设置输出元素的格式。

有关更多信息，请参阅[对 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤](registry_cli_reference.html#registry_cli_listing)。

</dd>
<dt>`-q`, `--quiet`</dt>
<dd>（可选）将列出每个映像，格式为 `repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>（可选）将输出限制为仅显示指定名称空间或名称空间和存储库中的映像。</dd>
<dt>`--include-ibm`</dt>
<dd>（可选）在输出中包含 {{site.data.keyword.IBM_notm}} 提供的公用映像。不使用此选项时，缺省情况下仅列出专用映像。</dd>
</dl>



## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

从注册表中删除一个或多个指定的映像。

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**参数**
<dl>
<dt>`IMAGE`</dt>
<dd>要获取其报告的映像的名称。可以通过在命令中列出每个映像（各名称之间用一个空格分隔）来同时删除多个映像。

<p>要查找映像的名称，请运行 `ibmcloud cr image-list`。将**存储库**和**标记**列的内容组合在一起，以创建格式为 `repository:tag` 的映像名称。如果未在映像名称中指定标记，那么缺省情况下会删除标记为 `latest` 的映像。</p>

</dd>
</dl>


## `ibmcloud cr login`
{: #bx_cr_login}

此命令针对注册表运行 `docker login` 命令。需要运行 `docker login` 命令后，才能对注册表运行 `docker push` 或 `docker pull` 命令。无需运行此命令就可运行其他 `ibmcloud cr` 命令。如果未安装 Docker，那么此命令将返回错误消息。

```
ibmcloud cr login
```
{: codeblock}


## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

向 {{site.data.keyword.Bluemix_notm}} 帐户添加名称空间。

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**参数**
<dl>
<dt>`NAMESPACE`</dt>
<dd>要添加的名称空间。名称空间在同一区域的所有 {{site.data.keyword.Bluemix_notm}} 帐户中必须唯一。
  
<p>  
<strong>提示</strong>：不要将个人信息放入名称空间名称中。
</p>
  
</dd>
</dl>


## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

显示 {{site.data.keyword.Bluemix_notm}} 帐户拥有的所有名称空间。

```
ibmcloud cr namespace-list
```
{: codeblock}


## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

从 {{site.data.keyword.Bluemix_notm}} 帐户中除去名称空间。除去名称空间时，将删除此名称空间中的映像。

```
ibmcloud cr namespace-rm NAMESPACE
```
{: codeblock}

**参数**
<dl>
<dt>`NAMESPACE`</dt>
<dd>要除去的名称空间。</dd>
</dl>


## `ibmcloud cr plan
`
{: #bx_cr_plan}

显示您的价格套餐。

```
ibmcloud cr plan
```
{: codeblock}


## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

升级到标准套餐。

有关套餐的信息，请参阅[注册表套餐](registry_overview.html#registry_plans)。

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**参数**
<dl>
<dt>`PLAN`</dt>
<dd>要升级到的价格套餐的名称。如果未指定 `PLAN`，缺省值为 `standard`。</dd>
</dl>


## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

将已从 [IBM Passport Advantage Online for customers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/passportadvantage/pao_customer.html) 下载并已打包与 Helm 配合使用的 IBM 软件导入到专用注册表名称空间。

容器映像会推送到专用 {{site.data.keyword.registryshort_notm}} 名称空间。Helm 图表会写入从中运行命令的目录中所创建的 `ppa-import` 目录。（可选）可以使用 [Chart Museum 开放式源代码项目 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 来托管 Helm 图表。

**示例命令**

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**参数**：
<dl>
  <dt>`--archive FILE`</dt>
  <dd>从 IBM Passport Advantage 下载的压缩文件的路径。</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>其中一个名称空间。压缩文件中的容器映像会推送到此名称空间。要列出名称空间，请运行 `ibmcloud cr namespace-list`。</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>（可选）您的 [Chart Museum ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 唯一资源标识。</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>（可选）您的 [Chart Museum ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 用户名。</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>（可选）您的 [Chart Museum ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) 密码。</dd>
</dl>


## `ibmcloud cr quota`
{: #bx_cr_quota}

显示流量和存储的当前配额以及这些配额的使用情况信息。

```
ibmcloud cr quota
```
{: codeblock}


## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

修改指定的配额。

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**参数**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>（可选）将流量配额更改为指定的值（以兆字节为单位）。如果您无权设置流量，或者如果设置的值超过当前价格套餐，那么操作会失败。</dd>
<dt>`--storage STORAGE`</dt>
<dd>（可选）将存储配额更改为指定的值（以兆字节为单位）。如果您无权设置存储配额，或者如果设置的值超过当前价格套餐，那么操作会失败。</dd>
</dl>


## `ibmcloud cr region
`
{: #bx_cr_region}

显示目标区域和注册表。

```
ibmcloud cr region
```
{: codeblock}

有关更多信息，请参阅[区域](registry_overview.html#registry_regions)。


## `ibmcloud cr region-set`
{: #bx_cr_region_set}

设置 {{site.data.keyword.registrylong_notm}} 命令的目标区域。要列出可用的区域，请运行不带任何参数的命令。

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**参数**
<dl>
<dt>`REGION`</dt>
<dd>（可选）目标区域的名称，例如 `us-south`。

有关更多信息，请参阅[区域](registry_overview.html#registry_regions)。

</dd>
</dl>


## `ibmcloud cr token-add`
{: #bx_cr_token_add}

添加可用于控制对注册表的访问权的令牌。

```
ibmcloud cr token-add [--description DESCRIPTION] [-q, --quiet] [--non-expiring] [--readwrite]
```
{: codeblock}


**参数**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>（可选）指定此值作为运行 `ibmcloud cr token-list` 时显示的令牌描述。如果令牌是由 {{site.data.keyword.containerlong_notm}} 自动创建的，那么描述会设置为 Kubernetes 集群名称。在这种情况下，除去集群时会自动除去该令牌。
  
<p> 
  <strong>提示</strong>：不要将个人信息放入令牌描述中。
</p>

  </dd>
<dt>`-q`, `--quiet`</dt>
<dd>（可选）仅显示令牌，不显示任何周围的文本。</dd>
<dt>`--non-expiring`</dt>
<dd>（可选）创建具有不会到期的访问权的令牌。未设置此参数时，缺省情况下令牌的访问权将在 24 小时后到期。</dd>
<dt>`--readwrite`</dt>
<dd>（可选）创建用于授予读写访问权的令牌。不使用此选项时，缺省情况下访问权为只读。</dd>
</dl>


## `ibmcloud cr token-get`
{: #bx_cr_token_get}

从注册表中检索指定的令牌。

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**参数**
<dl>
<dt>`TOKEN`</dt>
<dd>（可选）要检索的令牌的唯一标识。</dd>
</dl>


## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

显示 {{site.data.keyword.Bluemix_notm}} 帐户存在的所有令牌。

```
ibmcloud cr token-list --format FORMAT
```
{: codeblock}

**参数**
<dl>
<dt>`--format FORMAT`</dt>
<dd>（可选）使用 Go 模板来设置输出元素的格式。

有关更多信息，请参阅[对 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤](registry_cli_reference.html#registry_cli_listing)。

</dd>
</dl>


## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

除去一个或多个指定的令牌。

```
ibmcloud cr token-rm TOKEN [TOKEN...]
```
{: codeblock}

**参数**
<dl>
<dt>`TOKEN`</dt>
<dd>（可选）TOKEN 可以是令牌本身，也可以是令牌的唯一标识，如 `ibmcloud cr token-list` 中所示。可以指定多个令牌，并且令牌之间必须以一个空格分隔。</dd>
</dl>


## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

查看映像的漏洞评估报告。

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**参数**
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

有关更多信息，请参阅[使用漏洞顾问程序管理映像安全性](/docs/services/va/va_index.html)。

</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>（可选）命令输出以所选格式返回。缺省格式为 `text`。支持以下格式：

<ul>

<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>（可选）命令输出限制为仅显示漏洞。</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>（可选）命令输出限制为仅显示配置问题。</dd>
<dt>`--extended`, `-e`</dt>
<dd>（可选）命令输出显示有关有漏洞包的修订的其他信息。</dd>

</dl>
