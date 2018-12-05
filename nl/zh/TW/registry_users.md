---

copyright:
  years: 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 定義使用者存取角色原則
{: #user access}

當您作為管理者時，可以定義登錄的存取原則，以建立不同使用者的不同存取層次。例如，您可以授權某些使用者設定配額，而其他使用者只能檢視配額。
{: shortdesc}

您必須針對使用 {{site.data.keyword.registrylong}} 的每位使用者定義存取原則。存取原則的範圍是根據使用者的已定義角色而來，而角色可決定容許他們執行的動作。部分原則是預先定義的，但其他原則可以自訂。

如果您在 2018 年 10 月 4 日之前開始使用 {{site.data.keyword.registrylong_notm}}，則必須先啟用原則強制執行，您的原則才會生效，請參閱[啟用現有使用者的原則強制執行](#existing_users)。
{: tip}

若要進一步瞭解 {{site.data.keyword.iamlong}} (IAM) 存取角色原則，請參閱 [{{site.data.keyword.iamshort}}](/docs/iam/index.html#iamoverview)。

## 建立原則
{: #create}

如果您要控制資源存取權，則必須將角色指派給使用者或「服務 ID」。可以依名稱將 {{site.data.keyword.registrylong_notm}} 資源存取權授與名稱空間資源或整個服務（亦即，帳戶中的所有名稱空間）。

如果您要授與任何項目的存取權，請不要指定資源類型或資源。如果您要授與特定名稱空間的存取權，請將資源類型指定為 `namespace`，並使用名稱空間名稱作為資源。

**開始之前**

- 決定每位使用者所需的角色，以及 {{site.data.keyword.registrylong_notm}} 中的資源，請參閱 [IAM 角色](/docs/services/Registry/iam.html#iam)。請考量您可以建立多個原則，例如，您可以授與資源的寫入權，但只授與另一個資源的讀取權，而且無法授與另一個資源的存取權。原則是加總性的，表示廣域讀取原則及資源範圍寫入原則會授與該資源的讀取權及寫入權。

- [邀請使用者並指派存取權](/docs/iam/iamuserinv.html#iamuserinv)。 

  如果您要使用者可以在 {{site.data.keyword.containerlong_notm}} 中建立叢集，請確定您將 {{site.data.keyword.registrylong_notm}}「管理者」角色指派給這些使用者，而不指派資源群組，請參閱[準備建立叢集](/docs/containers/cs_clusters.html#cluster_prepare)。
  {: tip}

若要建立 {{site.data.keyword.registrylong_notm}} 的原則，服務名稱欄位必須是 `container-registry`。

* 若要建立使用者的原則，請參閱[管理資源存取權](/docs/iam/mngiam.html#iammanidaccser)。
* 若要建立「服務 ID」的原則，請執行 `ibmcloud iam service-policy-create` 指令，或使用 GUI 將角色連結至「服務 ID」。若要建立原則，您必須具有「管理者」角色。您自動具有自己帳戶的「管理者」角色。如需相關資訊，請參閱[建立及使用服務 ID](/docs/iam/serviceid.html#serviceids) 及[管理服務 ID 存取原則](/docs/iam/serviceidaccess.html#serviceidpolicy)。

## 啟用現有使用者的原則強制執行
{: #existing_users}

對於在 2018 年 10 月 4 日之後佈建的使用者，依預設會啟用 IAM 原則。對於在 2018 年 10 月 4 日之前佈建的使用者，您必須在建立原則之後啟用原則強制執行，才能讓原則生效。

1. 對於使用者及「服務 ID」，[建立原則](#create)。

2. 若要啟用原則強制執行，請執行 [`bx cr iam-policies-enable`](/docs/services/Registry/registry_cli.html#bx_cr_iam_policies_enable) 指令。

    您必須具有帳戶的「管理員」角色，才能執行 `ibmcloud cr iam-policies-enable` 指令。您自動具有自己帳戶的「管理員」角色。
    {: tip}
