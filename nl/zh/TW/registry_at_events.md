---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

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

請使用 {{site.data.keyword.cloudaccesstrailfull}} 服務，追蹤使用者和應用程式在 {{site.data.keyword.Bluemix}} 中與 {{site.data.keyword.registrylong}} 服務互動的情況。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服務會記錄由使用者起始，且會變更 {{site.data.keyword.Bluemix_notm}} 中服務狀態的活動。如需相關資訊，請參閱 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)。

下表列出呼叫時會產生事件的 API 方法：

<table>
  <caption>表 1. 產生事件的動作</caption>
  <tr>
    <th>動作</th>
	  <th>說明</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>建立漏洞警告器豁免。</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>刪除漏洞警告器豁免。</td>
  </tr>
 </table>

## 尋找事件的位置
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件位於 {{site.data.keyword.cloudaccesstrailshort}} **帳戶網域** 中，而此帳戶網域位於產生事件的 {{site.data.keyword.Bluemix_notm}} 地區中。

提供「漏洞警告器」事件的[地區](/docs/services/Registry/registry_overview.html#registry_regions)，對應於提供資源（例如映像檔或名稱空間）的 {{site.data.keyword.registrylong_notm}} 地區。
