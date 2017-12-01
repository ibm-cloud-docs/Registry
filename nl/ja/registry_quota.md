---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# ストレージおよびプル・トラフィックの割り当て量制限の管理
{: #registry_quota}

カスタム割り当て量制限を設定および管理することにより、{{site.data.keyword.Bluemix}} アカウントで使用できるストレージとプル・トラフィックの量を制限することができます。{:shortdesc}


## イメージの保管およびプルのための割り当て量制限の設定
{: #registry_quota_set}

独自の割り当て量制限を設定することにより、ストレージおよびプライベート・イメージへのプル・トラフィックの量を制限することができます。{:shortdesc}

始めに、自分が、割り当て量を設定しようとしている [{{site.data.keyword.Bluemix_notm}} アカウントの所有者または請求管理者](../../iam/users_roles.html#userroles)であることを確認してください。

{{site.data.keyword.registryshort_notm}} 標準プランにアップグレードすると、無制限の量のストレージおよびプライベート・イメージへのプル・トラフィックを使用できる利点があります。
望ましい支払いレベルを超えないようするために、ストレージおよびプル・トラフィックの量に個別の割り当て量を設定することができます。割り当て量制限は、{{site.data.keyword.registrylong_notm}} 内にセットアップされているすべての名前空間に適用されます。無料サービス・プランを使用している場合は、無料のストレージおよびプル・トラフィック量以内にカスタム割り当て量を設定することもできます。

割り当て量を設定するには、以下のようにします。

1.  {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
bx login```
    {: pre}

2.  ストレージおよびプル・トラフィックの現在の割り当て量制限を検討します。

    ```
bx cr quota```
    {: pre}

    出力は、以下のようになります。


    ```
Getting quotas and usage for the current month, for account '<account_owner> Account'...
QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB   

    OK```
    {: screen}

3.  ストレージおよびプル・トラフィックの割り当て量制限を変更します。プル・トラフィックの使用量を変更するには、**traffic** オプションを指定し、_&lt;traffic_quota&gt;_ を、プル・トラフィック割り当て量に設定する値 (M バイト単位) に置換します。アカウント内のストレージの量を変更する場合は、**storage** オプションを指定し、_&lt;storage_quota&gt;_ を、設定する値 (M バイト単位) に置換します。



    **注:** 無料プランを使用している場合は、無料層を超える量に割り当て量を設定することはできません。無料層では、ストレージは 512 MB、トラフィックは 5120 MB まで許可されます。

    ```
    bx cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    ストレージの割り当て量制限を 600 M バイトに設定し、プル・トラフィックを 7000 M バイトに設定する例は、以下のようになります。



    ```
bx cr quota-set --storage 600 --traffic 7000```
    {: pre}


## イメージを保管およびプルするための割り当て量制限と使用量の検討
{: #registry_quota_get}

アカウントの割り当て量制限を検討し、現在のストレージおよびプル・トラフィックの使用量を確認することができます。{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
bx login```
    {: pre}

2.  ストレージおよびプル・トラフィックの現在の割り当て量制限を検討します。

    ```
bx cr quota```
    {: pre}

    出力は、以下のようになります。


    ```
Getting quotas and usage for the current month, for account '<account_owner> Account'...
QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB   

    OK```
    {: screen}


## 指定された割り当て量制限内に収めるための、使用済みストレージの解放およびサービス・プランまたは割り当て量制限の変更
{: #registry_quota_freeup}

{{site.data.keyword.Bluemix_notm}} アカウントに設定されている割り当て量制限を超えた場合は、ストレージを解放し、サービス・プランまたは割り当て量制限を変更して、名前空間へのイメージのプッシュ、および名前空間からのイメージのプルを継続することができます。{:shortdesc}

{{site.data.keyword.Bluemix_notm}} アカウント内のイメージ・ストレージを解放するには、以下のようにします。

1.  {{site.data.keyword.Bluemix_notm}} アカウントのすべての名前空間内のすべてのイメージをリストします。

    ```
bx cr images```
    {: pre}

2.  名前空間からイメージを削除します。_&lt;image_name&gt;_ を、削除するイメージの名前に置換します。


    ```
    bx cr image-rm <image_name>
    ```
    {: pre}

    **注:** イメージのサイズに応じて、イメージが削除されてストレージが使用可能になるまでにしばらく時間がかかる場合があります。

3.  ストレージ割り当て量の使用量を検討します。

    ```
bx cr quota```
    {: pre}

4. **注:** 請求対象期間にプル・トラフィックの使用量を削減することはできません。

    名前空間からのイメージのプルを継続するには、以下のいずれかのオプションを選択します。

    -   次の請求処理サイクルが開始されるまで待つ。
    -   無料プランを使用している場合は、[標準サービス・プランにアップグレードする](registry_overview.html#registry_plan_upgrade)。
    -   既に標準プランを使用している場合は、[プル・トラフィックの新しい割り当て量制限を設定する](#registry_quota_set)。
