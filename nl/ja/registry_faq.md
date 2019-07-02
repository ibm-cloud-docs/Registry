---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, Vulnerability Advisor,

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
{:faq: data-hd-content-type='faq'}

# よくある質問 (FAQ)
{: #registry_faq}

{{site.data.keyword.registrylong}} に関するよくある質問。
{: shortdesc}

## パブリック・イメージの一覧を表示する方法を教えてください。
{: #faq_list_public_images}
{: faq}

パブリック・イメージの一覧を表示するには、次のように `ibmcloud` コマンドを実行してください。グローバル・レジストリーを対象にしてから、 IBM 提供のパブリック・イメージの一覧を表示します。

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Docker 以外のツールで、イメージを作成してレジストリーにプッシュすることはできますか?
{: #faq_tools}
{: faq}

はい。ただし、OCI のイメージ・フォーマットおよびプロトコルに対応したツールでなければなりません。

## IAM を使用してアクセス制御を行う方法を教えてください。
{: #faq_access_control}
{: faq}

{{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) ポリシーを作成して、{{site.data.keyword.registrylong_notm}} 内の名前空間へのアクセスを制御できます。 詳しくは、[チュートリアル: {{site.data.keyword.registrylong_notm}} リソースに対するアクセス権限の付与
](/docs/services/Registry?topic=registry-iam_access)と [Identity and Access Management を使用したユーザー・アクセス権限の管理](/docs/services/Registry?topic=registry-iam)を参照してください。

## {{site.data.keyword.registrylong_notm}} では、どの地域が選択可能ですか?
{: #faq_regions}
{: faq}

[ローカル領域](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local)でイメージをホストできます。 IBM でホストしているパブリック・イメージは[グローバル・レジストリー](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)から使用可能です。

## イメージを新規追加したら「スキャンが見つかりませんでした」というエラー・メッセージが表示されました。これはなぜですか?
{: #faq_va_new_scan_error}
{: faq}

イメージをレジストリーに追加した直後に脆弱性レポートを受信した場合、次のエラーになっている可能性があります。

```
BXNVA0009E:  <imagename> はスキャンされていません。 後で再試行してください。
この問題が続く場合は、サポートに連絡してヘルプを依頼してください。https://console.bluemix.net/docs/support/index.html#contacting-support を参照
```
{: screen}

このメッセージを受け取ったのは、イメージが結果の要求と同じタイミングでスキャンされず、スキャン・プロセスが完了するまでに時間がかかったためです。 イメージ・サイズとレジストリーが受信するトラフィックの量にもよりますが、通常の操作では、イメージを追加してから 2 分以内にスキャンが完了します。

このメッセージがビルド・パイプラインの一部として受信されており、このエラーが定期的に表示される場合は、短い休止を含む何らかの再試行ロジックを追加してみてください。

それでもパフォーマンスが改善されない場合は、サポートにお問い合わせください。[{{site.data.keyword.registrylong_notm}}のヘルプとサポートの入手](/docs/services/Registry?topic=registry-ts_index#gettinghelp)を参照してください。

## 脆弱性アドバイザーのスキャンはどのようにして起動しますか?
{: #faq_va_trigger_scan}
{: faq}

次のいずれかの場合に、イメージのスキャンが起動します。

- 新規イメージがレジストリーにプッシュされたとき。
- イメージがスキャンされずに 7 日間経過すると、イメージは再スキャンのキューに入ります。再スキャンが完了するまでには少し時間がかかる場合があります。
- イメージにインストールされたパッケージに関する新しいセキュリティー通知がリリースされると、そのイメージは再スキャンのキューに入ります。再スキャンが完了するまでには少し時間がかかる場合があります。 新規セキュリティー通知のリリースによる再スキャンの起動は、Ubuntu と Debian のイメージのみで可能です。

## セキュリティー通知はどれくらいの頻度で更新されますか?
{: #faq_va_update_security_notice}
{: faq}

脆弱性アドバイザーのセキュリティー通知は、約 12 時間ごとにベンダーのオペレーティング・システム・サイトからロードされます。
