---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

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

Prima di poter memorizzare le tue immagini Docker in {{site.data.keyword.registrylong}}, devi creare uno spazio dei nomi. Per utilizzare gli spazi dei nomi, installa il plugin CLI `container-registry`.
{:shortdesc}

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione (ad esempio, nei token di registro) o in qualsiasi dato di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{: important}

Prima di iniziare, installa la [CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

## Installazione del plugin CLI `container-registry`
{: #cli_namespace_registry_cli_install}

Installa il plugin CLI `container-registry` per utilizzare la riga di comando per gestire i tuoi spazi dei nomi e le tue immagini Docker in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Installa il plugin CLI `container-registry`.](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Facoltativo: [Configura il tuo client Docker per eseguire i comandi senza autorizzazioni root ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/install/linux/linux-postinstall/). Se non effettui questo passo, devi eseguire i comandi `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` con `sudo` o come root.

Puoi ora configurare il tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}.

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

## Configurazione di uno spazio dei nomi
{: #registry_namespace_setup}

Devi creare uno spazio dei nomi per memorizzare le tue immagini Docker in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Prima di iniziare**

- [Installa la CLI {{site.data.keyword.Bluemix_notm}} e il plugin CLI `container-registry`](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Pianifica come utilizzare e denominare i tuoi spazi dei nomi del registro](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces).

<br>
Per creare uno spazio dei nomi, vedi [Configura uno spazio dei nomi](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add) nella documentazione introduttiva. 

Puoi ora [eseguire il push delle immagini Docker al tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) e condividere queste immagini con altri utenti nel tuo account. Per controllare l'accesso agli spazi dei nomi in {{site.data.keyword.Bluemix_notm}} IAM, vedi [Creazione delle politiche](/docs/services/Registry?topic=registry-user#create).

## Rimozione degli spazi dei nomi
{: #registry_remove}

Se non hai più bisogno di uno spazio dei nomi del registro, puoi rimuoverlo dal tuo account {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1. Accedi a {{site.data.keyword.Bluemix_notm}}.

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
