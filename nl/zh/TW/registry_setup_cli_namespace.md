---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-19"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, 

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

# 設定 {{site.data.keyword.registrylong_notm}} CLI 及登錄名稱空間
{: #registry_setup_cli_namespace}

若要在 {{site.data.keyword.registrylong}} 中管理 Docker 映像檔，您必須安裝 `container-registry` CLI 外掛程式並建立名稱空間。
{:shortdesc}

請不要將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。
{: important}

開始之前，請安裝 {{site.data.keyword.cloud_notm}} CLI，請參閱[開始使用 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started)。

## 安裝 `container-registry` CLI 外掛程式
{: #cli_namespace_registry_cli_install}

安裝 `container-registry` CLI 外掛程式，以使用指令行在 {{site.data.keyword.registrylong_notm}} 中管理您的名稱空間及 Docker 映像檔。
{:shortdesc}

1. [安裝 `container-registry` CLI 外掛程式。](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. 選用項目：[配置 Docker 用戶端在沒有 root 使用者權限 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示") 的情況下執行指令](https://docs.docker.com/install/linux/linux-postinstall/)。如果您未執行此步驟，則必須使用 `sudo` 或以 root 使用者身分來執行 `ibmcloud login`、`ibmcloud cr login`、`docker pull` 及 `docker push` 指令。

您現在可以在 {{site.data.keyword.registrylong_notm}} 中設定自己的 [名稱空間](#registry_namespace_setup)。

## 更新 `container-registry` CLI 外掛程式
{: #registry_cli_update}

您可能要定期更新 `container-registry` CLI 外掛程式，才能使用新特性。
{:shortdesc}

1. 更新 `container-registry` CLI 外掛程式。

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. 驗證已順利更新 `container-registry` CLI 外掛程式。

    ```
    ibmcloud plugin list
    ```
     {: pre}

## 解除安裝 `container-registry` CLI 外掛程式
{: #registry_cli_uninstall}

如果您不再需要 `container-registry` CLI 外掛程式，則可以將它解除安裝。
{:shortdesc}

1. 解除安裝 `container-registry` CLI 外掛程式。

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. 驗證已順利解除安裝 `container-registry` CLI 外掛程式。

    ```
    ibmcloud plugin list
    ```
    {: pre}

    `container-registry` CLI 外掛程式未顯示在結果中。

## 設定名稱空間
{: #registry_namespace_setup}

您必須建立名稱空間，才能在 {{site.data.keyword.registrylong_notm}} 中儲存您的 Docker 映像檔。
{:shortdesc}

**開始之前**

- [安裝 {{site.data.keyword.cloud_notm}} CLI 及 `container-registry` CLI 外掛程式](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)。
- [計劃如何使用及命名您的登錄名稱空間](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces)。

若要建立名稱空間，請參閱「開始使用」文件中的[設定名稱空間](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add)。

此名稱空間在相同地區的所有 {{site.data.keyword.cloud_notm}} 帳戶中必須是唯一的。名稱空間必須有 4 - 30 個字元，且只能包含小寫字母、數字、連字號 (-) 及底線 (_)。名稱空間的開頭和結尾必須是字母或數字。
{: tip}

您現在可以[將 Docker 映像檔推送至{{site.data.keyword.registrylong_notm}} 中的名稱空間](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace)，並與您帳戶中的其他使用者共用這些映像檔。若要在 {{site.data.keyword.cloud_notm}} IAM 中控制名稱空間的存取權，請參閱[建立原則](/docs/services/Registry?topic=registry-user#create)。

## 移除名稱空間
{: #registry_remove}

如果您不再需要登錄名稱空間，則可以從 {{site.data.keyword.cloud_notm}} 帳戶中移除名稱空間。
{:shortdesc}

1. 登入 {{site.data.keyword.cloud_notm}}。

    ```
    ibmcloud login
    ```
    {: pre}

2. 列出可用的名稱空間。

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. 移除名稱空間。

    **注意：**當您移除名稱空間時，也會刪除該名稱空間中所儲存的任何映像檔。此動作無法復原。

    將 `<my_namespace>` 取代為您要移除的名稱空間。

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    在您刪除名稱空間之後，可能需要一些時間，該名稱空間才會再次變成可供重複使用。
