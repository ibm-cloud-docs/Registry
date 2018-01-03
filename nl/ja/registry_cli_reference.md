---

copyright:
  years: 2017
lastupdated: "2017-11-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 名前空間内で Docker イメージを管理するための {{site.data.keyword.registrylong_notm}} (`bx cr`) コマンド
{: #registry_cli_reference}

container-registry プラグインを使用して、IBM によってホストおよび管理されている専用レジストリー内に、Docker イメージを安全に保管したり、{{site.data.keyword.Bluemix}} アカウント内のすべてのユーザーと Docker イメージを共有したりできる、独自のイメージ名前空間をセットアップすることができます。
{:shortdesc}


## bx cr コマンド
{: #registry_cli_reference_bxcr}

{{site.data.keyword.registryshort_notm}} CLI で `bx cr` コマンドを実行します。
{:shortdesc}

サポートされているコマンドについては、[{{site.data.keyword.registrylong_notm}} CLI](../../cli/plugins/registry/index.html#containerregcli) を参照してください。

## {{site.data.keyword.registrylong_notm}} コマンドの CLI 出力のフォーマット設定およびフィルター操作
{: #registry_cli_listing}

サポートされている {{site.data.keyword.registrylong_notm}} コマンドの CLI 出力をフォーマット設定およびフィルター操作することができます。
{:shortdesc}

デフォルトで、CLI 出力は、人間が読める形式で表示されます。ただし、このビューでは、特にコマンドがプログラマチックに実行される場合、出力の使用能力が制限される可能性があります。例えば、`bx cr image-list` の CLI 出力で、`Size` フィールドを数値サイズでソートしたいかもしれませんが、コマンドから返されるのは文字列表記のサイズです。container-registry プラグインには、Go テンプレートを CLI 出力に適用するために使用できる format オプションが用意されています。Go テンプレートは、CLI 出力のカスタマイズを可能にする [Go プログラミング言語](https://golang.org/pkg/text/template/)のフィーチャーの 1 つです。

format オプションを次の 2 つの異なる方法で適用して、CLI 出力を変更できます。

1.  CLI 出力内のデータをフォーマット設定する。例えば、`Created` フィールドの出力を Unix 時刻から標準時刻に変更できます。
2.  CLI 出力内のデータをフィルター操作する。例えば、Go テンプレートの `if gt` 条件を使用することにより、イメージの詳細でフィルター操作してイメージの特定のサブセットを表示します。

format オプションは、次の {{site.data.keyword.registrylong_notm}} コマンドで使用できます。コマンドをクリックすると、使用可能なフィールドとそれらのデータ・タイプのリストが表示されます。

-   [`bx cr image-list`](registry_cli_reference.html#registry_cli_listing_imagelist)
-   [`bx cr image-inspect`](registry_cli_reference.html#registry_cli_listing_imageinspect)
-   [`bx cr token-list`](registry_cli_reference.html#registry_cli_listing_tokenlist)

次のサンプル・コードは、フォーマット設定オプションとフィルター操作オプションの使用方法を示しています。

-   次の `bx cr image-list` コマンドを実行すると、サイズが 1 MB を超えるすべてのイメージのリポジトリー、タグ、および脆弱性の状況が表示されます。

    ```
    bx cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .Vulnerable }}{{end}}"
    ```
    {: pre}

    出力例:

    ```
    example-registry.<region>.bluemix.net/user1/ibmliberty:latest OK
    example-registry.<region>.bluemix.net/user1/ibmnode:1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode:test1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode2:test2 Vulnerable
    ```
    {: screen}

-   次の `bx cr image-inspect` コマンドを実行すると、指定された IBM パブリック・イメージについて IBM 文書がホストされている場所が表示されます。

    ```
    bx cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"

    ```
    {: pre}

    出力例:

    ```
map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]```
    {: screen}

-   次の `bx cr image-inspect` コマンドを実行すると、指定されたイメージについて公開されているポートが表示されます。

    ```
    bx cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"

    ```
    {: pre}

    出力例:

    ```
    map[9080/tcp: 9443/tcp:]
    ```
    {: screen}

-   次の `bx cr token-list` コマンドを実行すると、すべての読み取り専用のトークンが表示されます。

    ```
    bx cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
    {: pre}

    出力例:

    ```
0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo```
    {: screen}


### `bx cr image-list` コマンド内の Go テンプレートのオプションおよびデータ・タイプ
{: #registry_cli_listing_imagelist}

以下の表を検討して、`bx cr image-list` コマンドで使用可能な、Go テンプレートのオプションおよびデータ・タイプを見つけてください。
{:shortdesc}

|フィールド|タイプ|説明|
|-----|----|-----------|
|`Created`|整数 (64 ビット)|イメージが作成された時刻を表示します。表記は [UNIX 時刻](https://en.wikipedia.org/wiki/Unix_time)の秒数です。
|
|`Digest`|文字列|イメージの固有 ID を表示します。|
|`Namespace`|文字列|イメージが保管されている名前空間を表示します。|
|`Repository`|文字列|イメージのリポジトリーを表示します。|
|`Size`|整数 (64 ビット)|イメージのサイズをバイト単位で表示します。|
|`Tag`|文字列|イメージのタグを表示します。|
|`Vulnerable`|文字列|イメージの脆弱性の状況を表示します。状況の種類については、[脆弱性アドバイザーによるイメージのセキュリティーの管理](../va/va_index.html)に記載しています。|
{: caption="表 1. bx cr image-list コマンドで使用可能なフィールドとデータ・タイプ。" caption-side="top"}

### `bx cr image-inspect` コマンドの Go テンプレートのオプションおよびデータ・タイプ
{: #registry_cli_listing_imageinspect}

以下の表を検討して、`bx cr image-inspect` コマンドで使用可能な、Go テンプレートのオプションおよびデータ・タイプを見つけてください。
{:shortdesc}

|フィールド|タイプ|説明|
|-----|----|-----------|
|`ID`|文字列|イメージの固有 ID を表示します。|
|`Parent`|文字列|このイメージのビルドに使用された親イメージの ID を表示します。|
|`Comment`|文字列|イメージの説明を表示します。|
|`Created`|文字列|イメージが作成された時刻の [UNIX タイム・スタンプ](https://en.wikipedia.org/wiki/Unix_time)を表示します。
|
|`Container`|文字列|イメージを作成したコンテナーの ID を表示します。|
|`ContainerConfig`|オブジェクト|このイメージから開始されるコンテナーのデフォルト構成を表示します。[Config](registry_cli_reference.html#config) でフィールド詳細を参照してください。|
|`DockerVersion`|文字列|このイメージのビルドに使用された Docker のバージョンを表示します。|
|`Author`|文字列|イメージの作成者を表示します。|
|`Config`|オブジェクト|イメージの構成メタデータを表示します。[Config](registry_cli_reference.html#config) でフィールド詳細を参照してください。|
|`Architecture`|文字列|このイメージのビルドに使用された、およびこのイメージの実行に必要なプロセッサー・アーキテクチャーを表示します。|
|`Os`|文字列|このイメージのビルドに使用された、およびこのイメージの実行に必要なオペレーティング・システム・ファミリーを表示します。|
|`OsVersion`|文字列|このイメージのビルドに使用されたオペレーティング・システムのバージョンを表示します。|
|`Size`|整数 (64 ビット)|イメージのサイズをバイト単位で表示します。|
|`VirtualSize`|整数 (64 ビット)|イメージ内の各レイヤーのサイズの合計をバイト単位で表示します。|
|`RootFS`|オブジェクト|イメージのルート・ファイルシステムを記述するメタデータを表示します。[RootFS](registry_cli_reference.html#rootfs) でフィールド詳細を参照してください。|
{: caption="表 2. bx cr image-inspect コマンドで使用可能なフィールドとデータ・タイプ。" caption-side="top"}

#### Config

|フィールド|タイプ|説明|
|-----|----|-----------|
|`Hostname`|文字列|コンテナーのホスト名を表示します。|
|`Domainname`|文字列|コンテナーの完全修飾ドメイン・ネームを表示します。|
|`User`|文字列|イメージが使用されているコンテナー内でコマンドを実行するユーザーを表示します。|
|`AttachStdin`|ブール|標準入力ストリームがコンテナーに付加されている場合は _true_ を表示し、そうでない場合は _false_ を表示します。|
|`AttachStdout`|ブール|標準出力ストリームがコンテナーに付加されている場合は _true_ を表示し、そうでない場合は _false_ を表示します。|
|`AttachStderr`|ブール|標準エラー・ストリームがコンテナーに付加されている場合は _true_ を表示し、そうでない場合は _false_ を表示します。|
|`ExposedPorts`|キーと値のマップ|公開されているポートのリストを `[123:,456:]` という形式で表示します。|
|`Tty`|ブール|コンテナーに疑似 TTY が割り当てられている場合は _true_ を表示し、そうでない場合は _false_ を表示します。|
|`OpenStdin`|ブール|標準入力ストリームがオープンしている場合は _true_ を表示し、標準入力ストリームがクローズしている場合は _false_ を表示します。|
|`StdinOnce`|ブール|付加されたクライアントが切断した後に標準入力ストリームがクローズされた場合は _true_ を表示し、標準入力ストリームがオープンしたままの場合は _false_ を表示します。|
|`Env`|文字列の配列|キーと値のペアの形式で環境変数のリストを表示します。|
|`Cmd`|文字列の配列|コンテナーの開始時に実行される、コンテナーに渡されるコマンドと引数を記述します。|
|`Healthcheck`|オブジェクト|コンテナーが正常であることの検査方法を記述します。[Healthcheck](registry_cli_reference.html#healthcheck) でフィールド詳細を参照してください。|
|`ArgsEscaped`|ブール|コマンドが既にエスケープされている場合、true を表示します (Windows のみ)。|
|`Image`|文字列|演算子によって渡されたイメージの名前を表示します。|
|`Volumes`|キーと値のマップ|コンテナーにマウントされているボリューム・マウントのリストを表示します。|
|`WorkingDir`|文字列|指定されたコマンドが実行される、コンテナー内の作業ディレクトリーを表示します。|
|`Entrypoint`|文字列の配列|コンテナーの開始時に実行されるコマンドを記述します。|
|`NetworkDisabled`|ブール|コンテナーでネットワーキングが無効になっている場合は _true_ を表示し、コンテナーでネットワーキングが有効になっている場合は _false_ を表示します。|
|`MacAddress`|文字列|コンテナーに割り当てられている MAC アドレスを表示します。|
|`OnBuild`|文字列の配列|イメージの Dockerfile に定義された ONBUILD メタデータを表示します。|
|`Labels`|キーと値のマップ|鍵と値のペアとして、イメージに追加されたラベルのリストを表示します。|
|`StopSignal`|文字列|コンテナーを停止するタイミングを送信するための UNIX ストップ信号を記述します。|
|`StopTimeout`|整数|コンテナーを停止するためのタイムアウトを秒単位で表示します。|
|`Shell`|文字列の配列|シェル形式の RUN、CMD、ENTRYPOINT を表示します。|
{: caption="表。" caption-side="top"}

#### Healthcheck

|フィールド|タイプ|説明|
|-----|----|-----------|
|`Test`|文字列の配列|ヘルス・チェック・テストの実行方法を表示します。使用可能なオプションは以下のとおりです。<ul><li>{}: ヘルス・チェックを継承</li><li>{"NONE"}: ヘルス・チェックは無効</li><li>{"CMD", args...}: 引数を直接実行</li><li>{"CMD-SHELL", command}: システムのデフォルト・シェルでコマンドを実行</li></ul>|
|`Interval`|整数 (64 ビット)|2 つのヘルス・チェック間の待ち時間をナノ秒で表示します。|
|`Timeout`|整数 (64 ビット)|ヘルス・チェックが失敗したと見なすまでの待ち時間をナノ秒で表示します。|
|`Retries`|整数|コンテナーが正常でないと見なすために必要な連続失敗回数を表示します。|
{: caption="表 4. Healthcheck 構造体で使用可能なフィールドとデータ・タイプ。" caption-side="top"}

#### RootFS

|オプション|タイプ|説明|
|------|----|-----------|
|`Type`|文字列|ファイル・システムのタイプを表示します。|
|`Layers`|文字列の配列|各イメージ・レイヤーの記述子を表示します。|
|`BaseLayer`|文字列|イメージ内の基本レイヤーの記述子を表示します。|
{: caption="表 5. RootFS 構造体で使用可能なフィールドとデータ・タイプ。" caption-side="top"}

### `bx cr token-list` コマンド内の Go テンプレートのオプションおよびデータ・タイプ
{: #registry_cli_listing_tokenlist}

以下の表を検討して、`bx cr token-list` コマンドで使用可能な、Go テンプレートのオプションおよびデータ・タイプを見つけてください。
{:shortdesc}

|フィールド|タイプ|説明|
|-----|----|-----------|
|`ID`|文字列|トークンの固有 ID を表示します。|
|`Expiry`|整数 (64 ビット)|トークンが期限切れになる時刻の [UNIX タイム・スタンプ](https://en.wikipedia.org/wiki/Unix_time)を表示します。
|
|`ReadOnly`|ブール|イメージのプルのみを実行できる場合は _true_ を表示し、名前空間へのイメージのプッシュ、および名前空間からのイメージのプルを実行できる場合は _false_ を表示します。|
|`Description`|文字列|トークンの説明を表示します。|
{: caption="表 6. bx cr token-list コマンドで使用可能なフィールドとデータ・タイプ。" caption-side="top"}
