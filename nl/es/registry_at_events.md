---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-06"

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

# Sucesos de {{site.data.keyword.cloudaccesstrailshort}}
{: #at_events}

Utilice el servicio {{site.data.keyword.cloudaccesstrailfull}} para realizar el seguimiento de cómo interactúan los usuarios y las aplicaciones con el servicio {{site.data.keyword.registrylong}} en {{site.data.keyword.Bluemix}}.
{:shortdesc}

El servicio {{site.data.keyword.cloudaccesstrailfull_notm}} registra las actividades iniciadas por el usuario que cambian el estado de un servicio en {{site.data.keyword.Bluemix_notm}}.
Para obtener más información, consulte [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla).


En la tabla siguiente se muestran los métodos de API que generan un suceso cuando se le llama:

<table>
  <caption>Tabla 1. Acciones que generan sucesos</caption>
  <tr>
    <th>Acción</th>
	  <th>Descripción</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Cree una exención de Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Suprima una exención de Vulnerability Advisor.</td>
  </tr>
 </table>

## Dónde buscar los sucesos
{: #ui}

Los sucesos de {{site.data.keyword.cloudaccesstrailshort}} están disponibles en el {{site.data.keyword.cloudaccesstrailshort}} **dominio de la cuenta** disponible en la región de {{site.data.keyword.Bluemix_notm}} donde se han generado los sucesos.

La [región](/docs/services/Registry?topic=registry-registry_overview#registry_regions) en la que está disponible un suceso de Vulnerability Advisor corresponde a la región de {{site.data.keyword.registrylong_notm}} onde está disponible el recurso (por ejemplo, la imagen o el espacio de nombres).
