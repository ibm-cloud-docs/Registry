---

copyright:
  years: 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# {{site.data.keyword.registrylong_notm}} CLI およびレジストリー名前空間のセットアップ
{: #registry_setup_cli_namespace}

{{site.data.keyword.registrylong}} に Docker イメージを保管する前に、{{site.data.keyword.Bluemix_notm}} CLI と {{site.data.keyword.registrylong_notm}} プラグインをインストールしてから、レジストリー名前空間をセットアップして、{{site.data.keyword.registrylong_notm}} 内に独自のイメージ・リポジトリーを作成する必要があります。{:shortdesc}


## {{site.data.keyword.registrylong_notm}} CLI (`bx cr`) プラグインのインストール
{: #registry_cli_install}

コマンド・ラインを使用して {{site.data.keyword.Bluemix_notm}} 専用レジストリーの名前空間および Docker イメージを管理するには、{{site.data.keyword.registrylong_notm}} CLI をインストールします。{:shortdesc}

1.  [container-registry プラグインをインストールします。
](index.html#registry_cli_install)
2.  オプション: [root 権限なしでコマンドを実行するように Docker クライアントを構成します](https://docs.docker.com/engine/installation/linux/linux-postinstall)。このステップを実行しない場合は、`bx login`、`bx cr login`、`docker pull`、`docker push` の各コマンドを、**sudo** を使用するか root として実行する必要があります。

これで、{{site.data.keyword.registrylong_notm}} 専用レジストリーに固有の名前空間をセットアップできます。

## {{site.data.keyword.registrylong_notm}} (`bx cr`) プラグインの更新
{: #registry_cli_update}

新しいフィーチャーを使用するために {{site.data.keyword.registrylong_notm}} CLI を定期的に更新することをお勧めします。{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
bx login```
    {: pre}

2.  container-registry プラグインを更新します。

    ```
bx plugin update container-registry -r Bluemix```
    {: pre}

3.  プラグインが正常に更新されたことを確認します。

    ```
bx plugin list```
     {: pre}


## {{site.data.keyword.registrylong_notm}} (`bx cr`) プラグインのアンインストール
{: #registry_cli_uninstall}

container-registry プラグインは、もはや必要がない場合、アンインストールすることができます。{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
bx login```
    {: pre}

2.  container-registry プラグインをアンインストールします。

    ```
bx plugin uninstall container-registry```
    {: pre}

3.  プラグインが正常にアンインストールされたことを確認します。

    ```
bx plugin list```
    {: pre}

    container-registry プラグインは結果に表示されません。


## 名前空間のセットアップ
{: #registry_namespace_add}

Docker イメージを安全に保管するには、{{site.data.keyword.registrylong_notm}} 専用レジストリー内に名前空間を作成する必要があります。{:shortdesc}

開始前に、以下のことを行います。

-   [{{site.data.keyword.Bluemix_notm}} CLI と container-registry プラグインをインストールします](#registry_cli_install)。
-   [レジストリー名前空間の使用方法と命名について計画します](registry_overview.html#registry_namespaces)。

概説資料の[名前空間のセットアップ](index.html#registry_namespace_add)を参照して名前空間を作成します。

これで、[{{site.data.keyword.Bluemix_notm}} レジストリー内の名前空間に Docker イメージをプッシュし](registry_images_.html#registry_images_pushing)、それらのイメージをアカウント内の他のユーザーと共有できるようになりました。

## 名前空間の削除
{: #registry_remove}

レジストリーの名前空間が不要になったら、{{site.data.keyword.Bluemix_notm}} アカウントからその名前空間を削除することができます。{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}} にログインします。

    ```
bx login```
    {: pre}

2.  使用可能な名前空間をリストします。

    ```
bx cr namespace-list```
    {: pre}

3.  名前空間を削除します。 

    **注意:** 名前空間を削除すると、その名前空間に保管されているイメージもすべて削除されます。このアクションは元に戻せません。
    
    _&lt;my_namespace&gt;_ を、削除する名前空間に置換します。


    ```
    bx cr namespace-rm <my_namespace>
    ```
    {: pre}

    名前空間を削除した後は、保管されていたイメージの数に応じて、その名前空間が再使用可能になるまでに数分間かかる可能性があります。
