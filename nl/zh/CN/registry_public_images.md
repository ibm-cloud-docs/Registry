---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 公共 {{site.data.keyword.IBM_notm}} 映像
{: #public_images}

您可以使用命令行来访问 {{site.data.keyword.IBM}} 提供的映像。不能再使用图形用户界面来访问公共 {{site.data.keyword.IBM_notm}} 映像。
{:shortdesc}

## 使用 CLI 访问公共 IBM 映像
{: #public_images_cli}

您可以使用命令行来访问公共 {{site.data.keyword.IBM_notm}} 映像。
{:shortdesc}

**开始之前**

- 登录到 [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)：

  ```
    ibmcloud login
    ```
  {: pre}

要列出公共映像，请完成以下步骤：

1. 将全局注册表设定为目标：

   ```
ibmcloud cr region-set global
```
   {: pre}

2. 列出 {{site.data.keyword.IBM_notm}} 公共映像：

   ```
ibmcloud cr images --include-ibm
```
   {: pre}
