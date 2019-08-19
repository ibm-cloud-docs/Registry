---

copyright:
  years: 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# Notas del release
{: #registry_release_notes}

Obtenga información sobre los últimos cambios realizados en {{site.data.keyword.registrylong}} y Vulnerability Advisor. Los cambios están agrupados por fecha.
{:shortdesc}

## 1 de agosto de 2019
{: #01aug2019}

<dl>
  <dt>El mandato `ibmcloud cr retention-run` está disponible</dt>
  <dd>El mandato `ibmcloud cr retention-run` limpia los espacios de nombres reteniendo las imágenes de cada uno de los repositorios de {{site.data.keyword.registrylong_notm}} según los criterios especificados. Todas las demás imágenes del espacio de nombres se suprimen.
  
  Para obtener más información, consulte [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) y [Retención de imágenes](/docs/services/Registry?topic=registry-registry_retention).</dd>
</dl>

## 25 de julio de 2019
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.at_full_notm}} disponible para {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Utilice el servicio {{site.data.keyword.at_full_notm}} para realizar el seguimiento de cómo interactúan los usuarios y las aplicaciones con el servicio {{site.data.keyword.registrylong_notm}} en {{site.data.keyword.cloud}}.

  Para obtener más información, consulte [Sucesos de Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>

## 1 de julio de 2019
{: #1jul2019}

<dl>
  <dt>El mandato `ibmcloud cr token-add` ya no está disponible</dt>
  <dd>El mandato `ibmcloud cr token-add` se ha retirado. Ya no puede añadir señales de registro ni en la CLI ni en la API.</dd>
</dl>

## 27 de junio de 2019
{: #27jun2019}

<dl>
  <dt>Container Scanner ya no está disponible</dt>
  <dd>Container Scanner se ha retirado. Vulnerability Advisor sigue explorando las imágenes que se envían a {{site.data.keyword.registrylong_notm}}.</dd>
</dl>

## 13 de junio de 2019
{: #13jun2019}

<dl>
  <dt>Eliminar etiquetas de imágenes</dt>
  <dd>Eliminar una o varias etiquetas, de cada imagen especificada en
{{site.data.keyword.registrylong_notm}}.

  Para eliminar una etiqueta específica de una imagen y dejar la imagen
subyacente y cualquier otra etiqueta en su sitio, utilice el mandato
[`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag). Si quiere suprimir la imagen subyacente y todas sus etiquetas, utilice en su lugar el mandato
[`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm).

  Para obtener más información, consulte
[Eliminación de etiquetas de imágenes en su repositorio privado de {{site.data.keyword.cloud_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag).</dd>
</dl>

## 13 de mayo de 2019
{: #13may2019}

<dl>
  <dt>Fin del soporte para Container Scanner</dt>
  <dd>Container Scanner está en desuso y ya no se puede utilizar.

  Para obtener más información, consulte [Instalación de Container Scanner (en desuso)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 2 de abril de 2019
{: #2apr2019}

<dl>
  <dt>Disponibilidad general de Container Image Security Enforcement</dt>
  <dd>Utilice Container Image Security Enforcement para verificar las imágenes del contenedor antes de desplegarlas en el clúster en {{site.data.keyword.containerlong_notm}}. Puede controlar desde dónde se despliegan las imágenes, forzar políticas de Vulnerability Advisor y asegurarse de que el [contenido de confianza](/docs/services/Registry?topic=registry-registry_trustedcontent) esté aplicado correctamente a la imagen.

  Para obtener más información, consulte [Imposición de seguridad de la imagen de contenedor](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 14 de marzo de 2019
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponible para {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Utilice el servicio {{site.data.keyword.cloudaccesstraillong_notm}} para realizar el seguimiento de cómo interactúan los usuarios y las aplicaciones con el servicio {{site.data.keyword.registrylong_notm}} en {{site.data.keyword.cloud}}.

  Para obtener más información, consulte [Sucesos de Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).
</dd>
</dl>

## 25 de febrero de 2019
{: #25feb2019}

<dl>
  <dt>Nuevos nombres de dominio</dt>
  <dd>{{site.data.keyword.registrylong_notm}} está adoptando nuevos nombres de dominio. Los nuevos nombres de dominio están disponibles en la consola y en la CLI. Ya puede utilizar los nuevos nombres de dominio `icr.io`. Los nombres de dominio `registry.bluemix.net` existentes están en desuso, pero puede continuar usándolos hasta el final de la fecha de fin de soporte. Todavía no hay una fecha de fin de soporte disponible. Para obtener más información, consulte [Regiones](/docs/services/Registry?topic=registry-registry_overview#registry_regions) e [Introducción a los nuevos nombres de dominio de IBM Cloud Container Registry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  Las firmas se aplican a todo el nombre de imagen, lo que incluye el nombre de dominio. Si utiliza la confianza de contenido, debe añadir nuevas firmas para poder consumir confianza de contenido bajo el nuevo nombre de dominio. Para obtener más información sobre la firma de imágenes, consulte [Firma de imágenes para contenido de confianza](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

<dl>
  <dt>Secretos de extracción de claves de API de IAM para clústeres de {{site.data.keyword.containerlong_notm}}</dt>
  <dd>Los nuevos secretos de extracción de imágenes de clúster para los dominios `icr.io` se autorizan mediante el uso de una clave de API de {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM). Por lo tanto, si desea un mayor control sobre el acceso a sus recursos de {{site.data.keyword.registrylong_notm}}, puede añadir más políticas de IAM. Por ejemplo, puede cambiar las políticas de claves de API del secreto de extracción del clúster para que las imágenes se extraigan únicamente de determinada región o de determinado espacio de nombres del registro.
  
  Para obtener más información, consulte [Visión general de cómo se autoriza al clúster a extraer imágenes de {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).</dd>
</dl>

<dl>
  <dt>Nueva región en ap-north</dt>
  <dd>Está disponible una nueva región en `ap-north`. Para utilizar la nueva región, use el nombre de dominio `jp.icr.io`.
  
  Para obtener más información, consulte [Regiones](/docs/services/Registry?topic=registry-registry_overview#registry_regions).</dd>
</dl>

## 21 de febrero de 2019
{: #21feb2019}

<dl>
  <dt>Automatización del acceso a los espacios de nombres</dt>
  <dd>El uso de señales para automatizar el envío por push y la extracción de imágenes de Docker a y desde los espacios de nombres está en desuso. Ahora debe utilizar claves de API para automatizar el acceso a sus espacios de nombres de {{site.data.keyword.registrylong_notm}} para poder enviar por push y extraer imágenes.

  Para obtener más información, consulte [Automatización del acceso a sus espacios de nombres mediante claves de API](/docs/services/Registry?topic=registry-registry_access#registry_api_key).</dd>
</dl>

## 8 de enero de 2019
{: #8jan2019}

 <dl>
  <dt>Fin del soporte de la API de Vulnerability Advisor versión 2</dt>
  <dd>La API de Vulnerability Advisor versión 2 ha quedado obsoleta y ya no se puede utilizar. Utilice la versión 3 de la API; consulte [API de Vulnerability Advisor para {{site.data.keyword.registrylong_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/container-registry/va).

  Para obtener más información, consulte [API de Vulnerability Advisor v2 en desuso ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/).</dd>
</dl>

## 4 de octubre de 2018
{: #4oct2018}

<dl>
  <dt>Gestión del acceso de usuarios</dt>
  <dd>Utilice {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) para controlar el acceso de los usuarios de su cuenta a {{site.data.keyword.registrylong_notm}}. Cuando las políticas de IAM están habilitadas para su cuenta en {{site.data.keyword.registrylong_notm}}, a cada usuario que acceda al servicio en su cuenta se le debe asignar una política de acceso con un rol de usuario de IAM definido. Esta política determina qué rol tiene el usuario dentro del contexto del servicio y qué acciones puede llevar a cabo el usuario.

  Para obtener más información, consulte [Gestión del acceso de usuario con {{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam), [Definición de políticas de rol de acceso de usuario](/docs/services/Registry?topic=registry-user#user) y [Guía de aprendizaje: Cómo otorgar acceso a los recursos de IBM Cloud Container Registry](/docs/services/Registry?topic=registry-iam_access#iam_access).</dd>
</dl>

## 7 de agosto de 2018
{: #7aug2018}

<dl>
  <dt>Políticas de exención disponibles en Vulnerability Advisor</dt>
  <dd>Si desea gestionar la seguridad de una organización de {{site.data.keyword.cloud_notm}}, puede utilizar el valor de política para determinar si un problema está exento o no. Puede utilizar Container Image Security Enforcement para asegurarse de que el despliegue solo se permita desde imágenes que no tengan problemas de seguridad después de justificar los problemas exentos por su política.

  Para obtener más información, consulte [Establecimiento de políticas de exención organizativas](/docs/services/Registry?topic=va-va_index#va_managing_policy).</dd>
</dl>

## 25 de julio de 2018
{: #25jul2018}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponible para Vulnerability Advisor</dt>
  <dd>Utilice el servicio {{site.data.keyword.cloudaccesstrailfull_notm}} para realizar el seguimiento de cómo interactúan los usuarios y las aplicaciones con el servicio {{site.data.keyword.registrylong_notm}} en {{site.data.keyword.cloud}}.

  Para obtener más información, consulte [Sucesos de Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>
  
## 12 de julio de 2018
{: #12jul2018}

<dl>
  <dt>API de Vulnerability Advisor versión 3</dt>
  <dd>La versión 3 de la API modifica el comportamiento de los puntos finales de API que se utilizan para obtener una lista de exenciones. Debe comprobar que el uso de la API no se basa en el comportamiento de la versión 2.

  Para obtener más información, consulte [Vulnerability Advisor para {{site.data.keyword.registrylong_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/container-registry/va).</dd>
</dl>

## 31 de mayo de 2018
{: #31may2018}

<dl>
  <dt>Uso de Helm para imágenes de Passport Advantage</dt>
  <dd>Importe software de {{site.data.keyword.IBM_notm}} que se descarga desde [IBM Passport Advantage Online para clientes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/software/passportadvantage/pao_customer.html) y que se empaqueta para utilizarlo con Helm en el espacio de nombres de {{site.data.keyword.registrylong_notm}}.

  Para obtener más información, consulte [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).</dd>
</dl>

## 21 de marzo de 2018
{: #21mar2018}

<dl>
  <dt>Container Scanner</dt>
  <dd>Container Scanner permite a Vulnerability Advisor informar sobre cualquier problema encontrado en contenedores en ejecución que no estén presentes en la imagen base del contenedor.

  Para obtener más información, consulte [Instalación de Container Scanner](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 16 de marzo de 2018
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement versión Beta</dt>
  <dd>Utilice Container Image Security Enforcement versión Beta para verificar las imágenes del contenedor antes de desplegarlas en el clúster en {{site.data.keyword.containerlong_notm}}. Puede controlar desde dónde se despliegan las imágenes, forzar políticas de Vulnerability Advisor y asegurarse de que el [contenido de confianza](/docs/services/Registry?topic=registry-registry_trustedcontent) esté aplicado correctamente a la imagen.

  Para obtener más información, consulte [Imposición de seguridad de la imagen de contenedor](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 20 de febrero de 2018
{: #20feb2018}

<dl>
  <dt>Contenido de confianza</dt>
  <dd>{{site.data.keyword.registrylong_notm}} proporciona tecnología de contenido de confianza para que pueda firmar imágenes para asegurar la integridad de las imágenes en el espacio de nombres de registro. Al extraer y enviar imágenes firmadas, puede verificar que las imágenes las ha enviado la parte correcta, como las herramientas de integración continua (CI).

  Para obtener más información, consulte [Firma de imágenes para contenido de confianza](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

## 6 de noviembre de 2017
{: #6nov2017}

<dl>
  <dt>Registro global</dt>
  <dd>Hay disponible un registro global. No tiene ninguna región incluida en su nombre de dominio (`icr.io`). Sólo las imágenes públicas que son proporcionadas por IBM están alojadas en este registro.

  Para obtener más información, consulte [Registro global](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).</dd>
</dl>

## 29 de septiembre de 2017
{: #29sep2017}

<dl>
  <dt>Creación de imágenes de Docker</dt>
  <dd>Está disponible el mandato `ibmcloud cr build` para ejecutar compilaciones de contenedores. Puede crear una imagen de Docker directamente en {{site.data.keyword.cloud_notm}} o crear su propia imagen de Docker en su sistema local y subirla (enviar por push) a su espacio de nombres en {{site.data.keyword.registrylong_notm}}.

  Para obtener más información, consulte [Creación de imágenes de Docker para utilizarlos con su espacio de nombres](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) e [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).</dd>
</dl>

## 24 de agosto de 2017
{: #24aug2017}

<dl>
  <dt>Interfaz gráfica de usuario publicada</dt>
  <dd>La interfaz gráfica de usuario de {{site.data.keyword.registrylong_notm}} está disponible en el catálogo; consulte [Container Registry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/kubernetes/catalog/registry).</dd>
</dl>

## 27 de junio de 2017
{: #27jun2017}

<dl>
  <dt>Disponibilidad general de {{site.data.keyword.registrylong_notm}}</dt>
  <dd>{{site.data.keyword.registrylong_notm}} está disponible a nivel general como servicio en {{site.data.keyword.cloud_notm}}. {{site.data.keyword.registrylong_notm}} da soporte a {{site.data.keyword.containerlong_notm}}.

  Para obtener más información sobre {{site.data.keyword.containerlong_notm}}, consulte la [Guía de aprendizaje de iniciación](/docs/containers?topic=containers-getting-started).</dd>
</dl>
