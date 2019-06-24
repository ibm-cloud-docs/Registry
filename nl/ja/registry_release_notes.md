---

copyright:
  years: 2019
lastupdated: "2019-05-17"

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

このリリース・ノートをお読みになり、{{site.data.keyword.registrylong}} と脆弱性アドバイザーの最新の変更点をご確認ください。 変更点は日付別に分類されています。
{:shortdesc}

## 2019 年 5 月 13 日
{: #13may2019}

- **Container Scanner のサポート終了**

  Container Scanner が非推奨になり、使用できなくなりました。

  詳しくは、[Container Scanner のインストール (非推奨)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner) を参照してください。

## 2019 年 4 月 2 日
{: #2apr2019}

- **Container Image Security Enforcement の一般出荷版**

  Container Image Security Enforcement を使用すると、{{site.data.keyword.containerlong_notm}} のクラスターにコンテナー・イメージをデプロイする前に、コンテナー・イメージを検査できます。 イメージのデプロイ元を制御し、脆弱性アドバイザーのポリシーを適用して、[コンテント・トラスト](/docs/services/Registry?topic=registry-registry_trustedcontent)をイメージに適切に適用することができます。

  詳しくは、[コンテナー・イメージ・セキュリティーの適用](/docs/services/Registry?topic=registry-security_enforce#security_enforce)を参照してください。

## 2019 年 3 月 14 日
{: #14mar2019}

- **{{site.data.keyword.registrylong_notm}} に関して {{site.data.keyword.cloudaccesstrailfull_notm}} を使用可能**

  {{site.data.keyword.cloudaccesstraillong_notm}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud}} の {{site.data.keyword.registrylong_notm}} サービスと行った対話を追跡できます。

  詳しくは、[Activity Tracker イベント](/docs/services/Registry?topic=registry-at_events#at_events)を参照してください。

## 2019 年 2 月 25 日
{: #25feb2019}

- **新しい DNS 名**

  {{site.data.keyword.registrylong_notm}} で新しいドメイン・ネームが導入されました。 新しいドメイン・ネームは、コンソールおよび CLI で使用可能です。 新しい `icr.io` というドメイン・ネームを利用できるようになりました。 既存の `registry.bluemix.net` ドメイン・ネームは非推奨となっていますが、当面の間は使用を継続できます。サポートの終了日は後に公表されます。 詳しくは、[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)および[新しい IBM Cloud Container Registry ドメイン・ネームの導入![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names)を参照してください。

  コンテント・トラストを使用している場合、署名はドメイン・ネームを含むすべてのイメージ名に適用されるため、新しい署名を追加し、新しいドメイン・ネームでコンテント・トラストを使用できるようにする必要があります。 イメージの署名について詳しくは、[信頼できるコンテンツのイメージへの署名](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)を参照してください。

- **{{site.data.keyword.containerlong_notm}} クラスター用の IAM API キーのプル・シークレット**

  `icr.io` ドメイン用の新しいクラスター・イメージのプル・シークレットは IAM API キーを使用して許可されるので、{{site.data.keyword.registrylong_notm}} リソースに対するアクセスの制御を強化する場合、IAM ポリシーを追加できます。 例えば、クラスターのプル・シークレットの API キー・ポリシーを変更して、イメージが特定のレジストリー地域または名前空間からのみプルされるようにできます。
  
  詳しくは、[{{site.data.keyword.registrylong_notm}} からのイメージのプルをクラスターに許可する方法](/docs/containers?topic=containers-images#cluster_registry_auth)を参照してください。

- **ap-north の新しい地域**

  `ap-north` で新しい地域を利用できるようになりました。 新しい地域はドメイン・ネーム `jp.icr.io` で使用できます。
  
  詳しくは、[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)を参照してください。

## 2019 年 2 月 21 日
{: #21feb2019}

- **名前空間へのアクセスの自動化**

  トークンを使用して、名前空間への Docker イメージのプッシュ、および名前空間からの Docker イメージのプルを自動化することは、非推奨となりました。 API キーを使用して、{{site.data.keyword.registrylong_notm}} 名前空間へのアクセスを自動化し、イメージのプッシュとプルを可能にすることが必要です。

  詳しくは、[API キーを使用した名前空間へのアクセスの自動化](/docs/services/Registry?topic=registry-registry_access#registry_api_key)を参照してください。

## 2019 年 1 月 8 日
{: #8jan2019}

- **脆弱性アドバイザー API バージョン 2 のサポート終了**

  脆弱性アドバイザーの API バージョン 2 が非推奨になり、使用できなくなりました。 API バージョン 3 を使用してください。詳細については、[{{site.data.keyword.registrylong_notm}} API の脆弱性アドバイザー![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/apidocs/container-registry/va)を参照してください。

  詳細については、[脆弱性アドバイザー v2 API は非推奨 ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://www.ibm.com/blogs/bluemix/2018/12/vulnerability-advisor-v2-api-deprecation/) を参照してください。

## 2018 年 10 月 4 日
{: #4oct2018}

- **ユーザー・アクセスの管理**

  {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) を使用して、{{site.data.keyword.registrylong_notm}} に対するご使用のアカウント内のユーザーによるアクセスを制御できます。 {{site.data.keyword.registrylong_notm}} 内のご使用のアカウントを対象に IAM ポリシーを有効にする際には、アカウント内の {{site.data.keyword.registrylong_notm}} サービスにアクセスするすべてのユーザーに、IAM ユーザー役割が定義されたアクセス・ポリシーを割り当てる必要があります。 そのポリシーによって、サービスのコンテキスト内でユーザーが持つ役割や、ユーザーが実行できるアクションが決まります。

  詳しくは、[{{site.data.keyword.iamshort}} を使用したユーザー・アクセスの管理](/docs/services/Registry?topic=registry-iam#iam)、[ユーザー・アクセスの役割ポリシーの定義](/docs/services/Registry?topic=registry-user#user)、および[チュートリアル: IBM Cloud Container Registry リソースに対するアクセス権を付与する](/docs/services/Registry?topic=registry-iam_access#iam_access)を参照してください。

## 2018 年 8 月 7 日
{: #7aug2018}

- **脆弱性アドバイザーで適用除外ポリシーを使用可能**

  {{site.data.keyword.cloud_notm}} 組織のセキュリティーを管理する場合は、ポリシー設定を使用して、問題を適用除外するかどうかを決定できます。 Container Image Security Enforcement を使用して、ポリシーによって適用除外される問題と判断された後はセキュリティー問題が含まれないイメージからのみデプロイメントを許可するという選択もできます。

  詳しくは、[組織の適用除外ポリシーの設定](/docs/services/Registry?topic=va-va_index#va_managing_policy)を参照してください。

## 2018 年 7 月 25 日
{: #25jul2018}

- **脆弱性アドバイザーで {{site.data.keyword.cloudaccesstrailfull_notm}} を使用可能**

  {{site.data.keyword.cloudaccesstrailfull_notm}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud}} の {{site.data.keyword.registrylong_notm}} サービスと行った対話を追跡できます。

  詳しくは、[Activity Tracker イベント](/docs/services/Registry?topic=registry-at_events#at_events)を参照してください。
  
## 2018 年 7 月 12 日
{: #12jul2018}

- **脆弱性アドバイザー API バージョン 3**

  API バージョン 3 では、適用除外をリストするのに使用する API エンドポイントの動作が変更されました。 現在使用している API がバージョン 2 の動作に依存していないことを確認する必要があります。

  詳細については、[{{site.data.keyword.registrylong_notm}} の脆弱性アドバイザー ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/apidocs/container-registry/va) を参照してください。

## 2018 年 5 月 31 日
{: #31may2018}

- **パスポート・アドバンテージ・イメージでの Helm の使用**

  [IBM お客様向けパスポート・アドバンテージ・オンライン ![外部リンクのアイコン](../icons/launch-glyph.svg "外部リンクのアイコン")](https://www.ibm.com/software/passportadvantage/pao_customer.html) からダウンロードした、Helm で使用できるようにパッケージ化された {{site.data.keyword.IBM_notm}} ソフトウェアを、{{site.data.keyword.registrylong_notm}} 名前空間にインポートします。

  詳細については、[`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load) を参照してください。

## 2018 年 3 月 21 日
{: #21mar2018}

- **Container Scanner**

  Container Scanner を使用すると、脆弱性アドバイザーはコンテナーの基本イメージに存在しないコンテナーの実行中に見つかった問題を報告できます。

  詳しくは、[Container Scanner のインストール](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)を参照してください。

## 2018 年 3 月 16 日
{: #16mar2018}

- **Container Image Security Enforcement ベータ版**

  Container Image Security Enforcement ベータ版を使用すると、{{site.data.keyword.containerlong_notm}} のクラスターにコンテナー・イメージをデプロイする前に、コンテナー・イメージを検査できます。 イメージのデプロイ元を制御し、脆弱性アドバイザーのポリシーを適用して、[コンテント・トラスト](/docs/services/Registry?topic=registry-registry_trustedcontent)をイメージに適切に適用することができます。

  詳しくは、[コンテナー・イメージ・セキュリティーの適用](/docs/services/Registry?topic=registry-security_enforce#security_enforce)を参照してください。

## 2018 年 2 月 20 日
{: #20feb2018}

- **信頼できるコンテンツ**

  {{site.data.keyword.registrylong_notm}} は、信頼できるコンテンツのテクノロジーを備えているので、レジストリー名前空間内のイメージに署名してイメージの完全性を保証できます。 署名付きのイメージをプル/プッシュすることで、イメージをプッシュしたのが継続的統合 (CI) ツールなどの正当なパーティーであることを検証できます。

  詳しくは、[信頼できるコンテンツのイメージへの署名](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)を参照してください。

## 2017 年 11 月 6 日
{: #6nov2017}

- **グローバル・レジストリー**

  グローバル・レジストリーを使用できます。このレジストリーの名前 (`icr.io`) には地域は含まれません。 このレジストリーでは、IBM が提供するパブリック・イメージのみがホストされます。

  詳細については、[グローバル・レジストリー](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)を参照してください。

## 2017 年 9 月 29 日
{: #29sep2017}

- **Docker イメージのビルド**

  `ibmcloud cr build` コマンドを使用してコンテナーのビルドを実行できるようになりました。 {{site.data.keyword.cloud_notm}} で Docker イメージを直接ビルドするか、ローカル・コンピューターで独自の Docker イメージを作成してから {{site.data.keyword.registrylong_notm}} の名前空間にアップロード (プッシュ) することができます。

  詳細については、[名前空間で使用する Docker イメージのビルド](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating)および [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) を参照してください。

## 2017 年 8 月 24 日
{: #24aug2017}

- **グラフィカル・ユーザー・インターフェースのリリース**

  {{site.data.keyword.registrylong_notm}} グラフィカル・ユーザー・インターフェースがカタログで使用できるようになりました。[コンテナー・レジストリー ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](https://cloud.ibm.com/kubernetes/catalog/registry) を参照してください。

## 2017 年 6 月 27 日
{: #27jun2017}

- **{{site.data.keyword.registrylong_notm}} の一般出荷版**

  {{site.data.keyword.registrylong_notm}} が {{site.data.keyword.cloud_notm}} 内のサービスとして一般出荷可能になりました。 {{site.data.keyword.registrylong_notm}} は {{site.data.keyword.containerlong_notm}} をサポートします。

  {{site.data.keyword.containerlong_notm}} の詳細については、[入門チュートリアル](/docs/containers?topic=containers-getting-started)を参照してください。
