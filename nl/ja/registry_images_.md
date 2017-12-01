---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# 名前空間へのイメージの追加
{: #registry_images_}

{{site.data.keyword.registrylong}} 内の名前空間にイメージを追加することで、
安全に Docker イメージを保管して他のユーザーと共有することができます。{:shortdesc}

名前空間に追加するすべてのイメージは、まずローカル・マシンに存在していなければなりません。
別のリポジトリーからローカル・マシンにイメージをダウンロード (プル) するか、
または Docker `build` コマンドを使用して Dockerfile から固有のイメージをビルドすることができます。
名前空間にイメージを追加するには、{{site.data.keyword.registrylong_notm}} 内の名前空間にローカル・イメージをアップロード (プッシュ) する必要があります。


## 別のレジストリーからのイメージのプル
{: #registry_images_pulling}

専用レジストリーまたはパブリック・レジストリーのソースからイメージをプル (ダウンロード) してタグ付けし、後に {{site.data.keyword.registrylong_notm}} で使用することができます。{:shortdesc}

開始前に、以下のことを行います。

- 名前空間内のイメージを処理するための [CLI をインストールします](registry_setup_cli_namespace.html#registry_cli_install)。
- [独自の名前空間を {{site.data.keyword.registrylong_notm}} にセットアップします](registry_setup_cli_namespace.html#registry_namespace_add)。
- [root 権限なしで Docker コマンドを実行できることを確認します](https://docs.docker.com/engine/installation/linux/linux-postinstall)。Docker クライアントが root 権限を必要とするようにセットアップされている場合は、`bx login`、`bx cr
login`、`docker pull`、および `docker push` の各コマンドを
`sudo` を使用して実行する必要があります。

  root 権限なしで Docker コマンドを実行できるように権限を変更した場合は、再度 `bx login` コマンドを実行する必要があります。



概説資料の[イメージのプル](index.html#registry_images_pulling)を参照して、イメージをダウンロードします。

  **ヒント:** 「unauthorized: authentication required」または「denied: requested access to the resource is denied」というメッセージを受け取った場合は、`bx cr login` コマンドを実行します。



イメージをプルして名前空間のタグを付けたら、イメージをローカル・マシンから名前空間にアップロード (プッシュ) できます。

## Docker イメージの名前空間へのプッシュ
{: #registry_images_pushing}

イメージを {{site.data.keyword.registrylong_notm}} 内の名前空間にプッシュ (アップロード) して、安全にイメージを保管して他のユーザーと共有することができます。{:shortdesc}

開始前に、以下のことを行います。

- 名前空間内のイメージを処理するための [CLI をインストールします](registry_setup_cli_namespace.html#registry_cli_install)。
- [独自の名前空間を {{site.data.keyword.registrylong_notm}} 専用レジストリー](registry_setup_cli_namespace.html#registry_namespace_add)にセットアップします。
- イメージを[プル](#registry_images_pulling)するか、ローカル・マシンで[ビルド](#registry_images_creating)し、そのイメージを名前空間情報でタグ付けします。

- [root 権限なしで Docker コマンドを実行できることを確認します](https://docs.docker.com/engine/installation/linux/linux-postinstall)。Docker クライアントが root 権限を必要とするようにセットアップされている場合は、`bx login`、`bx cr
login`、`docker pull`、および `docker push` の各コマンドを
`sudo` を使用して実行する必要があります。

  root 権限なしで Docker コマンドを実行できるように権限を変更した場合は、再度 `bx login` コマンドを実行する必要があります。



イメージをアップロード (プッシュ) するには、以下の手順に従います。

1. CLI にログインします。

  ```
bx cr login```
  {: pre}

  **注:** 専用 {{site.data.keyword.registrylong_notm}} からイメージをプルする場合は、ログインする必要があります。

2. ご使用のアカウントで利用できるすべての名前空間を表示するには、`bx cr namespace-list` コマンドを実行します。

3. [イメージを名前空間にアップロードします。](index.html#registry_images_pushing)

  **ヒント:** 「unauthorized: authentication required」または「denied: requested access to the resource is denied」というメッセージを受け取った場合は、`bx cr login` コマンドを実行します。


イメージを専用レジストリーにプッシュしたら、以下を行えます。

- [脆弱性アドバイザーでセキュリティーを管理](../va/va_index.html)して、潜在的なセキュリティー問題や脆弱性に関する情報を探します。
- {{site.data.keyword.containerlong_notm}} で、[クラスターを作成し、このイメージを使用してコンテナーをそのクラスターにデプロイします](../../containers/container_index.html)。

## レジストリー間でのイメージのコピー
{: #registry_images_copying}

ある領域内のレジストリーからイメージをプルし、別の領域内のレジストリーにそれをプッシュすることで、両方の領域のユーザー間でそのイメージを共有することができます。{:shortdesc}

開始前に、以下のことを行います。

- 名前空間内のイメージを処理するための [CLI をインストールします](registry_setup_cli_namespace.html#registry_cli_install)。
- [独自の名前空間を {{site.data.keyword.registrylong_notm}} 専用レジストリー](registry_setup_cli_namespace.html#registry_namespace_add)にセットアップします。
- [root 権限なしで Docker コマンドを実行できることを確認します](https://docs.docker.com/engine/installation/linux/linux-postinstall)。Docker クライアントが root 権限を必要とするようにセットアップされている場合は、`bx login`、`bx cr
login`、`docker pull`、および `docker push` の各コマンドを
`sudo` を使用して実行する必要があります。

  root 権限なしで Docker コマンドを実行できるように権限を変更した場合は、再度 `bx login` コマンドを実行する必要があります。



2 つのレジストリー間でイメージをコピーするには、以下のステップを実行してください。

1. [レジストリーからイメージをプルします](#registry_images_pulling)。
2. [イメージを別のレジストリーにプッシュします](#registry_images_pushing)。対象となる新しい領域について、正しいドメイン・ネームを使用していることを確認してください。

イメージをコピーした後、以下を行えます。

- [脆弱性アドバイザーでイメージのセキュリティーを管理](../va/va_index.html)して、潜在的なセキュリティー問題や脆弱性に関する情報を見つけます。
- {{site.data.keyword.containerlong_notm}} で、[クラスターを作成し、このイメージを使用してコンテナーをそのクラスターにデプロイします](../../containers/container_index.html)。

## 名前空間で使用する Docker イメージのビルド
{: #registry_images_creating}

{{site.data.keyword.Bluemix_notm}} で Docker イメージを直接ビルドするか、ローカル・マシンで独自の Docker イメージを作成してから {{site.data.keyword.registrylong_notm}} の名前空間にアップロード (プッシュ) することができます。
{:shortdesc}

開始前に、以下のことを行います。

- 名前空間内のイメージを処理するための [CLI をインストールします](registry_setup_cli_namespace.html#registry_cli_install)。
- [独自の名前空間を {{site.data.keyword.registrylong_notm}} 専用レジストリー](registry_setup_cli_namespace.html#registry_namespace_add)にセットアップします。
- [root 権限なしで Docker コマンドを実行できることを確認します](https://docs.docker.com/engine/installation/linux/linux-postinstall)。Docker クライアントが root 権限を必要とするようにセットアップされている場合は、`bx login`、`bx cr
login`、`docker pull`、および `docker push` の各コマンドを
`sudo` を使用して実行する必要があります。

  root 権限なしで Docker コマンドを実行できるように権限を変更した場合は、再度 `bx login` コマンドを実行する必要があります。



Docker イメージは、作成するすべてのコンテナーの基礎となるものです。イメージは、Dockerfile (イメージをビルドするための指示が入ったファイル) からビルドされます。Dockerfile の別個に保管されている指示の中で、ビルド成果物 (アプリ、アプリの構成、その従属関係) が参照されることもあります。

{{site.data.keyword.Bluemix_notm}} の計算リソースとインターネット接続を利用する必要がある場合、または Docker がワークステーションにインストールされていない場合は、{{site.data.keyword.Bluemix_notm}} でイメージを直接ビルドします。ファイアウォールの内側に存在するサーバーのリソースにビルドでアクセスする必要がある場合は、イメージをローカルでビルドします。

独自の Docker イメージをビルドするには、以下の手順を実行します。

1. ビルド・コンテキストを保管するローカル・ディレクトリーを作成します。ビルド・コンテキストには、Dockerfile および関連するビルド成果物 (アプリ・コードなど) が保管されます。コマンド・ライン・ウィンドウで、このディレクトリーにナビゲートします。
2. Dockerfile を作成します。
  1. ローカル・ディレクトリーに Dockerfile を作成します。

    ```
touch Dockerfile```
    {: pre}

  2. テキスト・エディターを使用して Dockerfile を開きます。少なくとも、イメージをビルドする元の基本イメージを追加する必要があります。
_&lt;source_image&gt;_ と _&lt;tag&gt;_ を、使用するイメージ・リポジトリーとタグに置き換えてください。
別の専用レジストリーのイメージを使用する場合は、この専用レジストリーのイメージに対する絶対パスを定義します。


    ```
    FROM <source_image>:<tag>
    ```
    {: pre}

    パブリック {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty (ibmliberty) イメージをベースとする Dockerfile の作成例:

    ```
    FROM registry.<region>.bluemix.net/ibmliberty:latest
    LABEL description="This is my test Dockerfile"
    EXPOSE 9080
    ```
    {: pre}

    この例では、イメージ・メタデータにラベルを追加し、ポート 9080 を公開します。
使用できる Dockerfile 指示の詳細については、[Dockerfile リファレンス](https://docs.docker.com/engine/reference/builder/)を参照してください。

3. イメージの名前を決めます。イメージ名は以下の形式でなければなりません。

  ```
  registry.<region>.bluemix.net/<my_namespace>/<repo_name>:<tag>
  ```
  {: pre}

  _&lt;my_namespace&gt;_ は名前空間の情報、_&lt;repo_name&gt;_ はリポジトリーの名前、_&lt;tag&gt;_ はイメージに使用するバージョンです。名前空間を見つけるには、`bx cr namespace-list` コマンドを実行します。

4. Dockerfile を含むディレクトリーのパスをメモします。作業ディレクトリーをビルド・コンテキストの保管場所に設定した状態で以下の手順のコマンドを実行する場合は、_&lt;directory&gt;_ をピリオド (.) に置換できます。
5. {{site.data.keyword.Bluemix_notm}} でイメージを直接ビルドするか、それとも、イメージをローカルでビルドしてテストしてから {{site.data.keyword.Bluemix_notm}} にプッシュするかを選択します。
  - イメージを {{site.data.keyword.Bluemix_notm}} で直接ビルドする場合は、以下のコマンドを実行します。

    ```
    bx cr build -t <image_name> <directory>
    ```
    {: pre}

    _&lt;image_name&gt;_ はイメージの名前、_&lt;directory&gt;_ はディレクトリーのパスです。

    `bx cr build` コマンドについて詳しくは、[{{site.data.keyword.registrylong_notm}} CLI](../../cli/plugins/registry/index.html#containerregcli) を参照してください。

  - イメージをローカルでビルドしてテストしてから {{site.data.keyword.Bluemix_notm}} にプッシュする場合は、以下の手順を実行します。
    1. ローカル・マシンで Dockerfile からイメージをビルドし、イメージ名のタグを付けます。

      ```
      docker build -t <image_name> <directory>
      ```
      {: pre}

      _&lt;image_name&gt;_ はイメージの名前、_&lt;directory&gt;_ はディレクトリーのパスです。

    2. オプション: イメージを名前空間にプッシュする前に、ローカル・マシンでテストします。

      ```
      docker run <image_name>
      ```
      {: pre}

      _&lt;image_name&gt;_ をイメージの名前に置き換えます。

    3. イメージを作成して名前空間用にタグ付けしたら、[名前空間専用レジストリーにイメージをプッシュできます](#registry_images_pushing)。

脆弱性アドバイザーを使用してイメージのセキュリティーをチェックする方法については、[脆弱性アドバイザーによるイメージのセキュリティーの管理](../va/va_index.html)を参照してください。

## 専用 {{site.data.keyword.Bluemix_notm}} イメージ・レジストリーからのイメージの削除
{: #registry_images_remove}

不要なイメージは専用イメージ・レジストリーから削除できます。
{:shortdesc}

始めに、イメージを使用しているすべてのコンテナーを削除してください。

パブリック {{site.data.keyword.IBM_notm}} イメージは、専用 {{site.data.keyword.Bluemix_notm}} レジストリーから削除できません。割り当て量としてカウントされることもありません。

1. `bx login` コマンドを実行して {{site.data.keyword.Bluemix_notm}} にログインします。
2. イメージを削除するには、次のコマンドを実行します。

  ```
  bx cr image-rm IMAGE
  ```
  {: pre}

  _IMAGE_ は、削除するイメージへの絶対 {{site.data.keyword.Bluemix_notm}} レジストリー・パス (形式は `namespace/image:tag`) です。

  イメージのパスにタグを指定しない場合、デフォルトでは、`latest` というタグが付いたイメージが削除されます。複数のイメージを削除するには、各専用 {{site.data.keyword.Bluemix_notm}} レジストリー・パスをスペースで区切ってコマンドにリストします。

  **ヒント:** `bx cr namespace-list` コマンドを実行して、名前空間の値を取得できます。

3. 以下のコマンドを実行し、リスト中にイメージが表示されないことを確認して、イメージが削除されたことを検証します。

  ```
bx cr image-list```
  {: pre}
