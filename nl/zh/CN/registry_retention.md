---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# 保留映像
{: #registry_retention}

您可以决定是删除还是保留映像。
{:shortdesc}

## 规划保留
{: #retention_plan}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) 命令会逐个名称空间运行，因此，通过在管道中使用多个名称空间，就意味着可以应用最符合您需求的不同的保留条件。

考虑使用带有开发、编译打包和生产环境的典型交付管道。在交付代码时，持续集成和持续部署会将映像推送到注册表中，然后会直接将其部署到开发环境中。经过测试之后，开发环境中的某些构建会升级到编译打包，然后可能会进入生产环境。在此方案中，映像的更改速度在开发环境中最快，在生产环境中最慢。如果所有环境都从同一个名称空间中拉出映像，那么由于上述更改速率不同，所以要选择的需要保留的适当映像数可能会很困难。

比较好的方法是将所有映像都传递到开发名称空间中，例如，`project-development`，然后在升级到管道中更高阶段时，使用 [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) 命令将映像标记到不同的名称空间中。在上面的示例中，可以有三个名称空间：开发 `project-development`、编译打包 `project-staging` 和生产 `project-production`。在从开发升级到编译打包时，会将映像从 `project-development` 名称空间标记到 `project-staging` 名称空间中，并且会将 `project-staging` 名称空间中的映像用于部署。与之类似，在从编译打包升级到生产时，会将映像从 `project-staging` 名称空间标记到 `project-production` 名称空间中，并且会将 `project-production` 名称空间中的映像用于生产部署。

使用此方法的好处在于：

* 可以针对开发、编译打包和生产名称空间选择不同的保留设置。
* 与为所有映像使用单个名称空间相比，此方法可以将意外除去可能会在编译打包或生产环境中用到的映像的概率降至最低。
* 您可以使用不同的 [IAM](/docs/services/Registry?topic=registry-iam) 策略。例如，您可以为生产映像设置更严格的访问权。
* 您可以对生产映像签名，但不对开发和编译打包映像签名。

## 清除名称空间，仅保留符合条件的映像
{: #retention_images}

在 {{site.data.keyword.registrylong_notm}} 中通过应用指定的条件来保留名称空间中每个存储库的映像。名称空间中的其他所有映像都会被删除。
{:shortdesc}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) 命令会列出将被删除的映像，让您在删除之前还可以取消。

如果存储库中的映像被多个标记引用，那么计数时对该映像只会计一次。将保留最新的映像。生命周期是在创建映像时决定的，而不是在将其推送到注册表时确定的。
{: tip}

删除映像的操作无法撤销。删除现有部署正在使用的映像可能会导致扩展和/或重新安排失败。
{: important}

要使用 CLI 减少名称空间中每个存储库的映像数，请完成下列步骤：

1. 通过运行 `ibmcloud login` 命令登录到 {{site.data.keyword.cloud_notm}}。
2. 通过运行以下命令并选择相应的区域来选择您要清除映像的注册表：

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. 要保留一些映像、删除其他映像，请运行以下命令：

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   其中，`IMAGECOUNT` 是要为名称空间 `NAMESPACE` 中每个存储库保留的映像数。

3. 通过运行以下命令，验证是否已删除映像，然后检查该映像是否不再出现在列表中。

   ```
    ibmcloud cr image-list
    ```
   {: pre}
