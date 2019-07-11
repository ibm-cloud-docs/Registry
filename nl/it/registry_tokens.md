---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

Puoi utilizzare una chiave API {{site.data.keyword.iamlong}} (IAM) per automatizzare l'accesso ai tuoi spazi dei nomi {{site.data.keyword.registrylong_notm}} in modo da poter eseguire il push e il pull delle immagini.
{:shortdesc}

Stai cercando di utilizzare le tue immagini del registro nelle distribuzioni Kubernetes? Consulta [Accesso alle immagini in altri spazi dei nomi Kubernetes, regioni {{site.data.keyword.cloud_notm}} e account](/docs/containers?topic=containers-images#other).
{: tip}

Le chiavi API sono collegate al tuo account e possono essere utilizzate in {{site.data.keyword.cloud_notm}} in modo che non hai bisogno di credenziali differenti per ogni servizio. Puoi utilizzare la chiave API nella CLI o come parte dell'automazione dell'accesso come tua identità utente.

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

Utilizza la chiave API per accedere al tuo registro eseguendo il seguente comando Docker. Sostituisci `<your_apikey>` con la tua chiave API e `<registry_url>` con l'URL del registro in cui sono configurati i tuoi spazi dei nomi.

- Per gli spazi dei nomi configurati in Asia Pacifico Nord, utilizza `jp.icr.io`
- Per gli spazi dei nomi configurati in Asia Pacifico Sud, utilizza `au.icr.io`
- Per gli spazi dei nomi configurati in Europa centrale, utilizza `de.icr.io`
- Per gli spazi dei nomi configurati in Regno Unito Sud, utilizza `uk.icr.io`
- Per gli spazi dei nomi configurati in Stati Uniti Sud, utilizza `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Per le informazioni di riferimento sul comando, consulta [Crea una nuova chiave API della piattaforma {{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Opzioni di autenticazione per tutti i client
{: #registry_authentication}

Puoi autenticarti utilizzando il comando `docker login` o altri client del registro.
{:shortdesc}

La maggior parte degli utenti possono utilizzare il comando `ibmcloud cr login` per semplificare `docker login`, ma se stai implementando l'automazione o stai utilizzando un client differente, potresti voler eseguire l'autenticazione manualmente. Devi fornire un nome utente e una password. In {{site.data.keyword.registrylong_notm}}, il nome utente indica il tipo di segreto fornito nella password.

I seguenti nomi utente sono validi:

- `iambearer` la password contiene un token di accesso IAM. Questo tipo di autenticazione è di breve durata, ma può essere derivato da tutti i tipi di identità IAM.
- `iamrefresh` la password deve contenere un token di aggiornamento IAM utilizzato internamente per generare e aggiornare un token di accesso IAM. Questo tipo di autenticazione non è più attivo e viene utilizzato dal comando `ibmcloud cr login`.
- `iamapikey` la password è una chiave API IAM. Questo tipo di autenticazione è il tipo preferito per l'automazione. Puoi utilizzare sia una chiave API dell'ID servizio che dell'utente, consulta [Creazione di una chiave API](#registry_api_key_create).

Non devi utilizzare il comando `docker` per l'autenticazione con il registro. Ad esempio, puoi avviare le applicazioni Cloud Foundry dalle immagini nel registro utilizzando la CLI Cloud Foundry:

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Sostituisci `<apikey>` con la tua chiave API, `<region>` con il nome della tua [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` con il tuo spazio dei nomi e `<image_repo>` con il repository.

Per ulteriori informazioni, vedi [Utilizzo di un registro di immagini privato](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
