---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

# {{site.data.keyword.registrylong_notm}} へのアクセスの自動化
{: #registry_access}

{{site.data.keyword.iamlong}} (IAM) API キーを使用して、{{site.data.keyword.registrylong_notm}} 名前空間へのアクセスを自動化し、イメージのプッシュとプルを可能にすることができます。
{:shortdesc}

Kubernetes デプロイメントでレジストリーのイメージを使用しようとしていますか? [他の Kubernetes 名前空間、{{site.data.keyword.cloud_notm}} 地域、アカウント内のイメージへのアクセス](/docs/containers?topic=containers-images#other)を確認してください。
{: tip}

API キーはアカウントにリンクされているので、{{site.data.keyword.cloud_notm}} 全体で使用できます。そのため、サービスごとに別の資格情報を使用する必要がありません。 API キーを CLI または自動ログインの中でユーザー ID として使用できます。

API キーを使用すると、IAM ポリシーを使用して名前空間へのアクセスを制御できます。 詳しくは、[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry?topic=registry-user#user)を参照してください。

{{site.data.keyword.registrylong_notm}} API キーについて詳しくは、[API キーの処理](/docs/iam?topic=iam-manapikey#manapikey)を参照してください。

始めに、[{{site.data.keyword.registrylong_notm}} および Docker CLI をインストールします](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)。

## API キーを使用した名前空間へのアクセスの自動化
{: #registry_api_key}

API キーを使用して、名前空間との間で行う Docker イメージのプッシュとプルを自動化できます。
{:shortdesc}

### API キーの作成
{: #registry_api_key_create}

レジストリーへのログインに使用する API キーを作成します。
{:shortdesc}

ユーザー API キーとサービス ID API キーの両方を作成できます。

- サービス ID API キーを作成するには、[サービス ID の API キーの作成](/docs/iam?topic=iam-serviceidapikeys#create_service_key)を参照してください。
- ユーザー API キーを作成するには、[API キーの作成](/docs/iam?topic=iam-userapikey#create_user_key)を参照してください。

### API キーを使用したアクセスの自動化
{: #registry_api_key_use}

API キーを使用して、{{site.data.keyword.registrylong_notm}} の名前空間へのアクセスを自動化できます。
{:shortdesc}

次の Docker コマンドを実行して、API キーでレジストリーにログインします。 `<your_apikey>` を API キーに置き換え、`<registry_url>` を、名前空間がセットアップされているレジストリーの URL に置き換えてください。

- アジア太平洋北地域でセットアップされている名前空間の場合、`jp.icr.io` を使用
- アジア太平洋南地域でセットアップされている名前空間の場合、`au.icr.io` を使用
- EU 中央部でセットアップされている名前空間の場合、`de.icr.io` を使用
- 英国南部でセットアップされている名前空間の場合、`uk.icr.io` を使用
- 米国南部でセットアップされている名前空間の場合、`us.icr.io` を使用

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

このコマンドの参照情報については、[新しい {{site.data.keyword.cloud_notm}} プラットフォーム API キーの作成](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create)を参照してください。

## すべてのクライアントに対する認証オプション
{: #registry_authentication}

`docker login` コマンドまたは他のレジストリー・クライアントを使用した認証が可能です。
{:shortdesc}

ほとんどのユーザーは、`docker login` をシンプルにするために `ibmcloud cr login` コマンドを使用できますが、自動化を実装している場合や別のクライアントを使用している場合は、手動で認証を行う必要があります。 ユーザー名とパスワードを提示する必要があります。 {{site.data.keyword.registrylong_notm}} では、ユーザー名は、パスワードで提示するシークレットのタイプを示します。

次のユーザー名が有効です。

- `iambearer`: パスワードには IAM アクセス・トークンが含まれています。 このタイプの認証は、存続時間は短いですが、あらゆるタイプの IAM ID から利用できます。
- `iamrefresh`: パスワードには、IAM アクセス・トークンを生成して更新するために内部的に使用される IAM リフレッシュ・トークンが含まれている必要があります。 このタイプの認証は、存続時間が長く、`ibmcloud cr login` コマンドで使用されます。
- `iamapikey`: パスワードは IAM API キーです。 このタイプの認証は、自動化に推奨されるタイプです。 ユーザー API キーまたはサービス ID API キーのどちらでも使用できます。[API キーの作成](#registry_api_key_create)を参照してください。

レジストリーから認証を受けるために `docker` コマンドを使用する必要はありません。 例えば、以下のように Cloud Foundry CLI を使用してレジストリー内のイメージから Cloud Foundry アプリを開始できます。

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

`<apikey>` を API キーに、`<region>` を[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)の名前に、`<my_namespace>` を名前空間に、`<image_repo>` をリポジトリーに置き換えてください。

詳しくは、[プライベート・イメージ・レジストリーの使用](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry)を参照してください。
