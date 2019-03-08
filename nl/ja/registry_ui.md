---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, vulnerability of images, security of images, security issues

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

# イメージの脆弱性のモニタリング
{: #registry_ui}

{{site.data.keyword.Bluemix_notm}} コンソールを使用して、{{site.data.keyword.registrylong}} パブリック・リポジトリーと専用リポジトリーにあるイメージの潜在的な脆弱性とセキュリティーに関する情報を確認できます。
{:shortdesc}

**「セキュリティー状況 (Security Status)」** 列は、イメージに関する以下の情報を示します。

- `Secure` セキュリティー問題は見つかりませんでした。
- `Vulnerable` セキュリティーまたは構成の問題が見つかったので、イメージをデプロイする前に問題に対処する必要があります。
- `Incomplete` スキャンは完了していません。 スキャンがまだ実行中であるか、またはイメージのオペレーティング・システムに互換性がない可能性があります。 時間を置いてからスキャンを再試行してください。 それでもスキャンが完了しない場合には、イメージを再プッシュして新たにスキャンを開始してください。 スキャンが完了していないイメージは、デプロイメント用にブロック化されません。
- `Unsupported OS` イメージ内のオペレーティング・システムはサポートされていません。

グラフィカル・ユーザー・インターフェースを表示するには、以下の手順を使用します。

1. IBMid を使用して {{site.data.keyword.cloud_notm}} コンソール ([https://cloud.ibm.com/login ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login)) にログインします。
2. 複数の {{site.data.keyword.Bluemix_notm}} アカウントをお持ちの場合は、使用するアカウントと領域をアカウント・メニューから選択します。
3. **「カタログ」**をクリックします。
4. **「コンテナー」**カテゴリーを選択し、**「Container Registry」**タイルをクリックします。
5. 専用リポジトリー内のイメージ関連情報を表示するには、**「イメージ」**をクリックします。 専用リポジトリー内のイメージのリストと各イメージのセキュリティー状況が表示されます。
6. タグやイメージ・ダイジェストを含む、潜在的な脆弱性の詳細を表示するには、表の中のイメージに関する行をクリックします。 **「イメージの詳細」**タブが開きます。
7. タイプ別の問題について調べるには、**「タイプ別の問題」**タブをクリックします。
8. 関連付けられたコンテナーについて調べるには、**「関連付けられたコンテナー」**タブをクリックします。

セキュリティー・レポートの情報の意味について詳しくは、[脆弱性アドバイザーによるイメージのセキュリティーの管理](/docs/services/va?topic=va-va_index)を参照してください。
