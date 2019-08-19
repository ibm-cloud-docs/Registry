---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker with LogDNA events, Activity Tracker events, events, track,

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

# Activity Tracker 事件
{: #at_events}

跟踪用户和应用程序如何与 {{site.data.keyword.cloud}} 中的 {{site.data.keyword.registrylong}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.at_full_notm}} 服务或（仅针对现有用户）{{site.data.keyword.cloudaccesstrailfull_notm}} 服务会记录用户发起的、会改变 {{site.data.keyword.cloud_notm}} 中服务状态的活动。
有关更多信息，请参阅 [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started)，或者（针对现有用户）[{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)。

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
    <td>`container-registry.image.bulkdelete`</td>
	  <td>从 {{site.data.keyword.registrylong_notm}} 中删除几个映像。</td>
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
	  <td>添加指示预先存在的 {{site.data.keyword.registrylong_notm}} 映像的标记。</td>
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
  </tr><tr>
    <td>`container-registry.retentionanalysis`</td>
	  <td>清除名称空间，仅保留符合条件的映像。在 {{site.data.keyword.registrylong_notm}} 中通过应用指定的条件来保留名称空间中每个存储库的映像。名称空间中的其他所有映像都会被删除。</br>
获取要删除的映像列表的请求是一个针对 `retentionanalysis` 事件类型的 `post` 操作。而删除是针对 `images` 事件类型的单个 `bulkdelete` 操作，也是针对每个单独映像的 `delete` 操作。</td>
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

### {{site.data.keyword.at_full_notm}} 事件
{: #ui_atlogdna}

{{site.data.keyword.at_full_notm}} 事件在 {{site.data.keyword.at_full_notm}} **帐户域**中可用，该帐户域在生成事件的 {{site.data.keyword.cloud_notm}} 区域中可用（`ap-south` 除外）。`ap-south` 的事件显示在 `Tokyo (jp-tok)` 中。

{{site.data.keyword.registrylong_notm}} 或漏洞顾问程序事件可用的[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)对应于资源可用的 {{site.data.keyword.registrylong_notm}} 区域。映像和名称空间是资源的示例。

|帐户注册表的区域|注册表的域名|{{site.data.keyword.at_full_notm}} 事件的位置|
|:-----------------|:-----------------|:-----------------|
| `美国南部` | `us.icr.io` |`达拉斯 (us-south)`|
| `欧洲中部` | `de.icr.io` |`法兰克福 (eu-de)`|
| `英国南部` | `uk.icr.io` | `伦敦 (eu-gb)` |
| `亚太南部` | `au.icr.io` |`东京 (jp-tok)`|
| `亚太北部` | `jp.icr.io` |`东京 (jp-tok)`|
{: caption="表 2. {{site.data.keyword.at_full_notm}} 事件的位置" caption-side="top"}

|注册表|全局注册表|{{site.data.keyword.at_full_notm}} 事件的位置|
|:-----------------|:-----------------|:-----------------|
| 全局 | `icr.io` |`达拉斯 (us-south)`|
{: caption="表 3. 全局注册表 {{site.data.keyword.at_full_notm}} 事件的位置" caption-side="top"}

### {{site.data.keyword.cloudaccesstraillong_notm}} 事件
{: #ui_at}

{{site.data.keyword.cloudaccesstraillong_notm}} 事件（仅针对现有用户）在 {{site.data.keyword.cloudaccesstraillong_notm}} **帐户域**中可用，该帐户域在生成事件的 {{site.data.keyword.cloud_notm}} 区域中可用（`ap-north` 除外）。`ap-north` 的事件显示在 `ap-south` 中。

不推荐使用 {{site.data.keyword.cloudaccesstrailfull_notm}}。从 2019 年 5 月 9 日开始，无法供应新的 {{site.data.keyword.cloudaccesstrailshort}} 实例。对现有高端套餐实例的支持持续到 2019 年 9 月 30 日。要继续监视 {{site.data.keyword.cloud_notm}} 帐户的活动，请供应 [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) 的实例。
{: deprecated}

{{site.data.keyword.registrylong_notm}} 或漏洞顾问程序事件可用的[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)对应于资源可用的 {{site.data.keyword.registrylong_notm}} 区域。映像和名称空间是资源的示例。
