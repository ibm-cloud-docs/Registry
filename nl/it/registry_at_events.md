---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker with LogDNA events, Activity Tracker events, events, track,

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

# Eventi di Activity Tracker
{: #at_events}

Tieni traccia del modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.registrylong}} in {{site.data.keyword.cloud}}.
{:shortdesc}

Il servizio {{site.data.keyword.at_full_notm}} o soltanto per gli utenti esistenti, il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.cloud_notm}}.
Per ulteriori informazioni, vedi [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started) o per gli utenti esistenti, [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

La seguente tabella elenca i metodi API che generano un evento quando vengono richiamati:

<table>
  <caption>Tabella 1. Azioni che generano eventi</caption>
  <tr>
    <th>Azione</th>
	  <th>Descrizione</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Crea un'esenzione del controllo vulnerabilità</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Elimina un'esenzione del controllo vulnerabilità</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>Crea un'immagine Docker in {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.bulkdelete`</td>
	  <td>Elimina diverse immagini da {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>Elimina un'immagine da {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>Visualizza i dettagli relativi a un'immagine.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>Elenca le immagini nel tuo account {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>Esegue il pull di un'immagine da {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>Esegue il push di un'immagine in {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>Elimina una o più immagini specificate da {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Aggiunge una tag che fa riferimento a un'immagine {{site.data.keyword.registrylong_notm}} preesistente.</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>Rimuovi una tag o delle tag da ogni immagine specificata in {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>Aggiunge uno spazio dei nomi a {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>Elimina uno spazio dei nomi da {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>Elenca gli spazi dei nomi nel tuo account {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>Visualizza le quote correnti per traffico e archiviazione e le informazioni di utilizzo rispetto a queste quote.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>Modifica le quote.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>Elimina un token di registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>Richiama le informazioni su un token di registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>Elenca i token di registro nel tuo account {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>Elimina più token di registro.</td>
  </tr><tr>
    <td>`container-registry.retentionanalysis`</td>
	  <td>Ripulisci i tuoi spazi dei nomi conservando solo le immagini che soddisfano i tuoi criteri. Conserva le immagini di ogni repository all'interno di uno spazio dei nomi in {{site.data.keyword.registrylong_notm}} applicando dei criteri specificati. Tutte le altre immagini nello spazio dei nomi vengono eliminate. </br> La richiesta per ottenere l'elenco di immagini da eliminare è un'azione `post` su un tipo di evento `retentionanalysis`. L'eliminazione è una singola azione `bulkdelete` su un tipo di evento `images` e anche un'azione `delete` per ogni singola immagine.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Visualizza le informazioni sul piano dei prezzi corrente.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Esegue l'upgrade al piano standard.</td>
  </tr>
 </table>

## Dove ricercare gli eventi
{: #ui}

### Eventi {{site.data.keyword.at_full_notm}}
{: #ui_atlogdna}

Gli eventi di {{site.data.keyword.at_full_notm}} sono disponibili nel {{site.data.keyword.at_full_notm}} **dominio dell'account** che è disponibile nella regione {{site.data.keyword.cloud_notm}} in cui vengono generati gli eventi, ad eccezione di `ap-south`. Gli eventi per `ap-south` vengono mostrati in `Tokyo (jp-tok)`.

La [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in cui è disponibile un {{site.data.keyword.registrylong_notm}} o un evento del Controllo vulnerabilità corrisponde alla regione di {{site.data.keyword.registrylong_notm}} in cui è disponibile la risorsa. Le immagini e gli spazi dei nomi sono esempi di risorse.

| Regione per il registro del tuo account | Nome di dominio del tuo registro | Ubicazione degli eventi {{site.data.keyword.at_full_notm}} |
|:-----------------|:-----------------|:-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="Tabella 2. Ubicazione degli eventi {{site.data.keyword.at_full_notm}} " caption-side="top"}

| Registro | Registro globale | Ubicazione degli eventi {{site.data.keyword.at_full_notm}} |
|:-----------------|:-----------------|:-----------------|
| Globale | `icr.io` | `Dallas (us-south)` |
{: caption="Tabella 3. Ubicazione degli eventi {{site.data.keyword.at_full_notm}} del registro globale" caption-side="top"}

### Eventi {{site.data.keyword.cloudaccesstraillong_notm}}
{: #ui_at}

Gli eventi di {{site.data.keyword.cloudaccesstraillong_notm}}, soltanto per gli utenti esistenti, sono disponibili nel {{site.data.keyword.cloudaccesstraillong_notm}} **dominio dell'account** che è disponibile nella regione {{site.data.keyword.cloud_notm}} in cui vengono generati gli eventi, ad eccezione di `ap-north`. Gli eventi per `ap-north` vengono mostrati in `ap-south`.

{{site.data.keyword.cloudaccesstrailfull_notm}} è obsoleto. A partire dal 9 maggio 2019, non puoi eseguire il provisioning di nuove istanze di {{site.data.keyword.cloudaccesstrailshort}}. Le istanze del piano Premium esistenti sono supportate fino al 30 settembre 2019. Per continuare a monitorare l'attività del tuo account {{site.data.keyword.cloud_notm}}, esegui il provisioning di un'istanza di [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).
{: deprecated}

La [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in cui è disponibile un {{site.data.keyword.registrylong_notm}} o un evento del Controllo vulnerabilità corrisponde alla regione di {{site.data.keyword.registrylong_notm}} in cui è disponibile la risorsa. Le immagini e gli spazi dei nomi sono esempi di risorse.
