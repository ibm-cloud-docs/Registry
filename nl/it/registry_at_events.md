---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-26"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker events, Activity Tracker events, events, track,

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

# Eventi {{site.data.keyword.cloudaccesstrailshort}}
{: #at_events}

Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.registrylong}} in {{site.data.keyword.cloud}}.
{:shortdesc}

Il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.cloud_notm}}.
Per ulteriori informazioni, vedi [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

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
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Aggiunge una nuova tag che fa riferimento a un'immagine {{site.data.keyword.registrylong_notm}} preesistente.</td>
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
    <td>`container-registry.registrytoken.create`</td>
	  <td>Crea un nuovo token di registro.</td>
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

Gli eventi di {{site.data.keyword.cloudaccesstrailshort}} sono disponibili nel {{site.data.keyword.cloudaccesstrailshort}} **dominio dell'account** che è disponibile nella regione {{site.data.keyword.cloud_notm}} in cui vengono generati gli eventi, ad eccezione di `ap-north`. Gli eventi per `ap-north` vengono mostrati in `ap-south`.

La [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in cui è disponibile un {{site.data.keyword.registrylong_notm}} o un evento del Controllo vulnerabilità corrisponde alla regione di {{site.data.keyword.registrylong_notm}} in cui è disponibile la risorsa (ad esempio, l'immagine o lo spazio dei nomi).
