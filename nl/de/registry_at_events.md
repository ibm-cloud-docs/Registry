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

# {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse
{: #at_events}

Verwenden Sie den {{site.data.keyword.cloudaccesstrailfull}}-Service, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.registrylong}}-Service in {{site.data.keyword.Bluemix}} interagieren.
{:shortdesc}

Der {{site.data.keyword.cloudaccesstrailfull_notm}} zeichnet die vom Benutzer gestarteten Aktivitäten auf, die den Status eines Service in {{site.data.keyword.Bluemix_notm}} ändern.
Weitere Informationen finden Sie unter [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla).

In der folgenden Tabelle werden die API-Methoden aufgelistet, die ein Ereignis auslösen, wenn sie aufgerufen werden:

<table>
  <caption>Tabelle 1. Aktionen, die Ereignisse generieren</caption>
  <tr>
    <th>Aktion</th>
	  <th>Beschreibung</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Erstellt eine Ausnahme für Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Löscht eine Ausnahme für Vulnerability Advisor.</td>
  </tr>
 </table>

## Speicherposition der Ereignisse
{: #ui}

Die {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse sind in der {{site.data.keyword.cloudaccesstrailshort}}-**Kontodomäne** verfügbar, die sich in der {{site.data.keyword.Bluemix_notm}}-Region befindet, in der die Ereignisse generiert wurden.

Die [Region](/docs/services/Registry?topic=registry-registry_overview#registry_regions), in der ein Vulnerability Advisor-Ereignis verfügbar ist, entspricht der Region von {{site.data.keyword.registrylong_notm}}, in der die Ressource (z. B. das Image oder der Namensbereich) verfügbar ist.
