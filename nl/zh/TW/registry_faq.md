---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, Vulnerability Advisor,

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

# 常見問題 (FAQ)
{: #registry_faq}

{{site.data.keyword.registrylong}} 常見問題。
{: shortdesc}

## 如何列出公用映像檔？
{: #faq_list_public_images}
{: faq}

若要列出公用映像檔，請執行下列 `ibmcloud` 指令，設定目標全球登錄並列出 IBM 提供的公用映像檔：

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## 我可以使用非 Docker 工具來建置映像檔並將它們推送至登錄嗎？
{: #faq_tools}
{: faq}

可以，如果工具支援 OCI 映像檔格式和通訊協定的話。

## 如何使用存取控制與 IAM 搭配？
{: #faq_access_control}
{: faq}

您可以在 {{site.data.keyword.registrylong_notm}} 中建立 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) 原則來控制對名稱空間的存取。如需相關資訊，請參閱[指導教學：授與 {{site.data.keyword.registrylong_notm}} 資源存取權](/docs/services/Registry?topic=registry-iam_access)及[使用 Identity and Access Management 管理使用者存取](/docs/services/Registry?topic=registry-iam)。

## 哪些地區可用於 {{site.data.keyword.registrylong_notm}}？
{: #faq_regions}
{: faq}

您可以在[本端地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local)中管理映像檔。IBM 管理的公用映像檔則可在[全球登錄](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)中找到。

## 為什麼我會收到新增映像檔的找不到掃描錯誤訊息?
{: #faq_va_new_scan_error}
{: faq}

如果您在將映像檔新增至登錄後立即取得漏洞報告，可能會收到下列錯誤：

```
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

您收到此訊息是因為映像檔會以非同步方式掃描來要求結果，而掃描處理程序需要一些時間才完成。在正常作業期間，掃描會在您將映像檔新增至登錄後的前幾分鐘內完成，視映像檔大小及登錄收到的資料流量數量之類的變數而定。

如果您在建置管線期間收到此訊息，並且經常看到這個錯誤，請嘗試新增包含短暫暫停的某個重試邏輯。

如果您仍然看到無法接受的效能，請與支援中心聯絡，請參閱[取得 {{site.data.keyword.registrylong_notm}} 的協助和支援](/docs/services/Registry?topic=registry-ts_index#gettinghelp)。

## 如何觸發 Vulnerability Advisor 掃描？
{: #faq_va_trigger_scan}
{: faq}

您可以使用下列其中一種方式觸發映像檔的掃描：

- 如果將新的映像檔推送至登錄。
- 如果未掃描映像檔長達 7 天，映像檔會排入佇列等待重新掃描，這可能需要一些時間才能完成。
- 如果針對映像檔中安裝的套件發行新的安全注意事項，映像檔會排入佇列等待重新掃描，這可能需要一些時間才能完成。發行新的安全注意事項所觸發的重新掃描僅可用於 Ubuntu 及 Debian 映像檔。

## 安全注意事項的更新頻率為何？
{: #faq_va_update_security_notice}
{: faq}

Vulnerability Advisor 的安全注意事項大約每隔 12 個小時從供應商的作業系統網站載入一次。
