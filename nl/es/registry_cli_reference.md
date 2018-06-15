---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Mandatos de {{site.data.keyword.registrylong_notm}} (`bx cr`) para gestionar imágenes de Docker en el espacio de nombres
{: #registry_cli_reference}

Puede utilizar el plug-in container-registry para configurar su propio espacio de nombres de imágenes en un registro privado gestionado y albergado por IBM en el que puede almacenar y compartir de forma segura imágenes de Docker con todos los usuarios de su cuenta de {{site.data.keyword.Bluemix}}.
{:shortdesc}


## Mandatos bx cr
{: #registry_cli_reference_bxcr}

Ejecute los mandatos `bx cr` en la CLI de {{site.data.keyword.registryshort_notm}}.
{:shortdesc}
  
Para ver los mandatos soportados, consulte [CLI de {{site.data.keyword.registrylong_notm}}](registry_cli.html).

## Formateo y filtrado de la salida de la CLI para mandatos de {{site.data.keyword.registrylong_notm}}
{: #registry_cli_listing}

Puede formatear y filtrar la salida de la CLI soportados para los mandatos admitidos de {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

De forma predeterminada, la salida de la CLI se muestra en un formato legible para las personas. Sin embargo, esta vista puede limitar su capacidad de utilizar la salida, especialmente si el mandato se ejecuta mediante programación. Por ejemplo, en la salida de la CLI de `bx cr image-list`, es posible que desee clasificar el campo `Size` por tamaño numérico, pero el mandato devuelve una descripción del tamaño en formato de serie de caracteres. El plug-in container-registry proporciona la opción format, que puede utilizar para aplicar una plantilla de Go a la salida de la CLI. La plantilla de Go es una característica del [lenguaje de programación Go](https://golang.org/pkg/text/template/) que le permite personalizar la salida de la CLI.

Puede modificar la salida de la CLI mediante la aplicación de la opción de formato de dos maneras:

1.  Formatee los datos de la salida de la CLI. Por ejemplo, cambie la salida del campo `Created` de Unix time a hora estándar.
2.  Filtre los datos en la salida de la CLI. Por ejemplo, filtre los detalles de la imagen para visualizar un subconjunto específicos de imágenes utilizando la condición `if gt` de la plantilla de Go.

Puede utilizar la opción format con los siguientes mandatos de {{site.data.keyword.registrylong_notm}}. Pulse el mandato para visualizar una lista de campos disponibles y sus tipos de datos.

-   [`bx cr image-list`](registry_cli_reference.html#registry_cli_listing_imagelist)
-   [`bx cr image-inspect`](registry_cli_reference.html#registry_cli_listing_imageinspect)
-   [`bx cr token-list`](registry_cli_reference.html#registry_cli_listing_tokenlist)

El código siguiente muestra cómo puede utilizar las opciones de formateo y de filtrado.

-   Ejecute el siguiente mandato `bx cr image-list` para visualizar el repositorio, la etiqueta y el estado de seguridad de todas las imágenes que tienen un tamaño de más de 1 MB:

    ```
    bx cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
    ```
    {: pre}

    Salida de ejemplo:

    ```
    example-registry.<region>.bluemix.net/user1/ibmliberty:latest No Issues
    example-registry.<region>.bluemix.net/user1/ibmnode:1 2 Issues
    example-registry.<region>.bluemix.net/user1/ibmnode:test1 1 Issue
    example-registry.<region>.bluemix.net/user1/ibmnode2:test2 7 Issues
    ```
    {: screen}


-   Ejecute el siguiente mandato `bx cr image-inspect` para ver dónde se encuentra la documentación de IBM correspondiente a una determinada imagen pública de IBM:

    ```
    bx cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"

    ```
    {: pre}

    Salida de ejemplo:

    ```
    map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
    ```
    {: screen}

-   Ejecute el siguiente mandato `bx cr image-inspect` para ver los puertos expuestos para una determinada imagen:

    ```
    bx cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"

    ```
    {: pre}

    Salida de ejemplo:

    ```
    map[9080/tcp: 9443/tcp:]
    ```
    {: screen}

-   Ejecute el siguiente mandato `bx cr token-list` para ver todas las señales de solo lectura:

    ```
    bx cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
    {: pre}

    Salida de ejemplo:

    ```
    0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
    ```
    {: screen}


### Opciones de plantilla de Go y tipos de datos en el mandato `bx cr image-list`
{: #registry_cli_listing_imagelist}

Revise la tabla siguiente para ver las opciones de plantilla de Go disponibles y los tipos de datos para el mandato `bx cr image-list`.
{:shortdesc}

|Campo|Tipo|Descripción|
|-----|----|-----------|
|`Created`|Entero (64 bits)|Muestra cuándo se ha creado la imagen, expresado en número de segundos en [hora de Unix](https://en.wikipedia.org/wiki/Unix_time).|
|`Digest`|Serie|Muestra el identificador exclusivo de una imagen.|
|`Namespace`|Serie|Muestra el espacio de nombres en el que está almacenada la imagen.|
|`Repository`|Serie|Muestra el repositorio de la imagen.|
|`Size`|Entero (64 bits)|Muestra el tamaño de la imagen en bytes.|
|`Tag`|Serie|Muestra la etiqueta de la imagen.|
|`SecurityStatus`|Estructura|Muestra el estado de vulnerabilidad de la imagen. Puede filtrar y formatear los valores siguientes: Status  `string`, IssueCount  `int`, y ExemptionCount  `int`. Los estados posibles se describen en [Revisión de un informe de vulnerabilidad mediante la CLI](../va/va_index.html#va_registry_cli).|
{: caption="Tabla 1. Campos y tipos de datos disponibles en el mandato bx cr image-list." caption-side="top"}

### Opciones de plantilla de Go y tipos de datos en el mandato `bx cr image-inspect`
{: #registry_cli_listing_imageinspect}

Revise la tabla siguiente para ver las opciones de plantilla de Go disponibles y los tipos de datos para el mandato `bx cr image-inspect`.
{:shortdesc}

|Campo|Tipo|Descripción|
|-----|----|-----------|
|`ID`|Serie|Muestra el identificador exclusivo de una imagen.|
|`Parent`|Serie|Muestra el ID de la imagen padre utilizada para crear esta imagen.|
|`Comment`|Serie|Muestra la descripción de la imagen.|
|`Created`|Serie|Muestra la [indicación de fecha y hora de Unix](https://en.wikipedia.org/wiki/Unix_time) en la que se creó la imagen.|
|`Container`|Serie|Muestra el ID del contenedor que ha creado la imagen.|
|`ContainerConfig`|Objeto|Muestra la configuración predeterminada de los contenedores iniciados desde esta imagen. Consulte los detalles del campo en [Config](registry_cli_reference.html#config).|
|`DockerVersion`|Serie|Muestra la versión de Docker utilizada para crear esta imagen.|
|`Author`|Serie|Muestra el autor de la imagen.|
|`Config`|Objeto|Muestra los metadatos de configuración para la imagen. Consulte los detalles del campo en [Config](registry_cli_reference.html#config).|
|`Architecture`|Serie|Muestra la arquitectura de procesador que se ha utilizado para crear esta imagen y que se necesita para ejecutar la imagen.|
|`Os`|Serie|Muestra la familia de sistema operativo que se ha utilizado para crear esta imagen y que se necesita para ejecutar la imagen.|
|`OsVersion`|Serie|Muestra la versión del sistema operativo que se ha utilizado para crear esta imagen.|
|`Size`|Entero (64 bits)|Muestra el tamaño de la imagen en bytes.|
|`VirtualSize`|Entero (64 bits)|Muestra la suma del tamaño de cada capa de la imagen en bytes.|
|`RootFS`|Objeto|Muestra metadatos que describen el sistema de archivos raíz correspondiente a la imagen. Consulte los detalles del campo en [RootFS](registry_cli_reference.html#rootfs).|
{: caption="Tabla 2. Campos y tipos de datos disponibles en el mandato bx cr image-inspect." caption-side="top"}

#### Config

|Campo|Tipo|Descripción|
|-----|----|-----------|
|`Hostname`|Serie|Muestra el nombre de host del contenedor.|
|`Domainname`|Serie|Muestra el nombre de dominio completo del contenedor.|
|`User`|Serie|Muestra el usuario que ejecuta mandatos dentro del contenedor en el que se utiliza la imagen.|
|`AttachStdin`|Booleano|Muestra _true_ si la corriente de entrada estándar se ha adjuntado al contenedor y _false_ si no es así.|
|`AttachStdout`|Booleano|Muestra _true_ si la corriente de salida estándar se ha adjuntado al contenedor y _false_ si no es así.|
|`AttachStderr`|Booleano|Muestra _true_ si la corriente de error estándar se ha adjuntado al contenedor y _false_ si no es así.|
|`ExposedPorts`|Correlación de clave-valor|Muestra la lista de puertos expuestos en el formato `[123:,456:]`.|
|`Tty`|Booleano|Muestra _true_ si se ha asignado un seudo-tty al contenedor y _false_ si no es así.|
|`OpenStdin`|Booleano|Muestra _true_ si la corriente de entrada estándar está abierta y _false_ si no es así.|
|`StdinOnce`|Booleano|Muestra _true_ si la corriente de entrada estándar se cierra cuando el cliente conectado se desconecta y _false_ si la corriente de entrada estándar permanece abierta.|
|`Env`|Matriz de series|Muestra la lista de variables de entorno en formato de pares clave-valor.|
|`Cmd`|Matriz de series|Describe los mandatos y argumentos que se pasen a un contenedor para que se ejecuten cuando se inicie el contenedor.|
|`Healthcheck`|Objeto|Describe cómo comprobar que el contenedor está en buen estado. Consulte los detalles del campo en [Healthcheck](registry_cli_reference.html#healthcheck).|
|`ArgsEscaped`|Booleano|Muestra true si el mandato ya está entre caracteres de escape (específico de Windows).|
|`Image`|Serie|Muestra el nombre de la imagen que se ha pasado el operador.|
|`Volumes`|Correlación de clave-valor|Muestra la lista de montajes de volúmenes que se han montado en un contenedor.|
|`WorkingDir`|Serie|Muestra el directorio de trabajo dentro del contenedor en el que se ejecutan los mandatos especificados.|
|`Entrypoint`|Matriz de series|Describe el mandato que se ejecuta cuando se inicia el contenedor.|
|`NetworkDisabled`|Booleano|Muestra _true_ si la conexión en red está inhabilitado para el contenedor y _false_ si la conexión en red está habilitada para el contenedor.|
|`MacAddress`|Serie|Muestra la dirección MAC asignada al contenedor.|
|`OnBuild`|Matriz de series|Muestra los metadatos ONBUILD que se han definido en el archivo Docker de la imagen.|
|`Labels`|Correlación de clave-valor|Muestra la lista de etiquetas que se han añadido a la imagen como pares clave-valor.|
|`StopSignal`|Serie|Describe la señal de detención de UNIX que se debe enviar cuando se desee detener el contenedor.|
|`StopTimeout`|Entero|Muestra el tiempo de espera excedido en segundos para detener un contenedor.|
|`Shell`|Matriz de series|Muestra el formato de shell de RUN, CMD, ENTRYPOINT.|
{: caption="Tabla. " caption-side="top"}

#### Healthcheck

|Campo|Tipo|Descripción|
|-----|----|-----------|
|`Test`|Matriz de series|Muestra cómo realizar la prueba de comprobación de estado. Las opciones disponibles son:<ul><li>{}: heredar comprobación de estado</li><li>{"NONE"}: la comprobación de estado está inhabilitada</li><li>{"CMD", args...}: ejecutar argumentos directamente</li><li>{"CMD-SHELL", command}: ejecutan el mandato con el shell predeterminado del sistema</li></ul>|
|`Interval`|Entero (64 bits)|Visualiza el tiempo que se debe esperar entre dos comprobaciones de estado en nanosegundos.|
|`Timeout`|Entero (64 bits)|Muestra el tiempo que se debe esperar antes de considerar que una comprobación de estado ha fallado en nanosegundos.|
|`Retries`|Entero|Muestra el número de errores consecutivos que se necesitan para considere que un contenedor está en mal estado.|
{: caption="Tabla 4. Campos y tipos de datos disponibles en la estructura Healthcheck." caption-side="top"}

#### RootFS

|Opción|Tipo|Descripción|
|------|----|-----------|
|`Type`|Serie|Muestra el tipo de sistema de archivos.|
|`Layers`|Matriz de series|Muestra los descriptores de cada capa de la imagen.|
|`BaseLayer`|Serie|Muestra el descriptor de la capa base de la imagen.|
{: caption="Tabla 5. Campos y tipos de datos disponibles en la estructura RootFS." caption-side="top"}

### Opciones de plantilla de Go y tipos de datos en el mandato `bx cr token-list`
{: #registry_cli_listing_tokenlist}

Revise la tabla siguiente para ver las opciones de plantilla de Go disponibles y los tipos de datos para el mandato `bx cr token-list`.
{:shortdesc}

|Campo|Tipo|Descripción|
|-----|----|-----------|
|`ID`|Serie|Muestra el identificador exclusivo de una señal.|
|`Expiry`|Entero (64 bits)|Muestra la [indicación de fecha y hora de Unix](https://en.wikipedia.org/wiki/Unix_time) en que caduca la señal.|
|`ReadOnly`|Booleano|Muestra _true_ cuando solo puede extraer imágenes y _false_ cuando puede extraer imágenes del espacio de nombres y transmitir imágenes al mismo.|
|`Description`|Serie|Muestra la descripción de la señal.|
{: caption="Tabla 6. Campos y tipos de datos disponibles en el mandato bx cr token-list." caption-side="top"}
