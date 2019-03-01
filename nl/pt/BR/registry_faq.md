---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry

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
{:faq: data-hd-content-type='faq'}

# Perguntas mais frequentes (FAQs)
{: #registry_faq}

Perguntas mais frequentes sobre o {{site.data.keyword.registrylong}}.
{: shortdesc}

## Como listar imagens públicas?
{: #faq_list_public_images}
{: faq}

Para listar imagens públicas, execute os comandos `ibmcloud` a seguir para ter como destino o registro global e listar as imagens públicas fornecidas pela IBM:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Posso usar ferramentas que não são do Docker para construir minhas imagens e enviá-las por push para o registro?
{: #faq_tools}
{: faq}

Sim, desde que a ferramenta suporte o formato e o protocolo de imagem do OCI.
