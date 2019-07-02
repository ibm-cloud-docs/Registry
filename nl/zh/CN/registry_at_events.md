---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-21"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker events, Activity Tracker events, events, track,

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

使用 {{site.data.keyword.cloudaccesstrailfull}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.cloud}} 中的 {{site.data.keyword.registrylong}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服务会记录哪些用户发起的活动会更改 {{site.data.keyword.cloud_notm}} 中服务的状态。有关更多信息，请参阅 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)。

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
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>在 {{site.data.keyword.registrylong_notm}} 中构建 Docker 映像。</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>从 {{site.data.keyword.registrylong_notm}} 中删除映像。</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>显示有关映像的详细信息。</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>列出 {{site.data.keyword.IBM_notm}} 帐户中的映像。</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>从 {{site.data.keyword.registrylong_notm}} 拉出映像。</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>将映像推送到 {{site.data.keyword.registrylong_notm}}。</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>从 {{site.data.keyword.registrylong_notm}} 中删除一个或多个指定的映像。</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>添加指示预先存在的 {{site.data.keyword.registrylong_notm}} 映像的新标记。</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>从 {{site.data.keyword.registrylong_notm}} 中的每个指定映像除去一个或多个标记。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>将名称空间添加到 {{site.data.keyword.registrylong_notm}}。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>从 {{site.data.keyword.registrylong_notm}} 中删除名称空间。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>列出 {{site.data.keyword.IBM_notm}} 帐户中的名称空间。</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>显示流量和存储的当前配额以及这些配额的使用情况信息。</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>修改配额。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.create`</td>
	  <td>创建新注册表令牌。（不推荐）</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>删除注册表令牌。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>检索有关注册表令牌的信息。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>列出 {{site.data.keyword.IBM_notm}} 帐户中的注册表令牌。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>删除多个注册表令牌。</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>显示有关当前价格套餐的信息。</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>升级到标准套餐。</td>
  </tr>
 </table>

## 在何处查找事件
{: #ui}

在生成事件的 {{site.data.keyword.cloud_notm}} 区域中可用的 {{site.data.keyword.cloudaccesstrailshort}} **帐户域**中，{{site.data.keyword.cloudaccesstrailshort}} 事件可用（`ap-north` 除外）。`ap-north` 的事件显示在 `ap-south` 中。

{{site.data.keyword.registrylong_notm}} 或漏洞顾问程序事件所在的[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)对应于映像或名称空间等资源所在的 {{site.data.keyword.registrylong_notm}} 区域。
