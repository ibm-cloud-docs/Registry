---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, public IBM images, images

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

# パブリック {{site.data.keyword.IBM_notm}} イメージ
{: #public_images}

コマンド・ラインを使用して、{{site.data.keyword.IBM}} 提供のイメージにアクセスできます。 グラフィカル・ユーザー・インターフェースを使用してパブリック {{site.data.keyword.IBM_notm}} イメージにアクセスすることはできなくなりました。
{:shortdesc}

## CLI を使用したパブリック IBM イメージへのアクセス
{: #public_images_cli}

コマンド・ラインを使用して、パブリック {{site.data.keyword.IBM_notm}} イメージにアクセスできます。
{:shortdesc}

**始めに**

- [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) にログインします。

  ```
  ibmcloud login
  ```
  {: pre}

パブリック・イメージをリストするには、以下のステップを実行します。

1. 以下のように、グローバル・レジストリーをターゲットにします。

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. 以下のように、{{site.data.keyword.IBM_notm}} パブリック・イメージをリストします。

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
