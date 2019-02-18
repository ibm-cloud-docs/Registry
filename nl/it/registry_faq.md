---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-04"

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

# Domande frequenti (FAQ)
{: #registry_faq}

Domande frequenti su {{site.data.keyword.registrylong}}.
{: shortdesc}

## Come elenco le immagini pubbliche?
{: #faq_list_public_images}
{: faq}

Per elencare le immagini pubbliche, immetti i seguenti comandi `ibmcloud` per selezionare il registro globale ed elencare le immagini pubbliche fornite da IBM.

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Posso utilizzare strumenti non docker per creare le mie immagini e passarle al registro?
{: #faq_tools}
{: faq}

Sì, a condizione che lo strumento supporti il protocollo e il formato l'immagine OCI.
