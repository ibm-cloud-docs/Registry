---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-04"

keywords: IBM Cloud Container Registry, troubleshooting, support, help, errors, error messages, failure, fails, lost keys, firewall, Docker manifest errors,

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

- Se hai domande tecniche sullo sviluppo o sulla distribuzione di un'applicazione con {{site.data.keyword.registrylong_notm}}, inserisci la tua domanda in [Stack Overflow ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://stackoverflow.com/search?q=+ibm-cloud+container-registry) e contrassegnala con le tag `ibm-cloud` e `container-registry`.
- Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum [IBM Developer Answers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/answers/topics/container-registry.html). Includi le tag `ibm-cloud` e `container-registry`.

Vedi [Utilizzo del Centro di supporto](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) per ulteriori dettagli sull'utilizzo dei forum.

Per informazioni su come aprire un ticket di supporto {{site.data.keyword.IBM_notm}} o sui livelli di supporto e sulla gravità dei ticket, vedi [Come posso ottenere il supporto di cui ho bisogno?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support)

## Accesso a {{site.data.keyword.registrylong_notm}} non riuscito
{: #ts_login}

Non puoi accedere a {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
Il comando `ibmcloud cr login` ha avuto esisto negativo.

{: tsCauses}

- Il plug-in CLI `container-registry` non è aggiornato e deve esserlo.
- Docker non è installato sul tuo computer locale o non è in esecuzione.
- Le tue credenziali di accesso {{site.data.keyword.cloud_notm}} sono scadute.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

- Esegui l'upgrade alla versione più recente del plug-in CLI `container-registry`, vedi [Aggiornamento del plug-in CLI `container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).
- Assicurati che Docker sia installato sul tuo computer. Se è già installato, riavvia il daemon Docker.
- Riesegui il comando `ibmcloud login` per aggiornare le tue credenziali di accesso {{site.data.keyword.cloud_notm}}.

## L'esecuzione di qualsiasi comando per {{site.data.keyword.registrylong_notm}} non riesce e restituisce l'errore `FAILED You are not logged in to IBM Cloud. `
{: #ts_login_cloud}

Non riesci ad eseguire alcun comando in {{site.data.keyword.registrylong_notm}}, anche se hai eseguito l'accesso a {{site.data.keyword.cloud_notm}}.

{: tsSymptoms}
Tutti i comandi `ibmcloud cr` hanno esito negativo.

{: tsCauses}

- Il plug-in CLI `container-registry` non è aggiornato e deve esserlo.

{: tsResolve}
Puoi correggere questo problema nel seguente modo:

- Esegui l'upgrade alla versione più recente del plug-in CLI `container-registry`, vedi [Aggiornamento del plug-in CLI `container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).

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

- Il plug-in CLI `container-registry` non è installato.

{: tsResolve}
Puoi correggere questo problema nel seguente modo:

- Installa il plugin CLI `container-registry`, consulta [Installazione del plugin CLI `container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Il comando `ibmcloud cr build` ha avuto esisto negativo
{: #ts_build_fails}

{: tsSymptoms}
Il comando build ha avuto esito negativo.

{: tsCauses}
Il server potrebbe non essere attivo oppure potrebbero esserci dei problemi con il tuo Dockerfile.

{: tsResolve}
Per trovare cosa causa il problema, esegui `docker build` localmente con le opzioni [`docker build` appropriate ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/engine/reference/commandline/build/):

```
docker build --no-cache .
```
{:  pre}

- Se il comando build in locale non funziona, controlla se sono presenti dei problemi con il tuo Dockerfile.
- Se il comando build in locale funziona, [contatta il supporto {{site.data.keyword.cloud_notm}}](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).

## Configurazione di uno spazio dei nomi non riuscita
{: #ts_problem}

{: tsSymptoms}
Quando esegui `ibmcloud cr namespace-add`, non riesci a impostare il tuo valore immesso come spazio dei nomi.

{: tsCauses}

- Hai immesso un valore per lo spazio dei nomi che è già utilizzato da un'altra organizzazione {{site.data.keyword.cloud_notm}}.
- Recentemente è stato eliminato uno spazio dei nomi e stai riutilizzando il suo nome. Se lo spazio dei nomi che è stato eliminato
conteneva molte risorse, è possibile che {{site.data.keyword.registrylong_notm}} non abbia ancora elaborato completamente l'eliminazione.
- Hai utilizzato caratteri non validi per il valore dello spazio dei nomi.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

- Segui le istruzioni visualizzate nel messaggio di errore restituito.
- Controlla di aver immesso uno spazio dei nomi valido:
  - Il tuo spazio dei nomi deve essere univoco tra tutti gli account {{site.data.keyword.cloud_notm}} nella stessa regione.
  - Il tuo spazio dei nomi deve avere una lunghezza compresa tra 4 e 30 caratteri.
  - Il tuo spazio dei nomi deve iniziare e terminare con una lettera o un numero.
  - Il tuo spazio dei nomi deve contenere solo lettere minuscole, numeri, trattini (-) e caratteri di sottolineatura (_).
- Scegli un valore diverso per il tuo spazio dei nomi.
- Se stai ricreando uno spazio dei nomi che era stato eliminato e che conteneva molte immagini, riprova più tardi.

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
Hai superato la tua quota di traffico di pull per il mese corrente.
Riesamina la tua quota di traffico di pull e il piano prezzi
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

- Docker non è installato.
- Il client Docker non è collegato a {{site.data.keyword.registrylong_notm}}.
- Il tuo token di accesso {{site.data.keyword.cloud_notm}} potrebbe essere scaduto.
- Hai superato il limite di quota per l'archiviazione o il traffico di pull impostato per il tuo account {{site.data.keyword.cloud_notm}}.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

- [Assicurati che Docker sia installato sul tuo computer](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- Controlla il tuo percorso di installazione Docker.
- Accedi a {{site.data.keyword.cloud_notm}} eseguendo `ibmcloud login`. Effettua quindi l'accesso alla CLI di {{site.data.keyword.registrylong_notm}} eseguendo `ibmcloud cr login`.
- [Riesamina i limiti e l'utilizzo della quota per l'archiviazione e il pull delle immagini Docker in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_quota#registry_quota_get).

## Impossibile eseguire il pull dell'immagine più recente utilizzando la tag `latest`
{: #ts_docker_latest}

{: tsSymptoms}
Stai tentando di eseguire il comando `docker pull`, ma viene restituita una versione della tua immagine che non è la più recente creata.

{: tsCauses}
Per impostazione predefinita, la tag `latest` viene applicata per fare riferimento a un'immagine quando esegui i comandi Docker
senza specificare il valore della tag. La tag `latest` viene applicata al comando più recente
`docker build` o `docker tag` che è stato eseguito senza un valore di
tag esplicitamente impostato. Pertanto, è possibile eseguire i comandi `docker` in ordine non valido oppure impostare esplicitamente le tag su alcune immagini e la tag `latest` per fare riferimento a una creazione che non è la più recente.

{: tsResolve}
In genere, è meglio definire ogni volta una tag sequenziale diversa per le tue immagini in modo esplicito
anziché affidarsi alla tag `latest`.

## Impossibile aggiungere altre immagini IBM al registro
{: #ts_ppa}

{: tsSymptoms}
Quando tenti di importare il contenuto utilizzato in altri prodotti IBM, ad esempio {{site.data.keyword.cloud_notm}} Private, non riesci a memorizzare le tue immagini e altri software concessi in licenza da [IBM Passport Advantage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/passportadvantage/index.html) nel registro.

{: tsCauses}
I pacchetti software come immagini e grafici Helm forniti da IBM Passport Advantage devono essere importati nel registro con il comando `ibmcloud cr ppa-archive-load`.

{: tsResolve}
**Prima di iniziare**

- Effettua l'accesso a {{site.data.keyword.cloud_notm}} eseguendo `ibmcloud login [--sso]`.
- Effettua l'accesso a {{site.data.keyword.registrylong_notm}} eseguendo `ibmcloud cr login`.
- [Indirizza la CLI `kubectl`](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) al tuo cluster.
- Se non hai ancora configurato Helm nel tuo cluster, [configura Helm nel cluster ora](/docs/containers?topic=containers-helm#helm).
- Se vuoi condividere i grafici all'interno della tua organizzazione, puoi installare il [progetto open source Chart Museum ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/helm/charts/tree/master/stable/chartmuseum). Per le istruzioni, vedi questa [strategia (recipe) di developerWorks ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/).

### Importazione dei prodotti IBM Passport Advantage per l'utilizzo in {{site.data.keyword.cloud_notm}}
{: #ts_ppa_import}

1. Ottieni il file compresso che vuoi importare da [IBM Passport Advantage![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/passportadvantage/index.html).

2. Specifica la regione che vuoi utilizzare come destinazione. Se non conosci il nome della regione, esegui il comando senza la regione e scegline una.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

3. Importa il file di archivio compresso. Specifica il percorso del file compresso e lo spazio dei nomi del registro in cui vuoi eseguire il push delle immagini.

   ```
   ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
   ```
   {: pre}

   Questo comando espande il file compresso, carica qualsiasi immagine contenuta nel tuo client Docker locale, quindi esegue il push delle immagini allo spazio dei nomi nel tuo registro.

   Se vuoi caricare i grafici Helm dall'archivio di IBM Passport Advantage in un chart museum, includi le seguenti opzioni nel comando: `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
   {: tip}

   **Output di esempio**

   ```
   user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
   Found 1 image(s) and 1 chart(s) to import.
   Importing 'iib-prod:10.0.0.10' and pushing it to 'us.icr.io/mynamespace/iib-prod:10.0.0.10'...
   Loaded image: iib-prod:10.0.0.10
   The push refers to repository [us.icr.io/mynamespace/iib-prod]
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

4. Se i file compressi contengono i grafici Helm, questi grafici vengono collocati in una directory di archivio chiamata `ppa-import` che viene creata nella tua directory di lavoro corrente. Apri la directory per ottenere il nome del grafico Helm, `<helm_chart>`, quindi controlla i suoi valori.

   ```
   helm inspect values ppa-import/charts/<helm_chart>.tgz
   ```
   {: pre}

   Se hai caricato i grafici in un chart museum nel passo precedente, puoi utilizzare `helm inspect` per controllare il grafico in chart museum.
   {: tip}

5. Configura il grafico Helm,`<helm_chart>`, in base ai valori emessi dal comando `helm inspect values`.

6. Distribuisci il grafico Helm, `<helm_chart>`, utilizzando il comando `helm install`. Puoi sovrascrivere i valori nel grafico come richiesto utilizzando l'opzione `--set`.

   ```
   helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
   ```
   {: pre}

## Ho utilizzato il comando `ibmcloud cr image-rm` per eliminare un'immagine e anche tutte le tag che facevano riferimento a tale immagine sono state eliminate
{: #ts_image-rm}

{: tsSymptoms}
Hai eliminato un'immagine utilizzando il comando `ibmcloud cr image-rm` e sono state eliminate anche tutte le tag nello stesso repository che facevano riferimento all'immagine.

{: tsCauses}
Dove sono presenti più tag per lo stesso digest immagine all'interno di un repository, il [comando `ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) rimuove l'immagine sottostante e tutte le relative tag. Se la stessa immagine è presente in uno spazio dei nomi o repository diversi, tale copia dell'immagine non viene rimossa.

{: tsResolve}
Se vuoi rimuovere una tag da un'immagine ma lasciare in vigore l'immagine sottostante e tutte le altre tag, utilizza il [comando `ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag). Per ulteriori informazioni, vedi [Rimozione delle tag dalle immagini nel tuo repository {{site.data.keyword.cloud_notm}} privato](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag) e [Eliminazione di immagini dal tuo repository {{site.data.keyword.cloud_notm}} privato](/docs/services/Registry?topic=registry-registry_images_#registry_images_remove).

## Accesso al registro con un firewall personalizzato non riuscito
{: #ts_firewall}

{: tsSymptoms}
Hai configurato un firewall aggiuntivo nel tuo ambiente di distribuzione con impostazioni personalizzate
per il traffico di rete in entrata e in uscita. Quando provi ad accedere a {{site.data.keyword.registrylong_notm}}, il collegamento ha esito negativo.

{: tsCauses}
Il tuo firewall personalizzato richiede che alcuni gruppi di rete siano aperti per il traffico di rete in entrata e in uscita
per consentire la comunicazione in entrata e uscita dal registro.

{: tsResolve}

Consenti al tuo cluster di accedere ai servizi e alle risorse dell'infrastruttura da dietro un firewall, consulta [Consentire al cluster di accedere alle risorse dell'infrastruttura e ad altri servizi](/docs/containers?topic=containers-firewall#firewall_outbound).

Per la connettività IN ENTRATA al tuo computer, consenti il traffico di rete in entrata dai gruppi di rete di origine all'indirizzo IP pubblico di destinazione del tuo computer.

Per la connettività IN USCITA dal tuo computer, utilizza gli stessi gruppi di rete e consenti il traffico di rete in uscita dall'indirizzo IP pubblico di origine del tuo computer ai gruppi di rete.

## Ripristino di chiavi perse o compromesse
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
Quando utilizzi i [contenuti attendibili](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent), non puoi più gestire le immagini attendibili perché le tue chiavi di firma sono perse o compromesse.

{: tsCauses}
La tua chiave di repository o root è persa o compromessa.

{: tsResolve}
Le opzioni per il ripristino delle chiavi perse o interessate dipendono dal tipo di chiave: repository o root:

- Per le [chiavi di repository](#trustedcontent_lostrepokey), puoi generare una nuova serie di chiavi di firma per il repository.
- Per le [chiavi root](#trustedcontent_lostrootkey), puoi richiedere che il repository venga eliminato e creare un nuovo repository.

### Chiavi di repository
{: #trustedcontent_lostrepokey}

Se la tua chiave di repository viene persa o compromessa, genera una nuova serie di chiavi di firma per il tuo repository.
{:shortdesc}

L'unico ruolo di firma che puoi ruotare è `targets`, che è l'amministratore del repository. Se sono interessati altri ruoli, genera nuove chiavi per tali ruoli, rimuovi quelli vecchi e aggiungine di nuovi come firmatari.
{:tip}

Prima di iniziare, richiama la passphrase della chiave root che hai creato quando hai [eseguito il push di un'immagine firmata](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_push).

1. Installa la versione della CLI del [progetto Notary ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli).

2. [Configura il tuo ambiente di contenuti attendibili](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_setup).

3. Crea una chiave API IAM:

   ```
   ibmcloud iam api-key-create notary-auth --file notary-auth
   ```
   {: pre}

4. Imposta NOTARY_AUTH:

   ```
   export NOTARY_AUTH="iamapikey:$(jq -r .apikey notary-auth)"
   ```
   {: pre}

5. Ruota le tue chiavi in modo che il contenuto firmato con quelle chiavi non sia più attendibile. Utilizza la variabile del server di attendibilità che hai impostato nel passo 2 e sostituisci `<image>` con l'immagine la cui chiave di repository è interessata.

   ```
   notary -s "$DOCKER_CONTENT_TRUST_SERVER" -d ~/.docker/trust key rotate <image> targets
   ```
   {: pre}

6. Se richiesto, immetti la passphrase della chiave root. Quindi, immetti una nuova passphrase della chiave root per la nuova chiave di repository quando viene richiesto.

7. [Esegui il push di un'immagine firmata](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_push) che utilizza le nuovi chiavi di firma.

8.  (Facoltativo) Quando hai finito, se vuoi revocare la tua chiave API, immetti il seguente comando:

    ```
    ibmcloud iam api-key-delete notary-auth
    ```
    {:pre}

### Chiavi root
{: #trustedcontent_lostrootkey}

Se la tua chiave root viene persa o compromessa, non puoi aggiornare alcun repository di contenuti attendibili che utilizzava tale chiave root.
{:shortdesc}

Puoi [eliminare gli spazi dei nomi](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_remove) con i repository che utilizzano la chiave root interessata, il che elimina le tue immagini e dati di attendibilità.

Se lo spazio dei nomi contiene repository con chiavi root non interessate, ad esempio uno spazio dei nomi per le immagini di produzione, potresti voler eliminare solo i dati di attendibilità associati alla chiave root interessata. Apri un ticket di supporto.

1. [Contatta il supporto {{site.data.keyword.cloud_notm}}](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support). Includi una breve descrizione del problema, l'ID account e un elenco degli spazi dei nomi che contengono i repository di immagini con le chiavi root interessate.

2. Dopo che {{site.data.keyword.cloud_notm}} ha risolto il problema, elimina il repository Docker Content Trust dal tuo computer locale.

   - Directory Linux e Mac: `~/.docker/trust/private` e `~/.docker/trust/tuf`

   - Directory Windows: `%HOMEPATH%\.docker\trust\private` e `%HOMEPATH%\.docker\trust\tuf`

   poiché la chiave root è interessata, questo passo elimina tutte le chiavi di firma, anche per altri server di attendibilità.
   {:tip}

3. Se utilizzi [{{site.data.keyword.cloud_notm}} Image Enforcement](/docs/services/Registry?topic=registry-security_enforce#security_enforce) nel tuo cluster {{site.data.keyword.containershort_notm}}, riavvia ogni pod di applicazione delle immagini. Per far sì che Kubernetes esegua automaticamente un riavvio progressivo dei pod, puoi modificare alcuni metadati sul pod. Ad esempio, [indirizza la CLI Kubernetes al tuo cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) e modifica la distribuzione.

   ```
   kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
   ```
   {: pre}

4. Genera repository di contenuti attendibili.

    - Se vuoi creare nuovi contenuti attendibili, [esegui il push di nuove immagini firmate](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_push).

    - Se non vuoi modificare i contenuti attendibili precedenti, aggiungi una firma alle immagini più recenti nel registro.

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
Rimuovi i restanti lavori di Kubernetes eseguendo il seguente comando:

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}

## I pod non vengono riavviati dopo che sono stati disattivati tutti i tuoi nodi di lavoro
{: #ts_pods}

{: tsSymptoms}
I pod non vengono riavviati dopo che sono stati disattivati tutti i tuoi nodi di lavoro del cluster. Viene distribuito Container Image Security Enforcement. I nodi di lavoro del cluster vengono visualizzati come integri, ma non viene pianificato nulla.

{: tsCauses}
Per impostazione predefinita, Container Image Security Enforcement aggiunge un webhook di ammissione chiuso con errore. Se tutti i pod di Container Image Security Enforcement sono inattivi, non sono disponibili per approvare il proprio ripristino.

{: tsResolve}
Per ripristinare il cluster quando è in questo stato, devi modificare la configurazione del webhook per renderlo non riuscito invece di chiuso.

Devi disporre dei privilegi RBAC (Role-based Access Control) per utilizzare i seguenti verbi:

- `GET`
- `PATCH`

su queste risorse:

- `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
- `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration`

Per ulteriori informazioni su RBAC, vedi [Autorizzazione di utenti con ruoli personalizzati di RBAC Kubernetes](/docs/containers?topic=containers-users#rbac) e [Kubernetes - Using RBAC Authorization ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

Completa la seguente procedura per modificare la configurazione webhook in modo che sia in errore di apertura invece che chiusa e poi, quando almeno un pod di Container Image Security Enforcement è in esecuzione, ripristina la configurazione webhook in modo che sia in errore di chiusura:

1. Aggiorna `MutatingWebhookConfiguration` immettendo il seguente comando:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Modifica `failurePolicy` con `Ignore`, salva e chiudi.

2. Aggiorna `ValidatingWebhookConfiguration` immettendo il seguente comando:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Modifica `failurePolicy` con `Ignore`, salva e chiudi.

3. Attendi che vengano avviati alcuni pod di Container Image Security Enforcement. Puoi controllare se i pod sono stati avviati immettendo il seguente comando finché non vedi che la colonna **STATUS** di almeno un pod visualizza `Running`:

   ```
   kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
   ```
   {: pre}

4. Quando almeno un pod di Container Image Security Enforcement è in esecuzione, aggiorna `MutatingWebhookConfiguration` immettendo il seguente comando:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Modifica `failurePolicy` con `Fail`, salva e chiudi.

5. Aggiorna `ValidatingWebhookConfiguration` immettendo il seguente comando:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Modifica `failurePolicy` con `Fail`, salva e chiudi.

## Errore manifest: `The manifest type for this image is not supported for tagging.`
{: #ts_manifest_error_type}

{: tsSymptoms}
Hai tentato di contrassegnare con tag la tua immagine, ma hai ricevuto il seguente messaggio di errore, `The manifest type for this image is not supported for tagging.`.

{: tsCauses}
Il tipo di manifest non è supportato.

{: tsResolve}
Per risolvere il problema, completa la seguente procedura:

1. Esegui il pull dell'immagine che hai tentato di contrassegnare con tag immettendo il seguente comando, dove `<source_image>` è il tuo nome immagine di origine:

   ```
   docker pull <source_image>
   ```
   {: pre}

2. Contrassegna con tag la tua copia locale dell'immagine di cui hai eseguito il pull nel precedente passo immettendo il seguente comando, dove `<target_image>` è il tuo nuovo nome immagine:

   ```
   docker tag <source_image> <target_image>
   ```
   {: pre}

3. Esegui il push dell'immagine che hai contrassegnato con tag nel passo precedente immettendo il seguente comando:

   ```
   docker push <target_image>
   ```
   {: pre}

## Errore manifest: `The manifest version for this image is not supported for tagging.`
{: #ts_manifest_error_version}

{: tsSymptoms}
Hai tentato di contrassegnare con tag la tua immagine, ma hai ricevuto il seguente messaggio di errore: `The manifest version for this image is not supported for tagging. To upgrade to a supported manifest version, pull and push this image by using Docker version 1.12 or later, then run the 'ibmcloud cr image-tag' command again.`

{: tsCauses}
La versione del manifest non è supportata.

{: tsResolve}
Per risolvere il problema, completa la seguente procedura:

1. Esegui l'upgrade a Docker Engine versione 1.12 o successive.

2. Esegui il pull dell'immagine che hai tentato di contrassegnare con tag immettendo il seguente comando, dove `<source_image>` è il tuo nome immagine di origine:

   ```
   docker pull <source_image>
   ```
   {: pre}

3. Per eseguire l'upgrade della versione del manifest, esegui il push dell'immagine immettendo il seguente comando:

   ```
   docker push <source_image>
   ```
   {: pre}

4. Contrassegna con tag l'immagine eseguendo il comando `ibmcloud cr image-tag`, consulta [Creazione di nuove immagini che fanno riferimento a un'immagine di origine](/docs/services/Registry?topic=registry-registry_images_#registry_images_source).

## L'accesso Docker non riesce su un Mac: `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`
{: #ts_docker_mac}

{: tsSymptoms}
Ricevi il seguente messaggio di errore quando provi ad eseguire il comando `ibmcloud cr login` su un Mac: `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`

{: tsCauses}
Questo è un problema con Docker per Mac che impedisce l'archiviazione delle tue credenziali nella keychain macOS:

{: tsResolve}
Potresti essere in grado di risolvere il problema riavviando il tuo Mac. Se il riavvio del tuo Mac non funziona, puoi disabilitare l'archiviazione degli accessi nella tua keychain Mac:

1. Nel tuo menu, fai clic sull'icona **Docker** e seleziona **Preferences**.
2. Deseleziona la casella di spunta **Securely store Docker logins in macOS keychain**.
