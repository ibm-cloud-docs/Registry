---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-16"

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

La console {{site.data.keyword.Bluemix_notm}} include una breve guida rapida. Per ulteriori informazioni su come utilizzare la console {{site.data.keyword.Bluemix_notm}}, vedi [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](/docs/services/va/va_index.html).

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione (ad esempio, nei token di registro) o in qualsiasi dato di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{:tip}

## Installa la CLI {{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1. Installa la CLI di [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://clis.ng.bluemix.net/ui/home.html) in modo da poter eseguire i comandi {{site.data.keyword.Bluemix_notm}} `ibmcloud`. Questa installazione installa anche i plug-in per {{site.data.keyword.containerlong_notm}} e {{site.data.keyword.registrylong_notm}}.

## Configura uno spazio dei nomi
{: #registry_namespace_add}

1. Accedi a {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

2. Aggiungi uno spazio dei nomi per creare il tuo proprio repository di immagini. Sostituisci _&lt;my_namespace&gt;_ con il tuo spazio dei nomi preferito.

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

3. Per assicurati che il tuo spazio dei nomi sia stato creato, esegui il comando `ibmcloud cr namespace-list`.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Esegui il pull di immagini da un altro registro alla tua macchina locale
{: #registry_images_pulling}

1. [Installa la CLI Docker ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.docker.com/community-edition#/download). Per Windows 8 o per OS X Yosemite 10.10.x o versioni precedenti, installa invece [Docker Toolbox ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/toolbox/).

2. Scarica (_pull_) l'immagine nella tua macchina locale. Sostituisci _&lt;source_image&gt;_ con il repository dell'immagine e _&lt;tag&gt;_ con la tag dell'immagine che vuoi utilizzare, ad esempio, _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Esempio, dove _&lt;source_image&gt;_ è `hello-world` e _&lt;tag&gt;_ è `latest`:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Contrassegna l'immagine con una tag. Sostituisci _&lt;source_image&gt;_ con il repository e
_&lt;tag&gt;_ con la tag della tua immagine locale di cui hai prima eseguito il pull. Sostituisci _&lt;image_name&gt;_ con il nome della tua [regione](registry_overview.html#registry_regions). Sostituisci _&lt;my_namespace&gt;_ con lo spazio dei nomi che hai creato in [Configura uno spazio dei nomi](index.html#registry_namespace_add). Definisci il
repository e la tag dell'immagine che vuoi utilizzare nel tuo spazio dei nomi sostituendo
_&lt;new_image_repo&gt;_ e _&lt;new_tag&gt;_.

   ```
   docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Esempio, dove _&lt;source_image&gt;_ è `hello-world`, _&lt;tag&gt;_ è `latest`, _&lt;region&gt;_ è `eu-gb`, _&lt;my_namespace&gt;_ è `namespace1`, _&lt;new_image_repo&gt;_ è `hw_repo` e _&lt;new_tag&gt;_ è `1`:

   ```
   docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

## Esegui il push delle immagini Docker nel tuo spazio dei nomi
{: #registry_images_pushing}

1. Esegui il comando `ibmcloud cr login` per registrare il tuo daemon Docker locale in {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Carica (_push_) l'immagine nel tuo spazio dei nomi. Sostituisci
_&lt;my_namespace&gt;_ con lo spazio dei nomi che hai creato in [Configura uno spazio dei nomi](index.html#registry_namespace_add) e
_&lt;image_repo&gt;_ e _&lt;tag&gt;_ con il repository e la tag
dell'immagine che hai scelto quando hai contrassegnato con tag l'immagine.

   ```
   docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}

   Esempio, dove _&lt;region&gt;_ è `eu-gb`, _&lt;my_namespace&gt;_ è `namespace1`, _&lt;image_repo&gt;_ è `hw_repo` e _&lt;tag&gt;_ è `1`:

   ```
   docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

3. Verifica che l'esecuzione del push dell'immagine sia stata eseguita correttamente con il seguente comando.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Ottimo lavoro! Hai configurato uno spazio dei nomi in {{site.data.keyword.registrylong_notm}} e hai eseguito il push della tua prima immagine allo
spazio dei nomi.

**Operazioni successive**

- [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](../va/va_index.html)
- [Riesamina il tuo utilizzo e i tuoi piani del servizio](registry_overview.html#registry_plans)
- [Memorizza e gestisci altre immagini nel tuo spazio dei nomi](registry_images_.html)
- [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry/registry_users.html#user)
- [Configurazione dei cluster e dei nodi di lavoro](/docs/containers/cs_clusters.html#clusters)
