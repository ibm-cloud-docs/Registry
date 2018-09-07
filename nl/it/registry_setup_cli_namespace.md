---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

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

Prima di poter memorizzare le tue immagini Docker in {{site.data.keyword.registrylong}}, devi installare la CLI {{site.data.keyword.Bluemix_notm}} e il plug-in container-registry
e configurare uno spazio dei nomi del registro per creare il tuo proprio repository di immagini in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione (ad esempio, nei token di registro) o in qualsiasi dato di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{:tip}

Prima di iniziare, installa la CLI [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://clis.ng.bluemix.net/ui/home.html).


## Installazione della CLI {{site.data.keyword.registrylong_notm}} (container-registry plug-in)
{: #registry_cli_install}

Installa la CLI di {{site.data.keyword.registrylong_notm}} per
utilizzare la riga di comando per gestire i tuoi spazi dei nomi e le tue immagini Docker nel registro privato {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1.  [Installa il plug-in container-registry. ](index.html#registry_cli_install)
2.  Facoltativo: [configura il tuo client Docker per eseguire i comandi senza autorizzazioni root](https://docs.docker.com/engine/installation/linux/linux-postinstall). Se non effettui questo passo, devi eseguire i comandi `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` con **sudo** o come root.

Puoi ora configurare il tuo proprio spazio dei nomi nel registro privato {{site.data.keyword.registrylong_notm}}.

## Aggiornamento del plug-in container-registry
{: #registry_cli_update}

Per utilizzare le nuove funzioni, ti consigliamo di aggiornare periodicamente la CLI
{{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Aggiorna il plug-in container-registry.

    ```
    ibmcloud plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  Verifica che il plug-in sia stato aggiornato correttamente.

    ```
    ibmcloud plugin list
    ```
     {: pre}


## Disinstallazione del plug-in container-registry
{: #registry_cli_uninstall}

Se non hai più bisogno del plug-in container-registry, puoi disinstallarlo.
{:shortdesc}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Disinstalla il plug-in container-registry.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

3.  Verifica che il plug-in sia stato disinstallato correttamente.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    Il plug-in container-registry non viene visualizzato nei risultati.


## Configurazione di uno spazio dei nomi
{: #registry_namespace_add}

Per memorizzare in modo sicuro le tue immagini Docker, devi creare uno spazio dei nomi nel registro privato {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Prima di iniziare**

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
    ibmcloud login
    ```
    {: pre}

2.  Elenca gli spazi dei nomi disponibili.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3.  Rimuovi uno spazio dei nomi.

    **Attenzione:** quando rimuovi uno spazio dei nomi, vengono eliminate anche tutte le immagini memorizzate in tale spazio dei nomi. Questa azione non può essere annullata.

    Sostituisci _&lt;mio_spazionomi&gt;_ con lo spazio dei
nomi che vuoi rimuovere.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    Dopo aver eliminato
uno spazio dei nomi, a seconda del numero di immagini che erano state memorizzate, potrebbero volerci alcuni
minuti prima che tale spazio dei nomi ridiventi disponibile per il riutilizzo.
