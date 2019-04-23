---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

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

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.Bluemix_notm}} アカウントのレジストリーとそのリソースを管理するには、`container-registry` CLI プラグイン内に用意されている {{site.data.keyword.registrylong}} CLI を使用できます。
{: shortdesc}

**前提条件**

* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli) をインストールします。 {{site.data.keyword.Bluemix_notm}} CLI を使用してコマンドを実行するための接頭部は、`ibmcloud` です。
* レジストリー・コマンドを実行する前に、`ibmcloud login` コマンドを使用して {{site.data.keyword.Bluemix_notm}} にログインし、アクセス・トークンを生成して、セッションを認証します。

`ibmcloud` CLI および `container-registry` CLI プラグインの更新が使用可能になると、コマンド・ラインに通知が表示されます。 使用可能なすべてのコマンドとフラグを使用できるように、CLI を最新の状態に保つようにしてください。

現行バージョンの `container-registry` CLI プラグインを表示しようとしている場合は、`ibmcloud plugin list` を実行します。

{{site.data.keyword.registrylong_notm}} CLI の使用方法については、[{{site.data.keyword.registrylong_notm}} の概説](/docs/services/Registry?topic=registry-getting-started#getting-started)を参照してください。

一部のコマンドにとって必要な IAM プラットフォームとサービス・アクセス役割について詳しくは、[Identity and Access Management を使用したユーザー・アクセス権限の管理](/docs/services/Registry?topic=registry-iam#iam)を参照してください。

コンテナー・イメージ、名前空間名、(レジストリー・トークンなどの) 説明フィールド、イメージ構成データ (イメージ名やイメージ・ラベルなど) に個人情報を含めないでください。
{:tip}

## `ibmcloud cr api`
{: #bx_cr_api}

コマンドの実行対象のレジストリー API エンドポイントに関する詳細を返します。

```
ibmcloud cr api
```
{: codeblock}

**前提条件**

なし

## `ibmcloud cr build`
{: #bx_cr_build}

{{site.data.keyword.registrylong_notm}} 内で Docker イメージをビルドします。

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
<dt>`DIRECTORY`</dt>
<dd>Dockerfile と前提条件ファイルが含まれているビルド・コンテキストの場所。 作業ディレクトリーをビルド・コンテキストの保管場所に設定した状態でコマンドを実行する場合は、`DIRECTORY` をピリオド (.) に置換できます。</dd>
<dt>`--no-cache`</dt>
<dd>(オプション) 指定した場合、キャッシュされている前のビルドのイメージ・レイヤーはこのビルドに使用されません。</dd>
<dt>`--pull`</dt>
<dd>(オプション) 指定した場合、タグが一致するイメージがビルド・ホスト上に既に存在していても、基本イメージがプルされます。</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(オプション) 指定されている場合、エラーが発生しない限り、ビルド出力は抑止されます。</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(オプション) 「``」の形式で追加のビルド引数を指定します。 このパラメーターを複数回指定して複数のビルド引数を指定することができます。 キーに一致する ARG 行を Dockerfile 内に指定すれば、各ビルド引数の値を環境変数として使用できます。</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(オプション) 複数のビルドのために複数の同じファイルを使用する場合は、別の Dockerfile のパスを選択できます。 ビルド・コンテキストに対する Dockerfile の相対位置を指定します。 指定しない場合、デフォルトは `PATH/Dockerfile` です。PATH は、ビルド・コンテキストのルートです。</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>ビルドするイメージのフルネーム。これには、レジストリーの URL と名前空間が含まれます。</dd>
</dl>

**例**

ビルド出力が抑止される、以前のビルドからのビルド・キャッシュを使用しない Docker イメージをビルドします。タグは *`us.icr.io/birds/bluebird:1`* で、ディレクトリーはご使用の作業ディレクトリーです。

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

セキュリティー問題の免除を作成します。 異なるスコープに適用されるセキュリティー問題の免除を作成できます。 スコープは、アカウント、名前空間、リポジトリー、またはタグの中から選択できます。

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>アカウントをスコープとして設定するには、`"*"` を値として使用します。 名前空間、リポジトリー、またはタグをスコープとして設定するには、次の形式のいずれかでその値を入力します: `namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>免除するセキュリティー問題のタイプ。 有効な問題タイプを見つけるには、`ibmcloud cr exemption-types` を実行します。
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>免除するセキュリティー問題の ID。 問題 ID を見つけるには、`ibmcloud cr va <image>` を実行 (`<image>` はイメージの名前) して、**「脆弱性 ID (Vulnerability ID)」**列または**「構成問題 ID (Configuration Issue ID)」**列の関連する値を使用します。
</dd>
</dl>

**例**

`us.icr.io/birds/bluebird` リポジトリー内のすべてのイメージについて、ID が `CVE-2018-17929` の CVE に対して CVE 免除を作成します。

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

ID が `CVE-2018-17929` の CVE に関するアカウント規模の CVE 免除を作成します。

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

タグが `us.icr.io/birds/bluebird:1` の単一のイメージについて、問題 `application_configuration:nginx.ssl_protocols` に対して構成問題の免除を作成します。

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

セキュリティー問題の免除をリストします。

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(オプション) このスコープに適用される免除のみをリストします。 名前空間、リポジトリー、またはタグをスコープとして設定するには、次の形式のいずれかでその値を入力します: `namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
</dl>

**例**

*`birds/bluebird`* リポジトリー内のイメージに適用するセキュリティー問題に関する免除をすべてリストします。 出力には、アカウント規模の免除、*`birds`* 名前空間が適用範囲になる免除、*`birds/bluebird`* リポジトリーは適用範囲になるものの *`birds/bluebird`* リポジトリー内の特定のタグは適用範囲にならない免除が含まれます。

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

セキュリティー問題の免除を削除します。 既存の免除を表示するには、`ibmcloud cr exemption-list` を実行します。

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>アカウントをスコープとして設定するには、`"*"` を値として使用します。 名前空間、リポジトリー、またはタグをスコープとして設定するには、次の形式のいずれかでその値を入力します: `namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>削除するセキュリティー問題の免除の問題タイプ。 免除の問題タイプを見つけるには、`ibmcloud cr exemption-list` を実行します。
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>削除するセキュリティー問題の免除の ID。 免除の問題 ID を見つけるには、`ibmcloud cr exemption-list` を実行します。
</dd>
</dl>

**例**

`us.icr.io/birds/bluebird` リポジトリー内のすべてのイメージについて、ID が `CVE-2018-17929` の CVE に対して CVE 免除を削除します。

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

ID が `CVE-2018-17929` の CVE に関するアカウント規模の CVE 免除を削除します。

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

タグが `us.icr.io/birds/bluebird:1` の単一のイメージについて、問題 `application_configuration:nginx.ssl_protocols` に対して構成問題の免除を削除します。

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

免除できるセキュリティー問題のタイプをリストします。

```
ibmcloud cr exemption-types
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

IAM 認証を使用している場合、このコマンドは微細化された許可を有効にします。 詳しくは、[Identity and Access Management を使用したユーザー・アクセス権限の管理](/docs/services/Registry?topic=registry-iam#iam)と[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry?topic=registry-user#user)を参照してください。

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

ターゲットである {{site.data.keyword.registryshort_notm}} アカウントの IAM ポリシーの状況を表示します。詳しくは、[Identity and Access Management を使用したユーザー・アクセス権限の管理](/docs/services/Registry?topic=registry-iam#iam)と[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry?topic=registry-user#user)を参照してください。

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

特定のイメージに関する詳細を表示します。

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(オプション) Go テンプレートを使用して出力要素のフォーマットを設定します。

詳しくは、[{{site.data.keyword.registrylong_notm}} コマンドの CLI 出力のフォーマット設定およびフィルター操作](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)を参照してください。

</dd>
<dt>`IMAGE`</dt>
<dd>レポートを取得するイメージの名前。 このコマンドに複数のイメージの名前をスペースで区切ってリストすると、複数のイメージの詳細を表示できます。

<p>イメージの名前を調べるには、`ibmcloud cr image-list` を実行します。 **Repository** 列と **Tag** 列の内容を組み合わせると、`repository:tag` の形式のイメージ名になります。 イメージ名の中にタグを指定しない場合は、`latest` というタグが付いたイメージの詳細が表示されます。 </p>

</dd>
</dl>

**例**

フォーマット設定ディレクティブ *`"{{ .Config.ExposedPorts }}"`* を使用して、イメージ *`us.icr.io/birds/bluebird:1`* の公開されているポートに関する詳細を表示します。

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

{{site.data.keyword.Bluemix_notm}} アカウント内のすべてのイメージを表示します。

イメージ名は、**Repository** 列と **Tag** 列の内容を `repository:tag` の形式で組み合わせたものです。
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--no-trunc`</dt>
<dd>(オプション) イメージ・ダイジェストを切り捨てません。</dd>
<dt>`--format FORMAT`</dt>
<dd>(オプション) Go テンプレートを使用して出力要素のフォーマットを設定します。

詳しくは、[{{site.data.keyword.registrylong_notm}} コマンドの CLI 出力のフォーマット設定およびフィルター操作](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)を参照してください。

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(オプション) 各イメージが、`repository:tag` という形式でリストされます。</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(オプション) 指定した名前空間内または名前空間とリポジトリー内のイメージのみを表示するように出力を制限します。 </dd>
<dt>`--include-ibm`</dt>
<dd>(オプション) {{site.data.keyword.IBM_notm}} 提供のパブリック・イメージを出力に含めます。 このオプションを指定しない場合、デフォルトではプライベート・イメージのみがリストされます。</dd>
</dl>

**例**

イメージ・ダイジェストを切り捨てずに、形式 `repository:tag` で *`birds`* 名前空間内のイメージを表示します。

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

指定した 1 つ以上のイメージを {{site.data.keyword.registrylong_notm}} から削除します。

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**

<dl>
<dt>`IMAGE`</dt>
<dd>削除するイメージの名前。 このコマンドに複数のイメージの名前をスペースで区切ってリストすると、複数のイメージを同時に削除できます。 `IMAGE` は `repository:tag` という形式である必要があります。例: `us.icr.io/namespace/image:latest`

<p>イメージの名前を調べるには、`ibmcloud cr image-list` を実行します。 **Repository** 列と **Tag** 列の内容を組み合わせると、`repository:tag` の形式のイメージ名になります。 イメージ名の中にタグを指定しない場合は、`latest` というタグが付いたイメージがデフォルトで削除されます。</p>

</dd>
</dl>

**例**
イメージ `us.icr.io/birds/bluebird:1` を削除します。

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

{{site.data.keyword.registrylong_notm}} で、ソース・イメージ SOURCE_IMAGE を参照する新しいイメージ TARGET_IMAGE を作成します。 ソース・イメージとターゲット・イメージは、同一の領域内になければなりません。

イメージの名前を調べるには、`ibmcloud cr image-list` を実行します。 **Repository** 列と **Tag** 列の内容を組み合わせると、`repository:tag` の形式のイメージ名になります。
{: tip}

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>ソース・イメージの名前。 `SOURCE_IMAGE` は `repository:tag` という形式である必要があります。例: `us.icr.io/namespace/image:latest`

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>ターゲット・イメージの名前。 `TARGET_IMAGE` は `repository:tag` という形式である必要があります。例: `us.icr.io/namespace/image:latest`

</dd>
</dl>

**例**

別のタグ参照 `latest` をイメージ `us.icr.io/birds/bluebird:1` に追加します。

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

イメージ `us.icr.io/birds/bluebird:peck` を同じ名前空間 `birds/pigeon` にある別のリポジトリーにコピーします。

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

イメージ `us.icr.io/birds/bluebird:peck` をアクセス権限のある別の名前空間 `animals` にコピーします。

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

ログインしているレジストリーの名前とアカウントを表示します。

```
ibmcloud cr info
```
{: codeblock}

**前提条件**

なし

## `ibmcloud cr login`
{: #bx_cr_login}

このコマンドはレジストリーに対して `docker login` コマンドを実行します。 レジストリーに対して `docker push` または `docker pull` コマンドを実行するためには、`docker login` コマンドを実行できなければなりません。 その他の `ibmcloud cr` コマンドの実行には、このコマンドは必要ではありません。 Docker がインストールされていない場合、このコマンドはエラー・メッセージを返します。

```
ibmcloud cr login
```
{: codeblock}

**前提条件**

なし

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

名前空間の名前を選択して、{{site.data.keyword.Bluemix_notm}} アカウントに追加します。

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
<dt>`NAMESPACE`</dt>
<dd>追加する名前空間。 名前空間は、同じ地域内のすべての {{site.data.keyword.Bluemix_notm}} アカウントにおいて固有でなければなりません。 名前空間は 4 文字から 30 文字までで、小文字、数字、ハイフン、下線のみを使用しなければなりません。 名前空間は、文字または数値で開始および終了する必要があります。
  
<p>  
<strong>ヒント</strong>: 名前空間名に個人情報を含めないでください。
</p>
  
</dd>
</dl>

**例**

*`birds`* という名前の名前空間を作成します。

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

{{site.data.keyword.Bluemix_notm}} アカウントが所有するすべての名前空間を表示します。

```
ibmcloud cr namespace-list
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

{{site.data.keyword.Bluemix_notm}} アカウントから名前空間を削除します。 名前空間を削除すると、この名前空間内のイメージが削除されます。

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
<dt>`NAMESPACE`</dt>
<dd>削除する名前空間。</dd>
<dt>`--force`, `-f`</dt>
<dd>(オプション) ユーザー・プロンプトを出さずに強制的にコマンドを実行します。</dd>
</dl>

**例**

名前空間 *`birds`* を削除します。

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

価格プランを表示します。

```
ibmcloud cr plan
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

標準プランにアップグレードします。

プランについて詳しくは、[レジストリーのプラン](/docs/services/Registry?topic=registry-registry_overview#registry_plans)を参照してください。

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

**コマンド・オプション**
<dl>
<dt>`PLAN`</dt>
<dd>(オプション) アップグレード先の価格プランの名前。 `PLAN` を指定しない場合、デフォルトは `standard` です。</dd>
</dl>

**例**

標準価格プランにアップグレードします。

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

[IBM お客様向けパスポート・アドバンテージ・オンライン ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/software/passportadvantage/pao_customer.html) からダウンロードした、Helm で使用できるようにパッケージ化された {{site.data.keyword.IBM_notm}} ソフトウェアを、{{site.data.keyword.registrylong_notm}}名前空間にインポートします。

コンテナー・イメージは、プライベート {{site.data.keyword.registryshort_notm}} 名前空間にプッシュされます。 Helm チャートは、このコマンドを実行したディレクトリー内に作成される `ppa-import` ディレクトリーに書き込まれます。 オプションで、[Chart Museum オープン・ソース・プロジェクト ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/helm/charts/tree/master/stable/chartmuseum) を使用して helm チャートをホストできます。

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>IBM パスポート・アドバンテージからダウンロードした圧縮ファイルのパス。</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>所有する名前空間のいずれか。 圧縮ファイルのコンテナー・イメージがこの名前空間にプッシュされます。 名前空間をリストするには、`ibmcloud cr namespace-list` を実行します。</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(オプション) [Chart Museum ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/helm/charts/tree/master/stable/chartmuseum) の固有リソース ID。</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(オプション) [Chart Museum ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/helm/charts/tree/master/stable/chartmuseum) のユーザー名。</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(オプション) [Chart Museum ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/helm/charts/tree/master/stable/chartmuseum) のパスワード。</dd>
</dl>

**例**

IBM ソフトウェアを{{site.data.keyword.registrylong_notm}} 名前空間 *`birds`* 内にインポートし、Helm で使用できるようにパッケージ化します。圧縮ファイルへのパスは *`downloads/compressed_file.tgz`* です。

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

トラフィックおよびストレージの現在の割り当て量、およびそれらの割り当て量に対する使用量の情報を表示します。

```
ibmcloud cr quota
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

指定された割り当て量を変更します。

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} を構成するためのアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_configure)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(オプション) トラフィック割り当て量を、指定した値 (M バイト単位) に変更します。 トラフィックを設定する権限がない場合や現在の価格プランを超える値を設定した場合、操作は失敗します。</dd>
<dt>`--storage STORAGE`</dt>
<dd>(オプション) ストレージ割り当て量を、指定した値 (M バイト単位) に変更します。 ストレージ割り当て量を設定する権限がない場合や現在の価格プランを超える値を設定した場合、操作は失敗します。</dd>
</dl>

**例**

プル・トラフィックの割り当て量制限を *7000* M バイトに設定し、ストレージを *600* M バイトに設定します。

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

ターゲットの地域とレジストリーを表示します。

```
ibmcloud cr region
```
{: codeblock}

**前提条件**

なし

詳しくは、[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)を参照してください。

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

{{site.data.keyword.registrylong_notm}} コマンドのターゲット地域を設定します。 使用可能な地域をリストするには、パラメーターなしでコマンドを実行します。

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**前提条件**

なし

**コマンド・オプション**
<dl>
<dt>`REGION`</dt>
<dd>(オプション) ターゲット地域の名前。例えば、`us-south` などです。

詳しくは、[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)を参照してください。

</dd>
</dl>

**例**

米国南部の地域をターゲットにします。

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-add`
{: #bx_cr_token_add}

レジストリーへのアクセスを制御するために使用できるトークンを追加します。

```
ibmcloud cr token-add [--description DESCRIPTION] [--quiet | -q] [--non-expiring] [--readwrite]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[プラットフォーム管理の役割](/docs/services/Registry?topic=registry-iam#platform_management_roles)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>(オプション) トークンの説明としての値を指定します。これは、`ibmcloud cr token-list` を実行したときに表示されます。 {{site.data.keyword.containerlong_notm}} が自動的に作成するトークンの場合は、Kubernetes クラスター名が説明として設定されます。 この場合、クラスターが削除されると、トークンは自動的に削除されます。
  
<p> 
  <strong>ヒント</strong>: トークンの説明に個人情報を含めないでください。
</p>

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(オプション) 周囲のテキストを含めずに、トークンのみを表示します。</dd>
<dt>`--non-expiring`</dt>
<dd>(オプション) 有効期限なしでアクセスできるトークンを作成します。 このパラメーターを設定しないと、デフォルトでは、トークンからのアクセスは 24 時間後に無効になります。</dd>
<dt>`--readwrite`</dt>
<dd>(オプション) 読み取り権限および書き込み権限を付与するトークンを作成します。 このオプションを指定しないと、デフォルトでは、読み取り専用のアクセスになります。</dd>
</dl>

**例**

トークンと説明 *Token for my account* を追加します。このトークンには有効期限はありません。読み取り/書き込みアクセス権限があります。

```
ibmcloud cr token-add --description "Token for my account" --non-expiring --readwrite
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

指定したトークンをレジストリーから取得します。

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[プラットフォーム管理の役割](/docs/services/Registry?topic=registry-iam#platform_management_roles)を参照してください。

**コマンド・オプション**
<dl>
<dt>`TOKEN`</dt>
<dd>取得するトークンの固有 ID。 トークンをリストするには、`ibmcloud cr token-list` を実行します。</dd>
</dl>

**例**

トークン *10101010-101x-1x10-x1xx-x10xx10xxx10* を取得します。

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

{{site.data.keyword.Bluemix_notm}} アカウント用に存在するすべてのトークンを表示します。

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[プラットフォーム管理の役割](/docs/services/Registry?topic=registry-iam#platform_management_roles)を参照してください。

**コマンド・オプション**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(オプション) Go テンプレートを使用して出力要素のフォーマットを設定します。

詳しくは、[{{site.data.keyword.registrylong_notm}} コマンドの CLI 出力のフォーマット設定およびフィルター操作](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)を参照してください。

</dd>
</dl>

**例**

フォーマット設定ディレクティブ *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`* を使用して、読み取り専用のトークンをすべて表示します。

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

この例は、次の形式で出力を生成します。

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

指定した 1 つ以上のレジストリー・トークンを削除します。

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[プラットフォーム管理の役割](/docs/services/Registry?topic=registry-iam#platform_management_roles)を参照してください。

**コマンド・オプション**
<dl>
<dt>`TOKEN`</dt>
<dd>TOKEN には、トークン自体を指定することもトークンの固有 ID (`ibmcloud cr token-list` で表示されます) を指定することもできます。 複数のトークンをスペースで区切って指定できます。</dd>
<dt>`--force`, `-f`</dt>
<dd>(オプション) ユーザー・プロンプトを出さずに強制的にコマンドを実行します。</dd>
</dl>

**例**

トークン *10101010-101x-1x10-x1xx-x10xx10xxx10* を削除します。

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

イメージの脆弱性評価レポートを表示します。

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**前提条件**

必要な許可について調べるには、[{{site.data.keyword.registrylong_notm}} の使用に関するアクセス役割](/docs/services/Registry?topic=registry-iam#access_roles_using)を参照してください。

**コマンド・オプション**
<dl>
<dt>`IMAGE`</dt>
<dd>レポートを取得するイメージの名前。 このレポートから、既知のパッケージ脆弱性がイメージにあるかどうかがわかります。 このコマンドに複数のイメージの名前をスペースで区切ってリストすると、複数のイメージについてのレポートを同時に要求できます。

<p>イメージの名前を調べるには、`ibmcloud cr image-list` を実行します。 **Repository** 列と **Tag** 列の内容を組み合わせると、`repository:tag` の形式のイメージ名になります。 イメージ名の中にタグを指定しない場合は、`latest` というタグが付いたイメージを評価したレポートになります。</p>

<p>以下のオペレーティング・システムがサポートされています。

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

詳しくは、[脆弱性アドバイザーによるイメージのセキュリティーの管理](/docs/services/va?topic=va-va_index)を参照してください。

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(オプション) 脆弱なパッケージのフィックスについての追加情報をコマンド出力に表示します。</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(オプション) 脆弱性のみを表示するようにコマンド出力を制限します。</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(オプション) 構成の問題のみを表示するようにコマンド出力を制限します。</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(オプション) 選択した形式でコマンド出力が返されます。 デフォルトの形式は `text` です。 以下の形式がサポートされています。

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**例**

イメージの標準的な脆弱性評価レポートを表示します。

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

JSON 形式でイメージ `us.icr.io/birds/bluebird:1` の脆弱性評価レポートを表示します。脆弱性のみ表示されます。

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
