---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

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

# {{site.data.keyword.registrylong_notm}} CLI およびレジストリー名前空間のセットアップ
{: #registry_setup_cli_namespace}

{{site.data.keyword.registrylong}} 内の Docker イメージを管理するには、`container-registry` CLI プラグインをインストールして、名前空間を作成する必要があります。
{:shortdesc}

コンテナー・イメージ、名前空間名、説明フィールド、イメージ構成データ (イメージ名やイメージ・ラベルなど) に個人情報を含めないでください。
{: important}

始めに、{{site.data.keyword.cloud_notm}} CLI をインストールします。[{{site.data.keyword.cloud_notm}} CLI の概要](/docs/cli?topic=cloud-cli-getting-started)を参照してください。

## `container-registry` CLI プラグインのインストール
{: #cli_namespace_registry_cli_install}

コマンド・ラインを使用して {{site.data.keyword.registrylong_notm}} の名前空間および Docker イメージを管理するには、`container-registry` CLI プラグインをインストールします。
{:shortdesc}

1. [`container-registry` CLI プラグインをインストールします。](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. オプション: [root 権限なしでコマンドを実行するように Docker クライアントを構成します ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/install/linux/linux-postinstall/)。 この手順を行わない場合は、`ibmcloud login`、`ibmcloud cr login`、`docker pull`、`docker push` の各コマンドを、`sudo` を使用して実行するか root として実行する必要があります。

これで、{{site.data.keyword.registrylong_notm}} に固有の[名前空間](#registry_namespace_setup)をセットアップできます。

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

## 名前空間の計画
{: #registry_setup_cli_namespace_plan}

{{site.data.keyword.registrylong_notm}} には、IBM によってホストおよび管理されているマルチテナントの専用イメージ・レジストリーが用意されています。 レジストリー名前空間をセットアップすることにより、このレジストリー内で Docker イメージを保管および共有することができます。
{:shortdesc}

複数の名前空間をセットアップし、例えば、実動用とステージング環境用に別々のリポジトリーを用意することができます。 レジストリーを複数の {{site.data.keyword.cloud_notm}} 地域で使用する場合は、地域ごとに名前空間をセットアップする必要があります。 名前空間名は、それぞれの地域内で固有です。 同じ名前空間名を各地域で使用できますが、別のユーザーが既にその名前で名前空間を設定している地域では使用できません。

IAM ポリシーを使用して、名前空間へのアクセスを制御できます。 詳しくは、[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry?topic=registry-user#user)を参照してください。

IBM 提供のパブリック・イメージのみを使用して作業する場合、名前空間をセットアップする必要はありません。

アカウントに名前空間が既に設定されているかどうかが不明な場合は、`ibmcloud cr namespace-list` コマンドを実行して、既存の名前空間に関する情報を取得してください。
{:tip}

名前空間を選択する際は、以下のルールを考慮してください。

- 名前空間は、同じ地域内のすべての {{site.data.keyword.cloud_notm}} アカウントにおいて固有でなければなりません。
- 名前空間は、4 文字から 30 文字でなければなりません。
- 名前空間は、文字または数値で開始および終了する必要があります。
- 名前空間には、小文字、数字、ハイフン (-) およびアンダースコアー (_) のみを使用できます。

名前空間名に個人情報を含めないでください。
{: important}

最初の名前空間を設定した後、無料の {{site.data.keyword.registrylong_notm}} サービス・プランが割り当てられます ([プランのアップグレード](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade)をまだ実行していない場合)。

## 名前空間のセットアップ
{: #registry_namespace_setup}

Docker イメージを {{site.data.keyword.registrylong_notm}} に保管するには、名前空間を作成する必要があります。
{:shortdesc}

**始めに**

- [{{site.data.keyword.cloud_notm}} CLI および `container-registry` CLI プラグイン](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)をインストールします。
- [レジストリー名前空間の使用方法と命名について計画します](#registry_setup_cli_namespace_plan)。

名前空間を作成するには、概説資料内の[名前空間のセットアップ](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add)を参照してください。

名前空間は、同じ地域内のすべての {{site.data.keyword.cloud_notm}} アカウントにおいて固有でなければなりません。 名前空間は 4 文字から 30 文字までで、含めることができるのは、小文字、数字、ハイフン (-)、下線 (_) のみです。 名前空間は、文字または数値で開始および終了する必要があります。
{: tip}

これで、[{{site.data.keyword.registrylong_notm}} 内の名前空間に Docker イメージをプッシュし](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace)、それらのイメージをアカウント内の他のユーザーと共有できるようになりました。 {{site.data.keyword.cloud_notm}} IAM で名前空間へのアクセスを制御するには、[ポリシーの作成](/docs/services/Registry?topic=registry-user#create)を参照してください。

## 名前空間の削除
{: #registry_remove}

レジストリーの名前空間が不要になったら、{{site.data.keyword.cloud_notm}} アカウントからその名前空間を削除することができます。
{:shortdesc}

1. {{site.data.keyword.cloud_notm}} にログインします。

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
