---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

You can use the {{site.data.keyword.registrylong}} CLI, which is provided in the container-registry plug-in, to manage your registry and its resources for your {{site.data.keyword.Bluemix_notm}} account.
{: shortdesc}

**Prerequisites**

* Install the [{{site.data.keyword.Bluemix_notm}} CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/cli/index.html#overview). The prefix for running commands by using the {{site.data.keyword.Bluemix_notm}} CLI is `ibmcloud`.

* Before running the registry commands, log in to {{site.data.keyword.Bluemix_notm}} with the `ibmcloud login` command to generate an access token and authenticate your session.

In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Ensure that you keep your CLI up-to-date so that you can use all the available commands and flags.

If you want to view the current version of your {{site.data.keyword.registrylong}} CLI plug-in (`container-registry`), run `ibmcloud plugin list`.

To find out about how to use the {{site.data.keyword.registrylong_notm}} CLI, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/services/Registry/index.html#index).

For more information about the IAM platform and service access roles that are required for some commands, see [Managing user access with Identity and Access Management](/docs/services/Registry/iam.html#iam).

Do not put personal information in your container images, namespace names, description fields (for example, in registry tokens), or in any image configuration data (for example, image names or image labels).
{:tip}

<table summary="Manage {{site.data.keyword.registrylong_notm}}">
<caption>Table 1. Commands for managing {{site.data.keyword.registrylong_notm}}
</caption>
 <thead>
 <th colspan="5">Commands for managing the registry</th>
 </thead>
 <tbody>
 <tr>
 <td>[ibmcloud cr api](#bx_cr_api)</td>
 <td>[ibmcloud cr build](#bx_cr_build)</td>
 <td>[ibmcloud cr exemption-add](#bx_cr_exemption_add)</td>
 <td>[ibmcloud cr exemption-list (ibmcloud cr exemptions)](#bx_cr_exemption_list)</td>
 <td>[ibmcloud cr exemption-rm](#bx_cr_exemption_rm)</td>
 </tr>
 <tr>
 <td>[ibmcloud cr exemption-types](#bx_cr_exemption_types)</td>
 <td>[ibmcloud cr iam-policies-enable](#bx_cr_iam_policies_enable)</td>
 <td>[ibmcloud cr image-inspect](#bx_cr_image_inspect)</td>
 <td>[ibmcloud cr image-list (ibmcloud cr images)](#bx_cr_image_list)</td>
 <td>[ibmcloud cr image-rm](#bx_cr_image_rm)</td>
 </tr>
 <tr>

 <td>[ibmcloud cr info](#bx_cr_info)</td>
 <td>[ibmcloud cr login](#bx_cr_login)</td>
 <td>[ibmcloud cr namespace-add](#bx_cr_namespace_add)</td>
 <td>[ibmcloud cr namespace-list (ibmcloud cr namespaces)](#bx_cr_namespace_list)</td>
 <td>[ibmcloud cr namespace-rm](#bx_cr_namespace_rm)</td>
 </tr>
 <tr>
 <td>[ibmcloud cr plan](#bx_cr_plan)</td>
 <td>[ibmcloud cr plan-upgrade](#bx_cr_plan_upgrade)</td>
 <td>[ibmcloud cr ppa-archive-load](#bx_cr_ppa_archive_load)</td>
 <td>[ibmcloud cr quota](#bx_cr_quota)</td>
 <td>[ibmcloud cr quota-set](#bx_cr_quota_set)</td>
 </tr>
 <tr>
 <td>[ibmcloud cr region](#bx_cr_region)</td>
 <td>[ibmcloud cr region-set](#bx_cr_region_set)</td>
 <td>[ibmcloud cr token-add](#bx_cr_token_add)</td>
 <td>[ibmcloud cr token-get](#bx_cr_token_get)</td>
 <td>[ibmcloud cr token-list (ibmcloud cr tokens)](#bx_cr_token_list)</td>
 </tr>
 <tr>
 <td>[ibmcloud cr token-rm](#bx_cr_token_rm)</td>
 <td>[ibmcloud cr vulnerability-assessment (ibmcloud cr va)](#bx_cr_va)</td>
 </tr>
 </tbody></table>

## ibmcloud cr api
{: #bx_cr_api}

Returns the details about the registry API endpoint that the commands are run against.

```
ibmcloud cr api
```
{: codeblock}

**Prerequisites** 

None

## ibmcloud cr build
{: #bx_cr_build}

Builds a Docker image in {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Prerequisites** 

Required permissions: Writer or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`DIRECTORY`</dt>
<dd>The location of your build context, which contains your Dockerfile and prerequisite files. If you run the command when your working directory is set to where your build context is stored, you can replace `DIRECTORY` with a period (.).</dd>
<dt>`--no-cache`</dt>
<dd>(Optional)  If specified, cached image layers from previous builds are not used in this build.</dd>
<dt>`--pull`</dt>
<dd>(Optional) If specified, the base images are pulled even if an image with a matching tag already exists on the build host.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) If specified, the build output is suppressed unless an error occurs.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(Optional) Specify an additional build argument in the format `'KEY=VALUE'`. Multiple build arguments can be specified by including this parameter multiple times. The value of each build argument is available as an environment variable when you specify an ARG line that matches the key in your Dockerfile.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(Optional) If you use the same files for multiple builds, you can choose a path to a different Dockerfile. Specify the location of the Dockerfile relative to the build context. If not specified, the default is `PATH/Dockerfile`, where PATH is the root of the build context.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>The full name for the image that you want to build, which includes the registry URL and namespace.</dd>
</dl>

## ibmcloud cr exemption-add
{: #bx_cr_exemption_add}

Create an exemption for a security issue. You can create an exemption for a security issue that applies to different scopes. The scope can be the account, namespace, repository, or tag.

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>To set your account as the scope, use `"*"` as the value. To set a namespace, repository, or tag as the scope, enter the value in one of the following formats: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>The type of security issue that you want to exempt. To find valid issue types, run `ibmcloud cr exemption-types`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>The ID of the security issue that you want to exempt. To find an issue ID, run `ibmcloud cr va <image>`, where *&lt;image&gt;* is the name of your image, and use the relevant value from either the **Vulnerability ID** or **Configuration Issue ID** column.
</dd>
</dl>

## ibmcloud cr exemption-list (ibmcloud cr exemptions)
{: #bx_cr_exemption_list}

List your exemptions for security issues.

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(Optional) List only the exemptions that apply to this scope. To set a namespace, repository, or tag as the scope, enter the value in one of the following formats: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
</dl>

## ibmcloud cr exemption-rm
{: #bx_cr_exemption_rm}

Delete an exemption for a security issue. To view your existing exemptions, run `ibmcloud cr exemption-list`.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>To set your account as the scope, use `"*"` as the value. To set a namespace, repository, or tag as the scope, enter the value in one of the following formats: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>The issue type of the exemption for the security issue that you want to remove. To find the issue types for your exemptions, run `ibmcloud cr exemption-list`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>The ID of the exemption for the security issue that you want to remove. To find the issue IDs for your exemptions, run `ibmcloud cr exemption-list`.
</dd>
</dl>

## ibmcloud cr exemption-types
{: #bx_cr_exemption_types}

Lists the types of security issues that you can exempt.

```
ibmcloud cr exemption-types
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

## ibmcloud cr iam-policies-enable
{: #bx_cr_iam_policies_enable}

If you are using IAM authentication, this command enables fine-grained authorization. For more information, see [Managing user access with Identity and Access Management](/docs/services/Registry/iam.html#iam) and [Defining user access role policies](/docs/services/Registry/registry_users.html#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

## ibmcloud cr image-inspect
{: #bx_cr_image_inspect}

Displays details about a specific image.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Prerequisites** 

Required permissions: Reader or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/services/Registry/registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>`IMAGE`</dt>
<dd>The name of the image for which you want to get a report. You can inspect multiple images by listing each image in the command with a space between each name.

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the image that is tagged `latest` is inspected. </p>

</dd>
</dl>

## ibmcloud cr image-list (ibmcloud cr images)
{: #bx_cr_image_list}

Displays all images in your {{site.data.keyword.Bluemix_notm}} account.

The image name is the combination of the content of the **Repository** and **Tag** columns in the format: `repository:tag`
{:tip}

```
 ibmcloud cr image-list [--no-trunc] [--format FORMAT] [-q, --quiet] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Prerequisites** 

Required permissions: Reader or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--no-trunc`</dt>
<dd>(Optional) Do not truncate the image digests.</dd>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/services/Registry/registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>`-q`, `--quiet`</dt>
<dd>(Optional) Each image is listed in the format: `repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Optional) Limit the output to display only images in the specified namespace or namespace and repository. </dd>
<dt>`--include-ibm`</dt>
<dd>(Optional) Includes {{site.data.keyword.IBM_notm}}-provided public images in the output. Without this option, by default private images only are listed.</dd>
</dl>

## ibmcloud cr image-rm
{: #bx_cr_image_rm}

Delete one or more specified images from your registry.

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Prerequisites** 

Required permissions: Writer or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`IMAGE`</dt>
<dd>The name of the image for which you want to get a report. You can delete multiple images at the same time by listing each image in the command with a space between each name.

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the image that is tagged `latest` is deleted by default.</p>

</dd>
</dl>

## ibmcloud cr info
{: #bx_cr_info}

Displays the name and the account of the registry that you are logged in to.

```
ibmcloud cr info
```
{: codeblock}

**Prerequisites** 

None

## ibmcloud cr login
{: #bx_cr_login}

This command runs the `docker login` command against the registry. The `docker login` command is required to be able to run the `docker push` or `docker pull` commands for the registry. This command is not required to run other `ibmcloud cr` commands. If Docker is not installed, this command returns an error message.

```
ibmcloud cr login
```
{: codeblock}

**Prerequisites** 

None

## ibmcloud cr namespace-add
{: #bx_cr_namespace_add}

Choose a name for your namespace and add it to your {{site.data.keyword.Bluemix_notm}} account.

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**Prerequisites** 

Required permissions: Writer or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`NAMESPACE`</dt>
<dd>The namespace you want to add. The namespace must be unique across all {{site.data.keyword.Bluemix_notm}} accounts in the same region. Namespaces must be between 4 and 30 characters long, and contain lowercase letters, numbers, hyphens, and underscores only. Namespaces must start and end with a letter or number.
  
<p>  
<strong>Tip</strong>: Do not put personal information in your namespace names.
</p>
  
</dd>
</dl>

## ibmcloud cr namespace-list (ibmcloud cr namespaces)
{: #bx_cr_namespace_list}

Displays all namespaces that are owned by your {{site.data.keyword.Bluemix_notm}} account.

```
ibmcloud cr namespace-list
```
{: codeblock}

**Prerequisites** 

Required permissions: Reader or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

## ibmcloud cr namespace-rm
{: #bx_cr_namespace_rm}

Removes a namespace from your {{site.data.keyword.Bluemix_notm}} account. Images in this namespace are deleted when the namespace is removed.

```
ibmcloud cr namespace-rm NAMESPACE
```
{: codeblock}

**Prerequisites** 

Required permissions: Writer or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`NAMESPACE`</dt>
<dd>The namespace that you want to remove.</dd>
</dl>

## ibmcloud cr plan
{: #bx_cr_plan}

Displays your pricing plan.

```
ibmcloud cr plan
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

## ibmcloud cr plan-upgrade
{: #bx_cr_plan_upgrade}

Upgrades you to the standard plan.

For information about plans, see [Registry plans](/docs/services/Registry/registry_overview.html#registry_plans).

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`PLAN`</dt>
<dd>The name of the pricing plan that you want to upgrade to. If `PLAN` is not specified, the default is `standard`.</dd>
</dl>

## ibmcloud cr ppa-archive-load
{: #bx_cr_ppa_archive_load}

Imports IBM software that is downloaded from [IBM Passport Advantage Online for customers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/passportadvantage/pao_customer.html) and packaged for use with Helm into your private registry namespace.

Container images are pushed to your private {{site.data.keyword.registryshort_notm}} namespace. Helm charts are written to a `ppa-import` directory that is created in the directory from which you run the command. Optionally, you can use the [Chart Museum open source project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) to host helm charts.

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Prerequisites** 

Required permissions: Writer or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>The path to the compressed file that is downloaded from IBM Passport Advantage.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>One of your namespaces. Container images from the compressed file are pushed to this namespace. To list namespaces, run `ibmcloud cr namespace-list`.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Optional) Your [Chart Museum ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) unique resource identifier.</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(Optional) Your [Chart Museum ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) user name.</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(Optional) Your [Chart Museum ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) password.</dd>
</dl>

## ibmcloud cr quota
{: #bx_cr_quota}

Displays your current quotas for traffic and storage, and usage information against those quotas.

```
ibmcloud cr quota
```
{: codeblock}

**Prerequisites** 

Required permissions: Reader, Writer, or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

## ibmcloud cr quota-set
{: #bx_cr_quota_set}

Modify the specified quota.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Prerequisites** 

Required permissions: Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(Optional) Changes your traffic quota to the specified value in megabytes. The operation fails if you are not authorized to set traffic, or if you set a value that exceeds your current pricing plan.</dd>
<dt>`--storage STORAGE`</dt>
<dd>(Optional) Changes your storage quota to the specified value in megabytes. The operation fails if you are not authorized to set storage quotas, or if you set a value that exceeds your current pricing plan.</dd>
</dl>

## ibmcloud cr region
{: #bx_cr_region}

Displays the targeted region and the registry.

```
ibmcloud cr region
```
{: codeblock}

**Prerequisites** 

None

For more information, see [Regions](/docs/services/Registry/registry_overview.html#registry_regions).

## ibmcloud cr region-set
{: #bx_cr_region_set}

Set a target region for the {{site.data.keyword.registrylong_notm}} commands. To list the available regions, run the command with no parameters.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**Prerequisites** 

None

**Command options**
<dl>
<dt>`REGION`</dt>
<dd>(Optional) The name of your target region, for example, `us-south`.

For more information, see [Regions](/docs/services/Registry/registry_overview.html#registry_regions).

</dd>
</dl>

## ibmcloud cr token-add
{: #bx_cr_token_add}

Add a token that you can use to control access to a registry.

```
ibmcloud cr token-add [--description DESCRIPTION] [-q, --quiet] [--non-expiring] [--readwrite]
```
{: codeblock}

**Prerequisites** 

Required permissions: Administrator IAM platform role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>(Optional) Specifies the value as a description for the token, which is displayed when you run `ibmcloud cr token-list`. If your token is created automatically by {{site.data.keyword.containerlong_notm}}, the description is set to your Kubernetes cluster name. In this case, the token is removed automatically when your cluster is removed.
  
<p> 
  <strong>Tip</strong>: Do not put personal information in your token description.
</p>

</dd>
<dt>`-q`, `--quiet`</dt>
<dd>(Optional) Displays the token only, without any surrounding text.</dd>
<dt>`--non-expiring`</dt>
<dd>(Optional) Creates a token with access that does not expire. Without this parameter set, access from a token expires after 24 hours by default.</dd>
<dt>`--readwrite`</dt>
<dd>(Optional) Creates a token that grants read and write access. Without this option, access is read-only by default.</dd>
</dl>

## ibmcloud cr token-get
{: #bx_cr_token_get}

Retrieve the specified token from the registry.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**Prerequisites** 

Required permissions: Administrator IAM platform role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`TOKEN`</dt>
<dd>(Optional) The unique identifier of the token that you want to retrieve. To list your tokens, run `ibmcloud cr token-list`.</dd>
</dl>

## ibmcloud cr token-list (ibmcloud cr tokens)
{: #bx_cr_token_list}

Displays all tokens that exist for your {{site.data.keyword.Bluemix_notm}} account.

```
ibmcloud cr token-list --format FORMAT
```
{: codeblock}

**Prerequisites** 

Required permissions: Administrator IAM platform role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/services/Registry/registry_cli_reference.html#registry_cli_listing).

</dd>
</dl>

## ibmcloud cr token-rm
{: #bx_cr_token_rm}

Remove one or more specified tokens.

```
ibmcloud cr token-rm TOKEN [TOKEN...]
```
{: codeblock}

**Prerequisites** 

Required permissions: Administrator IAM platform role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`TOKEN`</dt>
<dd>(Optional) TOKEN can be either the token itself, or the unique identifier of the token, as shown in `ibmcloud cr token-list`. Multiple tokens can be specified and they must be separated by a space.</dd>
</dl>

## ibmcloud cr vulnerability-assessment (ibmcloud cr va)
{: #bx_cr_va}

View a vulnerability assessment report for your images.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Prerequisites** 

Required permissions: Reader or Manager IAM service access role for {{site.data.keyword.registrylong_notm}}

**Command options**
<dl>
<dt>`IMAGE`</dt>
<dd>The name of the image for which you want to get a report. The report tells you whether the image has any known package vulnerabilities. You can request reports for multiple images at the same time by listing each image in the command with a space between each name.

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the report assesses the image that is tagged `latest`. </p>

<p>The following operating systems are supported:

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

For more information, see [Managing image security with Vulnerability Advisor](/docs/services/va/va_index.html).

</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(Optional) The command output is returned in the chosen format. The default format is `text`. The following formats are supported:

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Optional) The command output is restricted to show vulnerabilities only.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Optional) The command output is restricted to show configuration issues only.</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Optional) The command output shows additional information about fixes for vulnerable packages.</dd>

</dl>
