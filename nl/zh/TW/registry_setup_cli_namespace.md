---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-1"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 設定 {{site.data.keyword.registrylong_notm}} CLI 及登錄名稱空間
{: #registry_setup_cli_namespace}

您必須安裝 {{site.data.keyword.Bluemix_notm}} CLI 及 {{site.data.keyword.registrylong}}，然後在 {{site.data.keyword.registrylong_notm}} 中設定登錄名稱空間來建立自己的映像檔儲存庫，才能在 {{site.data.keyword.registrylong_notm}} 中儲存 Docker 映像檔。
{:shortdesc}


**附註**：請勿將個人資訊放在容器映像檔、名稱空間名稱、說明欄位（例如，在登錄記號中）或任何映像檔配置資料（例如，映像檔名稱或映像檔標籤）中。


## 安裝 {{site.data.keyword.registrylong_notm}} CLI (`bx cr`) 外掛程式
{: #registry_cli_install}

安裝 {{site.data.keyword.registrylong_notm}} CLI，以使用指令行來管理 {{site.data.keyword.Bluemix_notm}} 專用登錄中的名稱空間及 Docker 映像檔。
{:shortdesc}

1.  [安裝 container-registry 外掛程式。](index.html#registry_cli_install)
2.  選用項目：[配置 Docker 用戶端在沒有 root 許可權的情況下執行指令](https://docs.docker.com/engine/installation/linux/linux-postinstall)。如果您未執行此步驟，則必須使用 `sudo` 或以 root 使用者身分來執行 `bx login`、`bx cr login`、`docker pull` 及 **docker push** 指令。

您現在可以在 {{site.data.keyword.registrylong_notm}} 專用登錄中設定自己的名稱空間。

## 更新 {{site.data.keyword.registrylong_notm}} (`bx cr`) 外掛程式
{: #registry_cli_update}

您可能要定期更新 {{site.data.keyword.registrylong_notm}} CLI，才能使用新增特性。
{:shortdesc}

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
        bx login
    ```
    {: pre}

2.  更新 container-registry 外掛程式。

    ```
        bx plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  驗證已順利更新外掛程式。

    ```
        bx plugin list
    ```
     {: pre}


## 解除安裝 {{site.data.keyword.registrylong_notm}} (`bx cr`) 外掛程式
{: #registry_cli_uninstall}

如果您不再需要 container-registry 外掛程式，則可以將它解除安裝。
{:shortdesc}

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
        bx login
    ```
    {: pre}

2.  解除安裝 container-registry 外掛程式。

    ```
        bx plugin uninstall container-registry
    ```
    {: pre}

3.  驗證已順利解除安裝外掛程式。

    ```
        bx plugin list
    ```
    {: pre}

    container-registry 外掛程式未顯示在結果中。


## 設定名稱空間
{: #registry_namespace_add}

若要安全地儲存 Docker 映像檔，您必須在 {{site.data.keyword.registrylong_notm}} 專用登錄中建立名稱空間。
{:shortdesc}

開始之前：

-   [安裝 {{site.data.keyword.Bluemix_notm}} CLI 及 container-registry 外掛程式](#registry_cli_install)。
-   [計劃如何使用及命名您的登錄名稱空間](registry_overview.html#registry_namespaces)。

建立名稱空間，請參閱「開始使用」文件中的[設定名稱空間](index.html#registry_namespace_add)。

您現在可以[將 Docker 映像檔推送至 {{site.data.keyword.Bluemix_notm}} 登錄中的名稱空間](registry_images_.html#registry_images_pushing)，並與您帳戶中的其他使用者共用這些映像檔。

## 移除名稱空間
{: #registry_remove}

如果您不再需要登錄名稱空間，則可以從 {{site.data.keyword.Bluemix_notm}} 帳戶中移除名稱空間。
{:shortdesc}

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
        bx login
    ```
    {: pre}

2.  列出可用的名稱空間。

    ```
        bx cr namespace-list
    ```
    {: pre}

3.  移除名稱空間。

    **注意：**當您移除名稱空間時，也會刪除該名稱空間中所儲存的任何映像檔。此動作將無法復原。

    請將 _&lt;my_namespace&gt;_ 取代為您要移除的名稱空間。

    ```
        bx cr namespace-rm <my_namespace>
    ```
    {: pre}

    在您刪除名稱空間之後，根據所儲存映像檔的數目，在該名稱空間再次變成可供重複使用之前，可能需要幾分鐘的時間。
