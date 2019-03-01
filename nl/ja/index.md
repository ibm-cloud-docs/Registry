---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security


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

# {{site.data.keyword.registrylong_notm}} の概説
{: #index}

{{site.data.keyword.registrylong}} には、{{site.data.keyword.Bluemix_notm}} アカウント内で Docker イメージを保管したり、他のユーザーと Docker イメージを共有したりするために使用できる、マルチテナントの専用イメージ・レジストリーが用意されています。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} コンソールには、簡単なクイック・スタートが用意されています。 {{site.data.keyword.Bluemix_notm}} コンソールの使用方法について詳しくは、[脆弱性アドバイザーを使用したイメージ・セキュリティーの管理](/docs/services/va/va_index.html)を参照してください。

コンテナー・イメージ、名前空間名、(レジストリー・トークンなどの) 説明フィールド、イメージ構成データ (イメージ名やイメージ・ラベルなど) に個人情報を含めないでください。
{:tip}

## {{site.data.keyword.registrylong_notm}} CLI のインストール
{: #registry_cli_install}

1. {{site.data.keyword.Bluemix_notm}} `ibmcloud` コマンドを実行できるように、[{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview) をインストールします。このインストールでは、{{site.data.keyword.containerlong_notm}} と {{site.data.keyword.registrylong_notm}} の CLI プラグインもインストールされます。

## 名前空間のセットアップ
{: #registry_namespace_add}

1. {{site.data.keyword.Bluemix_notm}} にログインします。

   ```
   ibmcloud login
   ```
   {: pre}

   フェデレーテッド ID がある場合は、次のコマンドを使用してログインします。

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. 名前空間を追加して、独自のイメージ・リポジトリーを作成します。 `<my_namespace>` を、使用したい名前空間に置き換えてください。

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

3. 名前空間が作成されたことを確認するために、`ibmcloud cr namespace-list` コマンドを実行します。

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## 別のレジストリーからイメージをローカル・マシンにプルする
{: #registry_images_pulling}

1. [Docker CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.docker.com/community-edition#/download) をインストールします。 Windows 8、または OS X Yosemite 10.10.x 以前の場合は、代わりに [Docker Toolbox ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/toolbox/) をインストールします。 {{site.data.keyword.registrylong_notm}} は、Docker Engine v1.12.6 以降をサポートしています。

2. イメージをローカル・マシンにダウンロード (_プル_) します。 `<source_image>` を、イメージのリポジトリーに置き換え、`<tag>` を、イメージに使用するタグ (例: _latest_) に置き換えてください。

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   `<source_image>` が `hello-world`、`<tag>` が `latest` の場合の例:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. イメージにタグ付けします。 `<source_image>` を、先ほどプルしたローカル・イメージのリポジトリーに置き換え、`<tag>` を、そのイメージのタグに置き換えてください。`<region>` を[領域](/docs/services/Registry/registry_overview.html#registry_regions)の名前に置き換えます。`<my_namespace>` を、[名前空間のセットアップ](/docs/services/Registry/index.html#registry_namespace_add)で作成した名前空間に置き換えます。`<new_image_repo>` と `<new_tag>` を置き換えることで、名前空間で使用するイメージのリポジトリーとタグを定義します。

   ```
   docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   `<source_image>` が `hello-world`、`<tag>` が `latest`、`<region>` が `eu-gb`、`<my_namespace>` が `namespace1`、`<new_image_repo>` が `hw_repo`、`<new_tag>` が `1` の場合の例:

   ```
   docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

## Docker イメージを名前空間にプッシュする
{: #registry_images_pushing}

1. `ibmcloud cr login` コマンドを実行してローカル Docker デーモンを {{site.data.keyword.registrylong_notm}} にログインさせます。

   ```
   ibmcloud cr login
   ```
   {: pre}

2. イメージを名前空間にアップロード (_プッシュ_) します。 `<my_namespace>` を、[名前空間のセットアップ](/docs/services/Registry/index.html#registry_namespace_add)で作成した名前空間に置き換え、`<image_repo>` と `<tag>` を、イメージにタグを付けた際に選択したイメージのリポジトリーとタグに置き換えてください。

   ```
   docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}

   `<region>` が `eu-gb`、`<my_namespace>` が `namespace1`、`<image_repo>` が `hw_repo`、`<tag>` が `1` の場合の例:

   ```
   docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}
   

3. 次のコマンドを実行して、イメージが正常にプッシュされたことを確認します。

   ```
   ibmcloud cr image-list
   ```
   {: pre}

おつかれさまでした。 これで、{{site.data.keyword.registrylong_notm}} 内に名前空間がセットアップされ、最初のイメージが名前空間にプッシュされました。

**次の作業**

- [脆弱性アドバイザーでのイメージ・セキュリティーの管理](/docs/services/va/va_index.html)
- [サービス・プランと使用量を確認します](/docs/services/Registry/registry_overview.html#registry_plans)
- [名前空間で追加のイメージを保管および管理します](/docs/services/Registry/registry_images_.html)
- [ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry/registry_users.html#user)
- [クラスターとワーカー・ノードを設定します](/docs/containers/cs_clusters.html#clusters)
