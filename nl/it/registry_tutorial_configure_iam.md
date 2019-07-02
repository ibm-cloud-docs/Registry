---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-19"

keywords: IBM Cloud Container Registry, user access, tutorial, access control, 

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

# Esercitazione: concessione dell'accesso alle risorse {{site.data.keyword.registrylong_notm}}
{: #iam_access}

Utilizza questa esercitazione per scoprire come concedere l'accesso alle tue risorse configurando {{site.data.keyword.iamlong}} (IAM) per {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Questa esercitazione dura circa 45 minuti.

**Prima di iniziare**

- Completa le istruzioni in [Introduzione a {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started).

- Assicurati di avere la versione più recente del plug-in CLI `container-registry` per la CLI {{site.data.keyword.cloud_notm}}, consulta [Aggiornamento del plug-in `container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).

- Devi avere accesso a due [account {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login) che puoi utilizzare con questa esercitazione, uno per l'utente A e uno per l'utente B, ognuno dei quali deve utilizzare un indirizzo email univoco. Utilizza il tuo account, come utente A e invita un altro utente, l'utente B, ad utilizzare il tuo account. Puoi scegliere di creare un secondo account {{site.data.keyword.cloud_notm}}, oppure di collaborare con un collega che dispone di un account {{site.data.keyword.cloud_notm}}.

- Se hai iniziato ad utilizzare {{site.data.keyword.registrylong_notm}} nel tuo account prima del 4 ottobre 2018, devi abilitare l'applicazione della politica IAM eseguendo il comando `ibmcloud cr iam-policies-enable`. Se hai invitato altri utenti che utilizzano i tuoi spazi dei nomi {{site.data.keyword.registrylong_notm}} nel tuo account IBM Cloud, utilizza un account diverso come utente A per evitare l'interruzione del loro accesso.

## Passo 1: autorizza un utente per la configurazione del registro
{: #configure_registry}

In questa sezione, aggiungi un secondo utente al tuo account e concedi la capacità di configurare {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Aggiungi l'utente B all'account dell'utente A:

    1. Accedi all'account dell'utente A, immettendo il seguente comando:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Invita l'utente B ad accedere all'account dell'utente A, immettendo il seguente comando, dove _`<user.b@example.com>`_ è l'indirizzo email dell'utente B:

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. Ottieni l'ID account dell'utente A immettendo il seguente comando:

        ```
        ibmcloud target
        ```
        {: pre}

        Prendi nota dell'ID account tra parentesi ( ) nella riga Account.

2. Controlla che l'utente B può selezionare l'account dell'utente A ma non può ancora far nulla con {{site.data.keyword.registrylong_notm}}:

    1. Accedi come utente B e seleziona l'account dell'utente A immettendo il seguente comando, dove _`<YourAccountID>`_ è l'ID account dell'utente A:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Prova a modificare la tua quota di registro con 4 GB di traffico immettendo il seguente comando:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        Il comando ha esito negativo perché l'utente B non dispone dei diritti di accesso.

3. Concedi all'utente B il ruolo di Gestore in modo che possa configurare {{site.data.keyword.registrylong_notm}}:

    1. Accedi nuovamente al tuo account come te stesso, cioè l'utente A, immettendo il seguente comando:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Crea una politica che concede il ruolo di Gestore all'utente B immettendo il seguente comando:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. Controlla che l'utente B possa ora modificare le quote nell'account dell'utente A:

    1. Accedi come utente B, selezionando l'account dell'utente A e immettendo il seguente comando:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Prova a modificare la tua quota di registro con 4 GB di traffico immettendo il seguente comando:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        Funziona perché l'utente B ha il tipo di accesso corretto.

    3. Ora modifica la quota per riportarla al precedente valore immettendo il seguente comando:
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. Ripulisci:

    1. Accedi nuovamente al tuo account come te stesso, cioè l'utente A, immettendo il seguente comando:
  
        ```
        ibmcloud login
        ```
        {: pre}
  
    2. Elenca le politiche per l'utente B, trova la politica appena creata immettendo il seguente comando e prendi nota dell'ID:
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. Elimina la politica immettendo il seguente comando, dove _`<Policy_ID>`_ è il tuo ID politica:
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Passo 2: autorizza un utente ad accedere a spazi dei nomi specifici
{: #access_resources}

In questa sezione, crea alcuni spazi dei nomi con immagini di esempio e concedi l'accesso ad essi. Crea le politiche per concedere ruoli diversi a ciascuno spazio dei nomi e mostrane gli effetti.
{:shortdesc}

1. Crea tre nuovi spazi dei nomi nell'account dell'utente A. Questi spazi dei nomi devono essere univoci in tutta la regione, quindi scegli i tuoi nomi degli spazi dei nomi, tieni presente che questa esercitazione utilizza `namespace_a`, `namespace_b` e `namespace_c` come esempi:

    1. Accedi come utente A, immettendo il seguente comando:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Crea `namespace_a` immettendo il seguente comando:

        ```
        ibmcloud cr namespace-add namespace_a
        ```
        {: pre}

        Lo spazio dei nomi deve essere univoco tra tutti gli account {{site.data.keyword.cloud_notm}} nella stessa regione. Gli spazi dei nomi devono avere tra i 4 e i 30 caratteri e contenere solo lettere minuscole, numeri, trattini (-) e caratteri di sottolineatura (_). Gli spazi dei nomi devono iniziare e terminare con una lettera o un numero.
        {: tip}

    3. Crea `namespace_b` immettendo il seguente comando:

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}
            
    4. Crea `namespace_c` immettendo il seguente comando:

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. Controlla che l'utente B non veda nulla:

    1. Accedi come utente B, selezionando l'account dell'utente A e immettendo il seguente comando:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Prova ad elencare le immagini come utente B immettendo il seguente comando:

        ```
        ibmcloud cr images
        ```
        {: pre}

        Restituisce un elenco vuoto perché l'utente B non ha accesso ad alcuno spazio dei nomi.

3. Crea le politiche per concedere all'utente B la possibilità di interagire con gli spazi dei nomi immettendo il seguente comando:

    1. Accedi all'account dell'utente A immettendo il seguente comando:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Controlla che siano elencati almeno tre spazi dei nomi immettendo il seguente comando:

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        Vengono visualizzati i tre spazi dei nomi che hai creato in questa esercitazione (`namespace_a`, `namespace_b` e `namespace_c`). Se questi spazi dei nomi non vengono visualizzati, torna indietro e riesegui le istruzioni per crearli.

    3. Crea una politica che concede il ruolo di Lettore per `namespace_b` all'utente B immettendo il seguente comando, dove _`<Region>`_ è il nome della tua [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions), ad esempio `us-south`:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Reader
        ```
        {: pre}

    4. Crea una seconda politica che concede i ruoli di Lettore e Scrittore per `namespace_c` all'utente B immettendo il seguente comando:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        Questo comando aggiunge due ruoli alla stessa risorsa nella stessa politica.
        {: tip}

4. Esegui il push delle immagini in `namespace_a` e `namespace_b`:

    1. Esegui il pull dell'immagine `hello-world` immettendo il seguente comando:

        ```
        docker pull hello-world
        ```
        {: pre}

    2. Contrassegna con tag l'immagine con `namespace_a` immettendo il seguente comando:

        ```
        docker tag hello-world <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Contrassegna con tag l'immagine con `namespace_b` immettendo il seguente comando:

        ```
        docker tag hello-world <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. Accedi a {{site.data.keyword.registrylong_notm}} immettendo il seguente comando:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Esegui il push dell'immagine in `namespace_a` immettendo il seguente comando:

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. Esegui il push dell'immagine in `namespace_b` immettendo il seguente comando:

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

5. Controlla che l'utente B possa interagire con `namespace_b` e `namespace_c` ma non con `namespace_a`:

    1. Accedi come utente B immettendo il seguente comando:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Mostra che l'utente B può visualizzare `namespace_b` e `namespace_c` ma non `namespace_a` perché l'utente B non ha accesso a `namespace_a`, immettendo il seguente comando:

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. Elenca le tue immagini immettendo il seguente comando:

        ```
        ibmcloud cr images
        ```
        {: pre}

        L'immagine in `namespace_b` viene mostrata nell'elenco, ma non quella in `namespace_a`, perché l'utente B non ha accesso a `namespace_a`.

    4. Accedi a {{site.data.keyword.registrylong_notm}} immettendo il seguente comando:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Esegui il pull dell'immagine immettendo il seguente comando:

        ```
        docker pull <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. Esegui il push dell'immagine in `namespace_b` immettendo il seguente comando:

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        Questo comando ha esito negativo perché l'utente B non ha il ruolo di Scrittore in `namespace_b`.

    7. Contrassegna con tag l'immagine con `namespace_c` immettendo il seguente comando:

        ```
        docker tag hello-world <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. Esegui il push dell'immagine in `namespace_c` immettendo il seguente comando:

        ```
        docker push <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        Il comando funziona perché l'utente B ha il ruolo di Scrittore in `namespace_c`.

    9. Esegui il pull da `namespace_c` immettendo il seguente comando:

        ```
        docker pull <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        Il comando funziona perché l'utente B ha il ruolo di Lettore in `namespace_c`.

6. Ripulisci:

    1. Accedi nuovamente all'account dell'utente A immettendo il seguente comando:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Elenca le politiche per l'utente B immettendo il seguente comando:

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        Trova le politiche che hai appena creato e prendi nota degli ID politica.

    3. Elimina le politiche che hai appena creato immettendo il seguente comando, dove _`<Policy_ID>`_ è l'ID politica:

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Passo 3: crea un ID servizio e concedi l'accesso a una risorsa
{: #service_id}

In questa sezione, configura un ID servizio e concedi l'accesso al tuo spazio dei nomi {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Configura un ID servizio con l'accesso a {{site.data.keyword.registrylong_notm}} e crea una chiave API per esso:

    1. Accedi all'account dell'utente A immettendo il seguente comando:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Crea un ID servizio denominato `cr-roles-tutorial` con la descrizione `"Created during the access control tutorial for Container Registry"` immettendo il seguente comando:

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. Crea una politica del servizio per l'ID servizio che concede il ruolo di Lettore per `namespace_a` immettendo il seguente comando:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. Crea una seconda politica del servizio che concede il ruolo di Scrittore per `namespace_b` immettendo il seguente comando:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. Crea una chiave API per l'ID servizio immettendo il seguente comando:

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Utilizza Docker per accedere con la chiave API dell'ID servizio, dove _`<API_Key>`_ è la tua chiave API e interagisci con il registro:

    1. Accedi a {{site.data.keyword.registrylong_notm}} immettendo il seguente comando:

        ```
        docker login -u iamapikey -p <API_Key> <Region>.icr.io
        ```
        {: pre}

    2. Esegui il pull della tua immagine immettendo il seguente comando:

        ```
        docker pull <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Esegui il push della tua immagine in `namespace_a` immettendo il seguente comando:

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        Questo comando non funziona perché l'utente non ha il ruolo di Scrittore in `namespace_a`.

    4. Esegui il push della tua immagine in `namespace_b` immettendo il seguente comando:

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        Questo comando funziona perché l'utente ha il ruolo di Scrittore in `namespace_b`.

3. Ripulisci:

    1. Elenca le tue politiche del servizio immettendo il seguente comando:

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        Prendi nota dei tuoi ID politica.

    2. Elimina le tue politiche del servizio immettendo il seguente comando per ogni politica:

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. Elimina il tuo ID servizio immettendo il seguente comando:

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. Accedi nuovamente a {{site.data.keyword.registrylong_notm}} come utente A:

        ```
        ibmcloud cr login
        ```
        {: pre}

## Passo 4: ripulitura
{: #clean_up}

In questa sezione, elimini le risorse che hai creato nelle sezioni precedenti per lasciare il tuo account così come era all'inizio di questa esercitazione.
{:shortdesc}

1. Accedi al tuo account immettendo il seguente comando:

    ```
    ibmcloud login
    ```
    {: pre}

2. Elimina `namespace_a`, `namespace_b` e `namespace_c` immettendo i seguenti comandi:

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. Rimuovi l'utente B dal tuo account immettendo il seguente comando:

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

Complimenti. L'esercitazione è stata completata correttamente.
