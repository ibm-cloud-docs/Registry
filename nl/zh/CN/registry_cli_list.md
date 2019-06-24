---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-17"

keywords: IBM Cloud Container Registry, commands, format commands, filter command output, private registry, registry commands, formatting output, filtering output, output, Go template options, data types, 

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

# 对 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤
{: #registry_cli_list}

可以对支持的 {{site.data.keyword.registrylong_notm}} 命令的 CLI 输出进行格式设置和过滤。
{:shortdesc}

缺省情况下，CLI 输出会以人类可读的格式显示。但是，此视图可能会限制您使用输出的能力，尤其是在以编程方式运行命令的情况下。例如，在 `ibmcloud cr image-list` CLI 输出中，您可能希望按数字大小对 `Size` 字段排序，但命令返回的是对大小的字符串描述。`container-registry` CLI 插件提供了 format 选项，可用于将 Go 模板应用于 CLI 输出。Go 模板是 [Go 编程语言 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://golang.org/pkg/text/template/) 的功能部件，可用于定制 CLI 输出。

可以通过两种不同方式应用 format 选项来变更 CLI 输出：

1. 设置 CLI 输出中数据的格式。例如，将 `Created` 字段输出从 UNIX 时间更改为标准时间。
2. 过滤 CLI 输出中的数据。例如，通过使用 Go 模板 `if gt` 条件，按映像详细信息进行过滤以显示特定映像子集。

可以将 format 选项用于以下 {{site.data.keyword.registrylong_notm}} 命令。单击命令可查看可用字段及其数据类型的列表。

- [`ibmcloud cr image-list`](#registry_cli_list_imagelist)
- [`ibmcloud cr image-inspect`](#registry_cli_list_imageinspect)
- [`ibmcloud cr token-list`](#registry_cli_list_tokenlist)

以下代码示例演示了可如何对选项进行格式设置和过滤。

- 运行以下 `ibmcloud cr image-list` 命令，以显示大小超过 1 MB 的所有映像的存储库、标记和安全状态：

  ```
ibmcloud cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
    ```
  {: pre}

  **示例输出**

  ```
  example-<region>.icr.io/user1/ibmliberty:latest No Issues
  example-<region>.icr.io/user1/ibmnode:1 2 Issues
  example-<region>.icr.io/user1/ibmnode:test1 1 Issue
  example-<region>.icr.io/user1/ibmnode2:test2 7 Issues
  ```
  {: screen}

- 运行以下 `ibmcloud cr image-inspect` 命令，以显示指定 IBM 公共映像的 IBM 文档的托管位置：

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"
  ```
  {: pre}

  **示例输出**

  ```
    map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
    ```
  {: screen}

- 运行以下 `ibmcloud cr image-inspect` 命令，以显示指定映像的已公开端口：

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"
  ```
  {: pre}

  **示例输出**

  ```
    map[9080/tcp: 9443/tcp:]
    ```
  {: screen}

- 运行以下 `ibmcloud cr token-list` 命令，以显示所有只读令牌：

  ```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
  {: pre}

  **示例输出**

  ```
    0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
    ```
  {: screen}

## `ibmcloud cr image-list` 命令中的 Go 模板选项和数据类型
{: #registry_cli_list_imagelist}

查看下表以查找 `ibmcloud cr image-list` 命令的可用 Go 模板选项和数据类型。
{:shortdesc}

|字段|类型|描述|
|-----|----|-----------|
|`Created`|整数（64 位）|显示映像创建时间，用秒数（[UNIX 时间 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/Unix_time)）表示。|
|`Digest`|字符串|显示映像的唯一标识。|
|`Namespace`|字符串|显示存储映像的名称空间。|
|`Repository`|字符串|显示映像的存储库。|
|`Size`|整数（64 位）|显示映像的大小（以字节为单位）。|
|`Tag`|字符串|显示映像的标记。|
|`SecurityStatus`|结构|显示映像的漏洞状态。您可以过滤以下值，还可以为这些值设置格式：*Status*  `string`、*IssueCount*  `int` 和 *ExemptionCount*  `int`。有关可能的状态，请参阅[使用 CLI 查看漏洞报告](/docs/services/Registry?topic=va-va_index#va_registry_cli)。|
{: caption="表 1. <code>ibmcloud cr image-list</code> 命令中的可用字段和数据类型" caption-side="top"}

## `ibmcloud cr image-inspect` 命令中的 Go 模板选项和数据类型
{: #registry_cli_list_imageinspect}

查看下表以查找 `ibmcloud cr image-inspect` 命令的可用 Go 模板选项和数据类型。
{:shortdesc}

|字段|类型|描述|
|-----|----|-----------|
|`ID`|字符串|显示映像的唯一标识。|
|`Parent`|字符串|显示用于构建此映像的父映像的标识。|
|`Comment`|字符串|显示映像的描述。|
|`Created`|字符串|显示映像创建时的 [UNIX 时间戳记 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/Unix_time)。|
|`Container`|字符串|显示已创建映像的容器的标识。|
|`ContainerConfig`|对象|显示基于此映像启动的容器的缺省配置。请参阅 [`Config`](#registry_cli_list_imageinspect_config) 中的字段详细信息。|
|`DockerVersion`|字符串|显示用于构建此映像的 Docker 版本。|
|`Author`|字符串|显示映像的创建者。|
|`Config`|对象|显示映像的配置元数据。请参阅 [`Config`](#registry_cli_list_imageinspect_config) 中的字段详细信息。|
|`Architecture`|字符串|显示用于构建此映像以及运行此映像所需的处理器体系结构。|
|`Os`|字符串|显示用于构建此映像以及运行此映像所需的操作系统系列。|
|`OsVersion`|字符串|显示用于构建此映像的操作系统版本。|
|`Size`|整数（64 位）|显示映像的大小（以字节为单位）。|
|`VirtualSize`|整数（64 位）|显示映像中每层大小的总和（以字节为单位）。|
|`RootFS`|对象|显示用于描述映像的根文件系统的元数据。请参阅 [`RootFS`](#registry_cli_list_imageinspect_rootfs) 中的字段详细信息。|
{: caption="表 2. <code>ibmcloud cr image-inspect</code> 命令中的可用字段和数据类型" caption-side="top"}

### `Config`
{: #registry_cli_list_imageinspect_config}

|字段|类型|描述|
|-----|----|-----------|
|`Hostname`|字符串|显示容器的主机名。|
|`Domainname`|字符串|显示容器的标准域名。|
|`User`|字符串|显示在使用映像的容器内部运行命令的用户。|
|`AttachStdin`|布尔值|如果标准输入流连接到容器，将显示 _true_；否则，将显示 _false_。|
|`AttachStdout`|布尔值|如果标准输出流连接到容器，将显示 _true_；否则，将显示 _false_。|
|`AttachStderr`|布尔值|如果标准错误流连接到容器，将显示 _true_；否则，将显示 _false_。|
|`ExposedPorts`|键值映射|显示已公开端口的列表，格式为 `[123:,456:]`。|
|`Tty`|布尔值|如果将 `pseudo-tty` 分配给容器，将显示 _true_；否则，将显示 _false_。|
|`OpenStdin`|布尔值|如果标准输入流已打开，将显示 _true_；如果标准输入流已关闭，将显示 _false_。|
|`StdinOnce`|布尔值|如果标准输入流在所连接客户机断开连接后关闭，将显示 _true_；如果标准输入流保持打开，将显示 _false_。|
|`Env`|字符串数组|显示环境变量的列表，格式为键值对。|
|`Cmd`|字符串数组|描述传递给容器以在启动容器时运行的命令和自变量。|
|`Healthcheck`|对象|描述如何检查容器是否正常工作。请参阅 [`Healthcheck`](#registry_cli_list_imageinspect_healthcheck) 中的字段详细信息。|
|`ArgsEscaped`|布尔值|如果命令已经转义（特定于 Windows），将显示 true。|
|`Image`|字符串|显示操作程序传递的映像的名称。|
|`Volumes`|键值映射|显示安装到容器的卷安装的列表。|
|`WorkingDir`|字符串|显示运行指定命令的容器内部的工作目录。|
|`Entrypoint`|字符串数组|描述在容器启动时运行的命令。|
|`NetworkDisabled`|布尔值|如果容器禁用了联网，将显示 _true_；如果容器启用了联网，将显示 _false_。|
|`MacAddress`|字符串|显示分配给容器的 MAC 地址。|
|`OnBuild`|字符串数组|显示映像 Dockerfile 上定义的 `ONBUILD` 元数据。|
|`Labels`|键值映射|显示作为键值对添加到映像的标签的列表。|
|`StopSignal`|字符串|描述要停止容器时发送的 UNIX 停止信号。|
|`StopTimeout`|整数|显示停止容器的超时（以秒为单位）。|
|`Shell`|字符串数组|显示 shell 格式的 RUN、CMD 和 ENTRYPOINT。|
{: caption="表 3. <code>Config</code> 中的可用字段和数据类型。" caption-side="top"}

### `Healthcheck`
{: #registry_cli_list_imageinspect_healthcheck}

|字段|类型|描述|
|-----|----|-----------|
|`Test`|字符串数组|显示如何运行运行状况检查测试。可用选项包括：<ul><li>`{}`：继承运行状况检查</li><li>`{"NONE"}`：禁用运行状况检查</li><li>`{"CMD", args...}`：直接执行自变量</li><li>`{"CMD-SHELL", command}`：使用系统的缺省 shell 程序运行命令</li></ul>|
|`Interval`|整数（64 位）|显示两次运行状况检查之间等待的时间（以纳秒为单位）。|
|`Timeout`|整数（64 位）|显示将运行状况检查视为失败之前等待的时间（以纳秒为单位）。|
|`Retries`|整数|显示将容器视为工作不正常所需的连续失败次数。|
{: caption="表 4. <code>Healthcheck</code> 结构中的可用字段和数据类型。" caption-side="top"}

### `RootFS`
{: #registry_cli_list_imageinspect_rootfs}

|选项|类型|描述|
|------|----|-----------|
|`Type`|字符串|显示文件系统的类型。|
|`Layers`|字符串数组|显示每个映像层的描述符。|
|`BaseLayer`|字符串|显示映像中基本层的描述符。|
{: caption="表 5. <code>RootFS</code> 结构中的可用字段和数据类型。" caption-side="top"}

## `ibmcloud cr token-list` 命令中的 Go 模板选项和数据类型
{: #registry_cli_list_tokenlist}

查看下表以查找 `ibmcloud cr token-list` 命令的可用 Go 模板选项和数据类型。
{:shortdesc}

|字段|类型|描述|
|-----|----|-----------|
|`ID`|字符串|显示令牌的唯一标识。|
|`Expiry`|整数（64 位）|显示令牌到期时的 [UNIX 时间戳记 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/Unix_time)。|
|`ReadOnly`|布尔值|只能拉出映像时显示 _true_，可以向名称空间推送映像以及从名称空间中拉出映像时显示 _false_。|
|`描述`|字符串|显示令牌的描述。|
{: caption="表 6. <code>ibmcloud cr token-list</code> 命令中的可用字段和数据类型" caption-side="top"}
