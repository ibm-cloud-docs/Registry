---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-28"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Gestione dei limiti di quota per l'archiviazione e il traffico di pull
{: #registry_quota}

Puoi limitare la quantità di archiviazione e di traffico di pull che può essere utilizzata nel tuo account {{site.data.keyword.Bluemix}} impostando e gestendo dei limiti
di quota personalizzati.
{:shortdesc}


## Impostazione dei limiti di quota per l'archiviazione e il pull delle immagini
{: #registry_quota_set}

Puoi limitare la quantità di archiviazione e di traffico di pull per le tue immagini private impostando
i tuoi propri limiti di quota.
{:shortdesc}

Quando esegui l'aggiornamento al piano standard {{site.data.keyword.registryshort_notm}},
puoi beneficiare di quantità illimitate di archiviazione e traffico di pull per le tue immagini
private. Per evitare di superare il tuo livello di pagamento preferito, puoi impostare delle quote individuali per la
quantità di archiviazione e traffico di pull. I limiti di quota vengono applicati a tutti gli spazi dei nomi che hai configurato
in {{site.data.keyword.registrylong_notm}}. Se stai utilizzando il piano di
servizio gratuito, puoi anche impostare quote personalizzate all'interno della tua quantità gratuita di archiviazione e traffico di pull.

Per impostare una quota:

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Esamina i tuoi limiti di quota correnti per l'archiviazione e il traffico di pull.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Il tuo output
sarà simile al seguente.

    ```
    Richiamo delle quote e dell'utilizzo per il mese corrente, per l'account '<proprietario_account> Account'...

    QUOTA              LIMITE    UTILIZZATO
    Traffico di pull   5,1 GB    0 B
    Archiviazione      512 MB    511 MB

    OK
    ```
    {: screen}

3.  Modifica il limite di quota per l'archiviazione e il traffico di pull. Per modificare l'utilizzo del traffico di
pull, specifica l'opzione **traffic** e sostituisci
_&lt;quota_traffico&gt;_ con il valore in megabyte che vuoi impostare per la quota del traffico
di pull. Se vuoi modificare la quantità di archiviazione nel tuo account, specifica
l'opzione **storage** e sostituisci _&lt;quota_archiviazione&gt;_ con il
valore in megabyte da impostare.

    Se utilizzi il piano gratuito, non puoi impostare la tua quota su una quantità che superi il livello gratuito. Il livello gratuito permesso per l'archiviazione è 512 MB e per il traffico è 5120 MB.
    {:tip}

    ```
    ibmcloud cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    Esempio
per impostare il tuo limite di quota per l'archiviazione su 600 megabyte e il traffico di pull su 7000 megabyte:

    ```
    ibmcloud cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}


## Controllo dei limiti di quota e dell'utilizzo per l'archiviazione e il pull delle immagini
{: #registry_quota_get}

Puoi riesaminare i tuoi limiti di quota e controllare il tuo utilizzo corrente dell'archiviazione e del traffico di pull
per il tuo account.
{:shortdesc}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Esamina i tuoi limiti di quota correnti per l'archiviazione e il traffico di pull.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Il tuo output
sarà simile al seguente.

    ```
    Richiamo delle quote e dell'utilizzo per il mese corrente, per l'account '<proprietario_account> Account'...

    QUOTA              LIMITE    UTILIZZATO
    Traffico di pull   5,1 GB    0 B
    Archiviazione      512 MB    511 MB

    OK
    ```
    {: screen}


## Liberazione dello spazio di archiviazione utilizzato e modifica dei piani di servizio o dei limiti di quota per restare entro i limiti di quota forniti
{: #registry_quota_freeup}

Se hai superato i limiti di quota impostati per il tuo account {{site.data.keyword.Bluemix_notm}}, puoi liberare lo spazio di archiviazione
e modificare il tuo piano di servizio o i tuoi limiti di quota per continuare a eseguire il push e il pull delle immagini da e verso
il tuo spazio dei nomi.
{:shortdesc}

Per liberare lo spazio di archiviazione delle immagini nel tuo account {{site.data.keyword.Bluemix_notm}}:

1.  Elenca tutte le immagini di tutti gli spazi dei nomi del tuo account {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud cr images
    ```
    {: pre}

2.  Rimuovi un'immagine dal tuo spazio dei nomi. Sostituisci
_&lt;nome_immagine&gt;_ con il nome dell'immagine che vuoi rimuovere.

    ```
    ibmcloud cr image-rm <image_name>
    ```
    {: pre}

    A seconda della dimensione dell'immagine, potrebbero essere richiesti alcuni minuti prima che l'immagine venga rimossa e l'archiviazione sia disponibile.
    {:tip}

3.  Riesamina il tuo utilizzo di quota di archiviazione.

    ```
    ibmcloud cr quota
    ```
    {: pre}

4. Non puoi ridurre il tuo utilizzo di traffico di pull in un periodo di fatturazione.
   {:tip}

    Per continuare a eseguire il pull di immagini dai tuoi spazi dei nomi, scegli tra le seguenti opzioni.

    -   Attendi l'inizio del nuovo ciclo di fatturazione.
    -   Se hai un piano gratuito, [esegui l'upgrade al piano di servizio
standard](registry_overview.html#registry_plan_upgrade).
    -   Se hai già un piano standard, [imposta i nuovi limiti
di quota per il traffico di pull](#registry_quota_set).
