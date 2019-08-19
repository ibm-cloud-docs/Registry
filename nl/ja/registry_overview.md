---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, private Docker images, scalable private image registry, regions, plans, billing, registry, service plans, quotas, costs, terminology, glossary, domain names, Docker, global registry, 

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

# {{site.data.keyword.registrylong_notm}} の概要
{: #registry_overview}

{{site.data.keyword.registrylong}} を使用して、可用性が高く、高度にスケーラブルなアーキテクチャーでプライベート Docker イメージを保管およびアクセスします。
{:shortdesc}

{{site.data.keyword.registrylong_notm}} には、{{site.data.keyword.IBM_notm}} によってホストおよび管理されている、マルチテナントの、可用性が高く、スケーラブルで、暗号化された専用イメージ・レジストリーが用意されています。 {{site.data.keyword.registrylong_notm}} を使用し、独自のイメージ名前空間をセットアップして名前空間に Docker イメージをプッシュすることができます。

<img src="images/registry_architecture1.svg" alt="IBM Cloud Container Registry コンテナーとの対話方法を示すイメージ。コンテナー・レジストリーにはプライベート・リポジトリーとパブリック・リポジトリーの両方、およびサービスと対話するための API が含まれています。ローカルの Docker クライアントはレジストリー内のプライベート・リポジトリーへ、またはプライベート・リポジトリーからイメージをプルまたはプッシュでき、パブリック・リポジトリーをプルできます。IBM Cloud の Web UI (コンソール) はコンテナー・レジストリー API と対話してイメージのリストを作成します。コンテナー・レジストリー CLI は API と対話して、イメージおよび他の管理機能の一覧表示、作成、調査、削除を行います。ローカルの Docker クライアントはローカル・イメージ・ストアから他のレジストリーにイメージをプルまたはプッシュすることもできます。"/>

**図 1. {{site.data.keyword.registrylong_notm}} と Docker イメージの対話**

Docker イメージは、作成するすべてのコンテナーの基礎となるものです。 イメージは、Dockerfile (イメージをビルドするための指示が入ったファイル) から作成されます。 Dockerfile の別個に保管されている指示の中で、ビルド成果物 (アプリ、アプリの構成、その従属関係) が参照されることもあります。 イメージは通常、レジストリーに保管されます。だれでもアクセスできるレジストリー (パブリック・レジストリー) を使用することも、小さなグループのユーザーだけにアクセスを限定したレジストリー (専用レジストリー) をセットアップすることもできます。 {{site.data.keyword.registrylong_notm}} を使用することにより、{{site.data.keyword.cloud_notm}} アカウントへのアクセス権を持つユーザーだけが、イメージにアクセスできます。

イメージを {{site.data.keyword.registrylong_notm}} にプッシュする際、潜在的なセキュリティー問題および脆弱性がないかスキャンするための標準装備の脆弱性アドバイザー・フィーチャーが役立ちます。 脆弱性アドバイザーは、特定の Docker 基本イメージ内に脆弱なパッケージがないか、およびアプリ構成設定内に既知の脆弱性がないかをチェックします。 脆弱性が検出されると、その脆弱性に関する情報が提供されます。 この情報を利用してセキュリティー問題を解決することで、脆弱性のあるイメージからコンテナーがデプロイされないようにすることができます。

以下の表を検討して、{{site.data.keyword.registrylong_notm}} を使用した場合の利点の概要を確認してください。

|利点|説明|
|-------|-----------|
|可用性が高く、高度にスケーラブルな専用レジストリー|<ul><li>{{site.data.keyword.IBM_notm}} によってホストおよび管理されている、マルチテナントと、可用性が高く、スケーラブルで、暗号化された専用イメージ・レジストリー内に独自のイメージ名前空間をセットアップする。</li><li>{{site.data.keyword.cloud_notm}} アカウント内にプライベート Docker イメージを保管し、そのアカウント内のユーザーとそれらのイメージを共有する。</li></ul>|
|脆弱性アドバイザーとのイメージ・セキュリティー・コンプライアンス|<ul><li>名前空間にあるイメージの自動スキャンが有用。</li><li>オペレーティング・システム固有の推奨を検討して、潜在的な脆弱性を修正し、コンテナーを不正アクセスから保護する。</li></ul>|
|ストレージおよびプル・トラフィックの割り当て量制限|<ul><li>無料割り当て量に達するまで、ストレージおよびプライベート・イメージのプル・トラフィックを無料で利用できる。</li><li>1 カ月当たりのストレージおよびプル・トラフィック量のカスタム割り当て量制限を設定して、望ましい支払いレベルを超えないようにする。</li></ul>|
{: caption="表 1. {{site.data.keyword.registrylong_notm}} 利点" caption-side="top"}

## サービス・プラン
{: #registry_plans}

無料または標準の {{site.data.keyword.registrylong_notm}} サービス・プランを選択して Docker イメージを保管し、これらのイメージを {{site.data.keyword.cloud_notm}} アカウント内のユーザーが使用できるようにします。
{:shortdesc}

{{site.data.keyword.registrylong_notm}} サービス・プランは、プライベート・イメージに使用できるストレージ量とプル・トラフィックを決定します。 サービス・プランは、{{site.data.keyword.cloud_notm}} アカウントに関連付けられており、ストレージおよびイメージのプル・トラフィックの制限は、アカウント内にセットアップしているすべての名前空間に適用されます。

以下の表は、使用可能な {{site.data.keyword.registrylong_notm}} サービス・プランとそれらの特性を示しています。 課金方法と、サービス・プランの制限を超過した場合の対応について詳しくは、[{{site.data.keyword.registrylong_notm}} の割り当て量制限および課金](#registry_plan_billing)を参照してください。

|特性|無料|標準|
|---------------|----|--------|
|説明|Docker イメージを保管し、共有するために、{{site.data.keyword.registrylong_notm}} をお試しください。 このプランは、{{site.data.keyword.registrylong_notm}} で最初の名前空間をセットアップする際のデフォルトのサービス・プランです。|無制限のストレージおよびプル・トラフィック使用量の利点を享受し、{{site.data.keyword.cloud_notm}} アカウント内のすべての名前空間の Docker イメージを管理します。|
|イメージ用のストレージ量|500 MB|無制限|
|プル・トラフィック|1 カ月当たり 5 GB|無制限|
|請求処理|ストレージまたはプル・トラフィックの制限を超えると、名前空間にイメージをプッシュすることも、名前空間からイメージをプルすることもできなくなります。 詳細については、[{{site.data.keyword.registrylong_notm}} の割り当て量制限および課金](#registry_plan_billing)を参照してください。|<ul><li>ストレージ: 1 カ月当たりの GB 使用量によって料金が請求されます。 最初の 0.5 GB/月は無料です。 その後、オファリングの詳細ページの記載に従って料金が請求されます。[コンテナー・レジストリー![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/kubernetes/catalog/registry) を参照してください。</li><li>プル・トラフィック: 1 カ月当たりの GB 使用量によって料金が請求されます。 最初の 5 GB は無料です。 その後、オファリングの詳細ページの記載に従って料金が請求されます。[コンテナー・レジストリー![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/kubernetes/catalog/registry) を参照してください。 ストレージまたはプル・トラフィックの制限を超えると、名前空間にイメージをプッシュすることも、名前空間からイメージをプルすることもできなくなります。 ストレージ、プル・トラフィック、コスト見積もりツールについて詳しくは、[{{site.data.keyword.registrylong_notm}} の割り当て量制限および課金](#registry_plan_billing)を参照してください。</li></ul>|
{: caption="表 2. {{site.data.keyword.registrylong_notm}} プラン" caption-side="top"}

## 割り当て量制限および請求処理
{: #registry_plan_billing}

{{site.data.keyword.registrylong_notm}} で請求処理と割り当て量制限がどのように機能しているかについての情報および例を示します。
{:shortdesc}

すべてのイメージは、それぞれが基本イメージからの増分変更を表す多くのレイヤーから構築されます。 イメージをプッシュまたはプルすると、各レイヤーに必要なストレージおよびプル・トラフィックの量が、月々の使用量に追加されます。 同一レイヤーは、{{site.data.keyword.cloud_notm}} アカウント内のイメージ間で自動的に共有され、他のイメージを作成する際に再使用されます。 同一のレイヤーのストレージに対する課金は、1 回のみ行われます。そのレイヤーを参照しているアカウント内のイメージ数は関係ありません。

イメージのプッシュの例:

Ubuntu イメージに基づいたイメージを名前空間にプッシュします。 Ubuntu イメージには、複数のレイヤーが含まれています。 アカウント内にはこれらのレイヤーがまだないため、これらのレイヤーに必要なストレージの量が、月々の使用量に追加されます。

その後、Ubuntu イメージに基づいた別のイメージを作成します。 追加のコマンドやファイルを Dockerfile に追加して、Ubuntu 基本イメージに変更を加えます。 それぞれの変更は、新しいイメージ・レイヤーを表しています。 このイメージをプッシュすると、{{site.data.keyword.registrylong_notm}} は、基本の Ubuntu イメージのすべてのレイヤーが既にアカウント内に保管されていることを認識します。 イメージを別の名前空間にプッシュした場合でも、これらのレイヤーの保管に関して 2 度目の課金が行われることはありません。 {{site.data.keyword.registrylong_notm}} は、すべての新しいレイヤーのサイズを判別し、ストレージの量を月々の使用量に追加します。

### ストレージおよびプル・トラフィックの請求処理
{: #registry_billing_traffic}

選択しているサービス・プランに応じて、各地域で 1 カ月当たりに使用するストレージおよびプル・トラフィックに対して課金されます。
{:shortdesc}

#### ストレージ
{: #registry_billing_traffic_storage}

  すべての {{site.data.keyword.registrylong_notm}} サービス・プランには、{{site.data.keyword.cloud_notm}} アカウント内の名前空間に Docker イメージを保管するために使用できる一定量のストレージが付属しています。 標準プランを使用している場合は、1 カ月当たりの GB 使用量によって課金されます。 最初の 0.5 GB/月は無料です。 無料プランを使用している場合は、無料プランの割り当て量制限に達するまで、無料で {{site.data.keyword.registrylong_notm}} にイメージを保管できます。 GB/月は、1 カ月間 (730 時間) での 1 GB ストレージ 1 つの平均です。
{:shortdesc}

  標準プランの例:

  ちょうど半月で 5 GB を使用し、いくつかのイメージを名前空間にプッシュして残りの半月に 10 GB を使用したとします。 この場合、月々の使用量は次のように計算されます。
  
  (5 GB x 0.5 (カ月)) + (10 GB x 0.5 (カ月)) = 2.5 + 5 = 7.5 GB/月
  
  標準プランでは、最初の 0.5 GB/月は無料なので、7 GB/月 (7.5 GB/月 - 0.5 GB/月) に対して課金されます。

#### プル・トラフィック
{: #registry_billing_traffic_pull_traffic}

  すべての {{site.data.keyword.registrylong_notm}} サービス・プランには、名前空間に保管されているプライベート・イメージへの一定量の無料プル・トラフィックが含まれています。 プル・トラフィックとは、名前空間からローカル・マシンにイメージのレイヤーをプルする際に使用する処理能力です。 標準プランを使用している場合は、1 カ月当たりの GB 使用量によって課金されます。 毎月、最初の 5 GB は無料です。 無料プランを使用している場合は、無料プランの割り当て量制限に達するまで、名前空間からイメージをプルできます。
{:shortdesc}

  標準プランの例:

  この月に、レイヤーを含む合計サイズ 14 GB のイメージをプルしたとします。 この場合、月々の使用量は次のように計算されます。
  
  標準プランでは、最初の 5 GB/月は無料のため、9 GB (14 GB - 5 GB) に対して課金されます。

### ストレージおよびプル・トラフィックの割り当て量制限
{: #registry_quota_limits}

選択しているサービス・プランに応じて、各地域のプラン固有の割り当て量制限またはカスタム割り当て量制限に達するまで、名前空間にイメージをプッシュしたり名前空間からイメージをプルしたりすることができます。
{:shortdesc}

#### ストレージ
{: #registry_quota_limits_storage}

  ご使用プランの割り当て量制限に達した場合やその制限を超えた場合は、名前空間から[イメージを削除してスペースを解放する](/docs/services/Registry?topic=registry-registry_quota#registry_quota_freeup)か、[標準プランにアップグレードする](#registry_plan_upgrade)まで、{{site.data.keyword.cloud_notm}} アカウント内の名前空間にイメージをプッシュできなくなります。 無料プランまたは標準プランでストレージの割り当て量制限を設定している場合も、[この割り当て制限を増加](/docs/services/Registry?topic=registry-registry_quota#registry_quota_set)して、新しいイメージのプッシュを再び可能にすることができます。
{:shortdesc}

  標準プランの例:

  ストレージの現在の割り当て量制限は 1 GB に設定されています。 {{site.data.keyword.cloud_notm}} アカウントの名前空間に保管されているすべてのプライベート・イメージで、既にこのストレージの 900 MB が使用されています。 割り当て量制限に達するまでの使用可能なストレージは 100 MB です。 あるユーザーが、2 GB のサイズのイメージをローカル・マシンにプッシュすることを望んでいます。 まだ割り当て量制限に達していないので、{{site.data.keyword.registrylong_notm}} は、ユーザーがこのイメージをプッシュすることを許可します。
  
  このプッシュの後、{{site.data.keyword.registrylong_notm}} は、名前空間内のイメージの実際のサイズ (ローカル・マシン上のサイズと異なる場合がある) を判別し、ストレージの制限に達しているかどうかチェックします。 この例では、ストレージ使用量は 900 MB から 2 GB 増加しています。 現在の割り当て量制限は 1 GB に設定されているため、{{site.data.keyword.registrylong_notm}} は、ユーザーが追加イメージを名前空間にプッシュすることを禁止します。

#### プル・トラフィック
{: #registry_quota_limits_pull_traffic}

  ご使用プランの割り当て量制限に達した場合やその制限を超えた場合は、次回の請求対象期間が開始されるまで待つか、[標準プランにアップグレードするか](#registry_plan_upgrade)、または[プル・トラフィックの割り当て量制限を増加する](/docs/services/Registry?topic=registry-registry_quota#registry_quota_set)まで、{{site.data.keyword.cloud_notm}} アカウント内の名前空間からイメージをプルできなくなります。
{:shortdesc}

  標準プランの例:

  この月に、ユーザーのプル・トラフィックの割り当て量制限は 5 GB に設定されています。 既に名前空間からイメージをプルし、このプル・トラフィックの 4.5 GB を使用しています。 割り当て量制限に達するまでの使用可能なプル・トラフィックは 0.5 GB です。 あるユーザーが、1 GB のサイズのイメージを名前空間からプルすることを望んでいます。 まだ割り当て量制限に達していないので、{{site.data.keyword.registrylong_notm}} は、ユーザーがこのイメージをプルすることを許可します。
  
  イメージがプルされた後、{{site.data.keyword.registrylong_notm}} は、このプルの間に使用された処理能力を判別し、プル・トラフィックの制限に達しているかどうかチェックします。 この例では、プル・トラフィックの使用量は 4.5 GB から 5.5 GB に増加しています。 現在の割り当て量制限は 5 GB に設定されているため、{{site.data.keyword.registrylong_notm}} は、ユーザーが名前空間からイメージをプルすることを禁止します。

### 料金
{: #registry_cost}

オファリングの詳細ページの価格設定プランで {{site.data.keyword.registrylong_notm}} の料金を確認できます。[コンテナー・レジストリー![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/kubernetes/catalog/registry) を参照してください。
{:shortdesc}

## サービス・プランのアップグレード
{: #registry_plan_upgrade}

サービス・プランをアップグレードして、無制限のストレージおよびプル・トラフィック使用量という利点を活用し、{{site.data.keyword.cloud_notm}} アカウント内のすべての名前空間の Docker イメージを管理することができます。
{:shortdesc}

ターゲットにしているレジストリー地域の使用中のサービス・プランを確認するには、`ibmcloud cr plan` コマンドを実行します。
{: tip}

サービス・プランをアップグレードするには、以下の手順を実行します。

1. {{site.data.keyword.cloud_notm}} にログインします。

   ```
   ibmcloud login
   ```
   {: pre}

   フェデレーテッド ID がある場合は、`ibmcloud login --sso` を使用して、{{site.data.keyword.cloud_notm}} CLI にログインします。 ユーザー名を入力し、CLI 出力に示された URL を使用してワンタイム・パスコードを取得します。 フェデレーテッド ID がある場合、`--sso` がなければログインは失敗し、`--sso` オプションを付ければログインが成功します。
{:tip}

2. プランをアップグレードする地域をターゲットにするには、以下のようにします。

   ```
   ibmcloud cr region-set
   ```
   {: pre}

   詳しくは、[`ibmcloud cr region-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) および[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)を参照してください。

3. 標準プランにアップグレードします。

   ```
   ibmcloud cr plan-upgrade standard
   ```
   {: pre}

   {{site.data.keyword.cloud_notm}} Lite アカウントを使用している場合は、`ibmcloud cr plan-upgrade` を実行する前に、{{site.data.keyword.cloud_notm}} の従量課金 (PAYG) アカウントまたはサブスクリプション・アカウントにアップグレードする必要があります。
   {:tip}

   詳しくは、[`ibmcloud cr plan-upgrade`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade) を参照してください。

## {{site.data.keyword.registrylong_notm}} で使用される用語の説明
{: #terms}

{{site.data.keyword.registrylong_notm}} で使用される用語の説明。
{:shortdesc}

<dl>
  <dt>Dockerfile</dt>
  <dd>Dockerfile は、Docker イメージをビルドするための指示が含まれるテキスト・ファイルです。 イメージは通常、基本オペレーティング・システム (Ubuntu など) が含まれる基本イメージを元にビルドされます。 アプリの実行に必要な環境を定義する Dockerfile の指示の基本イメージを徐々に変更することができます。 基本イメージの変更のたびに、イメージの新規レイヤーが記述されます。Dockerfile の単一の行に複数の変更を加えることができます。 Dockerfile 内の指示は、別個に保管されたビルド成果物 (アプリ、アプリの構成、その従属関係など) を参照していることもあります。 Dockerfile の詳細については、[Dockerfile リファレンス![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://docs.docker.com/engine/reference/builder/)を参照してください。</dd>
</dl>

<dl>
  <dt>Docker V2 イメージ</dt>
  <dd>[Docker: Image Manifest V2, Schema 2![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/registry/spec/manifest-v2-2/) に準拠したコンテナー・イメージ。 Docker Image Manifest V2, Schema 2 のメディア・タイプは `application/vnd.docker.distribution.manifest.v2+json` で、マニフェスト・リストのメディア・タイプは `application/vnd.docker.distribution.manifest.list.v2+json` です。 Docker のサポートについて詳しくは、[Docker](/docs/services/Registry?topic=registry-registry_overview#docker) を参照してください。</dd>
</dl>

<dl>
  <dt>イメージ</dt>
  <dd>コンテナーを作成するためにコンテナー・ランタイム内で使用されるファイル・システムおよびその実行パラメーター。 ファイル・システムは、継続的な更新によってイメージが構築されるときに作成され、実行時に結合される一連のレイヤーで構成されます。 コンテナーが実行する際に、イメージの状態は保持されません。</dd>
</dl>

<dl>
  <dt>名前空間</dt>
  <dd>名前空間は、{{site.data.keyword.registrylong_notm}} 内でイメージのリポジトリーを編成する手段です。 名前空間は、{{site.data.keyword.cloud_notm}} アカウントに関連付けられています。 {{site.data.keyword.registrylong_notm}} に独自の名前空間をセットアップすると、その名前空間が次のようにレジストリー URL に付加されます: <code><em>&lt;region&gt;</em>.icr.io/my_namespace</code>。

  {{site.data.keyword.cloud_notm}} アカウントに存在するすべてのユーザーは、対象のレジストリー名前空間に保管されているイメージを表示したり処理したりできます。 複数の名前空間をセットアップし、例えば、実動用とステージング環境用に別々のリポジトリーを用意することができます。</dd>
</dl>

<dl>
  <dt>OCI コンテナー・イメージ</dt>
  <dd>[OCI イメージ・フォーマット仕様![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/opencontainers/image-spec) に準拠したコンテナー・イメージ。 OCI コンテナー・イメージのメディア・タイプは `application/vnd.oci.image.manifest.v1+json` です。</dd>
</dl>

<dl>
  <dt>レジストリー</dt>
  <dd>レジストリーとは、OCI イメージ (別名 Docker イメージ) のためのストレージを提供するサービスです。 OCI イメージは、適切なレジストリー・ドメイン・ネームを使用した OCI クライアントから、取得 (プル) できます。 イメージには、だれでも取得できるもの (パブリック・イメージ) と、特定のグループに取得が制限されたもの (プライベート・イメージ) があります。 {{site.data.keyword.registrylong_notm}} は、{{site.data.keyword.IBM_notm}} がホストおよび管理する、可用性の高いマルチテナント型プライベート・イメージ・レジストリーを提供します。 このレジストリーにアカウント専用の名前空間を追加し、イメージをその名前空間にプッシュすることができます。</dd>
</dl>

<dl>
  <dt>リポジトリー</dt>
  <dd>イメージ・リポジトリーは、レジストリー内に存在する、関連性がありタグ付けされた複数のイメージの集合です。 リポジトリーはイメージと同じ用語としてよく使用されますが、リポジトリーには、1 つのイメージに由来するタグ付けされた複数の異形が含まれることがあります。</dd>
</dl>

<dl>
  <dt>タグ</dt>
  <dd>タグは、リポジトリー内にあるイメージの識別子です。 タグを使用して、リポジトリー内にある同じ基本イメージを持つさまざまなバージョンを区別できます。 リポジトリー・イメージのタグを指定しないで Docker コマンドを実行すると、<code>latest</code> タグの付いたイメージがデフォルトで使用されます。</dd>
</dl>

Docker 固有の用語について詳しくは、[Docker 用語集 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/glossary/) を参照してください。

## 地域
{: #registry_regions}

{{site.data.keyword.registrylong_notm}} レジストリーは、複数の地域で使用できます。
{:shortdesc}

すべてのレジストリー成果物は、現在使用している特定の地域レジストリーが範囲になります。 例えば、名前空間、イメージ、トークン、割り当て量の設定、プランの設定はすべて、地域レジストリーごとに管理する必要があります。

### ローカル地域
{: #registry_regions_local}

ローカル地域とは、専用のエンドポイントからアクセスされる地理的な地域のことです。 地域の {{site.data.keyword.registrylong_notm}} ドメイン・ネームは変更されています。 新しいドメイン・ネームは、コンソールおよび CLI で使用可能です。 {:shortdesc}

ドメイン・ネームを以下の表に示します。

| ローカル・レジストリー地域 | 新しいドメイン・ネーム | 非推奨のドメイン・ネーム |
|-----|----|-----------|
| `ap-north` | `jp.icr.io` | 適用外 |
| `ap-south` | `au.icr.io` | `registry.au-syd.bluemix.net` |
| `eu-central` | `de.icr.io` | `registry.eu-de.bluemix.net` |
| `uk-south` | `uk.icr.io` | `registry.eu-gb.bluemix.net` |
| `us-south` | `us.icr.io` | `registry.ng.bluemix.net` |
{: caption="表 3. ローカル地域のドメイン・ネーム。" caption-side="top"}

既存の `bluemix.net` ドメイン・ネームは非推奨となっていますが、当面の間は使用を継続できます。サポートの終了日は後に公表されます。
{: deprecated}

#### 脆弱性アドバイザーのドメイン・ネーム
{: #registry_regions_local_va}

地域の脆弱性アドバイザーのドメイン・ネームは変更されています。 新しいドメイン・ネームは、コンソールおよび CLI で使用可能です。 {:shortdesc}

新しいドメイン・ネームを以下の表に示します。

| ローカルの脆弱性アドバイザー地域 | 新しいドメイン・ネーム | 非推奨のドメイン・ネーム |
|-----|----|-----------|
| `ap-north` | `jp.icr.io/va` | 適用外 |
| `ap-south` | `au.icr.io/va` | `va.au-syd.bluemix.net` |
| `eu-central` | `de.icr.io/va` | `va.eu-de.bluemix.net` |
| `uk-south` | `uk.icr.io/va` | `va.eu-gb.bluemix.net` |
| `us-south` | `us.icr.io/va` | `va.ng.bluemix.net` |
{: caption="表 4. ローカル地域のドメイン・ネーム。" caption-side="top"}

既存の `bluemix.net` ドメイン・ネームは非推奨となっていますが、当面の間は使用を継続できます。サポートの終了日は後に公表されます。
{: deprecated}

#### ローカル地域のターゲット設定
{: #registry_regions_local_target}

ローカル地域以外の地域を使用する場合は、[`ibmcloud cr region-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) コマンドを実行して、アクセスしたい地域をターゲットにします。 このコマンドをパラメーターなしで実行して使用可能な地域のリストを表示することも、パラメーターとして地域を指定することもできます。
{:shortdesc}

1. パラメーターを指定してコマンドを実行する場合は、`<region>` を[リージョン](#registry_regions_local)の名前に置き換えます。

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

   例えば、`eu-central` リージョンをターゲットにするには、以下のコマンドを実行します。

   ```
   ibmcloud cr region-set eu-central
   ```
   {: pre}

2. `ibmcloud cr login` コマンドを実行することにより、レジストリーにログインします。

### グローバル・レジストリー
{: #registry_regions_global}

グローバル・レジストリーを使用できます。このレジストリーの名前 (`icr.io`) には地域は含まれません。 このレジストリーでは、IBM が提供するパブリック・イメージのみがホストされます。 名前空間をセットアップする、イメージにタグを付けてレジストリーにプッシュする、などの自分のイメージの管理を行うには、[ローカルな地域のレジストリー](#registry_regions_local)を使用してください。
{:shortdesc}

グローバル・レジストリーのドメイン・ネームは変更されています。 新しいドメイン・ネームは、コンソールおよび CLI で使用可能です。

新しいドメイン・ネームを以下の表に示します。

| レジストリー | 新しいドメイン・ネーム | 非推奨のドメイン・ネーム |
|-----|----|-----------|
| グローバル | `icr.io` | `registry.bluemix.net` |
{: caption="表 5. グローバル・レジストリーのドメイン・ネーム。" caption-side="top"}

既存の `bluemix.net` ドメイン・ネームは非推奨となっていますが、当面の間は使用を継続できます。サポートの終了日は後に公表されます。
{: deprecated}

#### 脆弱性アドバイザーのドメイン・ネーム
{: #registry_regions_global_va}

グローバルの脆弱性アドバイザーのドメイン・ネームは変更されています。 新しいドメイン・ネームは、コンソールおよび CLI で使用可能です。{:shortdesc}

新しいドメイン・ネームを以下の表に示します。

| 脆弱性アドバイザー | 新しいドメイン・ネーム  | 非推奨のドメイン・ネーム |
|-----|----|-----------|
| グローバル | `icr.io/va` | `va.bluemix.net` |
{: caption="表 6. 脆弱性アドバイザーのグローバル・レジストリーのドメイン・ネーム。" caption-side="top"}

既存の `bluemix.net` ドメイン・ネームは非推奨となっていますが、当面の間は使用を継続できます。サポートの終了日は後に公表されます。
{: deprecated}

#### グローバル・レジストリーのターゲット設定
{: #registry_regions_global_target}

[`ibmcloud cr region-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set) コマンドを実行して、グローバル・レジストリーをターゲットにすることができます。
{:shortdesc}

1. グローバル・レジストリーをターゲットにするには、以下のコマンドを実行します。

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. ローカル Docker デーモンがグローバル・レジストリーにログインするようにし、{{site.data.keyword.IBM_notm}} 提供のパブリック・イメージをプルできるようにするには、`ibmcloud cr login` コマンドを実行します。

## Docker のサポート
{: #docker}

{{site.data.keyword.registrylong_notm}} は、Docker Engine V1.12.6 以降をサポートしています。

Docker が必要になるのは、イメージをプッシュまたはプルするとき、または `ibmcloud cr ppa-archive-load` コマンドを実行するときだけです。

Docker V2 Schema 2 イメージがサポートされています。 マニフェスト・リストもサポートされています。 詳細については、[Docker: Image Manifest Version 2,Schema 2 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/registry/spec/manifest-v2-2/)を参照してください。

Docker V1 イメージは非推奨です。
{: deprecated}
