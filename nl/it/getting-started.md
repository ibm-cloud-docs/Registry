---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-19"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security, cli, namespaces, tutorial, Docker, images, registry

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

# Esercitazione introduttiva
{: #getting-started}

{{site.data.keyword.registrylong}} fornisce un registro delle immagini privato a più tenant che puoi utilizzare per memorizzare e condividere le tue immagini Docker con gli utenti nel tuo account {{site.data.keyword.cloud_notm}}.
{:shortdesc}

La console {{site.data.keyword.cloud_notm}} include una breve guida rapida. Per ulteriori informazioni su come utilizzare la console {{site.data.keyword.cloud_notm}}, vedi [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](/docs/services/va?topic=va-va_index).

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione (ad esempio, nei token di registro) o in qualsiasi dato di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{: important}

## Installa la CLI {{site.data.keyword.registrylong_notm}}
{: #gs_registry_cli_install}

1. Installa la CLI {{site.data.keyword.cloud_notm}} in modo da poter eseguire i {{site.data.keyword.cloud_notm}}comandi `ibmcloud`, vedi [Introduzione alla CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started). Questa installazione installa anche i plug-in CLI per {{site.data.keyword.containerlong_notm}} e {{site.data.keyword.registrylong_notm}}.

## Configura uno spazio dei nomi
{: #gs_registry_namespace_add}

1. Accedi a {{site.data.keyword.cloud_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

   Se hai un ID federato, accedi utilizzando il seguente comando:

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. Aggiungi uno spazio dei nomi per creare il tuo proprio repository di immagini. Sostituisci `<my_namespace>` con il tuo spazio dei nomi preferito.

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

   Lo spazio dei nomi deve essere univoco tra tutti gli account {{site.data.keyword.cloud_notm}} nella stessa regione. Gli spazi dei nomi devono avere tra i 4 e i 30 caratteri e contenere solo lettere minuscole, numeri, trattini (-) e caratteri di sottolineatura (_). Gli spazi dei nomi devono iniziare e terminare con una lettera o un numero.
   {: tip}

3. Per assicurati che il tuo spazio dei nomi sia stato creato, esegui il comando `ibmcloud cr namespace-list`.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Esegui il pull di immagini da un altro registro alla tua macchina locale
{: #gs_registry_images_pulling}

1. [Installa la CLI Docker Engine ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.docker.com/products/container-runtime#/download). Per Windows 8 o per OS X Yosemite 10.10.x o versioni precedenti, installa invece [Docker Toolbox ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/toolbox/). {{site.data.keyword.registrylong_notm}} supporta Docker Engine v1.12.6 o successive.

2. Scarica (_pull_) l'immagine nella tua macchina locale. Sostituisci `<source_image>` con il repository dell'immagine e `<tag>` con la tag dell'immagine che vuoi utilizzare, ad esempio, _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Esempio, dove `<source_image>` è `hello-world` e `<tag>` è `latest`:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Contrassegna l'immagine con una tag. Sostituisci `<source_image>` con il repository e `<tag>` con la tag della tua immagine locale di cui hai prima eseguito il pull. Sostituisci `<region>` con il nome della tua [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions). Sostituisci `<my_namespace>` con lo spazio dei nomi che hai creato in [Configura uno spazio dei nomi](#gs_registry_namespace_add). Definisci il repository e la tag dell'immagine che vuoi utilizzare nel tuo spazio dei nomi sostituendo `<new_image_repo>` e `<new_tag>`.

   ```
   docker tag <source_image>:<tag> <region>.icr.io/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Per trovare il nome della tua regione, esegui il comando `ibmcloud cr region`.
   {: tip}

   Esempio, dove `<source_image>` è `hello-world`, `<tag>` è `latest`, `<region>` è `uk`, `<my_namespace>` è `namespace1`, `<new_image_repo>` è `hw_repo` e `<new_tag>` è `1`:

   ```
   docker tag hello-world:latest uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

## Esegui il push delle immagini Docker nel tuo spazio dei nomi
{: #gs_registry_images_pushing}

1. Esegui il comando `ibmcloud cr login` per registrare il tuo daemon Docker locale in {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Carica (_push_) l'immagine nel tuo spazio dei nomi. Sostituisci `<my_namespace>` con lo spazio dei nomi che hai creato in [Configura uno spazio dei nomi](#gs_registry_namespace_add) e `<image_repo>` e `<tag>` con il repository e la tag dell'immagine che hai scelto quando hai contrassegnato con tag l'immagine.

   ```
   docker push <region>.icr.io/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}
   
   Esempio, dove `<region>` è `uk`, `<my_namespace>` è `namespace1`, `<image_repo>` è `hw_repo` e `<tag>` è `1`:

   ```
   docker push uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

3. Verifica che l'esecuzione del push dell'immagine sia stata eseguita correttamente con il seguente comando.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Ottimo lavoro! Hai configurato uno spazio dei nomi in {{site.data.keyword.registrylong_notm}} e hai eseguito il push della tua prima immagine allo
spazio dei nomi.

## Passi successivi
{: #gs_get_start_next}

- [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](/docs/services/va?topic=va-va_index)
- [Riesamina il tuo utilizzo e i tuoi piani del servizio](/docs/services/Registry?topic=registry-registry_overview#registry_plans)
- [Memorizza e gestisci altre immagini nel tuo spazio dei nomi](/docs/services/Registry?topic=registry-registry_images_)
- [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry?topic=registry-user#user)
- [Configurazione dei cluster e dei nodi di lavoro](/docs/containers?topic=containers-clusters#clusters)
