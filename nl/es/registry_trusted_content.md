---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Firma de imágenes para contenido de confianza
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} proporciona tecnología de contenido de confianza para que pueda firmar imágenes para asegurar la integridad de las imágenes en el espacio de nombres de registro. Al extraer y enviar imágenes firmadas, puede verificar que las imágenes las ha enviado la parte correcta, como el conjunto de herramientas de integración continua (CI). Para utilizar esta característica, debe tener Docker versión 1.11 o posterior. Puede obtener más información revisando la documentación de [Docker Content Trust](https://docs.docker.com/engine/security/trust/content_trust/) y del [proyecto de Notary](https://github.com/theupdateframework/notary).
{:shortdesc}

Al enviar la imagen con el contenido de confianza habilitado, el cliente de Docker también envía un objeto de metadatos firmado al servidor de confianza de {{site.data.keyword.Bluemix_notm}}. Al extraer una imagen etiquetada con Docker Content Trust habilitado, el cliente de Docker contacta con el servidor de confianza para establecer la última versión firmada de la etiqueta que ha solicitado, verifica la firma del contenido y descarga la imagen firmada.

Un nombre de imagen se compone de un repositorio y de una etiqueta. Al utilizar contenido de confianza, cada repositorio utiliza una clave de firma exclusiva. Cada etiqueta de un repositorio utiliza la clave que pertenece al repositorio. Si tiene varios equipos publicando contenido, cada uno en su propio repositorio dentro de los espacios de nombres de {{site.data.keyword.registrylong_notm}}, cada equipo puede utilizar sus propias claves para firmar su contenido, de modo que pueda verificar que cada imagen la produzca el equipo apropiado.

Un repositorio puede contener contenido firmado y no firmado. Si tiene Docker Content Trust habilitado, puede acceder al contenido firmado en un repositorio, aunque haya otro contenido no firmado junto a él.

Docker Content Trust utiliza un modelo de seguridad "trust on first use" ("confianza en el primer uso"). La clave de repositorio se extrae del servidor de confianza al extraer una imagen firmada de un repositorio por primera vez, y dicha clave se utiliza para verificar imágenes de ese repositorio en el futuro. Debe verificar que confíe en el servidor de confianza o en la imagen y su editor antes de extraer el repositorio por primera vez. Si la información de confianza del servidor está en peligro y no ha extraído una imagen del repositorio antes, el cliente de Docker podría extraer la información en peligro del servidor de confianza. Si los datos de confianza están en peligro después de extraer la imagen por primera vez, en extracciones posteriores, el cliente de Docker no podrá verificar los datos en peligro y no extraerá la imagen. Para obtener más información sobre cómo inspeccionar datos de confianza para una imagen, consulte [Visualización de imágenes firmadas](#trustedcontent_viewsigned).

Para obtener más información sobre el modelo de seguridad "trust on first use" ("confianza en el primer uso"), consulte [The Update Framework (TUF)](https://theupdateframework.github.io/). 


## Configuración del entorno de contenido de confianza
{: #trustedcontent_setup}

De forma predeterminada, Docker Content Trust está inhabilitado. Habilite el entorno de Content Trust antes de iniciar sesión en {{site.data.keyword.registrylong_notm}} y trabajar con imágenes firmadas.
{:shortdesc}

1.  Habilite la variable de entorno de Docker Content Trust en el terminal.

    Para Linux o Mac:

    ```
    export DOCKER_CONTENT_TRUST=1
    ```
    {: codeblock}

    Para Windows:

    ```
    set DOCKER_CONTENT_TRUST=1
    ```
    {: codeblock}

2.  Inicie la sesión en la CLI de {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login [--sso]
    ```
    {: pre}

    Si tiene un ID federado, utilice `ibmcloud login --sso` para iniciar la sesión. Especifique el nombre de usuario y utilice el URL proporcionado en su salida de CLI para recuperar el código de acceso de un solo uso. Sabe tiene un ID federado cuando el inicio de sesión falla sin el `--sso` y se lleva a cabo correctamente con la opción `--sso`.
    {:tip}

3.  Establezca la región que desee utilizar. Si no conoce el nombre de la región, puede ejecutar el mandato sin la región y elegir uno.

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

4.  Inicie una sesión en {{site.data.keyword.registrylong_notm}}.

    ```
    ibmcloud cr login
    ```
    {: pre}

    La salida le indica que exporte la variable de entorno de Docker Content Trust. Por ejemplo:

    ```
    user:~ user$ ibmcloud cr login
    Logging in to 'registry.ng.bluemix.net'...
    Logged in to 'registry.ng.bluemix.net'.

    To set up your Docker client with content trust, export the following environment variable:
    export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
    {: screen}

5.  Copie y pegue el mandato de la variable de entorno en el terminal. Por ejemplo:

    ```
    export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
    {: pre}


Ahora está listo para enviar, extraer y gestionar imágenes firmadas de confianza.

Durante la sesión con Docker Content Trust habilitado, si desea realizar una operación con el contenido de confianza habilitado (como extraer una imagen no firmada), utilice el distintivo `--disable-content-trust` con el mandato.
{: tip}

## Envío de una imagen firmada
{: #trustedcontent_push}

Cuando envíe por primera vez una imagen firmada, Docker crea automáticamente un par de claves de firma: raíz y repositorio. Para firmar una imagen en un repositorio donde se hayan enviado antes las imágenes firmadas, debe tener la clave de firma de repositorios correcta cargada en la máquina que está enviando la imagen.
{:shortdesc}

Antes de empezar, [configure su espacio de nombres de registro](index.html#registry_namespace_add).

1.  [Configure su entorno de contenido de confianza](#trustedcontent_setup).

2.  [Envíe su imagen](index.html#registry_images_pushing). La etiqueta es obligatoria para contenido de confianza. En la salida de mandato que ve, "Firma y envío de metadatos de imagen".

3.  **Enviando por primera vez un repositorio firmado.** Al enviar una imagen firmada a un repositorio nuevo, el mandato creará dos claves de firma, clave raíz y clave de repositorio, y las almacenará en la máquina local. Especifique y guarde frases de contraseña seguras para cada clave, y a continuación [haga copia de seguridad de sus claves](#trustedcontent_backupkeys). La copia de seguridad de sus claves es fundamental porque sus [opciones de recuperación](ts_index.html#ts_recoveringtrustedcontent) son limitadas.


## Extracción de una imagen firmada
{: #trustedcontent_pull}

La primera vez que extraiga una imagen firmada con Docker Content Trust habilitado, el cliente de Docker reconocerá la firma como de confianza. El cliente de Docker extrae la versión firmada más reciente de la imagen que especifica. Las imágenes no firmadas o el contenido que no es de confianza no se extraerá.
{:shortdesc}


1.  [Configure su entorno de contenido de confianza](#trustedcontent_setup).

2.  Extraiga la imagen. Sustituya _&lt;source_image&gt;_ por el repositorio de la imagen y _&lt;tag&gt;_ por la etiqueta de la imagen que desea utilizar, como por ejemplo _latest_. Para listar las imágenes disponibles a extraer, ejecute `ibmcloud cr image-list`.

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Especifique la etiqueta cuando envíe o extraiga una imagen firmada. La etiqueta `latest` solo tiene el valor predeterminado cuando la confianza de contenido esté inhabilitada.
    {: tip}

## Gestión de contenido de confianza
{: #trustedcontent_managetrust}

Mediante los mandatos `docker trust`, puede ver quién ha firmado las imágenes, así como también revocar el estado del contenido de confianza. Para ejecutar los mandatos `docker trust`, necesita Docker 17.12 o posterior.
{:shortdesc}

### Visualización de imágenes firmadas
{: #trustedcontent_viewsigned}

Puede revisar versiones firmadas de un repositorio de imágenes o de una etiqueta, incluida información sobre el ID de clave y el firmante.
{:shortdesc}

1.  [Configure su entorno de contenido de confianza](#trustedcontent_setup).

2.  Revise la información de la etiqueta, del resumen y del firmante para cada imagen. **Opcional**: Especifique la etiqueta _&lt;tag&gt;_ para ver información para dicha versión de la imagen.

    ```
    docker trust view <image>:<tag>
    ```
    {: pre}

### Revocación de confianza
{: #trustedcontent_revoketrust}

Puede revocar el estado de contenido de confianza de una imagen.
{:shortdesc}

Antes de empezar, recupere la frase de contraseña de clave de repositorio que ha guardado al [enviar por primera vez el repositorio de confianza](#trustedcontent_push). Si necesita identificar qué clave se utiliza para la imagen de confianza, utilice el [mandato](#trustedcontent_viewsigned) `docker view`.

1.  [Configure su entorno de contenido de confianza](#trustedcontent_setup).

2.  Elimine todos los metadatos de confianza para el repositorio de imágenes. Escriba la frase de contraseña de clave de repositorio cuando se le solicite. **Opcional**: Especifique una etiqueta para revocar los metadatos de confianza solo para dicha versión de la imagen.

    ```
    docker trust revoke <image>:<tag>
    ```
    {: pre}

3.  Verifique que la confianza se haya revocado en la lista de contenido de confianza. **Opcional**: Incluya la etiqueta si desea verificar el contenido revocado para una imagen etiquetada.

    ```
    $ docker trust view <image>:<tag>

    No signatures for <image>:<tag>
    ```
    {: codeblock}

## Copia de seguridad de claves de firma
{: #trustedcontent_backupkeys}

Al enviar por primera vez una imagen firmada a un repositorio nuevo, Docker Content Trust creará dos claves de firma, clave raíz y clave de repositorio, y las almacena en la máquina local:

*  Directorio de Linux y Mac: `~/.docker/trust/private`

*  Directorio de Windows: `%HOMEPATH%\.docker\trust\private`

   Si ya cambiado el directorio de configuración de Docker, busque el subdirectorio `trust` allí.
   {: tip}

Debe realizar copia de seguridad de todas sus claves, y especialmente de la clave raíz. Si una clave se pierde o está en peligro, las [opciones de recuperación](ts_index.html#ts_recoveringtrustedcontent) estarán limitadas.

Para hacer copia de seguridad de sus claves, consulte la [documentación de Docker Content Trust](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys).


## Gestión de firmantes de confianza
{: #trustedcontent_signers}

Puede añadir y eliminar firmantes de las imágenes de firma en un repositorio.
{:shortdesc}

### Adición de firmantes a un repositorio de confianza
{: #trustedcontent_addsigners}

Para permitir que otros usuarios firmen imágenes en un repositorio, añada las claves de firma para dichos usuarios a dicho repositorio.
{:shortdesc}

Antes de empezar:
- Los firmantes de imágenes deben tener permiso para enviar imágenes al espacio de nombres. 
- Los propietarios del repositorio y los firmantes adicionales deben tener Docker 17.12 o posterior instalado.
- Cree un repositorio de contenido de confianza [enviando una imagen firmada](#trustedcontent_push). Los propietarios del repositorio deben tener las claves de administración del repositorio para el repositorio disponibles en la carpeta de confianza de Docker en su máquina local. Si no tiene la clave admin de repositorio, póngase en contacto con el propietario para que realice esta tarea.

Al añadir un firmante, ya no podrá utilizar la clave admin del repositorio para firmar imágenes en dicho repositorio. Debe contener la clave privada para que la firme uno de los firmantes aprobados. Para conservar la posibilidad de firmar imágenes tras añadir un firmante, siga estas instrucciones de nuevo para generar y añadir un rol de firmante para sí mismo.
{:tip}

Para compartir las claves de firma:

1.  Si el nuevo firmante no ha generado un par de claves todavía, este debe generarse y cargarse. 
  
    a. Generar la clave. Para el <em>NAME</em>, puede especificar cualquier nombre; sin embargo, el nombre que seleccione estará visible cuando alguien inspeccione la confianza en el repositorio. Trabaje con el propietario del repositorio para satisfacer los convenios de denominación que pueden ser utilizados por la organización y para seleccionar un nombre que sea identificable para dicho firmante.

      ```
      docker trust key generate <NAME>
      ```
      {: pre}
  
    b. Especificar una frase de contraseña para la clave privada. Se genera una clave pública (`.pub`), y la clave privada correspondiente se carga automáticamente en la configuración de confianza de Docker.
  
    c. El nuevo firmante debe enviar al propietario del repositorio la clave pública.

2.  El propietario del repositorio debe añadir la clave del firmante al repositorio.

    a. [Configure el entorno de contenido de confianza](#trustedcontent_setup)
    
    b. Añada la clave del firmante al repositorio.

      ```
      docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}
    
3.  El firmante puede configurar su entorno y firmar una imagen.

    a. [Configure el entorno de contenido de confianza](#trustedcontent_setup)
    
    b. El firmante debe firmar una imagen. Cuando se le solicite, especifique la frase de contraseña para la clave privada.

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4.  Para verificar que se haya añadido el firmante, consulte [Visualización de imágenes firmadas](#trustedcontent_viewsigned).



### Eliminación de un firmante de un repositorio
{: #trustedcontent_removesigner}

Si ya no desea que un firmante pueda firmar imágenes en el repositorio, puede eliminarlo como firmante.
{:shortdesc}

Antes de empezar:
- Los propietarios del repositorio y los firmantes adicionales deben tener Docker 17.12 o posterior instalado.

Si elimina un firmante, el servidor de confianza no confía en sus versiones firmadas de la imagen. Para asegurarse de que la imagen se pueda extraer tras eliminar el firmante, asegúrese de que el firmante no haya firmado la versión más reciente de la imagen antes de continuar. Si el firmante ha firmado la versión más reciente de la imagen, envíe una actualización a la imagen y fírmela con la clave antes de continuar.
{:tip}

Para eliminar un firmante:

1. [Configure su entorno de contenido de confianza](#trustedcontent_setup).

2. Elimine el firmante.

    ```
    docker trust signer remove <NAME> <repository>
    ```
    {: pre}
    
3. Para verificar que el firmante se haya eliminado, visualice los datos de confianza para la imagen y verifique que el firmante ya no esté listado. Para obtener más información sobre la visualización de datos de confianza, consulte [Visualización de imágenes firmadas](#trustedcontent_viewsigned).
