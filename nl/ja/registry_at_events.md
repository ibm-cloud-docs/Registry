---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker events, Activity Tracker events, events, track,

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

# {{site.data.keyword.cloudaccesstrailshort}} イベント
{: #at_events}

{{site.data.keyword.cloudaccesstrailfull}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud}} の {{site.data.keyword.registrylong}} サービスと行った対話を追跡できます。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} サービスは、{{site.data.keyword.cloud_notm}} のサービスの状態を変更するアクティビティーをユーザーが開始すると、そのアクティビティーを記録します。
詳細については、[{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)を参照してください。

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
	  <td>既存の {{site.data.keyword.registrylong_notm}} イメージを参照する新規タグを追加します。</td>
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

{{site.data.keyword.cloudaccesstrailshort}} イベントは、イベントが生成される {{site.data.keyword.cloud_notm}} 地域 (`ap-north` 以外) で利用できる {{site.data.keyword.cloudaccesstrailshort}} **アカウント・ドメイン**で使用できます。 `ap-north` でのイベントは `ap-south` 内に表示されます。

{{site.data.keyword.registrylong_notm}} または脆弱性アドバイザーのイベントを確認できる[地域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)は、リソース (イメージや名前空間など) が存在する {{site.data.keyword.registrylong_notm}} の地域に対応します。
