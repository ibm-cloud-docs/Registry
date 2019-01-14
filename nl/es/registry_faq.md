---

copyright:
  years: 2018, 
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:faq: data-hd-content-type='faq'}

# Preguntas frecuentes (FAQ)
{: #registry_faq}

Preguntas frecuentes sobre {{site.data.keyword.registrylong}}.
{: shortdesc}

## ¿Cómo listo imágenes públicas?
{: #faq_list_public_images}
{: faq}

Para listar imágenes públicas, ejecute los mandatos siguientes de `ibmcloud` para acceder al registro global y listar las imágenes públicas proporcionadas por IBM:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## ¿Puedo utilizar herramientas que no sean docker para crear mis imágenes y enviarlas por push al registro?
{: #faq_tools}
{: faq}

Sí, siempre que la herramienta admita el formato y el protocolo de la imagen OCI.
