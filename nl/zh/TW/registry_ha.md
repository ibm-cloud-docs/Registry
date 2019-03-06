---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, high availability


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

# 高可用性及災難回復
{: #ha-dr}

{{site.data.keyword.registrylong}} 服務是高可用性的地區服務。
{:shortdesc}

* 在每個支援的地區中，資料流量會在多個可用性區域的登錄基礎架構之間進行負載平衡，沒有單一失敗點。

* 儲存在 {{site.data.keyword.registrylong_notm}} 中的資料會定期備份，提供額外的備援。

* 如果您擔心整個地區無法使用時的映像檔可用性，可以選擇將映像檔推送至多個地區登錄。
  
  您也可能選擇將映像檔推送至多個登錄，以防意外刪除或改寫映像檔。

  如需地區的相關資訊，請參閱[地區](/docs/services/Registry/registry_overview.html#registry_regions)。
