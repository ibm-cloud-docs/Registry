---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker with LogDNA events, Activity Tracker events, events, track,

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

# Activity Tracker イベント
{: #at_events}

ユーザーとアプリケーションが、{{site.data.keyword.cloud}} の中の {{site.data.keyword.registrylong}} サービスとどうやり取りするかを追跡します。
{:shortdesc}

{{site.data.keyword.at_full_notm}} サービス、または (既存ユーザーの場合のみ) {{site.data.keyword.cloudaccesstrailfull_notm}} サービスは、{{site.data.keyword.cloud_notm}} の中のサービスの状態を変更するユーザー開始アクティビティーを記録します。
詳しくは、[{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started)、または (既存ユーザーの場合) [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)を参照してください。

次の表に、呼び出されるとイベントを生成する API メソッドをリストします。

<table>
  <caption>表 1. イベントを生成する操作</caption>
  <tr>
    <th>操作</th>
	  <th>説明</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>脆弱性アドバイザーの免除を作成する。</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>脆弱性アドバイザーの免除を削除する。</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>{{site.data.keyword.registrylong_notm}} 内で Docker イメージをビルドします。</td>
  </tr>
  <tr>
    <td>`container-registry.image.bulkdelete`</td>
	  <td>{{site.data.keyword.registrylong_notm}} から複数のイメージを削除します。</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>{{site.data.keyword.registrylong_notm}} からイメージを削除します。</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>イメージに関する詳細を表示します。</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>{{site.data.keyword.IBM_notm}} アカウント内のイメージをリストします。</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>{{site.data.keyword.registrylong_notm}} からイメージをプルします。</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>{{site.data.keyword.registrylong_notm}} にイメージをプッシュします。</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>指定した 1 つ以上のイメージを {{site.data.keyword.registrylong_notm}} から削除します。</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>以前に存在する {{site.data.keyword.registrylong_notm}} イメージを参照するタグを追加します。</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>{{site.data.keyword.registrylong_notm}} 内の指定された各イメージから 1 つまたは複数のタグを削除します。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>名前空間を {{site.data.keyword.registrylong_notm}} に追加します。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>{{site.data.keyword.registrylong_notm}} から名前空間を削除します。</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>{{site.data.keyword.IBM_notm}} アカウント内の名前空間をリストします。</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>トラフィックおよびストレージの現在の割り当て量と、それらの割り当て量に対する使用量の情報を表示します。</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>割り当て量を変更します。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>レジストリー・トークンを削除します。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>レジストリー・トークンに関する情報を取得します。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>{{site.data.keyword.IBM_notm}} アカウント内のレジストリー・トークンをリストします。</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>複数のレジストリー・トークンを削除します。</td>
  </tr><tr>
    <td>`container-registry.retentionanalysis`</td>
	  <td>指定する基準を満たすイメージだけを保持することにより、名前空間をクリーンアップします。指定する基準を適用することにより、{{site.data.keyword.registrylong_notm}} の中の名前空間内の各リポジトリーのイメージを保持します。その名前空間の中のその他のすべてのイメージは削除されます。</br>削除するイメージのリストを取得する要求は、`retentionanalysis` イベント・タイプに対する `post` アクションです。削除は、`images` イベント・タイプに対する単一の `bulkdelete` アクションであり、また個々の各イメージについての `delete` アクションでもあります。</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>現在の価格プランに関する情報を表示します。</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>標準プランにアップグレードします。</td>
  </tr>
 </table>

## イベントを探す場所
{: #ui}

### {{site.data.keyword.at_full_notm}} イベント
{: #ui_atlogdna}

{{site.data.keyword.at_full_notm}} イベントは、イベントが生成された {{site.data.keyword.cloud_notm}} リージョン (`ap-south` を除く) に存在する {{site.data.keyword.at_full_notm}} **アカウント・ドメイン**で確認できます。`ap-south` についてのイベントは、`東京 (jp-tok)` 内に表示されます。

{{site.data.keyword.registrylong_notm}} または脆弱性アドバイザー・イベントが利用可能な[リージョン](/docs/services/Registry?topic=registry-registry_overview#registry_regions)は、そのリソースが利用可能な {{site.data.keyword.registrylong_notm}} の地域に対応します。リソースの例としては、イメージや名前空間があります。

| アカウントのレジストリーのリージョン | レジストリーのドメイン・ネーム | {{site.data.keyword.at_full_notm}} イベントの場所 |
|:-----------------|:-----------------|:-----------------|
| `us-south` | `us.icr.io` | `ダラス (us-south)` |
| `eu-central` | `de.icr.io` | `フランクフルト (eu-de)` |
| `uk-south` | `uk.icr.io` | `ロンドン (eu-gb)` |
| `ap-south` | `au.icr.io` | `東京 (jp-tok)` |
| `ap-north` | `jp.icr.io` | `東京 (jp-tok)` |
{: caption="表 2. {{site.data.keyword.at_full_notm}} イベントの場所" caption-side="top"}

| レジストリー | グローバル・レジストリー | {{site.data.keyword.at_full_notm}} イベントの場所 |
|:-----------------|:-----------------|:-----------------|
| グローバル | `icr.io` | `ダラス (us-south)` |
{: caption="表 3. グローバル・レジストリー {{site.data.keyword.at_full_notm}} イベントの場所" caption-side="top"}

### {{site.data.keyword.cloudaccesstraillong_notm}} イベント
{: #ui_at}

{{site.data.keyword.cloudaccesstraillong_notm}} イベント (既存ユーザーのみ) は、イベントが生成された {{site.data.keyword.cloud_notm}} リージョンで利用可能な {{site.data.keyword.cloudaccesstraillong_notm}} **アカウント・ドメイン**で使用可能です (`ap-north` を除く)。`ap-north` でのイベントは `ap-south` 内に表示されます。

{{site.data.keyword.cloudaccesstrailfull_notm}} は非推奨になりました。2019 年 5 月 9 日以降、新しい {{site.data.keyword.cloudaccesstrailshort}} インスタンスをプロビジョンできません。既存のプレミアム・プランのインスタンスは、2019 年 9 月 30 日までサポートされます。{{site.data.keyword.cloud_notm}} アカウントのアクティビティーのモニタリングを続行するには、[{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) のインスタンスをプロビジョンします。
{: deprecated}

{{site.data.keyword.registrylong_notm}} または脆弱性アドバイザー・イベントが利用可能な[リージョン](/docs/services/Registry?topic=registry-registry_overview#registry_regions)は、そのリソースが利用可能な {{site.data.keyword.registrylong_notm}} の地域に対応します。リソースの例としては、イメージや名前空間があります。
