---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, user access role policies, access policies, policies

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

# ユーザー・アクセスの役割ポリシーの定義
{: #user access}

管理者は、レジストリーのアクセス・ポリシーを定義して、さまざまなユーザーを対象にさまざまなレベルのアクセス権限を作成することができます。 例えば、特定のユーザーには割り当て量を設定する権限を与える一方で、他のユーザーには割り当て量を表示する権限だけを与えることができます。
{: shortdesc}

{{site.data.keyword.registrylong}} を使用するすべてのユーザー用にアクセス・ポリシーを定義する必要があります。 アクセス・ポリシーの適用範囲は、実行を許可する操作を定義するためのユーザーの定義役割に基づきます。 事前定義されているポリシーもあれば、カスタマイズ可能なポリシーもあります。

2018 年 10 月 4 日より前に {{site.data.keyword.registrylong_notm}} の使用を開始した場合は、ポリシーを有効にする前に、ポリシーの制約を有効にしなければなりません。[既存のユーザーに対してポリシー制約を有効にする](#existing_users)を参照してください。
{: tip}

{{site.data.keyword.iamlong}} (IAM) アクセス役割ポリシーについて詳しくは、[{{site.data.keyword.iamshort}}](/docs/iam/index.html#iamoverview) を参照してください。

## ポリシーの作成
{: #create}

リソースへのアクセスを制御しようとしている場合は、役割をユーザーかサービス ID に割り当てなければなりません。 {{site.data.keyword.registrylong_notm}} リソースへのアクセス権限は、名前によって単一の名前空間リソースに対して付与することも、サービス全体、つまりアカウント内のすべての名前空間に対して付与することもできます。

すべてのものへのアクセス権限を付与しようとしている場合は、リソース・タイプやリソースを指定しないでください。 特定の名前空間へのアクセス権限を付与しようとしている場合は、リソース・タイプを `namespace` として指定し、リソース名をリソースとして使用します。

**始めに**

- 各ユーザーが {{site.data.keyword.registrylong_notm}} 内のどのリソースに対してどの役割が必要か判別するには、[IAM 役割](/docs/services/Registry/iam.html#iam)を参照してください。 複数のポリシーを作成できるということを考慮してください。例えば、あるリソースに対して書き込みアクセス権限を付与し、別のリソースに対しては読み取りアクセス権限のみを付与し、さらに別のリソースに対してはアクセス権限を付与しないようにすることができます。 ポリシーは加算的です。つまり、グローバルな読み取りポリシーとリソースを有効範囲とする書き込みポリシーがあると、そのリソースに対する読み取りアクセス権限と書き込みアクセス権限が両方とも付与されます。

- [ユーザーの招待とアクセス権限の割り当て](/docs/iam/iamuserinv.html#iamuserinv)を行います。

  ユーザーが {{site.data.keyword.containerlong_notm}} 内でクラスターを作成できるようにしようとしている場合は、そのユーザーに {{site.data.keyword.registrylong_notm}} 管理者の役割を割り当てており、リソース・グループを割り当てていないことを確認してください。[クラスターの作成の準備](/docs/containers/cs_clusters.html#cluster_prepare)を参照してください。
  {: tip}

{{site.data.keyword.registrylong_notm}} のポリシーを作成するには、サービス名フィールドを `container-registry` にしなければなりません。

- ユーザーのポリシーを作成するには、[リソースに対するアクセス権限の管理](/docs/iam/mngiam.html#iammanidaccser)を参照してください。
- サービス ID のポリシーを作成するには、`ibmcloud iam service-policy-create` コマンドを実行するか、GUI を使用して役割をサービス ID にバインドします。 ポリシーを作成するには、管理者の役割が必要です。 所有するアカウントには管理者の役割が自動的に与えられます。 詳しくは、[サービス ID の作成と処理](/docs/iam/serviceid.html#serviceids)と、[サービス ID のアクセス・ポリシーの管理](/docs/iam/serviceidaccess.html#serviceidpolicy)を参照してください。

## 既存のユーザーに対してポリシー制約を有効にする
{: #existing_users}

2018 年 10 月 4 日より後にプロビジョンしたユーザーの場合、デフォルトで IAM ポリシーが有効になっています。 2018 年 10 月 4 日より前にプロビジョンしたユーザーの場合、ポリシーを作成した後に、そのポリシーが有効になるように、ポリシーの制約を有効になければなりません。

1. ユーザーとサービス ID の[ポリシーを作成](#create)します。

2. ポリシーの制約を有効にするには、[`bx cr iam-policies-enable`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_iam_policies_enable) コマンドを実行します。

    アカウントにマネージャーの役割がないと、`ibmcloud cr iam-policies-enable` コマンドを実行できません。 所有するアカウントにはマネージャーの役割が自動的に与えられます。
    {: tip}
