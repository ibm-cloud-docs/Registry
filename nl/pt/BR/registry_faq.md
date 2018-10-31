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


# Perguntas frequentes
{: #registry_faq}


## Como listar imagens públicas?
{: #faq_list_public_images}

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

Sim, desde que a ferramenta suporte o formato e o protocolo de imagem do OCI.
