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






# トークンを使用した、{{site.data.keyword.registrylong_notm}} 内の名前空間へのアクセスの自動化
{: #registry_tokens}

トークンを使用して、名前空間への Docker イメージのプッシュ、および名前空間からの Docker イメージのプルを自動化することができます。{:shortdesc}

始めに、[{{site.data.keyword.registrylong_notm}} および Docker CLI をインストールします](registry_setup_cli_namespace.html#registry_cli_install)。

セキュリティー・トークンは、トークンを所有するすべてのユーザーが、保護された情報にアクセスすることを許可します。トークンは、API キーと同じような方法で使用されます。{{site.data.keyword.Bluemix_notm}} アカウント用のトークンを作成して、領域にセットアップしたすべての名前空間へのアクセスを、{{site.data.keyword.Bluemix_notm}} アカウント外部のユーザーに付与することができます。このトークンを所有するすべてのユーザーまたはアプリは、container-registry プラグインをインストールせずに、名前空間にイメージをプッシュしたり名前空間からイメージをプルしたりすることができます。

{{site.data.keyword.Bluemix_notm}} アカウント用のトークンを作成する際に、そのトークンがレジストリーへの読み取り専用アクセス (プル) を許可するのか、それとも書き込みアクセス (プッシュおよびプル) を許可するのかを決定できます。
また、トークンを永続的にするか、または 24 時間後に期限切れするかについても指定できます。複数のトークンを作成および使用して、さまざまなタイプのアクセスを制御することができます。


## {{site.data.keyword.Bluemix_notm}} アカウント用のトークンの作成
{: #registry_tokens_create}

領域のすべての {{site.data.keyword.registrylong_notm}} 名前空間へのアクセスを付与するためのトークンを作成できます。{:shortdesc}

1.  トークンを作成します。以下の例は、領域内にセットアップされているすべての名前空間への読み取りおよび書き込みアクセスを持つ、有効期限がないトークンを作成します。


    ```
    bx cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png"/> このコマンドの構成要素について</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>オプションです。このオプションを使用して、後でより容易に識別できるようにトークンを記述します。</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>オプションです。このオプションを使用して、有効期限がないトークンを作成します。このオプションを指定しないと、トークンは 24 時間後に無効になります。<br> **ヒント:** 名前空間へのアクセスをブロックするための有効期限がないトークンが不要になったら、必ずそのトークンを削除してください。</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>オプションです。このオプションを使用して、ユーザーが名前空間にイメージをプッシュしたり名前空間からイメージをプルすることを可能にするトークンを作成します。このオプションを指定しないと、トークンは、イメージをプルするためにのみ使用できます。</td>
        </tr>
        </tbody>
        </table>

    CLI 出力は、以下のような出力になります。

    ```
    Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
    Token              <token_value>
    ```
    {: screen}

2.  トークンが作成されたことを確認します。

    ```
bx cr token-list```
    {: pre}


## トークンを使用した名前空間へのアクセスの自動化
{: #registry_tokens_use}

`docker login` コマンドでトークンを使用して、{{site.data.keyword.registrylong_notm}} の名前空間へのアクセスを自動化することができます。トークンに読み取り専用アクセスを設定するか、または読み取り/書き込みアクセスを設定するかに応じて、ユーザーは、名前空間にイメージをプッシュしたり、名前空間からイメージをプルしたりすることができます。{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
bx login```
    {: pre}

2.  {{site.data.keyword.Bluemix_notm}} アカウント内のすべてのトークンをリストし、使用するトークン ID をメモします。

    ```
bx cr token-list```
    {: pre}

3.  トークンのトークン値を取得します。&lt;token_id&gt; は、トークンの ID に置換してください。

    ```
    bx cr token-get <token_id>
    ```
    {: pre}

    CLI 出力の**「トークン」**に、トークン値が表示されます。

4.  トークンを `docker login` コマンドの一部として使用します。&lt;token_value&gt; を、前の手順で取得したトークン値に置換し、&lt;registry_url&gt; を、名前空間がセットアップされているレジストリーの URL に置換します。


    -   米国南部でセットアップされている名前空間の場合: registry.ng.bluemix.net
    -   英国南部でセットアップされている名前空間の場合: registry.eu-gb.bluemix.net
    -   EU 中央部でセットアップされている名前空間の場合: registry.eu-de.bluemix.net
    -   アジア太平洋南地域でセットアップされている名前空間の場合: registry.au-syd.bluemix.net

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}

    トークンを使用して Docker にログインすると、名前空間にイメージをプッシュしたり、名前空間からイメージをプルしたりすることができます。


## {{site.data.keyword.Bluemix_notm}} アカウントからのトークンの削除
{: #registry_tokens_remove}

{{site.data.keyword.registrylong_notm}} トークンが不要になったら、削除します。{:shortdesc}

**注:** 有効期限が切れた {{site.data.keyword.registrylong_notm}} トークンは {{site.data.keyword.Bluemix_notm}} アカウントから自動的に削除されるため、手動で削除する必要はありません。

1.  {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
bx login```
    {: pre}

2.  {{site.data.keyword.Bluemix_notm}} アカウント内のすべてのトークンをリストし、削除するトークン ID をメモします。

    ```
bx cr token-list```
    {: pre}

3.  トークンを削除します。

    ```
    bx cr token-rm <token_id>
    ```
    {: pre}


