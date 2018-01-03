---

copyright:
  years: 2017
lastupdated: "2017-10-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# トラブルシューティング
{: #ts_index}

ここでは、{{site.data.keyword.registrylong}} の使用に関する一般的なトラブルシューティングの質問への回答を示します。
{:shortdesc}


## {{site.data.keyword.registrylong_notm}} のヘルプとサポートの入手
{: #gettinghelp}

{{site.data.keyword.registrylong_notm}} を使用していて問題や疑問が生じた場合は、情報を検索するか、フォーラムを通じて質問することにより、ヘルプを利用できます。
また、{{site.data.keyword.IBM_notm}} サポート・チケットをオープンすることもできます。


フォーラムを使用して質問するときは、{{site.data.keyword.registrylong_notm}} 開発チームの目に留まるように、質問にタグを付けてください。

-   {{site.data.keyword.registrylong_notm}} でのアプリの開発またはデプロイに関する技術的な質問がある場合は、[スタック・オーバーフロー](http://stackoverflow.com/search?q=+ibm-bluemix)で質問を投稿し、質問に `ibm-bluemix` および `container-registry` のタグを付けてください。
-   サービスおよび概説の指示に関する質問については、[IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) フォーラムを使用してください。`bluemix` タグと `container-registry` タグを含めてください。

フォーラムの使用について詳しくは、[ヘルプの取得](../../support/index.html#getting-help)を参照してください。


{{site.data.keyword.IBM_notm}} サポート・チケットを開く方法や、サポート・レベルとチケットの重大度については、[サポートへのお問い合わせ](../../support/index.html#contacting-support)を参照してください。

## {{site.data.keyword.registrylong_notm}} へのログインが失敗する
{: #ts_login}

{{site.data.keyword.registrylong_notm}} にログインできません。

{: tsSymptoms}
`bx cr login` コマンドが失敗します。

{: tsCauses}
-   container-registry プラグインが古いため、更新する必要がある。
-   Docker がローカル・マシンにインストールされていないか、稼働していない。
-   {{site.data.keyword.Bluemix_notm}} ログイン資格情報の有効期限が切れている。

{: tsResolve}
この問題は、以下の方法で修正できます。

-   {{site.data.keyword.registryshort_notm}} プラグインの最新バージョンにアップグレードします。[">{{site.data.keyword.registrylong_notm}} (`bx cr`) プラグインの更新](registry_setup_cli_namespace.html#registry_cli_update)を参照してください。
-   Docker がマシンにインストールされていることを確認します。既にインストールされている場合、Docker デーモンを再始動します。
-   `bx login` コマンドを再実行して、{{site.data.keyword.Bluemix_notm}} ログイン資格情報をリフレッシュします。


## {{site.data.keyword.registrylong_notm}} コマンドが `'cr' is not a registered command. See 'bx help'.` で失敗する
{: #ts_login_error}

`cr` は登録された `bx` コマンドではないため、`bx cr` コマンドを実行できません。

{: tsSymptoms}
以下のいずれかのエラー・メッセージと同じエラー・メッセージが表示されます。 

```
bx cr login 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

```
bx cr namespace 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

{: tsCauses}
-   The container-registry plug-in is not installed.


{: tsResolve}
この問題は、以下の方法で解決できます。

-   container-registry プラグインをインストールします。[{{site.data.keyword.registryshort_notm}} CLI (bx cr) プラグインのインストール](registry_setup_cli_namespace.html#registry_cli_install)を参照してください。


## 名前空間のセットアップが失敗する
{: #ts_problem}

{: tsSymptoms}
`bx cr namespace-add` を実行するときに、入力した値を名前空間として設定できない。

{: tsCauses}
-   別の {{site.data.keyword.Bluemix_notm}} 組織によって既に使用されている名前空間値を入力した。
-   名前空間は最近削除されており、その名前を再使用している。削除された名前空間に多くのリソースが含まれていた場合、その削除が {{site.data.keyword.registrylong_notm}} によってまだ完全に処理されていない可能性があります。
-   名前空間値に無効な文字を使用した。

{: tsResolve}
この問題は、以下の方法で修正できます。

-   返されたエラー・メッセージに示されている指示に従います。
-   以下を参照して、有効な名前空間を入力したか確認します。
    -   名前空間は、4 文字から 30 文字の長さでなければなりません。
    -   名前空間は、文字または数字で始まる必要があります。
    -   名前空間には、小文字、数字、またはアンダースコアー (_) のみを使用できます。
-   名前空間に別の値を選択します。
-   削除された名前空間を再作成しており、その名前空間に多くのイメージが含まれていた場合は、後で再試行してください。

## Docker イメージのプッシュまたはプルが失敗する
{: #ts_pushpull}

{: tsSymptoms}
Docker イメージをプッシュまたはプルするコマンドを実行すると、エラー・メッセージを受け取る。このエラー・メッセージは、根本原因によって異なります。受け取る可能のあるエラー・メッセージとしては、以下のようなものがあります。


```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan```
{: screen}

```
You have exceeded your pull traffic quota for the current month. Review your pull traffic quota and pricing plan```
{: screen}

```
unauthorized: authentication required```
{: screen}

```
denied: requested access to the resource is denied```
{: screen}

{: tsCauses}
-   Docker がインストールされていない。
-   Docker クライアントが {{site.data.keyword.registrylong_notm}} にログインしていない。
-   {{site.data.keyword.Bluemix_notm}} アクセス・トークンの有効期限が切れている可能性がある。
-   {{site.data.keyword.Bluemix_notm}} アカウントに設定されているストレージまたはプル・トラフィックの割り当て量制限を超えた。

{: tsResolve}
この問題は、以下の方法で修正できます。

-   [Docker がマシンにインストールされていることを確認します](index.html#registry_cli_install)。
-   Docker のインストール・パスを確認します。
-   `bx login` を実行して {{site.data.keyword.Bluemix_notm}} にログインします。次に、`bx cr login` を実行して {{site.data.keyword.registrylong_notm}} CLI にログインします。
-   [{{site.data.keyword.registrylong_notm}} で Docker イメージを保管およびプルするための割り当て量制限と使用量を検討します](registry_quota.html#registry_quota_get)。

## latest タグを使用して最新イメージをプルできない
{: #ts_docker_latest}

{: tsSymptoms}
コマンド `docker pull` を実行しようとしているが、最新バージョンのビルドではないイメージのバージョンが返される。

{: tsCauses}
タグ値を指定せずに Docker コマンドを実行すると、デフォルトでは、イメージを参照するために `latest` タグが適用されます。`latest` タグは、タグ値を明示的に設定せずに実行された最新の `docker build` コマンドまたは `docker tag` コマンドに適用されます。したがって、`docker` コマンドの実行順序が適切でなかったり、一部のイメージに対してタグが明示的に設定されたり、`latest` タグが、最新でないビルドを参照する可能性があります。

{: tsResolve}
通常は、`latest` タグに頼らずに、イメージに毎回別の順次タグを明示的に定義する方が得策です。

## カスタム・ファイアウォールを設定したレジストリーへのアクセスが失敗する
{: #ts_firewall}

{: tsSymptoms}
開発環境において、インバウンドとアウトバウンドのネットワーク・トラフィック用に、カスタム設定を行った追加ファイアウォールをセットアップします。
{{site.data.keyword.registrylong_notm}} にアクセスしようとすると、接続は失敗します。


{: tsCauses}
インバウンドとアウトバウンドのネットワーク・トラフィックでレジストリーとの間の通信を可能にするには、カスタム・ファイアウォールにおいて特定のネットワーク・グループを開く必要があります。


{: tsResolve}
カスタマイズしたファイアウォールで次のネットワーク・グループを開きます。


1.  {{site.data.keyword.registrylong_notm}} に接続するために使用するマシンのパブリック IP アドレスをメモしておいてください。
Kubernetes を使用する場合、ワーカー・ノードのパブリック IP アドレスを使用します。
`bx cs workers <cluster_name_or_id>` を実行して、ワーカー・ノードのパブリック IP アドレスを取得します。*&lt;cluster_name_or_id&gt;* はクラスターの名前または ID です。
2.  ファイアウォールで、マシンとの間の次の接続を許可します。

    -   マシンへの INBOUND 接続については、次のソース・ネットワーク・グループからマシンの宛先パブリック IP アドレスへの着信ネットワーク・トラフィックを許可します。


        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   マシンからの OUTBOUND 接続については、同じネットワーク・グループを使用し、マシンの送信元パブリック IP アドレスからこれらのネットワーク・グループへの発信ネットワーク・トラフィックを許可します。


