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

# Sucesos de Activity Tracker
{: #at_events}

Puede realizar el seguimiento de cómo interactúan los usuarios y las aplicaciones con el servicio {{site.data.keyword.registrylong}} en {{site.data.keyword.cloud}}.
{:shortdesc}

El servicio {{site.data.keyword.at_full_notm}} o, sólo para usuarios existentes, el servicio {{site.data.keyword.cloudaccesstrailfull_notm}} registra las actividades iniciadas por el usuario que cambian el estado de un servicio en {{site.data.keyword.cloud_notm}}.
Para obtener más información, consulte [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started) o, sólo para usuarios existentes, [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

En la tabla siguiente se muestran los métodos de API que generan un suceso cuando se le llama:

<table>
  <caption>Tabla 1. Acciones que generan sucesos</caption>
  <tr>
    <th>Acción</th>
	  <th>Descripción</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Crear una exención de Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Suprimir una exención de Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>Crear una imagen de Docker en {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.bulkdelete`</td>
	  <td>Suprimir varias imágenes de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>Suprimir una imagen de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>Mostrar los detalles sobre una imagen.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>Enumerar las imágenes de su cuenta de {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>Extraer una imagen de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>Enviar una imagen a {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>Suprimir una o varias de las imágenes especificadas de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Añadir una etiqueta que hace referencia a una imagen de {{site.data.keyword.registrylong_notm}} preexistente.</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>Eliminar una o varias etiquetas, de cada imagen especificada en
{{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>Añadir un espacio de nombres a {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>Suprimir un espacio de nombres de {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>Enumerar los espacios de nombres de su cuenta de {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>Visualizar sus cuotas actuales de tráfico y almacenamiento, así como información de utilización relacionada con las mismas.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>Modificar las cuotas.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>Suprimir una señal de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>Recuperar información sobre una señal de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>Enumerar las señales de registro de su cuenta de {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>Suprimir múltiples señales de registro.</td>
  </tr><tr>
    <td>`container-registry.retentionanalysis`</td>
	  <td>Limpiar los espacios de nombres reteniendo únicamente las imágenes que cumplan unos criterios. Retener imágenes de cada uno de los repositorios de {{site.data.keyword.registrylong_notm}} según los criterios especificados. Todas las demás imágenes del espacio de nombres se suprimen. </br> La solicitud de obtener la lista de imágenes a suprimir es una acción `post` sobre un tipo de suceso `retentionanalysis`. La supresión es una acción `bulkdelete` sobre un tipo de suceso `images` y también una acción `delete` para cada una de las imágenes.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Visualizar información sobre el plan de precios actual.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Actualizarse al plan estándar.</td>
  </tr>
 </table>

## Dónde buscar los sucesos
{: #ui}

### Sucesos de {{site.data.keyword.at_full_notm}}
{: #ui_atlogdna}

Los sucesos de {{site.data.keyword.at_full_notm}} están disponibles en el **dominio de cuenta** de {{site.data.keyword.at_full_notm}}, que está disponible en la región de {{site.data.keyword.cloud_notm}} donde se han generado los sucesos, excepto `ap-south`. Los sucesos de `ap-south` se muestran en `Tokyo (jp-tok)`.

La [región](/docs/services/Registry?topic=registry-registry_overview#registry_regions) en la que está disponible un suceso de Vulnerability Advisor o {{site.data.keyword.registrylong_notm}} corresponde a la región de {{site.data.keyword.registrylong_notm}} donde está disponible el recurso. Las imágenes y los espacios de nombres son ejemplos de recursos.

| Región del registro de la cuenta | Nombre de dominio del registro | Ubicación de los sucesos de {{site.data.keyword.at_full_notm}} |
|:-----------------|:-----------------|:-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Frankfurt (eu-de)` |
| `uk-south` | `uk.icr.io` | `London (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="Tabla 2. Ubicación de los sucesos de {{site.data.keyword.at_full_notm}}" caption-side="top"}

| Registro | Registro global | Ubicación de los sucesos de {{site.data.keyword.at_full_notm}} |
|:-----------------|:-----------------|:-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Tabla 3. Ubicación de los sucesos de {{site.data.keyword.at_full_notm}} de registro global" caption-side="top"}

### Sucesos de {{site.data.keyword.cloudaccesstraillong_notm}}
{: #ui_at}

Los sucesos de {{site.data.keyword.cloudaccesstraillong_notm}}, sólo para usuarios existentes, están disponibles en el **dominio de cuenta** de {{site.data.keyword.cloudaccesstraillong_notm}} que está disponible en la región de {{site.data.keyword.cloud_notm}} donde se han generado los sucesos, excepto `ap-north`. Los sucesos para `ap-north` se muestran en `ap-south`.

{{site.data.keyword.cloudaccesstrailfull_notm}} está en desuso. A partir del 9 de mayo de 2019, no se pueden suministrar nuevas instancias de {{site.data.keyword.cloudaccesstrailshort}}. Se da soporte a las instancias existentes del plan premium hasta el 30 de septiembre de 2019. Para continuar supervisando la actividad de la cuenta de {{site.data.keyword.cloud_notm}}, suministre una instancia de [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).
{: deprecated}

La [región](/docs/services/Registry?topic=registry-registry_overview#registry_regions) en la que está disponible un suceso de Vulnerability Advisor o {{site.data.keyword.registrylong_notm}} corresponde a la región de {{site.data.keyword.registrylong_notm}} donde está disponible el recurso. Las imágenes y los espacios de nombres son ejemplos de recursos.
