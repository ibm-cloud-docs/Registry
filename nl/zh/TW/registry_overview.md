---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-27"

keywords: IBM Cloud Container Registry, private Docker images, scalable private image registry, regions, plans, billing, registry

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

# 關於 {{site.data.keyword.registrylong_notm}}
{: #registry_overview}

使用 {{site.data.keyword.registrylong}}，在高可用性且可擴充的架構中，儲存及存取專用 Docker 映像檔。
{:shortdesc}

{{site.data.keyword.registrylong_notm}} 提供 {{site.data.keyword.IBM_notm}} 所管理的多方承租戶、高可用性且可擴充的專用映像檔登錄。您可以藉由設定自己的映像檔名稱空間，並將 Docker 映像檔推送至名稱空間，來使用 {{site.data.keyword.registrylong_notm}}。

<img src="images/registry_architecture1.svg" alt="顯示如何與 IBM Cloud Container Registry 互動的影像。Container Registry 同時包含專用及公用儲存庫，以及用來與服務互動的 API。您的本端 Docker 用戶端可以從登錄中的專用儲存庫取回映像檔以及將映像檔推送至其中，也可以取回公用儲存庫。IBM Cloud Web 使用者介面（主控台）可與 Container Registry API 互動，以列出映像檔。Container Registry CLI 可與 API 互動，以列出、建立、檢查及移除映像檔，以及其他管理功能。您的本端 Docker 用戶端也可以從本端映像檔儲存庫中取回映像檔，並將其推送至其他登錄。"/>

**圖 1. {{site.data.keyword.registrylong_notm}} 如何與您的 Docker 映像檔互動**

Docker 映像檔是每個您建立之容器的基準。映像檔是從 Dockerfile 建立，而 Dockerfile 是包含映像檔建置指示的檔案。Dockerfile 可能會在其指示中參照個別儲存的建置構件，例如應用程式、應用程式的配置，以及其相依關係。映像檔一般儲存在登錄中，而登錄可供公開存取（公用登錄）或設定一小群使用者的有限存取（專用登錄）。使用 {{site.data.keyword.registrylong_notm}} 時，只有具有 {{site.data.keyword.Bluemix_notm}} 帳戶存取權的使用者才能存取映像檔。

將映像檔推送至 {{site.data.keyword.registrylong_notm}} 時，您可以受益於內建的「漏洞警告器」特性，它們會掃描潛在的安全問題及漏洞。「漏洞警告器」會檢查特定 Docker 基礎映像檔以尋找有漏洞的套件，以及應用程式配置設定中的已知漏洞。發現漏洞時，會提供漏洞的相關資訊。您可以使用此資訊來解決安全問題，以避免從有漏洞的映像檔部署容器。

請檢閱下表，以查看使用 {{site.data.keyword.registrylong_notm}} 的好處概觀。

|好處|說明|
|-------|-----------|
|高可用性且可擴充的專用登錄|<ul><li>在 {{site.data.keyword.IBM_notm}} 所管理的多方承租戶、高可用性且可擴充的專用登錄中，設定自己的映像檔名稱空間。</li><li>儲存專用 Docker 映像檔，並將它們與 {{site.data.keyword.Bluemix_notm}} 帳戶中的使用者共用。</li></ul>|
|漏洞警告器的映像檔安全規範|<ul><li>受益於自動掃描名稱空間中的映像檔。</li><li>檢閱作業系統特有的建議，以修正潛在漏洞，並保護容器免於洩漏。</li></ul>|
|儲存空間及取回資料流量的配額限制|<ul><li>受益於專用映像檔的免費儲存空間及取回資料流量，直到達到免費配額為止。</li><li>設定每個月的儲存空間量及取回資料流量的自訂配額限制，以避免超出偏好的付費等級。</li></ul>|
{: caption="表 1. {{site.data.keyword.registrylong_notm}} 的好處" caption-side="top"}

## 服務方案
{: #registry_plans}

您可以選擇免費或標準 {{site.data.keyword.registrylong_notm}} 服務方案來儲存 Docker 映像檔，並讓 {{site.data.keyword.Bluemix_notm}} 帳戶中的使用者可使用這些映像檔。
{:shortdesc}

{{site.data.keyword.registrylong_notm}} 服務方案會決定可用於專用映像檔的儲存空間量及取回資料流量。服務方案與 {{site.data.keyword.Bluemix_notm}} 帳戶相關聯，而且儲存空間及映像檔取回資料流量的限制適用於帳戶中設定的所有名稱空間。

下表顯示可用的 {{site.data.keyword.registrylong_notm}} 服務方案及其特徵。如需計費運作方式以及您超出服務方案限制時會發生什麼情況的相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} 中的配額限制及計費](#registry_plan_billing)。

|特徵|免費|標準|
|---------------|----|--------|
|說明|試用 {{site.data.keyword.registrylong_notm}}，以儲存及共用 Docker 映像檔。當您在 {{site.data.keyword.registrylong_notm}} 中設定第一個名稱空間時，此方案是預設服務方案。|受益於無限制的儲存空間及取回資料流量用量，以管理 {{site.data.keyword.Bluemix_notm}} 帳戶中所有名稱空間的 Docker 映像檔。|
|映像檔的儲存空間量|500 MB|無限制|
|取回資料流量|每個月 5 GB|無限制|
|計費|如果您超出儲存空間或取回資料流量限制，便無法將映像檔推送至名稱空間或從中取回映像檔。如需相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} 中的配額限制及計費](#registry_plan_billing)。|<ul><li>儲存空間：會依使用的 GB-月向您收費。前 0.5 GB-月免費。之後，會依定價計算機中所述向您收費。</li><li>取回資料流量：會依每個月使用的 GB 量向您收費。前 5 GB 免費。之後，會依定價計算機中所述向您收費。如果您超出儲存空間或取回資料流量限制，便無法將映像檔推送至名稱空間或從中取回映像檔。如需儲存空間、取回資料流量及定價計算機的相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} 中的配額限制及計費](#registry_plan_billing)。</li></ul>|
{: caption="表 2. {{site.data.keyword.registrylong_notm}} 方案" caption-side="top"}

## 配額限制及計費
{: #registry_plan_billing}

尋找計費處理程序及配額限制在 {{site.data.keyword.registrylong_notm}} 中如何運作的資訊及範例。
{:shortdesc}

每個映像檔都是從數層建置而來，每一層都代表從基礎映像檔算起的漸進式變更。當您推送或取回映像檔時，會將每一層所需的儲存空間量及取回資料流量加到您的每月用量。相同的層會在 {{site.data.keyword.Bluemix_notm}} 帳戶中的映像檔之間自動共用，而且可以在建立其他映像檔時重複使用。每一個相同層的儲存空間都只收費一次，不論帳戶中有多少映像檔參照該層。

推送映像檔的範例：

> 您將映像檔推送至以 Ubuntu 映像檔為其礎的名稱空間。Ubuntu 映像檔包含數層。因為您的帳戶中還沒有這些層，所以會將這些層所需的儲存空間量加到您的每月用量。
>
> 後來，您建立了第二個以 Ubuntu 映像檔為其礎的映像檔。您變更 Ubuntu 基礎映像檔，例如，藉由將其他指令或檔案新增至 Dockerfile 來變更。每一個變更都代表新的映像檔層。當您推送第二個映像檔時，{{site.data.keyword.registrylong_notm}} 會認出基礎 Ubuntu 映像檔的所有層都已儲存在帳戶中。第二次儲存這些層時不會向您收費，即使您已將映像檔推送至另一個名稱空間。{{site.data.keyword.registrylong_notm}} 會判斷所有新層的大小，並將儲存空間量加到您的每月用量。

### 儲存空間及取回資料流量的計費
{: #registry_billing_traffic}

取決於選擇的服務方案而定，會根據每個月使用的儲存空間及取回資料流量向您收費。
{:shortdesc}

**儲存空間：**

  每個 {{site.data.keyword.registrylong_notm}} 服務方案都有一定的儲存空間量，可用來將 Docker 映像檔儲存在 {{site.data.keyword.Bluemix_notm}} 帳戶的名稱空間中。如果您使用標準方案，則會依使用的 GB-月向您收費。前 0.5 GB-月免費。如果您使用免費方案，則在達到免費方案的配額限制之前，可以將映像檔免費儲存在 {{site.data.keyword.registrylong_notm}} 中。GB-月是指一個月（730 小時）平均 1 GB 儲存空間。

  標準方案的範例：

  > 您正好半個月使用 5 GB，然後將數個映像檔推送至名稱空間，並在剩下的半個月使用 10 GB。您的每月用量計算如下：
  >
  > (5 GB x 0.5（月）) + (10 GB x 0.5（月）) = 2.5 + 5 = 7.5 GB-月
  >
  > 在標準方案中，前 0.5 GB-月免費，因此會向您收取 7 GB-月（7.5 GB-月 - 0.5 GB-月）的費用。

  

**取回資料流量：**

  每個 {{site.data.keyword.registrylong_notm}} 服務方案都包括特定數量的專用映像檔（儲存在名稱空間中）免費取回資料流量。取回資料流量是您在將映像檔層從名稱空間取回至本端機器時使用的頻寬。如果您使用標準方案，則會依每個月使用的 GB 量向您收費。每個月的前 5 GB 免費。如果您使用免費方案，則在達到免費方案的配額限制之前，可以從名稱空間取回映像檔。

  標準方案的範例：

  > 在該月，您已取回包含大小總計 14 GB 之層的映像檔。您的每月用量計算如下：
  >
  > 在標準方案中，每個月的前 5 GB 免費，因此會向您收取 9 GB (14 GB - 5 GB) 的費用。

  

### 儲存空間及取回資料流量的配額限制
{: #registry_quota_limits}

視選擇的服務方案而定，您可以在達到方案特定或自訂配額限制之前，將映像檔推送至名稱空間以及從中取回映像檔。
{:shortdesc}

**儲存空間：**

  達到或超出方案的配額限制時，在從名稱空間[移除映像檔來釋放空間](/docs/services/Registry?topic=registry-registry_quota#registry_quota_freeup)或[升級至標準方案](#registry_plan_upgrade)之前，您無法將任何映像檔推送至 {{site.data.keyword.Bluemix_notm}} 帳戶中的名稱空間。如果您設定了免費或標準方案中的儲存空間配額限制，您也可以[增加此配額限制](/docs/services/Registry?topic=registry-registry_quota#registry_quota_set)，以重新啟用新映像檔的推送。

  標準方案的範例：

  > 您的現行儲存空間配額限制設為 1 GB。{{site.data.keyword.Bluemix_notm}} 帳戶的名稱空間中所儲存的所有專用映像檔，已使用這個儲存空間中的 900 MB。在達到配額限制之前，您有 100 MB 的儲存空間可用。有一位使用者想要在本端機器上推送大小為 2 GB 的映像檔。因為尚未達到配額限制，所以 {{site.data.keyword.registrylong_notm}} 容許使用者推送此映像檔。
  >
  > 推送之後，{{site.data.keyword.registrylong_notm}} 會判斷名稱空間中映像檔的實際大小（這可能會與本端機器上的大小不同），並檢查是否達到儲存空間的限制。在此範例中，儲存空間用量會從 900 MB 增加 2 GB。在現行配額限制設為 1 GB 的情況下，{{site.data.keyword.registrylong_notm}} 會阻止您將其他映像檔推送至名稱空間。

**取回資料流量：**

  達到或超出方案的配額限制時，在等待下一個計費期間開始、[升級至標準方案](#registry_plan_upgrade)或[增加取回資料流量的配額限制](/docs/services/Registry?topic=registry-registry_quota#registry_quota_set)之前，您無法從 {{site.data.keyword.Bluemix_notm}} 帳戶中的名稱空間取回任何映像檔。

  標準方案的範例：

  > 在該月，取回資料流量的配額限制設為 5 GB。您已從名稱空間取回映像檔，並已使用這個取回資料流量中的 4.5 GB。在達到配額限制之前，您有 0.5 GB 的取回資料流量可用。一位使用者想要從名稱空間取回大小為 1 GB 的映像檔。因為尚未達到配額限制，所以 {{site.data.keyword.registrylong_notm}} 容許使用者取回此映像檔。
  >
  > 取回映像檔之後，{{site.data.keyword.registrylong_notm}} 會判斷您在取回期間已使用的頻寬，並檢查是否已達到取回資料流量的限制。在此範例中，取回資料流量用量會從 4.5 GB 增加到 5.5 GB。在現行配額限制設為 5 GB 的情況下，{{site.data.keyword.registrylong_notm}} 會阻止您從名稱空間取回映像檔。

### 預估成本
{: #registry_estimating_costs}

使用 {{site.data.keyword.Bluemix_notm}} 定價計算機來預估方案的成本。
{:shortdesc}

您可以使用 {{site.data.keyword.Bluemix_notm}} 提供的成本計算機來為應用程式定價。

1. 開啟定價單，請參閱 [{{site.data.keyword.Bluemix_notm}} 定價 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/pricing)。
2. 在**隨收隨付制**區段中，按一下**使用計算機預估成本**。即會開啟計算機。
3. 在**容器費用**區段中，捲動至 **Container Registry** 區段。
4. 在提供的欄位中，輸入您的儲存空間及資料流量預估值。

您的預估成本即會顯示在計算機中。

## 升級服務方案
{: #registry_plan_upgrade}

您可以升級服務方案，受益於無限制的儲存空間及取回資料流量用量，以管理 {{site.data.keyword.Bluemix_notm}} 帳戶中所有名稱空間的 Docker 映像檔。
{:shortdesc}

如果您要找出您所擁有的服務方案，請執行 `ibmcloud cr plan` 指令。

1. 登入 {{site.data.keyword.Bluemix_notm}}。

   ```
   ibmcloud login
   ```
   {: pre}

   如果您有聯合 ID，請使用 `ibmcloud login --sso` 登入 {{site.data.keyword.Bluemix_notm}} CLI。請輸入您的使用者名稱，並使用 CLI 輸出中提供的 URL，來擷取一次性密碼。若未使用 `--sso` 時登入失敗，而有使用 `--sso` 選項時登入成功，即表示您有聯合 ID。
    {:tip}

2. 升級為標準方案。

   ```
   ibmcloud cr plan-upgrade standard
   ```
   {: pre}

   如果您有 {{site.data.keyword.Bluemix_notm}} 精簡帳戶，則必須先升級至 {{site.data.keyword.Bluemix_notm}} 隨收隨付制或訂閱帳戶，然後才執行 `ibmcloud cr plan-upgrade`。
    {:tip}

## 學習基本觀念
{: #registry_planning}

學習登錄基本觀念，以準備好使用 {{site.data.keyword.registrylong_notm}} 來儲存及共用 Docker 映像檔。
{:shortdesc}

請不要將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。
{:tip}

### 瞭解 {{site.data.keyword.registrylong_notm}} 中使用的術語
{: #terms}

<dl>
  <dt>Dockerfile</dt>
  <dd>Dockerfile 是包含 Docker 映像檔建置指示的文字檔。映像檔通常建置在基礎映像檔之上，而基礎映像檔中包含基礎作業系統，例如 Ubuntu。您可以利用 Dockerfile 指示漸進式地變更基礎映像檔，以定義應用程式執行所需的環境。基礎映像檔的每項變更都會說明新的一層映像檔，您可以在單一 Dockerfile 行中進行多項變更。Dockerfile 中的指示也可能參照個別儲存的建置構件，例如應用程式、應用程式的配置，以及其相依關係。</dd>
</dl>

<dl>
  <dt>映像檔 (Image)</dt>
  <dd>容器運行環境內用來建立容器的檔案系統及其執行參數。檔案系統包含一系列已建立的層（在執行時結合），這些層是隨著連續更新建置映像檔而建立。在容器執行時，映像檔不會保留狀態。</dd>
</dl>

<dl>
  <dt>名稱空間 (Namespace)</dt>
  <dd>名稱空間是在 {{site.data.keyword.registrylong_notm}} 內組織映像檔儲存庫的一種方式。名稱空間與 {{site.data.keyword.Bluemix_notm}} 帳戶相關聯。當您在 {{site.data.keyword.registrylong_notm}} 中設定自己的名稱空間時，會將名稱空間附加至登錄 URL，如下所示：<code><em>&lt;region&gt;</em>.icr.io/my_namespace</code>。

  您 {{site.data.keyword.Bluemix_notm}} 帳戶中的每個使用者都可以檢視及使用登錄名稱空間中所儲存的映像檔。例如，您可以設定多個名稱空間，讓正式作業及編譯打包環境具有不同的儲存庫。</dd>
</dl>

<dl>
  <dt>OCI 容器映像檔 (OCI container images)</dt>
  <dd>遵登 [OCI 映像檔格式規格 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/opencontainers/image-spec) 的容器映像檔。</dd>
</dl>

<dl>
  <dt>登錄 (Registry)</dt>
  <dd>登錄是為 OCI 映像檔（也稱為 Docker 映像檔）提供儲存空間的服務。OCI 映像檔可以由使用適當登錄網域名稱的 OCI 用戶端存取或「取回」。映像檔可以由任何人存取（公用映像檔），或是可以將存取權限制為一個群組（專用映像檔）。{{site.data.keyword.registrylong_notm}} 提供 {{site.data.keyword.IBM_notm}} 所管理的多方承租戶、高可用性的專用映像檔登錄。您可以藉由將帳戶專用的名稱空間新增至您的帳戶，然後推送映像檔至名稱空間，來使用登錄。</dd>
</dl>

<dl>
  <dt>儲存庫 (Repository)</dt>
  <dd>映像檔儲存庫是登錄中已標記且相關之映像檔的集合。儲存庫經常與映像檔互換使用，但儲存庫可能會存放映像檔的多個已標記變式。</dd>
</dl>

<dl>
  <dt>標籤 (Tag)</dt>
  <dd>標籤是儲存庫內映像檔的 ID。您可以使用標籤來識別儲存庫內相同基礎映像檔的不同版本。當您執行 Docker 指令但未指定儲存庫映像檔的標籤時，依預設會使用以 <code>latest</code> 標記的映像檔。</dd>
</dl>

若要進一步瞭解 Docker 特有術語，[請參閱 Docker 名詞解釋 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.docker.com/glossary/)。

### 規劃名稱空間
{: #registry_namespaces}

{{site.data.keyword.registrylong_notm}} 提供 IBM 所管理的多方承租戶專用映像檔登錄。您可以藉由設定登錄名稱空間，以在此登錄中儲存及共用 Docker 映像檔。
{:shortdesc}

例如，您可以設定多個名稱空間，讓正式作業及編譯打包環境具有不同的儲存庫。如果您要將登錄用於多個 {{site.data.keyword.Bluemix_notm}} 地區，則必須設定每一個地區的名稱空間。名稱空間名稱在地區內是唯一的。您可以針對每一個地區使用相同的名稱空間名稱，除非他人已在該地區中設定了具有該名稱的名稱空間。

您可以使用 IAM 原則來控制名稱空間的存取。如需相關資訊，請參閱[定義使用者存取角色原則](/docs/services/Registry?topic=registry-user#user)。

若只要使用 IBM 提供的公用映像檔，您不需要設定名稱空間。

如果您不確定是否已為您的帳戶設定名稱空間，請執行 `ibmcloud cr namespace-list` 指令來擷取現有名稱空間資訊。
{:tip}

當您選擇名稱空間時，請考量下列規則：

- 在 {{site.data.keyword.Bluemix_notm}} 地區中，名稱空間必須是唯一的。
- 名稱空間的長度必須是 4 - 30 個字元。
- 名稱空間的開頭必須至少使用一個字母或數字。
- 名稱空間只能包含小寫字母、數字或底線 (_)。

請不要將個人資訊放在名稱空間名稱中。
{:tip}

在設定第一個名稱空間之後，您會獲指派免費 {{site.data.keyword.registrylong_notm}} 服務方案（如果您尚未[升級方案](#registry_plan_upgrade)的話）。

## 地區
{: #registry_regions}

{{site.data.keyword.registrylong_notm}} 登錄可在數個地區中使用。
{:shortdesc}

### 本端地區
{: #registry_regions_local}

本端地區是專用端點存取的地理區域。地區的 {{site.data.keyword.registrylong_notm}} 網域名稱已變更。新的網域名稱提供於主控台及 CLI 中。

下表顯示網域名稱。

|本端登錄地區|新的網域名稱|已淘汰的網域名稱|
|-----|----|-----------|
| `ap-north` | `jp.icr.io` |不適用|
| `ap-south` | `au.icr.io` | `registry.au-syd.bluemix.net` |
| `eu-central` | `de.icr.io` | `registry.eu-de.bluemix.net` |
| `uk-south` | `uk.icr.io` | `registry.eu-gb.bluemix.net` |
| `us-south` | `us.icr.io` | `registry.ng.bluemix.net` |
{: caption="表 3. 本端地區的網域名稱。" caption-side="top"}

現有的 `bluemix.net` 網域名稱已淘汰，但您目前可以繼續使用它們，以後將會公布支援結束日期。
{: deprecated}

**漏洞警告器網域名稱**

地區的漏洞警告器網域名稱已變更。新的網域名稱提供於主控台及 CLI 中。

下表顯示新的網域名稱。

|本端漏洞警告器地區|新的網域名稱|已淘汰的網域名稱|
|-----|----|-----------|
| `ap-north` | `jp.icr.io/va` |不適用|
| `ap-south` | `au.icr.io/va` | `va.au-syd.bluemix.net` |
| `eu-central` | `de.icr.io/va` | `va.eu-de.bluemix.net` |
| `uk-south` | `uk.icr.io/va` | `va.eu-gb.bluemix.net` |
| `us-south` | `us.icr.io/va` | `va.ng.bluemix.net` |
{: caption="表 4. 本端地區的網域名稱。" caption-side="top"}

現有的 `bluemix.net` 網域名稱已淘汰，但您目前可以繼續使用它們，以後將會公布支援結束日期。
{: deprecated}

所有登錄構件的範圍設定為您目前使用中的特定地區登錄。例如，名稱空間、映像檔、記號、配額設定及方案設定必須全都針對每一個地區登錄個別管理。

如果您要使用非本端地區的地區，則可以執行 `ibmcloud cr region-set` 指令，將目標設定為您要存取的地區。您可以在不含任何參數的情況下執行指令來取得可用地區的清單，也可以將地區指定為參數。

若要搭配參數執行指令，請將 `<region>` 取代為地區的名稱，例如 `eu-central`。

```
ibmcloud cr region-set <region>
```
{: pre}

例如，若要將目標設定為 eu-central 地區，請執行下列指令：

```
ibmcloud cr region-set eu-central
```
{: pre}

將目標設定為不同的地區之後，請重新登入登錄：`ibmcloud cr login`。

### 全球登錄
{: #registry_regions_global}

有全球登錄可供使用，其名稱 (`icr.io`) 中不含地區。此登錄中僅管理 IBM 提供的公用映像檔。若要管理您自己的映像檔（例如設定名稱空間或標記映像檔並將映像檔推送至登錄），請使用[本端地區登錄](#registry_regions_local)。
{:shortdesc}

全球登錄的網域名稱已變更。新的網域名稱提供於主控台及 CLI 中。 

下表顯示新的網域名稱。

|登錄|新的網域名稱|已淘汰的網域名稱|
|-----|----|-----------|
|全球| `icr.io` | `registry.bluemix.net` |
{: caption="表 5. 全球登錄的網域名稱。" caption-side="top"}

現有的 `bluemix.net` 網域名稱已淘汰，但您目前可以繼續使用它們，以後將會公布支援結束日期。
{: deprecated}

您可以執行 `ibmcloud cr region-set` 指令，將目標設定為全球登錄。

例如，若要將目標設定為全球登錄，請執行下列指令：

```
ibmcloud cr region-set global
```
{: pre}

如需 `ibmcloud cr region-set` 指令的相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} CLI](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set)。

將目標設定為全球登錄之後，請執行 `ibmcloud cr login` 指令，將本端 Docker 常駐程式登入全球登錄，以便您可以取回 {{site.data.keyword.IBM_notm}} 提供的公用映像檔。

**漏洞警告器網域名稱**

全球的漏洞警告器網域名稱已變更。新的網域名稱提供於主控台及 CLI 中。 

下表顯示新的網域名稱。

|漏洞警告器|新的網域名稱|已淘汰的網域名稱|
|-----|----|-----------|
|全球| `icr.io/va` | `va.bluemix.net` |
{: caption="表 6. 全球登錄的漏洞警告器網域名稱。" caption-side="top"}

現有的 `bluemix.net` 網域名稱已淘汰，但您目前可以繼續使用它們，以後將會公布支援結束日期。
{: deprecated}

## Docker 支援
{: #docker}

{{site.data.keyword.registrylong_notm}} 支援 Docker Engine 1.12.6 版或更新版本。

只有在您要推送或取回映像檔，或者要執行 `ibmcloud cr ppa-archive-load` 指令時，才需要 Docker。
