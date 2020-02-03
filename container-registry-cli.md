---

copyright:
  years: 2017, 2020
lastupdated: "2020-02-03"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands, cli

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
{:term: .term}
{:external: target="_blank" .external}


# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

You can use the {{site.data.keyword.registrylong}} CLI, which is provided in the `container-registry` CLI plug-in, to manage your registry and its resources for your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

## Prerequisites
{: #containerregcli_prereq}

- Install the {{site.data.keyword.cloud_notm}} CLI, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started). The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.
- Before running the registry commands, log in to {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command to generate an access token and authenticate your session.

In the command line, you are notified when updates to the `ibmcloud` CLI and `container-registry` CLI plug-ins are available. Ensure that you keep your CLI up-to-date so that you can use all the available commands and flags.

If you want to view the current version of your `container-registry` CLI plug-in, run `ibmcloud plugin list`.

To find out about how to use the {{site.data.keyword.registrylong_notm}} CLI, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-getting-started#getting-started).

For more information about the IAM platform and service access roles that are required for some commands, see [Managing user access with Identity and Access Management](/docs/Registry?topic=registry-iam#iam).

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

## `ibmcloud cr build`
{: #bx_cr_build}

Builds a Docker image in {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

### Prerequisites
{: #bx_cr_build_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_build_option}

<dl>
<dt>`DIRECTORY`</dt>
<dd>The location of your build context, which contains your Dockerfile and prerequisite files. If you run the command when your working directory is set to where your build context is stored, you can replace `DIRECTORY` with a period (.).</dd>
<dt>`--no-cache`</dt>
<dd>(Optional)  If specified, cached image layers from previous builds are not used in this build.</dd>
<dt>`--pull`</dt>
<dd>(Optional) If specified, the base images are pulled, even if an image with a matching tag already exists on the build host.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) If specified, the build output is suppressed unless an error occurs.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(Optional) Specify an extra build argument in the format `'KEY=VALUE'`. Multiple build arguments can be specified by including this parameter multiple times. The value of each build argument is available as an environment variable when you specify an ARG line that matches the key in your Dockerfile.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(Optional) If you use the same files for multiple builds, you can choose a path to a different Dockerfile. Specify the location of the Dockerfile relative to the build context. If not specified, the default is `PATH/Dockerfile`, where PATH is the root of the build context.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>The full name for the image that you want to build, which includes the registry URL and namespace.</dd>
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

Create an exemption for a security issue. You can create an exemption for a security issue that applies to different scopes. The scope can be the account, namespace, repository, or tag.

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_add_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_add_option}

<dl>
<dt>`--scope SCOPE`</dt>
<dd>To set your account as the scope, use `"*"` as the value. To set a namespace, repository, or tag as the scope, enter the value in one of the following formats: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>The type of security issue that you want to exempt. To find valid issue types, run `ibmcloud cr exemption-types`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>The ID of the security issue that you want to exempt. To find an issue ID, run `ibmcloud cr va <image>`, where `<image>` is the name of your image, and use the relevant value from either the **Vulnerability ID** or **Configuration Issue ID** column.
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

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

List your exemptions for security issues.

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_list_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_list_option}

<dl>
<dt>`--scope SCOPE`</dt>
<dd>(Optional) List only the exemptions that apply to this scope. To set a namespace, repository, or tag as the scope, enter the value in one of the following formats: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
</dl>

### Example
{: #bx_cr_exemption_list_example}

List all your exemptions for security issues that apply to images in the *`birds/bluebird`* repository. The output includes exemptions that are account-wide, exemptions that are scoped to the *`birds`* namespace, and exemptions that are scoped to the *`birds/bluebird`* repository, but not any that are scoped to specific tags within the *`birds/bluebird`* repository.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Delete an exemption for a security issue. To view your existing exemptions, run `ibmcloud cr exemption-list`.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_rm_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_rm_option}

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

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Lists the types of security issues that you can exempt.

```
ibmcloud cr exemption-types
```
{: codeblock}

### Prerequisites
{: #bx_cr_exemption_types_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

If you are using IAM authentication, this command enables fine-grained authorization. For more information, see [Managing user access with Identity and Access Management](/docs/Registry?topic=registry-iam#iam) and [Defining user access role policies](/docs/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

### Prerequisites
{: #bx_cr_iam_policies_enable_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

Displays the IAM policy status of the targeted {{site.data.keyword.registryshort_notm}} account. For more information, see [Managing user access with Identity and Access Management](/docs/Registry?topic=registry-iam#iam) and [Defining user access role policies](/docs/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-digests` (`ibmcloud cr digests`)
{: #bx_cr_image_digests}

Lists all images, including untagged images, in your {{site.data.keyword.cloud_notm}} account. If you want to list tagged images only, run the [`ibmcloud cr image-list`](#bx_cr_image_list) command.

You can refer to an image by using a combination of the **Repository** column and the **Digest** column, for example, `repository@digest`. You can also refer to the image name by using a combination of the content of the **Repository** column and and one of the tags in the **Tags** column in the format: `repository:tag`.
{: tip}

```
ibmcloud cr image-digests [--format FORMAT | --quiet | -q | --json] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

### Prerequisites
{: bx_cr_image_digests_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_digests_option}

<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Each image is listed in the format: `repository@digest`</dd>
<dt>`--json`</dt>
<dd>(Optional) Outputs the list in JSON format.</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Optional) Limit the output to display only images in the specified namespace or repository. </dd>
<dt>`--include-ibm`</dt>
<dd>(Optional) Includes {{site.data.keyword.IBM_notm}}-provided public images in the output. By default only private images are listed. You can view {{site.data.keyword.IBM_notm}}-provided  images in the global registry only.</dd>

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

Displays details about a specific image.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_inspect_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_inspect_option}

<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`IMAGE`</dt>
<dd>The name of the image for which you want to get a report. You can inspect multiple images by listing each image in the command with a space between each name.

`IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the image that is tagged `latest` is inspected.</p>

</dd>
</dl>

### Example
{: #bx_cr_image_inspect_example}

Display details about the exposed ports for the image *`us.icr.io/birds/bluebird:1`*, by using the formatting directive *`"{{ .Config.ExposedPorts }}"`*.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Displays all images in your {{site.data.keyword.cloud_notm}} account.

The image name is the combination of the content of the **Repository** and **Tag** columns in the format: `repository:tag`
{:tip}

```
ibmcloud cr image-list [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm] [--no-trunc] [--show-type]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_list_option}

<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Each image is listed in the format: `repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Optional) Limit the output to display only images in the specified namespace or repository. </dd>
<dt>`--include-ibm`</dt>
<dd>(Optional) Includes {{site.data.keyword.IBM_notm}}-provided public images in the output. By default only private images are listed. You can view {{site.data.keyword.IBM_notm}}-provided images in the global registry only.</dd>
<dt>`--no-trunc`</dt>
<dd>(Optional) Do not truncate the image digests.</dd>
<dt>`--show-type`</dt>
<dd>(Optional) Displays the image manifest type.</dd>
</dl>

### Example
{: #bx_cr_image_list_example}

Display the images in the *`birds`* namespace in the format `repository:tag`, without truncating the image digests.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-restore`
{: #bx_cr_image_restore}

Restore a deleted image from the trash. To find out what is in the trash, run the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command.
{: shortdesc}

```
ibmcloud cr image-restore IMAGE
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_restore_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_restore_option}

<dl>
<dt>`IMAGE`</dt>
<dd>The name of the image that you want to restore from the trash.
<p>To find the names of your images in the trash, run [`ibmcloud cr trash-list`](#bx_cr_trash_list). `IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

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

For more information about how to use the `ibmcloud cr image-restore` command, see [Restoring images](/docs/Registry?topic=registry-registry_images_#registry_images_restore).

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Delete one or more specified images from {{site.data.keyword.registrylong_notm}}.

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

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_rm_option}

<dl>
<dt>`IMAGE`</dt>
<dd>The name of the image that you want to delete. You can delete multiple images at the same time by listing each image in the command with a space between each name. `IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

<p>Removed images are stored in the trash for 30 days.</p>

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the image that is tagged `latest` is deleted by default.</p>



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

Add a tag that you specify in the command to an existing image, copy the tag to another repository, or copy the tag to a repository in a different namespace. The target image, `TARGET_IMAGE`, is the new image and the source image, `SOURCE_IMAGE`, is the existing image in {{site.data.keyword.registrylong_notm}}. The source and target images must be in the same region.

To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.
{: tip}


```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

### Prerequisites
{: #bx_cr_image_tag_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_tag_option}

<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>The name of the source image. `SOURCE_IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>The name of the target image. `TARGET_IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

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

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_untag_option}

<dl>
<dt>`IMAGE`</dt>
<dd>The name of the image for which you want to remove the tag. You can delete the tag from multiple images at the same time by listing each image in the command with a space between each name. `IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the command fails.</p>

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

### Prerequisites
{: #bx_cr_login_prereq}

None

## `ibmcloud cr manifest-inspect`
{: #bx_cr_manifest_inspect}

View the contents of the manifest for an image.

```
ibmcloud cr manifest-inspect [--quiet | -q ] IMAGE
```
{: codeblock}

### Prerequisites
{: #bx_cr_manifest_inspect_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_manifest_inspect_option}

<dl>
<dt>`IMAGE`</dt>
<dd>The name of the image for which you want to inspect the manifest.`IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`.</p>


</dd>

<dt>`--quiet`, `-q`</dt>
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

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

### Prerequisites
{: #bx_cr_namespace_add_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_namespace_add_option}

<dl>
<dt>`NAMESPACE`</dt>
<dd>The namespace that you want to add. The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters, and contain lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.
  
<p>  
<strong>Important</strong> Do not put personal information in your namespace names.
</p>
  
</dd>
</dl>

### Example
{: #bx_cr_namespace_add_example}

Create a namespace with the name *`birds`*.

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Displays all namespaces that are owned by your {{site.data.keyword.cloud_notm}} account.

```
ibmcloud cr namespace-list
```
{: codeblock}

### Prerequisites
{: #bx_cr_namespace_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Removes a namespace from your {{site.data.keyword.cloud_notm}} account. Images in this namespace are deleted when the namespace is removed.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

### Prerequisites
{: #bx_cr_namespace_rm_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_namespace_rm_option}

<dl>
<dt>`NAMESPACE`</dt>
<dd>The namespace that you want to remove.</dd>
<dt>`--force`, `-f`</dt>
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

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Upgrades you to the standard plan for the registry region that you're targeting.

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

For more information about plans, see [Registry plans](/docs/Registry?topic=registry-registry_overview#registry_plans).

### Prerequisites
{: #bx_cr_plan_upgrade_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

### Command options
{: #bx_cr_plan_upgrade_option}

<dl>
<dt>`PLAN`</dt>
<dd>(Optional) The name of the pricing plan that you want to upgrade to. If `PLAN` is not specified, the default is `standard`.</dd>
</dl>

### Example
{: #bx_cr_plan_upgrade_example}

Upgrade to the standard pricing plan.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

Imports {{site.data.keyword.IBM_notm}} software that is downloaded from [IBM Passport Advantage Online for customers](https://www.ibm.com/software/passportadvantage/pao_customer.html){: external} and packaged for use with Helm into your {{site.data.keyword.registrylong_notm}} namespace.

Container images are pushed to your private {{site.data.keyword.registryshort_notm}} namespace. Helm charts are written to a `ppa-import` directory that is created in the directory from which you run the command. Optionally, you can use the [Chart Museum open source project](https://github.com/helm/charts/tree/master/stable/chartmuseum){: external} to host helm charts.

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

### Prerequisites
{: #bx_cr_ppa_archive_load_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_ppa_archive_load_option}

<dl>
  <dt>`--archive FILE`</dt>
  <dd>The path to the compressed file that is downloaded from IBM Passport Advantage.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>One of your namespaces. Container images from the compressed file are pushed to this namespace. To list namespaces, run `ibmcloud cr namespace-list`.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Optional) Your [Chart Museum](https://github.com/helm/charts/tree/master/stable/chartmuseum){: external} unique resource identifier.</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(Optional) Your [Chart Museum](https://github.com/helm/charts/tree/master/stable/chartmuseum){: external} user name.</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(Optional) Your [Chart Museum](https://github.com/helm/charts/tree/master/stable/chartmuseum){: external} password.</dd>
</dl>

### Example
{: #bx_cr_ppa_archive_load_example}

Import IBM software and package it for use with Helm in your {{site.data.keyword.registrylong_notm}} namespace *`birds`*, where the path to the compressed file is *`downloads/compressed_file.tgz`*.

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
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

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Modify the specified quota for the registry region that you're targeting.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

### Prerequisites
{: #bx_cr_quota_set_prereq}

To find out about the required permissions, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_configure).

### Command options
{: #bx_cr_quota_set_option}

<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(Optional) Changes your traffic quota to the specified value in megabytes. The operation fails if you are not authorized to set traffic, or if you set a value that exceeds your current pricing plan.</dd>
<dt>`--storage STORAGE`</dt>
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

For more information, see [Regions](/docs/Registry?topic=registry-registry_overview#registry_regions).

### Prerequisites
{: #bx_cr_region_prereq}

None

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Set a target region for the {{site.data.keyword.registrylong_notm}} commands. To list the available regions, run the command with no parameters.

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
<dt>`REGION`</dt>
<dd>(Optional) The name of your target region, for example, `us-south`.

For more information, see [Regions](/docs/Registry?topic=registry-registry_overview#registry_regions).

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

List the image retention policies for your account. Image retention policies retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.
{: shortdesc}

Where an image within a repository is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

```
ibmcloud cr retention-policy-list
```
{: codeblock}

### Prerequisites
{: #bx_cr_retention_policy_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Example
{: #bx_cr_retention_policy_list_example}

List the retention policies in your account.

```
ibmcloud cr retention-policy-list
```
{: pre}

For more information about how to use the `ibmcloud cr retention-policy-list` command, see [Retaining images](/docs/Registry?topic=registry-registry_retention).

## `ibmcloud cr retention-policy-set`
{: #bx_cr_retention_policy_set}

Set a policy to retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted. When you set a policy it runs interactively, subsequently it runs on a daily basis. You can set only one policy in each namespace.
{: shortdesc}

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If a retention policy deletes an image that you want to keep, you can restore the image. To identify the image, list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore the selected image by running the  [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

If you want to cancel a retention policy, see [Updating a retention policy so that it keeps all your images](/docs/Registry?topic=registry-registry_retention#retention_policy_keep).

```
ibmcloud cr retention-policy-set --images IMAGECOUNT NAMESPACE
```
{: codeblock}

### Prerequisites
{: #bx_cr_retention_policy_set_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_retention_policy_set_option}

<dl>
<dt>`NAMESPACE`</dt>
<dd>The namespace for which you want to create a policy.</dd>
<dt>`--images`</dt>
<dd>Determines how many images to keep within each repository in the specified namespace. The newest images are retained. The age of images is determined by their build date. `IMAGECOUNT` is the number of images that you want to retain in each repository for the namespace. To return a policy to the default state that keeps all the images, set `IMAGECOUNT` to `All`.</dd>
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
  
For more information about how to use the `ibmcloud cr retention-policy-set` command, see [Retaining images](/docs/Registry?topic=registry-registry_retention).

## `ibmcloud cr retention-run`
{: #bx_cr_retention_run}

Cleans up a namespace by retaining a specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.
{: shortdesc}

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore a selected image by running the  [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

```
ibmcloud cr retention-run [--force | -f [--json]] --images IMAGECOUNT NAMESPACE
```
{: codeblock}

### Prerequisites
{: #bx_cr_retention_run_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_retention_run_option}

<dl>
<dt>`NAMESPACE`</dt>
<dd>The namespace that you want to clean up.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Optional) Force the command to run with no user prompts.</dd>
<dt>`--json`</dt>
<dd>(Optional) Outputs JSON that contains the results of cleaning your namespace. This flag must be used with `--force`.</dd>
<dt>`--images`</dt>
<dd>Determines how many images to keep within each repository in the specified namespace. The newest images are retained. The age of images is determined by their build date. `IMAGECOUNT` is the number of images that you want to retain in each repository for the namespace.
</dd>
</dl>

### Example
{: #bx_cr_retention_run_example}

Retain the newest 20 images within each repository, in the namespace `birds`.

```
ibmcloud cr retention-run --images 20 birds
```
{: pre}

For more information about how to use the `ibmcloud cr retention-run` command, see [Retaining images](/docs/Registry?topic=registry-registry_retention).

## `ibmcloud cr token-get` - deprecated
{: #bx_cr_token_get}

Retrieve the specified token from the registry.

This command is deprecated.
{: deprecated}

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

### Prerequisites
{: #bx_cr_token_get_prereq}

To find out about the required permissions, see [Platform management roles](/docs/Registry?topic=registry-iam#platform_management_roles).

### Command options
{: #bx_cr_token_get_option}

<dl>
<dt>`TOKEN`</dt>
<dd>The unique identifier of the token that you want to retrieve. To list your tokens, run `ibmcloud cr token-list`.</dd>
</dl>

### Example
{: #bx_cr_token_get_example}

Retrieve the token *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`) - deprecated
{: #bx_cr_token_list}

Displays all tokens that exist for your {{site.data.keyword.cloud_notm}} account.

This command is deprecated.
{: deprecated}

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

### Prerequisites
{: #bx_cr_token_list_prereq}

To find out about the required permissions, see [Platform management roles](/docs/Registry?topic=registry-iam#platform_management_roles).

### Command options
{: #bx_cr_token_list_option}

<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Format the output elements by using a Go template.

For more information, see [Formatting and filtering the CLI output for {{site.data.keyword.registrylong_notm}} commands](/docs/Registry?topic=registry-registry_cli_list).

</dd>
</dl>

### Example
{: #bx_cr_token_list_example}

Display all tokens that are read-only, by using the formatting directive *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`*.

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

This example produces output in the following format:

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm` - deprecated
{: #bx_cr_token_rm}

Remove one or more specified registry tokens.

This command is deprecated.
{: deprecated}

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

### Prerequisites
{: #bx_cr_token_rm_prereq}

To find out about the required permissions, see [Platform management roles](/docs/Registry?topic=registry-iam#platform_management_roles).

### Command options
{: #bx_cr_token_rm_option}

<dl>
<dt>`TOKEN`</dt>
<dd>TOKEN can be either the token itself, or the unique identifier of the token, as shown in `ibmcloud cr token-list`. Multiple tokens can be specified and they must be separated by a space.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Optional) Force the command to run with no user prompts.</dd>
</dl>

### Example
{: #bx_cr_token_rm_example}

Remove the token *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr trash-list`
{: #bx_cr_trash_list}

Displays all images in the trash in your {{site.data.keyword.cloud_notm}} account. You can also see the number of days left until the image is removed from the trash. The number of days left until removal is rounded up, therefore if the time left until removal is 2 hours, it will show as 1 day. Images remain in the trash for 30 days after they've been deleted from your live repository.

If you want to restore an image from the trash, run the [`ibmcloud cr image-restore`](#bx_cr_image_restore) command, see [Restoring images](/docs/Registry?topic=registry-registry_images_#registry_images_restore).

```
ibmcloud cr trash-list [--restrict NAMESPACE] [--json]
```
{: codeblock}

### Prerequisites
{: #bx_cr_trash_list_prereq}

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_trash_list_option}

<dl>
<dt>`--restrict NAMESPACE`</dt>
<dd>(Optional) Limit the output to display only images in the specified namespace. </dd>
<dt>`--json`</dt>
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

To find out about the required permissions, see [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#access_roles_using).

### Command options
{: #bx_cr_va_option}

<dl>
<dt>`IMAGE`</dt>
<dd>The name of the image for which you want to get a report. The report states whether the image has any known package vulnerabilities. You can request reports for multiple images at the same time by listing each image in the command with a space between each name.

<p>To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** and **Tag** columns to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the report assesses the image that is tagged `latest`.</p>

<p>The following operating systems are supported:

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

For more information, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index).

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Optional) The command output shows additional information about fixes for vulnerable packages.</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Optional) The command output is restricted to show vulnerabilities only.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Optional) The command output is restricted to show configuration issues only.</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(Optional) The command output is returned in the chosen format. The default format is `text`. The following formats are supported:

<ul>
<li>`text`</li>
<li>`json`</li>
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
