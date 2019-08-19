---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# イメージの保持
{: #registry_retention}

イメージを削除するか保持するかを自分で決定できます。
{:shortdesc}

## 保持の計画
{: #retention_plan}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) コマンドは名前空間ごとに動作します。したがって、パイプラインの中で複数の名前空間を使用することにより、要件に応じてそれぞれ異なる保持基準を、最適な保持基準として適用できることになります。

開発、ステージング、実稼働の各環境について、それぞれの典型的な配信パイプラインを考慮してください。コードが配信されるにつれて、継続的統合デプロイメントと継続的デプロイメントにより、イメージがレジストリーにプッシュされた後、それらがストレートに開発環境にデプロイされます。テストの後、開発によるビルドの一部がステージングにプロモートされた後、場合によって実稼働へとさらにプロモートされます。このシナリオの場合、イメージの変更速度は開発では最速であり、実稼働では最も遅くなります。すべての環境が同じ名前空間からイメージをプルする場合、そのような速度の違いのため、保持するイメージ数を適切に選択することは困難な場合があります。

1 つの有効なアプローチは、すべてのイメージを開発名前空間 (`project-development` など) に配信した後、パイプラインのうちさらに高いステージへとプロモートされる時点で、[`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) コマンドを使用することによって異なる名前空間になるようにイメージをタグ付けするというものです。前出の例の場合、開発には `project-development`、ステージングには `project-staging`、実稼働には `project-production` の 3 つの名前空間とすることができます。開発からステージングにプロモートする際には、イメージのタグ変更により `project-development` 名前空間から `project-staging` 名前空間に変更し、`project-staging` 名前空間のイメージをデプロイメントに使用します。同じように、ステージングから実稼働にプロモートする場合、イメージのタグ変更により `project-staging` 名前空間から `project-production` 名前空間に変更し、`project-production` 名前空間のイメージを実稼働デプロイメントに使用します。

この手法を使用することには、次のようなメリットがあります。

* 開発、ステージング、実稼働の各名前空間について、それぞれ異なる保持設定を選択できます。
* 全イメージに単一の名前空間を使用する場合に比べ、ステージング環境または実稼働環境で使用されるかもしれないイメージを誤って削除してしまう可能性が最小限になります。
* 異なる複数の [IAM](/docs/services/Registry?topic=registry-iam) ポリシーを使用できます。例えば、実稼働イメージへのアクセスの制限をさらに厳しくすることができます。
* 実稼働イメージに署名する一方、開発イメージとステージング・イメージは未署名のままにすることができます。

## 基準を満たすイメージのみ保持することにより名前空間をクリーンアップする
{: #retention_images}

指定する基準を適用することにより、{{site.data.keyword.registrylong_notm}} の中の名前空間内の各リポジトリーのイメージを保持します。その名前空間の中のその他のすべてのイメージは削除されます。
{:shortdesc}

[`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) コマンドを使用すると、削除されることになるイメージのリストが出力され、削除の前にキャンセルできるようになります。

リポジトリー内で 1 つのイメージが複数のタグによって参照されている場合、そのイメージは 1 回のみカウントされます。最新のイメージが保持されます。経過時間は、イメージがレジストリーにプッシュされた時刻ではなくイメージ作成時刻によって決定されます。
{: tip}

イメージの削除は元に戻せません。 既存のデプロイメントで使用されているイメージを削除すると、スケールアップ、スケジュール変更、またはその両方が失敗する場合があります。
{: important}

CLI を使用することにより名前空間内の各リポジトリーの中のイメージの数を少なくするには、次の手順を実行します。

1. `ibmcloud login` コマンドを実行して {{site.data.keyword.cloud_notm}} にログインします。
2. 次のコマンドを実行し、適切なリージョンを選択することにより、イメージをクリーンアップするレジストリーを選択します。

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. 一部のイメージを保持し、それ以外は削除するには、次のコマンドを実行します。

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   `IMAGECOUNT` は、名前空間 `NAMESPACE` 内の各リポジトリーについて保持するイメージの数です。

3. 以下のコマンドを実行して、リストに削除対象のイメージが表示されないことを確認することにより、それらのイメージが削除されたことを確認してください。

   ```
   ibmcloud cr image-list
   ```
   {: pre}
