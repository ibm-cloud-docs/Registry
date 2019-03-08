---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, Activity Tracker events, events

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

# {{site.data.keyword.cloudaccesstrailshort}} 事件
{: #at_events}

使用 {{site.data.keyword.cloudaccesstrailfull}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.registrylong}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服务会记录哪些用户发起的活动会更改 {{site.data.keyword.Bluemix_notm}} 中服务的状态。有关更多信息，请参阅 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla)。

下表列出了在调用时生成事件的 API 方法：

<table>
  <caption>表 1. 生成事件的操作</caption>
  <tr>
    <th>操作</th>
	  <th>描述</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>创建漏洞顾问程序豁免。</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>删除漏洞顾问程序豁免。</td>
  </tr>
 </table>

## 在何处查找事件
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件可在事件生成所在 {{site.data.keyword.Bluemix_notm}} 区域中的 {{site.data.keyword.cloudaccesstrailshort}} **帐户域**中进行查找。

漏洞顾问程序事件所在的[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)对应于映像或名称空间等资源所在的 {{site.data.keyword.registrylong_notm}} 区域。
