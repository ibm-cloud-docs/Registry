---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# {{site.data.keyword.registrylong_notm}} へのアクセスの自動化
{: #registry_access}

レジストリー・トークンまたは {{site.data.keyword.iamlong}} (IAM) API キーを使用して、{{site.data.keyword.registrylong_notm}} 名前空間へのアクセスを自動化し、イメージのプッシュとプルを可能にすることができます。
{:shortdesc}

Kubernetes デプロイメントでレジストリーのイメージを使用しようとしていますか? [他の Kubernetes 名前空間、{{site.data.keyword.Bluemix_notm}} 地域、アカウント内のイメージへのアクセス](/docs/containers/cs_images.html#other)を確認してください。
{: tip}

API キーはアカウントにリンクされているので、{{site.data.keyword.Bluemix_notm}} 全体で使用できます。そのため、サービスごとに別の資格情報を使用する必要がありません。 API キーを CLI または自動ログインの中でユーザー ID として使用できます。

レジストリー・トークンの有効範囲は、{{site.data.keyword.registrylong_notm}} のみです。 レジストリー・トークンは、読み取り専用アクセスに制限したり、有効期限の有無を設定したりできます。

API キーを使用すると、IAM ポリシーを使用して名前空間へのアクセスを制御できます。詳しくは、[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry/registry_users.html#user)を参照してください。

{{site.data.keyword.registrylong_notm}} API キーについて詳しくは、[API キーの処理](/docs/iam/apikeys.html#manapikey)を参照してください。

始めに、[{{site.data.keyword.registrylong_notm}} および Docker CLI をインストールします](registry_setup_cli_namespace.html#registry_cli_install)。

## API キーを使用した名前空間へのアクセスの自動化
{: #registry_api_key}

API キーを使用して、名前空間との間で行う Docker イメージのプッシュとプルを自動化できます。
{:shortdesc}

### API キーの作成
{: #registry_api_key_create}

レジストリーへのログインに使用する API キーを作成します。
{:shortdesc}

ユーザー API キーとサービス ID API キーの両方を作成できます。

- サービス ID API キーを作成するには、[サービス ID の API キーの作成](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id)を参照してください。
- ユーザー API キーを作成するには、[API キーの作成](/docs/iam/userid_keys.html#creating-an-api-key)を参照してください。

### API キーを使用したアクセスの自動化
{: #registry_api_key_use}

API キーを使用して、{{site.data.keyword.registrylong_notm}} の名前空間へのアクセスを自動化できます。
{:shortdesc}

次の Docker コマンドを実行して、API キーでレジストリーにログインします。 &lt;your_apikey&gt; を API キーに置き換え、&lt;registry_url&gt; を名前空間がセットアップされているレジストリーの URL に置き換えてください。

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

このコマンドの参照情報については、[新しい {{site.data.keyword.Bluemix_notm}} プラットフォーム API キーの作成](/docs/cli/reference/ibmcloud/cli_api_policy.html#ibmcloud_iam_api_key_create)を参照してください。

## トークンを使用した名前空間へのアクセスの自動化
{: #registry_tokens}

トークンを使用して、{{site.data.keyword.registrylong_notm}} 名前空間との間で行う Docker イメージのプッシュとプルを自動化できます。
{:shortdesc}

レジストリー・トークンを所有していれば、だれでも保護された情報にアクセスできます。 {{site.data.keyword.Bluemix_notm}} アカウント用のトークンを作成して、領域にセットアップしたすべての名前空間へのアクセスを、{{site.data.keyword.Bluemix_notm}} アカウント外部のユーザーに付与することができます。 このトークンを所有するすべてのユーザーまたはアプリは、container-registry プラグインをインストールせずに、名前空間にイメージをプッシュしたり名前空間からイメージをプルしたりすることができます。

{{site.data.keyword.Bluemix_notm}} アカウント用のトークンを作成する際に、そのトークンがレジストリーへの読み取り専用アクセス (プル) を許可するのか、それとも書き込みアクセス (プッシュおよびプル) を許可するのかを決定できます。 また、トークンを永続的にするか、または 24 時間後に期限切れするかについても指定できます。 複数のトークンを作成および使用して、さまざまなタイプのアクセスを制御することができます。

レジストリー・トークンを使用して {{site.data.keyword.registrylong_notm}} にログインする場合には、IAM アクセス・ポリシーは適用されません。自動化に使用する ID を対象に 1 つ以上の名前空間にアクセスを制限しようとしている場合は、レジストリー・トークンではなく IAM サービス ID の API キーを使用することを考慮してください。API キーの作成と、{{site.data.keyword.registrylong_notm}} での使用について詳しくは、[API キーを使用した名前空間へのアクセスの自動化](#registry_api_key)を参照してください。

以下のタスクを使用してトークンを管理します。

- [{{site.data.keyword.Bluemix_notm}} アカウントのトークンの作成](#registry_tokens_create)
- [トークンを使用した名前空間へのアクセスの自動化](#registry_tokens_use)
- [{{site.data.keyword.Bluemix_notm}} アカウントのトークンの削除](#registry_tokens_remove)

### {{site.data.keyword.Bluemix_notm}} アカウント用のトークンの作成
{: #registry_tokens_create}

領域内のすべての {{site.data.keyword.registrylong_notm}} 名前空間へのアクセスを付与するトークンを作成できます。
{:shortdesc}

1. トークンを作成します。 以下の例は、領域内にセットアップされているすべての名前空間への読み取りおよび書き込みアクセスを持つ、有効期限がないトークンを作成します。

   ```
   ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
   ```
   {: pre}

   <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="電球アイコン"/> このコマンドの構成要素の説明</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>オプションです。 このオプションを使用して、後でより容易に識別できるようにトークンを記述します。</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>オプションです。 このオプションを使用して、有効期限がないトークンを作成します。 このオプションを指定しないと、トークンは 24 時間後に無効になります。 <br> **ヒント:** 名前空間へのアクセスをブロックするための有効期限がないトークンが不要になったら、必ずそのトークンを削除してください。</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>オプションです。 このオプションを使用して、ユーザーが名前空間にイメージをプッシュしたり名前空間からイメージをプルすることを可能にするトークンを作成します。 このオプションを指定しないと、トークンは、イメージをプルするためにのみ使用できます。</td>
        </tr>
        </tbody>
   </table>

   CLI 出力は、以下のような出力になります。

   ```
   Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
    Token              <token_value>
   ```
   {: screen}

2. トークンが作成されたことを確認します。

   ```
   ibmcloud cr token-list
   ```
   {: pre}

### トークンを使用した名前空間へのアクセスの自動化
{: #registry_tokens_use}

`docker login` コマンドでトークンを使用して、{{site.data.keyword.registrylong_notm}} の名前空間へのアクセスを自動化することができます。 トークンに読み取り専用アクセスを設定するか、または読み取り/書き込みアクセスを設定するかに応じて、ユーザーは、名前空間にイメージをプッシュしたり、名前空間からイメージをプルしたりすることができます。
{:shortdesc}

1. {{site.data.keyword.Bluemix_notm}} にログインします。

   ```
   ibmcloud login
   ```
   {: pre}

2. {{site.data.keyword.Bluemix_notm}} アカウント内のすべてのトークンをリストし、使用するトークン ID をメモします。

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. トークンのトークン値を取得します。 &lt;token_id&gt; は、トークンの ID に置換してください。

   ```
   ibmcloud cr token-get <token_id>
   ```
   {: pre}

    CLI 出力の**「トークン」**に、トークン値が表示されます。

4. トークンを `docker login` コマンドの一部として使用します。 &lt;token_value&gt; を、前の手順で取得したトークン値に置換し、&lt;registry_url&gt; を、名前空間がセットアップされているレジストリーの URL に置換します。

   - 米国南部でセットアップされている名前空間の場合、`registry.ng.bluemix.net` を使用
   - 英国南部でセットアップされている名前空間の場合、`registry.eu-gb.bluemix.net` を使用
   - EU 中央部でセットアップされている名前空間の場合、`registry.eu-de.bluemix.net` を使用
   - アジア太平洋南地域でセットアップされている名前空間の場合、`registry.au-syd.bluemix.net` を使用

   ```
   docker login -u token -p <token_value> <registry_url>
   ```
   {: pre}

   `-u` パラメーターの場合、トークン ID ではなくストリング `token` を入力してください。
   {: tip}

   トークンを使用して Docker にログインすると、名前空間にイメージをプッシュしたり、名前空間からイメージをプルしたりすることができます。

### {{site.data.keyword.Bluemix_notm}} アカウントからのトークンの削除
{: #registry_tokens_remove}

{{site.data.keyword.registrylong_notm}} トークンが不要になったら、削除します。
{:shortdesc}

有効期限が切れた {{site.data.keyword.registrylong_notm}} トークンは {{site.data.keyword.Bluemix_notm}} アカウントから自動的に削除されるため、手動で削除する必要はありません。
{:tip}

1. {{site.data.keyword.Bluemix_notm}} にログインします。

   ```
   ibmcloud login
   ```
   {: pre}

2. {{site.data.keyword.Bluemix_notm}} アカウント内のすべてのトークンをリストし、削除するトークン ID をメモします。

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. トークンを削除します。

   ```
   ibmcloud cr token-rm <token_id>
   ```
   {: pre}

## すべてのクライアントに対する認証オプション
{: #registry_authentication}

`docker login` コマンドまたは他のレジストリー・クライアントを使用した認証が可能です。
{:shortdesc}

ほとんどのユーザーは、`docker login` をシンプルにするために `ibmcloud cr login` コマンドを使用できますが、自動化を実装している場合や別のクライアントを使用している場合は、手動で認証を行う必要があります。 ユーザー名とパスワードを提示する必要があります。 {{site.data.keyword.registrylong_notm}} では、ユーザー名は、パスワードで提示するシークレットのタイプを示します。

次のユーザー名が有効です。

- `iambearer`: パスワードには IAM アクセス・トークンが含まれています。 このタイプの認証は、存続時間は短いですが、あらゆるタイプの IAM ID から利用できます。
- `iamrefresh`: パスワードには、IAM アクセス・トークンを生成して更新するために内部的に使用される IAM リフレッシュ・トークンが含まれている必要があります。 このタイプの認証は、存続時間が長く、`ibmcloud cr login` コマンドで使用されます。
- `iamapikey`: パスワードは IAM API キーです。 このタイプの認証は、自動化に推奨されるタイプです。 ユーザー API キーまたはサービス ID API キーのどちらでも使用できます。[API キーの作成](#registry_api_key_create)を参照してください。
- `token`: パスワードはレジストリー・トークンです。 このユーザー名は自動化に使用できます。

レジストリーから認証を受けるために `docker` コマンドを使用する必要はありません。 例えば、以下のように Cloud Foundry CLI を使用してレジストリー内のイメージから Cloud Foundry アプリを開始できます。

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o registry.<region>.bluemix.net/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

_&lt;apikey&gt;_ を API キーに、_&lt;region&gt;_ を[領域](registry_overview.html#registry_regions)の名前に、_&lt;my_namespace&gt;_ を名前空間に、_&lt;image_repo&gt;_ をリポジトリーに置き換えてください。

詳しくは、[プライベート・イメージ・レジストリーの使用](/docs/services/ContinuousDelivery/pipeline_custom_docker_images.html#private_image_registry)を参照してください。
