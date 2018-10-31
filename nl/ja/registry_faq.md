---

copyright:
  years: 2018, 
lastupdated: "2018-09-03"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# FAQ
{: #registry_faq}


## パブリック・イメージの一覧を表示する方法を教えてください。
{: #faq_list_public_images}

パブリック・イメージの一覧を表示するには、次のように `ibmcloud` コマンドを実行してください。グローバル・レジストリーを対象にしてから、 IBM 提供のパブリック・イメージの一覧を表示します。

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}


## Docker 以外のツールで、イメージを作成してレジストリーにプッシュすることはできますか?
{: #faq_tools}

はい。ただし、OCI のイメージ・フォーマットおよびプロトコルに対応したツールでなければなりません。
