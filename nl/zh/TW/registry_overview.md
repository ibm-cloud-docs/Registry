---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-2"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 關於 {{site.data.keyword.registrylong_notm}}
{: #registry_overview}

使用 {{site.data.keyword.registrylong}} 在高可用性且可擴充的架構中，安全地儲存及存取專用 Docker 映像檔。
{:shortdesc}

{{site.data.keyword.registrylong_notm}} 提供 IBM 所管理的多方承租戶、高可用性且可擴充的專用映像檔登錄。您可以設定自己的映像檔名稱空間，並將 Docker 映像檔推送至名稱空間，來使用專用登錄。

<img src="images/registry_architecture.png" alt="此影像顯示您可以如何與 IBM Cloud Container Registry 互動。Container Registry 同時包含專用和公用登錄，以及用來與服務互動的 API。您的本端 Docker 用戶端可以從登錄中的專用儲存庫取回映像檔以及將映像檔推送至其中，也可以取回公用儲存庫。IBM Cloud Web 使用者介面（主控台）可與 Container Registry API 互動以列出映像檔。Container Registry CLI 可與 API 互動以列出、建立、檢查及移除映像檔，以及其他管理功能。您的本端 Docker 用戶端也可以從本端映像檔儲存庫中取回映像檔並將其推送至其他儲存庫。"/>

**圖 1. {{site.data.keyword.registrylong_notm}} 如何與您的 Docker 映像檔互動**

Docker 映像檔是每個您建立之容器的基礎。映像檔是從 Dockerfile 建立，而 Dockerfile 是包含映像檔建置指示的檔案。Dockerfile 可能會在其指示中參照分開儲存的建置構件，例如應用程式、應用程式的配置，以及其相依關係。映像檔一般儲存在登錄中，而登錄可供公開存取（公用登錄）或設定一小群使用者的有限存取（專用登錄）。藉由使用 {{site.data.keyword.registrylong_notm}}，只有具有 {{site.data.keyword.Bluemix_notm}} 帳戶存取權的使用者才能存取映像檔。

當您將映像檔推送至 {{site.data.keyword.registrylong_notm}} 時，可以受益於內建的「漏洞警告器」特性，它們會掃描潛在的安全問題及漏洞。「漏洞警告器」會檢查特定 Docker 基礎映像檔中是否包含有漏洞的套件，以及應用程式配置設定中是否有已知漏洞。發現漏洞時，會提供漏洞的相關資訊。您可以使用此資訊來解決安全問題，以避免從有漏洞的映像檔部署容器。

請檢閱下表，以查看使用 {{site.data.keyword.registrylong_notm}} 的好處概觀。

|好處|說明|
|-------|-----------|
|高可用性且可擴充的專用登錄|<ul><li>在 IBM 所管理的多方承租戶、高可用性且可擴充的專用登錄中，設定自己的映像檔名稱空間。</li><li>安全地儲存專用 Docker 映像檔，並將它們與 {{site.data.keyword.Bluemix_notm}} 帳戶中的使用者共用。</li></ul>|
|漏洞警告器的映像檔安全規範|<ul><li>受益於自動掃描名稱空間中的映像檔。</li><li>檢閱作業系統特定建議，以修正潛在漏洞，並保護容器免於洩漏。</li></ul>|
|儲存空間及取回資料流量的配額限制|<ul><li>受益於專用映像檔的免費儲存空間及取回資料流量，直到達到免費配額。</li><li>設定每個月的儲存空間量及取回資料流量的自訂配額限制，以避免超出偏好的付費等級。</li></ul>|
{: caption="表 1. {{site.data.keyword.registrylong_notm}} 的好處" caption-side="top"}

## 服務方案
{: #registry_plans}

您可以選擇免費或標準 {{site.data.keyword.registrylong_notm}} 服務方案來儲存 Docker 映像檔，並讓 {{site.data.keyword.Bluemix_notm}} 帳戶中的使用者可使用這些映像檔。
{:shortdesc}

{{site.data.keyword.registrylong_notm}} 服務方案會決定可用於專用映像檔的儲存空間量及取回資料流量。服務方案與 {{site.data.keyword.Bluemix_notm}} 帳戶相關聯，而且儲存空間及映像檔取回資料流量的限制適用於帳戶中所設定的所有名稱空間。

下表顯示可用的 {{site.data.keyword.registrylong_notm}} 服務方案及其特徵。如需計費運作方式以及您超出服務方案限制時會發生什麼情況的相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} 中的配額限制及計費](#registry_plan_billing)。

|特徵|免費|標準|
|---------------|----|--------|
|說明|試用 {{site.data.keyword.registrylong_notm}} 中的專用登錄，以安全地儲存及共用 Docker 映像檔。當您在 {{site.data.keyword.registrylong_notm}} 中設定第一個名稱空間時，此方案是預設服務方案。|受益於無限制的儲存空間及取回資料流量用量，以管理 {{site.data.keyword.Bluemix_notm}} 帳戶中所有名稱空間的 Docker 映像檔。|
|映像檔的儲存空間量|500 MB|無限制|
|取回資料流量|每個月 5 GB|無限制|
|計費|如果您超出儲存空間或取回資料流量限制，便無法從名稱空間中推送或取回映像檔。如需相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} 中的配額限制及計費](#registry_plan_billing)。|<ul><li>儲存空間：會依使用的 GB-月向您收費。前 0.5 GB-月免費。之後，會依定價計算機中所述向您收費。</li><li>取回資料流量：會依每個月使用的 GB 量向您收費。前 5 GB 免費。之後，會依定價計算機中所述向您收費。如果您超出儲存空間或取回資料流量限制，則無法從名稱空間中推送或取回映像檔。如需儲存空間、取回資料流量及定價計算機的相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} 中的配額限制及計費](#registry_plan_billing)。</li></ul>|
{: caption="表 2. {{site.data.keyword.registrylong_notm}} 方案" caption-side="top"}

## 配額限制及計費
{: #registry_plan_billing}

尋找計費處理程序及配額限制在 {{site.data.keyword.registrylong_notm}} 中如何運作的資訊及範例。
{:shortdesc}

每個映像檔都是從數層建置而來，每一層都代表從基礎映像檔算起的漸進式變更。當您推送或取回映像檔時，會將每一層所需的儲存空間量及取回資料流量加到您的每月用量。相同的層會在 {{site.data.keyword.Bluemix_notm}} 帳戶中的映像檔之間自動共用，而且可以在建立其他映像檔時重複使用。每一個相同層的儲存空間都只會收費一次，而且不論帳戶中有多少映像檔參照該層。

推送映像檔的範例：

> 您將映像檔推送至根據 Ubuntu 映像檔的名稱空間。Ubuntu 映像檔包含數層。因為您的帳戶中還沒有這些層，所以會將這些層所需的儲存空間量加到您的每月用量。
>
> 之後，您建立第二個根據 Ubuntu 映像檔的映像檔。您藉由例如將其他指令或檔案新增至 Dockerfile，變更 Ubuntu 基礎映像檔。每一個變更都代表新的映像檔層。當您推送第二個映像檔時，{{site.data.keyword.registrylong_notm}} 會認出基礎 Ubuntu 映像檔的所有層都已儲存在帳戶中。第二次儲存這些層時不會向您收費，即使您已將映像檔推送至另一個名稱空間也是一樣。{{site.data.keyword.registrylong_notm}} 會判斷所有新層的大小，並將儲存空間量加到您的每月用量。

### 儲存空間及取回資料流量的計費
{: #registry_billing_traffic}

視選擇的服務方案而定，會根據每個月使用的儲存空間及取回資料流量向您收費。
{:shortdesc}

**儲存空間：**

  每個 {{site.data.keyword.registrylong_notm}} 服務方案都會隨附特定儲存空間量，可用來將 Docker 映像檔安全地儲存至 {{site.data.keyword.Bluemix_notm}} 帳戶的名稱空間。如果您使用標準方案，則會依使用的 GB-月向您收費。前 0.5 GB-月免費。如果您使用免費方案，則在達到免費方案的配額限制之前，可以將映像檔免費儲存在 {{site.data.keyword.registrylong_notm}} 中。GB-月是一個月儲存 1GB 的平均值（730 小時）。

  標準方案的範例：

  > 您剛好半個月使用 5 GB，然後將數個映像檔推送至名稱空間，並在剩下的半個月使用 10 GB。您的每月用量計算如下：
  >
  > (5 GB x 0.5（月）) + (10 GB x 0.5（月）) = 2.5 + 5 = 7.5 GB-月
  >
  > 在標準方案中，前 0.5 GB-月免費，因此會向您收取 7 GB-月（7.5 GB-月 - 0.5 GB-月）的費用。

  

**取回資料流量：**

  每個 {{site.data.keyword.registrylong_notm}} 服務方案都會在名稱空間中所儲存的專用映像檔中包括特定的免費取回資料流量。取回資料流量是您在將映像檔的層從名稱空間取回至本端機器時使用的頻寬。如果您使用標準方案，則會依每個月使用的 GB 向您收費。每個月的前 5 GB 免費。如果您使用免費方案，則在達到免費方案的配額限制之前，可以從名稱空間取回映像檔。

  標準方案的範例：

  > 在該月，您已取回包含總大小 14 GB 之層的映像檔。您的每月用量計算如下：
  >
  > 在標準方案中，每個月的前 5 GB 免費，因此會向您收取 9 GB (14 GB - 5 GB) 的費用。

  

### 儲存空間及取回資料流量的配額限制
{: #registry_quota_limits}

視選擇的服務方案而定，您可以在達到方案特定或自訂配額限制之前，從名稱空間推送及取回映像檔。
{:shortdesc}

**儲存空間：**

  當您達到或超出方案的配額限制時，在從名稱空間[移除映像檔來釋放空間](registry_quota.html#registry_quota_freeup)或[升級至標準方案](#registry_plan_upgrade)之前，無法將任何映像檔推送至 {{site.data.keyword.Bluemix_notm}} 帳戶中的名稱空間。如果您設定免費或標準方案中儲存空間的配額限制，則也可以[增加此配額限制](registry_quota.html#registry_quota_set)，以重新啟用新映像檔的推送。

  標準方案的範例：

  > 您的現行儲存空間配額限制設為 1 GB。{{site.data.keyword.Bluemix_notm}} 帳戶的名稱空間中所儲存的所有專用映像檔，已使用這個儲存空間中的 900 MB。在您達到配額限制之前，有 100 MB 的儲存空間可用。有一位使用者想要在本端機器上推送大小為 2 GB 的映像檔。因為尚未達到配額限制，所以 {{site.data.keyword.registrylong_notm}} 容許使用者推送此映像檔。
  >
  > 推送之後，{{site.data.keyword.registrylong_notm}} 會判斷名稱空間中映像檔的實際大小（這可能會與本端機器上的大小不同），並檢查是否達到儲存空間的限制。在此範例中，儲存空間用量會從 900 MB 增加 2 GB。在現行配額限制設為 1 GB 的情況下，{{site.data.keyword.registrylong_notm}} 會阻止您將其他映像檔推送至名稱空間。

**取回資料流量：**

  當您達到或超出方案的配額限制時，在等待下一個計費期間開始、[升級至標準方案](#registry_plan_upgrade)或[增加取回資料流量的配額限制](registry_quota.html#registry_quota_set)之前，無法從 {{site.data.keyword.Bluemix_notm}} 帳戶中的名稱空間取回任何映像檔。

  標準方案的範例：

  > 在該月，取回資料流量的配額限制設為 5 GB。您已從名稱空間取回映像檔，並已使用這個取回資料流量中的 4.5 GB。在您達到配額限制之前，有 0.5 GB 的取回資料流量可用。一位使用者想要從名稱空間取回大小為 1 GB 的映像檔。因為尚未達到配額限制，所以 {{site.data.keyword.registrylong_notm}} 容許使用者取回此映像檔。
  >
  > 取回映像檔之後，{{site.data.keyword.registrylong_notm}} 會判斷您在取回期間已使用的頻寬，並檢查是否達到取回資料流量的限制。在此範例中，取回資料流量用量會從 4.5 GB 增加到 5.5 GB。在現行配額限制設為 5 GB 的情況下，{{site.data.keyword.registrylong_notm}} 會阻止您從名稱空間取回映像檔。

### 預估成本
{: #registry_estimating_costs}

使用 {{site.data.keyword.Bluemix_notm}} 定價計算機預估方案的成本。
{:shortdesc}

您可以使用 {{site.data.keyword.Bluemix_notm}} 提供的成本計算機來為應用程式定價。

1.  開啟定價單，請參閱 [{{site.data.keyword.Bluemix_notm}} 定價](https://www.ibm.com/cloud-computing/bluemix/pricing)。
2.  在**隨收隨付制**區段中，按一下**使用計算機預估成本**。計算機隨即開啟。
3.  在**容器費用**區段捲動至 **Container Registry** 區段。
4.  在提供的欄位中輸入您的儲存空間和資料流量預估。

您的預估成本會顯示在計算機中。

## 升級服務方案
{: #registry_plan_upgrade}

您可以升級服務方案，受益於無限制儲存空間及取回資料流量用量，以管理 {{site.data.keyword.Bluemix_notm}} 帳戶中所有名稱空間的 Docker 映像檔。
{:shortdesc}

如果您要找出您有什麼服務方案，請執行 `bx cr plan` 指令。

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
        bx login
    ```
    {: pre}

    **附註**：如果您有聯合 ID，請使用 `bx login --sso` 來登入 {{site.data.keyword.Bluemix_notm}} CLI。請輸入您的使用者名稱，並使用 CLI 輸出中提供的 URL，來擷取一次性密碼。若沒有 `--sso` 時登入失敗，而有 `--sso` 選項時登入成功，即表示您有聯合 ID。

2.  升級為標準方案。

    ```
    bx cr plan-upgrade standard
    ```
    {: pre}

    **附註：**如果您有 {{site.data.keyword.Bluemix_notm}} 試用帳戶，必須升級至 {{site.data.keyword.Bluemix_notm}} 標準帳戶，才能執行 `bx cr plan-upgrade`。


## 瞭解基本觀念
{: #registry_planning}

瞭解登錄基本觀念，以便準備好使用 {{site.data.keyword.registrylong_notm}} 安全地儲存及共用 Docker 映像檔。
{:shortdesc}

**附註**：請勿將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。


### 瞭解 {{site.data.keyword.registrylong_notm}} 中所用的術語
{: #terms}


<dl>
  <dt>登錄 (Registry)</dt>
  <dd>登錄是一項服務，它提供基礎架構來儲存 Docker 映像檔，且可以藉由使用登錄主機 URL 及選用性的埠來存取。登錄可供公開存取（公用登錄）或已設定一小組使用者的有限存取（專用登錄）。{{site.data.keyword.registrylong_notm}} 提供 IBM 所管理的多方承租戶且高度可用的專用映像檔登錄。您可以設定自己的映像檔名稱空間來使用專用登錄，並開始將 Docker 映像檔推送至名稱空間。</dd>
</dl>

<dl>
  <dt>名稱空間 (Namespace)</dt>
  <dd>名稱空間是在 {{site.data.keyword.registrylong_notm}} 內組織映像檔儲存庫的一種方式。名稱空間會與 {{site.data.keyword.Bluemix_notm}} 帳戶相關聯。當您在 {{site.data.keyword.registrylong_notm}} 中設定自己的名稱空間時，會將名稱空間附加至登錄 URL，如下所示：<code>registry.<em>&lt;region&gt;</em>.bluemix.net/my_namespace</code>。



  您 {{site.data.keyword.Bluemix_notm}} 帳戶中的每個使用者都可以檢視及使用登錄名稱空間中所儲存的映像檔。例如，您可以設定多個名稱空間，讓正式作業及編譯打包環境具有不同的儲存庫。</dd>
</dl>

<dl>
  <dt>儲存庫 (Repository)</dt>
  <dd>映像檔儲存庫是登錄中已標記之相關映像檔的集合。儲存庫 經常與映像檔 互換使用，但儲存庫可能會存放映像檔的多個已標記變化。</dd>
</dl>

<dl>
  <dt>映像檔 (Image)</dt>
  <dd>Docker 映像檔建置在 Dockerfile 中提供的指示之上，且代表容器的基準。建置 Docker 映像檔之後，您可以用它來建立容器，以部署您的應用程式及其相依關係。映像檔儲存在登錄中。能夠存取您的
{{site.data.keyword.Bluemix_notm}} 帳戶的使用者即可存取您的映像檔。</dd>
</dl>

<dl>
  <dt>標籤 (Tag)</dt>
  <dd>標籤是儲存庫內映像檔的 ID。您可以使用標籤來區別儲存庫內相同基礎映像檔的不同版本。當您執行 Docker 指令且未指定儲存庫映像檔的標籤時，依預設會使用以 <code>latest</code> 標記的映像檔。</dd>
</dl>

<dl>
  <dt>Dockerfile</dt>
  <dd>Dockerfile 是包含 Docker 映像檔建置指示的文字檔。映像檔通常建置在基礎映像檔之上，基礎映像檔中包含基礎作業系統，例如 Ubuntu。您可以漸進式地以 Dockerfile 指示定義應用程式執行所需的環境，來變更基礎映像檔。
基礎映像檔的每項變更會說明新的一層映像檔，您可以在單一 Dockerfile 行裡進行多項變更。Dockerfile 中的指示也可能參照分開儲存的建置構件，例如應用程式、應用程式的配置，以及其相依關係。</dd>
</dl>

若要進一步瞭解 Docker 特有術語，[請參閱 Docker 名詞解釋](https://docs.docker.com/glossary/)。


### 規劃名稱空間
{: #registry_namespaces}

{{site.data.keyword.registrylong_notm}} 提供 IBM 所管理的多方承租戶專用映像檔登錄。您可以設定登錄名稱空間，以在此登錄中安全地儲存及共用 Docker 映像檔。
{:shortdesc}

例如，您可以設定多個名稱空間，讓正式作業及編譯打包環境具有不同的儲存庫。如果您要將登錄用於多個 {{site.data.keyword.Bluemix_notm}} 地區，則必須設定每個地區的名稱空間。名稱空間名稱在地區內是唯一的。您可以針對每個地區使用相同的名稱空間，除非別人已經在該地區中設定了該名稱的名稱空間。

若只要使用 IBM 提供的公用映像檔，您不需要設定名稱空間。

**附註**：如果您不確定是否已設定帳戶的名稱空間，請執行 `bx cr namespace-list` 指令來擷取現有名稱空間資訊。如果您是使用[單一及可擴充容器群組](../../containers/cs_classic.html)的現有 {{site.data.keyword.containerlong_notm}} 客戶，則已設定名稱空間。您可以建立其他名稱空間，但無法對多個名稱空間執行 `cf ic namespace set`。

當您選擇名稱空間時，請考量下列規則：

-   在 {{site.data.keyword.Bluemix_notm}} 地區中，名稱空間必須是唯一的。
-   名稱空間的長度必須是 4 - 30 個字元。
-   名稱空間的開頭必須至少使用一個字母或數字。
-   名稱空間只能包含小寫字母、數字或底線 (_)。

**附註**：請勿將個人資訊放在名稱空間名稱中。

在您設定第一個名稱空間之後，則會獲指派免費 {{site.data.keyword.registrylong_notm}} 服務方案（如果您尚未[升級方案](#registry_plan_upgrade)的話）。

## 地區
{: #registry_regions}

{{site.data.keyword.registrylong_notm}} 登錄可在數個地區中使用。
{:shortdesc}

### 本端地區
{: #registry_regions_local}

地區是專用端點存取的地理區域。{{site.data.keyword.registrylong_notm}} 登錄可在下列地區中使用：

-   ap-south：`registry.au-syd.bluemix.net`
-   eu-central：`registry.eu-de.bluemix.net`
-   uk-south：`registry.eu-gb.bluemix.net`
-   us-south：`registry.ng.bluemix.net`

所有登錄構件的範圍設定為您目前使用中的特定地區登錄。例如，名稱空間、映像檔、記號、配額設定及方案設定必須全都針對每個地區登錄分開管理。

如果您想要使用非當地地區的地區，則可以執行 `bx cr region-set` 指令，將目標設定為您要存取的地區。您可以在不含任何參數的情況下執行指令來取得可用地區的清單，也可以將地區指定為參數。

若要搭配參數執行指令，請將 _&lt;region&gt;_ 取代為地區的名稱，例如 `eu-central`。

```
bx cr region-set <region>
```
{: pre}

例如，若要將目標設定為 eu-central 地區，請執行下列指令：

```
bx cr region-set eu-central
```
{: pre}

將目標設為不同的地區之後，請重新登入登錄：`bx cr login`。

### 全球登錄
{: #registry_regions_global}

有全球登錄可供使用，其名稱（`registry.bluemix.net`）不含地區。此登錄中僅管理 IBM 提供的公用映像檔。若要管理您自己的映像檔（例如設定名稱空間或標記映像檔並將映像檔推送至登錄），請使用[本端區域登錄](#registry_regions_local)。
{:shortdesc}

您可以執行 `bx cr region-set` 指令，將目標設定為全球登錄。

例如，若要將目標設定為全球登錄，請執行下列指令：

```
bx cr region-set global
```
{: pre}

如需 `bx cr region-set` 指令的相關資訊，請參閱 [{{site.data.keyword.registrylong_notm}} CLI](registry_cli.html#bx_cr_region_set)。

將目標設定為全球登錄之後，請執行 `bx cr login` 指令，將本端 Docker 常駐程式登入全球登錄，以便您可以取回 {{site.data.keyword.IBM_notm}} 提供的公用映像檔。
