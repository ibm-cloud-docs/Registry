---

copyright:
  years: 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# リリース・ノート
{: #registry_release_notes}

{{site.data.keyword.registrylong}} と脆弱性アドバイザーの最新の変更点をご確認ください。変更点は日付別に分類されています。
{:shortdesc}

## 2019 年 8 月 1 日
{: #01aug2019}

<dl>
  <dt>`ibmcloud cr retention-run` コマンドが使用可能</dt>
  <dd>`ibmcloud cr retention-run` コマンドは、指定された基準を適用することによって、{{site.data.keyword.registrylong_notm}} の中の名前空間内の各リポジトリーのイメージを保持することにより、名前空間をクリーンアップします。その名前空間の中のその他のすべてのイメージは削除されます。
  
  詳しくは、[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) と、[イメージの保持](/docs/services/Registry?topic=registry-registry_retention)を参照してください。</dd>
</dl>

## 2019 年 7 月 25 日
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.registrylong_notm}} について {{site.data.keyword.at_full_notm}} が使用可能</dt>
  <dd>{{site.data.keyword.at_full_notm}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud}} の {{site.data.keyword.registrylong_notm}} サービスと行った対話を追跡できます。

  詳しくは、[Activity Tracker イベント](/docs/services/Registry?topic=registry-at_events#at_events)を参照してください。</dd>
</dl>

## 2019 年 7 月 1 日
{: #1jul2019}

<dl>
  <dt>`ibmcloud cr token-add` コマンドは使用できなくなります</dt>
  <dd>`ibmcloud cr token-add` コマンドは廃止されます。 今後はレジストリー・トークンを CLI でも API でも追加できません。</dd>
</dl>

## 2019 年 6 月 27 日
{: #27jun2019}

<dl>
  <dt>Container Scanner は使用できなくなります</dt>
  <dd>Container Scanner は廃止されます。{{site.data.keyword.registrylong_notm}} にプッシュされるイメージは、引き続き脆弱性アドバイザーによりスキャンされます。</dd>
</dl>

## 2019 年 6 月 13 日
{: #13jun2019}

<dl>
  <dt>イメージからタグを削除する</dt>
  <dd>{{site.data.keyword.registrylong_notm}} 内の指定された各イメージから 1 つまたは複数のタグを削除します。

  イメージから指定されたタグを削除し、基になるイメージとその他のタグはそのまま残しておく場合は、[`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag)コマンドを使用します。 基になるイメージとそのすべてのタグを削除する場合は、代わりに [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) コマンドを使用します。

  詳しくは、[プライベート {{site.data.keyword.cloud_notm}} リポジトリーのイメージからのタグの削除](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag)を参照してください。</dd>
</dl>

## 2019 年 5 月 13 日
{: #13may2019}

<dl>
  <dt>Container Scanner のサポート終了</dt>
  <dd>Container Scanner が非推奨になり、使用できなくなりました。

  詳しくは、[Container Scanner のインストール (非推奨)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner) を参照してください。</dd>
</dl>

## 2019 年 4 月 2 日
{: #2apr2019}

<dl>
  <dt>Container Image Security Enforcement の一般出荷版</dt>
  <dd>Container Image Security Enforcement を使用すると、{{site.data.keyword.containerlong_notm}} のクラスターにコンテナー・イメージをデプロイする前に、コンテナー・イメージを検査できます。 イメージのデプロイ元を制御し、脆弱性アドバイザーのポリシーを適用して、[コンテント・トラスト](/docs/services/Registry?topic=registry-registry_trustedcontent)をイメージに適切に適用することができます。

  詳しくは、[コンテナー・イメージ・セキュリティーの適用](/docs/services/Registry?topic=registry-security_enforce#security_enforce)を参照してください。</dd>
</dl>

## 2019 年 3 月 14 日
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.registrylong_notm}} について {{site.data.keyword.cloudaccesstrailfull_notm}} が使用可能</dt>
  <dd>{{site.data.keyword.cloudaccesstraillong_notm}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud}} の {{site.data.keyword.registrylong_notm}} サービスと行った対話を追跡できます。

  詳しくは、[Activity Tracker イベント](/docs/services/Registry?topic=registry-at_events#at_events)を参照してください。
</dd>
</dl>

## 2019 年 2 月 25 日
{: #25feb2019}

<dl>
  <dt>新しいドメイン・ネーム</dt>
  <dd>{{site.data.keyword.registrylong_notm}} で新しいドメイン・ネームが導入されました。 新しいドメイン・ネームは、コンソールおよび CLI で使用可能です。 新しい `icr.io` というドメイン・ネームを利用できるようになりました。 既存の `registry.bluemix.net` ドメイン・ネームは非推奨となっていますが、サポート終了日までは使用を継続できます。サポート終了日はまだ発表されていません。詳しくは、[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)および[新しい IBM Cloud Container Registry ドメイン・ネームの導入![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names)を参照してください。

  署名は、ドメイン・ネームを含むイメージ名全体に適用されます。コンテント・トラストを使用している場合、新しい署名を追加することにより、新しいドメイン・ネームでコンテント・トラストを使用できるようにする必要があります。イメージの署名について詳しくは、[信頼できるコンテンツのイメージへの署名](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)を参照してください。</dd>
</dl>

<dl>
  <dt>{{site.data.keyword.containerlong_notm}} クラスターの IAM API キー・プル・シークレット</dt>
  <dd>`icr.io` ドメイン用の新しいクラスター・イメージのプル・シークレットは、{{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) API キーを使用することによって許可されます。したがって、{{site.data.keyword.registrylong_notm}} リソースに対するアクセスの制御を強化するには、IAM ポリシーを追加することができます。例えば、クラスターのプル・シークレットの API キー・ポリシーを変更して、イメージが特定のレジストリー地域または名前空間からのみプルされるようにできます。
  
  詳しくは、[{{site.data.keyword.registrylong_notm}} からのイメージのプルをクラスターに許可する方法](/docs/containers?topic=containers-images#cluster_registry_auth)を参照してください。</dd>
</dl>

<dl>
  <dt>ap-north の新しい地域</dt>
  <dd>`ap-north` で新しい地域を利用できるようになりました。 新しい地域はドメイン・ネーム `jp.icr.io` で使用できます。
  
  詳しくは、[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)を参照してください。</dd>
</dl>

## 2019 年 2 月 21 日
{: #21feb2019}

<dl>
  <dt>名前空間へのアクセスの自動化</dt>
  <dd>トークンを使用して、名前空間への Docker イメージのプッシュ、および名前空間からの Docker イメージのプルを自動化することは、非推奨となりました。 API キーを使用して、{{site.data.keyword.registrylong_notm}} 名前空間へのアクセスを自動化し、イメージのプッシュとプルを可能にすることが必要です。

  詳しくは、[API キーを使用した名前空間へのアクセスの自動化](/docs/services/Registry?topic=registry-registry_access#registry_api_key)を参照してください。</dd>
</dl>

## 2019 年 1 月 8 日
{: #8jan2019}

 <dl>
  <dt>脆弱性アドバイザー API バージョン 2 のサポート終了</dt>
  <dd>脆弱性アドバイザーの API バージョン 2 が非推奨になり、使用できなくなりました。 API バージョン 3 を使用してください。詳細については、[{{site.data.keyword.registrylong_notm}} API の脆弱性アドバイザー![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/apidocs/container-registry/va)を参照してください。

  詳細については、[脆弱性アドバイザー v2 API は非推奨 ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/) を参照してください。</dd>
</dl>

## 2018 年 10 月 4 日
{: #4oct2018}

<dl>
  <dt>ユーザー・アクセス権限の管理</dt>
  <dd>{{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) を使用して、{{site.data.keyword.registrylong_notm}} に対するご使用のアカウント内のユーザーによるアクセスを制御できます。 {{site.data.keyword.registrylong_notm}} 内のご使用のアカウントを対象に IAM ポリシーを有効にする際には、アカウント内のサービスにアクセスするすべてのユーザーに、IAM ユーザー役割が定義されたアクセス・ポリシーを割り当てる必要があります。そのポリシーによって、サービスのコンテキスト内でユーザーが持つ役割や、ユーザーが実行できるアクションが決まります。

  詳しくは、[{{site.data.keyword.iamshort}} を使用したユーザー・アクセスの管理](/docs/services/Registry?topic=registry-iam#iam)、[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry?topic=registry-user#user)、および[チュートリアル: IBM Cloud Container Registry リソースに対するアクセス権を付与する](/docs/services/Registry?topic=registry-iam_access#iam_access)を参照してください。</dd>
</dl>

## 2018 年 8 月 7 日
{: #7aug2018}

<dl>
  <dt>脆弱性アドバイザーで適用除外ポリシーを使用可能</dt>
  <dd>{{site.data.keyword.cloud_notm}} 組織のセキュリティーを管理する場合は、ポリシー設定を使用して、問題を適用除外するかどうかを決定できます。 Container Image Security Enforcement を使用して、ポリシーによって適用除外されたすべての問題を考慮した後、セキュリティー問題が含まれないイメージからのみデプロイメントを許可するようにすることができます。

  詳しくは、[組織の適用除外ポリシーの設定](/docs/services/Registry?topic=va-va_index#va_managing_policy)を参照してください。</dd>
</dl>

## 2018 年 7 月 25 日
{: #25jul2018}

<dl>
  <dt>脆弱性アドバイザーで {{site.data.keyword.cloudaccesstrailfull_notm}} を使用可能</dt>
  <dd>{{site.data.keyword.cloudaccesstrailfull_notm}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud}} の {{site.data.keyword.registrylong_notm}} サービスと行った対話を追跡できます。

  詳しくは、[Activity Tracker イベント](/docs/services/Registry?topic=registry-at_events#at_events)を参照してください。</dd>
</dl>
  
## 2018 年 7 月 12 日
{: #12jul2018}

<dl>
  <dt>脆弱性アドバイザー API バージョン 3</dt>
  <dd>API バージョン 3 では、適用除外をリストするのに使用する API エンドポイントの動作が変更されました。 現在使用している API がバージョン 2 の動作に依存していないことを確認する必要があります。

  詳細については、[{{site.data.keyword.registrylong_notm}} の脆弱性アドバイザー ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/apidocs/container-registry/va) を参照してください。</dd>
</dl>

## 2018 年 5 月 31 日
{: #31may2018}

<dl>
  <dt>パスポート・アドバンテージ・イメージで Helm を使用する</dt>
  <dd>[IBM お客様向けパスポート・アドバンテージ・オンライン ![外部リンクのアイコン](../icons/launch-glyph.svg "外部リンクのアイコン")](https://www.ibm.com/software/passportadvantage/pao_customer.html) からダウンロードした、Helm で使用できるようにパッケージ化された {{site.data.keyword.IBM_notm}} ソフトウェアを、{{site.data.keyword.registrylong_notm}} 名前空間にインポートします。

  詳細については、[`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load) を参照してください。</dd>
</dl>

## 2018 年 3 月 21 日
{: #21mar2018}

<dl>
  <dt>Container Scanner</dt>
  <dd>Container Scanner を使用すると、脆弱性アドバイザーはコンテナーの基本イメージに存在しないコンテナーの実行中に検出された問題を報告できます。

  詳しくは、[Container Scanner のインストール](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)を参照してください。</dd>
</dl>

## 2018 年 3 月 16 日
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement ベータ版</dt>
  <dd>Container Image Security Enforcement ベータ版を使用すると、{{site.data.keyword.containerlong_notm}} のクラスターにコンテナー・イメージをデプロイする前に、コンテナー・イメージを検査できます。 イメージのデプロイ元を制御し、脆弱性アドバイザーのポリシーを適用して、[コンテント・トラスト](/docs/services/Registry?topic=registry-registry_trustedcontent)をイメージに適切に適用することができます。

  詳しくは、[コンテナー・イメージ・セキュリティーの適用](/docs/services/Registry?topic=registry-security_enforce#security_enforce)を参照してください。</dd>
</dl>

## 2018 年 2 月 20 日
{: #20feb2018}

<dl>
  <dt>信頼できるコンテンツ</dt>
  <dd>{{site.data.keyword.registrylong_notm}} は、信頼できるコンテンツのテクノロジーを備えているので、レジストリー名前空間内のイメージに署名してイメージの完全性を保証できます。 署名付きのイメージをプル/プッシュすることで、イメージをプッシュしたのが継続的統合 (CI) ツールなどの正当なパーティーであることを検証できます。

  詳しくは、[信頼できるコンテンツのイメージへの署名](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)を参照してください。</dd>
</dl>

## 2017 年 11 月 6 日
{: #6nov2017}

<dl>
  <dt>グローバル・レジストリー</dt>
  <dd>グローバル・レジストリーが使用可能です。そのドメイン・ネーム (`icr.io`) にはリージョンが含まれていません。このレジストリーでは、IBM が提供するパブリック・イメージのみがホストされます。

  詳細については、[グローバル・レジストリー](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)を参照してください。</dd>
</dl>

## 2017 年 9 月 29 日
{: #29sep2017}

<dl>
  <dt>Docker イメージをビルドする</dt>
  <dd>`ibmcloud cr build` コマンドを使用してコンテナーのビルドを実行できるようになりました。 {{site.data.keyword.cloud_notm}} で Docker イメージを直接ビルドするか、ローカル・コンピューターで独自の Docker イメージを作成してから {{site.data.keyword.registrylong_notm}} の名前空間にアップロード (プッシュ) することができます。

  詳細については、[名前空間で使用する Docker イメージのビルド](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating)および [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) を参照してください。</dd>
</dl>

## 2017 年 8 月 24 日
{: #24aug2017}

<dl>
  <dt>グラフィカル・ユーザー・インターフェースのリリース</dt>
  <dd>{{site.data.keyword.registrylong_notm}} グラフィカル・ユーザー・インターフェースがカタログで使用できるようになりました。[コンテナー・レジストリー ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/kubernetes/catalog/registry) を参照してください。</dd>
</dl>

## 2017 年 6 月 27 日
{: #27jun2017}

<dl>
  <dt>{{site.data.keyword.registrylong_notm}} の一般出荷版</dt>
  <dd>{{site.data.keyword.registrylong_notm}} が {{site.data.keyword.cloud_notm}} 内のサービスとして一般出荷可能になりました。 {{site.data.keyword.registrylong_notm}} は {{site.data.keyword.containerlong_notm}} をサポートします。

  {{site.data.keyword.containerlong_notm}} の詳細については、[入門チュートリアル](/docs/containers?topic=containers-getting-started)を参照してください。</dd>
</dl>
