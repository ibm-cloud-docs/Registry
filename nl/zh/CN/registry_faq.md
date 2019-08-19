---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, FAQ, Vulnerability Advisor,

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

## 如何使用访问控制和 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}？
{: #faq_access_control}
{: faq}

您可以创建 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) 策略来控制对 {{site.data.keyword.registrylong_notm}} 中名称空间的访问权。有关更多信息，请参阅[教程：授予对 {{site.data.keyword.registrylong_notm}} 资源的访问权](/docs/services/Registry?topic=registry-iam_access)和[使用 Identity and Access Management 管理用户访问权](/docs/services/Registry?topic=registry-iam)。

## 哪些区域可用于 {{site.data.keyword.registrylong_notm}}？
{: #faq_regions}
{: faq}

您可以在[本地区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local)托管映像。IBM 托管的公共映像位于[全局注册表](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)中。

## 为什么我收到扫描未找到新增映像的错误消息？
{: #faq_va_new_scan_error}
{: faq}

如果您在将映像添加到注册表后立即收到漏洞报告，那么可能会收到以下错误消息：

```
BXNVA0009E: 扫描未找到 <imagename>。请稍后重试。
如果问题仍然存在，请联系支持人员以获取帮助；
请参阅 https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

您收到此消息是因为图像扫描与结果请求不是同步的，而扫描过程需要一段时间才能完成。正常操作期间，在您将映像添加到注册表后的几分钟内即会完成扫描。具体花费的时间取决于映像大小和进入注册表的流量等可变因素。

如果您是在构建管道流程中收到此消息，并且此错误定期出现，请尝试添加包含短暂停顿的重试逻辑。

如果仍有无法接受的性能问题，可联系支持人员，请参阅[获取有关 {{site.data.keyword.registrylong_notm}} 的帮助和支持](/docs/services/Registry?topic=registry-ts_index#gettinghelp)。

## 如何触发漏洞顾问程序扫描？
{: #faq_va_trigger_scan}
{: faq}

如果出现下列其中一种情况，就会触发映像扫描：

- 有新的映像推送到注册表。
- 如果距最后一次扫描的已经超过 7 天，那么映像会排队等待重新扫描，这可能需要一些时间才能完成。
- 针对映像中安装的包发布了新的安全通知，该映像将排队等待重新扫描，这可能需要一些时间才能完成。因发布新的安全通知而触发的重新扫描仅适用于 Ubuntu 和 Debian 映像。

## 安全通知多久更新一次？
{: #faq_va_update_security_notice}
{: faq}

漏洞顾问程序的安全通知大约每 12 小时从供应商的操作系统站点装入一次。
