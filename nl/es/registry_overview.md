---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Acerca de {{site.data.keyword.registrylong_notm}}
{: #registry_overview}

Utilice {{site.data.keyword.registrylong}} para almacenar de forma segura y acceder a imágenes privadas de Docker en una arquitectura escalable y de alta disponibilidad.
{:shortdesc}

{{site.data.keyword.registrylong_notm}} proporciona un registro de imágenes privado multiarrendatario, escalable y de alta disponibilidad que IBM aloja y gestiona. Puede utilizar el registro privado configurando su propio espacio de nombres de imágenes y transmitir imágenes de Docker imágenes a su espacio de nombres.

<img src="images/registry_architecture1.svg" alt="Imagen que muestra cómo interactuar con IBM Cloud Container Registry. Container Registry contiene repositorios públicos y privados, y API para interactuar con el servicio. Su cliente Docker local puede extraer y enviar por push imágenes desde y hacia sus repositorios privados en el registro, y puede extraer repositorios públicos. La IU de la web de IBM Cloud (consola) interactúa con la API de Container Registry para listar imágenes. La CLI de Container Registry interactúa con la API para listar, crear, inspeccionar y eliminar imágenes, así como otras funciones administrativas. Su cliente Docker local también puede extraer y enviar por push imágenes desde su almacén de imágenes local a otros registros."/>

**Figura 1. Cómo interactúa {{site.data.keyword.registrylong_notm}} con sus imágenes Docker **

Una imagen de Docker es la base para todos los contenedores que cree. Una imagen se crea a partir de un Dockerfile, que es un archivo que contiene las instrucciones para crear la imagen. Un Dockerfile podría hacer referencia a los artefactos de compilación en sus instrucciones que se almacenan por separado, como por ejemplo una app, la configuración de la app y sus dependencias. Las imágenes se almacenan normalmente en un registro que puede ser accesible para el público (registro público) o configurado con acceso limitado para un pequeño grupo de usuarios (registro privado). Mediante {{site.data.keyword.registrylong_notm}}, sólo los usuarios con acceso a su cuenta de {{site.data.keyword.Bluemix_notm}} pueden acceder a sus imágenes.

Al enviar imágenes por push a {{site.data.keyword.registrylong_notm}}, se beneficia de las características integradas de Vulnerability Advisor, que realizan exploraciones en busca de posibles problemas de seguridad y vulnerabilidades. Vulnerability Advisor comprueba si hay paquetes vulnerables en determinadas imágenes básicas de Docker y vulnerabilidades conocidas en los valores de configuración de las apps. Cuando se encuentran vulnerabilidades, se proporciona información acerca de las mismas. Puede utilizar esta información para resolver problemas de seguridad, de forma que no se desplieguen contenedores a partir de imágenes vulnerables.

Revise la siguiente tabla para ver una visión general de las ventajas de utilizar {{site.data.keyword.registrylong_notm}}.

|Ventaja|Descripción|
|-------|-----------|
|Registro privado escalable y de alta disponibilidad|<ul><li>Configure su propio espacio de nombres de imágenes en un registro privado multiarrendatario, escalable y de alta disponibilidad alojado y gestionado por IBM.</li><li>Almacene de forma segura sus imágenes privadas de Docker y compártalas con usuarios en su cuenta de {{site.data.keyword.Bluemix_notm}}.</li></ul>|
|Conformidad con la seguridad de imágenes con Vulnerability Advisor|<ul><li>Benefíciese de la exploración automática de imágenes en el espacio de nombres.</li><li>Revise las recomendaciones específicas del sistema operativo para solucionar posibles vulnerabilidades y proteger la seguridad de los contenedores.</li></ul>|
|Límites de almacenamiento para almacenamiento y tráfico de extracción|<ul><li>Aproveche las ventajas del almacenamiento gratuito y del tráfico de extracción de sus imágenes privadas hasta alcanzar su cuota gratuita.</li><li>Configure límites de cuota personalizados para la cantidad de almacenamiento y tráfico de extracción mensual para no superar el nivel de pago elegido.</li></ul>|
{: caption="Tabla 1. Ventajas de {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Planes de servicio
{: #registry_plans}

Existe la posibilidad de elegir entre los planes de servicio de {{site.data.keyword.registrylong_notm}} estándar o gratuitos para almacenar las imágenes de Docker y hacer disponibles estas imágenes para los usuarios de su cuenta de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

El plan de servicio {{site.data.keyword.registrylong_notm}} determina la cantidad de almacenamiento y extrae el tráfico que puede utilizar para sus imágenes privadas. El servicio plan está asociado a su cuenta de {{site.data.keyword.Bluemix_notm}}, y los límites de almacenamiento y de tráfico de extracción de imágenes se aplican a todos los espacios de nombres que ha configurado en su cuenta.

La tabla siguiente muestra los planes de servicio {{site.data.keyword.registrylong_notm}} y sus características. Para obtener más información sobre cómo funciona la facturación y lo que sucede cuando se sobrepasan los límites de planes de servicio, consulte [Límites de cuota y facturación en {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).

|Características|Gratuito|Estándar|
|---------------|----|--------|
|Descripción|Pruebe el registro privado de {{site.data.keyword.registrylong_notm}} para almacenar y compartir de forma segura las imágenes de Docker. Este plan es el plan de servicio predeterminado cuando configura el primer espacio de nombres en {{site.data.keyword.registrylong_notm}}.|Saque partido del almacenamiento ilimitado y extraiga el uso de tráfico para gestionar las imágenes de Docker para todos los espacios de nombres en su cuenta de {{site.data.keyword.Bluemix_notm}}.|
|Cantidad de almacenamiento para las imágenes|500 MB|Ilimitado|
|Tráfico de extracción|5 GB por mes|Ilimitado|
|Facturación|Si supera los límites de almacenamiento o los límites de extracción de tráfico, no puede enviar por push ni extraer imágenes a y desde el espacio de nombres. Para obtener más información, consulte [Límites de cuota y facturación en {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).|<ul><li>Almacenamiento: Se le facturará por Gigabyte-mes de uso. Los primeros 0,5 GB-mes son gratuitos. Luego se le facturará como se indica en la calculadora de tarifas.</li><li>Tráfico de extracción: Se le facturará por Gigabyte uso mensual. Los primeros 5 GB son gratuitos. Luego se le facturará como se indica en la calculadora de tarifas. Si supera los límites de almacenamiento o los límites de extracción de tráfico, no puede enviar por push ni extraer imágenes a y desde el espacio de nombres. Para obtener más información acerca de almacenamiento, tráfico de extracción y el calculador de precios, consulte [Límites de cuota y facturación en {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).</li></ul>|
{: caption="Tabla 2. Planes de {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Límites de cuota y facturación
{: #registry_plan_billing}

Encontrará información y ejemplos sobre el funcionamiento del proceso de facturación y los límites de cuota en {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Cada imagen se crea a partir de un número de capas, cada una de las cuales representa un cambio incremental con respecto a la imagen base. Cuando transfiere o extrae una imagen, la cantidad de almacenamiento y de tráfico de extracción necesaria para cada capa se añade al uso mensual. Las capas idénticas se comparten automáticamente entre imágenes en la cuenta de {{site.data.keyword.Bluemix_notm}} y se reutilizan al crear otras imágenes. El almacenamiento correspondiente a cada capa idéntica se factura una sola vez, independientemente del número de imágenes de la cuenta que hagan referencia a la capa.

Ejemplo de transferencia de imágenes:

> Transfiere una imagen al espacio de nombres que se basa en la imagen Ubuntu. La imagen Ubuntu contiene varias capas. Puesto que aún no tiene estas capas en la cuenta, la cantidad de almacenamiento que necesitan dichas capas se añade a su uso mensual.
>
> Más tarde, crea una segunda imagen que se basa en la imagen Ubuntu. Cambia la imagen base Ubuntu, por ejemplo, añade mandatos o archivos al Dockerfile. Cada cambio representa una nueva capa de la imagen. Cuando transfiere la segunda imagen, {{site.data.keyword.registrylong_notm}} reconoce que todas las capas de la imagen Ubuntu base ya están almacenadas en la cuenta. No se le factura por almacenar dichas capas una segunda vez, aunque haya transferido la imagen a otro espacio de nombres. {{site.data.keyword.registrylong_notm}} determina el tamaño de todas las nuevas capas y añade la cantidad de almacenamiento al uso mensual.

### Facturación del almacenamiento y el tráfico de extracción
{: #registry_billing_traffic}

En función del plan de servicio que elija, se le facturará el almacenamiento y el tráfico de extracción que utilice al mes.
{:shortdesc}

**Almacenamiento: **

  Cada plan de servicio de {{site.data.keyword.registrylong_notm}} viene con una determinada cantidad de almacenamiento que puede utilizar para almacenar de forma segura las imágenes de Docker en los espacios de nombres de la cuenta de {{site.data.keyword.Bluemix_notm}}. Si tiene el plan estándar, se le facturará por GB-mes de uso. Los primeros 0,5 GB-mes son gratuitos. Si tiene el plan gratuito, pueda almacenar sus imágenes en {{site.data.keyword.registrylong_notm}} gratuitamente hasta alcanzar los límites de cuota del plan gratuito. Un GB-mes es un promedio de 1 GB de almacenamiento para un mes (730 horas).

  Ejemplo para el plan estándar:

  > Utiliza 5 GB para exactamente la mitad del mes y entonces envía por push varias imágenes a su espacio de nombres y utiliza 10 GB el resto del mes. El uso mensual se calcula del siguiente modo:
  >
  > (5 GB x 0,5 (meses)) + (10 GB x 0,5 (meses)) = 2,5 + 5 = 7,5 GB-mes
  >
  > En el plan estándar, los primeros 0,5 GB-mes son gratuitos, de modo que se le facturan 7 GB-mes (7,5 GB-mes - 0,5 GB-mes).

  

**Tráfico de extracción: **

  Cada plan de servicio de {{site.data.keyword.registrylong_notm}} incluye una determinada cantidad de tráfico de extracción gratuito de imágenes privadas almacenadas en el espacio de nombres. El tráfico de extracción es el ancho de banda que se utiliza para extraer una capa de una imagen del espacio de nombres en la máquina local. Si tiene el plan estándar, se le facturará por GB de uso al mes. Los 5 primeros GB son gratuitos. Si tiene el plan gratuito, puede extraer imágenes del espacio de nombres hasta alcanzar el límite de cuota del plan gratuito.

  Ejemplo para el plan estándar:

  > En el mes, ha extraído imágenes que contienen capas con un tamaño total de 14 GB. El uso mensual se calcula del siguiente modo:
  >
  > En el plan estándar, los 5 primeros GB al mes son gratuitos, por lo que se le facturan 9 GB (14 GB - 5 GB).

  

### Límites de almacenamiento para almacenamiento y tráfico de extracción
{: #registry_quota_limits}

En función del plan de servicio que elija, puede transferir imágenes al espacio de nombres y extraer imágenes del mismo hasta alcanzar los límites de cuota específicos del plan o personalizados.
{:shortdesc}

**Almacenamiento: **

  Cuando alcance o supere los límites de cuota de su plan, no puede transferir imágenes a los espacios de nombres de la cuenta de {{site.data.keyword.Bluemix_notm}} hasta que [libere espacio eliminando imágenes](registry_quota.html#registry_quota_freeup) de los espacios de nombres o [actualice al plan estándar](#registry_plan_upgrade). Si establece límites de cuota para el almacenamiento en el plan gratuito o estándar, también puede [aumentar este límite de cuota](registry_quota.html#registry_quota_set) para volver a permitir la transferencia de nuevas imágenes.

  Ejemplo para el plan estándar:

  > Su límite de cuota actual para el almacenamiento está establecido en 1 GB. Todas las imágenes privadas que se han almacenado en los espacios de nombres de su cuenta de {{site.data.keyword.Bluemix_notm}} ya utilizan 900 MB de este almacenamiento. Tiene 100 MB de almacenamiento disponible hasta alcanzar el límite de cuota. Un usuario desea transferir una imagen con un tamaño de 2 GB en la máquina local. Puesto que aún no se ha alcanzado el límite de cuota, {{site.data.keyword.registrylong_notm}} permite que el usuario transfiera esta imagen.
  >
  > Después de la transferencia, {{site.data.keyword.registrylong_notm}} determina el tamaño real de la imagen en el espacio de nombres, que puede variar con respecto al tamaño en la máquina local, y comprueba si se ha alcanzado el límite de almacenamiento. En este ejemplo, el uso de almacenamiento aumenta de 900 MB a 2 GB. Como el límite de cuota actual está establecido en 1 GB, {{site.data.keyword.registrylong_notm}} le impide transferir más imágenes al espacio de nombres.

**Tráfico de extracción: **

  Cuando alcanza o supera los límites de cuota del plan, no puede extraer imágenes de los espacios de nombres de la cuenta de {{site.data.keyword.Bluemix_notm}} hasta que comienza el siguiente periodo de facturación, [actualiza al plan estándar](#registry_plan_upgrade) o [aumenta los límites de cuota para el tráfico de extracción](registry_quota.html#registry_quota_set).

  Ejemplo para el plan estándar:

  > En el mes, el límite de cuota para el tráfico de extracción está establecido en 5 GB. Ya ha extraído imágenes de los espacios de nombres y ha utilizado
4,5 GB de este tráfico de extracción. Tiene 0,5 GB de tráfico de extracción disponible hasta alcanzar el límite de cuota. Un usuario desea extraer una imagen de 1 GB del espacio de nombres. Puesto que aún no se ha alcanzado el límite de cuota, {{site.data.keyword.registrylong_notm}} permite que el usuario extraiga esta imagen.
  >
  > Una vez extraída la imagen, {{site.data.keyword.registrylong_notm}} determina el ancho de banda que ha utilizado durante la extracción y comprueba si se ha alcanzado el límite del tráfico de extracción. En este ejemplo, el uso del tráfico de extracción ha aumentado de 4,5 GB a 5,5 GB. Como el límite de cuota actual está establecido en 5 GB, {{site.data.keyword.registrylong_notm}} le impide extraer imágenes del espacio de nombres.

### Estimación de costes
{: #registry_estimating_costs}

Utilice la calculadora de tarifas de {{site.data.keyword.Bluemix_notm}} para estimar el coste de su plan.
{:shortdesc}

Puede establecer el precio de su app utilizando las calculadores de coste proporcionadas por {{site.data.keyword.Bluemix_notm}}.

1.  Abra la hoja de precios. Consulte Tarifas de [{{site.data.keyword.Bluemix_notm}}](https://www.ibm.com/cloud-computing/bluemix/pricing).
2.  En la sección **Pago según uso**, pulse **Calcule sus costes con nuestra calculadora**. Se abre la calculadora.
3.  Desplácese hasta la sección **Container Registry** dentro de **Cargos por contenedor**.
4.  Escriba las estimaciones de almacenamiento y de tráfico en los campos proporcionados.

Los costes estimados se muestran en la calculadora.

## Actualización del plan de servicio
{: #registry_plan_upgrade}

Puede actualizar su plan de servicio para beneficiarse de un almacenamiento ilimitado y uso de tráfico de extracción para gestionar las imágenes de Docker para todos los espacios de nombres en su cuenta de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Si desea conocer el plan de servicio que tiene, ejecute el mandato `ibmcloud cr plan`.

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

    Si tiene un ID federado, utilice `ibmcloud login --sso` para iniciar sesión en la CLI de {{site.data.keyword.Bluemix_notm}}. Especifique el nombre de usuario y utilice el URL proporcionado en su salida de CLI para recuperar el código de acceso de un solo uso. Sabe tiene un ID federado cuando el inicio de sesión falla sin el `--sso` y se lleva a cabo correctamente con la opción `--sso`.
    {:tip}

2.  Actualice al plan estándar.

    ```
    ibmcloud cr plan-upgrade standard
    ```
    {: pre}

    Si tiene una cuenta Lite de {{site.data.keyword.Bluemix_notm}}, debe actualizar una cuenta de pago por uso o de suscripción de {{site.data.keyword.Bluemix_notm}} para poder ejecutar `ibmcloud cr plan-upgrade`.
    {:tip}


## Conceptos básicos
{: #registry_planning}

Prepárese para almacenar y compartir de forma segura sus imágenes de Docker con {{site.data.keyword.registrylong_notm}} aprendiendo los conceptos básicos del registro.
{:shortdesc}

No coloque información personal en las imágenes de contenedor, nombres de espacio de nombres, campos de descripción (por ejemplo, en señales de registro), o en cualesquiera datos de configuración de imágenes (por ejemplo, nombres de imágenes o etiquetas de imagen).
{:tip}


### Visión general de los términos utilizados en {{site.data.keyword.registrylong_notm}}
{: #terms}

<dl>
  <dt>Dockerfile</dt>
  <dd>Un Dockerfile es un archivo de texto que contiene instrucciones sobre cómo crear una imagen de Docker. Típicamente, una imagen se crea sobre una imagen base que contiene un sistema operativo base, como Ubuntu. Puede cambiar esta imagen base incrementalmente con las instrucciones del Dockerfile para definir el entorno en que la app necesita ejecutarse. Cada cambio de la imagen base describe una nueva capa de la imagen, y puede realizar varios cambios en una sola línea de Dockerfile. Las instrucciones de un Dockerfile también podrían hacer referencia a los artefactos de compilación que se almacenan por separado, como por ejemplo una app, la configuración de la app y sus dependencias.</dd>
</dl>

<dl>
  <dt>Image</dt>
  <dd>Sistema de archivos y sus parámetros de ejecución que se utilizan dentro de un tiempo de ejecución de contenedor para crear un contenedor. El sistema de archivos consta de una serie de capas, combinadas en tiempo de ejecución, que se crean a medida que la imagen se construye mediante actualizaciones sucesivas. La imagen no conserva el estado cuando se ejecuta el contenedor.</dd>
</dl>

<dl>
  <dt>Espacio de nombres</dt>
  <dd>Los espacios de nombres son una forma de organizar los repositorios de sus imágenes dentro de {{site.data.keyword.registrylong_notm}}. El espacio de nombres está asociado a su cuenta de {{site.data.keyword.Bluemix_notm}}. Cuando se configura el propio espacio de nombres en {{site.data.keyword.registrylong_notm}}, el espacio de nombres se añade al URL de registro como se indica a continuación: <code>registry.<em>&lt;region&gt;</em>.bluemix.net/mi_espaciodenombres</code>.

  Cada usuario de la cuenta de {{site.data.keyword.Bluemix_notm}} podrá ver y trabajar con imágenes que se han almacenado en su espacio de nombres de registro. Puede configurar varios espacios de nombres, por ejemplo, para tener diferentes repositorios para los entornos de producción y de transferencia.</dd>
</dl>

<dl>
  <dt>Imágenes de contenedor OCI</dt>
  <dd>Las imágenes de contenedor que son compatibles con la [Especificación de formato de imágenes de OCI ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/opencontainers/image-spec).</dd>
</dl>

<dl>
  <dt>Registro</dt>
  <dd>Un registro es un servicio que proporciona almacenamiento para imágenes OCI (también conocidas como imágenes Docker). Los clientes de OCI que utilizan el nombre de dominio de registro apropiado pueden acceder a las imágenes OCI o "extraerlas". Las imágenes pueden ser accedidas por cualquier persona (imágenes públicas) o el acceso puede estar limitado a un grupo (imágenes privadas). {{site.data.keyword.registrylong_notm}} proporciona un registro de imágenes privado, multiarrendatario y de alta disponibilidad que {{site.data.keyword.IBM_notm}} aloja y gestiona. Puede utilizar el registro añadiendo un espacio de nombres privado a su cuenta y luego enviar por push imágenes a su espacio de nombres.</dd>
</dl>

<dl>
  <dt>Repositorio</dt>
  <dd>Un repositorio de imágenes es un conjunto de imágenes etiquetadas relacionadas en el registro. Repositorio se utiliza a menudo de forma intercambiable con imagen, pero potencialmente un repositorio contiene varias variantes etiquetadas de una imagen.</dd>
</dl>

<dl>
  <dt>Etiqueta</dt>
  <dd>Una etiqueta es un identificador de una imagen dentro de un repositorio. Puede utilizar etiquetas para distinguir entre distintas versiones de la misma imagen base dentro de un repositorio. Cuando ejecuta un mandato de Docker y no especifica la etiqueta de una imagen del repositorio, se utilizará de forma predeterminada la imagen con la etiqueta <code>latest</code>.</dd>
</dl>


Para obtener más información sobre los términos específicos de Docker, [consulte el glosario de Docker ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.docker.com/glossary/).


### Planificación de espacios de nombres
{: #registry_namespaces}

{{site.data.keyword.registrylong_notm}} proporciona un registro de imágenes privado multiarrendatario que IBM aloja y gestiona. Puede almacenar y compartir de forma segura y las imágenes de Docker en este registro estableciendo un espacio de nombres del registro.
{:shortdesc}

Puede configurar varios espacios de nombres, por ejemplo, para tener diferentes repositorios para los entornos de producción y de transferencia. Si desea utilizar el registro en varias regiones de {{site.data.keyword.Bluemix_notm}}, debe configurar un espacio de nombres para cada región. Los espacios de nombres son exclusivos dentro de las regiones. Puede utilizar el mismo espacio de nombres para cada región, a menos que otra persona ya tenga un espacio de nombres con ese nombre configurado en esa región.

Para trabajar sólo con imágenes públicas proporcionadas por IBM, no tiene que volver a configurar un espacio de nombres.

Si no está seguro de si ya se ha establecido un espacio de nombres para su cuenta, ejecute el mandato `ibmcloud cr namespace-list` para recuperar la información de espacio de nombres existente.
{:tip}

Considere las reglas siguientes al elegir un espacio de nombres:

-   Su espacio de nombres debe ser exclusivo en una región de {{site.data.keyword.Bluemix_notm}}.
-   Su espacio de nombres debe tener entre 4 y 30 caracteres.
-   El espacio de nombres debe empezar por al menos una letra o un número.
-   Su espacio de nombres debe contener letras minúsculas, números, o subrayados (_) sólo.

No coloque información personal en los nombres del espacio de nombres.
{:tip}

Después de establecer su primer espacio de nombres, se le asigna el plan de servicio gratuito de {{site.data.keyword.registrylong_notm}} si todavía no ha [actualizado su plan](#registry_plan_upgrade).

## Regiones
{: #registry_regions}

Los registros de {{site.data.keyword.registrylong_notm}} están disponibles en varias regiones.
{:shortdesc}

### Regiones locales
{: #registry_regions_local}

Una región es un área geográfica a la que se accede mediante un punto final dedicado. Los registros de {{site.data.keyword.registrylong_notm}} están disponibles en las siguientes regiones:

-   ap-south: `registry.au-syd.bluemix.net`
-   eu-central: `registry.eu-de.bluemix.net`
-   uk-south: `registry.eu-gb.bluemix.net`
-   us-south: `registry.ng.bluemix.net`

Todos los artefactos de registro abarcan el registro regional específico con el que está trabajando actualmente. Por ejemplo, espacios de nombres, imágenes, señales, valores de cuota y valores de plan deben ser gestionados independientemente para cada registro regional.

Si desea utilizar una región diferente a su región local, puede acceder a la región que desea, si ejecuta el mandato `ibmcloud cr region-set`. Puede ejecutar el mandato sin parámetros para obtener una lista de regiones disponibles, o puede especificar la región como un parámetro.

Para ejecutar el mandato con parámetros, substituya _&lt;region&gt;_ con el nombre de la región, por ejemplo, `eu-central`.

```
ibmcloud cr region-set <region>
```
{: pre}

Por ejemplo, para acceder a la región de UE central, ejecute el mandato siguiente:

```
ibmcloud cr region-set eu-central
```
{: pre}

Después de elegir una región distinta, inicie sesión en el registro de nuevo: `ibmcloud cr login`.

### Registro global
{: #registry_regions_global}

Hay disponible un registro global, que no tiene ninguna región incluida en su nombre (`registry.bluemix.net`). En este registro se alojan únicamente las imágenes públicas proporcionadas por IBM. Para gestionar sus propias imágenes como por ejemplo estableciendo espacios de nombres o etiquetando y enviando imágenes a un registro, utilice un [registro regional local](#registry_regions_local).
{:shortdesc}

Puede acceder al registro global ejecutando el mandato `ibmcloud cr region-set`.

Por ejemplo, para acceder al registro global, ejecute el mandato siguiente:

```
ibmcloud cr region-set global
```
{: pre}

Para obtener más información acerca del mandato `ibmcloud cr region-set`, consulte [{{site.data.keyword.registrylong_notm}} CLI](registry_cli.html#bx_cr_region_set).

Después de haber accedido al registro global, ejecute el mandato `ibmcloud cr login` para registrar su daemon Docker local en el registro global para que pueda extraer imágenes públicas proporcionadas por {{site.data.keyword.IBM_notm}}.
