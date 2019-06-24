---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-16"

keywords: IBM Cloud Container Registry, Docker Content Trust, keys, trusted content, signing, signing images, repository keys, 

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

# 对映像签名以实现可信内容
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} 提供可信内容技术，以便您可以对映像签名，以确保注册表名称空间中映像的完整性。通过拉出和推送签名的映像，可以验证映像是否由正确的参与方（例如，连续集成 (CI) 工具）推送。要使用此功能，您必须具有 Docker V18.03 或更高版本。您可以通过查看 [Docker Content Trust ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.docker.com/engine/security/trust/content_trust/) 和 [Notary 项目 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/theupdateframework/notary) 文档来了解更多信息。
{:shortdesc}

在启用了可信内容的情况下推送映像时，Docker 客户机还会将签名的元数据对象也推送到 {{site.data.keyword.cloud_notm}} 信任服务器中。在启用了 Docker Content Trust 的情况下拉出标记的映像时，Docker 客户机会联系信任服务器，以确定所请求标记的最新签名版本，验证内容签名，然后下载签名的映像。

映像名称由存储库和标记组成。使用可信内容时，每个存储库都使用唯一的签名密钥。存储库中的每个标记都会使用属于该存储库的密钥。如果您有多个团队在发布内容，每个团队将内容发布到 {{site.data.keyword.registrylong_notm}} 名称空间内其自己的存储库，那么每个团队可以使用自己的密钥来对其内容进行签名，以便您可以验证各个映像是否由相应的团队生成。

存储库可以包含签名的内容和未签名的内容。如果启用了 Docker Content Trust，那么可以访问存储库中签名的内容，即使同时存在其他未签名的内容也不例外。

针对旧 (`registry.bluemix.net`) 域名和新 (`icr.io`) 域名，映像具有不同的签名。从旧域名中拉出该映像后，现有签名才会有效。如果想要从新域名中拉出签名的内容，必须为新域名 `icr.io` 对该映像重新签名，请参阅[为新域名对映像重新签名](#trustedcontent_resign)。
{: note}

Docker Content Trust 使用“首次使用时信任”安全模型。首次从存储库拉出签名的映像时，将从信任服务器中拉出存储库密钥，该密钥未来将用于对来自该存储库中的映像进行验证。首次拉出存储库之前，必须确定您是信任信任服务器还是信任映像及其发布程序。如果服务器中的信任信息遭到破坏，并且您之前尚未从存储库中拉出映像，那么 Docker 客户机可能会从信任服务器中拉出遭到破坏的信息。如果首次拉出映像后信任数据遭到破坏，那么后续拉出时，Docker 客户机将无法验证遭到破坏的数据，并且不会拉出映像。有关如何检查映像的信任数据的更多信息，请参阅[查看签名的映像](#trustedcontent_viewsigned)。

有关“首次使用时信任”安全模型的更多信息，请参阅 [The Update Framework ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://theupdateframework.github.io/)。

## 设置可信内容环境
{: #trustedcontent_setup}

缺省情况下，Docker Content Trust 处于禁用状态。请在登录到 {{site.data.keyword.registrylong_notm}} 并使用签名的映像之前，启用内容信任环境。
{:shortdesc}

1. 在终端中启用 Docker Content Trust 环境变量。

   对于 Linux 或 Mac：

   ```
export DOCKER_CONTENT_TRUST=1
    ```
   {: codeblock}

   对于 Windows：

   ```
set DOCKER_CONTENT_TRUST=1
    ```
   {: codeblock}

2. 登录到 {{site.data.keyword.cloud_notm}} CLI。

   ```
    ibmcloud login [--sso]
    ```
   {: pre}

   如果拥有的是联合标识，请使用 `ibmcloud login --sso` 登录。输入您的用户名，并使用 CLI 输出中提供的 URL 来检索一次性密码。如果您有联合标识，那么应该知道不使用 `--sso` 会登录失败，使用 `--sso` 选项会登录成功。
    {: tip}

3. 将要使用的区域设定为目标。如果您不知道区域名称，可以运行不带区域的命令，然后选择区域。

   ```
    ibmcloud cr region-set <region>
    ```
   {: pre}

4. 登录到 {{site.data.keyword.registrylong_notm}}。

   ```
  ibmcloud cr login
  ```
   {: pre}

   输出会指示您导出 Docker Content Trust 环境变量。

   **示例**

   ```
   user:~ user$ ibmcloud cr login
   正在登录到 'us.icr.io'...
   已登录到 'us.icr.io'。

   要使用内容信任来设置 Docker 客户机，请导出以下环境变量：
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: screen}

5. 在终端中复制并粘贴该环境变量命令。例如：

   ```
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: pre}

现在，您已准备就绪，可以推送、拉出和管理可信的签名映像。

在启用了 Docker Content Trust 的会话期间，如果要在禁用可信内容的情况下执行操作（例如，拉出未签名映像），请将 `--disable-content-trust` 标志与命令配合使用。
{: tip}

## 推送签名的映像
{: #trustedcontent_push}

首次推送签名的映像时，Docker 会自动创建一对签名密钥：根密钥和存储库密钥。要对之前已推送签名映像的存储库中的映像签名，必须在要推送该映像的机器上装入正确的存储库签名密钥。
{:shortdesc}

开始之前，请[设置注册表名称空间](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add)。

1. [设置可信内容环境](#trustedcontent_setup)。

2. [推送映像](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)。必须对可信内容使用标记。在命令输出中，您会看到：

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

3. **首次推送签名的存储库**。将签名的映像推送到新存储库时，命令会创建两个签名密钥 - 根密钥和存储库密钥，并将它们存储在本地计算机中。为每个密钥输入并保存安全口令，然后[备份密钥](#trustedcontent_backupkeys)。由于[恢复选项](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent)受到限制，因此备份密钥非常重要。

## 拉出签名的映像
{: #trustedcontent_pull}

首次在启用了 Docker Content Trust 的情况下拉出签名的映像时，Docker 客户机会将该签名识别为可信。Docker 客户机会拉出所指定映像的最新签名版本。不会拉出未签名的映像或不可信内容。
{:shortdesc}

1. [设置可信内容环境](#trustedcontent_setup)。

2. 拉出映像。将 `<source_image>` 替换为映像的存储库，并将 `<tag>` 替换为要使用的映像标记，例如 _latest_。要列出可拉出的可用映像，请运行 `ibmcloud cr image-list`。

   ```
    docker pull <source_image>:<tag>
    ```
   {: pre}

    在推送或拉出签名的映像时指定标记。仅当禁用了内容信任时，才会缺省使用 `latest` 标记。
    {: tip}

## 为新域名对映像重新签名
{: #trustedcontent_resign}

要为新域名 `icr.io` 对映像重新签名，必须拉出、标记和推送该映像。
{:shortdesc}

1. 从旧域名中拉出已签名的映像。将 `<source_image>` 替换为映像的存储库，并将 `<tag>` 替换为要使用的映像标记，例如 _latest_。要列出可拉出的可用映像，请运行 `ibmcloud cr image-list`。

   ```
    docker pull <source_image>:<tag>
    ```
   {: pre}

    在推送或拉出签名的映像时指定标记。仅当禁用了内容信任时，才会缺省使用 `latest` 标记。
    {: tip}

2. 针对新域名运行 `docker tag` 命令。将 `<old_domain_name>` 替换为旧域名，将 `<new_domain_name>` 替换为新域名，将 `<repository>` 替换为存储库的名称，将 `<tag>` 替换为标记的名称。

   ```
   docker tag <old_domain_name>/<repository>:<tag> <new_domain_name>/<repository>:t<tag>
   ```
   {: pre}

3. 通过使用新域名来推送映像，请参阅[将 Docker 映像推送到名称空间](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)。必须对可信内容使用标记。在命令输出中，您会看到：

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

## 管理可信内容
{: #trustedcontent_managetrust}

通过使用 `docker trust` 命令，可以查看映像的签署者和撤销信任内容状态。要运行 `docker trust` 命令，您必须具有 Docker 18.03 或更高版本。
{:shortdesc}

### 查看签名的映像
{: #trustedcontent_viewsigned}

可以查看映像存储库或标记的签名版本，包括有关密钥标识和签署者的信息。
{:shortdesc}

1. [设置可信内容环境](#trustedcontent_setup)。

2. 查看每个映像的标记、摘要和签署者信息。

   （可选）指定标记 `<tag>` 以查看有关该版本映像的信息。

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### 撤销信任
{: #trustedcontent_revoketrust}

可以撤销映像的可信内容状态。
{:shortdesc}

开始之前，请先检索[首次推送可信存储库](#trustedcontent_push)时保存的存储库密钥口令。如果需要确定哪个密钥用于可信映像，请使用 `docker view` [命令](#trustedcontent_viewsigned)。

1. [设置可信内容环境](#trustedcontent_setup)。

2. 除去映像存储库的所有可信元数据。在提示时输入存储库密钥口令。

   （可选）指定标记以仅撤销该版本映像的可信元数据。

   ```
docker trust revoke <image>:<tag>
    ```
   {: pre}

3. 验证可信内容列表中信任是否已撤销。

   （可选）如果要验证所标记映像的已撤销内容，请包含此标记。

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   前一个命令的输出：

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## 备份签名密钥
{: #trustedcontent_backupkeys}

首次将签名的映像推送到新存储库时，Docker Content Trust 会创建两个签名密钥 - 根密钥和存储库密钥，并将它们存储在本地计算机上：

- Linux 和 Mac 目录：`~/.docker/trust/private`

- Windows 目录：`%HOMEPATH%\.docker\trust\private`

   如果更改了 Docker 配置目录，请在更改后的目录中查找 `trust` 子目录。
   {: tip}

您必须备份所有密钥，尤其是根密钥。如果密钥丢失或遭到破坏，[恢复选项](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent)会受到限制。

要备份密钥，请参阅 [Docker Content Trust 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys)。

## 管理可信签署者
{: #trustedcontent_signers}

可以在存储库中签名的映像中添加和除去签署者。
{:shortdesc}

### 向可信存储库添加签署者
{: #trustedcontent_addsigners}

要允许其他用户对存储库中的映像签名，请将这些用户的签名密钥添加到该存储库。
{:shortdesc}

**开始之前**

- 映像签署者必须具有将映像推送到名称空间的许可权。
- 存储库所有者和其他签署者必须安装了 Docker 18.03 或更高版本。
- 通过[推送签名的映像](#trustedcontent_push)来创建可信内容存储库。存储库所有者必须具有用于其本地计算机上 Docker 信任文件夹中可用存储库的存储库管理密钥。如果您没有存储库管理密钥，请与所有者联系以执行此任务。

添加签署者后，您不能再使用存储库管理密钥来对该存储库中的映像签名。您必须持有其中一个已核准签署者的专用密钥才能签名。要在添加签署者后保留对映像签名的能力，请再次遵循上述指示信息来为自己生成并添加签署者角色。
{:tip}

要共享签名密钥，请执行以下操作：

1. 如果新的签署者尚未生成密钥对，那么必须生成并装入密钥对。
  
    a. 生成密钥。您可以为 `<NAME>` 输入任何名称，但是，您选择的名称在有人检查对存储库的信任时会显示。与存储库所有者合作，以满足组织可能使用的任何命名约定，并选择可识别该签署者的名称。

      ```
docker trust key generate <NAME>
      ```
      {: pre}
  
    b. 输入专用密钥的口令。这将生成公用密钥 (`.pub`) ，并且对应的专用密钥会自动装入到 Docker 信任配置中。
  
    c. 新的签署者必须向存储库所有者发送公用密钥。

2. 存储库所有者必须将签署者的密钥添加到存储库。

    a. [设置可信内容环境](#trustedcontent_setup)。

    b. 将签署者的密钥添加到存储库。

      ```
docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}

3. 签署者可以设置其环境并对映像签名。

    a. [设置可信内容环境](#trustedcontent_setup)。

    b. 签署者必须对映像签名。提示时，输入专用密钥的口令。

      ```
docker trust sign <repository>:<tag>
      ```
      {: pre}

4. 要验证是否添加了签署者，请参阅[查看签名的映像](#trustedcontent_viewsigned)。

### 从存储库中除去签署者
{: #trustedcontent_removesigner}

如果您不再希望签署者能够对存储库中的映像签名，那么可以将其作为签署者除去。
{:shortdesc}

开始之前，存储库所有者和其他签署者必须安装了 Docker 18.03 或更高版本。

如果除去签署者，那么信任服务器不会再信任其所签名的映像版本。要确保在除去签署者之后可以拉出该映像，请确保签署者未对最新版本的映像签名，然后再继续操作。如果签署者已对最新版本的映像签名，请将更新推送到该映像，使用您的密钥对其签名，然后再继续操作。
{:tip}

要除去签署者，请执行以下操作：

1. [设置可信内容环境](#trustedcontent_setup)。

2. 除去签署者。

   ```
docker trust signer remove <NAME> <repository>
    ```
   {: pre}

3. 要验证是否除去了签署者，请查看映像的信任数据，并验证该签署者是否不再列出。有关查看信任数据的更多信息，请参阅[查看签名的映像](#trustedcontent_viewsigned)。
