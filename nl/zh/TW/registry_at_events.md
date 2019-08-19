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

追蹤使用者和應用程式如何與 {{site.data.keyword.cloud}} 中的 {{site.data.keyword.registrylong}} 服務互動。
{:shortdesc}

{{site.data.keyword.at_full_notm}} 服務或（僅針對現有使用者）{{site.data.keyword.cloudaccesstrailfull_notm}} 服務會記錄由使用者起始，且會變更 {{site.data.keyword.cloud_notm}} 中服務狀態的活動。如需相關資訊，請參閱 [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started)，或者（針對現有使用者）[{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)。

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
    <td>`container-registry.image.bulkdelete`</td>
	  <td>從 {{site.data.keyword.registrylong_notm}} 中刪除數個映像檔。</td>
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
    <td>`container-registry.image.rm`</td>
	  <td>從 {{site.data.keyword.registrylong_notm}} 中刪除一個以上的指定映像檔。</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>新增指示預先存在的 {{site.data.keyword.registrylong_notm}} 映像檔的標籤。</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>從 {{site.data.keyword.registrylong_notm}} 中的每個指令映像檔移除一個標籤或數個標籤。</td>
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
  </tr><tr>
    <td>`container-registry.retentionanalysis`</td>
	  <td>清除您的名稱空間，只保留符合準則的映像檔。請套用指定的準則，以在 {{site.data.keyword.registrylong_notm}} 中為名稱空間內的每個儲存庫保留映像檔。名稱空間中的所有其他映像檔都會刪除。</br> 取得要刪除的映像檔清單的要求是一個針對 `retentionanalysis` 事件類型的 `post` 動作。而刪除是針對 `images` 事件類型的單一 `bulkdelete` 動作，也是針對每個個別映像檔的 `delete` 動作。</td>
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

### {{site.data.keyword.at_full_notm}} 事件
{: #ui_atlogdna}

{{site.data.keyword.at_full_notm}} 事件在 {{site.data.keyword.at_full_notm}} **帳戶網域**中可用，該帳戶網域在產生事件的 {{site.data.keyword.cloud_notm}} 地區中可用（`ap-south` 除外）。`ap-south` 的事件顯示在 `Tokyo (jp-tok)` 中。

提供 {{site.data.keyword.registrylong_notm}} 或 Vulnerability Advisor 事件的[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)，會對應於提供資源的 {{site.data.keyword.registrylong_notm}}。資源的範例包括映像檔及名稱空間。

|帳戶登錄的地區|登錄的網域名稱|{{site.data.keyword.at_full_notm}} 事件的位置|
|:-----------------|:-----------------|:-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="表 2. {{site.data.keyword.at_full_notm}} 事件的位置" caption-side="top"}

|登錄|全球登錄|{{site.data.keyword.at_full_notm}} 事件的位置|
|:-----------------|:-----------------|:-----------------|
|全球| `icr.io` | `Dallas (us-south)` |
{: caption="表 3. 全球登錄 {{site.data.keyword.at_full_notm}} 事件的位置" caption-side="top"}

### {{site.data.keyword.cloudaccesstraillong_notm}} 事件
{: #ui_at}

{{site.data.keyword.cloudaccesstraillong_notm}} 事件（僅針對現有使用者）在 {{site.data.keyword.cloudaccesstraillong_notm}} **帳戶網域**中可用，該帳戶網域在產生事件的 {{site.data.keyword.cloud_notm}} 地區中可用（`ap-north` 除外）。`ap-north` 的事件會顯示於 `ap-south`。

淘汰使用 {{site.data.keyword.cloudaccesstrailfull_notm}}。從 2019 年 5 月 9 日開始，無法佈建新的 {{site.data.keyword.cloudaccesstrailshort}} 實例。現有的超值方案實例將支援到 2019 年 9 月 30 日為止。若要繼續監視 {{site.data.keyword.cloud_notm}} 帳戶的活動，請佈建 [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) 的實例。
{: deprecated}

提供 {{site.data.keyword.registrylong_notm}} 或 Vulnerability Advisor 事件的[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)，會對應於提供資源的 {{site.data.keyword.registrylong_notm}}。資源的範例包括映像檔及名稱空間。
