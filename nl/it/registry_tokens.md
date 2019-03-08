---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-27"

keywords: IBM Cloud Container Registry, API keys, tokens

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

# Automazione dell'accesso a {{site.data.keyword.registrylong_notm}}
{: #registry_access}

Puoi utilizzare i token del registro o una chiave API {{site.data.keyword.iamlong}} (IAM) per accedere ai tuoi spazi dei nomi  {{site.data.keyword.registrylong_notm}} in modo da poter ricevere o trasmettere le immagini.
{:shortdesc}

Stai cercando di utilizzare le tue immagini del registro nelle distribuzioni Kubernetes? Consulta [Accesso alle immagini in altri spazi dei nomi Kubernetes, regioni {{site.data.keyword.Bluemix_notm}} e account](/docs/containers?topic=containers-images#other).
{: tip}

Le chiavi API sono collegate al tuo account e possono essere utilizzate in {{site.data.keyword.Bluemix_notm}} in modo che non hai bisogno di credenziali differenti per ogni servizio. Puoi utilizzare la chiave API nella CLI o come parte dell'automazione dell'accesso come tua identità utente.

I token del registro sono applicabili solo a {{site.data.keyword.registrylong_notm}}. Puoi limitarli all'accesso in sola lettura e puoi scegliere se scadono o meno.

Se utilizzi una chiave API, puoi controllare l'accesso ai tuoi spazi dei nomi utilizzando le politiche IAM. Per ulteriori informazioni, consulta [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry?topic=registry-user#user).

Per ulteriori informazioni sulle chiavi API {{site.data.keyword.registrylong_notm}}, consulta [Gestione delle chiavi API](/docs/iam?topic=iam-manapikey#manapikey).

Prima di iniziare, [installa la CLI {{site.data.keyword.registrylong_notm}} e Docker](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API
{: #registry_api_key}

Puoi utilizzare le chiavi API per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi.
{:shortdesc}

### Creazione di una chiave API
{: #registry_api_key_create}

Puoi creare una chiave API che puoi successivamente utilizzare per accedere al tuo registro.
{:shortdesc}

Puoi creare sia le chiavi API dell'utente che le chiavi API dell'ID servizio.

- Per creare una chiave API a, consulta [Creazione di una chiave API per un ID servizio](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
- Per creare una chiave API a, consulta [Creazione di una chiave API](/docs/iam?topic=iam-userapikey#create_user_key).

### Utilizzo di una chiave API per automatizzare l'accesso
{: #registry_api_key_use}

Puoi utilizzare una chiave API per automatizzare l'accesso ai tuoi spazi dei nomi in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Utilizza la chiave API per accedere al tuo registro eseguendo il seguente comando Docker. Sostituisci `<your_apikey>` con la tua chiave API e sostituisci `<registry_url>` con l'URL del registro in cui sono configurati i tuoi spazi dei nomi.

- Per gli spazi dei nomi configurati in Asia Pacifico Nord, utilizza `jp.icr.io`
- Per gli spazi dei nomi configurati in Asia Pacifico Sud, utilizza `au.icr.io`
- Per gli spazi dei nomi configurati in Europa centrale, utilizza `de.icr.io`
- Per gli spazi dei nomi configurati in Regno Unito Sud, utilizza `uk.icr.io`
- Per gli spazi dei nomi configurati in Stati Uniti Sud, utilizza `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Per le informazioni di riferimento sul comando, consulta [Crea una nuova chiave API della piattaforma {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Automazione dell'accesso agli spazi dei nomi utilizzando i token (obsoleta)
{: #registry_tokens}

Puoi utilizzare i token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

L'utilizzo dei token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi è obsoleto. Utilizza invece le chiavi API per automatizzare l'accesso ai tuoi spazi dei nomi, consulta [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](#registry_api_key).
{: deprecated}

Chiunque in possesso di un token del registro può accedere alle informazioni protette. Se vuoi che degli utenti all'esterno del tuo account possano accedere a tutti i tuoi spazi dei nomi che hai configurato in una regione, puoi creare un token per il tuo account {{site.data.keyword.Bluemix_notm}}. Ogni utente o applicazione in possesso di questo token, può eseguire il push e il pull di immagini da e verso i tuoi spazi dei nomi senza dover installare il plug-in CLI `container-registry`.

Quando crei un token per il tuo account {{site.data.keyword.Bluemix_notm}}, puoi decidere se tale token autorizza l'accesso in sola lettura (pull) o in scrittura (push e pull) al registro. Inoltre, puoi specificare se il token è permanente o se scade dopo 24 ore. Puoi e utilizzare più token per controllare i diversi tipi di accesso.

Se accedi a {{site.data.keyword.registrylong_notm}} utilizzando un token di registro, le tue politiche di accesso IAM non vengono applicate. Se desideri limitare l'accesso a uno o più spazi dei nomi per un ID che viene utilizzato nell'automazione, considera l'utilizzo di una chiave API dell'ID servizio IAM invece di un token di registro. Per ulteriori informazioni sulla creazione di una chiave API e il suo utilizzo con {{site.data.keyword.registrylong_notm}}, consulta [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](#registry_api_key).

Utilizza le seguenti attività per gestire i tuoi token:

- [Creazione di un token per il tuo account {{site.data.keyword.Bluemix_notm}} ](#registry_tokens_create)
- [Utilizzo di un token per automatizzare l'accesso ai tuoi spazi dei nomi](#registry_tokens_use)
- [Rimozione di un token dal tuo account {{site.data.keyword.Bluemix_notm}} ](#registry_tokens_remove)

### Creazione di un token per il tuo account {{site.data.keyword.Bluemix_notm}} (obsoleta)
{: #registry_tokens_create}

Puoi creare un token per concedere l'accesso a tutti i tuoi spazi dei nomi {{site.data.keyword.registrylong_notm}} in una regione.
{:shortdesc}

L'utilizzo dei token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi è obsoleto. Utilizza invece le chiavi API per automatizzare l'accesso ai tuoi spazi dei nomi, consulta [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](#registry_api_key).
{: deprecated}

1. Crea un token. Nel seguente esempio viene creato un token senza scadenza che ha l'accesso in lettura e scrittura a tutti gli spazi dei nomi configurati in una regione.

   ```
   ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
   ```
   {: pre}

   <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="light bulb icon"/> Descrizione dei componenti di questo comando</th>
        </thead>
          <caption>Tabella 1. I componenti del comando `ibmcloud cr token-add`</caption>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>Facoltativo. Utilizza questa opzione per descrivere il token in modo da poterlo identificare più facilmente in un secondo momento.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>Facoltativo. Utilizza questa opzione per creare un token senza scadenza. Se non specifichi questa opzione, il token non sarà più valido dopo 24 ore. <br> **Suggerimento:** quando non hai più bisogno di un token senza scadenza per bloccare l'accesso ai tuoi spazi dei nomi, ricorda di rimuovere il token.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>Facoltativo. Utilizza questa opzione per creare un token che consenta agli utenti di eseguire il push e il pull di immagini da e verso i tuoi spazi dei nomi. Se non specifichi questa opzione, il token può essere utilizzato solo per eseguire il pull delle immagini.</td>
        </tr>
        </tbody>
   </table>

   L'output della CLI sarà simile al seguente:

   ```
   Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad
   Token              eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJpYm0uY29tIiwibmFtZSI6Ikdpbm5pIFJvbWV0dHkiLCJpYXQiOjE1NDYzMDA4MDB9.wYMmTPHmrqhyHtgw5T8lbl1hxr2ykHq5T5s3mvMxjDw
   ```
   {: screen}

2. Verifica che il token sia stato creato.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

### Utilizzo di un token per automatizzare l'accesso ai tuoi spazi dei nomi (obsoleto)
{: #registry_tokens_use}

Puoi utilizzare un token nel tuo comando `docker login` per automatizzare l'accesso ai tuoi spazi dei nomi in {{site.data.keyword.registrylong_notm}}. A seconda che l'accesso impostato per il token sia di sola lettura o di lettura/scrittura, gli utenti possono eseguire il push e il pull delle immagini da e verso i tuoi spazi dei nomi.
{:shortdesc}

L'utilizzo dei token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi è obsoleto. Utilizza invece le chiavi API per automatizzare l'accesso ai tuoi spazi dei nomi, consulta [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](#registry_api_key).
{: deprecated}

1. Accedi a {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

2. Elenca tutti i token nel tuo account {{site.data.keyword.Bluemix_notm}} e prendi nota dell'ID token che vuoi utilizzare.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. Richiama il valore per il token. Sostituisci `<token_id>` con l'ID del token.

   ```
   ibmcloud cr token-get <token_id>
   ```
   {: pre}

    Il valore del token viene visualizzato in **Token** nell'output della CLI.

4. Utilizza il token come parte del tuo comando `docker login`. Sostituisci `<token_value>` con il valore del token richiamato nel passo precedente e `<registry_url>` con l'URL del registro in cui sono configurati i tuoi spazi dei nomi.

   - Per gli spazi dei nomi configurati in Asia Pacifico Nord, utilizza `jp.icr.io`
   - Per gli spazi dei nomi configurati in Asia Pacifico Sud, utilizza `au.icr.io`
   - Per gli spazi dei nomi configurati in Europa centrale, utilizza `de.icr.io`
   - Per gli spazi dei nomi configurati in Regno Unito Sud, utilizza `uk.icr.io`
   - Per gli spazi dei nomi configurati in Stati Uniti Sud, utilizza `us.icr.io`

   ```
   docker login -u token -p <valore_token> <url_registro>
   ```
   {: pre}

   Per il parametro `-u`, assicurati di immettere la stringa `token`, non l'ID token.
   {: tip}

   Dopo aver effettuato l'accesso a Docker utilizzando il token, puoi eseguire il push o il pull delle immagini da e verso i tuoi spazi dei nomi.

### Rimozione di un token dal tuo account {{site.data.keyword.Bluemix_notm}} (obsoleta)
{: #registry_tokens_remove}

Rimuovi un token {{site.data.keyword.registrylong_notm}} quando non ne hai più bisogno.
{:shortdesc}

L'utilizzo dei token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi è obsoleto. Utilizza invece le chiavi API per automatizzare l'accesso ai tuoi spazi dei nomi, consulta [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](#registry_api_key).
{: deprecated}

I token {{site.data.keyword.registrylong_notm}} scaduti vengono rimossi automaticamente dal tuo account {{site.data.keyword.Bluemix_notm}} e non è necessario rimuoverli manualmente.
{:tip}

1. Accedi a {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

2. Elenca tutti i token nel tuo account {{site.data.keyword.Bluemix_notm}} e prendi nota dell'ID token che vuoi rimuovere.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. Rimuovi il token.

   ```
   ibmcloud cr token-rm <token_id>
   ```
   {: pre}

## Opzioni di autenticazione per tutti i client
{: #registry_authentication}

Puoi autenticarti utilizzando il comando `docker login` o altri client del registro.
{:shortdesc}

La maggior parte degli utenti possono utilizzare il comando `ibmcloud cr login` per semplificare `docker login`, ma se stai implementando l'automazione o stai utilizzando un client differente, potresti voler eseguire l'autenticazione manualmente. Devi fornire un nome utente e una password. In {{site.data.keyword.registrylong_notm}}, il nome utente indica il tipo di segreto fornito nella password.

I seguenti nomi utente sono validi:

- `iambearer` la password contiene un token di accesso IAM. Questo tipo di autenticazione è di breve durata, ma può essere derivato da tutti i tipi di identità IAM.
- `iamrefresh` la password deve contenere un token di aggiornamento IAM utilizzato internamente per generare e aggiornare un token di accesso IAM. Questo tipo di autenticazione non è più attivo e viene utilizzato dal comando `ibmcloud cr login`.
- `iamapikey` la password è una chiave API IAM. Questo tipo di autenticazione è il tipo preferito per l'automazione. Puoi utilizzare sia una chiave API dell'ID servizio che dell'utente, consulta [Creazione di una chiave API](#registry_api_key_create).
- `token` (obsoleto) la password è un token del registro. Puoi utilizzare questo nome utente per l'automazione.

  L'utilizzo dei token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi è obsoleto. Utilizza invece le chiavi API per automatizzare l'accesso ai tuoi spazi dei nomi, consulta [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](#registry_api_key).
  {: deprecated}

Non devi utilizzare il comando `docker` per l'autenticazione con il registro. Ad esempio, puoi avviare le applicazioni Cloud Foundry dalle immagini nel registro utilizzando la CLI Cloud Foundry:

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Sostituisci `<apikey>` con la tua chiave API, `<region>` con il nome della tua [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` con il tuo spazio dei nomi e `<image_repo>` con il repository.

Per ulteriori informazioni, vedi [Utilizzo di un registro di immagini privato](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
