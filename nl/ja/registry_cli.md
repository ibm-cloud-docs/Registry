---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-21"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.Bluemix_notm}} アカウントのレジストリーとそのリソースを管理するには、container-registry プラグイン内に用意されている {{site.data.keyword.registrylong}} CLI を使用できます。
{: shortdesc}

**前提条件**
* レジストリー・コマンドを実行する前に、`ibmcloud login` コマンドを使用して {{site.data.keyword.Bluemix_notm}} にログインし、アクセス・トークンを生成して、セッションを認証します。

{{site.data.keyword.registrylong_notm}} CLI の使用方法については、『[{{site.data.keyword.registrylong_notm}} の概説](index.html)』を参照してください。

コンテナー・イメージ、名前空間名、(レジストリー・トークンなどの) 説明フィールド、イメージ構成データ (イメージ名やイメージ・ラベルなど) に個人情報を含めないでください。
{:tip}


<table summary="{{site.data.keyword.registrylong_notm}} の管理">
<caption>表 1. {{site.data.keyword.registrylong_notm}} を管理するためのコマンド
</caption>
 <thead>
 <th colspan="5">レジストリーを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[`ibmcloud cr api`](#bx_cr_api)</td>
 <td>[`ibmcloud cr build`](#bx_cr_build)</td>
 <td>[`ibmcloud cr exemption-add`](#bx_cr_exemption_add)</td>
 <td>[`ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)](#bx_cr_exemption_list)</td>
 <td>[`ibmcloud cr exemption-rm`](#bx_cr_exemption_rm)</td>
 </tr>
 <tr>
 <td>[`ibmcloud cr exemption-types`](#bx_cr_exemption_types)</td>
 <td>[`ibmcloud cr info`](#bx_cr_info)</td>
 <td>[`ibmcloud cr image-inspect`](#bx_cr_image_inspect)</td>
 <td>[`ibmcloud cr image-list` (`ibmcloud cr images`)](#bx_cr_image_list)</td>
 <td>[`ibmcloud cr image-rm`](#bx_cr_image_rm)</td>
  </tr>
 <tr>
 <td>[`ibmcloud cr login`](#bx_cr_login)</td>
 <td>[`ibmcloud cr namespace-add`](#bx_cr_namespace_add)</td>
 <td>[`ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)](#bx_cr_namespace_list)</td>
 <td>[`ibmcloud cr namespace-rm`](#bx_cr_namespace_rm)</td>
 <td>[`ibmcloud cr plan`](#bx_cr_plan)</td>
 </tr>
 <tr>
 <td>[`ibmcloud cr plan-upgrade`](#bx_cr_plan_upgrade)</td>
 <td>[`ibmcloud cr ppa-archive-load`](#bx_cr_ppa_archive_load)</td>
 <td>[`ibmcloud cr quota`](#bx_cr_quota)</td>
 <td>[`ibmcloud cr quota-set`](#bx_cr_quota_set)</td>
 <td>[`ibmcloud cr region`](#bx_cr_region)</td>
 </tr><tr>
 <td>[`ibmcloud cr region-set`](#bx_cr_region_set)</td>
 <td>[`ibmcloud cr token-add`](#bx_cr_token_add)</td>
 <td>[`ibmcloud cr token-get`](#bx_cr_token_get)</td>
 <td>[`ibmcloud cr token-list` (`ibmcloud cr tokens`)](#bx_cr_token_list)</td>
 <td>[`ibmcloud cr token-rm`](#bx_cr_token_rm)</td>
  </tr><tr>
  <td>[`ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)](#bx_cr_va)</td>
 </tr>
 </tbody></table>



## `ibmcloud cr api`
{: #bx_cr_api}

コマンドの実行対象のレジストリー API エンドポイントに関する詳細を返します。

```
ibmcloud cr api
```
{: codeblock}


## `ibmcloud cr build`
{: #bx_cr_build}

{{site.data.keyword.registrylong_notm}} 内で Docker イメージをビルドします。

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**パラメーター**
<dl>
<dt>`DIRECTORY`</dt>
<dd>Dockerfile と前提条件ファイルが含まれているビルド・コンテキストの場所。</dd>
<dt>`--no-cache`</dt>
<dd>(オプション) 指定した場合、キャッシュされている前のビルドのイメージ・レイヤーはこのビルドに使用されません。</dd>
<dt>`--pull`</dt>
<dd>(オプション) 指定した場合、タグが一致するイメージがビルド・ホスト上に既に存在していても、基本イメージがプルされます。</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(オプション) 指定されている場合、エラーが発生しない限り、ビルド出力は抑止されます。</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(オプション) 「KEY=VALUE」の形式で追加のビルド引数を指定します。 このパラメーターを複数回指定して複数のビルド引数を指定することができます。 キーに一致する ARG 行を Dockerfile 内に指定すれば、各ビルド引数の値を環境変数として使用できます。</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(オプション) 複数のビルドのために複数の同じファイルを使用する場合は、別の Dockerfile のパスを選択できます。 ビルド・コンテキストに対する Dockerfile の相対位置を指定します。 指定しない場合、デフォルトは `PATH/Dockerfile` です。PATH は、ビルド・コンテキストのルートです。</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>ビルドするイメージのフルネーム。これには、レジストリーの URL と名前空間が含まれます。</dd>
</dl>


## `ibmcloud cr info`
{: #bx_cr_info}

ログインしているレジストリーの名前とアカウントを表示します。

```
ibmcloud cr info
```
{: codeblock}


## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

セキュリティー問題の免除を作成します。 異なるスコープに適用されるセキュリティー問題の免除を作成できます。 スコープは、アカウント、名前空間、リポジトリー、またはタグの中から選択できます。 

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**パラメーター**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>アカウントをスコープとして設定するには、`"*"` を値として使用します。 名前空間、リポジトリー、またはタグをスコープとして設定するには、次の形式のいずれかでその値を入力します: `namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>免除するセキュリティー問題のタイプ。 有効な問題タイプを見つけるには、`ibmcloud cr exemption-types` を実行します。
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>免除するセキュリティー問題の ID。 問題 ID を見つけるには、`ibmcloud cr va <image>` を実行 (*&lt;image&gt;* はイメージの名前) して、**「脆弱性 ID (Vulnerability ID)」**列または**「構成問題 ID (Configuration Issue ID)」**列の関連する値を使用します。
</dd>
</dl>


## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

セキュリティー問題の免除をリストします。 

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(オプション) このスコープに適用される免除のみをリストします。 名前空間、リポジトリー、またはタグをスコープとして設定するには、次の形式のいずれかでその値を入力します: `namespace`、`namespace/repository`、`namespace/repository:tag`
</dd>
</dl>


## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

セキュリティー問題の免除を削除します。 既存の免除を表示するには、`ibmcloud cr exemption-list` を実行します。

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**パラメーター**
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


## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

免除できるセキュリティー問題のタイプをリストします。

```
ibmcloud cr exemption-types
```
{: codeblock}


## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

特定のイメージに関する詳細を表示します。

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(オプション) Go テンプレートを使用して出力要素のフォーマットを設定します。

詳しくは、[{{site.data.keyword.registrylong_notm}} コマンドの CLI 出力のフォーマット設定およびフィルター操作](registry_cli_reference.html#registry_cli_listing)を参照してください。

</dd>
<dt>`IMAGE`</dt>
<dd>レポートを取得するイメージの名前。 このコマンドに複数のイメージの名前をスペースで区切ってリストすると、複数のイメージの詳細を表示できます。

<p>イメージの名前を調べるには、`ibmcloud cr image-list` を実行します。 **Repository** 列と **Tag** 列の内容を組み合わせると、`repository:tag` の形式のイメージ名になります。イメージ名の中にタグを指定しない場合は、`latest` というタグが付いたイメージの詳細が表示されます。 </p>

</dd>
</dl>


## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

{{site.data.keyword.Bluemix_notm}} アカウント内のすべてのイメージを表示します。

イメージ名は、<strong>Repository</strong> 列と <strong>Tag</strong> 列の内容を `repository:tag` の形式で組み合わせたものです。
{:tip}

```
 ibmcloud cr image-list [--no-trunc] [--format FORMAT] [-q, --quiet] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`--no-trunc`</dt>
<dd>(オプション) イメージ・ダイジェストを切り捨てません。</dd>
<dt>`--format FORMAT`</dt>
<dd>(オプション) Go テンプレートを使用して出力要素のフォーマットを設定します。

詳しくは、[{{site.data.keyword.registrylong_notm}} コマンドの CLI 出力のフォーマット設定およびフィルター操作](registry_cli_reference.html#registry_cli_listing)を参照してください。

</dd>
<dt>`-q`, `--quiet`</dt>
<dd>(オプション) 各イメージが、`repository:tag` という形式でリストされます。</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(オプション) 指定した名前空間内または名前空間とリポジトリー内のイメージのみを表示するように出力を制限します。 </dd>
<dt>`--include-ibm`</dt>
<dd>(オプション) {{site.data.keyword.IBM_notm}} 提供のパブリック・イメージを出力に含めます。 このオプションを指定しない場合、デフォルトではプライベート・イメージのみがリストされます。</dd>
</dl>



## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

指定した 1 つ以上のイメージをレジストリーから削除します。

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`IMAGE`</dt>
<dd>レポートを取得するイメージの名前。 このコマンドに複数のイメージの名前をスペースで区切ってリストすると、複数のイメージを同時に削除できます。

<p>イメージの名前を調べるには、`ibmcloud cr image-list` を実行します。 **Repository** 列と **Tag** 列の内容を組み合わせると、`repository:tag` の形式のイメージ名になります。イメージ名の中にタグを指定しない場合は、`latest` というタグが付いたイメージがデフォルトで削除されます。</p>

</dd>
</dl>


## `ibmcloud cr login`
{: #bx_cr_login}

このコマンドはレジストリーに対して `docker login` コマンドを実行します。 レジストリーに対して `docker push` または `docker pull` コマンドを実行するためには、`docker login` コマンドを実行できなければなりません。 その他の `ibmcloud cr` コマンドの実行には、このコマンドは必要ではありません。 Docker がインストールされていない場合、このコマンドはエラー・メッセージを返します。

```
ibmcloud cr login
```
{: codeblock}


## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

{{site.data.keyword.Bluemix_notm}} アカウントに名前空間を追加します。

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**パラメーター**
<dl>
<dt>`NAMESPACE`</dt>
<dd>追加する名前空間。 名前空間は、同じ地域内のすべての {{site.data.keyword.Bluemix_notm}} アカウントにおいて固有でなければなりません。
  
<p>  
<strong>ヒント</strong>: 名前空間名に個人情報を含めないでください。
</p>
  
</dd>
</dl>


## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

{{site.data.keyword.Bluemix_notm}} アカウントが所有するすべての名前空間を表示します。

```
ibmcloud cr namespace-list
```
{: codeblock}


## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

{{site.data.keyword.Bluemix_notm}} アカウントから名前空間を削除します。 名前空間を削除すると、この名前空間内のイメージが削除されます。

```
ibmcloud cr namespace-rm NAMESPACE
```
{: codeblock}

**パラメーター**
<dl>
<dt>`NAMESPACE`</dt>
<dd>削除する名前空間。</dd>
</dl>


## `ibmcloud cr plan`
{: #bx_cr_plan}

価格プランを表示します。

```
ibmcloud cr plan
```
{: codeblock}


## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

標準プランにアップグレードします。

プランについて詳しくは、[レジストリーのプラン](registry_overview.html#registry_plans)を参照してください。

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`PLAN`</dt>
<dd>アップグレード先の価格プランの名前。 `PLAN` を指定しない場合、デフォルトは `standard` です。</dd>
</dl>


## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

[IBM お客様向けパスポート・アドバンテージ・オンライン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/software/passportadvantage/pao_customer.html) からダウンロードした、Helm で使用できるようにパッケージ化された IBM ソフトウェアを、プライベート・レジストリー名前空間にインポートします。

コンテナー・イメージは、プライベート {{site.data.keyword.registryshort_notm}} 名前空間にプッシュされます。 Helm チャートは、このコマンドを実行したディレクトリー内に作成される `ppa-import` ディレクトリーに書き込まれます。 オプションで、[Chart Museum オープン・ソース・プロジェクト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) を使用して helm チャートをホストできます。

**コマンド例**

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**パラメーター**:
<dl>
  <dt>`--archive FILE`</dt>
  <dd>IBM パスポート・アドバンテージからダウンロードした圧縮ファイルのパス。</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>所有する名前空間のいずれか。 圧縮ファイルのコンテナー・イメージがこの名前空間にプッシュされます。 名前空間をリストするには、`ibmcloud cr namespace-list` を実行します。</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(オプション) [Chart Museum ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) の固有リソース ID。</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(オプション) [Chart Museum ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) のユーザー名。</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(オプション) [Chart Museum ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) のパスワード。</dd>
</dl>


## `ibmcloud cr quota`
{: #bx_cr_quota}

トラフィックおよびストレージの現在の割り当て量、およびそれらの割り当て量に対する使用量の情報を表示します。

```
ibmcloud cr quota
```
{: codeblock}


## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

指定された割り当て量を変更します。

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(オプション) トラフィック割り当て量を、指定した値 (M バイト単位) に変更します。 トラフィックを設定する権限がない場合や現在の価格プランを超える値を設定した場合、操作は失敗します。</dd>
<dt>`--storage STORAGE`</dt>
<dd>(オプション) ストレージ割り当て量を、指定した値 (M バイト単位) に変更します。 ストレージ割り当て量を設定する権限がない場合や現在の価格プランを超える値を設定した場合、操作は失敗します。</dd>
</dl>


## `ibmcloud cr region`
{: #bx_cr_region}

ターゲットの地域とレジストリーを表示します。

```
ibmcloud cr region
```
{: codeblock}

詳しくは、[地域](registry_overview.html#registry_regions)を参照してください。


## `ibmcloud cr region-set`
{: #bx_cr_region_set}

{{site.data.keyword.registrylong_notm}} コマンドのターゲット地域を設定します。 使用可能な地域をリストするには、パラメーターなしでコマンドを実行します。

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`REGION`</dt>
<dd>(オプション) ターゲット地域の名前。例えば、`us-south` などです。

詳しくは、[地域](registry_overview.html#registry_regions)を参照してください。

</dd>
</dl>


## `ibmcloud cr token-add`
{: #bx_cr_token_add}

レジストリーへのアクセスを制御するために使用できるトークンを追加します。

```
ibmcloud cr token-add [--description DESCRIPTION] [-q, --quiet] [--non-expiring] [--readwrite]
```
{: codeblock}


**パラメーター**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>(オプション) トークンの説明としての値を指定します。これは、`ibmcloud cr token-list` を実行したときに表示されます。 {{site.data.keyword.containerlong_notm}} が自動的に作成するトークンの場合は、Kubernetes クラスター名が説明として設定されます。 この場合、クラスターが削除されると、トークンは自動的に削除されます。
  
<p> 
  <strong>ヒント</strong>: Do not put personal information in your token description.
</p>

  </dd>
<dt>`-q`, `--quiet`</dt>
<dd>(オプション) 周囲のテキストを含めずに、トークンのみを表示します。</dd>
<dt>`--non-expiring`</dt>
<dd>(オプション) 有効期限なしでアクセスできるトークンを作成します。 このパラメーターを設定しないと、デフォルトでは、トークンからのアクセスは 24 時間後に無効になります。</dd>
<dt>`--readwrite`</dt>
<dd>(オプション) 読み取り権限および書き込み権限を付与するトークンを作成します。 このオプションを指定しないと、デフォルトでは、読み取り専用のアクセスになります。</dd>
</dl>


## `ibmcloud cr token-get`
{: #bx_cr_token_get}

指定したトークンをレジストリーから取得します。

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**パラメーター**
<dl>
<dt>`TOKEN`</dt>
<dd>(オプション) 取得するトークンの固有 ID。</dd>
</dl>


## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

{{site.data.keyword.Bluemix_notm}} アカウント用に存在するすべてのトークンを表示します。

```
ibmcloud cr token-list --format FORMAT
```
{: codeblock}

**パラメーター**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(オプション) Go テンプレートを使用して出力要素のフォーマットを設定します。

詳しくは、[{{site.data.keyword.registrylong_notm}} コマンドの CLI 出力のフォーマット設定およびフィルター操作](registry_cli_reference.html#registry_cli_listing)を参照してください。

</dd>
</dl>


## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

指定した 1 つ以上のトークンを削除します。

```
ibmcloud cr token-rm TOKEN [TOKEN...]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`TOKEN`</dt>
<dd>(オプション) TOKEN には、トークン自体を指定することもトークンの固有 ID (`ibmcloud cr token-list` で表示されます) を指定することもできます。 複数のトークンをスペースで区切って指定できます。</dd>
</dl>


## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

イメージの脆弱性評価レポートを表示します。

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**パラメーター**
<dl>
<dt>`IMAGE`</dt>
<dd>レポートを取得するイメージの名前。 このレポートから、既知のパッケージ脆弱性がイメージにあるかどうかがわかります。 このコマンドに複数のイメージの名前をスペースで区切ってリストすると、複数のイメージについてのレポートを同時に要求できます。

<p>イメージの名前を調べるには、`ibmcloud cr image-list` を実行します。 **Repository** 列と **Tag** 列の内容を組み合わせると、`repository:tag` の形式のイメージ名になります。イメージ名の中にタグを指定しない場合は、`latest` というタグが付いたイメージを評価したレポートになります。 </p>

<p>以下のオペレーティング・システムがサポートされています。

<ul>

<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>

</p>

詳しくは、[脆弱性アドバイザーによるイメージのセキュリティーの管理](/docs/services/va/va_index.html)を参照してください。

</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(オプション) 選択した形式でコマンド出力が返されます。 デフォルトの形式は `text` です。 以下の形式がサポートされています。

<ul>

<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(オプション) 脆弱性のみを表示するようにコマンド出力を制限します。</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(オプション) 構成の問題のみを表示するようにコマンド出力を制限します。</dd>
<dt>`--extended`, `-e`</dt>
<dd>(オプション) 脆弱なパッケージのフィックスについての追加情報をコマンド出力に表示します。</dd>

</dl>
