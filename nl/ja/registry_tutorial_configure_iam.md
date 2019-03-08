---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-25"

keywords: IBM Cloud Container Registry, user access, tutorial

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

# チュートリアル: {{site.data.keyword.registrylong_notm}} リソースに対するアクセス権限の付与
{: #iam_access}

このチュートリアルには、{{site.data.keyword.iamlong}} (IAM) を {{site.data.keyword.registrylong_notm}} 用に構成して、リソースへのアクセス権限を付与する方法が示されています。
{:shortdesc}

このチュートリアルの完了には、約 45 分間かかります。

**始めに**

- [{{site.data.keyword.registrylong_notm}} の概説](/docs/services/Registry?topic=registry-index#index)の指示を完了します。

- {{site.data.keyword.cloud_notm}} CLI に関する `container-registry` CLI プラグインの最新バージョンがあることを確認します。[`container-registry` CLI プラグインの更新](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update)を参照してください。

- このチュートリアルで使用できる 2 つの [{{site.data.keyword.cloud_notm}} アカウント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login) へのアクセス権限がなければなりません。User A 用に 1 つと User B 用に 1 つで、それぞれ固有の E メール・アドレスを使用しなければなりません。 自分のアカウントの User A で作業し、そのアカウントを使用するように別のユーザー User B を招待します。 2 つ目の {{site.data.keyword.cloud_notm}} アカウントを作成することを選択することも、{{site.data.keyword.cloud_notm}} アカウントを持つ同僚と作業することもできます。

- 2018 年 10 月 4 日より前にご使用のアカウントで {{site.data.keyword.registrylong_notm}} の使用を開始した場合は、`ibmcloud cr iam-policies-enable` コマンドを実行して、IAM ポリシーの制約を有効にしなければなりません。 {{site.data.keyword.registrylong_notm}} 名前空間を使用する他のユーザーをご使用の IBM Cloud アカウントに招待した場合は、そのユーザーのアクセスの途絶を防ぐために、User A とは別のアカウントを使用してください。

## ステップ 1: ユーザーがレジストリーを構成するのを許可する
{: #configure_registry}

このセクションでは、2 人目のユーザーをご使用のアカウントに追加し、{{site.data.keyword.registrylong_notm}} を構成する権限を付与します。
{:shortdesc}

1. 以下のように、User B を User A のアカウントに追加します。

    1. 次のコマンドを実行して、User A のアカウントにログインします。

        ```
        ibmcloud login
        ```
        {: pre}

    2. 次のコマンドを実行して、User A のアカウントにアクセスするように User B を招待します。_`<user.b@example.com>`_ は User B の E メール・アドレスです。

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. 次のコマンドを実行して、User A のアカウント ID を取得します。

        ```
        ibmcloud target
        ```
        {: pre}

        Account 行の括弧 ( ) に囲まれているアカウント ID をメモします。

2. User B は User A のアカウントをターゲットにできるものの、まだ {{site.data.keyword.registrylong_notm}} で何も行えないことを確認します。

    1. User B としてログインし、次のコマンドを実行して User A のアカウントをターゲットにします。_`<YourAccountID>`_ は User A のアカウント ID です。

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 次のコマンドを実行し、レジストリー割り当て量が 4 GB のトラフィックになるように編集を試行します。

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        User B には正しいアクセス権限がないので、コマンドは失敗します。

3. 以下のように、User B が {{site.data.keyword.registrylong_notm}} を構成できるように、User B にマネージャーの役割を付与します。

    1. 次のコマンドを実行し、ご使用のアカウントに自分自身 (User A) として再ログインします。

        ```
        ibmcloud login
        ```
        {: pre}

    2. 次のコマンドを実行して、User B にマネージャーの役割を付与するポリシーを作成します。

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. 以下のように、User B が User A のアカウントで割り当て量を変更できるようになったことを確認します。

    1. 次のコマンドを実行して、User B として User A のアカウントをターゲットにしてログインします。

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 次のコマンドを実行し、レジストリー割り当て量が 4 GB のトラフィックになるように編集を試行します。

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        User B には正しいタイプのアクセス権限があるので、このコマンドは正常に実行されます。

    3. この時点で次のコマンドを実行し、割り当て量を変更して元に戻します。
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. 以下のようにクリーンアップします。

    1. 次のコマンドを実行し、ご使用のアカウントに自分自身 (User A) として再ログインします。
  
        ```
        ibmcloud login
        ```
        {: pre}
  
    2. 次のコマンドを実行して、User B のポリシーをリストし、作成したばかりのポリシーを見つけ、その ID をメモします。
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. 次のコマンドを実行して、ポリシーを削除します。_`<Policy_ID>`_ はポリシー ID です。
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## ステップ 2: ユーザーが特定の名前空間にアクセスするのを許可する
{: #access_resources}

このセクションでは、サンプルのイメージを使用して名前空間を作成し、その名前空間にアクセス権限を付与します。 各名前空間に対するさまざまな役割を付与するポリシーを作成して、その影響を示します。
{:shortdesc}

1. User A のアカウント内に 3 つの名前空間を新しく作成します。 これらの名前空間は地域全体で固有でなければならないので、独自の名前空間の名前を選択しますが、このチュートリアルでは例として `namespace_a`、`namespace_b`、`namespace_c` を使用します。

    1. 次のコマンドを実行して、User A としてログインします。

        ```
        ibmcloud login
        ```
        {: pre}

    2. 次のコマンドを実行して、名前空間 `namespace_b` を作成します。

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}

        名前空間の名前は、領域内で固有でなければなりません。
        {: tip}

    3. 次のコマンドを実行して、別の名前空間 `namespace_c` を作成します。

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. 以下のようにして、User B が何も参照できないことを確認します。

    1. 次のコマンドを実行して、User B として User A のアカウントをターゲットにしてログインします。

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 次のコマンドを実行して、User B としてイメージのリストを試行します。

        ```
        ibmcloud cr images
        ```
        {: pre}

        User B には名前空間へのアクセス権限がないので、空のリストが戻されます。

3. 次のコマンドを実行して、User B が名前空間と対話できるようにするポリシーを作成します。

    1. 次のコマンドを実行して、User A のアカウントとしてログインします。

        ```
        ibmcloud login
        ```
        {: pre}

    2. 次のコマンドを実行して、少なくとも 3 つの名前空間がリストされることを確認します。

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        このチュートリアルで作成した 3 つの名前空間 (`namespace_a`、`namespace_b`、`namespace_c`) が表示されます。 これらの名前空間が表示されない場合は、戻って指示に従い、再度作成します。

    3. 次のコマンドを実行して、`namespace_b` に関するリーダーの役割を User B に付与する、ポリシーを作成します。_`<Region>`_ は、`us-south` などの[領域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)の名前です。

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource <namespace_b> --roles Reader
        ```
        {: pre}

    4. 次のコマンドを実行して、`namespace_c` に関するリーダーとライターの役割を User B に付与する 2 つ目のポリシーを作成します。

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        このコマンドは、同一のポリシー内で同じリソースに対する 2 つの役割を追加します。
        {: tip}

4. 以下のように、イメージを `namespace_a` と `namespace_b` 内にプッシュします。

    1. 次のコマンドを実行して、`hello-world` イメージをプルします。

        ```
        docker pull hello-world
        ```
        {: pre}

    2. 次のコマンドを実行して、イメージを `namespace_a` にタグ付けします。

        ```
        docker tag hello-world <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. 次のコマンドを実行して、イメージを `namespace_b` にタグ付けします。

        ```
        docker tag hello-world <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. 次のコマンドを実行して、{{site.data.keyword.registrylong_notm}} にログインします。

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. 次のコマンドを実行して、イメージを `namespace_a` にプッシュします。

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. 次のコマンドを実行して、イメージを `namespace_b` にプッシュします。

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

5. 以下のように、User B が `namespace_b` や `namespace_c` と対話できるものの、`namespace_a` とは対話できないことを確認します。

    1. 次のコマンドを実行して、User B としてログインします。

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 次のコマンドを実行して、User B には `namespace_a` へのアクセス権限がないので、User B は `namespace_b` と `namespace_c` を参照できるものの `namespace_a` を参照できないことを確認します。

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. 次のコマンドを実行して、イメージをリストします。

        ```
        ibmcloud cr images
        ```
        {: pre}

        User B には `namespace_a` へのアクセス権限がないので、`namespace_b` 内のイメージはリスト内に表示されますが `namespace_a` 内のイメージは表示されません。

    4. 次のコマンドを実行して、{{site.data.keyword.registrylong_notm}} にログインします。

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. 次のコマンドを実行して、イメージをプルします。

        ```
        docker pull <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. 次のコマンドを実行して、イメージを `namespace_b` にプッシュします。

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        User B には `namespace_b` 内でのライターの役割がないので、このコマンドは失敗します。

    7. 次のコマンドを実行して、イメージを `namespace_c` とタグ付けします。

        ```
        docker tag hello-world <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. 次のコマンドを実行して、イメージを `namespace_c` にプッシュします。

        ```
        docker push <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        User B には `namespace_c` 内でのライターの役割があるので、コマンドは正常に実行されます。

    9. 次のコマンドを実行して、`namespace_c` からプルします。

        ```
        docker pull <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        User B には `namespace_c` 内でのリーダーの役割があるので、コマンドは正常に実行されます。

6. 以下のようにクリーンアップします。

    1. 次のコマンドを実行して、User A のアカウントに再ログインします。

        ```
        ibmcloud login
        ```
        {: pre}

    2. 次のコマンドを実行して、User B のポリシーをリストします。

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        作成したばかりのポリシーを見つけ、ポリシー ID をメモします。

    3. 次のコマンドを実行し、作成したばかりのポリシーを削除します。_`<Policy_ID>`_ はポリシー ID です。

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## ステップ 3: サービス ID を作成してリソースへのアクセス権限を付与する
{: #service_id}

このセクションでは、サービス ID を構成して、{{site.data.keyword.registrylong_notm}} 名前空間へのアクセス権限を付与します。
{:shortdesc}

1. {{site.data.keyword.registrylong_notm}} へのアクセス権限を持つサービス ID をセットアップし、その ID 用の API キーを作成します。

    1. 次のコマンドを実行して、User A のアカウントにログインします。

        ```
        ibmcloud login
        ```
        {: pre}

    2. 次のコマンドを実行して、`cr-roles-tutorial` という名前のサービス ID と、説明 `"Created during the access control tutorial for Container Registry"` を作成します。

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. 次のコマンドを実行して、`namespace_a` でのリーダーの役割を付与する、サービス ID のサービス・ポリシーを作成します。

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. 次のコマンドを実行して、`namespace_b` に関するライターの役割を付与する 2 つ目のサービス・ポリシーを作成します。

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. 次のコマンドを実行して、サービス ID 用の API キーを作成します。

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. 以下のように、Docker を使用して、サービス ID の API キーでログインし (_`<API_Key>`_ は API キー)、レジストリーと対話します。

    1. 次のコマンドを実行して、{{site.data.keyword.registrylong_notm}} にログインします。

        ```
        docker login -u iamapikey -p <API_Key> <Region>.icr.io
        ```
        {: pre}

    2. 次のコマンドを実行して、ご使用のイメージをプルします。

        ```
        docker pull <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        このコマンドは正常に実行されます。

    3. 次のコマンドを実行して、ご使用のイメージを `namespace_a` にプッシュします。

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        ユーザーには `namespace_a` 内でのライターの役割がないので、このコマンドは正常に実行されません。

    4. 次のコマンドを実行して、ご使用のイメージを `namespace_b` にプッシュします。

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        ユーザーには `namespace_b` 内でのライターの役割があるので、このコマンドは正常に実行されます。

3. 以下のようにクリーンアップします。

    1. 次のコマンドを実行して、サービス・ポリシーをリストします。

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        ご使用のポリシー ID をメモします。

    2. ポリシーごとに次のコマンドを実行して、サービス・ポリシーを削除します。

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. 次のコマンドを実行して、サービス ID を削除します。

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. User A として {{site.data.keyword.registrylong_notm}} に再ログインします。

        ```
        ibmcloud cr login
        ```
        {: pre}

## ステップ 4: クリーンアップ
{: #clean_up}

このセクションでは、前のセクションで作成したリソースを削除して、ご使用のアカウントをこのチュートリアルの開始時点の状態にします。
{:shortdesc}

1. 次のコマンドを実行して、ご使用のアカウントにログインします。

    ```
    ibmcloud login
    ```
    {: pre}

2. 次のコマンドを実行して、`namespace_a`、`namespace_b`、`namespace_c` を削除します。

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. 次のコマンドを実行して、ご使用のアカウントから User B を削除します。

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

お疲れ様でした。 このチュートリアルが正常に完了しました。
