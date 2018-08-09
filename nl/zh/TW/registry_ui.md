---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 監視映像檔的漏洞
{: #registry_ui}

您可以使用 {{site.data.keyword.Bluemix_notm}} 主控台檢視潛在漏洞的相關資訊，以及 {{site.data.keyword.registrylong}} 公用與專用儲存庫中的映像檔安全。
{:shortdesc}

**安全報告**直欄向您顯示映像檔的下列相關資訊：
-   `安全`：未發現任何安全問題。
-   `有漏洞`：發現安全或配置問題，而且必須在部署映像檔之前予以解決。
-   `未完成`：掃描未完成。掃描可能仍在執行中，或是映像檔的作業系統可能不相容。請稍候，然後重試掃描。如果掃描仍未完成，請重新推送映像檔來啟動新的掃描。不會封鎖掃描未完成的映像檔進行部署。
-   `不受支援的 OS`：不支援映像檔中的作業系統。

若要檢視圖形使用者介面，請使用下列步驟：

1.  使用您的 IBM ID 登入 {{site.data.keyword.Bluemix_notm}} 主控台 ([https://console.bluemix.net](https://console.bluemix.net))。
2.  如果您有多個 {{site.data.keyword.Bluemix_notm}} 帳戶，請從帳戶功能表中選取要使用的帳戶及地區。
3.  按一下**型錄**。
4.  選取**容器**種類，然後按一下 **Container Registry** 磚。
5.  若要檢視專用儲存庫中的映像檔相關資訊，請按一下**專用儲存庫**。即會顯示專用儲存庫中的映像檔清單，以及每一個映像檔的安全報告狀態。若要找出潛在漏洞的相關資訊（包括標籤及映像檔摘要），請按一下表格中的列。
6.  若要檢視公用儲存庫中的映像檔相關資訊，請按一下**公用儲存庫**。即會顯示公用儲存庫中的映像檔清單，其列出連接至每一個映像檔的文件及安全報告的鏈結。若要找出潛在漏洞的相關資訊（包括標籤及映像檔摘要），請按一下表格中的列。

若要找出安全報告中資訊所代表的相關內涵，請參閱[使用漏洞警告器管理映像檔安全](../va/va_index.html)。
