---

copyright:
  years: 2017, 2025
lastupdated: "2025-08-12"

keywords: IBM Cloud Container Registry, container registry, ibmcloud cr, container-registry, managing container registry cli, ibm cloud container registry cli, ibm cloud registry, container-registry cli, managing registry, managing registry resources, container-registry cli plugin, registry cli, registry commands, container registry commands, ibm cloud container registry terminal, ibm cloud container registry command line, icr.io commands

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.registryshort_notm}} CLI (`ibmcloud cr`)
{: #containerregcli}

You can use the {{site.data.keyword.registrylong}} command-line interface (CLI), which is provided in the `container-registry` CLI plug-in, to manage your [registry](#x2064940){: term} and its resources for your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

## Prerequisites
{: #containerregcli_prereq}

Before you can use the {{site.data.keyword.registryshort}} CLI, you must complete the following prerequisites.

1. Install the `ibmcloud` CLI plug-in, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
2. Install the `container-registry` CLI plug-in, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).
3. Log in to {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command to generate an [access token](#x2113001){: term} and authenticate your session so that you can run commands in the CLI.

### Notes
{: #containerregcli_prereq_notes}

To find out more about how to use the {{site.data.keyword.registryshort}} CLI, the `ibmcloud cr` commands, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

You're notified on the command line when updates to the `ibmcloud` CLI and `container-registry` CLI plug-ins are available. Ensure that you keep your CLIs up to date so that you can use all the available commands and options. If you want to view the current version of your `container-registry` CLI plug-in, run the `ibmcloud plugin list` command.

For more information about the IAM platform and service access roles that are required for some {{site.data.keyword.registryshort}} commands, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam).

Do not put personal information in your container images, namespace names, description fields, or in any image configuration data (for example, image names or image labels).
{: important}

If {{site.data.keyword.registryshort_notm}} `ibmcloud cr`, commands fail with an error that says that they're not registered commands, see [Why do {{site.data.keyword.registryshort}} commands fail with a message that states that they’re not registered?](/docs/Registry?topic=Registry-troubleshoot-login-error) for assistance. If the commands fail with a message that you're not logged in, see [Why can't I log in to Container Registry?](/docs/Registry?topic=Registry-troubleshoot-login) for assistance.
{: tip}

## `ibmcloud cr api`
{: #bx_cr_api}

This command returns the details about the registry API endpoint that the commands are run against.

```sh
ibmcloud cr api
```

### Example
{: #bx_cr_api_example}

Find out the details for the registry API endpoint.

```sh
ibmcloud cr api
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Create an exemption for a security issue. You can create an exemption for a security issue that applies to different scopes. The scope can be the account, [namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace), [repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository), [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest), or [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag).

You can identify the images in the scope by using either the tag or the digest. You can reference the image by digest `<dns>/<namespace>/<repo>@<digest>`, which affects the digest and all its tags in the same repository, or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag. To list all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command.
{: tip}

```sh
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID [--output json | -o json]
```

### Prerequisites
{: #bx_cr_exemption_add_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_add_option}

`--scope SCOPE`
:   To set your account as the scope, use `"*"` as the value.

    To set a namespace, repository, digest, or tag as the scope, enter the value in one of the following formats:

    - `namespace`
    - `namespace/repository`
    - `namespace/repository:tag`
    - `namespace/repository@digest`

`--issue-type ISSUE_TYPE`
:   The type of security issue that you want to exempt. To find valid issue types, run `ibmcloud cr exemption-types`.

`--issue-id ISSUE_ID`
:   The ID of the security issue that you want to exempt. To find an issue ID, run `ibmcloud cr va <image>`, where `<image>` is the name of your image, and use the relevant value from the **Vulnerability ID** column.

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Examples
{: #bx_cr_exemption_add_example}

Create a CVE exemption for the CVE with ID `CVE-2018-17929` for all images in the `us.icr.io/birds/bluebird` repository by entering `us.icr.io/birds/bluebird` for the scope, `cve` for the issue type, and `CVE-2018-17929` for the issue ID.

```sh
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Create an account-wide CVE exemption for the CVE with ID `CVE-2018-17929` by entering `"*"` for the scope, `cve` for the issue type, and `CVE-2018-17929` for the issue ID.

```sh
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

List your exemptions for security issues.

You can identify the images in the scope by using either the [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) or the [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest). You can reference the image by digest `<dns>/<namespace>/<repo>@<digest>`, which affects the digest and all its tags in the same repository, or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag. To list all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command.
{: tip}

```sh
ibmcloud cr exemption-list [--scope SCOPE] [--output json | -o json]
```

### Prerequisites
{: #bx_cr_exemption_list_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_list_option}

`--scope SCOPE`
:   (Optional) List only the exemptions that apply to this scope.

    To set a namespace, repository, digest, or tag as the scope, enter the value in one of the following formats:

    - `namespace`
    - `namespace/repository`
    - `namespace/repository:tag`
    - `namespace/repository@digest`

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Examples
{: #bx_cr_exemption_list_example}

List all your exemptions for security issues that apply to images in the `birds/bluebird` repository by entering `birds/bluebird` as the scope.

The output includes exemptions that are account-wide, exemptions that are scoped to the `birds` namespace, and exemptions that are scoped to the `birds/bluebird` repository. The output doesn't include any exemptions that are scoped to specific tags within the `birds/bluebird` repository.

```sh
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

List all your exemptions for security issues that apply to images in the `birds/bluebird@sha256:101010101010` digest by entering `birds/bluebird@sha256:101010101010` as the scope.

The output includes exemptions that are account-wide, exemptions that are scoped to the `birds` namespace, and exemptions that are scoped to the `birds/bluebird` repository and to the `birds/bluebird@sha256:101010101010` digest. The output doesn't include any exemptions that are scoped to specific tags within the `birds/bluebird` repository.

```sh
ibmcloud cr exemption-list --scope birds/bluebird@sha256:101010101010
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Delete an exemption for a security issue. To view your existing exemptions, run `ibmcloud cr exemption-list`.

You can identify the images in the scope by using either the [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) or the [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest). You can reference the image by digest `<dns>/<namespace>/<repo>@<digest>`, which affects the digest and all its tags in the same repository, or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag. To list all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command.
{: tip}

```sh
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```

### Prerequisites
{: #bx_cr_exemption_rm_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_rm_option}

`--scope SCOPE`
:   To set your account as the scope, use `"*"` as the value.

    To set a namespace, repository, digest, or tag as the scope, enter the value in one of the following formats:

    - `namespace`
    - `namespace/repository`
    - `namespace/repository:tag`
    - `namespace/repository@digest`

`--issue-type ISSUE_TYPE`
:   The type of issue for the exemption for the security issue that you want to remove. To find the types of issue for your exemptions, run `ibmcloud cr exemption-list`.

`--issue-id ISSUE_ID`
:   The ID of the exemption for the security issue that you want to remove. To find the issue IDs for your exemptions, run `ibmcloud cr exemption-list`.

### Examples
{: #bx_cr_exemption_rm_example}

Delete a CVE exemption for the CVE with ID `CVE-2018-17929` for all images in the `us.icr.io/birds/bluebird` repository by entering `us.icr.io/birds/bluebird` as the scope, `cve` as the issue type, and `CVE-2018-17929` as the issue ID.

```sh
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Delete an account-wide CVE exemption for the CVE with ID `CVE-2018-17929` by entering `"*"` as the scope, `cve` as the issue type, and `CVE-2018-17929` as the issue ID.

```sh
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Lists the types of security issues that you can exempt.

```sh
ibmcloud cr exemption-types [--output json | -o json]
```

### Prerequisites
{: #bx_cr_exemption_types_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_exemption_types_option}

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Example
{: #bx_cr_exemption_types_example}

List the types of security issues in JSON format by entering `json` as the output.

```sh
ibmcloud cr exemption-types -o json
```
{: pre}

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

All accounts require {{site.data.keyword.iamshort}} (IAM) access policies.
{: important}

If you're using IAM authentication, this command enables fine-grained authorization. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam) and [Defining IAM access policies](/docs/Registry?topic=Registry-user#user).

```sh
ibmcloud cr iam-policies-enable
```

### Prerequisites
{: #bx_cr_iam_policies_enable_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Example
{: #bx_cr_iam_policies_enable_example}

Use IAM policies to enable fine-grained authorization.

```sh
ibmcloud cr iam-policies-enable
```
{: pre}

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

This command displays the IAM access policy status of the targeted {{site.data.keyword.registrylong_notm}} account. For more information, see [Managing IAM access for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-iam) and [Defining IAM access policies](/docs/Registry?topic=Registry-user#user).

All accounts require {{site.data.keyword.iamlong}} (IAM) access policies.
{: important}

```sh
ibmcloud cr iam-policies-status
```

### Example
{: #bx_cr_iam_policies_status_example}

Show the status of the IAM access policy for your account.

```sh
ibmcloud cr iam-policies-status
```
{: pre}

## `ibmcloud cr image-digests` (`ibmcloud cr digests`)
{: #bx_cr_image_digests}

Lists all images, including [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images, in your {{site.data.keyword.cloud_notm}} account. This command returns the [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) in its long format. When you're using the digest to identify an image, always use the long format.

If you want to list tagged images only, run the [`ibmcloud cr image-list`](#bx_cr_image_list) command.

You can refer to an image by using a combination of the **Repository** column (`repository`) and the **Digest** column (`digest`) separated by an at (`@`) symbol to create the image name in the format `repository@digest`. You can also refer to the image name by using a combination of the content of the **Repository** column (`repository`) and one of the tags in the **Tags** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`.
{: tip}

```sh
ibmcloud cr image-digests [--format FORMAT | --quiet | -q | --output json | -o json] [--restrict RESTRICTION] [--include-ibm] [--no-va] [--va]
```

### Prerequisites
{: #bx_cr_image_digests_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_digests_option}

`--format FORMAT`
:   (Optional) Format the output elements by using a Go template. For more information, see [Formatting and filtering the {{site.data.keyword.registryshort}} CLI output](/docs/Registry?topic=Registry-registry_cli_list).

`--quiet`, `-q`
:   (Optional) Each image is listed in the format: `repository@digest`

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

`--restrict RESTRICTION`
:   (Optional) Limit the output to display only images in the specified namespace or repository.

`--include-ibm`
:   (Optional) Includes {{site.data.keyword.IBM_notm}}-provided public images in the output. By default only private images are listed. You can view {{site.data.keyword.IBM_notm}}-provided images in the global registry only.

`--no-va`
:   (Optional) Excludes the Vulnerability Advisor security status results from the output. If you don't need the security status results as part of your `ibmcloud cr image-digests` output, you can use this option to increase performance.

`--va`
:   (Optional) Includes the Vulnerability Advisor security status results in the output. Use this option to ensure that you are ready for [{{site.data.keyword.registrylong_notm}} CLI plug-in version 1.0.0](/docs/Registry?topic=Registry-registry_notices_lists). You can use the `--va` option with the `--restrict` option to receive just the information that you require.

### Example
{: #bx_cr_image_digests_example}

Display all the images in the `birds` namespace, including untagged images, in the format `repository@digest` by using `--quiet` to list the images in the format `repository@digest` and by entering `birds` as the restriction.

```sh
ibmcloud cr image-digests --restrict birds --quiet
```
{: pre}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Displays details about a specific image. You can reference the image that you want to inspect either by [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) `repository@digest`, or by [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) `repository:tag`.

```sh
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```

### Prerequisites
{: #bx_cr_image_inspect_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_image_inspect_argument}

`IMAGE`
:   The name of the image for which you want to get a report. You can inspect multiple images by listing each image in the command with a space between each name.

    You can identify images by using either the digest `<dns>/<namespace>/<repo>@<digest>` or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag.

    To find the names of your images, run one of the following commands:

    - To identify your image by digest, run the `ibmcloud cr image-digests` command. Combine the content of the **Repository** column (`repository`) and the **Digest** column (`digest`) separated by an at (`@`) symbol to create the image name in the format `repository@digest`.
    - To identify your image by tag, run the `ibmcloud cr image-list` command. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the image that is tagged `latest` is deleted by default.

### Command options
{: #bx_cr_image_inspect_option}

`--format FORMAT`
:   (Optional) Format the output elements by using a Go template. For more information, see [Formatting and filtering the {{site.data.keyword.registryshort}} CLI output](/docs/Registry?topic=Registry-registry_cli_list).

### Example
{: #bx_cr_image_inspect_example}

Display details about the exposed ports for the `us.icr.io/birds/bluebird:1` image by using the formatting directive `"{{ .Config.ExposedPorts }}"` and by entering `us.icr.io/birds/bluebird:1` as the image.

```sh
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Displays all tagged images in your {{site.data.keyword.cloud_notm}} account. If you want to list all your images, including untagged images, run the [`ibmcloud cr image-digests`](#bx_cr_image_digests) command. By default, the `ibmcloud cr image-list` command returns the [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) for the images in a truncated format. The `ibmcloud cr image-digests` command returns the long format of the digest.

When you're using the digest to identify an image, always use the long format.
{: requirement}

The image name is the combination of the content of the **Repository** and **Tag** columns in the format: `repository:tag`
{: tip}

If the command to list images times out, see [Why is it timing out when I list images?](/docs/Registry?topic=Registry-troubleshoot-image-timeout) for assistance.
{: tip}

```sh
ibmcloud cr image-list [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm] [--no-trunc] [--show-type] [--no-va] [--va] [--output json | -o json]
```

### Prerequisites
{: #bx_cr_image_list_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_image_list_option}

`--format FORMAT`
:   (Optional) Format the output elements by using a Go template. For more information, see [Formatting and filtering the {{site.data.keyword.registryshort}} CLI output](/docs/Registry?topic=Registry-registry_cli_list).

`--quiet`, `-q`
:   (Optional) Each image is listed in the format: `repository:tag`

`--restrict RESTRICTION`
:   (Optional) Limit the output to display only images in the specified namespace or repository.

`--include-ibm`
:   (Optional) Includes {{site.data.keyword.IBM_notm}}-provided public images in the output. By default only private images are listed. You can view {{site.data.keyword.IBM_notm}}-provided images in the global registry only.

`--no-trunc`
:   (Optional) Returns the image digest in its long format.

`--show-type`
:   (Optional) Displays the image manifest type.

`--no-va`
:   (Optional) Excludes the Vulnerability Advisor security status results from the output. If you don't need the security status results as part of your `ibmcloud cr image-list` output, you can use this option to increase performance.

`--va`
:   (Optional) Includes the Vulnerability Advisor security status results in the output. Use this option to ensure that you are ready for [{{site.data.keyword.registrylong_notm}} CLI plug-in version 1.0.0](/docs/Registry?topic=Registry-registry_notices_lists). You can use the `--va` option with the `--restrict` option to receive just the information that you require.

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Example
{: #bx_cr_image_list_example}

Display the images in the `birds` namespace in the format `repository:tag`, without truncating the image digests by using `--quiet` to display the image in the format `repository:tag`, `--no-trunc` to display the image digest in the long format, and by entering `birds` as the restriction.

```sh
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-prune-untagged`
{: #ic_cr_image_prune_untagged}

Delete all [untagged](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged) images in your {{site.data.keyword.registrylong_notm}} account.

```sh
ibmcloud cr image-prune-untagged [--force | -f [--output json | -o json]] --restrict RESTRICTION
```

### Prerequisites
{: #ic_cr_image_prune_untagged_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #ic_cr_image_prune_untagged_option}

`--force`, `-f`
:   (Optional) Force the command to run with no user prompts.

`--output json`, `-o json`
:   (Optional) Outputs JSON that contains the results of cleaning up your untagged images. This option must be used with `--force`.

`--restrict`
:   (Optional) Limit the clean up to only untagged images in the specified namespace or repository.

### Example
{: #ic_cr_image_prune_untagged_example}

Delete all untagged images that are in the `birds` namespace without any user prompts and output the results in JSON format by using the `--force` option to force the command to run with no user prompts, and by entering `--json` as the output and `birds` as the restriction.

```sh
ibmcloud cr image-prune-untagged [--force | -f [--json]] --restrict birds
```
{: pre}

## `ibmcloud cr image-restore`
{: #bx_cr_image_restore}

Restore a deleted image from the trash. You can choose to restore by [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) or by [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest). If you restore by digest, the digest and all its tags in the same repository are restored. To find out what is in the trash, run the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command.

If you get an error when you're restoring an image that says that the tagged image exists, see [Why do I get an error when I'm restoring an image?](/docs/Registry?topic=Registry-troubleshoot-image-restore) for assistance.
{: tip}

If you're restoring an image by digest, but some tags aren't restored, see [Why aren't all the tags restored when I restore by digest?](/docs/Registry?topic=Registry-troubleshoot-image-restore-digest) for assistance.
{: tip}

```sh
ibmcloud cr image-restore IMAGE
```

### Prerequisites
{: #bx_cr_image_restore_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_image_restore_argument}

`IMAGE`
:   The name of the image that you want to restore from the trash.

    To find the names of your images in the trash, run the `ibmcloud cr trash-list` command.

    You can identify images by using either the tag or the digest. The image to restore can be referenced by digest `<dns>/<namespace>/<repo>@<digest>`, which restores the digest and all its tags in the same repository, or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag.

    Images are stored in the trash for 30 days.

### Example
{: #bx_cr_image_restore_example}

Restore the `us.icr.io/birds/bluebird:1` image by entering `us.icr.io/birds/bluebird:1` as the image.

```sh
ibmcloud cr image-restore us.icr.io/birds/bluebird:1
```
{: pre}

For more information about how to use the `ibmcloud cr image-restore` command, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Delete one or more specified images from {{site.data.keyword.registryshort}}. You can reference the image that you want to delete either by [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) `repository@digest`, or by [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) `repository:tag`.

Where multiple tags exist for the same image digest within a repository, the `ibmcloud cr image-rm` command removes the underlying image and all its tags. If the same image exists in a different repository or namespace, then that copy of the image is not removed. If you want to remove a tag from an image and leave the underlying image and any other tags in place, use the [`ibmcloud cr image-untag`](#bx_cr_image_untag) command.
{: tip}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore a selected image by running the [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

```sh
ibmcloud cr image-rm IMAGE [IMAGE...]
```

### Prerequisites
{: #bx_cr_image_rm_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_image_rm_argument}

`IMAGE`
:   The name of the image that you want to delete. You can delete multiple images at the same time by listing each image in the command with a space between each name. You can identify images by using either the digest `<dns>/<namespace>/<repo>@<digest>` or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag.

    Images are stored in the trash for 30 days.

    To find the names of your images, run one of the following commands:

    - To identify your image by digest, run the `ibmcloud cr image-digests` command. Combine the content of the **Repository** column (`repository`) and the **Digest** column (`digest`) separated by an at (`@`) symbol to create the image name in the format `repository@digest`.
    - To identify your image by tag, run the `ibmcloud cr image-list` command. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the image that is tagged `latest` is deleted by default.

### Example
{: #bx_cr_image_rm_example}

Delete the `us.icr.io/birds/bluebird:1` image by entering `us.icr.io/birds/bluebird:1` as the image.

```sh
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

Add a [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) that you specify in the command to an existing image, copy the tag to another repository, or copy the tag to a repository in a different namespace. When you copy a tag, any {{site.data.keyword.redhat_full}} signatures for its [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) are also copied. The target image `TARGET_IMAGE` is the new image and the source image `SOURCE_IMAGE` is the existing image in {{site.data.keyword.registrylong_notm}}. The source and target images must be in the same region. You can reference the source image that you want to tag by either digest `repository@digest`, or by tag `repository:tag`. You must reference the target image by tag.

You can identify source images by using either the digest `<dns>/<namespace>/<repo>@<digest>` or by tag `<dns>/<namespace>/<repo>:<tag>`. You must reference the target image by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag.

To find the names of your images, use one of the following alternatives:

- To identify your image by digest, run the `ibmcloud cr image-digests` command. Combine the content of the **Repository** column (`repository`) and the **Digest** column (`digest`) separated by an at (`@`) symbol to create the image name in the format `repository@digest`.
- To identify your image by tag, run the `ibmcloud cr image-list` command. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`.

If you get a manifest error when you try to tag your image, the following topics might be of assistance:
- [Why do I get a manifest type error when I tag my image?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-type)
- [Why do I get a manifest version error?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-version)
- [Why do I get a manifest list invalid error?](/docs/Registry?topic=Registry-troubleshoot-manifest-list-error)


```sh
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```

### Prerequisites
{: #bx_cr_image_tag_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_image_tag_argument}

`SOURCE_IMAGE`
:   The name of the source image. You can identify source images by using either the digest `<dns>/<namespace>/<repo>@<digest>` or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag.

`TARGET_IMAGE`
:   The name of the target image. `TARGET_IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

### Examples
{: #bx_cr_image_tag_example}

Add another tag reference `latest`, to the image `us.icr.io/birds/bluebird:1` by entering `us.icr.io/birds/bluebird:1` as the source image and `us.icr.io/birds/bluebird:latest` as the target image.

```sh
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

Copy the image `us.icr.io/birds/bluebird:peck` to another repository in the same namespace `birds/pigeon` by entering `us.icr.io/birds/bluebird:peck` as the source image and `us.icr.io/birds/pigeon:peck` as the target image.

```sh
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

Copy the `us.icr.io/birds/bluebird:peck` image to another namespace that you have access to, in this example the `animals` namespace, by entering `us.icr.io/birds/bluebird:peck` as the source image and `us.icr.io/animals/dog:bark` as the target image.

```sh
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr image-untag`
{: #bx_cr_image_untag}

Remove a [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag), or tags, from each specified image in {{site.data.keyword.registrylong_notm}}.

To remove a specific tag from an image and leave the underlying image and any other tags in place, use the `ibmcloud cr image-untag` command. If you want to delete the underlying image, and all its tags, use the [`ibmcloud cr image-rm`](#bx_cr_image_rm) command instead.
{: tip}

```sh
ibmcloud cr image-untag IMAGE [IMAGE...]
```

### Prerequisites
{: #bx_cr_image_untag_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_image_untag_argument}

`IMAGE`
:   The name of the image for which you want to remove the tag. You can delete the tag from multiple images at the same time by listing each image in the command with a space between each name. `IMAGE` must be in the format `repository:tag`, for example, `us.icr.io/namespace/image:latest`.

    To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the command fails.

### Example
{: #bx_cr_image_untag_example}

Remove the tag `1` from the `us.icr.io/birds/bluebird:1` image by entering `us.icr.io/birds/bluebird:1` as the image.

```sh
ibmcloud cr image-untag us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

Displays the name and the account of the registry that you are logged in to.

```sh
ibmcloud cr info
```

### Example
{: #bx_cr_info_example}

Find the name and account of the registry.

```sh
ibmcloud cr info
```
{: pre}

## `ibmcloud cr login`
{: #bx_cr_login}

Log the local Docker or Podman client in to {{site.data.keyword.registrylong_notm}}.

This command is required if you want to run the `push` or `pull` commands for the registry. If you want to run other `ibmcloud cr` commands, you're not required to log in to {{site.data.keyword.registryshort}}.

```sh
ibmcloud cr login [--client CLIENT]
```

{{site.data.keyword.registryshort}} supports other clients as well as Docker and Podman. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).

If you have a problem when you try to log in, see [Why can't I log in to {{site.data.keyword.registryshort_notm}}?](/docs/Registry?topic=Registry-troubleshoot-login) for assistance. [macOS]{: tag-macos} If you're using a Mac and you have a problem when you try to log in, see [Why is Docker login on my Mac failing?](/docs/Registry?topic=Registry-troubleshoot-docker-mac) for assistance.
{: tip}

Logging in to {{site.data.keyword.registryshort}} by using the `ibmcloud cr login` command is subject to IAM login session limits. If your login expires, see [Why does the {{site.data.keyword.registryshort}} login keep expiring?](/docs/Registry?topic=Registry-troubleshoot-login-expire) for assistance.
{: tip}

### Command options
{: #bx_cr_login_option}

`-- client`
:   (Optional) Select the client that you want to log in. Valid values are `docker` and `podman`. If this option is not used and Docker is installed, the default is `docker`; if Docker is not installed, the default is `podman`.

### Example
{: #bx_cr_login__example}

To log in to the registry by using Podman, enter `podman` as the client.

```sh
ibmcloud cr login --client podman
```
{: pre}

## `ibmcloud cr manifest-inspect`
{: #bx_cr_manifest_inspect}

View the contents of the [manifest](/docs/Registry?topic=Registry-registry_overview#overview_elements_manifest) for an image. You can reference the image that you want to inspect either by [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) `repository@digest`, or by [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag) `repository:tag`.

```sh
ibmcloud cr manifest-inspect [--quiet | -q ] IMAGE
```

### Prerequisites
{: #bx_cr_manifest_inspect_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_manifest_inspect_argument}

`IMAGE`
:   The name of the image for which you want to inspect the manifest. You can identify images by using either the digest `<dns>/<namespace>/<repo>@<digest>` or by tag `<dns>/<namespace>/<repo>:<tag>`. Where `<dns>` is the domain name, `<namespace>` is the namespace, `<repo>` is the repository, `<digest>` is the digest, and `<tag>` is the tag.

    To find the names of your images, run one of the following commands:

    - To identify your image by digest, run the `ibmcloud cr image-digests` command. Combine the content of the **Repository** column (`repository`) and the **Digest** column (`digest`) separated by an at (`@`) symbol to create the image name in the format `repository@digest`.
    - To identify your image by tag, run the `ibmcloud cr image-list` command. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`.

### Command options
{: #bx_cr_manifest_inspect_option}

`--quiet`, `-q`
:   (Optional) Reduces the output to display essential elements only.

### Example
{: #bx_cr_manifest_inspect_example}

View the contents of the manifest for the `us.icr.io/birds/bluebird:1` image by entering `us.icr.io/birds/bluebird:1` as the image.

```sh
ibmcloud cr manifest-inspect us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Choose a name for your [namespace](#x2031005){: term} and add it to your {{site.data.keyword.cloud_notm}} account.

You can create a namespace in a [resource group](#x2161955){: term} of your choice by using one of the following options.

- Before you create the namespace, run the [`ibmcloud target -g RESOURCE_GROUP`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target) command, where `RESOURCE_GROUP` is the resource group.
- Specify the required resource group by using the `-g` option on the `ibmcloud cr namespace-add` command.

If you create a namespace in a resource group, you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. However, you can still set permissions for the namespace at the account level or in the namespace itself. If you don't specify a resource group, and a resource group isn't targeted, the default resource group is used.

If you have an older namespace that is not in a resource group, you can assign it to a resource group, see [`ibmcloud cr namespace-assign`](#ic_cr_namespace_assign).

Namespaces that are assigned to a resource group show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.
{: tip}

```sh
ibmcloud cr namespace-add [-g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID)] NAMESPACE
```

For more information about resource groups, see [Creating a resource group](/docs/account?topic=account-rgs&interface=ui#create_rgs).

If you have a problem when you try to add a namespace, see [Why can't I add a namespace?](/docs/Registry?topic=Registry-troubleshoot-add-namespace) for assistance.
{: tip}

### Prerequisites
{: #bx_cr_namespace_add_prereq}

To find out more about the required permissions, see [Platform management roles](/docs/Registry?topic=Registry-iam#platform_management_roles) and [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command arguments
{: #bx_cr_namespace_add_argument}

`NAMESPACE`
:   The namespace that you want to add. The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters, and contain lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.

    Do not put personal information in your namespace names.
    {: important}

### Command options
{: #bx_cr_namespace_add_option}

`-g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID)`
:   (Optional) Specify the name or ID of the resource group to which you want to add the namespace. If you don't set this option, the targeted resource group is used. If you don't set this option and a resource group is not targeted, the default resource group for the account is used.

### Example
{: #bx_cr_namespace_add_example}

Create a namespace with the name `birds` and add it to the resource group `beaks` by entering `beaks` as the resource group name and `birds` as the namespace.

```sh
ibmcloud cr namespace-add -g beaks birds
```
{: pre}

## `ibmcloud cr namespace-assign`
{: #ic_cr_namespace_assign}

Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the {{site.data.keyword.cloud_notm}} console before 29 July 2020 are not assigned to resource groups. You can assign an unassigned namespace to a resource group for your {{site.data.keyword.cloud_notm}} account. If you assign a namespace to a resource group, you can configure access to resources within the namespace at the [resource group](/docs/account?topic=account-rgs) level. If you don't specify a resource group, and a resource group isn't targeted, the command fails.

You can assign a namespace to a resource group only once. When a namespace is in a resource group, you can't move it to another resource group.
{: note}

To find out which namespaces are assigned to resource groups and which are unassigned, run the [`ibmcloud cr namespace-list`](#bx_cr_namespace_list) command with the `-v` option. Namespaces that are assigned to a resource group also show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.
{: tip}

```sh
ibmcloud cr namespace-assign -g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID) NAMESPACE
```

For more information about resource groups, see [Creating a resource group](/docs/account?topic=account-rgs&interface=ui#create_rgs).

### Prerequisites
{: #ic_cr_namespace_assign_prereq}

To find out more about the required permissions, see [Platform management roles](/docs/Registry?topic=Registry-iam#platform_management_roles) and [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command arguments
{: #ic_cr_namespace_assign_argument}

`NAMESPACE`
:   The namespace that you want to assign to a resource group.

### Command options
{: #ic_cr_namespace_assign_option}

`-g (RESOURCE_GROUP_NAME | RESOURCE_GROUP_ID)`
:   (Optional) Specify the name or ID of the resource group to which you want to assign the namespace. If you don't set this option, the targeted resource group is used.

### Example
{: #ic_cr_namespace_assign_example}

Assign a namespace with the name `birds` to the resource group `beaks` by entering `beaks` as the resource group name and `birds` as the namespace.

```sh
ibmcloud cr namespace-assign -g beaks birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Displays all namespaces that are owned by your {{site.data.keyword.cloud_notm}} account. You can use this command to list your namespaces so that you can verify which namespaces are assigned to resource groups, and which namespaces are unassigned. Namespaces that are assigned to a resource group also show in the **Resource list** page of the {{site.data.keyword.cloud_notm}} console.

```sh
ibmcloud cr namespace-list [--verbose | -v] [--output json | -o json]
```

### Prerequisites
{: #bx_cr_namespace_list_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_namespace_list_option}

`--verbose`, `-v`
:   (Optional) List all the namespaces and include information about the resource group and the creation date of the namespace.

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Example
{: #bx_cr_namespace_list_example}

View a list of all your namespaces, including information about resource groups and creation dates, by using the `--verbose` option.

```sh
ibmcloud cr namespace-list -v
```
{: pre}

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Removes a namespace from your {{site.data.keyword.cloud_notm}} account. Images in this namespace are deleted when the namespace is removed.

```sh
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```

### Prerequisites
{: #bx_cr_namespace_rm_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command arguments
{: #bx_cr_namespace_rm_argument}

`NAMESPACE`
:   The namespace that you want to remove.

### Command options
{: #bx_cr_namespace_rm_option}

`--force`, `-f`
:   (Optional) Force the command to run with no user prompts.

### Example
{: #bx_cr_namespace_rm_example}

Remove the `birds` namespace by entering `birds` as the namespace.

```sh
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

Displays your pricing plan for the registry region that you're targeting.

```sh
ibmcloud cr plan [--output json | -o json]
```

### Prerequisites
{: #bx_cr_plan_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_plan_option}

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Example
{: #bx_cr_plan_example}

Output your pricing plan in JSON format by entering `json` as the output.

```sh
ibmcloud cr plan -o json
```
{: pre}

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Upgrades you to the standard plan for the registry region that you're targeting.

```sh
ibmcloud cr plan-upgrade [PLAN]
```

For more information about plans, see [Registry plans](/docs/Registry?topic=Registry-registry_overview#registry_plans).

### Prerequisites
{: #bx_cr_plan_upgrade_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command arguments
{: #bx_cr_plan_upgrade_argument}

`PLAN`
:   (Optional) The name of the pricing plan that you want to upgrade to. If `PLAN` is not specified, the default is `standard`.

### Example
{: #bx_cr_plan_upgrade_example}

Upgrade to the standard pricing plan by entering `standard` as the plan.

```sh
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr platform-metrics`
{: #ic_cr_platform_metrics}

You can use the command to enable and disable platform metrics. You can also use it to find out whether you have platform metrics set up on your account for the registry region that you're targeting.

If you want to view the platform metrics for {{site.data.keyword.registrylong_notm}}, you must opt in by running the `ibmcloud cr platform-metrics` command.
{: requirement}

You must specify one of the command options or the command fails with an error.
{: requirement}

```sh
ibmcloud cr platform-metrics --enable | --disable | --status
```

For more information about the platform metrics that you can view in {{site.data.keyword.registryshort}}, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor).

### Prerequisites
{: #ic_cr_platform_metrics_prereq}

- You must set up {{site.data.keyword.mon_full_notm}}, see [Getting started tutorial for {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).
- [Enable your {{site.data.keyword.mon_full_notm}} instance for platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).
- To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #ic_cr_platform_metrics_option}

`--enable`
:   (Optional) Enable the setting for your account.

`--disable`
:   (Optional) Disable the setting for your account.

`--status`
:   (Optional) Display whether the setting is enabled for your account.

### Example
{: #ic_cr_platform_metrics_example}

Enable platform metrics for your account by using the `--enable` option.

```sh
ibmcloud cr platform-metrics --enable
```
{: pre}

## `ibmcloud cr private-only`
{: #ic_cr_private_only}

Prevent image pulls or pushes over public network connections for your account for the registry region that you're targeting. You must specify one of the command options or the command fails with an error.

```sh
ibmcloud cr private-only --enable | --disable | --status
```

### Prerequisites
{: #ic_cr_private_only_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #ic_cr_private_only_option}

`--enable`
:   (Optional) Prevent image pulls or pushes over public network connections for your account.

`--disable`
:   (Optional) Reinstate image pulls or pushes over public network connections for your account.

`--status`
:   (Optional) Check whether the use of public connections is prevented for image pushes or pulls in your account.

### Example
{: #ic_cr_private_only_example}

Prevent image pulls or pushes over public network connections for your account by using the `--enable` option.

```sh
ibmcloud cr private-only --enable
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

Display your quotas for traffic and storage, and the usage information against those quotas for the registry region that you're targeting.

```sh
ibmcloud cr quota [--output json | -o json]
```

### Prerequisites
{: #bx_cr_quota_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_quota_option}

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Example
{: #bx_cr_quota_example}

Display your traffic and storage quotas in JSON format by entering `json` as the output option.

```sh
ibmcloud cr quota -o json
```
{: pre}

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Modify the specified quota for the registry region that you're targeting.

```sh
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```

### Prerequisites
{: #bx_cr_quota_set_prereq}

To find out more about the required permissions, see [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

### Command options
{: #bx_cr_quota_set_option}

`--traffic TRAFFIC`
:   (Optional) Changes your traffic quota to the specified value in megabytes. The operation fails if you are not authorized to set traffic, or if you set a value that exceeds your current pricing plan.

`--storage STORAGE`
:   (Optional) Changes your storage quota to the specified value in megabytes. The operation fails if you are not authorized to set storage quotas, or if you set a value that exceeds your current pricing plan.

### Example
{: #bx_cr_quota_set_example}

Set your quota limit for pull traffic to 7000 megabytes and storage to 600 megabytes by entering `7000` as your traffic quota and `600` as your storage quota.

```sh
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

Displays the targeted region and the registry. For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

```sh
ibmcloud cr region
```

### Example
{: #bx_cr_region_example}

Find out which region and registry you're targeting.

```sh
ibmcloud cr region
```
{: pre}

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Set a target region for the {{site.data.keyword.registrylong_notm}} commands. To list the available regions, run the command with no options. For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

```sh
ibmcloud cr region-set [REGION]
```

### Command arguments
{: #bx_cr_region_set_argument}

`REGION`
:   (Optional) The name of your target region, for example `us-south`. For more information, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

### Example
{: #bx_cr_region_set_example}

Target the Dallas region by entering `us-south` as the region.

```sh
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr retention-policy-list`
{: #bx_cr_retention_policy_list}

List the image retention policies for your account. Image retention policies retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted. You can also see whether the option to retain all untagged images applies to the policy.

Where an image within a repository is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

```sh
ibmcloud cr retention-policy-list [--output json | -o json]
```

### Prerequisites
{: #bx_cr_retention_policy_list_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_retention_policy_list_option}

`--output json`, `-o json`
:   (Optional) Outputs the list in JSON format.

### Example
{: #bx_cr_retention_policy_list_example}

List the retention policies in your account in JSON format by entering `json` as the output.

```sh
ibmcloud cr retention-policy-list -o json
```
{: pre}

For more information about how to use the `ibmcloud cr retention-policy-list` command, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## `ibmcloud cr retention-policy-set`
{: #bx_cr_retention_policy_set}

Set a policy to retain the specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted. When you set a policy it runs interactively, then it runs daily. You can set only one policy in each namespace.

You can choose whether to exclude all untagged images from the total number of images that you decide to retain.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If a retention policy deletes an image that you want to keep, you can restore the image. To identify the image, list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore the selected image by running the [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

If you want to cancel a retention policy, see [Update a retention policy to keep all your images](/docs/Registry?topic=Registry-registry_retention#retention_policy_keep).

```sh
ibmcloud cr retention-policy-set [--retain-untagged] [--force | -f] --images IMAGE_COUNT NAMESPACE
```

### Prerequisites
{: #bx_cr_retention_policy_set_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_retention_policy_set_argument}

`NAMESPACE`
:   The namespace for which you want to create a policy.

### Command options
{: #bx_cr_retention_policy_set_option}

`--retain-untagged`
:   (Optional) Retain all untagged images when the retention policy is being processed. Only tagged images are analyzed and, if the images don't meet the criteria, they are deleted. If the option isn't specified, all tagged and untagged images are analyzed and, if the images don't meet the criteria, they are deleted.

`--force`, `-f`
:   (Optional) Force the command to run with no user prompts.

`--images`
:   Determines how many images to keep within each repository in the specified namespace. The newest images are retained. The age of images is determined by their build date. `IMAGE_COUNT` is the number of images that you want to retain in each repository for the namespace. To return a policy to the default state that keeps all the images set `IMAGE_COUNT` to `All`.

### Examples
{: #bx_cr_retention_policy_set_example}

Set a policy that retains the newest 20 images within each repository in the `birds` namespace by entering `20` as the number of images to keep and `birds` as the namespace.

```sh
ibmcloud cr retention-policy-set --images 20 birds
```
{: pre}

Revert the policy to the default state so that you keep all your images in the `birds` namespace by entering `All` as the number of images to keep and `birds` as the namespace.

```sh
ibmcloud cr retention-policy-set --images All birds
```
{: pre}

For more information about how to use the `ibmcloud cr retention-policy-set` command, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## `ibmcloud cr retention-run`
{: #bx_cr_retention_run}

Cleans up a namespace by retaining a specified number of images for each repository within a namespace in {{site.data.keyword.registrylong_notm}}. All other images in the namespace are deleted.

You can choose whether to exclude all untagged images from the total number of images that you decide to retain.

Where an image, within a repository, is referenced by multiple tags, that image is counted only once. Newest images are retained. Age is determined by when the image was created, not when it was pushed to the registry.
{: tip}

If you want to restore a deleted image, you can list the contents of the trash by running the [`ibmcloud cr trash-list`](#bx_cr_trash_list) command and restore a selected image by running the [`ibmcloud cr image-restore`](#bx_cr_image_restore) command.
{: tip}

If an image that you're expecting to see doesn't show in the list that is produced, see [Why doesn't the retention command show all the images?](/docs/Registry?topic=Registry-troubleshoot-image-list-retention) for assistance.
{: tip}

```sh
ibmcloud cr retention-run [--force | -f [--output json | -o json]] [--retain-untagged] --images IMAGE_COUNT NAMESPACE
```

### Prerequisites
{: #bx_cr_retention_run_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_retention_run_argument}

`NAMESPACE`
:   The namespace that you want to clean up.

### Command options
{: #bx_cr_retention_run_option}

`--force`, `-f`
:   (Optional) Force the command to run with no user prompts.

`--output json`, `-o json`
:   (Optional) Outputs JSON that contains the results of cleaning your namespace. This option must be used with `--force`.

`--retain-untagged`
:   (Optional) Retain all untagged images when the retention policy is being processed. Only tagged images are analyzed and, if the images don't meet the criteria, they are deleted. If the option isn't specified, all tagged and untagged images are analyzed and, if the images don't meet the criteria, they are deleted.

`--images`
:   Determines how many images to keep within each repository in the specified namespace. The newest images are retained. The age of images is determined by their build date. `IMAGE_COUNT` is the number of images that you want to retain in each repository for the namespace.

### Example
{: #bx_cr_retention_run_example}

Retain the newest 20 images within each repository in the `birds` namespace by entering `20` as the number of images to keep and `birds` as the namespace.

```sh
ibmcloud cr retention-run --images 20 birds
```
{: pre}

For more information about how to use the `ibmcloud cr retention-run` command, see [Retaining images](/docs/Registry?topic=Registry-registry_retention).

## `ibmcloud cr trash-list`
{: #bx_cr_trash_list}

Displays all images in the trash in your {{site.data.keyword.cloud_notm}} account. You can also see the number of days that remain until the image is removed from the trash. The number of days that remain until removal is rounded up. For example, if the time until removal is 2 hours, it shows as 1 day. Images remain in the trash for 30 days after they are deleted from your live repository.

If you want to restore an image from the trash, run the [`ibmcloud cr image-restore`](#bx_cr_image_restore) command, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).

```sh
ibmcloud cr trash-list [--restrict NAMESPACE] [--output json | -o json]
```

### Prerequisites
{: #bx_cr_trash_list_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command options
{: #bx_cr_trash_list_option}

`--restrict NAMESPACE`
:   (Optional) Limit the output to display only images in the specified namespace.

`--output json`, `-o json`
:   (Optional) Outputs JSON that contains the details of the contents of the trash.

### Example
{: #bx_cr_trash_list_example}

Display the images that are in the trash in the `birds` namespace by entering `birds` as the restriction.

```sh
ibmcloud cr trash-list --restrict birds
```
{: pre}

## `ibmcloud cr va-version`
{: #ic_cr_va_version}

Find out which version of Vulnerability Advisor you're using. Version 4 is the only valid version.

```sh
ibmcloud cr va-version
```

### Example
{: #ic_cr_va_version_example}

Find out which version of Vulnerability Advisor you're using.

```sh
ibmcloud cr va-version
```
{: pre}

## `ibmcloud cr va-version-set`
{: #ic_cr_va_version_set}

Set the version of Vulnerability Advisor. The only valid value is `v4`.

If you try to set an invalid version of Vulnerability Advisor, you get en error, see [Why do I get an error about an invalid version of Vulnerability Advisor being specified?](/docs/Registry?topic=Registry-troubleshoot-va-version-error) for assistance.
{: tip}

```sh
ibmcloud cr va-version-set VERSION
```

### Command arguments
{: #ic_cr_va_version_set_argument}

`VERSION`
:   The version of Vulnerability Advisor that you want to use. The only valid value is `v4`.

### Example
{: #ic_cr_va_version_set_example}

Set the version of Vulnerability Advisor to version 4 by entering `v4` as the version:

```sh
ibmcloud cr va-version-set v4
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

View a vulnerability assessment report for your images.

```sh
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```

### Prerequisites
{: #bx_cr_va_prereq}

To find out more about the required permissions, see [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using).

### Command arguments
{: #bx_cr_va_argument}

`IMAGE`
:   The name of the image for which you want to get a report. The report states whether the image has any known package vulnerabilities. You can request reports for multiple images at the same time by listing each image in the command with a space between each name.

    To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the **Repository** column (`repository`) and **Tag** column (`tag`) separated by a colon (`:`) to create the image name in the format `repository:tag`. If a tag is not specified in the image name, the report assesses the image that is tagged `latest`.

    For more information about supported Docker base images, see [Vulnerable packages](/docs/Registry?topic=Registry-va_index&interface=ui#packages).

    For more information, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=Registry-va_index&interface=ui).

### Command options
{: #bx_cr_va_option}

`--extended`, `-e`
:   (Optional) The command output shows additional information about fixes for vulnerable packages.

`--vulnerabilities`, `-v`
:   (Optional) The command output is restricted to show vulnerabilities only.

`--output FORMAT`, `-o FORMAT`
:   (Optional) The command output is returned in the chosen format. The default format is `text`.

    The following formats are supported:

    - `text`
    - `json`

### Examples
{: #bx_cr_va_example}

View a standard vulnerability assessment report for the `us.icr.io/birds/bluebird:1` image by entering `us.icr.io/birds/bluebird:1` as the image.

```sh
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

View a vulnerability assessment report that shows the vulnerabilities for the `us.icr.io/birds/bluebird:1` image in JSON format by using the `-- vulnerabilities` option, and by entering `json` as the format for the output and `us.icr.io/birds/bluebird:1` as the image.

```sh
ibmcloud cr vulnerability-assessment --vulnerabilities --output json us.icr.io/birds/bluebird:1
```
{: pre}
