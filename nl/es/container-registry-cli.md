---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

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

# CLI de {{site.data.keyword.registrylong_notm}}
{: #containerregcli}

La CLI de {{site.data.keyword.registrylong}}, que se proporciona en el plugin de CLI `container-registry`, sirve para gestionar su registro y sus recursos para su cuenta de {{site.data.keyword.cloud_notm}}.
{: shortdesc}

**Requisitos previos**

* Instale la CLI de {{site.data.keyword.cloud_notm}}; consulte [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started). El prefijo para ejecutar mandatos mediante la CLI de {{site.data.keyword.cloud_notm}} es `ibmcloud`.
* Antes de ejecutar los mandatos de registro, inicie sesión en {{site.data.keyword.cloud_notm}} con el mandato `ibmcloud login` para generar una señal de acceso y autenticar la sesión.

En la línea de mandatos, se le notifica cuando hay actualizaciones de la CLI de `ibmcloud` y de los plugins de CLI `container-registry` disponibles. Asegúrese de mantener la CLI actualizada para poder utilizar todos los mandatos y distintivos disponibles.

Si desea ver la versión actual del plugin de CLI `container-registry`, ejecute `ibmcloud plugin list`.

Para obtener más información sobre cómo utilizar la CLI de {{site.data.keyword.registrylong_notm}}, consulte [Iniciación a {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started).

Para obtener más información sobre la plataforma IAM y los roles de acceso al servicio necesarios para algunos mandatos, consulte [Gestión del acceso de usuario con Identity and Access Management](/docs/services/Registry?topic=registry-iam#iam).

No coloque información personal en las imágenes de contenedor, nombres de espacio de nombres, campos de descripción, o en cualesquiera datos de configuración de imágenes (por ejemplo, nombres de imágenes o etiquetas de imagen).
{: important}

## `ibmcloud cr api`
{: #bx_cr_api}

Devuelve los detalles sobre el punto final de la API de registro sobre el que se ejecutan los mandatos.

```
ibmcloud cr api
```
{: codeblock}

**Requisitos previos**

Ninguno

## `ibmcloud cr build`
{: #bx_cr_build}

Crea una imagen de Docker en {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
<dt>`DIRECTORY`</dt>
<dd>La ubicación de su contexto de construcción, que contiene los archivos Dockerfile y de requisito previo. Si ejecuta el mandato cuando el directorio de trabajo está establecido en el lugar en el que está almacenado el contexto de compilación, puede sustituir `DIRECTORY` por un punto (.).</dd>
<dt>`--no-cache`</dt>
<dd>(Opcional) Si se especifica, las capas de imágenes almacenadas en memoria caché de compilaciones anteriores no se utilizan en esta compilación.</dd>
<dt>`--pull`</dt>
<dd>(Opcional) Si se especifica, las imágenes base se extraerán aunque ya exista una imagen con una etiqueta coincidente en el host de compilación.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Opcional) Si se especifica, la salida de compilación se suprimirá a menos que se produzca un error.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(Opcional) Especifica un argumento de compilación adicional en el formato `'KEY=VALUE'`. Se pueden especificar varios argumentos de compilación incluyendo este parámetro varias veces. El valor de cada argumento de compilación está disponible como una variable de entorno cuando especifica una línea ARG que coincide con la clave del archivo Docker.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(Opcional) Si utiliza los mismos archivos para varias compilaciones, puede elegir una vía de acceso hasta un Dockerfile diferente. Especifique la ubicación del Dockerfile relativo al contexto de compilación. Si no se especifica, el valor predeterminado es `PATH/Dockerfile`, donde PATH es la raíz del contexto de compilación.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>El nombre completo de la imagen que desea compilar, que incluye el espacio de nombres y el URL de registro.</dd>
</dl>

**Ejemplo**

Crea una imagen de Docker que no utiliza una memoria caché de compilación, en la que la salida de compilación está suprimida, la etiqueta es *`us.icr.io/birds/bluebird:1`* y el directorio es su directorio de trabajo.

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Crea una exención para un problema de seguridad. Puede crear una exención para un problema de seguridad que se aplique a varios ámbitos. El ámbito puede ser una cuenta, un espacio de nombres, un repositorio o una etiqueta.

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opciones del mandato**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Para establecer su cuenta como ámbito, utilice el valor `"*"`. Para establecer un espacio de nombres, un repositorio o una etiqueta como ámbito, especifique el valor en uno de los siguientes formatos: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>El tipo del problema de seguridad que desea eximir. Ejecute `ibmcloud cr exemption-types` para averiguar los tipos de problema válidos.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>El ID del problema de seguridad que desea eximir. Para localizar un ID de problema, ejecute `ibmcloud cr va <image>`, donde `<image>` es el nombre de la imagen, o utilice el valor relevante de la columna **ID de vulnerabilidad** o **ID de problema de configuración**.
</dd>
</dl>

**Ejemplos**

Crea una exención para CVE con el ID `CVE-2018-17929` para todas las imágenes del repositorio `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Crea una exención de CVE de toda la cuenta para el CVE con el ID `CVE-2018-17929`.

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Crea una exención de problema de configuración para el problema `application_configuration:nginx.ssl_protocols` para una sola imagen con la etiqueta `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

Enumerar las exenciones para los problemas de seguridad.

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opciones del mandato**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(Opcional) Únicamente muestra una lista de las exenciones que se aplican a este ámbito. Para establecer un espacio de nombres, un repositorio o una etiqueta como ámbito, especifique el valor en uno de los siguientes formatos: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
</dl>

**Ejemplo**

Enumera todas las exenciones para los problemas de seguridad que se aplican a las imágenes del repositorio *`birds/bluebird`*. La salida incluye las exenciones que son de toda la cuenta, las exenciones que están limitadas al espacio de nombres *`birds`* y las exenciones que están limitadas al repositorio *`birds/bluebird`*, pero no las que están limitadas a etiquetas específicas dentro del repositorio *`birds/bluebird`*.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Suprime una exención para un problema de seguridad. Para ver una lista de las exenciones existentes, ejecute `ibmcloud cr exemption-list`.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opciones del mandato**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Para establecer su cuenta como ámbito, utilice el valor `"*"`. Para establecer un espacio de nombres, un repositorio o una etiqueta como ámbito, especifique el valor en uno de los siguientes formatos: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Tipo de problema de la exención para el problema de seguridad que desea eliminar. Para encontrar los tipos de problema para sus exenciones, ejecute `ibmcloud cr exemption-list`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>ID de la exención para el problema de seguridad que desea eliminar. Para encontrar los ID para sus exenciones, ejecute `ibmcloud cr exemption-list`.
</dd>
</dl>

**Ejemplos**

Suprime una exención para CVE con el ID `CVE-2018-17929` para todas las imágenes del repositorio `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Suprime una exención de CVE de toda la cuenta para el CVE con el ID `CVE-2018-17929`.

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Suprime una exención de problema de configuración para el problema `application_configuration:nginx.ssl_protocols` para una sola imagen con la etiqueta `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Lista los tipos de problemas de seguridad que puede eximir.

```
ibmcloud cr exemption-types
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

Si está utilizando la autenticación de IAM, este mandato habilita la autorización detallada. Para obtener más información, consulte [Gestión del acceso de usuario con Identity and Access Management](/docs/services/Registry?topic=registry-iam#iam) y [Definición de políticas de roles de acceso](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

Muestra el estado de la política de IAM de la cuenta de {{site.data.keyword.registryshort_notm}} establecida como destino. Para obtener más información, consulte [Gestión del acceso de usuario con Identity and Access Management](/docs/services/Registry?topic=registry-iam#iam) y [Definición de políticas de roles de acceso](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Visualiza detalles sobre una imagen específica.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go.

Para obtener más información, consulte [Formateo y filtrado de la salida de la CLI para mandatos de {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`IMAGE`</dt>
<dd>El nombre de la imagen de la que desea obtener un informe. Puede examinar varias imágenes creando una lista de cada imagen en el mandato con un espacio entre cada nombre.

<p>Para encontrar los nombres de sus imágenes, ejecute `ibmcloud cr image-list`. Combine el contenido de las columnas **Repositorio** y **Etiqueta** para crear el nombre de imagen en el formato `repository:tag`. Si no se especifica ninguna etiqueta en el nombre de la imagen, se examina la imagen etiquetada como `latest`. </p>

</dd>
</dl>

**Ejemplo**

Visualiza detalles sobre los puertos expuestos para la imagen *`us.icr.io/birds/bluebird:1`* mediante la directriz de formateo *`"{{ .Config.ExposedPorts }}"`*.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Visualiza todas las imágenes de su cuenta de {{site.data.keyword.cloud_notm}}.

El nombre de imagen es la combinación del contenido de las columnas **Repositorio** y **Etiqueta** en el formato `repository:tag`
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
<dt>`--no-trunc`</dt>
<dd>(Opcional) No truncar los resúmenes de imagen.</dd>
<dt>`--format FORMAT`</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go.

Para obtener más información, consulte [Formateo y filtrado de la salida de la CLI para mandatos de {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Opcional) Cada imagen se lista en el formato: `repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Opcional) Limitar la salida para visualizar solo imágenes en el espacio de nombres y repositorio o el espacio de nombres especificado. </dd>
<dt>`--include-ibm`</dt>
<dd>(Opcional) Incluye en la salida las imágenes públicas proporcionadas por {{site.data.keyword.IBM_notm}}. Sin esta opción, de forma predeterminada solo se muestran en la lista las imágenes privadas.</dd>
</dl>

**Ejemplo**

Visualiza las imágenes del espacio de nombres *`birds`* en el formato `repository:tag`, sin truncar los resúmenes de imagen.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Suprime una o varias de las imágenes especificadas de {{site.data.keyword.registrylong_notm}}.

Cuando haya varias etiquetas para el mismo resumen de imagen dentro de un repositorio,
el mandato `ibmcloud cr image-rm` elimina todas las imágenes subyacentes y todas sus
etiquetas. Si existe una imagen igual en un otro repositorio o espacio de nombres,
dicha copia de la imagen se elimina. Si quiere eliminar una etiqueta de una imagen y dejar la imagen
subyacente y cualquier otra etiqueta en su sitio, utilice el mandato
[`ibmcloud cr image-untag`](#bx_cr_image_untag).
{: tip}

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**

<dl>
<dt>`IMAGE`</dt>
<dd>El nombre de la imagen que desea suprimir. Puede suprimir varias imágenes al mismo tiempo creando una lista de cada imagen en el mandato con un espacio entre cada nombre. `IMAGE` debe estar en el formato `repository:tag`, por ejemplo: `us.icr.io/namespace/image:latest`

<p>Para encontrar los nombres de sus imágenes, ejecute `ibmcloud cr image-list`. Combine el contenido de las columnas **Repositorio** y **Etiqueta** para crear el nombre de imagen en el formato `repository:tag`. Si no se especifica una etiqueta en el nombre de la imagen, la imagen etiquetada como `latest` se suprime de forma predeterminada.</p>

</dd>
</dl>

**Ejemplo**
Suprime la imagen `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

Añada una etiqueta que especifique en el mandato a una imagen existente, copie la etiqueta en otro repositorio,
o cópiela en un repositorio con un espacio de nombres distinto. La imagen de destino,
`TARGET_IMAGE`, es la nueva imagen y la imagen de origen, `SOURCE_IMAGE`,
es la imagen existente en {{site.data.keyword.registrylong_notm}}. Las imágenes de origen y de destino deben estar en la misma región.

Para encontrar los nombres de sus imágenes, ejecute `ibmcloud cr image-list`. Combine el contenido de las columnas **Repositorio** y **Etiqueta** para crear el nombre de imagen en el formato `repository:tag`.
{: tip}

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>El nombre de la imagen de origen. `SOURCE_IMAGE` debe estar en el formato `repository:tag`, por ejemplo: `us.icr.io/namespace/image:latest`

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>El nombre de la imagen de destino. `TARGET_IMAGE` debe estar en el formato `repository:tag`, por ejemplo: `us.icr.io/namespace/image:latest`

</dd>
</dl>

**Ejemplos**

Añade otra referencia de etiqueta, `latest`, a la imagen `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

Copia la imagen `us.icr.io/birds/bluebird:peck` en otro repositorio en el mismo espacio de nombres `birds/pigeon`.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

Copia la imagen `us.icr.io/birds/bluebird:peck` en otro espacio de nombres `animals` al que tenga acceso.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr image-untag`
{: #bx_cr_image_untag}

Eliminar una o varias etiquetas, de cada imagen especificada en
{{site.data.keyword.registrylong_notm}}.

Para eliminar una etiqueta específica de una imagen y dejar la imagen
subyacente y cualquier otra etiqueta en su sitio, utilice el mandato
`ibmcloud cr image-untag`. Si quiere suprimir la imagen subyacente y todas sus etiquetas, utilice en su lugar el mandato
[`ibmcloud cr image-rm`](#bx_cr_image_rm).
{: tip}

```
ibmcloud cr image-untag IMAGE [IMAGE...]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**

<dl>
<dt>`IMAGE`</dt>
<dd>El nombre de la imagen de la que desea eliminar una etiqueta. Puede suprimir la etiqueta de varias imágenes al mismo tiempo creando una lista de cada imagen en el mandato con un espacio entre cada nombre. `IMAGE` debe estar en el formato `repository:tag`, por ejemplo: `us.icr.io/namespace/image:latest`

<p>Para encontrar los nombres de sus imágenes, ejecute `ibmcloud cr image-list`. Combine el contenido de las columnas **Repositorio** y **Etiqueta** para crear el nombre de imagen en el formato `repository:tag`. Si en el nombre de la imagen no se ha especificado una etiqueta,
el mandato falla.</p>

</dd>
</dl>

**Ejemplo**

Eliminar la etiqueta `1` de la imagen `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-untag us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

Visualiza el nombre y la cuenta del registro en el que ha iniciado una sesión.

```
ibmcloud cr info
```
{: codeblock}

**Requisitos previos**

Ninguno

## `ibmcloud cr login`
{: #bx_cr_login}

Este mandato ejecuta el mandato `docker login` sobre el registro. Se necesita el mandato `docker login` para poder ejecutar los mandatos `docker push` o `docker pull` para el registro. Este mandato no es necesario para ejecutar otros mandatos `ibmcloud cr`. Si Docker no está instalado, este mandato devuelve un mensaje de error.

```
ibmcloud cr login
```
{: codeblock}

**Requisitos previos**

Ninguno

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Elige un nombre para el espacio de nombres y lo añade a su cuenta de {{site.data.keyword.cloud_notm}}.

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
<dt>`NAMESPACE`</dt>
<dd>El espacio de nombres que desea añadir. El espacio de nombres debe ser exclusivo entre todas las cuentas de {{site.data.keyword.cloud_notm}} en la misma región. Los
espacios de nombres deben tener entre 4 y 30 caracteres y solo deben contener letras en minúsculas, números, guiones (-)
y guiones bajos (_). Los espacios de nombres deben empezar y finalizar con una letra o un número.
  
<p>  
<strong>Importante</strong> No coloque información personal en los nombres del espacio de nombres.
</p>
  
</dd>
</dl>

**Ejemplo**

Crea un espacio de nombres con el nombre *`birds`*.

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Visualiza todos los espacios de nombres cuyo propietario es su cuenta de {{site.data.keyword.cloud_notm}}.

```
ibmcloud cr namespace-list
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Elimina un espacio de nombres de su cuenta de {{site.data.keyword.cloud_notm}}. Las imágenes en este espacio de nombres se suprimen cuando se elimina el espacio de nombres.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
<dt>`NAMESPACE`</dt>
<dd>El espacio de nombres que desea eliminar.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Opcional) Forzar la ejecución del mandato sin que el usuario lo solicite.</dd>
</dl>

**Ejemplo**

Elimina el espacio de nombres *`birds`*.

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

Muestra el plan de precios de la región de registro que está estableciendo como destino.

```
ibmcloud cr plan
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Actualiza al plan estándar para la región de registro que está estableciendo como destino.

Para obtener más información sobre los planes, consulte [Planes de registro](/docs/services/Registry?topic=registry-registry_overview#registry_plans).

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opciones del mandato**
<dl>
<dt>`PLAN`</dt>
<dd>(Opcional) El nombre del plan de precios al que desea actualizar. Si no se especifica `PLAN`, el valor predeterminado será `standard`.</dd>
</dl>

**Ejemplo**

Actualiza al plan de precios estándar.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

Importa software de {{site.data.keyword.IBM_notm}} que se descarga desde [IBM Passport Advantage Online para clientes ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/software/passportadvantage/pao_customer.html) y que se empaqueta para utilizarlo con Helm en el espacio de nombres de {{site.data.keyword.registrylong_notm}}.

Las imágenes de contenedor se envían al espacio de nombres privado de {{site.data.keyword.registryshort_notm}}. Las gráficas de Helm se graban en un directorio `ppa-import` que se crea en el directorio desde el que ejecuta el mandato. Opcionalmente, puede utilizar el [proyecto de código abierto de Chart Museum ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/helm/charts/tree/master/stable/chartmuseum) para alojar gráficas de helm.

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>La vía de acceso al archivo comprimido que se descarga desde IBM Passport Advantage.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>Uno de sus espacios de nombres. Las imágenes de contenedor del archivo comprimido se envían a este espacio de nombres. Para listar los espacios de nombres, ejecute `ibmcloud cr namespace-list`.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Opcional) El identificador de recursos exclusivo de [Chart Museum ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(Opcional) El nombre de usuario de [Chart Museum ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(Opcional) La contraseña de [Chart Museum ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
</dl>

**Ejemplo**

Importa el software y el paquete de IBM para utilizarlo con Helm en el espacio de nombres de {{site.data.keyword.registrylong_notm}} *`birds`*, donde la vía de acceso al archivo comprimido es *`downloads/compressed_file.tgz`*.

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

Muestra sus cuotas actuales de tráfico y almacenamiento, así como información de utilización relacionada con dichas cuotas para la región de registro que está estableciendo como destino.

```
ibmcloud cr quota
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Modifica la cuota especificada para la región de registro que está estableciendo como destino.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para configurar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opciones del mandato**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(Opcional) Cambia su cuota de tráfico al valor que especifique en megabytes. La operación falla si no está autorizado a establecer cuotas de tráfico, o si establece un valor por encima del que permite su plan de precios actual.</dd>
<dt>`--storage STORAGE`</dt>
<dd>(Opcional) Cambia su cuota de almacenamiento al valor que especifique en megabytes. La operación falla si no está autorizado a establecer cuotas de almacenamiento, o si establece un valor por encima del que permite su plan de precios actual.</dd>
</dl>

**Ejemplo**

Establece el límite de cuota para el tráfico de extracción en *7000* megabytes y el almacenamiento en *600* megabytes.

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

Visualiza la región de destino y el registro.

```
ibmcloud cr region
```
{: codeblock}

**Requisitos previos**

Ninguno

Para obtener más información, consulte [Regiones](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Establece una región de destino para los mandatos de {{site.data.keyword.registrylong_notm}}. Para enumerar las regiones disponibles, ejecute el mandato sin parámetros.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**Requisitos previos**

Ninguno

**Opciones del mandato**
<dl>
<dt>`REGION`</dt>
<dd>(Opcional) El nombre de su región de destino, por ejemplo, `us-south`.

Para obtener más información, consulte [Regiones](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

</dd>
</dl>

**Ejemplo**

Establece como destino la región EE.UU. sur.

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

Recupera la señal especificada desde el registro.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de gestión de plataforma](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Opciones del mandato**
<dl>
<dt>`TOKEN`</dt>
<dd>Identificador exclusivo de la señal que desea recuperar. Para obtener una lista de sus señales, ejecute `ibmcloud cr token-list`.</dd>
</dl>

**Ejemplo**

Recupera la señal *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

Visualiza todas las señales que existen para su cuenta de {{site.data.keyword.cloud_notm}}.

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de gestión de plataforma](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Opciones del mandato**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go.

Para obtener más información, consulte [Formateo y filtrado de la salida de la CLI para mandatos de {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
</dl>

**Ejemplo**

Visualiza todas las señales que son solo de lectura mediante el uso de la directriz de formateo *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`*.

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

Este ejemplo genera la salida en el formato siguiente:

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

Elimina una o varias de las señales especificadas.

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de gestión de plataforma](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Opciones del mandato**
<dl>
<dt>`TOKEN`</dt>
<dd>TOKEN puede ser la propia señal, o el identificador exclusivo de la señal, tal como se muestra en `ibmcloud cr token-list`. Es posible especificar varias señales separándolas con espacios en blanco.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Opcional) Forzar la ejecución del mandato sin que el usuario lo solicite.</dd>
</dl>

**Ejemplo**

Elimina la señal *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

Visualiza un informe de valoración de vulnerabilidad para sus imágenes.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Requisitos previos**

Para obtener información sobre los permisos necesarios, consulte [Roles de acceso para utilizar {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opciones del mandato**
<dl>
<dt>`IMAGE`</dt>
<dd>El nombre de la imagen de la que desea obtener un informe. El informe indica si la imagen tiene vulnerabilidades de empaquetamiento conocidas. Puede solicitar informes para varias imágenes al mismo tiempo creando una lista de cada imagen en el mandato con un espacio entre cada nombre.

<p>Para encontrar los nombres de sus imágenes, ejecute `ibmcloud cr image-list`. Combine el contenido de las columnas **Repositorio** y **Etiqueta** para crear el nombre de imagen en el formato `repository:tag`. Si no se especifica una etiqueta en el nombre de la imagen, el informe evalúa la imagen que está etiquetada como `latest`.</p>

<p>Se admiten los siguientes sistemas operativos:

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

Para obtener más información, consulte [Gestión de imágenes de seguridad con Vulnerability Advisor](/docs/services/va?topic=va-va_index).

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Opcional) La salida del mandato muestra información adicional sobre arreglos para paquetes vulnerables.</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Opcional) La salida del mandato se restringe para mostrar solo vulnerabilidades.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Opcional) La salida del mandato se restringe para mostrar solo problemas de configuración.</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(Opcional) La salida del mandato se devuelve en el formato elegido. El formato predeterminado es `text`. Se admiten los formatos siguientes:

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**Ejemplos**

Muestra un informe de evaluación de vulnerabilidad estándar para su imagen.

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

Muestra un informe de evaluación de vulnerabilidad para la imagen `us.icr.io/birds/bluebird:1` en formato JSON, que muestre solo vulnerabilidades.

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
