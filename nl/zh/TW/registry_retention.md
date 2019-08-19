---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# 保留映像檔
{: #registry_retention}

您可以決定是刪除還是保留映像檔。
{:shortdesc}

## 規劃保留
{: #retention_plan}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) 指令會根據每個名稱空間的基礎來執行，因此，藉由在管線中使用多個名稱空間，以表示可以套用最符合您需求的不同保留準則。

請考慮使用具有開發、暫置和正式作業環境的一般交付管線。在交付程式碼時，持續整合和連續部署會將映像檔推送到登錄中，然後會直接將其部署到您的開發環境。經過測試之後，開發環境中的某些建置會提升到暫置，然後可能會進入正式作業環境。在此情境中，映像檔的變更速度在開發環境中最快，在正式作業環境中最慢。如果所有環境都從相同的名稱空間中取回映像檔，則由於上述變更速度不同，所以要選擇需要保留的適當映像檔數可能會很困難。

有一個好方法是將所有映像檔都交付到開發名稱空間中，例如 `project-development`，然後在提升到管線中更高階段時，使用 [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) 指令將映像檔標記到不同的名稱空間。在上面的範例中，可以有三個名稱空間：開發 `project-development`、暫置 `project-staging` 和正式作業 `project-production`。在從開發提升到暫置時，會將映像檔從 `project-development` 名稱空間標記為 `project-staging` 名稱空間，並且會將 `project-staging` 名稱空間中的映像檔用於部署。同樣地，在從暫置提升到正式作業時，會將映像檔從 `project-staging` 名稱空間標記為 `project-production` 名稱空間，並且會將 `project-production` 名稱空間中的映像檔用於正式作業部署。

使用此技術的好處在於：

* 可以針對開發、暫置和正式作業名稱空間選擇不同的保留設定。
* 與為所有映像檔使用單一名稱空間相比，此方法可以將意外移除可能會在暫置或正式作業環境中用到之映像檔的機會降至最低。
* 您可以使用不同的 [IAM](/docs/services/Registry?topic=registry-iam) 原則。例如，您可以針對正式作業映像檔有較嚴格的存取權。
* 您可以簽署正式作業映像檔，但不簽署開發和暫置映像檔。

## 清除名稱空間，僅保留符合條件的映像檔
{: #retention_images}

請套用指定的準則，以在 {{site.data.keyword.registrylong_notm}} 中為名稱空間內的每個儲存庫保留映像檔。名稱空間中的所有其他映像檔都會刪除。
{:shortdesc}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) 指令會列出將刪除的映像檔，並讓您可以取消刪除。

儲存庫內的某個映像檔由多個標籤參照時，該映像檔只會計算一次。會保留最新的映像檔。經歷時間是由映像檔的建立時間所決定，而不是它推送到登錄的時間。
{: tip}

刪除映像檔無法復原。刪除現有部署正在使用的映像檔，可能會導致擴增及（或）重新排程失敗。
{: important}

若要使用 CLI 減少名稱空間中每個儲存庫的映像檔數，請完成下列步驟：

1. 執行 `ibmcloud login` 指令，以登入 {{site.data.keyword.cloud_notm}}。
2. 執行下列指令並選取適當的地區，來選擇您要清理映像檔的登錄：

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. 若要保留部分映像檔而刪除其他映像檔，請執行下列指令：

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   其中，`IMAGECOUNT` 是要為名稱空間 `NAMESPACE` 內每個儲存庫保留的映像檔數目。

3. 執行下列指令，驗證已刪除映像檔，並確認映像檔未顯示在清單中。

   ```
   ibmcloud cr image-list
   ```
   {: pre}
