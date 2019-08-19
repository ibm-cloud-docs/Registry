---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, FAQ, Vulnerability Advisor,

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

# Domande frequenti (FAQ)
{: #registry_faq}

Domande frequenti su {{site.data.keyword.registrylong}}.
{: shortdesc}

## Come elenchi le immagini pubbliche?
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

Sì, se lo strumento supporta il protocollo e il formato dell'immagine OCI.

## Come utilizzi il controllo dell'accesso con {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}?
{: #faq_access_control}
{: faq}

Puoi creare delle politiche {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) per controllare l'accesso ai tuoi spazi dei nomi in {{site.data.keyword.registrylong_notm}}. Per ulteriori informazioni, vedi [Esercitazione: concessione dell'accesso alle risorse {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam_access) e [Gestione dell'accesso utente con Identity and Access Management (IAM)](/docs/services/Registry?topic=registry-iam).

## Quali regioni sono disponibili per {{site.data.keyword.registrylong_notm}}?
{: #faq_regions}
{: faq}

Puoi ospitare le immagini nelle [regioni locali](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local). Le immagini pubbliche ospitate da IBM sono disponibili nel [registro globale](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## Perché ho ricevuto un messaggio di errore di scansione non trovata per un'immagine appena aggiunta?
{: #faq_va_new_scan_error}
{: faq}

Se ricevi il report di vulnerabilità immediatamente dopo aver aggiunto l'immagine al registro, potresti ricevere il seguente errore:

```
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

Ricevi questo messaggio perché le immagini vengono scansionate in modo asincrono rispetto alle richieste per i risultati e il processo di scansione impiega del tempo per essere completato. Durante un'operazione normale, la scansione viene completata nei primi minuti dopo che hai aggiunto l'immagine al registro. Il tempo necessario per il completamento dipende da variabili come la dimensione dell'immagine e la quantità di traffico ricevuta dal registro.

Se ricevi questo messaggio come parte di una pipeline di creazione e visualizzi questo errore regolarmente, prova ad aggiungere una logica di nuovo tentativo che contiene una breve pausa.

Se ancora hai delle prestazioni non accettabili, contatta il supporto, vedi [Come ottenere aiuto e supporto per {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-ts_index#gettinghelp).

## Come viene attivata la scansione del Controllo vulnerabilità?
{: #faq_va_trigger_scan}
{: faq}

La scansione di un'immagine viene attivata in uno dei seguenti modi:

- Se viene eseguito il push di una nuova immagine al registro.
- Se l'ultima scansione è più vecchia di 7 giorni, l'immagine viene accodata per la nuova scansione, che potrebbe comportare del tempo per il completamento.
- Se viene rilasciato un nuovo avviso di sicurezza per un pacchetto installato nell'immagine, l'immagine viene accodata per la nuova scansione, che potrebbe comportare del tempo per il completamento. Le nuove scansioni vengono attivate quando sono disponibili delle release di nuovi avvisi di sicurezza solo per le immagini Ubuntu e Debian.

## Quanto spesso gli avvisi di sicurezza vengono aggiornati?
{: #faq_va_update_security_notice}
{: faq}

Gli avvisi di sicurezza per il Controllo vulnerabilità vengono caricati dai siti del sistema operativo dei fornitori circa ogni 12 ore.
