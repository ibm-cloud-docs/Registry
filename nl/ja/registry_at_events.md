---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, Activity Tracker events, events

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

{{site.data.keyword.cloudaccesstrailfull}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.Bluemix}} の {{site.data.keyword.registrylong}} サービスとどのような対話を実行したのかを追跡できます。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} サービスは、{{site.data.keyword.Bluemix_notm}} のサービスの状態を変更するアクティビティーをユーザーが開始すると、そのアクティビティーを記録します。
詳細については、[{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla)を参照してください。

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
 </table>

## イベントを探す場所
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} イベントは、イベントが生成された {{site.data.keyword.Bluemix_notm}} 領域に存在する {{site.data.keyword.cloudaccesstrailshort}} **アカウント・ドメイン** で確認できます。

脆弱性アドバイザーのイベントを確認できる[領域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)は、リソース (イメージや名前空間など) が存在する {{site.data.keyword.registrylong_notm}} の領域に対応します。
