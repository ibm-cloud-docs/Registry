---



copyright:
  years: 2017, 2018
lastupdated: "2018-05-31"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI es un plugin que permite gestionar su registro y sus recursos de su cuenta de {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

**Requisitos previos**
* Antes de ejecutar mandatos de registro, inicie una sesión en {{site.data.keyword.Bluemix_notm}}
 con el mandato `bx login` para generar una señal de acceso y autenticar la sesión.

Para obtener más información sobre cómo utilizar la {{site.data.keyword.registrylong_notm}} CLI, consulte [Iniciación a {{site.data.keyword.registrylong_notm}}](index.html).

**Nota**: No coloque información personal en las imágenes de contenedor, nombres de espacio de nombres, campos de descripción (por ejemplo, en señales de registro), o en cualesquiera datos de configuración de imágenes (por ejemplo, nombres de imágenes o etiquetas de imagen).


<table summary="Gestionar {{site.data.keyword.registrylong_notm}}">
<caption>Tabla 1. Mandatos para gestionar {{site.data.keyword.registrylong_notm}}
</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar el registro</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr build](#bx_cr_build)</td>
 <td>[bx cr info](#bx_cr_info)</td>
 <td>[bx cr image-inspect](#bx_cr_image_inspect)</td>
 <td>[bx cr image-list (bx cr images)](#bx_cr_image_list)</td>
 </tr>
 <tr>
 <td>[bx cr image-rm](#bx_cr_image_rm)</td>
 <td>[bx cr login](#bx_cr_login)</td>
 <td>[bx cr namespace-add](#bx_cr_namespace_add)</td>
 <td>[bx cr namespace-list (bx cr namespaces)](#bx_cr_namespace_list)</td>
 <td>[bx cr namespace-rm](#bx_cr_namespace_rm)</td>
 </tr>
 <tr>
 <td>[bx cr plan](#bx_cr_plan)</td>
 <td>[bx cr plan-upgrade](#bx_cr_plan_upgrade)</td>
 <td>[bx cr ppa-archive-load](#bx_cr_ppa_archive_load)</td>
 <td>[bx cr quota](#bx_cr_quota)</td>
 <td>[bx cr quota-set](#bx_cr_quota_set)</td>
 </tr>
 <tr>
 <td>[bx cr region](#bx_cr_region)</td>
 <td>[bx cr region-set](#bx_cr_region_set)</td>
 <td>[bx cr token-add](#bx_cr_token_add)</td>
 <td>[bx cr token-get](#bx_cr_token_get)</td>
 <td>[bx cr token-list (bx cr tokens)](#bx_cr_token_list)</td>
 </tr><tr>
 <td>[bx cr token-rm](#bx_cr_token_rm)</td>
 <td>[bx cr vulnerability-assessment (bx cr va)](#bx_cr_va)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

Devuelve los detalles sobre el punto final de la API de registro sobre el que se ejecutan los mandatos.

```
bx cr api
```
{: codeblock}


## bx cr build
{: #bx_cr_build}

Crea una imagen de Docker en {{site.data.keyword.registrylong_notm}}.

```
bx cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Parámetros**
<dl>
<dt>DIRECTORY</dt>
<dd>La ubicación de su contexto de construcción, que contiene los archivos Dockerfile y de requisito previo.</dd>
<dt>--no-cache</dt>
<dd>(Opcional) Si se especifica, las capas de imágenes almacenadas en memoria caché de compilaciones anteriores no se utilizan en esta compilación.</dd>
<dt>--pull</dt>
<dd>(Opcional) Si se especifica, las imágenes base se extraerán aunque ya exista una imagen con una etiqueta coincidente en el host de compilación.</dd>
<dt>--quiet, -q</dt>
<dd>(Opcional) Si se especifica, la salida de compilación se suprimirá a menos que se produzca un error.</dd>
<dt> --build-arg KEY=VALUE</dt>
<dd>(Opcional) Especifica un argumento de compilación adicional en el formato 'KEY=VALUE'. Se pueden especificar varios argumentos de compilación incluyendo este parámetro varias veces. El valor de cada argumento de compilación está disponible como una variable de entorno cuando especifica una línea ARG que coincide con la clave del archivo Docker.</dd>
<dt>--file FILE, -f FILE</dt>
<dd>(Opcional) Si utiliza los mismos archivos para varias compilaciones, puede elegir una vía de acceso hasta un Dockerfile diferente. Especifique la ubicación del Dockerfile relativo al contexto de compilación. Si no se especifica, el valor predeterminado es `PATH/Dockerfile`, donde PATH es la raíz del contexto de compilación.</dd>
<dt>--tag TAG, -t TAG</dt>
<dd>El nombre completo de la imagen que desea compilar, que incluye el espacio de nombres y el URL de registro.</dd>
</dl>


## bx cr info
{: #bx_cr_info}

Visualiza el nombre y la cuenta del registro en el que ha iniciado una sesión.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
{: #bx_cr_image_inspect}

Visualiza detalles sobre una imagen específica.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Parámetros**
<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go.

Para obtener más información, consulte [Formateo y filtrado de la salida de la CLI para mandatos de {{site.data.keyword.registrylong_notm}}](registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>IMAGE</dt>
<dd>El nombre de la imagen de la que desea obtener un informe. Puede examinar varias imágenes creando una lista de cada imagen en el mandato con un espacio entre cada nombre.

<p>Para encontrar los nombres de sus imágenes, ejecute `bx cr image-list`. Combine el contenido de las columnas Repositorio y Etiqueta para crear el nombre de imagen en el formato `repository:tag`. Si no se especifica ninguna etiqueta en el nombre de la imagen, se examina la imagen etiquetada como `latest`. </p>

</dd>
</dl>


## bx cr image-list (bx cr images)
{: #bx_cr_image_list}

Visualiza todas las imágenes de su cuenta de {{site.data.keyword.Bluemix_notm}}.

<p>**Nota:** el nombre de imagen es la combinación del contenido de las columnas Repositorio y Etiqueta en el formato `repository:tag`. </p>

```
 bx cr image-list [--no-trunc] [--format FORMAT] [-q, --quiet] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Parámetros**
<dl>
<dt>--no-trunc</dt>
<dd>(Opcional) No truncar los resúmenes de imagen.</dd>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go.

Para obtener más información, consulte [Formateo y filtrado de la salida de la CLI para mandatos de {{site.data.keyword.registrylong_notm}}](registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Cada imagen se lista en el formato: `repository:tag`</dd>
<dt>--restrict RESTRICTION</dt>
<dd>(Opcional) Limitar la salida para visualizar solo imágenes en el espacio de nombres y repositorio o el espacio de nombres especificado. </dd>
<dt>--include-ibm</dt>
<dd>(Opcional) Incluye en la salida las imágenes públicas proporcionadas por {{site.data.keyword.IBM_notm}}. Sin esta opción, de forma predeterminada solo se muestran en la lista las imágenes privadas.</dd>
</dl>



## bx cr image-rm
{: #bx_cr_image_rm}

Suprime de su registro una o varias de las imágenes especificadas.

```
bx cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Parámetros**
<dl>
<dt>IMAGE</dt>
<dd>El nombre de la imagen de la que desea obtener un informe. Puede suprimir varias imágenes al mismo tiempo creando una lista de cada imagen en el mandato con un espacio entre cada nombre.

<p>Para encontrar los nombres de sus imágenes, ejecute `bx cr image-list`. Combine el contenido de las columnas Repositorio y Etiqueta para crear el nombre de imagen en el formato `repository:tag`. Si no se especifica una etiqueta en el nombre de la imagen, la imagen etiquetada como `latest` se suprime de forma predeterminada.</p>

</dd>
</dl>


## bx cr login
{: #bx_cr_login}

Este mandato ejecuta el mandato `docker login` sobre el registro. Se necesita el mandato `docker login` para poder ejecutar los mandatos `docker push` o `docker pull` para el registro. Este mandato no es necesario para ejecutar otros mandatos `bx cr`. Si Docker no está instalado, este mandato devuelve un mensaje de error.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
{: #bx_cr_namespace_add}

Añade un espacio de nombres a su cuenta {{site.data.keyword.Bluemix_notm}}.

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parámetros**
<dl>
<dt>NAMESPACE</dt>
<dd>El espacio de nombres que desea añadir. El espacio de nombres debe ser exclusivo entre todas las cuentas de {{site.data.keyword.Bluemix_notm}} en la misma región.
  
<p>  
<strong>Nota</strong>: No coloque información personal en los nombres del espacio de nombres.
</p>
  
</dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
{: #bx_cr_namespace_list}

Visualiza todos los espacios de nombres cuyo propietario es su cuenta de {{site.data.keyword.Bluemix_notm}}.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
{: #bx_cr_namespace_rm}

Elimina un espacio de nombres de su cuenta de {{site.data.keyword.Bluemix_notm}}. Las imágenes en este espacio de nombres se suprimen cuando se elimina el espacio de nombres.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parámetros**
<dl>
<dt>NAMESPACE</dt>
<dd>El espacio de nombres que desea eliminar.</dd>
</dl>


## bx cr plan
{: #bx_cr_plan}

Visualiza su plan de precios.

```
bx cr plan
```
{: codeblock}


## bx cr plan-upgrade
{: #bx_cr_plan_upgrade}

Actualiza al plan estándar.

Para obtener más información sobre los planes, consulte [Planes de registro](registry_overview.html#registry_plans).

```
bx cr plan-upgrade [PLAN]
```
{: codeblock}

**Parámetros**
<dl>
<dt>PLAN</dt>
<dd>El nombre del plan de precios al que desea actualizar. Si no se especifica PLAN, el valor predeterminado será `standard`.</dd>
</dl>


## bx cr ppa-archive-load
{: #bx_cr_ppa_archive_load}

Las importaciones de software de IBM que se descargan desde [IBM Passport Advantage ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www-01.ibm.com/software/passportadvantage/pao_customer.html) y que se empaquetan para utilizarlas con Helm en el espacio de nombres de registro privado.

Las imágenes de contenedor se envían al espacio de nombres privado de {{site.data.keyword.registryshort_notm}}. Las gráficas de Helm se graban en un directorio `ppa-import` que se crea en el directorio desde el que ejecuta el mandato. Opcionalmente, puede utilizar el [proyecto de código abierto de Chart Museum ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) para alojar gráficas de helm.

**Mandato de ejemplo**:
```
bx cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Parámetros**:
<dl>
  <dt>--archive FILE</dt>
  <dd>La vía de acceso al archivo comprimido que se descarga desde IBM Passport Advantage.</dd>
  <dt>--namespace NAMESPACE</dt>
  <dd>Uno de sus espacios de nombres. Las imágenes de contenedor del archivo comprimido se envían a este espacio de nombres. Para listar los espacios de nombres, ejecute `bx cr namespace-list`.</dd>
  <dt>--chartmuseum-uri URI</dt>
  <dd>(Opcional) El identificador de recursos exclusivo de [Chart Museum ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>--chartmuseum-user USER</dt>
  <dd>(Opcional) El nombre de usuario de [Chart Museum ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>--chartmuseum-password PASSWORD</dt>
  <dd>(Opcional) La contraseña de [Chart Museum ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
</dl>


## bx cr quota
{: #bx_cr_quota}

Visualiza sus cuotas actuales de tráfico y almacenamiento, así como información de utilización relacionada con las mismas.

```
bx cr quota
```
{: codeblock}


## bx cr quota-set
{: #bx_cr_quota_set}

Modifica la cuota especificada.

```
bx cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Parámetros**
<dl>
<dt>--traffic TRAFFIC</dt>
<dd>(Opcional) Cambia su cuota de tráfico al valor que especifique en megabytes. La operación falla si no está autorizado a establecer cuotas de tráfico, o si establece un valor por encima del que permite su plan de precios actual.</dd>
<dt>--storage STORAGE</dt>
<dd>(Opcional) Cambia su cuota de almacenamiento al valor que especifique en megabytes. La operación falla si no está autorizado a establecer cuotas de almacenamiento, o si establece un valor por encima del que permite su plan de precios actual.</dd>
</dl>


## bx cr region
{: #bx_cr_region}

Visualiza la región de destino y el registro.

```
bx cr region
```
{: codeblock}

Para obtener más información, consulte [Regiones](registry_overview.html#registry_regions).


## bx cr region-set
{: #bx_cr_region_set}

Establezca una región de destino para los mandatos de {{site.data.keyword.registrylong_notm}}. Para enumerar las regiones disponibles, ejecute el mandato sin parámetros.

```
bx cr region-set [REGION]
```
{: codeblock}

**Parámetros**
<dl>
<dt>REGION</dt>
<dd>(Opcional) El nombre de su región de destino, por ejemplo, `us-south`.

Para obtener más información, consulte [Regiones](registry_overview.html#registry_regions).

</dd>
</dl>


## bx cr token-add
{: #bx_cr_token_add}

Añade una señal que sirve para controlar el acceso a un registro.

```
bx cr token-add [--description DESCRIPTION] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**Parámetros**
<dl>
<dt>--description DESCRIPTION</dt>
<dd>(Opcional) Especifica el valor como una descripción para la señal, que se visualiza al ejecutar `bx cr token-list`. Si la señal la crea automáticamente {{site.data.keyword.containerlong_notm}}, la descripción se establecerá en el nombre de clúster de Kubernetes. En este caso, la señal se elimina de forma automática al eliminar su clúster.
  
<p> 
  <strong>Nota</strong>: No coloque información personal en la descripción de la señal.
</p>

  </dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Visualiza únicamente la señal, sin ningún texto a su alrededor.</dd>
<dt>--non-expiring</dt>
<dd>(Opcional) Crea una señal con un acceso que no caduca. Si no se establece este parámetro, de forma predeterminada el acceso con la señal caduca después de 24 horas.</dd>
<dt>--readwrite</dt>
<dd>(Opcional) Crea una señal que otorga acceso de lectura y escritura. Sin esta opción, de forma predeterminada el acceso es de solo lectura.</dd>
</dl>


## bx cr token-get
{: #bx_cr_token_get}

Recupera la señal especificada desde el registro.

```
bx cr token-get TOKEN
```

{: codeblock}

**Parámetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) Identificador exclusivo de la señal que desea recuperar.</dd>
</dl>


## bx cr token-list (bx cr tokens)
{: #bx_cr_token_list}

Visualiza todas las señales que existen para su cuenta de {{site.data.keyword.Bluemix_notm}}.

```
bx cr token-list --format FORMAT
```
{: codeblock}

**Parámetros**
<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go.

Para obtener más información, consulte [Formateo y filtrado de la salida de la CLI para mandatos de {{site.data.keyword.registrylong_notm}}](registry_cli_reference.html#registry_cli_listing).

</dd>
</dl>


## bx cr token-rm
{: #bx_cr_token_rm}

Elimina una o varias de las señales especificadas.

```
bx cr token-rm TOKEN [TOKEN...]
```
{: codeblock}

**Parámetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) TOKEN puede ser la propia señal, o el identificador exclusivo de la señal, tal como se muestra en `bx cr token-list`. Es posible especificar varias señales separándolas con espacios en blanco.</dd>
</dl>


## bx cr vulnerability-assessment (bx cr va)
{: #bx_cr_va}

Visualiza un informe de valoración de vulnerabilidad para sus imágenes.

```
bx cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Parámetros**
<dl>
<dt>IMAGE</dt>
<dd>El nombre de la imagen de la que desea obtener un informe. El informe indica si la imagen tiene vulnerabilidades de empaquetamiento conocidas. Puede solicitar informes para varias imágenes al mismo tiempo creando una lista de cada imagen en el mandato con un espacio entre cada nombre.

<p>Para encontrar los nombres de sus imágenes, ejecute `bx cr image-list`. Combine el contenido de las columnas Repositorio y Etiqueta para crear el nombre de imagen en el formato `repository:tag`. Si no se especifica una etiqueta en el nombre de la imagen, el informe evalúa la imagen que está etiquetada como `latest`. </p>

<p>Se admiten los siguientes sistemas operativos:

<ul>

<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>

</p>

Para obtener más información, consulte [Gestión de imágenes de seguridad con Vulnerability Advisor](../va/va_index.html).

</dd>
<dt>--output FORMAT, -o FORMAT</dt>
<dd>(Opcional) La salida del mandato se devuelve en el formato elegido. El formato predeterminado es `text`. Se admiten los formatos siguientes:

<ul>

<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
<dt>--vulnerabilities, -v</dt>
<dd>(Opcional) La salida del mandato se restringe para mostrar solo vulnerabilidades.</dd>
<dt>--configuration-issues, -c</dt>
<dd>(Opcional) La salida del mandato se restringe para mostrar solo problemas de configuración.</dd>
<dt>--extended, -e </dt>
<dd>(Opcional) La salida del mandato muestra información adicional sobre arreglos para paquetes vulnerables.</dd>

</dl>
