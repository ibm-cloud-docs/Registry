---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

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

Utilice el servicio {{site.data.keyword.cloudaccesstrailfull}} para realizar el seguimiento de cómo interactúan los usuarios y las aplicaciones con el servicio {{site.data.keyword.registrylong}} en {{site.data.keyword.cloud}}.
{:shortdesc}

El servicio {{site.data.keyword.cloudaccesstrailfull_notm}} registra las actividades iniciadas por el usuario que cambian el estado de un servicio en {{site.data.keyword.cloud_notm}}.
Para obtener más información, consulte [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

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
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>Cree una imagen de Docker en {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>Suprima una imagen de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>Muestra los detalles sobre una imagen.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>Enumere las imágenes de su cuenta de {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>Extraiga una imagen de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>Envíe una imagen a {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>Suprime una o varias de las imágenes especificadas de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Añada una nueva etiqueta que haga referencia a una imagen de {{site.data.keyword.registrylong_notm}} preexistente.</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>Eliminar una o varias etiquetas, de cada imagen especificada en
{{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>Añada un espacio de nombres a {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>Suprima un espacio de nombres de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>Enumere los espacios de nombres de su cuenta de {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>Visualice sus cuotas actuales de tráfico y almacenamiento, así como información de utilización relacionada con las mismas.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>Modifique las cuotas.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>Suprima una señal de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>Recupere información sobre una señal de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>Enumere las señales de registro de su cuenta de {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>Suprima múltiples señales de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Visualice información sobre el plan de precios actual.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Actualice al plan estándar.</td>
  </tr>
 </table>

## Dónde buscar los sucesos
{: #ui}

Los sucesos de {{site.data.keyword.cloudaccesstrailshort}} están disponibles en el **dominio de cuenta** de {{site.data.keyword.cloudaccesstrailshort}}, que está disponible en la región de {{site.data.keyword.cloud_notm}} donde se han generado los sucesos, excepto `ap-north`. Los sucesos para `ap-north` se muestran en `ap-south`.

La [región](/docs/services/Registry?topic=registry-registry_overview#registry_regions) en la que está disponible un suceso de Vulnerability Advisor o {{site.data.keyword.registrylong_notm}} corresponde a la región de {{site.data.keyword.registrylong_notm}} donde está disponible el recurso (por ejemplo, la imagen o el espacio de nombres).
