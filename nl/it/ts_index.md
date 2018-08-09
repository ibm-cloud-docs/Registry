---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# Risoluzione dei problemi
{: #ts_index}

Qui troverai le risposte alle domande per la risoluzione dei problemi comuni relativi all'utilizzo di {{site.data.keyword.registrylong}}.
{:shortdesc}


## Come ottenere aiuto e supporto per {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Se hai delle domande o dei problemi quando utilizzi {{site.data.keyword.registrylong_notm}}, puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Puoi anche aprire un ticket di supporto {{site.data.keyword.IBM_notm}}.

Se utilizzi i forum per fare una domanda, contrassegna la tua domanda con una tag in modo che sia visualizzabile dal team di sviluppo {{site.data.keyword.registrylong_notm}}.

-   Se hai domande tecniche sullo sviluppo o sulla distribuzione di un'applicazione con {{site.data.keyword.registrylong_notm}}, inserisci la tua domanda in [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) e contrassegnala con le tag `ibm-bluemix` e `container-registry`.
-   Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Includi le tag `bluemix` e `container-registry`.

Vedi [Utilizzo del Centro di supporto](../../get-support/howtogetsupport.html#using-avatar) per ulteriori dettagli sull'utilizzo dei forum.

Per informazioni su come aprire un ticket di supporto {{site.data.keyword.IBM_notm}} o sui livelli di supporto e sulla gravità dei ticket, vedi [Apertura di un ticket di supporto](../../get-support/howtogetsupport.html#open-ticket).

## Accesso a {{site.data.keyword.registrylong_notm}} non riuscito
{: #ts_login}

Non puoi accedere a {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
Il comando `ibmcloud cr login` ha avuto esisto negativo.

{: tsCauses}
-   Il plug-in container-registry non è aggiornato e deve esserlo.
-   Docker non è installato sulla tua macchina locale o non è in esecuzione.
-   Le tue credenziali di accesso {{site.data.keyword.Bluemix_notm}} sono scadute.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

-   Esegui l'upgrade alla versione più recente del plug-in container-registry; vedi [Aggiornamento del plug-in container-registry](registry_setup_cli_namespace.html#registry_cli_update).
-   Assicurati che Docker sia installato sulla tua macchina. Se è già installato, riavvia il daemon Docker.
-   Riesegui il comando `ibmcloud login` per aggiornare le tue credenziali di accesso {{site.data.keyword.Bluemix_notm}}.
  
## L'esecuzione di qualsiasi comando per {{site.data.keyword.registrylong_notm}} non riesce e restituisce l'errore `FAILED You are not logged in to IBM Cloud. ` 
{: #ts_login_cloud}

Non riesci ad eseguire alcun comando in {{site.data.keyword.registrylong_notm}}, anche se hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}.

{: tsSymptoms}
Tutti i comandi `ibmcloud cr` hanno esito negativo.

{: tsCauses}
-   Il plug-in container-registry non è aggiornato e deve esserlo.

{: tsResolve}
Puoi correggere questo problema nel seguente modo:

-   Esegui l'upgrade alla versione più recente del plug-in container-registry; vedi [Aggiornamento del plug-in container-registry](registry_setup_cli_namespace.html#registry_cli_update).



## I comandi {{site.data.keyword.registrylong_notm}} hanno esito negativo con `'cr' non è un comando registrato. Vedi 'ibmcloud help'. `
{: #ts_login_error}

Non puoi eseguire un comando `ibmcloud cr` perché `cr` non è un comando `ibmcloud` registrato.

{: tsSymptoms}
Vedi un messaggio di errore simile a uno dei seguenti:

```
ibmcloud cr login
'cr' non è un comando registrato. Vedi 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' non è un comando registrato. Vedi 'ibmcloud help'.
```
{: pre}

{: tsCauses}
-   Il plug-in container-registry non è installato.


{: tsResolve}
Puoi correggere questo problema nel seguente modo:

-   Installa il plug-in container-registry; vedi [Installazione della CLI {{site.data.keyword.registryshort_notm}} (plug-in container-registry)](registry_setup_cli_namespace.html#registry_cli_install).


## Configurazione di uno spazio dei nomi non riuscita
{: #ts_problem}

{: tsSymptoms}
Quando esegui `ibmcloud cr namespace-add`, non riesci a impostare il tuo valore immesso come spazio dei nomi.

{: tsCauses}
-   Hai immesso un valore per lo spazio dei nomi che è già utilizzato da un'altra organizzazione {{site.data.keyword.Bluemix_notm}}.
-   Recentemente è stato eliminato uno spazio dei nomi e stai riutilizzando il suo nome. Se lo spazio dei nomi che è stato eliminato
conteneva molte risorse, è possibile che {{site.data.keyword.registrylong_notm}} non abbia ancora elaborato completamente l'eliminazione.
-   Hai utilizzato caratteri non validi per il valore dello spazio dei nomi.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

-   Segui le istruzioni visualizzate nel messaggio di errore restituito.
-   Controlla di aver immesso uno spazio dei nomi valido:
    -   Il tuo spazio dei nomi deve avere una lunghezza compresa tra 4 e 30 caratteri.
    -   Il tuo spazio dei nomi deve iniziare con almeno una lettera o un numero.
    -   Il tuo spazio dei nomi deve contenere solo lettere minuscole, numeri o caratteri di sottolineatura (_).
-   Scegli un valore diverso per il tuo spazio dei nomi.
-   Se stai ricreando uno spazio dei nomi che era stato eliminato e che conteneva molte immagini, riprova più tardi.

## L'esecuzione del push o del pull di un'immagine Docker non riesce
{: #ts_pushpull}

{: tsSymptoms}
Quando esegui i comandi per il push o il pull delle immagini Docker, ricevi un messaggio di errore. Il
messaggio di errore varia a seconda della causa principale. I messaggi di errore potenziali potrebbero essere:

```
Hai superato la tua quota di archiviazione. Elimina una o più immagini o riesamina la tua quota di archiviazione e il piano prezzi
```
{: screen}

```
Hai superato la tua quota di traffico di pull per il mese corrente. Riesamina la tua quota di traffico di pull e il piano prezzi
```
{: screen}

```
non autorizzato: autenticazione richiesta
```
{: screen}

```
negato: l'accesso richiesto alla risorsa è stato negato
```
{: screen}

{: tsCauses}
-   Docker non è installato.
-   Il client Docker non è collegato a {{site.data.keyword.registrylong_notm}}.
-   Il tuo token di accesso {{site.data.keyword.Bluemix_notm}} potrebbe essere scaduto.
-   Hai superato il limite di quota per l'archiviazione o il traffico di pull impostato per il tuo account {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

-   [Assicurati che Docker sia installato sulla tua macchina](index.html#registry_cli_install).
-   Controlla il tuo percorso di installazione Docker.
-   Effettua l'accesso a {{site.data.keyword.Bluemix_notm}} eseguendo `ibmcloud login`. Effettua quindi l'accesso alla CLI di {{site.data.keyword.registrylong_notm}} eseguendo `ibmcloud cr login`.
-   [Riesamina i limiti e l'utilizzo della quota per l'archiviazione e il pull delle immagini Docker in {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).

## Impossibile eseguire il pull dell'ultima immagine utilizzando la tag latest
{: #ts_docker_latest}

{: tsSymptoms}
Stai tentando di eseguire il comando `docker pull`, ma viene restituita una
versione della tua immagine che non è l'ultima versione creata.

{: tsCauses}
Per impostazione predefinita, la tag `latest` viene applicata per fare riferimento a un'immagine quando esegui i comandi Docker
senza specificare il valore della tag. La tag `latest` viene applicata all'ultimo comando
`docker build` o `docker tag` che è stato eseguito senza un valore di
tag esplicitamente impostato. Pertanto, è possibile eseguire i comandi `docker` in ordine non valido
oppure impostare esplicitamente le tag su alcune immagini e la tag `latest` per fare riferimento a una creazione
che non è la più recente.

{: tsResolve}
In genere, è meglio definire ogni volta una tag sequenziale diversa per le tue immagini in modo esplicito
anziché affidarsi alla tag `latest`.


## Impossibile aggiungere altre immagini IBM al registro
{: #ts_ppa}


{: tsSymptoms}
Quando tenti di importare il contenuto utilizzato in altri prodotti IBM, ad esempio {{site.data.keyword.Bluemix_notm}} Private, non riesci a memorizzare le tue immagini e altri software concessi in licenza da [IBM Passport Advantage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www-01.ibm.com/software/passportadvantage/index.html) nel registro.

{: tsCauses}
I pacchetti software come immagini e grafici Helm forniti da IBM Passport Advantage devono essere importati nel registro con il comando `ibmcloud cr ppa-archive-load`.

{: tsResolve}
Prima di iniziare:
* Effettua l'accesso a {{site.data.keyword.Bluemix_notm}} eseguendo `ibmcloud login [--sso]`.
* Effettua l'accesso a {{site.data.keyword.registrylong_notm}} eseguendo `ibmcloud cr login`.
* [Indirizza la CLI `kubectl`](../../containers/cs_cli_install.html#cs_cli_configure) al tuo cluster.
* Se non hai ancora configurato Helm nel tuo cluster, [configura Helm nel cluster ora](../../containers/cs_integrations.html#helm).
* Se vuoi condividere i grafici all'interno della tua organizzazione, puoi installare il [progetto open source Chart Museum ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum). Per le istruzioni, vedi questa [strategia (recipe) di developerWorks ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/).

### Importazione dei prodotti IBM Passport Advantage per l'utilizzo in {{site.data.keyword.Bluemix_notm}}

1.  Ottieni il file compresso che vuoi importare da [IBM Passport Advantage![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www-01.ibm.com/software/passportadvantage/index.html).

2.  Specifica la regione che vuoi utilizzare come destinazione. Se non conosci il nome della regione, esegui il comando senza la regione e scegline una.

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

3.  Importa il file di archivio compresso. Specifica il percorso del file compresso e lo spazio dei nomi del registro in cui vuoi eseguire il push delle immagini.

    ```
    ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
    ```
    {: pre}

    Questo comando espande il file compresso, carica qualsiasi immagine contenuta nel tuo client Docker locale, quindi esegue il push delle immagini allo spazio dei nomi nel tuo registro.
    
    Se vuoi caricare i grafici Helm dall'archivio di IBM Passport Advantage in un chart museum, includi le seguenti opzioni nel comando: `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **Output di esempio**:
    ```
    user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

    OK
    ```
    {: screen}

4.  Se i file compressi contengono i grafici Helm, questi grafici vengono collocati in una directory di archivio chiamata `ppa-import` che viene creata nella tua directory di lavoro corrente. Apri la directory per ottenere il nome del grafico Helm, `<helm_chart>`, quindi controlla i suoi valori.

    ```
    helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    Se hai caricato i grafici in un chart museum nel passo precedente, puoi utilizzare `helm inspect` per controllare il grafico in chart museum.
    {: tip}

5.  Configura il grafico Helm,`<helm_chart>`, in base ai valori emessi dal comando `helm inspect values`.

6.  Distribuisci il grafico Helm, `<helm_chart>`, utilizzando il comando `helm install`. Puoi sovrascrivere i valori nel grafico come richiesto utilizzando l'opzione `--set`.

    ```
    helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## Accesso al registro con un firewall personalizzato non riuscito
{: #ts_firewall}

{: tsSymptoms}
Hai configurato un firewall aggiuntivo nel tuo ambiente di distribuzione con impostazioni personalizzate
per il traffico di rete in entrata e in uscita. Quando provi ad accedere a {{site.data.keyword.registrylong_notm}}, il collegamento ha esito negativo.

{: tsCauses}
Il tuo firewall personalizzato richiede che alcuni gruppi di rete siano aperti per il traffico di rete in entrata e in uscita
per consentire la comunicazione in entrata e uscita dal registro.

{: tsResolve}
Apri i seguenti gruppi di rete nel tuo firewall personalizzato.

1.  Prendi nota dell'indirizzo IP pubblico della macchina che desideri utilizzare per il collegamento a {{site.data.keyword.registrylong_notm}}. Se stai utilizzando Kubernetes,
utilizza l'indirizzo IP pubblico del tuo nodo di lavoro. Richiama l'indirizzo IP pubblico del tuo nodo di lavoro eseguendo `ibmcloud ks workers <cluster_name_or_id>`, dove *&lt;nome_o_id_cluster&gt;* è il nome o l'ID del tuo cluster.
2.  Nel tuo firewall, consenti i seguenti collegamenti in entrata e uscita dalla tua macchina:
    -   Per la connettività IN ENTRATA alla tua macchina, consenti il traffico di rete in entrata dai seguenti gruppi di rete di origine
all'indirizzo IP pubblico di destinazione della tua macchina.

        `registry.bluemix.net`:

        ```
        169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   Per la connettività IN USCITA dalla tua macchina, utilizza gli stessi gruppi di rete e consenti il traffico di rete in uscita
dall'indirizzo IP pubblico di origine della tua macchina a tali gruppi di rete.

## Ripristino di chiavi perse o compromesse
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
Quando utilizzi i [contenuti attendibili](registry_trusted_content.html), non puoi più gestire le immagini attendibili perché le tue chiavi di firma sono perse o compromesse.

{: tsCauses}
La tua chiave di repository o root è persa o compromessa.

{: tsResolve}
Le opzioni per il ripristino delle chiavi perse o interessate dipendono dal tipo di chiave: repository o root:

*  Per le [chiavi di repository](#trustedcontent_lostrepokey), puoi generare una nuova serie di chiavi di firma per il repository.
*  Per le [chiavi root](#trustedcontent_lostrootkey), puoi richiedere che il repository venga eliminato e creare un nuovo repository.

### Chiavi di repository
{: #trustedcontent_lostrepokey}

Se la tua chiave di repository viene persa o compromessa, genera una nuova serie di chiavi di firma per il tuo repository.
{:shortdesc}

L'unico ruolo di firma che puoi ruotare è `targets`, che è l'amministratore del repository. Se sono interessati altri ruoli, genera nuove chiavi per tali ruoli, rimuovi quelli vecchi e aggiungine di nuovi come firmatari.
{:tip}

Prima di iniziare, richiama la passphrase della chiave root che hai creato quando hai [eseguito il push di un'immagine firmata](registry_trusted_content.html#trustedcontent_push).

1.  Installa la versione della CLI del [progetto Notary](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli).

2.  [Configura il tuo ambiente di contenuti attendibili](registry_trusted_content.html#trustedcontent_setup).

3.  Annota l'URL dal comando di esportazione nel passo precedente. Ed esempio, `https://registry.ng.bluemix.net:4443`.

4.  Genera un token di registro.

    ```
    ibmcloud cr token-add --readwrite
    ```
    {: pre}

5.	Ruota le tue chiavi in modo che il contenuto firmato con quelle chiavi non sia più attendibile. Sostituisci _&lt;URL&gt;_ con l'URL del comando di esportazione che hai annotato nel passo 2 e _&lt;image&gt;_ con l'immagine la cui chiave di repository è interessata.

    ```
    notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	Se richiesto, immetti la passphrase della chiave root. Quindi, immetti una nuova passphrase della chiave root per la nuova chiave di repository quando viene richiesto.

7.	[Esegui il push di un'immagine firmata](registry_trusted_content.html#trustedcontent_push) che utilizza le nuovi chiavi di firma.

### Chiavi root
{: #trustedcontent_lostrootkey}

Se la tua chiave root viene persa o compromessa, non puoi aggiornare alcun repository di contenuti attendibili che utilizzava tale chiave root.
{:shortdesc}

Puoi [eliminare gli spazi dei nomi](registry_setup_cli_namespace.html#registry_remove) con i repository che utilizzano la chiave root interessata, il che elimina le tue immagini e dati di attendibilità.

Se lo spazio dei nomi contiene repository con chiavi root non interessate, ad esempio uno spazio dei nomi per le immagini di produzione, potresti voler eliminare solo i dati di attendibilità associati alla chiave root interessata. Apri un ticket di supporto.

1.  [Contatta il supporto {{site.data.keyword.Bluemix_notm}}](../../get-support/howtogetsupport.html). Includi una breve descrizione del problema, l'ID account e un elenco degli spazi dei nomi che contengono i repository di immagini con le chiavi root interessate.

2.  Dopo che {{site.data.keyword.Bluemix_notm}} ha risolto il problema, elimina il repository Docker Content Trust dalla tua macchina locale.

    * Directory Linux e Mac: `~/.docker/trust/private` e `~/.docker/trust/tuf`

    * Directory Windows: `%HOMEPATH%\.docker\trust\private` e `%HOMEPATH%\.docker\trust\tuf`

    poiché la chiave root è interessata, questo passo elimina tutte le chiavi di firma, anche per altri server di attendibilità.
    {:tip}

3.  Se utilizzi [{{site.data.keyword.Bluemix_notm}} Image Enforcement](registry_security_enforce.html) nel tuo cluster {{site.data.keyword.containershort_notm}}, riavvia ogni pod di applicazione delle immagini. Per far sì che Kubernetes esegua automaticamente un riavvio progressivo dei pod, puoi modificare alcuni metadati sul pod. Ad esempio, [indirizza la CLI Kubernetes al tuo cluster](../../containers/cs_cli_install.html#cs_cli_configure) e modifica la distribuzione.
    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  Genera repository di contenuti attendibili.

    *  Se vuoi creare nuovi contenuti attendibili, [esegui il push di nuove immagini firmate](registry_trusted_content.html#trustedcontent_push).

    *  Se non vuoi modificare i contenuti attendibili precedenti, aggiungi una firma alle immagini più recenti nel registro.

       ```
       docker trust sign <image>:<tag>
       ```
       {: pre}
       

## L'installazione di Container Image Security Enforcement non riesce e restituisce l'errore `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists`
{: #ts_install_cise_fail}


{: tsSymptoms}
La tua installazione di Container Image Security Enforcement non è riuscita e hai ricevuto il seguente messaggio:

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
L'installazione precedente non è riuscita e la successiva disinstallazione non ha rimosso tutti i lavori di Kubernetes associati all'installazione.

{: tsResolve}
Rimuovi i restanti lavori di Kubernetes immettendo il seguente comando:

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}
