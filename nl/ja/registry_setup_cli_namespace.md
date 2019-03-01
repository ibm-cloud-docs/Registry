---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing

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

# {{site.data.keyword.registrylong_notm}} CLI およびレジストリー名前空間のセットアップ
{: #registry_setup_cli_namespace}

{{site.data.keyword.registrylong}} に Docker イメージを保管する前に、名前空間を作成する必要があります。 名前空間の作業をするためには、その前に `container-registry` CLI プラグインをインストールする必要があります。
{:shortdesc}

コンテナー・イメージ、名前空間名、(レジストリー・トークンなどの) 説明フィールド、イメージ構成データ (イメージ名やイメージ・ラベルなど) に個人情報を含めないでください。
{:tip}

始めに、[{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview) をインストールします。

## `container-registry` CLI プラグインのインストール
{: #cli_namespace_registry_cli_install}

コマンド・ラインを使用して {{site.data.keyword.registrylong_notm}} の名前空間および Docker イメージを管理するには、`container-registry` CLI プラグインをインストールします。
{:shortdesc}

1. [`container-registry` CLI プラグインをインストールします。](/docs/services/Registry/index.html#registry_cli_install)
2. オプション: [root 権限なしでコマンドを実行するように Docker クライアントを構成します ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/engine/installation/linux/linux-postinstall)。 この手順を行わない場合は、`ibmcloud login`、`ibmcloud cr login`、`docker pull`、`docker push` の各コマンドを、**sudo** を使用して実行するか root として実行する必要があります。

これで、{{site.data.keyword.registrylong_notm}} に固有の名前空間をセットアップできます。

## `container-registry` CLI プラグインの更新
{: #registry_cli_update}

新しいフィーチャーを使用するために `container-registry` CLI プラグインを定期的に更新することをお勧めします。
{:shortdesc}

1. `container-registry` CLI プラグインを更新します。

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. `container-registry` CLI プラグインが正常に更新されたことを確認します。

    ```
    ibmcloud plugin list
    ```
     {: pre}

## `container-registry` CLI プラグインのアンインストール
{: #registry_cli_uninstall}

`container-registry` CLI プラグインは、もはや必要がない場合、アンインストールすることができます。
{:shortdesc}

1. `container-registry` CLI プラグインをアンインストールします。

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. `container-registry` CLI プラグインが正常にアンインストールされたことを確認します。

    ```
    ibmcloud plugin list
    ```
    {: pre}

    `container-registry` CLI プラグインは結果に表示されません。

## 名前空間のセットアップ
{: #registry_namespace_setup}

Docker イメージを {{site.data.keyword.registrylong_notm}} に保管するには、名前空間を作成する必要があります。
{:shortdesc}

**始めに**

- [{{site.data.keyword.Bluemix_notm}} CLI と `container-registry` CLI プラグインをインストールします](/docs/services/Registry/index.html#registry_cli_install)。
- [レジストリー名前空間の使用方法と命名について計画します](/docs/services/Registry/registry_overview.html#registry_namespaces)。

概説資料の[名前空間のセットアップ](/docs/services/Registry/index.html#registry_namespace_add)を参照して名前空間を作成します。

これで、[{{site.data.keyword.registrylong_notm}} 内の名前空間に Docker イメージをプッシュし](/docs/services/Registry/registry_images_.html#registry_images_pushing_namespace)、それらのイメージをアカウント内の他のユーザーと共有できるようになりました。

## 名前空間の削除
{: #registry_remove}

レジストリーの名前空間が不要になったら、{{site.data.keyword.Bluemix_notm}} アカウントからその名前空間を削除することができます。
{:shortdesc}

1. {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
    ibmcloud login
    ```
    {: pre}

2. 使用可能な名前空間をリストします。

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. 名前空間を削除します。

    **注意:** 名前空間を削除すると、その名前空間に保管されているイメージもすべて削除されます。 このアクションは元に戻せません。

    `<my_namespace>` を、削除する名前空間に置換します。

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    名前空間を削除した後は、その名前空間が再使用可能になるまでに数分間かかる可能性があります。
