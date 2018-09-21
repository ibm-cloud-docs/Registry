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


# 常見問題
{: #registry_faq}


## 如何列出公用映像檔？
{: #faq_list_public_images}

若要列出公用映像檔，請執行下列　`ibmcloud` 指令，設定目標全球登錄並列出 IBM 提供的公用映像檔：

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}


## 我可以使用非 Docker 工具來建置映像檔並將它們推送至登錄嗎？
{: #faq_tools}

可以，如果工具支援 OCI 映像檔格式和通訊協定的話。
