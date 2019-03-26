---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, Docker Content Trust, keys, trusted content, signing, signing images, repository keys, 

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

# 信頼できるコンテンツのイメージへの署名
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} は、信頼できるコンテンツのテクノロジーを備えているので、レジストリー名前空間内のイメージに署名してイメージの完全性を保証できます。 署名付きのイメージをプル/プッシュすることで、イメージをプッシュしたのが継続的統合 (CI) ツールなどの正当なパーティーであることを検証できます。 この機能を使用するには、Docker バージョン 18.03 以降が必要です。 詳しくは、[Docker のコンテント・トラスト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/engine/security/trust/content_trust/) および [Notary プロジェクト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/theupdateframework/notary) の資料を参照してください。
{:shortdesc}

信頼できるコンテンツを有効にしてイメージをプッシュすると、Docker クライアントが、署名付きのメタデータ・オブジェクトも {{site.data.keyword.Bluemix_notm}} トラスト・サーバーにプッシュします。 Docker コンテント・トラストを有効にしてタグ付きのイメージをプルしようとすると、Docker クライアントが、要求されたタグの署名付きの最新バージョンをトラスト・サーバーに確認し、コンテンツの署名を検証し、署名付きのイメージをダウンロードします。

イメージ名は、リポジトリーとタグで構成されます。 信頼できるコンテンツを使用する場合は、リポジトリーごとに固有の署名鍵が使用されます。 特定のリポジトリー内のすべてのタグに、そのリポジトリーに属する鍵が使用されます。 複数のチームが {{site.data.keyword.registrylong_notm}} 名前空間内の各チーム用のリポジトリーにコンテンツを公開する場合、チームごとに独自の鍵を使用して自分たちのコンテンツに署名できます。そのため、各イメージが適切なチームによって作成されたことを検証できます。

リポジトリーには、署名ありのコンテンツと署名なしのコンテンツの両方を含められます。 署名のない他のコンテンツが含まれていても、Docker コンテント・トラストを有効にしていれば、リポジトリー内の署名付きのコンテンツにアクセスできます。

イメージに含まれる署名は、古い (`registry.bluemix.net`) ドメイン・ネームと新しい (`icr.io`) ドメイン・ネームとで異なります。 イメージが古いドメイン・ネームかプルされたときは、既存の署名が機能します。 署名ありのコンテンツを新しいドメイン・ネームからプルする場合、新しいドメイン・ネーム `icr.io` のイメージに再度署名する必要があります。[新しいドメイン・ネームのイメージに対する再署名](#trustedcontent_resign)を参照してください。
{: note}

Docker コンテント・トラストでは、「Trust on first use」セキュリティー・モデルが使用されます。 リポジトリーから初めて署名付きのイメージをプルするときに、リポジトリーの鍵がトラスト・サーバーからプルされ、それ以降はその鍵がそのリポジトリーのイメージの検証に使用されます。 初めてリポジトリーをプルする前に、トラスト・サーバー、またはイメージとそのパブリッシャーを信頼することをユーザーが確認する必要があります。 サーバー内のトラスト情報が改ざんされている場合、まだそのリポジトリーからイメージをプルしたことがなければ、Docker クライアントは改ざんされた情報をトラスト・サーバーからプルする可能性があります。 初めてイメージをプルした後にトラスト・データが改ざんされた場合、それ以降のプルでは、Docker クライアントは、改ざんされたデータを検証できないので、イメージをプルしません。 イメージのトラスト・データの詳細を表示する方法について詳しくは、[署名付きのイメージを表示する](#trustedcontent_viewsigned)を参照してください。

「trust on first use」セキュリティー・モデルについて詳しくは、[The Update Framework (TUF) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://theupdateframework.github.io/) を参照してください。

## 信頼できるコンテンツ環境をセットアップする
{: #trustedcontent_setup}

デフォルトでは、Docker コンテント・トラストは無効です。 {{site.data.keyword.registrylong_notm}} にログインして署名付きのイメージを使用する前に、コンテント・トラスト環境を有効にしてください。
{:shortdesc}

1. 端末で Docker コンテント・トラスト環境変数を有効にします。

   Linux または Mac の場合:

   ```
   export DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

   Windows の場合:

   ```
   set DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

2. {{site.data.keyword.Bluemix_notm}} CLI にログインします。

   ```
   ibmcloud login [--sso]
   ```
   {: pre}

   フェデレーテッド ID がある場合は、`ibmcloud login --sso` を使用してログインします。 ユーザー名を入力し、CLI 出力に示された URL を使用してワンタイム・パスコードを取得します。 `--sso` なしではログインに失敗し、`--sso` オプションを指定すると成功する場合、フェデレーテッド ID があることがわかります。
   {: tip}

3. 使用する地域をターゲットにします。 地域名がわからない場合は、地域を指定せずにコマンドを実行してから地域を選択することができます。

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

4. {{site.data.keyword.registrylong_notm}} にログインします。

   ```
   ibmcloud cr login
   ```
   {: pre}

   出力で、Docker コンテント・トラスト環境変数をエクスポートするように指示されます。

   **例**

   ```
   user:~ user$ ibmcloud cr login
   Logging in to 'us.icr.io'...
   Logged in to 'us.icr.io'.

   To set up your Docker client with content trust,
   export the following environment variable:
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: screen}

5. この環境変数コマンドをコピーして端末に貼り付けます。 以下に例を示します。

   ```
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: pre}

これで、信頼できる署名付きのイメージをプッシュ、プル、管理する準備ができました。

Docker コンテント・トラストを有効にしたセッションで、信頼できるコンテンツを無効にした操作 (未署名のイメージをプルするなど) を実行する場合は、コマンドで `--disable-content-trust` フラグを使用してください。
{: tip}

## 署名付きのイメージをプッシュする
{: #trustedcontent_push}

署名付きのイメージを初めてプッシュすると、Docker が自動的に署名鍵のペア (ルートとリポジトリー) を作成します。 署名付きのイメージが前にプッシュされたことがあるリポジトリー内のイメージに署名するには、イメージをプッシュするマシン上に、正しいリポジトリー署名鍵をロードしていなければなりません。
{:shortdesc}

始める前に、[レジストリー名前空間をセットアップします](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add)。

1. [信頼できるコンテンツ環境をセットアップします](#trustedcontent_setup)。

2. [イメージをプッシュします](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)。 信頼できるコンテンツにはタグが必須です。 コマンド出力に、次のように表示されます。

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

3. **署名付きリポジトリーを初めてプッシュする場合**。 署名付きのイメージを新規リポジトリーにプッシュすると、コマンドによってルート鍵とリポジトリー鍵の 2 つの署名鍵が作成され、ローカル・マシンに保管されます。 両方の鍵について安全なパスフレーズを入力して保存し、[鍵をバックアップします](#trustedcontent_backupkeys)。 [リカバリー方法](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent)が限られているので、鍵のバックアップは重要です。

## 署名付きのイメージをプルする
{: #trustedcontent_pull}

Docker コンテント・トラストを有効にした状態で初めて署名付きのイメージをプルすると、Docker クライアントは、その署名を信頼できるものとして認識します。 Docker クライアントは、指定されたイメージの署名付きの最新バージョンをプルします。 署名のないイメージと信頼できないコンテンツはプルされません。
{:shortdesc}

1. [信頼できるコンテンツ環境をセットアップします](#trustedcontent_setup)。

2. イメージをプルします。 `<source_image>` を、イメージのリポジトリーに置き換え、`<tag>` を、イメージに使用するタグ (_latest_ など) に置き換えてください。 プルできるイメージをリストするには、`ibmcloud cr image-list` を実行します。

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    署名付きのイメージをプッシュまたはプルするときにはタグを指定してください。 `latest` タグがデフォルトとして使用されるのは、コンテント・トラストが無効な場合だけです。
    {: tip}

## 新しいドメイン・ネームのイメージに対する再署名
{: #trustedcontent_resign}

新しいドメイン・ネーム `icr.io` のイメージに再度署名するには、そのイメージをプル、タグ設定、およびプッシュする必要があります。
{:shortdesc}

1. 署名付きのイメージを古いドメイン・ネームからプルします。 `<source_image>` を、イメージのリポジトリーに置き換え、`<tag>` を、イメージに使用するタグ (_latest_ など) に置き換えてください。 プルできるイメージをリストするには、`ibmcloud cr image-list` を実行します。

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    署名付きのイメージをプッシュまたはプルするときにはタグを指定してください。 `latest` タグがデフォルトとして使用されるのは、コンテント・トラストが無効な場合だけです。
    {: tip}

2. 新しいドメイン・ネームに対して `docker tag` コマンドを実行します。 `<old_domain_name>` を古いドメイン・ネームに、`<new_domain_name>` を新しいドメイン・ネームに、`<repository>` をリポジトリーの名前に、`<tag>` をタグの名前に置き換えてください。

   ```
   docker tag <old_domain_name>/<repository>:<tag> <new_domain_name>/<repository>:t<tag>
   ```
   {: pre}

3. 新しいドメイン・ネームを使用してイメージをプッシュします。[Docker イメージを名前空間にプッシュする](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)を参照してください。 信頼できるコンテンツにはタグが必須です。 コマンド出力に、次のように表示されます。

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

## 信頼できるコンテンツを管理する
{: #trustedcontent_managetrust}

`docker trust` コマンドを使用して、イメージの署名者を確認したり、トラスト・コンテンツ状況を取り消したりできます。 `docker trust` コマンドを実行するには、Docker 18.03 以降が必要です。
{:shortdesc}

### 署名付きのイメージを表示する
{: #trustedcontent_viewsigned}

鍵 ID や署名者に関する情報を含め、署名付きのバージョンのイメージ・リポジトリーまたはタグを参照できます。
{:shortdesc}

1. [信頼できるコンテンツ環境をセットアップします](#trustedcontent_setup)。

2. 各イメージのタグ、ダイジェスト、署名者情報を参照します。

   (オプション) タグ `<tag>` を指定すると、そのバージョンのイメージに関する情報を表示できます。

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### トラストを取り消す
{: #trustedcontent_revoketrust}

イメージの信頼できるコンテンツ状況を取り消すことができます。
{:shortdesc}

始める前に、[信頼できるリポジトリーを初めてプッシュしたとき](#trustedcontent_push)に保存したリポジトリー鍵のパスフレーズを取得します。 信頼できるイメージに使用された鍵を調べるには、`docker view` [コマンド](#trustedcontent_viewsigned)を使用してください。

1. [信頼できるコンテンツ環境をセットアップします](#trustedcontent_setup)。

2. イメージ・リポジトリーのすべてのトラステッド・メタデータを削除します。 プロンプトが表示されたら、リポジトリー鍵のパスフレーズを入力してください。

   (オプション) タグを指定することで、そのバージョンのイメージのトラステッド・メタデータのみを取り消すことができます。

   ```
   docker trust revoke <image>:<tag>
   ```
   {: pre}

3. 信頼できるコンテンツのリストで、信頼が取り消されたことを確認します。

   (オプション) タグ付きのイメージのコンテンツの信頼が取り消されたことを確認しようとしている場合は、タグを含めます。

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   前述のコマンドからの出力:

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## 署名鍵をバックアップする
{: #trustedcontent_backupkeys}

署名付きのイメージを新規リポジトリーに初めてプッシュすると、Docker コンテント・トラストによってルート鍵とリポジトリー鍵の 2 つの署名鍵が作成され、ローカル・マシンに保管されます。

- Linux および Mac ディレクトリー: `~/.docker/trust/private`

- Windows ディレクトリー: `%HOMEPATH%&#xa5;.docker&#xa5;trust&#xa5;private`

   Docker 構成ディレクトリーを変更した場合は、そこで `trust` サブディレクトリーを探してください。
   {: tip}

すべての鍵、特にルート鍵をバックアップする必要があります。 鍵が失われたり改ざんされたりした場合、[リカバリー方法](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent)は限られています。

鍵をバックアップするには、[Docker コンテント・トラストの資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys) を参照してください。

## 信頼できる署名者の管理
{: #trustedcontent_signers}

リポジトリー内のイメージに署名する署名者を、追加および削除することができます。
{:shortdesc}

### 信頼できるリポジトリーに署名者を追加する
{: #trustedcontent_addsigners}

リポジトリー内のイメージに署名することを他のユーザーに許可するには、そのユーザーの署名鍵をそのリポジトリーに追加します。
{:shortdesc}

**始めに**

- イメージ署名者には、イメージを名前空間にプッシュする権限が必要です。
- リポジトリー所有者および追加の署名者は、Docker 18.03 以降をインストールしておく必要があります。
- [署名付きのイメージをプッシュ](#trustedcontent_push)して、信頼できるコンテンツ・リポジトリーを作成します。 リポジトリー所有者は、自分のローカル・マシン上の Docker トラスト・フォルダーに、リポジトリーのリポジトリー管理者鍵を用意しておく必要があります。 リポジトリー管理者鍵がない場合は、所有者に連絡してこのタスクを実行してもらってください。

署名者を追加すると、リポジトリー管理者鍵はそのリポジトリー内のイメージの署名に使用できなくなります。 署名するには、承認された署名者の秘密鍵が必要になります。 署名者を追加した後もイメージに署名できるようにするには、以下の手順を再実行して自分用の署名者役割を生成して追加してください。
{:tip}

署名鍵を共有するには、以下のようにします。

1. 新規署名者がまだ鍵ペアを生成していない場合は、鍵ペアを生成してロードする必要があります。
  
    a. 鍵を生成します。 `<NAME>` には任意の名前を入力できます。ただし、選択した名前は、だれかがリポジトリーのトラストを検査するときに表示されます。 リポジトリー所有者と一緒に、組織で使用されている命名規則を満たし、かつ、署名者が識別できる名前を選択してください。

      ```
      docker trust key generate <NAME>
      ```
      {: pre}
  
    b. 秘密鍵のパスフレーズを入力します。 公開鍵 (`.pub`) が生成され、対応する秘密鍵が自動的に Docker トラスト構成にロードされます。
  
    c. 新規署名者は、リポジトリー所有者に公開鍵を送信する必要があります。

2. リポジトリー所有者は、署名者の鍵をリポジトリーに追加する必要があります。

    a. [信頼できるコンテンツ環境をセットアップします](#trustedcontent_setup)。

    b. 署名者の鍵をリポジトリーに追加します。

      ```
      docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}

3. 署名者は環境をセットアップし、イメージに署名することができます。

    a. [信頼できるコンテンツ環境をセットアップします](#trustedcontent_setup)。

    b. 署名者はイメージに署名する必要があります。 プロンプトが表示されたら、秘密鍵のパスフレーズを入力します。

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4. 署名者が追加されたことを確認するには、[署名付きのイメージを表示する](#trustedcontent_viewsigned)を参照してください。

### リポジトリーから署名者を削除する
{: #trustedcontent_removesigner}

ある署名者を、リポジトリー内のイメージに署名できないようにするには、その署名者を削除します。
{:shortdesc}

始めに、リポジトリー所有者と追加の署名者は、Docker 18.03 以降をインストールしておく必要があります。

署名者を削除すると、トラスト・サーバーは、その署名者の署名付きのイメージのバージョンを信頼しなくなります。 署名者を削除した後もイメージをプルできるようにするには、その署名者が最新バージョンのイメージに署名していないことを確認してから、作業を進めてください。 署名者が最新バージョンのイメージに署名している場合は、イメージの更新をプッシュし、自分の鍵を使用してそれに署名してから、作業を進めてください。
{:tip}

署名者を削除するには、以下のようにします。

1. [信頼できるコンテンツ環境をセットアップします](#trustedcontent_setup)。

2. 署名者を削除します。

   ```
   docker trust signer remove <NAME> <repository>
   ```
   {: pre}

3. 署名者が削除されたことを確認するために、イメージのトラスト・データを表示し、その署名者がリストされなくなったことを確認します。 トラスト・データの表示方法について詳しくは、[署名付きのイメージを表示する](#trustedcontent_viewsigned)を参照してください。
