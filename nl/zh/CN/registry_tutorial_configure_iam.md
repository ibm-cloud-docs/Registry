---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, user access, tutorial, access control, 

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

# 教程：授予对 {{site.data.keyword.registrylong_notm}} 资源的访问权
{: #iam_access}

使用本教程可了解如何通过为 {{site.data.keyword.registrylong_notm}} 配置 {{site.data.keyword.iamlong}} (IAM) 来授予对资源的访问权。
{:shortdesc}

本教程大约需要 45 分钟。

**开始之前**

- 完成 [{{site.data.keyword.registrylong_notm}} 入门](/docs/services/Registry?topic=registry-getting-started#getting-started)中的指示信息。

- 确保您具有 {{site.data.keyword.cloud_notm}} CLI 的 `container-registry` CLI 插件的最新版本；请参阅[更新 `container-registry` CLI 插件](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update)。

- 您必须有权访问可用于本教程的两个 [{{site.data.keyword.cloud_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login)，一个是用户 A 的帐户，一个是用户 B 的帐户，每个帐户必须使用唯一的电子邮件地址。您在自己的帐户（用户 A）中工作，并邀请另一个用户（用户 B）使用您的帐户。您可以选择创建第二个 {{site.data.keyword.cloud_notm}} 帐户，也可以与有 {{site.data.keyword.cloud_notm}} 帐户的同事一起合作。

- 如果您在 2018 年 10 月 4 日之前就开始使用 {{site.data.keyword.registrylong_notm}}，那么必须通过运行 `ibmcloud cr iam-policies-enable` 命令来启用 IAM 策略强制实施。如果您邀请了其他使用您的 {{site.data.keyword.registrylong_notm}} 名称空间的用户加入您的 IBM Cloud 帐户，请以用户 A 的身份使用其他帐户以防止其访问中断。

## 步骤 1：授权用户配置注册表
{: #configure_registry}

在此部分中，您将向帐户添加第二个用户，并向其授予配置 {{site.data.keyword.registrylong_notm}} 的能力。
{:shortdesc}

1. 将用户 B 添加到用户 A 的帐户：

    1. 通过运行以下命令，登录到用户 A 的帐户：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 通过运行以下命令，邀请用户 B 访问用户 A 的帐户，其中 _`<user.b@example.com>`_ 是用户 B 的电子邮件地址：

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. 通过运行以下命令，获取用户 A 的帐户标识：

        ```
        ibmcloud target
        ```
        {: pre}

        记下“帐户”行中括号 ( ) 内的“帐户标识”。

2. 证明用户 B 可以将用户 A 的帐户设为目标，但尚不能对 {{site.data.keyword.registrylong_notm}} 执行任何操作：

    1. 以用户 B 的身份登录，并运行以下命令将用户 A 的帐户设定为目标，其中 _`<YourAccountID>`_ 是用户 A 的帐户标识：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 尝试通过运行以下命令，将注册表配额编辑为 4 GB 流量：

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        此命令失败，因为用户 B 没有正确的访问权。

3. 授予用户 B“管理者”角色，以便用户 B 可以配置 {{site.data.keyword.registrylong_notm}}：

    1. 通过运行以下命令，以您自己的身份（即用户 A）重新登录到您的帐户：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 通过运行以下命令，创建策略以用于将“管理者”角色授予用户 B：

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. 证明用户 B 现在可以在用户 A 的帐户中更改配额：

    1. 通过运行以下命令，以用户 B 的身份登录，并将用户 A 的帐户设为目标：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 尝试通过运行以下命令，将注册表配额编辑为 4 GB 流量：

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        此命令有效，因为用户 B 有正确类型的访问权。

    3. 现在，通过运行以下命令将配额更改回原来的值：
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. 清除：

    1. 通过运行以下命令，以您自己的身份（即用户 A）重新登录到您的帐户：
  
        ```
    ibmcloud login
    ```
        {: pre}
  
    2. 列出用户 B 的策略，通过运行以下命令找到您刚才创建的策略，并记下相应标识：
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. 通过运行以下命令来删除策略，其中 _`<Policy_ID>`_ 是策略标识：
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## 步骤 2：授权用户访问特定名称空间
{: #access_resources}

在此部分中，您将创建一些具有样本映像的名称空间，并授予对这些名称空间的访问权。您可以创建策略来为每个名称空间授予不同的角色，并显示相应的影响。
{:shortdesc}

1. 在用户 A 的帐户中创建三个新的名称空间。这些名称空间在整个区域中必须唯一，因此，请选择您自己的名称空间名称，但本教程使用的是 `namespace_a`、`namespace_b` 和 `namespace_c` 作为示例：

    1. 通过运行以下命令，以用户 A 的身份登录：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 通过运行以下命令，创建名称空间 `namespace_b`：

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}

        名称空间名称在区域中必须唯一。
        {: tip}

    3. 通过运行以下命令，创建另一个名称空间 `namespace_c`：

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. 证明用户 B 看不到任何内容：

    1. 通过运行以下命令，以用户 B 的身份登录，并将用户 A 的帐户设为目标：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 通过运行以下命令，以用户 B 的身份尝试列出映像：

        ```
    ibmcloud cr images
    ```
        {: pre}

        这会返回空列表，因为用户 B 无权访问任何名称空间。

3. 通过运行以下命令，创建策略以用于授予用户 B 与名称空间进行交互的能力：

    1. 通过运行以下命令，以用户 A 的帐户身份登录：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 通过运行以下命令，检查是否至少列出了三个名称空间：

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        这将显示在本教程中创建的三个名称空间（`namespace_a`、`namespace_b` 和 `namespace_c`）。如果看不到这些名称空间，请返回并遵循指示信息以再次创建这些名称空间。

    3. 通过运行以下命令，创建策略以用于授予用户 B 在 `namespace_b` 上的“读取者”角色，其中 _`<Region>`_ 是[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)的名称，例如 `us-south`：

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource <namespace_b> --roles Reader
        ```
        {: pre}

    4. 通过运行以下命令，创建第二个策略以用于授予用户 B 在 `namespace_c` 上的“读取者”和“写入者”角色：

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        此命令会在同一策略中向同一资源添加两个角色。
        {: tip}

4. 将映像推送到 `namespace_a` 和 `namespace_b`：

    1. 通过运行以下命令，拉出 `hello-world` 映像：

        ```
        docker pull hello-world
        ```
        {: pre}

    2. 通过运行以下命令，将映像标记为 `namespace_a`：

        ```
        docker tag hello-world <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. 通过运行以下命令，将映像标记为 `namespace_b`：

        ```
        docker tag hello-world <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. 通过运行以下命令，登录到 {{site.data.keyword.registrylong_notm}}：

        ```
    ibmcloud cr login
    ```
        {: pre}

    5. 通过运行以下命令，将映像推送到 `namespace_a`：

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. 通过运行以下命令，将映像推送到 `namespace_b`：

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

5. 证明用户 B 可以与 `namespace_b` 和 `namespace_c` 交互，但不能与 `namespace_a` 交互：

    1. 通过运行以下命令，以用户 B 的身份登录：

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 通过运行以下命令，表明用户 B 可以看到 `namespace_b` 和 `namespace_c`，但看不到 `namespace_a`，因为用户 B 无权访问 `namespace_a`：

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. 通过运行以下命令来列出映像：

        ```
    ibmcloud cr images
    ```
        {: pre}

        `namespace_b` 中的映像会显示在列表中，但 `namespace_a` 中的映像不会显示在列表中，因为用户 B 无权访问 `namespace_a`。

    4. 通过运行以下命令，登录到 {{site.data.keyword.registrylong_notm}}：

        ```
    ibmcloud cr login
    ```
        {: pre}

    5. 通过运行以下命令来拉出映像：

        ```
        docker pull <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. 通过运行以下命令，将映像推送到 `namespace_b`：

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        由于用户 B 在 `namespace_b` 中没有“写入者”角色，所以此命令失败。

    7. 通过运行以下命令，将映像标记为 `namespace_c`：

        ```
        docker tag hello-world <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. 通过运行以下命令，将映像推送到 `namespace_c`：

        ```
        docker push <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        此命令有效，因为用户 B 在 `namespace_c` 中具有“写入者”角色。

    9. 通过运行以下命令，从 `namespace_c` 中执行拉出：

        ```
        docker pull <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        此命令用效，因为用户 B 在 `namespace_c` 中具有“读取者”角色。

6. 清除：

    1. 通过运行以下命令，重新登录到用户 A 的帐户：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 通过运行以下命令，列出用户 B 的策略：

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        找到刚才创建的策略并记下策略标识。

    3. 通过运行以下命令，删除刚才创建的策略，其中 _`<Policy_ID>`_ 是策略标识：

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## 步骤 3：创建服务标识并授予对资源的访问权
{: #service_id}

在此部分中，您将配置服务标识并向其授予对 {{site.data.keyword.registrylong_notm}} 名称空间的访问权。
{:shortdesc}

1. 为服务标识设置对 {{site.data.keyword.registrylong_notm}} 的访问权，并为其创建 API 密钥：

    1. 通过运行以下命令，登录到用户 A 的帐户：

        ```
    ibmcloud login
    ```
        {: pre}

    2. 通过运行以下命令，创建名为 `cr-roles-tutorial` 的服务标识，并使用描述 `"Created during the access control tutorial for Container Registry"`：

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. 通过运行以下命令，为服务标识创建服务策略，用于授予该标识在 `namespace_a` 上的“读取者”角色：

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. 通过运行以下命令，创建第二个服务策略，用于授予在 `namespace_b` 上的“写入者”角色：

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. 通过运行以下命令，为服务标识创建 API 密钥：

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. 通过 Docker 使用服务标识 API 密钥进行登录，其中 _`<API_Key>`_ 是您的 API 密钥，用于与注册表进行交互：

    1. 通过运行以下命令，登录到 {{site.data.keyword.registrylong_notm}}：

        ```
        docker login -u iamapikey -p <API_Key> <Region>.icr.io
        ```
        {: pre}

    2. 通过运行以下命令来拉出映像：

        ```
        docker pull <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        此命令有效。

    3. 通过运行以下命令，将映像推送到 `namespace_a`：

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        由于用户在 `namespace_a` 中没有“写入者”角色，所以此命令无效。

    4. 通过运行以下命令，将映像推送到 `namespace_b`：

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        此命令有效，因为用户在 `namespace_b` 中具有“写入者”角色。

3. 清除：

    1. 通过运行以下命令来列出服务策略：

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        记下您的策略标识。

    2. 通过对每个服务策略运行以下命令来删除策略：

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. 通过运行以下命令来删除服务标识：

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. 以用户 A 的身份重新登录到 {{site.data.keyword.registrylong_notm}}：

        ```
    ibmcloud cr login
    ```
        {: pre}

## 步骤 4：清除
{: #clean_up}

在此部分中，您将除去先前部分中创建的资源，以使帐户保留为在本教程开始时的原样。
{:shortdesc}

1. 通过运行以下命令，登录到您的帐户：

    ```
    ibmcloud login
    ```
    {: pre}

2. 通过运行以下命令，删除 `namespace_a`、`namespace_b` 和 `namespace_c`：

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. 通过运行以下命令，除去您帐户中的用户 B：

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

做得不错！您已成功完成本教程。
