---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, 

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

# Configurazione della CLI di {{site.data.keyword.registrylong_notm}} e
del tuo spazio dei nomi del registro
{: #registry_setup_cli_namespace}

Per gestire le tue immagini Docker in {{site.data.keyword.registrylong}}, devi installare il plugin CLI `container-registry` e creare uno spazio dei nomi.
{:shortdesc}

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione o nei dati di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{: important}

Prima di cominciare, installa la CLI {{site.data.keyword.cloud_notm}}, vedi [Introduzione alla CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started).

## Installazione del plugin CLI `container-registry`
{: #cli_namespace_registry_cli_install}

Installa il plugin CLI `container-registry` per utilizzare la riga di comando per gestire i tuoi spazi dei nomi e le tue immagini Docker in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Installa il plugin CLI `container-registry`.](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Facoltativo: [Configura il tuo client Docker per eseguire i comandi senza autorizzazioni root ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/install/linux/linux-postinstall/). Se non effettui questo passo, devi eseguire i comandi `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` con `sudo` o come root.

Puoi ora [configurare il tuo [spazio dei nomi](#registry_namespace_setup) in {{site.data.keyword.registrylong_notm}}.

## Aggiornamento del plugin CLI `container-registry`
{: #registry_cli_update}

Per utilizzare le nuove funzioni, ti consigliamo di aggiornare periodicamente il plugin CLI `container-registry`.
{:shortdesc}

1. Aggiorna il plug-in `container-registry`.

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. Verifica che il plugin CLI `container-registry` sia stato aggiornato correttamente.

    ```
    ibmcloud plugin list
    ```
     {: pre}

## Disinstallazione del plugin CLI `container-registry`
{: #registry_cli_uninstall}

Se non hai più bisogno del plug-in CLI `container-registry`, puoi disinstallarlo.
{:shortdesc}

1. Disinstalla il plug-in `container-registry`.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. Verifica che il plugin CLI `container-registry` sia stato disinstallato correttamente.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    Il plug-in CLI `container-registry` non viene visualizzato nei risultati.

## Pianificazione degli spazi dei nomi
{: #registry_setup_cli_namespace_plan}

{{site.data.keyword.registrylong_notm}} fornisce un registro delle immagini privato
a più tenant che viene ospitato e gestito da IBM. Puoi memorizzare e condividere le tue immagini Docker in questo registro configurando uno spazio dei nomi del registro.
{:shortdesc}

Puoi configurare più spazi dei nomi per avere, ad esempio, repository separati per i tuoi
ambienti di produzione e di preparazione. Se vuoi utilizzare il registro in più regioni {{site.data.keyword.cloud_notm}}, devi configurare uno spazio dei nomi per
ogni regione. I nomi degli spazi dei nomi sono univoci nelle regioni. Puoi utilizzare lo stesso nome dello spazio dei nomi per ogni regione, a meno che
qualcun altro abbia già configurato uno spazio dei nomi con quel nome in tale regione.

Puoi controllare l'accesso ai tuoi spazi dei nomi utilizzando le politiche IAM. Per ulteriori informazioni, consulta [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry?topic=registry-user#user).

Per lavorare solo con le immagini pubbliche fornite da IBM, non hai bisogno di configurare uno
spazio dei nomi.

Se non sei sicuro che uno spazio dei nomi sia già impostato per il tuo account, esegui il comando `ibmcloud cr namespace-list` per richiamare le informazioni sugli spazi dei nomi esistenti.
{:tip}

Quando scegli uno spazio dei nomi, considera le seguenti regole:

- Il tuo spazio dei nomi deve essere univoco tra tutti gli account {{site.data.keyword.cloud_notm}} nella stessa regione.
- Il tuo spazio dei nomi deve avere una lunghezza compresa tra 4 e 30 caratteri.
- Il tuo spazio dei nomi deve iniziare e terminare con una lettera o un numero.
- Il tuo spazio dei nomi deve contenere solo lettere minuscole, numeri, trattini (-) e caratteri di sottolineatura (_).

Non inserire informazioni personali nei tuoi nomi dello spazio dei nomi.
{: important}

Dopo aver impostato il tuo primo spazio dei nomi, ti verrà assegnato il piano del servizio {{site.data.keyword.registrylong_notm}}
gratuito se non hai già [eseguito l'upgrade del tuo piano](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade).

## Configurazione di uno spazio dei nomi
{: #registry_namespace_setup}

Devi creare uno spazio dei nomi per memorizzare le tue immagini Docker in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Prima di iniziare**

- [Installa la CLI {{site.data.keyword.cloud_notm}} e il plugin CLI `container-registry`](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Pianifica come utilizzare e denominare i tuoi spazi dei nomi del registro](#registry_setup_cli_namespace_plan).

Per creare uno spazio dei nomi, vedi [Configura uno spazio dei nomi](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add) nella documentazione introduttiva.

Lo spazio dei nomi deve essere univoco tra tutti gli account {{site.data.keyword.cloud_notm}} nella stessa regione. Gli spazi dei nomi devono avere tra i 4 e i 30 caratteri e contenere solo lettere minuscole, numeri, trattini (-) e caratteri di sottolineatura (_). Gli spazi dei nomi devono iniziare e terminare con una lettera o un numero.
{: tip}

Puoi ora [eseguire il push delle immagini Docker al tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) e condividere queste immagini con altri utenti nel tuo account. Per controllare l'accesso agli spazi dei nomi in {{site.data.keyword.cloud_notm}} IAM, vedi [Creazione delle politiche](/docs/services/Registry?topic=registry-user#create).

## Rimozione degli spazi dei nomi
{: #registry_remove}

Se non hai più bisogno di uno spazio dei nomi del registro, puoi rimuoverlo dal tuo account {{site.data.keyword.cloud_notm}}.
{:shortdesc}

1. Accedi a {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Elenca gli spazi dei nomi disponibili.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. Rimuovi uno spazio dei nomi.

    **Attenzione:** quando rimuovi uno spazio dei nomi, vengono eliminate anche tutte le immagini memorizzate in tale spazio dei nomi. Questa azione non può essere annullata.

    Sostituisci `<my_namespace>` con lo spazio dei nomi che vuoi rimuovere.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    Dopo aver eliminato uno spazio dei nomi, potrebbero volerci alcuni minuti prima che tale spazio dei nomi ridiventi disponibile per il riutilizzo.
