---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# {{site.data.keyword.registrylong_notm}} の概説
{: #index}

{{site.data.keyword.registrylong}} には、{{site.data.keyword.Bluemix_notm}} アカウント内で Docker イメージを安全に保管したり、他のユーザーと Docker イメージを共有したりするために使用できる、マルチテナントの専用イメージ・レジストリーが用意されています。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} コンソールには、簡単なクイック・スタートが用意されています。 {{site.data.keyword.Bluemix_notm}} コンソールの使用方法について詳しくは、[脆弱性アドバイザーを使用したイメージ・セキュリティーの管理](/docs/services/va/va_index.html)を参照してください。

コンテナー・イメージ、名前空間名、(レジストリー・トークンなどの) 説明フィールド、イメージ構成データ (イメージ名やイメージ・ラベルなど) に個人情報を含めないでください。
{:tip}

## {{site.data.keyword.registrylong_notm}} CLI のインストール
{: #registry_cli_install}

1. {{site.data.keyword.Bluemix_notm}} `ibmcloud` コマンドを実行できるように、 [{{site.data.keyword.Bluemix_notm}} CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://clis.ng.bluemix.net/ui/home.html)をインストールします。 このインストールでは、{{site.data.keyword.containerlong_notm}} と {{site.data.keyword.registrylong_notm}} に関するプラグインもインストールされます。

## 名前空間のセットアップ
{: #registry_namespace_add}

1. {{site.data.keyword.Bluemix_notm}} にログインします。

   ```
   ibmcloud login
   ```
   {: pre}

2. 名前空間を追加して、独自のイメージ・リポジトリーを作成します。 _&lt;my_namespace&gt;_ を、使用したい名前空間に置換します。

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

1. [Docker CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.docker.com/community-edition#/download) をインストールします。 Windows 8、または OS X Yosemite 10.10.x 以前の場合は、代わりに [Docker Toolbox ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/toolbox/) をインストールします。

2. イメージをローカル・マシンにダウンロード (_プル_) します。 _&lt;source_image&gt;_ をイメージのリポジトリーに置き換え、_&lt;tag&gt;_ をイメージに使用するタグ (例: _latest_) に置き換えてください。

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   _&lt;source_image&gt;_ が `hello-world` で _&lt;tag&gt;_ が `latest` の場合の例:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. イメージにタグ付けします。 _&lt;source_image&gt;_ を先ほどプルしたローカル・イメージのリポジトリーに、_&lt;tag&gt;_ をそのイメージのタグに置き換えてください。 _&lt;region&gt;_ を[領域](registry_overview.html#registry_regions)の名前に置き換えます。 _&lt;my_namespace&gt;_ を[名前空間のセットアップ](index.html#registry_namespace_add)で作成した名前空間に置き換えます。 _&lt;new_image_repo&gt;_ と _&lt;new_tag&gt;_ を置き換えることで、名前空間で使用するイメージのリポジトリーとタグを定義します。

   ```
   docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   _&lt;source_image&gt;_ が `hello-world`、_&lt;tag&gt;_ が `latest`、_&lt;region&gt;_ が `eu-gb`、_&lt;my_namespace&gt;_ が `namespace1`、_&lt;new_image_repo&gt;_ が `hw_repo`、_&lt;new_tag&gt;_ が `1` の場合の例:

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

2. イメージを名前空間にアップロード (_プッシュ_) します。 _&lt;my_namespace&gt;_ を[名前空間のセットアップ](index.html#registry_namespace_add)で作成した名前空間に置き換え、_&lt;image_repo&gt;_ と _&lt;tag&gt;_ をイメージにタグを付けた際に選択したイメージのリポジトリーとタグに置き換えます。

   ```
   docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}

   _&lt;region&gt;_ が `eu-gb`、_&lt;my_namespace&gt;_ が `namespace1`、_&lt;image_repo&gt;_ が `hw_repo`、_&lt;tag&gt;_ が `1` の場合の例:

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

- [脆弱性アドバイザーでのイメージ・セキュリティーの管理](../va/va_index.html)
- [サービス・プランと使用量を確認します](registry_overview.html#registry_plans)
- [名前空間で追加のイメージを保管および管理します](registry_images_.html)
- [ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry/registry_users.html#user)
- [クラスターとワーカー・ノードを設定します](/docs/containers/cs_clusters.html#clusters)
