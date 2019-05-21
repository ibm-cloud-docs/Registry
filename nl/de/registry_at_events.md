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

# {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse
{: #at_events}

Verwenden Sie den {{site.data.keyword.cloudaccesstrailfull}}-Service, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.registrylong}}-Service in {{site.data.keyword.cloud}} interagieren.
{:shortdesc}

Der {{site.data.keyword.cloudaccesstrailfull_notm}} zeichnet die vom Benutzer gestarteten Aktivitäten auf, die den Status eines Service in {{site.data.keyword.cloud_notm}} ändern.
Weitere Informationen finden Sie unter [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

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
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>Erstellt ein Docker-Image in {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>Löscht ein Image aus {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>Zeigt Details zu einem Image an.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>Führt die Images in Ihrem {{site.data.keyword.IBM_notm}}-Konto auf.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>Extrahiert ein Image mit Pull-Operation aus {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>Führt für ein Image eine Push-Operation nach {{site.data.keyword.registrylong_notm}} durch.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Fügt einen neuen Tag hinzu, der sich auf ein bereits bestehendes {{site.data.keyword.registrylong_notm}}-Image bezieht.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>Fügt einen Namensbereich zu {{site.data.keyword.registrylong_notm}} hinzu.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>Löscht einen Namensbereich aus {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>Führt die Namensbereiche in Ihrem {{site.data.keyword.IBM_notm}}-Konto auf.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>Zeigt die aktuellen Kontingente für Datenverkehr und Speicher sowie Nutzungsinformationen zu diesen Kontingenten an.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>Modifiziert die Kontingente.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.create`</td>
	  <td>Erstellt ein neues Registry-Token.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>Löscht ein Registry-Token.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>Ruft Informationen zu einem Registry-Token ab.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>Führt die Registry-Tokens in Ihrem {{site.data.keyword.IBM_notm}}-Konto auf.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>Löscht mehrere Registry-Tokens.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Zeigt Informationen zum aktuellen Preistarif an.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Führt ein Upgrade auf den Standardplan durch.</td>
  </tr>
 </table>

## Speicherposition der Ereignisse
{: #ui}

Die {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse sind in der {{site.data.keyword.cloudaccesstrailshort}}-**Kontodomäne** verfügbar, die sich in der {{site.data.keyword.cloud_notm}}-Region befindet, in der die Ereignisse generiert wurden; eine Ausnahme bildet `ap-north`. Ereignisse für `ap-north` werden in `ap-south` angezeigt.

Die [Region](/docs/services/Registry?topic=registry-registry_overview#registry_regions), in der ein {{site.data.keyword.registrylong_notm}}- oder Vulnerability Advisor-Ereignis verfügbar ist, entspricht der Region von {{site.data.keyword.registrylong_notm}}, in der die Ressource (z. B. das Image oder der Namensbereich) verfügbar ist.
