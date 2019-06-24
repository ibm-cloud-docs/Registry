---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-07"

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

請使用 {{site.data.keyword.cloudaccesstrailfull}} 服務，追蹤使用者和應用程式在 {{site.data.keyword.cloud}} 中與 {{site.data.keyword.registrylong}} 服務互動的情況。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服務會記錄由使用者起始，且會變更 {{site.data.keyword.cloud_notm}} 中服務狀態的活動。如需相關資訊，請參閱 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)。

下表列出呼叫時會產生事件的 API 方法：

<table>
  <caption>表 1. 產生事件的動作</caption>
  <tr>
    <th>動作</th>
	  <th>說明</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>建立 Vulnerability Advisor 豁免。</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>刪除 Vulnerability Advisor 豁免。</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>在 {{site.data.keyword.registrylong_notm}} 中建置 Docker 映像檔。</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>從 {{site.data.keyword.registrylong_notm}} 中刪除映像檔。</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>顯示映像檔的詳細資料。</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>列出 {{site.data.keyword.IBM_notm}} 帳戶中的映像檔。</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>從 {{site.data.keyword.registrylong_notm}} 取回映像檔。</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>將映像檔推送至 {{site.data.keyword.registrylong_notm}}。</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>新增參照既存 {{site.data.keyword.registrylong_notm}} 映像檔的標籤。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>新增名稱空間至 {{site.data.keyword.registrylong_notm}}。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>從 {{site.data.keyword.registrylong_notm}} 中刪除名稱空間。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>列出 {{site.data.keyword.IBM_notm}} 帳戶中的名稱空間。</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>顯示資料流量及儲存空間的現行配額，以及這些配額的用量資訊。</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>修改配額。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.create`</td>
	  <td>建立新的登錄記號。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>刪除登錄記號。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>擷取登錄記號的相關資訊。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>列出 {{site.data.keyword.IBM_notm}} 帳戶中的登錄記號。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>刪除多個登錄記號。</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>顯示現行定價方案的相關資訊。</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>升級為標準方案。</td>
  </tr>
 </table>

## 尋找事件的位置
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件位於 {{site.data.keyword.cloudaccesstrailshort}} **帳戶網域**，而此帳戶網域位於產生事件的 {{site.data.keyword.cloud_notm}} 地區（`ap-north` 除外）。`ap-north` 的事件會顯示於 `ap-south`。

提供 {{site.data.keyword.registrylong_notm}} 或 Vulnerability Advisor 事件的[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)，會對應於提供資源（例如映像檔或名稱空間）的 {{site.data.keyword.registrylong_notm}}。
