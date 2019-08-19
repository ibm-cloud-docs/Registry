---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# Conservazione delle immagini
{: #registry_retention}

Puoi decidere se eliminare o conservare le immagini.
{:shortdesc}

## Pianificazione della conservazione
{: #retention_plan}

Il [comando `ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) funziona su una base per spazio dei nomi, pertanto, utilizzando più spazi dei nomi nella tua pipeline, puoi applicare diversi criteri di conservazione per soddisfare in modo migliore i tuoi requisiti.

Prendi in considerazione una delivery pipeline con ambienti di sviluppo, di preparazione e di produzione. Nel modo in cui viene fornito il codice, l'integrazione e lo sviluppo continui eseguono il push delle immagini nel registro e poi le distribuiscono direttamente al tuo ambiente di sviluppo. Dopo la verifica, alcune build dallo sviluppo vengono promosse alla fase di preparazione e poi potenzialmente alla produzione. In questo scenario, la modifica alla frequenza di immagini è più veloce nello sviluppo e più lenta nella produzione. Se tutti i tuoi ambienti eseguono il pull delle immagini dallo stesso spazio dei nomi, può essere difficile scegliere un numero di immagini appropriato da conservare a causa di questa differenza nella velocità.

Un buon approccio è quello di fornire tutte le immagini in uno spazio dei nomi di sviluppo, ad esempio, `project-development` e poi utilizzare il comando [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) per contrassegnare con tag l'immagine in uno spazio dei nomi diverso quando viene promossa a una fase superiore della pipeline. Nel precedente esempio, puoi avere tre spazi dei nomi: sviluppo `project-development`, preparazione, `project-staging` e produzione, `project-production`. Quando stai promuovendo dallo sviluppo alla preparazione, le immagini vengono contrassegnate mediante tag dallo spazio dei nomi `project-development` nello spazio dei nomi `project-staging` e le immagini da `project-staging` vengono utilizzate per la distribuzione. In modo simile, quando stai promuovendo dalla preparazione alla produzione, le immagini vengono contrassegnate mediante tag dallo spazio dei nomi `project-staging` nello spazio dei nomi `project-production` e le immagini di `project-production` vengono utilizzare nella distribuzione di produzione.

Ottieni i seguenti vantaggi utilizzando questa tecnica:

* Puoi scegliere diverse impostazioni di conservazione per gli spazi dei nomi di sviluppo, preparazione e produzione.
* Minimizzi le possibilità di rimuovere in modo accidentale un'immagine che potrebbe essere in uso nei tuoi ambienti di preparazione o produzione, in confronto all'utilizzo di un solo spazio dei nomi per tutte le immagini.
* Puoi utilizzare politiche [IAM](/docs/services/Registry?topic=registry-iam) diverse. Ad esempio, puoi avere un accesso più restrittivo alle immagini di produzione.
* Puoi firmare le immagini di produzione, ma lasciare le immagini di sviluppo e preparazione non firmate.

## Ripulisci i tuoi spazi dei nomi conservando solo le immagini che soddisfano i tuoi criteri
{: #retention_images}

Conserva le immagini di ogni repository all'interno di uno spazio dei nomi in {{site.data.keyword.registrylong_notm}} applicando dei criteri specificati. Tutte le altre immagini nello spazio dei nomi vengono eliminate.
{:shortdesc}

Il [comando `ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) elenca le immagini che saranno eliminate e ti fornisce l'opzione di annullare l'eliminazione.

Quando a un'immagine, all'interno di un repository, viene fatto riferimento da più tag, tale immagine viene contata una sola volta. Le immagini più recenti vengono conservate. L'età viene determinata dal momento in cui è stata creata l'immagine, non da quando ne è stato eseguito il push al registro.
{: tip}

L'eliminazione di un'immagine non può essere annullata. L'eliminazione di un'immagine utilizzata da una distribuzione esistente potrebbe causare la mancata riuscita di un ridimensionamento, di una ripianificazione o di entrambe le operazioni.
{: important}

Per ridurre il numero di immagini in ogni repository all'interno del tuo spazio dei nomi utilizzando la CLI, completa la seguente procedura:

1. Effettua l'accesso a {{site.data.keyword.cloud_notm}} eseguendo il comando `ibmcloud login`.
2. Scegli il registro in cui vuoi ripulire le tue immagini immettendo il seguente comando e selezionando la regione appropriata:

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. Per conservare alcune immagini ed eliminarne altre, immetti il seguente comando:

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   Dove `IMAGECOUNT` è il numero di immagini che vuoi conservare per ogni repository all'interno del tuo spazio dei nomi, `NAMESPACE`.

3. Verifica che le immagini siano state eliminate immettendo il seguente comando e controlla che le immagini non siano visualizzate nell'elenco.

   ```
   ibmcloud cr image-list
   ```
   {: pre}
