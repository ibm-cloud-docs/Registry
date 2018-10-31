---

copyright:
  years: 2018, 
lastupdated: "2018-09-03"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 常见问题
{: #registry_faq}


## 如何列出公共映像？
{: #faq_list_public_images}

要列出公共映像，请运行以下 `ibmcloud` 命令来将全局注册表设定为目标并列出 IBM 提供的公共映像：

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}


## 是否能使用非 Docker 工具构建映像并推送到注册表？
{: #faq_tools}

是，只要工具支持 OCI 图像格式和协议即可。
