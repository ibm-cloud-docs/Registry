---

copyright:
  years: 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# 版本注意事項
{: #registry_release_notes}

瞭解 {{site.data.keyword.registrylong}} 和 Vulnerability Advisor 的最新變更。這些變更是依日期分組。
{:shortdesc}

## 2019 年 8 月 1 日
{: #01aug2019}

<dl>
  <dt>`ibmcloud cr retention-run` 指令可用</dt>
  <dd>`ibmcloud cr retention-run` 指令會藉由套用指定的準則，在 {{site.data.keyword.registrylong_notm}} 中為名稱空間內的每個儲存庫保留映像檔，而清理名稱空間。名稱空間中的所有其他映像檔都會刪除。

  
  如需相關資訊，請參閱 [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) 和[保留映像檔](/docs/services/Registry?topic=registry-registry_retention)。</dd>
</dl>

## 2019 年 7 月 25 日
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.at_full_notm}} 適用於 {{site.data.keyword.registrylong_notm}}</dt>
  <dd>請使用 {{site.data.keyword.at_full_notm}} 服務，追蹤使用者和應用程式在 {{site.data.keyword.cloud}} 中與 {{site.data.keyword.registrylong_notm}} 服務互動的情況。


  如需相關資訊，請參閱 [Activity Tracker 事件](/docs/services/Registry?topic=registry-at_events#at_events)。</dd>
</dl>

## 2019 年 7 月 1 日
{: #1jul2019}

<dl>
  <dt>`ibmcloud cr token-add` 指令不再可用</dt>
  <dd>`ibmcloud cr token-add` 指令已停止使用。您無法再從 CLI 或 API 新增登錄記號。</dd>
</dl>

## 2019 年 6 月 27 日
{: #27jun2019}

<dl>
  <dt>容器掃描器不再可用</dt>
  <dd>容器掃描器已停止使用。Vulnerability Advisor 仍將掃描推送到 {{site.data.keyword.registrylong_notm}} 的映像檔。</dd>
</dl>

## 2019 年 6 月 13 日
{: #13jun2019}

<dl>
  <dt>從映像檔移除標籤</dt>
  <dd>從 {{site.data.keyword.registrylong_notm}} 中的每個指令映像檔移除一個標籤或數個標籤。

  若要從映像檔移除一個或數個標籤，而讓基礎映像檔及任何其他標籤保留原樣，請使用 [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) 指令。如果您想要刪除基礎映像檔及其所有標籤，請改用 [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) 指令。


  如需相關資訊，請參閱[從專用 {{site.data.keyword.cloud_notm}} 儲存庫中的映像檔移除標籤](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag)。</dd>
</dl>

## 2019 年 5 月 13 日
{: #13may2019}

<dl>
  <dt>終止對容器掃描器的支援</dt>
  <dd>「容器掃描器」現已淘汰，再也無法使用。

  如需相關資訊，請參閱[安裝容器掃描器（已淘汰）](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)。</dd>
</dl>

## 2019 年 4 月 2 日
{: #2apr2019}

<dl>
  <dt>Container Image Security Enforcement 的通用版</dt>
  <dd>請先使用 Container Image Security Enforcement 來驗證容器映像檔，再將它們部署到 {{site.data.keyword.containerlong_notm}} 中的叢集。您可以控制從何處部署映像檔、強制執行 Vulnerability Advisor 原則，以及確定[內容信任](/docs/services/Registry?topic=registry-registry_trustedcontent)已適當地套用至映像檔。

  如需相關資訊，請參閱[強制執行容器映像檔安全](/docs/services/Registry?topic=registry-security_enforce#security_enforce)。</dd>
</dl>

## 2019 年 3 月 14 日
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} 適用於 {{site.data.keyword.registrylong_notm}}</dt>
  <dd>請使用 {{site.data.keyword.cloudaccesstraillong_notm}} 服務，追蹤使用者和應用程式在 {{site.data.keyword.cloud}} 中與 {{site.data.keyword.registrylong_notm}} 服務互動的情況。


  如需相關資訊，請參閱 [Activity Tracker 事件](/docs/services/Registry?topic=registry-at_events#at_events)。
</dd>
</dl>

## 2019 年 2 月 25 日
{: #25feb2019}

<dl>
  <dt>新網域名稱</dt>
  <dd>{{site.data.keyword.registrylong_notm}} 採用新的網域名稱。新的網域名稱提供於主控台及 CLI 中。您現在可以使用新的 `icr.io` 網域名稱。淘汰使用現有的 `registry.bluemix.net` 網域名稱，但可以繼續使用到支援日期結束為止。
支援結束日期尚未確定。如需相關資訊，請參閱[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)及[簡介新的 IBM Cloud Container Registry 網域名稱 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names)。

  簽章套用於整個映像檔名稱，也包含網域名稱。如果使用內容信任，您必須新增簽章，以便您可以在新網域名稱下使用內容信任。如需簽署映像檔的相關資訊，請參閱[簽署受信任內容的映像檔](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)。</dd>
</dl>

<dl>
  <dt>{{site.data.keyword.containerlong_notm}} 叢集的 IAM API 金鑰取回密碼</dt>
  <dd>使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) API 金鑰授予 `icr.io` 網域的新的叢集映像檔取回密碼。因此，如果您想要進一步控制對 {{site.data.keyword.registrylong_notm}} 資源的存取權，您可以新增 IAM 原則。例如，您可以變更叢集取回密碼中的 API 金鑰原則，以便只從特定登錄地區或名稱空間取回映像檔。
  
  如需相關資訊，請參閱[瞭解如何授權叢集以從 {{site.data.keyword.registrylong_notm}} 取回映像檔](/docs/containers?topic=containers-images#cluster_registry_auth)。</dd>
</dl>

<dl>
  <dt>亞太地區北部的新地區</dt>
  <dd>`ap-north` 中提供新地區。您可以使用網域名稱 `jp.icr.io` 來使用新地區。
  
  如需相關資訊，請參閱[地區](/docs/services/Registry?topic=registry-registry_overview#registry_regions)。</dd>
</dl>

## 2019 年 2 月 21 日 
{: #21feb2019}

<dl>
  <dt>實現對名稱空間的自動存取</dt>
  <dd>使用記號，以自動化將 Docker 映像檔推送至名稱空間以及從名稱空間取回 Docker 映像檔的作法已經淘汰。您現在必須使用 API 金鑰，才能自動化 {{site.data.keyword.registrylong_notm}} 名稱空間的存取，以推送及取回映像檔。

  如需相關資訊，請參閱[使用 API 金鑰自動化名稱空間的存取](/docs/services/Registry?topic=registry-registry_access#registry_api_key)。</dd>
</dl>

## 2019 年 1 月 8 日
{: #8jan2019}

 <dl>
  <dt>終止對 Vulnerability Advisor API 第 2 版的支援</dt>
  <dd>Vulnerability Advisor API 第 2 版已淘汰，再也無法使用。請使用第 3 版 API。如需相關資訊，請參閱 [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/container-registry/va)。

  如需相關資訊，請參閱 [Vulnerability Advisor 第 2 版 API 淘汰 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/)。</dd>
</dl>

## 2018 年 10 月 4 日
{: #4oct2018}

<dl>
  <dt>管理使用者存取權</dt>
  <dd>請使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM)，控制您帳戶中使用者對 {{site.data.keyword.registrylong_notm}} 的存取權。如果在 {{site.data.keyword.registrylong_notm}} 中為帳戶已啟用了 IAM 原則，則必須使用定義的 IAM 使用者角色，為帳戶中存取服務的每個使用者指派存取原則。該原則決定使用者在服務環境定義內所具有的角色，以及使用者可執行的動作。

  如需相關資訊，請參閱[使用 {{site.data.keyword.iamshort}} 管理使用者存取](/docs/services/Registry?topic=registry-iam#iam)、[定義使用者存取角色原則](/docs/services/Registry?topic=registry-user#user)，以及[指導教學：授與對 IBM Cloud Container Registry 資源的存取權](/docs/services/Registry?topic=registry-iam_access#iam_access)。</dd>
</dl>

## 2018 年 8 月 7 日
{: #7aug2018}

<dl>
  <dt>Vulnerability Advisor 中可用的豁免原則</dt>
  <dd>如果您想要管理 {{site.data.keyword.cloud_notm}} 組織的安全，則可以使用您的原則設定，來判定是否豁免某個問題。您可以使用 Container Image Security Enforcement，確保在考慮原則所免除的任何問題後，只容許來自不包含任何安全問題的映像檔的部署。


  如需相關資訊，請參閱[設定組織豁免原則](/docs/services/Registry?topic=va-va_index#va_managing_policy)。</dd>
</dl>

## 2018 年 7 月 25 日
{: #25jul2018}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} 適用於 Vulnerability Advisor</dt>
  <dd>請使用 {{site.data.keyword.cloudaccesstrailfull_notm}} 服務，追蹤使用者和應用程式在 {{site.data.keyword.cloud}} 中與 {{site.data.keyword.registrylong_notm}} 服務互動的情況。


  如需相關資訊，請參閱 [Activity Tracker 事件](/docs/services/Registry?topic=registry-at_events#at_events)。</dd>
</dl>
  
## 2018 年 7 月 12 日
{: #12jul2018}

<dl>
  <dt>Vulnerability Advisor API 第 3 版</dt>
  <dd>第 3 版 API 會變更用來列出豁免之 API 端點的行為。您必須確認您對 API 的使用不會依賴第 2 版的行為。

  如需相關資訊，請參閱 [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![如需相關資訊](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/container-registry/va)。</dd>
</dl>

## 2018 年 5 月 31 日
{: #31may2018}

<dl>
  <dt>使用 Helm for Passport Advantage 映像檔</dt>
  <dd>將從 [IBM Passport Advantage Online for customers ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/software/passportadvantage/pao_customer.html) 下載並包裝以與 Helm 搭配使用的 {{site.data.keyword.IBM_notm}} 軟體，匯入到您的 {{site.data.keyword.registrylong_notm}} 名稱空間。

  如需相關資訊，請參閱 [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load)。</dd>
</dl>

## 2018 年 3 月 21 日
{: #21mar2018}

<dl>
  <dt>容器掃描器</dt>
  <dd>容器掃描器讓 Vulnerability Advisor 能回報執行中容器裡，所發現且不存在於容器基礎映像檔的任何問題。

  如需相關資訊，請參閱[安裝容器掃描器](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)。</dd>
</dl>

## 2018 年 3 月 16 日
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement 測試版</dt>
  <dd>請先使用 Container Image Security Enforcement 測試版來驗證容器映像檔，再將它們部署到 {{site.data.keyword.containerlong_notm}} 中的叢集。您可以控制從何處部署映像檔、強制執行 Vulnerability Advisor 原則，以及確定[內容信任](/docs/services/Registry?topic=registry-registry_trustedcontent)已適當地套用至映像檔。

  如需相關資訊，請參閱[強制執行容器映像檔安全](/docs/services/Registry?topic=registry-security_enforce#security_enforce)。</dd>
</dl>

## 2018 年 2 月 20 日
{: #20feb2018}

<dl>
  <dt>授信任內容</dt>
  <dd>{{site.data.keyword.registrylong_notm}} 提供受信任內容技術，讓您可以簽署映像檔，以確保登錄名稱空間中之映像檔的完整性。透過取回及推送已簽署的映像檔，您可以驗證映像檔已由正確的參與方推送，例如您的持續整合 (CI) 工具。

  如需相關資訊，請參閱[簽署受信任內容的映像檔](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)。</dd>
</dl>

## 2017 年 11 月 6 日
{: #6nov2017}

<dl>
  <dt>全球登錄</dt>
  <dd>可以使用全球登錄。在其網域名稱中不包含任何地區 (`icr.io`)。此登錄中僅管理 IBM 提供的公用映像檔。

  如需相關資訊，請參閱[全球登錄](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)。</dd>
</dl>

## 2017 年 9 月 29 日
{: #29sep2017}

<dl>
  <dt>建置 Docker 映像檔</dt>
  <dd>`ibmcloud cr build` 指令現在可用於執行容器建置。您可以直接在 {{site.data.keyword.cloud_notm}} 建置 Docker 映像檔，或在本端電腦上建立自己的 Docker 映像檔，並將它上傳（推送）至 {{site.data.keyword.registrylong_notm}} 中的名稱空間。


  如需相關資訊，請參閱[建置 Docker 映像檔以與名稱空間搭配使用](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating)，以及 [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build)。</dd>
</dl>

## 2017 年 8 月 24 日
{: #24aug2017}

<dl>
  <dt>發佈的圖形使用者介面</dt>
  <dd>{{site.data.keyword.registrylong_notm}} 圖形使用者介面在型錄中提供，請參閱[容器登錄
![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/kubernetes/catalog/registry)。</dd>
</dl>

## 2017 年 6 月 27 日
{: #27jun2017}

<dl>
  <dt>{{site.data.keyword.registrylong_notm}} 的通用版</dt>
  <dd>已正式發行 {{site.data.keyword.registrylong_notm}} 作為 {{site.data.keyword.cloud_notm}} 中的服務。{{site.data.keyword.registrylong_notm}} 支援 {{site.data.keyword.containerlong_notm}}。

  如需 {{site.data.keyword.containerlong_notm}} 的相關資訊，請參閱[入門指導教學](/docs/containers?topic=containers-getting-started)。</dd>
</dl>
