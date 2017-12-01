---

copyright:
  years: 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Configurazione della CLI di {{site.data.keyword.registrylong_notm}} e
del tuo spazio dei nomi del registro
{: #registry_setup_cli_namespace}

Prima di poter memorizzare le tue immagini Docker in {{site.data.keyword.registrylong}}, devi installare la CLI {{site.data.keyword.Bluemix_notm}} e il plugin {{site.data.keyword.registrylong_notm}}
e configurare uno spazio dei nomi del registro per creare il tuo proprio repository di immagini in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}


## Installazione del plug-in CLI di {{site.data.keyword.registrylong_notm}} (`bx cr`)
{: #registry_cli_install}

Installa la CLI di {{site.data.keyword.registrylong_notm}} per
utilizzare la riga di comando per gestire i tuoi spazi dei nomi e le tue immagini Docker nel registro privato {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1.  [Installa il plug-in container-registry. ](index.html#registry_cli_install)
2.  Facoltativo: [configura il tuo client Docker per eseguire i comandi senza autorizzazioni root](https://docs.docker.com/engine/installation/linux/linux-postinstall). Se non effettui questo passaggio, devi eseguire i comandi `bx login`, `bx cr
login`, `docker pull` e `docker push` con **sudo** o come root.

Puoi ora configurare il tuo proprio spazio dei nomi nel registro privato {{site.data.keyword.registrylong_notm}}.

## Aggiornamento del plug-in {{site.data.keyword.registrylong_notm}} (`bx
cr`)
{: #registry_cli_update}

Per utilizzare le nuove funzioni, ti consigliamo di aggiornare periodicamente la CLI
{{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Aggiorna il plug-in container-registry.

    ```
    bx plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  Verifica che il plug-in sia stato aggiornato correttamente.

    ```
    bx plugin list
    ```
     {: pre}


## Disinstallazione del plug-in {{site.data.keyword.registrylong_notm}}
(`bx cr`)
{: #registry_cli_uninstall}

Se non hai più bisogno del plug-in container-registry, puoi disinstallarlo.
{:shortdesc}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Disinstalla il plug-in container-registry.

    ```
    bx plugin uninstall container-registry
    ```
    {: pre}

3.  Verifica che il plug-in sia stato disinstallato correttamente.

    ```
    bx plugin list
    ```
    {: pre}

    Il plug-in container-registry non viene visualizzato nei risultati.


## Configurazione di uno spazio dei nomi
{: #registry_namespace_add}

Per memorizzare in modo sicuro le tue immagini Docker, devi creare uno spazio dei nomi nel registro privato {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Prima di iniziare:

-   [Installa la CLI {{site.data.keyword.Bluemix_notm}} e il plugin container-registry](#registry_cli_install).
-   [Pianifica come utilizzare e denominare i tuoi spazi dei nomi del registro](registry_overview.html#registry_namespaces).

Crea uno spazio dei nomi; vedi [Configura uno spazio dei nomi](index.html#registry_namespace_add) nella documentazione introduttiva.

Puoi ora [eseguire il push delle immagini Docker al tuo spazio dei nomi nel registro {{site.data.keyword.Bluemix_notm}}](registry_images_.html#registry_images_pushing) e condividere queste immagini con altri utenti nel tuo account.

## Rimozione degli spazi dei nomi
{: #registry_remove}

Se non hai più bisogno di uno spazio dei nomi del registro, puoi rimuoverlo dal tuo account {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Elenca gli spazi dei nomi disponibili.

    ```
    bx cr namespace-list
    ```
    {: pre}

3.  Rimuovi uno spazio dei nomi. 

    **Attenzione:** quando rimuovi uno spazio dei nomi, vengono eliminate anche tutte le immagini memorizzate in tale spazio dei nomi. Questa azione non può essere annullata.
    
    Sostituisci _&lt;mio_spazionomi&gt;_ con lo spazio dei
nomi che vuoi rimuovere.

    ```
    bx cr namespace-rm <mio_spazionomi>
    ```
    {: pre}

    Dopo aver eliminato
uno spazio dei nomi, a seconda del numero di immagini che erano state memorizzate, potrebbero volerci alcuni
minuti prima che tale spazio dei nomi ridiventi disponibile per il riutilizzo.
