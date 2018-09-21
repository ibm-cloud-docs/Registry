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


# Domande frequenti (FAQ) 
{: #registry_faq}


## Come elenco le immagini pubbliche? 
{: #faq_list_public_images}

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

Sì, a condizione che lo strumento supporti il protocollo e il formato l'immagine OCI.
