---

copyright:
  years: 2017, 2020
lastupdated: "2020-02-28"

keywords: commands, format commands, filter command output, private registry, registry commands, formatting output, filtering output, output, Go template options, data types, cli

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
{:term: .term}
{:external: target="_blank" .external}

# Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands
{: #registry_cli_list}

You can format and filter the CLI output for supported {{site.data.keyword.registrylong}} commands.
{:shortdesc}

By default, the CLI output is displayed in a human-readable format. However, this view might limit your ability to use the output, particularly if the command is run programmatically. For example, in the `ibmcloud cr image-list` CLI output, you might want to sort the `Size` field by numerical size, but the command returns a string description of the size. The `container-registry` CLI plug-in provides the format option that you can use to apply a Go template to the CLI output. The Go template is a feature of the [Go programming language](https://golang.org/pkg/text/template/){: external} that you can use to customize the CLI output.

You can alter the CLI output by applying the format option in two different ways:

1. Format data in your CLI output. For example, change the `Created` field output from UNIX time to standard time.
2. Filter data in your CLI output. For example, filter by details of the image to display a specific subset of images by using the Go template `if gt` condition.

You can use the format option with the following {{site.data.keyword.registrylong_notm}} commands. Click a command to view a list of available fields and their data types.

- [`ibmcloud cr image-digests`](#registry_cli_list_imagedigests)
- [`ibmcloud cr image-list`](#registry_cli_list_imagelist)
- [`ibmcloud cr image-inspect`](#registry_cli_list_imageinspect)

The following code examples demonstrate how you might use the formatting and filtering options.

- Run the following `ibmcloud cr image-digests` command to display all untagged images referenced by their digests:

  ```
  ibmcloud cr image-digests --format '{{if not .Tags}}{{.Repository}}@{{.Digest}}{{end}}'
  ```
  {: pre}

  The following message is an example of the output from the command:

  ```
  example-<region>.icr.io/user1/ibmliberty@<digest1>
  example-<region>.icr.io/user1/ibmliberty@<digest2>
  example-<region>.icr.io/user1/ibmliberty@<digest3>
  ```
  {: screen}

- Run the following `ibmcloud cr image-list` command to display repository, tag, and security status of all tagged images that have a size over 1 MB:

  ```
  ibmcloud cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
  ```
  {: pre}

  The following message is an example of the output from the command:

  ```
  example-<region>.icr.io/user1/ibmliberty:latest No Issues
  example-<region>.icr.io/user1/ibmnode:1 2 Issues
  example-<region>.icr.io/user1/ibmnode:test1 1 Issue
  example-<region>.icr.io/user1/ibmnode2:test2 7 Issues
  ```
  {: screen}

- Run the following `ibmcloud cr image-inspect` command to display where {{site.data.keyword.IBM_notm}} documentation is hosted for a specified {{site.data.keyword.IBM_notm}} public image:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"
  ```
  {: pre}

  The following message is an example of the output from the command:

  ```
  map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
  ```
  {: screen}

- Run the following `ibmcloud cr image-inspect` command to display the exposed ports for a specified image:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"
  ```
  {: pre}

  The following message is an example of the output from the command:

  ```
  map[9080/tcp: 9443/tcp:]
  ```
  {: screen}

## Go template options and data types in the `ibmcloud cr image-digests` command
{: #registry_cli_list_imagedigests}

Review the following table to find available Go template options and data types for the [`ibmcloud cr image-digests`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests) command.
{:shortdesc}

| Field | Type | Description |
|-----|----|-----------|
| `Created` | Integer (64 bit) | Displays when the image was created, expressed in number of seconds in [UNIX time](https://en.wikipedia.org/wiki/Unix_time){: external}. |
| `Digest` | String | Displays the unique identifier for an image. |
| `ManifestType` | String | Displays the image manifest type. |
| `Repository` | String | Displays the repository of the image. |
| `SecurityStatus` | Object | Displays the vulnerability status for the image. You can filter and format the following values: *Status*  `string`, *IssueCount*  `int`, and *ExemptionCount*  `int`. The possible statuses are described in [Reviewing a vulnerability report by using the CLI](/docs/Registry?topic=va-va_index#va_registry_cli). |
| `Size` | Integer (64 bit) | Displays the size of the image in bytes. |
| `Tags` | Array of strings | Displays the tags for the image. |
{: caption="Table 1. Available fields and data types in the <code>ibmcloud cr image-digests</code> command." caption-side="top"}

## Go template options and data types in the `ibmcloud cr image-list` command
{: #registry_cli_list_imagelist}

Review the following table to find available Go template options and data types for the [`ibmcloud cr image-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) command.
{:shortdesc}

| Field | Type | Description |
|-----|----|-----------|
| `Created` | Integer (64 bit) | Displays when the image was created, expressed in number of seconds in [UNIX time](https://en.wikipedia.org/wiki/Unix_time){: external}. |
| `Digest` | String | Displays the unique identifier for an image. |
| `ManifestType` | String | Displays the image manifest type. |
| `Namespace` | String | Displays the namespace where the image is stored. |
| `Repository` | String | Displays the repository of the image. |
| `SecurityStatus` | Object | Displays the vulnerability status for the image. You can filter and format the following values: *Status*  `string`, *IssueCount*  `int`, and *ExemptionCount*  `int`. The possible statuses are described in [Reviewing a vulnerability report by using the CLI](/docs/Registry?topic=va-va_index#va_registry_cli). |
| `Size` | Integer (64 bit) | Displays the size of the image in bytes. |
| `Tag` | String | Displays the tag for the image. |
{: caption="Table 2. Available fields and data types in the <code>ibmcloud cr image-list</code> command." caption-side="top"}

## Go template options and data types in the `ibmcloud cr image-inspect` command
{: #registry_cli_list_imageinspect}

Review the following table to find available Go template options and data types for the [`ibmcloud cr image-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) command.
{:shortdesc}

| Field | Type | Description |
|-----|----|-----------|
| `Architecture` | String | Displays the processor architecture that was used to build this image, and that is required to run the image. |
| `Author` | String | Displays the author of the image. |
| `Comment` | String | Displays the description of the image. |
| `Config` | Object | Displays configuration metadata for the image. See the field details in [`Config`](#registry_cli_list_imageinspect_config). |
| `Container` | String | Displays the ID of the container that created the image. |
| `ContainerConfig` | Object | Displays the default configuration for containers that are started from this image. See the field details in [`Config`](#registry_cli_list_imageinspect_config). |
| `Created` | String | Displays the [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time){: external} when the image was created. |
| `DockerVersion` | String | Displays the Docker version that was used to build this image. |
| `ID` | String | Displays the unique identifier for an image. |
| `Os` | String | Displays the operating system family that was used to build this image, and that is required to run the image. |
| `OsVersion` | String | Displays the version of the operating system that was used to build this image. |
| `Parent` | String | Displays the ID of the parent image that was used to build this image. |
| `RootFS` | Object | Displays metadata that describe the root file system for the image. See the field details in [`RootFS`](#registry_cli_list_imageinspect_rootfs). |
| `Size` | Integer (64 bit) | Displays the size of the image in bytes. |
| `VirtualSize` | Integer (64 bit) | Displays the sum of the size of each layer in the image in bytes. |
{: caption="Table 3. Available fields and data types in the <code>ibmcloud cr image-inspect</code> command." caption-side="top"}

### `Config`
{: #registry_cli_list_imageinspect_config}

| Field | Type | Description |
|-----|----|-----------|
| `ArgsEscaped` | Boolean | Displays true if the command is already escaped (Windows specific). |
| `AttachStderr` | Boolean | Displays _true_ if the standard error stream is attached to the container and _false_ if not. |
| `AttachStdin` | Boolean | Displays _true_ if the standard input stream is attached to the container and _false_ if not. |
| `AttachStdout` | Boolean | Displays _true_ if the standard output stream is attached to the container and _false_ if not. |
| `Cmd` | Array of strings|Describes the commands and arguments that are passed to a container to run when the container is started. |
| `Domainname` | String | Displays the fully qualified domain name of the container. |
| `Entrypoint` | Array of strings | Describes the command that is run when the container starts. |
| `Env` | Array of strings | Displays the list of environment variables in the form of key-value pairs. |
| `ExposedPorts` | Key-value map | Displays the list of exposed ports in the format `[123:,456:]`. |
| `Healthcheck` | Object | Describes how to check that the container is working correctly. See the field details in [`Healthcheck`](#registry_cli_list_imageinspect_healthcheck). |
| `Hostname` | String | Displays the host name of the container. |
| `Image` | String | Displays the name of the image that was passed by the operator. |
| `Labels` | Key-value map | Displays the list of labels that were added to the image as key-value pairs. |
| `MacAddress` | String | Displays the MAC address that is assigned to the container. |
| `NetworkDisabled` | Boolean | Displays _true_ if the networking is disabled for the container and _false_ if the networking is enabled for the container. |
| `OnBuild` | Array of strings | Displays the `ONBUILD` metadata that were defined on the image Dockerfile. |
| `OpenStdin` | Boolean | Displays _true_ if the standard input stream is opened and _false_ if the standard input stream is closed. |
| `Shell` | Array of strings | Displays the shell-form of RUN, CMD, ENTRYPOINT. |
| `StdinOnce` | Boolean | Displays _true_ if the standard input stream is closed after the attached client disconnects and _false_ if the standard input stream stays open. |
| `StopSignal` | String | Describes the UNIX stop signal to send when to stop the container. |
| `StopTimeout` | Integer | Displays the timeout in seconds to stop a container. |
| `Tty` | Boolean | Displays _true_ if a `pseudo-tty` is allocated to the container and _false_ if not. |
| `User` | String | Displays the user that runs commands inside the container where the image is used. |
| `Volumes` | Key-Value map | Displays the list of volume mounts that are mounted to a container. |
| `WorkingDir` | String | Displays the working directory inside the container where specified commands are run. |
{: caption="Table 4. Available fields and data types in <code>Config</code>. " caption-side="top"}

### `Healthcheck`
{: #registry_cli_list_imageinspect_healthcheck}

| Field | Type | Description |
|-----|----|-----------|
| `Interval` | Integer (64 bit)|Displays the time to wait between two health checks in nanoseconds. |
| `Retries` | Integer|Displays the number of consecutive failures that are needed to consider a container as not working correctly. |
| `Test` | Array of strings | Displays how to run the health check test. Available options are: </br></br>`{}`: inherit the health check</br></br>`{"NONE"}`: the health check is disabled</br></br>`{"CMD", args...}`: exec arguments directly</br></br>`{"CMD-SHELL", command}`: run the command with the system's default shell |
| `Timeout` | Integer (64 bit) | Displays the time to wait before considering the health check to have failed in nanoseconds. |
{: caption="Table 5. Available fields and data types in the <code>Healthcheck</code>." caption-side="top"}

### `RootFS`
{: #registry_cli_list_imageinspect_rootfs}

| Option | Type | Description |
|------|----|-----------|
| `BaseLayer` | String | Displays the descriptor for the base layer in the image. |
| `Layers` | Array of strings|Displays the descriptors of each image layer. |
| `Type` | String | Displays the type of file system. |
{: caption="Table 6. Available fields and data types in the <code>RootFS</code>." caption-side="top"}
