---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-02"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, 

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
{:faq: data-hd-content-type='faq'}

# 常见问题 (FAQ)
{: #registry_faq}

有关 {{site.data.keyword.registrylong}} 的常见问题。
{: shortdesc}

## 如何列出公共映像？
{: #faq_list_public_images}
{: faq}

要列出公共映像，请运行以下 `ibmcloud` 命令来定位到全局注册表并列出 IBM 提供的公共映像：

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## 是否可以使用非 Docker 工具来构建映像并将映像推送到注册表中？
{: #faq_tools}
{: faq}

可以，只要工具支持 OCI 图像格式和协议即可。
