---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, Activity Tracker events, events

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

Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.registrylong}} in {{site.data.keyword.Bluemix}}.
{:shortdesc}

Il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.Bluemix_notm}}.
Per ulteriori informazioni, vedi [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla).

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
 </table>

## Dove ricercare gli eventi
{: #ui}

Gli eventi di {{site.data.keyword.cloudaccesstrailshort}} sono disponibili nel **dominio dell'account** {{site.data.keyword.cloudaccesstrailshort}}, che è disponibile nella regione {{site.data.keyword.Bluemix_notm}} in cui vengono generati gli eventi.

La [regione](/docs/services/Registry?topic=registry-registry_overview#registry_regions) in cui è disponibile un evento del Controllo vulnerabilità corrisponde alla regione di {{site.data.keyword.registrylong_notm}} in cui è disponibile la risorsa (ad esempio, l'immagine o lo spazio dei nomi).
