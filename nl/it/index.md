---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Introduzione a {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}} fornisce un registro delle
immagini privato a più tenant che puoi utilizzare per memorizzare e condividere in modo sicuro le tue immagini Docker con gli utenti
nel tuo account {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La console {{site.data.keyword.Bluemix_notm}} include una una breve guida rapida. Per ulteriori informazioni su come utilizzare la console {{site.data.keyword.Bluemix_notm}}, vedi [Visualizzazione delle informazioni su immagini nella console {{site.data.keyword.Bluemix_notm}}](registry_ui.html).


## Installa la CLI {{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1.  Installa la CLI di [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://clis.ng.bluemix.net/ui/home.html) in modo da poter eseguire i comandi {{site.data.keyword.Bluemix_notm}} **bx**.
2.  Installa il plug-in container-registry:

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}


## Configura uno spazio dei nomi
{: #registry_namespace_add}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Aggiungi uno spazio dei nomi per creare il tuo proprio repository di immagini. Sostituisci
_&lt;mio_spazionomi&gt;_ con il tuo spazio dei nomi preferito.

    ```
    bx cr namespace-add <mio_spazionomi>
    ```
    {: pre}


## Esegui il pull di immagini da un altro registro alla tua macchina locale
{: #registry_images_pulling}

1.  [Installa la CLI Docker ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.docker.com/community-edition#/download). Per Windows 8 o per OS X Yosemite 10.10.x o versioni precedenti, installa invece [Docker Toolbox ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.docker.com/products/docker-toolbox).

2.  Accedi alla CLI:

    ```
    bx cr login
    ```
    {: pre}

    **Nota:** se esegui il pull di un'immagine dal tuo {{site.data.keyword.registrylong_notm}} privato, devi effettuare l'accesso.

3.  Scarica (_pull_) l'immagine nella tua macchina locale. Sostituisci _&lt;immagine_di_origine&gt;_ con il
repository dell'immagine e _&lt;tag&gt;_ con la tag dell'immagine che vuoi
utilizzare, ad es.,
_latest_.

    ```
    docker pull <immagine_di_origine>:<tag>
    ```
    {: pre}

    Esempio:

    ```
    docker pull hello-world:latest
    ```
    {: pre}

4.  Contrassegna l'immagine con una tag. Sostituisci _&lt;immagine_di_origine&gt;_ con il repository e
_&lt;tag&gt;_ con la tag della tua immagine locale di cui hai prima eseguito il pull. Definisci il
repository e la tag dell'immagine che vuoi utilizzare nel tuo spazio dei nomi sostituendo
_&lt;nuovo_repo_immagine&gt;_ e _&lt;nuova_tag&gt;_.

    ```
    docker tag <immagine_di_origine>:<tag> registry.<region>.bluemix.net/<mio_spazionomi>/<nuovo_repo_immagine>:<nuova_tag>
    ```
    {: pre}

    Esempio:

    ```
    docker tag hello-world:latest registry.<region>.bluemix.net/my_namespace/hw_repo:1
    ```
    {: pre}


## Esegui il push delle immagini Docker nel tuo spazio dei nomi
{: #registry_images_pushing}

1.  Carica (_push_) l'immagine nel tuo spazio dei nomi. Sostituisci
_&lt;mio_spazionomi&gt;_ con lo spazio dei nomi in cui vuoi caricare la tua immagine e
_&lt;repo_immagine&gt;_ e _&lt;tag&gt;_ con il repository e la tag
dell'immagine che hai scelto quando hai contrassegnato con tag l'immagine.

    ```
    docker push registry.<region>.bluemix.net/<mio_spazionomi>/<repo_immagine>:<tag>
    ```
    {: pre}

    Esempio:

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/hw_repo:1
    ```
    {: pre}

2.  Verifica che l'esecuzione del push dell'immagine sia stata eseguita correttamente con il seguente comando.

    ```
    bx cr image-list
    ```
    {: pre}


Ottimo lavoro! Hai configurato uno spazio dei nomi in {{site.data.keyword.registrylong_notm}} e hai eseguito il push della tua prima immagine allo
spazio dei nomi.

**Operazioni successive**

-   [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](../va/va_index.html).
-   [Riesamina il tuo utilizzo e i tuoi piani del servizio](registry_overview.html#registry_plans)
-   [Memorizza e gestisci altre immagini nel tuo spazio dei nomi](registry_images_.html).
-   [Crea e distribuisci un
contenitore dalla tua immagine a un cluster Kubernetes](../../containers/cs_cluster.html).

