---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-07"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands, cli

subcollection: container-registry-cli-plugin

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

You can use the {{site.data.keyword.registrylong}} CLI, which is provided in the `container-registry` CLI plug-in, to manage your registry and its resources for your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

## Prerequisites
{: #containerregcli_prereq}

- Install the {{site.data.keyword.cloud_notm}} CLI, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.
- Before you run the registry commands, log in to {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command to generate an access token and authenticate your session.

In the command line, you are notified when updates to the `ibmcloud` CLI and `container-registry` CLI plug-ins are available. Ensure that you keep your CLI up-to-date so that you can use all the available commands and options.

If you want to view the current version of your `container-registry` CLI plug-in, run `ibmcloud plugin list`.

To find out about how to use the {{site.data.keyword.registrylong_notm}} CLI, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

For more information about the IAM platform and service access roles that are required for some commands, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).

Do not put personal information in your container images, namespace names, description fields, or in any image configuration data (for example, image names or image labels).
{: important}

## `ibmcloud cr api`
{: #bx_cr_api}

Returns the details about the registry API endpoint that the commands are run against.

```
ibmcloud cr api
```
{: codeblock}

### Prerequisites
{: #bx_cr_api_prereq}

None

## `ibmcloud cr build` - deprecated
{: #bx_cr_build}

This command is deprecated from 6 October 2020. You can use [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images) instead. For more information, see the [{{site.data.keyword.registrylong_notm}} is Deprecating Container Builds](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecating-container-builds){: external} blog post.
{: deprecated}

Builds a Docker image in {{site.data.keyword.registrylong_notm}}.

The `br-sao`, `ca-tor`, and `jp-osa` regions don't have a build service because they were created after the command was deprecated.
{: note}

Builds are pushed to the private domain name of the registry over a private connection, but you can pull the image from all domains.
{: tip}

You can't use [IAM IP allowlists](/docs/Registry?topic=Registry-registry_iam_ip) in combination with the `ibmcloud cr image-build` command.
{: note}

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY --accept-deprecation
```
{: codeblock}

### Prerequisites
{: #bx_cr_build_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_build_option}

<dl>
<dt><code>DIRECTORY</code></dt>
<dd>The location of your build context, which contains your Dockerfile and prerequisite files. If you run the command when your working directory is set to where your build context is stored, you can replace <code>DIRECTORY</code> with a period (.).</dd>
<dt><code>--no-cache</code></dt>
<dd>(Optional)  If specified, cached image layers from previous builds are not used in this build.</dd>
<dt><code>--pull</code></dt>
<dd>(Optional) If specified, the base images are pulled, even if an image with a matching tag exists on the build host.</dd>
<dt><code>--quiet</code>, <code>-q</code></dt>
<dd>(Optional) If specified, the build output is suppressed unless an error occurs.</dd>
<dt><code>--build-arg KEY=VALUE</code></dt>
<dd>(Optional) Specify an extra build argument in the format <code>'KEY=VALUE'</code>. Multiple build arguments can be specified by including this option multiple times. The value of each build argument is available as an environment variable when you specify an ARG line that matches the key in your Dockerfile.</dd>
<dt><code>--file FILE</code>, <code>-f FILE</code></dt>
<dd>(Optional) If you use the same files for multiple builds, you can choose a path to a different Dockerfile. Specify the location of the Dockerfile relative to the build context. If not specified, the default is <code>PATH/Dockerfile</code>, where <code>PATH</code> is the root of the build context.</dd>
<dt><code>--tag TAG</code>, <code>-t TAG</code></dt>
<dd>The full name for the image that you want to build, which includes the registry URL and namespace.</dd>
<dt><code>--accept-deprecation</code></dt>
<dd>(Optional) Confirm that you are aware that the build command is deprecated, and will be removed soon.</dd>
</dl>

### Example
{: #bx_cr_build_example}

Build a Docker image that doesn’t use a build cache from previous builds, where the build output is suppressed, the tag is *`us.icr.io/birds/bluebird:1`*, and the directory is your working directory.

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Create an exemption for a security issue. You can create an exemption for a security issue that applies to different scopes. The scope can be the account, namespace, repository, digest, or tag.

You can identify the images in the scope by using either the tag or the digest. You can reference the image by digest `<dns>/<namespace>/<repo>@<digest>`, which affects the digest and all of its tags in the same repository, or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag. To list all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command.
{: tip}

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_add_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_add_option}

<dl>
<dt><code>--scope SCOPE</code></dt>
<dd>To set your account as the scope, use <code>"*"</code> as the value. To set a namespace, repository, digest, or tag as the scope, enter the value in one of the following formats: <code>namespace</code>, <code>namespace/repository</code>, <code>namespace/repository:tag</code>, <code>namespace/repo@digest</code>.
</dd>
<dt><code>--issue-type ISSUE_TYPE</code></dt>
<dd>The type of security issue that you want to exempt. To find valid issue types, run <code>ibmcloud cr exemption-types</code>.
</dd>
<dt><code>--issue-id ISSUE_ID</code></dt>
<dd>The ID of the security issue that you want to exempt. To find an issue ID, run <code>ibmcloud cr va &lt;image&gt;</code>, where <code>&lt;image&gt;</code> is the name of your image, and use the relevant value from either the <strong>Vulnerability ID</strong> or <strong>Configuration Issue ID</strong> column.
</dd>
</dl>

### Examples
{: #bx_cr_exemption_add_example}

Create a CVE exemption for CVE with ID `CVE-2018-17929` for all images in the `us.icr.io/birds/bluebird` repository.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Create an account-wide CVE exemption for CVE with ID `CVE-2018-17929`.

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Create a configuration issue exemption for issue `application_configuration:nginx.ssl_protocols` for a single image with the tag `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

Create a configuration issue exemption for issue `application_configuration:nginx.ssl_protocols` for a single image with the digest `us.icr.io/birds/bluebird@sha256:101010101010`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird@sha256:101010101010 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

List your exemptions for security issues.

You can identify the images in the scope by using either the tag or the digest. You can reference the image by digest `<dns>/<namespace>/<repo>@<digest>`, which affects the digest and all of its tags in the same repository, or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag. To list all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command.
{: tip}

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_list_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_list_option}

<dl>
<dt><code>--scope SCOPE</code></dt>
<dd>(Optional) List only the exemptions that apply to this scope. To set a namespace, repository, digest, or tag as the scope, enter the value in one of the following formats: <code>namespace</code>, <code>namespace/repository</code>, <code>namespace/repository:tag</code>, <code>namespace/repo@digest</code>.
</dd>
</dl>

### Examples
{: #bx_cr_exemption_list_example}

List all your exemptions for security issues that apply to images in the *`birds/bluebird`* repository. The output includes exemptions that are account-wide, exemptions that are scoped to the *`birds`* namespace, and exemptions that are scoped to the *`birds/bluebird`* repository. The output doesn't include any exemptions that are scoped to specific tags within the *`birds/bluebird`* repository.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

List all your exemptions for security issues that apply to images in the *`birds/bluebird@sha256:101010101010`* digest. The output includes exemptions that are account-wide, exemptions that are scoped to the *`birds`* namespace, and exemptions that are scoped to the *`birds/bluebird`* repository and to the *`birds/bluebird@sha256:101010101010`* digest. The output doesn't include any exemptions that are scoped to specific tags within the *`birds/bluebird`* repository.

```
ibmcloud cr exemption-list --scope birds/bluebird@sha256:101010101010
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Delete an exemption for a security issue. To view your existing exemptions, run `ibmcloud cr exemption-list`.

You can identify the images in the scope by using either the tag or the digest. You can reference the image by digest `<dns>/<namespace>/<repo>@<digest>`, which affects the digest and all of its tags in the same repository, or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag. To list all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command.
{: tip}

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_rm_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_rm_option}

<dl>
<dt><code>--scope SCOPE</code></dt>
<dd>To set your account as the scope, use <code>"*"</code> as the value. To set a namespace, repository, digest, or tag as the scope, enter the value in one of the following formats: <code>namespace</code>, <code>namespace/repository</code>, <code>namespace/repository:tag</code>, <code>namespace/repo@digest</code>.
</dd>
<dt><code>--issue-type ISSUE_TYPE</code></dt>
<dd>The issue type of the exemption for the security issue that you want to remove. To find the issue types for your exemptions, run <code>ibmcloud cr exemption-list</code>.
</dd>
<dt><code>--issue-id ISSUE_ID</code></dt>
<dd>The ID of the exemption for the security issue that you want to remove. To find the issue IDs for your exemptions, run <code>ibmcloud cr exemption-list</code>.
</dd>
</dl>

### Examples
{: #bx_cr_exemption_rm_example}

Delete a CVE exemption for CVE with ID `CVE-2018-17929` for all images in the `us.icr.io/birds/bluebird` repository.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Delete an account-wide CVE exemption for CVE with ID `CVE-2018-17929`.

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Delete a configuration issue exemption for issue `application_configuration:nginx.ssl_protocols` for a single image with the tag `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

Delete a configuration issue exemption for issue `application_configuration:nginx.ssl_protocols` for a single image with the digest `us.icr.io/birds/bluebird@sha256:101010101010`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird@sha256:101010101010 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Lists the types of security issues that you can exempt.

```
ibmcloud cr exemption-types
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_types_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

If you are using IAM authentication, this command enables fine-grained authorization. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam) and [Defining user access role policies](/docs/Registry?topic=Registry-user#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

### Prerequisites
{: #bx_cr_iam_policies_enable_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

Displays the IAM policy status of the targeted {{site.data.keyword.registrylong_notm}} account. For more information, see [Managing access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam) and [Defining user access role policies](/docs/Registry?topic=Registry-user#user).

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-digests` (`ibmcloud cr digests`)
{: #bx_cr_image_digests}

Lists all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, in your {{site.data.keyword.cloud_notm}} account. If you want to list tagged images only, run the [`ibmcloud cr image-list`](#bx_cr_image_list) command.

You can refer to an image by using a combination of the **Repository** column and the **Digest** column, for example, `repository@digest`. You can also refer to the image name by using a combination of the content of the **Repository** column and one of the tags in the **Tags** column in the format: `repository:tag`.
{: tip}

```
ibmcloud cr image-digests [--format FORMAT | --quiet | -q | --json] [--restrict RESTRICTION] [--include-ibm] [--no-va]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_digests_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_digests_option}

<dl>
<dt><code>--format FORMAT</code></dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=Registry-registry_cli_list).

</dd>
<dt><code>--quiet</code>, <code>-q</code></dt>
<dd>(Optional) Each image is listed in the format: <code>repository@digest</code></dd>
<dt><code>--json</code></dt>
<dd>(Optional) Outputs the list in JSON format.</dd>
<dt><code>--restrict RESTRICTION</code></dt>
<dd>(Optional) Limit the output to display only images in the specified namespace or repository. </dd>
<dt><code>--include-ibm</code></dt>
<dd>(Optional) Includes {{site.data.keyword.IBM_notm}}-provided public images in the output. By default only private images are listed. You can view {{site.data.keyword.IBM_notm}}-provided  images in the global registry only.</dd>
<dt><code>--no-va</code></dt>
<dd>(Optional) Excludes the security status (Vulnerability Advisor) results from the output. If you don't need the security status results as part of your <code>ibmcloud cr image-digests</code> output, you can use this option to increase performance.</dd>
</dl>

### Example
{: #bx_cr_image_digests_example}

Display all the images in the *`birds`* namespace, including untagged images, in the format `repository@digest`.

```
ibmcloud cr image-digests --restrict birds --quiet
```
{: pre}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Displays details about a specific image. You can reference the image that you want to inspect either by digest, `repository@digest`, or by tag,`repository:tag`.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_inspect_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_inspect_option}

<dl>
<dt><code>--format FORMAT</code></dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=Registry-registry_cli_list).

</dd>
<dt><code>IMAGE</code></dt>
<dd>The name of the image for which you want to get a report. You can inspect multiple images by listing each image in the command with a space between each name.

You can identify images by using either the digest <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;@&lt;digest&gt;</code> or by tag <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;:&lt;tag&gt;</code>. Where <code>&lt;dns&gt;</code> is the domain name, <code>&lt;namespace&gt;</code> is the namespace, <code>&lt;repo&gt;</code> is the repository, <code>&lt;digest&gt;</code> is the digest, and <code>&lt;tag&gt;</code> is the tag.

<p>To find the names of your images, run one of the following commands:

<ul>
<li>To identify your image by digest, run the <code>ibmcloud cr image-digests</code> command. Combine the content of the <strong>Repository</strong> column and the <strong>Digest</strong> column, for example, <code>repository@digest</code>.</li>
<li>To identify your image by tag, run the <code>ibmcloud cr image-list</code> command. Combine the content of the <strong>Repository</strong> and <strong>Tag</strong> columns to create the image name in the format <code>repository:tag</code>. If a tag is not specified in the image name, the image that is tagged <code>latest</code> is deleted by default.</li>
</ul></p>

</dd>
</dl>

### Example
{: #bx_cr_image_inspect_example}

Display details about the exposed ports for the image `us.icr.io/birds/bluebird:1`, by using the formatting directive `"{{ .Config.ExposedPorts }}"`.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Displays all tagged images in your {{site.data.keyword.cloud_notm}} account. If you want to list all your images, including untagged images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command.

The image name is the combination of the content of the **Repository** and **Tag** columns in the format: `repository:tag`
{: tip}

```
ibmcloud cr image-list [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm] [--no-trunc] [--show-type] [--no-va]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_list_option}

<dl>
<dt><code>--format FORMAT</code></dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=Registry-registry_cli_list).

</dd>
<dt><code>--quiet</code>, <code>-q</code></dt>
<dd>(Optional) Each image is listed in the format: <code>repository:tag</code></dd>
<dt><code>--restrict RESTRICTION</code></dt>
<dd>(Optional) Limit the output to display only images in the specified namespace or repository. </dd>
<dt><code>--include-ibm</code></dt>
<dd>(Optional) Includes {{site.data.keyword.IBM_notm}}-provided public images in the output. By default only private images are listed. You can view {{site.data.keyword.IBM_notm}}-provided images in the global registry only.</dd>
<dt><code>--no-trunc</code></dt>
<dd>(Optional) Do not truncate the image digests.</dd>
<dt><code>--show-type</code></dt>
<dd>(Optional) Displays the image manifest type.</dd>
<dt><code>--no-va</code></dt>
<dd>(Optional) Excludes the security status (Vulnerability Advisor) results from the output. If you don't need the security status results as part of your <code>ibmcloud cr image-list</code> output, you can use this option to increase performance.</dd>
</dl>

### Example
{: #bx_cr_image_list_example}

Display the images in the *`birds`* namespace in the format `repository:tag`, without truncating the image digests.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-prune-untagged`
{: #ic_cr_image_prune_untagged}

Delete all [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images in your {{site.data.keyword.registrylong_notm}} account.
{: shortdesc}

```
ibmcloud cr image-prune-untagged [--force | -f [--json]] --restrict RESTRICTION
```
{: codeblock}

### Prerequisites
{: #ic_cr_image_prune_untagged_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #ic_cr_image_prune_untagged_option}

<dl>
<dt><code>--force, -f</code></dt>
<dd>(Optional) Force the command to run with no user prompts.</dd>
<dt><code>--json</code></dt>
<dd>(Optional) Outputs JSON that contains the results of cleaning up your untagged images. This option must be used with <code>--force</code>.</dd>
<dt><code>--restrict</code></dt>
<dd>(Optional) Limit the clean up to only untagged images in the specified namespace or repository.</dd>
</dl>

### Example
{: #ic_cr_image_prune_untagged_example}

Delete all untagged images that are in the *`birds`* namespace and output the results in JSON format.

```
ibmcloud cr image-prune-untagged [--force | -f [--json]] --restrict birds
```
{: pre}

## `ibmcloud cr image-restore`
{: #bx_cr_image_restore}

Restore a deleted image from the trash. You can choose to restore by tag or by digest. If you restore by digest, the digest and all of its tags in the same repository are restored. To find out what is in the trash, run the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command.
{: shortdesc}

```
ibmcloud cr image-restore IMAGE
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_restore_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_restore_option}

<dl>
<dt><code>IMAGE</code></dt>
<dd>The name of the image that you want to restore from the trash.
<p>To find the names of your images in the trash, run the <code>ibmcloud cr trash-list</code> command. You can identify images by using either the tag or the digest. The image to restore can be referenced by digest <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;@&lt;digest&gt;</code>, which restores the digest and all of its tags in the same repository, or by tag <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;:&lt;tag&gt;</code>. Where <code>&lt;dns&gt;</code> is the domain name, <code>&lt;namespace&gt;</code> is the namespace, <code>&lt;repo&gt;</code> is the repository, <code>&lt;digest&gt;</code> is the digest, and <code>&lt;tag&gt;</code> is the tag.</p>

<p>Images are stored in the trash for 30 days.</p>

</dd>
</dl>

### Example
{: #bx_cr_image_restore_example}

To restore the image `us.icr.io/birds/bluebird:1`, run the following command.

```
ibmcloud cr image-restore us.icr.io/birds/bluebird:1
```
{: pre}

For more information about how to use the `ibmcloud cr image-restore` command, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Delete one or more specified images from {{site.data.keyword.registrylong_notm}}. You can reference the image that you want to delete either by digest or by tag.

Where multiple tags exist for the same image digest within a repository, the `ibmcloud cr image-rm` command removes the underlying image and all its tags. If the same image exists in a different repository or namespace, that copy of the image is not removed. If you want to remove a tag from an image and leave the underlying image and any other tags in place, use the [`ibmcloud cr image-untag`](#bx_cr_image_untag) command.
{: tip}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore a selected image by running the  [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_rm_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_rm_option}

<dl>
<dt><code>IMAGE</code></dt>
<dd>The name of the image that you want to delete. You can delete multiple images at the same time by listing each image in the command with a space between each name. You can identify images by using either the digest <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;@&lt;digest&gt;</code> or by tag <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;:&lt;tag&gt;</code>. Where <code>&lt;dns&gt;</code> is the domain name, <code>&lt;namespace&gt;</code> is the namespace, <code>&lt;repo&gt;</code> is the repository, <code>&lt;digest&gt;</code> is the digest, and <code>&lt;tag&gt;</code> is the tag.

<p>Images are stored in the trash for 30 days.</p>

<p>To find the names of your images, run one of the following commands:

<ul>
<li>To identify your image by digest, run the <code>ibmcloud cr image-digests</code> command. Combine the content of the <strong>Repository</strong> column and the <strong>Digest</strong> column, for example, <code>repository@digest</code>.</li>
<li>To identify your image by tag, run the <code>ibmcloud cr image-list</code> command. Combine the content of the <strong>Repository</strong> and <strong>Tag</strong> columns to create the image name in the format <code>repository:tag</code>. If a tag is not specified in the image name, the image that is tagged <code>latest</code> is deleted by default.</li>
</ul></p>

</dd>
</dl>

### Example
{: #bx_cr_image_rm_example}

Delete the image `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

Add a tag that you specify in the command to an existing image, copy the tag to another repository, or copy the tag to a repository in a different namespace. When you copy a tag, any Red Hat&reg; signatures for its digest are also copied. The target image, `TARGET_IMAGE`, is the new image and the source image, `SOURCE_IMAGE`, is the existing image in {{site.data.keyword.registrylong_notm}}. The source and target images must be in the same region. You can reference the source image that you want to tag by either digest, `repository@digest`, or by tag, `repository:tag`. You must reference the target image by tag.

You can identify source images by using either the digest `<dns>/<namespace>/<repo>@<digest>` or by tag `<dns>/<namespace>/<repo>:<tag>`. You must reference the target image by tag, `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag.

To find the names of your images, use one of the following alternatives:

- To identify your image by digest, run the `ibmcloud cr image-digests` command. Combine the content of the **Repository** column and the **Digest** column, for example, `repository@digest`.
- To identify your image by tag, run the `ibmcloud cr image-list` command. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`.

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_tag_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_tag_option}

<dl>
<dt><code>SOURCE_IMAGE</code></dt>
<dd>The name of the source image. You can identify source images by using either the digest <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;@&lt;digest&gt;</code> or by tag <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;:&lt;tag&gt;</code>. Where <code>&lt;dns&gt;</code> is the domain name, <code>&lt;namespace&gt;</code> is the namespace, <code>&lt;repo&gt;</code> is the repository, <code>&lt;digest&gt;</code> is the digest, and <code>&lt;tag&gt;</code> is the tag.

</dd>
<dt><code>TARGET_IMAGE</code></dt>
<dd>The name of the target image. <code>TARGET_IMAGE</code> must be in the format <code>repository:tag</code>, for example, <code>us.icr.io/namespace/image:latest</code>.

</dd>
</dl>

### Examples
{: #bx_cr_image_tag_example}

Add another tag reference, `latest`, to the image `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

Copy the image `us.icr.io/birds/bluebird:peck` to another repository in the same namespace `birds/pigeon`.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

Copy the image `us.icr.io/birds/bluebird:peck` to another namespace `animals` to which you have access.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr image-untag`
{: #bx_cr_image_untag}

Remove a tag, or tags, from each specified image in {{site.data.keyword.registrylong_notm}}.

To remove a specific tag from an image and leave the underlying image and any other tags in place, use the `ibmcloud cr image-untag` command. If you want to delete the underlying image, and all of its tags, use the [`ibmcloud cr image-rm`](#bx_cr_image_rm) command instead.
{: tip}

```
ibmcloud cr image-untag IMAGE [IMAGE...]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_untag_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_untag_option}

<dl>
<dt><code>IMAGE</code></dt>
<dd>The name of the image for which you want to remove the tag. You can delete the tag from multiple images at the same time by listing each image in the command with a space between each name. <code>IMAGE</code> must be in the format <code>repository:tag</code>, for example, <code>us.icr.io/namespace/image:latest</code>.

<p>To find the names of your images, run <code>ibmcloud cr image-list</code>. Combine the content of the <strong>Repository</strong> and <strong>Tag</strong> columns to create the image name in the format <code>repository:tag</code>. If a tag is not specified in the image name, the command fails.</p>

</dd>
</dl>

### Example
{: #bx_cr_image_untag_example}

Remove the tag `1` from the image `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-untag us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

Displays the name and the account of the registry that you are logged in to.

```
ibmcloud cr info
```
{: codeblock}

### Prerequisites
{: #bx_cr_info_prereq}

None

## `ibmcloud cr login`
{: #bx_cr_login}

This command runs the `docker login` command against the registry. The `docker login` command is required to be able to run the `docker push` or `docker pull` commands for the registry. This command is not required to run other `ibmcloud cr` commands. If Docker is not installed, this command returns an error message.

```
ibmcloud cr login
```
{: codeblock}

Logging in to {{site.data.keyword.registrylong_notm}} by using the `ibmcloud cr login` command is subject to IAM login session limits. If your login expires, see [Why does the {{site.data.keyword.registrylong_notm}} login keep expiring?](/docs/Registry?topic=Registry-troubleshoot-login-expire) for assistance.
{: tip}

### Prerequisites
{: #bx_cr_login_prereq}

None

## `ibmcloud cr manifest-inspect`
{: #bx_cr_manifest_inspect}

View the contents of the manifest for an image. You can reference the image that you want to inspect either by digest or by tag.

```
ibmcloud cr manifest-inspect [--quiet | -q ] IMAGE
```
{: codeblock}

### Prerequisites
{: #bx_cr_manifest_inspect_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_manifest_inspect_option}

<dl>
<dt><code>IMAGE</code></dt>
<dd>The name of the image for which you want to inspect the manifest. You can identify images by using either the digest <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;@&lt;digest&gt;</code> or by tag <code>&lt;dns&gt;/&lt;namespace&gt;/&lt;repo&gt;:&lt;tag&gt;</code>. Where <code>&lt;dns&gt;</code> is the domain name, <code>&lt;namespace&gt;</code> is the namespace, <code>&lt;repo&gt;</code> is the repository, <code>&lt;digest&gt;</code> is the digest, and <code>&lt;tag&gt;</code> is the tag.

<p>To find the names of your images, run one of the following commands:

<ul>
<li>To identify your image by digest, run the <code>ibmcloud cr image-digests</code> command. Combine the content of the <strong>Repository</strong> column and the <strong>Digest</strong> column, for example, <code>repository@digest</code>.</li>
<li>To identify your image by tag, run the <code>ibmcloud cr image-list</code> command. Combine the content of the <strong>Repository</strong> and <strong>Tag</strong> columns to create the image name in the format <code>repository:tag</code>.</li>
</ul></p>
</dd>

<dt><code>--quiet</code>, <code>-q</code></dt>
<dd>(Optional) Reduces the output to display essential elements only.</dd>
</dl>

### Example
{: #bx_cr_manifest_inspect_example}

To view the contents of the manifest for the image `us.icr.io/birds/bluebird:1`, run the following command.

```
ibmcloud cr manifest-inspect us.icr.io/birds/bluebird:1
```
{: codeblock}

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Choose a name for your namespace and add it to your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

You can create a namespace in a resource group of your choice by using one of the following options.

- Before you create the namespace, run the [`ibmcloud target -g <resource_group>`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target) command, where `<resource_group>` is the resource group.
- Specify the required resource group by using the `-g` option on the [`ibmcloud cr namespace-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add) command.

If you create a namespace in a resource group, you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. However, you can still set permissions for the namespace at the account level or in the namespace itself.

Namespaces created in version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020 are created in a resource group. Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the {{site.data.keyword.cloud_notm}} console before 29 July 2020 are not created in a resource group. If you want to assign a namespace to a resource group, see [`ibmcloud cr namespace-assign`](#ic_cr_namespace_assign). Namespaces that are assigned to a resource group show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.
{: tip}

```
ibmcloud cr namespace-add [-g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID)] NAMESPACE
```
{: codeblock}

For more information about resource groups, see [Creating a resource group](/docs/account?topic=account-rgs#create_rgs).

### Prerequisites
{: #bx_cr_namespace_add_prereq}

To find out about the required permissions, see [Platform management roles](/docs/Registry?topic=Registry-iam#platform_management_roles) and [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_namespace_add_option}

<dl>
<dt><code>NAMESPACE</code></dt>
<dd>The namespace that you want to add. The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters, and contain lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.

<p>
<strong>Important</strong> Do not put personal information in your namespace names.
</p>

</dd>
<dt><code>-g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID)</code></dt>
<dd>(Optional) Specify the name or ID of the resource group to which you want to add the namespace. If you don't set this option, the targeted resource group is used. If you don't set this option and a resource group is not targeted, the default resource group for the account is used.
</dd>
</dl>

### Example
{: #bx_cr_namespace_add_example}

Create a namespace with the name *`birds`* and add it to the resource group *`beaks`*.

```
ibmcloud cr namespace-add -g beaks birds
```
{: pre}

## `ibmcloud cr namespace-assign`
{: #ic_cr_namespace_assign}

Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the {{site.data.keyword.cloud_notm}} console before 29 July 2020 are not assigned to resource groups. You can assign an unassigned namespace to a resource group for your {{site.data.keyword.cloud_notm}} account. If you assign a namespace to a resource group, you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. If you don't specify a resource group, and a resource group isn't targeted, the command fails.
{: shortdesc}

You can assign a namespace to a resource group only once. When a namespace is in a resource group, you can't move it to another resource group.
{: note}

To find out which namespaces are assigned to resource groups and which are unassigned, run the [`ibmcloud cr namespace-list`](#bx_cr_namespace_list) command with the `-v` option. Namespaces that are assigned to a resource group also show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.
{: tip}

```
ibmcloud cr namespace-assign -g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID) NAMESPACE
```
{: codeblock}

For more information about resource groups, see [Creating a resource group](/docs/account?topic=account-rgs#create_rgs).

### Prerequisites
{: #ic_cr_namespace_assign_prereq}

To find out about the required permissions, see [Platform management roles](/docs/Registry?topic=Registry-iam#platform_management_roles) and [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #ic_cr_namespace_assign_option}

<dl>
<dt><code>-g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID)</code></dt>
<dd>(Optional) Specify the name or ID of the resource group to which you want to assign the namespace. If you don't set this option, the targeted resource group is used.</dd>
<dt><code>NAMESPACE</code></dt>
<dd>The namespace that you want to assign to a resource group.</dd>
</dl>

### Example
{: #ic_cr_namespace_assign_example}

Assign a namespace with the name *`birds`* to the resource group *`beaks`*.

```
ibmcloud cr namespace-assign -g beaks birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Displays all namespaces that are owned by your {{site.data.keyword.cloud_notm}} account. You can use this command to list your namespaces so that you can verify which namespaces are assigned to resource groups, and which namespaces are unassigned. Namespaces that are assigned to a resource group also show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.

```
ibmcloud cr namespace-list [--verbose | -v]
```
{: codeblock}

### Prerequisites
{: #bx_cr_namespace_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_namespace_list_option}

<dl>
<dt><code>--verbose</code>, <code>-v</code></dt>
<dd>(Optional) List all the namespaces and include information about the resource group and the creation date of the namespace.
</dd>
</dl>

### Example
{: #bx_cr_namespace_list_example}

View a list of all your namespaces, including information about resource groups and creation dates.

```
ibmcloud cr namespace-list  -v
```
{: pre}

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Removes a namespace from your {{site.data.keyword.cloud_notm}} account. Images in this namespace are deleted when the namespace is removed.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

### Prerequisites
{: #bx_cr_namespace_rm_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_namespace_rm_option}

<dl>
<dt><code>NAMESPACE</code></dt>
<dd>The namespace that you want to remove.</dd>
<dt><code>--force</code>, <code>-f</code></dt>
<dd>(Optional) Force the command to run with no user prompts.</dd>
</dl>

### Example
{: #bx_cr_namespace_rm_example}

Remove the namespace *`birds`*.

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

Displays your pricing plan for the registry region that you're targeting.

```
ibmcloud cr plan
```
{: codeblock}

### Prerequisites
{: #bx_cr_plan_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Upgrades you to the standard plan for the registry region that you're targeting.

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

For more information about plans, see [Registry plans](/docs/Registry?topic=Registry-registry_overview#registry_plans).

### Prerequisites
{: #bx_cr_plan_upgrade_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_plan_upgrade_option}

<dl>
<dt><code>PLAN</code></dt>
<dd>(Optional) The name of the pricing plan that you want to upgrade to. If <code>PLAN</code> is not specified, the default is <code>standard</code>.</dd>
</dl>

### Example
{: #bx_cr_plan_upgrade_example}

Upgrade to the standard pricing plan.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr platform-metrics`
{: #ic_cr_platform_metrics}

You can use the command to enable and disable platform metrics. You can also use it to find out whether you have platform metrics set up on your account for the registry region that you're targeting.
{: shortdesc}

If you want to view the platform metrics for {{site.data.keyword.registrylong_notm}}, you must opt in by running the `ibmcloud cr platform-metrics` command.
{: important}

You must specify one of the command options or the command fails with an error.
{: tip}

```
ibmcloud cr platform-metrics --enable | --disable | --status
```
{: codeblock}

For more information about the platform metrics that you can view in {{site.data.keyword.registrylong_notm}}, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor).

### Prerequisites
{: #ic_cr_platform_metrics_prereq}

- You must set up {{site.data.keyword.mon_full_notm}}, see [Getting started tutorial for {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).
- [Enable your {{site.data.keyword.mon_full_notm}} instance for platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).
- To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #ic_cr_platform_metrics_option}

<dl>
<dt><code>--enable</code></dt>
<dd>(Optional) Enable the setting for your account.</dd>
<dt><code>--disable</code></dt>
<dd>(Optional) Disable the setting for your account.</dd>
<dt><code>--status</code></dt>
<dd>(Optional) Display whether the setting is enabled for your account.</dd>
</dl>

### Example
{: #ic_cr_platform_metrics_example}

Enable platform metrics for your account.

```
ibmcloud cr platform-metrics --enable
```
{: pre}

## `ibmcloud cr ppa-archive-load` - obsolete
{: #bx_cr_ppa_archive_load}

The [`ibmcloud cr ppa-archive-load` command is obsolete](/docs/Registry?topic=Registry-registry_release_notes#04may2021_ppa). Containerized software is distributed in {{site.data.keyword.cloud}} Paks, see [{{site.data.keyword.cloud_notm}} Paks](https://www.ibm.com/cloud/paks){: external}. To run {{site.data.keyword.cloud_notm}} Paks on {{site.data.keyword.openshiftlong}}, see [Adding Cloud Paks](/docs/openshift?topic=openshift-openshift_cloud_paks). For more information about setting up your {{site.data.keyword.containerlong_notm}} cluster to pull entitled software, see [Setting up a cluster to pull entitled software](/docs/containers?topic=containers-registry#secret_entitled_software).

## `ibmcloud cr private-only`
{: #ic_cr_private_only}

Prevent image pulls or pushes over public network connections for your account for the registry region that you're targeting. You must specify one of the command options or the command fails with an error.

```
ibmcloud cr private-only --enable | --disable | --status
```
{: codeblock}

### Prerequisites
{: #ic_cr_private_only_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #ic_cr_private_only_option}

<dl>
<dt><code>--enable</code></dt>
<dd>(Optional) Prevent image pulls or pushes over public network connections for your account.</dd>
<dt><code>--disable</code></dt>
<dd>(Optional) Reinstate image pulls or pushes over public network connections for your account.</dd>
<dt><code>--status</code></dt>
<dd>(Optional) Check whether the use of public connections is prevented for image pushes or pulls in your account.</dd>
</dl>

### Example
{: #ic_cr_private_only_example}

Prevent image pulls or pushes over public network connections for your account.

```
ibmcloud cr private-only --enable
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

Displays your current quotas for traffic and storage, and usage information against those quotas for the registry region that you're targeting.

```
ibmcloud cr quota
```
{: codeblock}

### Prerequisites
{: #bx_cr_quota_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Modify the specified quota for the registry region that you're targeting.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

### Prerequisites
{: #bx_cr_quota_set_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_quota_set_option}

<dl>
<dt><code>--traffic TRAFFIC</code></dt>
<dd>(Optional) Changes your traffic quota to the specified value in megabytes. The operation fails if you are not authorized to set traffic, or if you set a value that exceeds your current pricing plan.</dd>
<dt><code>--storage STORAGE</code></dt>
<dd>(Optional) Changes your storage quota to the specified value in megabytes. The operation fails if you are not authorized to set storage quotas, or if you set a value that exceeds your current pricing plan.</dd>
</dl>

### Example
{: #bx_cr_quota_set_example}

Set your quota limit for pull traffic to *7000* megabytes and storage to *600* megabytes.

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

Displays the targeted region and the registry.

```
ibmcloud cr region
```
{: codeblock}

For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

### Prerequisites
{: #bx_cr_region_prereq}

None

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Set a target region for the {{site.data.keyword.registrylong_notm}} commands. To list the available regions, run the command with no options.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

### Prerequisites
{: #bx_cr_region_set_prereq}

None

### Command options
{: #bx_cr_region_set_option}

<dl>
<dt><code>REGION</code></dt>
<dd>(Optional) The name of your target region, for example, <code>us-south</code>.

For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

</dd>
</dl>

### Example
{: #bx_cr_region_set_example}

Target the US South region.

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr retention-policy-list`
{: #bx_cr_retention_policy_list}

List the image retention policies for your account. Image retention policies retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted. You can also see whether the option to retain all untagged images applies to the policy.
{: shortdesc}

Where an image within a repository is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

```
ibmcloud cr retention-policy-list
```
{: codeblock}

### Prerequisites
{: #bx_cr_retention_policy_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Example
{: #bx_cr_retention_policy_list_example}

List the retention policies in your account.

```
ibmcloud cr retention-policy-list
```
{: pre}

For more information about how to use the `ibmcloud cr retention-policy-list` command, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## `ibmcloud cr retention-policy-set`
{: #bx_cr_retention_policy_set}

Set a policy to retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted. When you set a policy it runs interactively, then it runs daily. You can set only one policy in each namespace.
{: shortdesc}

You can choose whether to exclude all untagged images from the total number of images that you decide to retain.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If a retention policy deletes an image that you want to keep, you can restore the image. To identify the image, list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore the selected image by running the  [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

If you want to cancel a retention policy, see [Updating a retention policy so that it keeps all your images](/docs/Registry?topic=Registry-registry_retention#retention_policy_keep).

```
ibmcloud cr retention-policy-set [--retain-untagged] --images IMAGECOUNT NAMESPACE
```
{: codeblock}

### Prerequisites
{: #bx_cr_retention_policy_set_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_retention_policy_set_option}

<dl>
<dt><code>NAMESPACE</code></dt>
<dd>The namespace for which you want to create a policy.</dd>
<dt><code>--retain-untagged</code></dt>
<dd>(Optional) Retain all untagged images when the retention policy is being processed. Only tagged images are analyzed and, if the images don't meet the criteria, they are deleted. If the option isn't specified, all tagged and untagged images are analyzed and, if the images don't meet the criteria, they are deleted.</dd>
<dt><code>--images</code></dt>
<dd>Determines how many images to keep within each repository in the specified namespace. The newest images are retained. The age of images is determined by their build date. <code>IMAGECOUNT</code> is the number of images that you want to retain in each repository for the namespace. To return a policy to the default state that keeps all the images, set <code>IMAGECOUNT</code> to <code>All</code>.</dd>
</dl>

### Examples
{: #bx_cr_retention_policy_set_example}

Set a policy that retains the newest 20 images within each repository in the namespace `birds`.

```
ibmcloud cr retention-policy-set --images 20 birds
```
{: pre}

Set the policy back to the default state so that you keep all your images in the namespace `birds`.

```
ibmcloud cr retention-policy-set --images All birds
```
{: pre}

For more information about how to use the `ibmcloud cr retention-policy-set` command, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## `ibmcloud cr retention-run`
{: #bx_cr_retention_run}

Cleans up a namespace by retaining a specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.
{: shortdesc}

You can choose whether to exclude all untagged images from the total number of images that you decide to retain.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore a selected image by running the  [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

```
ibmcloud cr retention-run [--force | -f [--json]] [--retain-untagged] --images IMAGECOUNT NAMESPACE
```
{: codeblock}

### Prerequisites
{: #bx_cr_retention_run_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_retention_run_option}

<dl>
<dt><code>NAMESPACE</code></dt>
<dd>The namespace that you want to clean up.</dd>
<dt><code>--force</code>, <code>-f</code></dt>
<dd>(Optional) Force the command to run with no user prompts.</dd>
<dt><code>--json</code></dt>
<dd>(Optional) Outputs JSON that contains the results of cleaning your namespace. This option must be used with <code>--force</code>.</dd>
<dt><code>--retain-untagged</code></dt>
<dd>(Optional) Retain all untagged images when the retention policy is being processed. Only tagged images are analyzed and, if the images don't meet the criteria, they are deleted. If the option isn't specified, all tagged and untagged images are analyzed and, if the images don't meet the criteria, they are deleted.</dd>
<dt><code>--images</code></dt>
<dd>Determines how many images to keep within each repository in the specified namespace. The newest images are retained. The age of images is determined by their build date. <code>IMAGECOUNT</code> is the number of images that you want to retain in each repository for the namespace.
</dd>
</dl>

### Example
{: #bx_cr_retention_run_example}

Retain the newest 20 images within each repository, in the namespace `birds`.

```
ibmcloud cr retention-run --images 20 birds
```
{: pre}

For more information about how to use the `ibmcloud cr retention-run` command, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## `ibmcloud cr token-get` - discontinued
{: #bx_cr_token_get}

From 19 August 2021, using {{site.data.keyword.registrylong_notm}} tokens is discontinued and will no longer work. For more information, see [{{site.data.keyword.registrylong_notm}} Deprecates Registry Tokens for Authentication](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecates-registry-tokens-for-authentication){: external}.
{: deprecated}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`) - discontinued
{: #bx_cr_token_list}

From 19 August 2021, using {{site.data.keyword.registrylong_notm}} tokens is discontinued and will no longer work. For more information, see [{{site.data.keyword.registrylong_notm}} Deprecates Registry Tokens for Authentication](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecates-registry-tokens-for-authentication){: external}.
{: deprecated}

## `ibmcloud cr token-rm` - discontinued
{: #bx_cr_token_rm}

From 19 August 2021, using {{site.data.keyword.registrylong_notm}} tokens is discontinued and will no longer work. For more information, see [{{site.data.keyword.registrylong_notm}} Deprecates Registry Tokens for Authentication](https://www.ibm.com/cloud/blog/announcements/ibm-cloud-container-registry-deprecates-registry-tokens-for-authentication){: external}.
{: deprecated}

## `ibmcloud cr trash-list`
{: #bx_cr_trash_list}

Displays all images in the trash in your {{site.data.keyword.cloud_notm}} account. You can also see the number of remaining days until the image is removed from the trash. The number of remaining days until removal is rounded up. For example, if the time until removal is 2 hours, it shows as 1 day. Images remain in the trash for 30 days after they are deleted from your live repository.

If you want to restore an image from the trash, run the [`ibmcloud cr image-restore`](#bx_cr_image_restore) command, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

```
ibmcloud cr trash-list [--restrict NAMESPACE] [--json]
```
{: codeblock}

### Prerequisites
{: #bx_cr_trash_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_trash_list_option}

<dl>
<dt><code>--restrict NAMESPACE</code></dt>
<dd>(Optional) Limit the output to display only images in the specified namespace. </dd>
<dt><code>--json</code></dt>
<dd>(Optional) Outputs JSON that contains the details of the contents of the trash.</dd>
</dl>

### Example
{: #bx_cr_trash_list_example}

Display the images that are in the trash in the *`birds`* namespace.

```
ibmcloud cr trash-list --restrict birds
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

View a vulnerability assessment report for your images.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

### Prerequisites
{: #bx_cr_va_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_va_option}

<dl>
<dt><code>IMAGE</code></dt>
<dd>The name of the image for which you want to get a report. The report states whether the image has any known package vulnerabilities. You can request reports for multiple images at the same time by listing each image in the command with a space between each name.

<p>To find the names of your images, run <code>ibmcloud cr image-list</code>. Combine the content of the <strong>Repository</strong> and <strong>Tag</strong> columns to create the image name in the format <code>repository:tag</code>. If a tag is not specified in the image name, the report assesses the image that is tagged <code>latest</code>.</p>

<p>The following operating systems are supported:

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>{{site.data.keyword.redhat_full}} Enterprise Linux&reg; (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

For more information, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index).

</dd>
<dt><code>--extended</code>, <code>-e</code></dt>
<dd>(Optional) The command output shows additional information about fixes for vulnerable packages.</dd>
<dt><code>--vulnerabilities</code>, <code>-v</code></dt>
<dd>(Optional) The command output is restricted to show vulnerabilities only.</dd>
<dt><code>--configuration-issues</code>, <code>-c</code></dt>
<dd>(Optional) The command output is restricted to show configuration issues only.</dd>
<dt><code>--output FORMAT</code>, <code>-o FORMAT</code></dt>
<dd>(Optional) The command output is returned in the chosen format. The default format is <code>text</code>. The following formats are supported:

<ul>
<li><code>text</code></li>
<li><code>json</code></li>
</ul>

</dd>
</dl>

### Examples
{: #bx_cr_va_example}

View a standard vulnerability assessment report for your image.

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

View a vulnerability assessment report for your image `us.icr.io/birds/bluebird:1` in JSON format, showing vulnerabilities only.

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}


