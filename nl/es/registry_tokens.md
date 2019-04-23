---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-29"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

# Automatización del acceso a {{site.data.keyword.registrylong_notm}}
{: #registry_access}

Puede utilizar elementos de registro o una clave de API (IAM) de {{site.data.keyword.iamlong}} para automatizar el acceso a sus espacios de nombres de {{site.data.keyword.registrylong_notm}} para poder enviar por push y extraer imágenes.
{:shortdesc}

¿Está intentando utilizar las imágenes de registro en despliegues de Kubernetes? Consulte [Acceso a imágenes en otros espacios de nombres de Kubernetes, regiones de {{site.data.keyword.Bluemix_notm}} y cuentas](/docs/containers?topic=containers-images#other).
{: tip}

Las claves de API están enlazadas a su cuenta y pueden utilizarse en {{site.data.keyword.Bluemix_notm}} sin que necesite distintas credenciales para cada servicio. Puede utilizar la clave de API en la CLI o como parte de la automatización para iniciar sesión como su identidad de usuario.

Los elementos de registro solo abarcan {{site.data.keyword.registrylong_notm}}. Puede limitarlos a un acceso de sólo lectura y puede seleccionar si caducan o no caducan.

Si utiliza una clave de API, puede controlar el acceso a los espacios de nombres utilizando las políticas de IAM. Para obtener más información, consulte [Definición de políticas de rol de acceso de usuario](/docs/services/Registry?topic=registry-user#user).

Para obtener más información acerca de las claves de API de {{site.data.keyword.registrylong_notm}}, consulte [Cómo trabajar con claves de API](/docs/iam?topic=iam-manapikey#manapikey).

Antes de empezar, [instale {{site.data.keyword.registrylong_notm}} y la CLI de Docker](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Acceso automático a sus espacios de nombres mediante el uso de claves de API
{: #registry_api_key}

Puede utilizar claves de API para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres.
{:shortdesc}

### Creación de una clave de API
{: #registry_api_key_create}

Puede crear un clave de API que puede utilizar para iniciar sesión en su registro.
{:shortdesc}

Puede crear tanto claves de API de usuario como claves de API de ID de servicio.

- Para crear una clave de API de ID de servicio, consulte [Creación de una clave de API para un ID de servicio](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
- Para crear una clave de API de usuario, consulte [Creación de una clave de API](/docs/iam?topic=iam-userapikey#create_user_key).

### Utilización de una clave de API para automatizar el acceso
{: #registry_api_key_use}

Puede utilizar una clave de API para automatizar el acceso a sus espacios de nombres en {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Utilice la clave de API para iniciar sesión en su registro mediante la ejecución del siguiente mandato Docker. Sustituya `<your_apikey>` por su clave de API y sustituya `<registry_url>` por el URL del registro en el que están configurados sus espacios de nombres.

- Para espacios de nombres configurados en AP-North, utilice `jp.icr.io`
- Para espacios de nombres configurados en AP sur, utilice `au.icr.io`
- Para espacios de nombres configurados en UE central, utilice `de.icr.io`
- Para espacios de nombres configurados en Reino Unido sur, utilice `uk.icr.io`
- Para espacios de nombres configurados en EE.UU. sur, utilice `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Para obtener información acerca del mandato, consulte [Cree una nueva clave de API de plataforma {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Automatización del acceso a sus espacios de nombres mediante señales (en desuso)
{: #registry_tokens}

Puede utilizar señales para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Utilizar señales para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres está en desuso. Utilice claves de API para automatizar el acceso al espacio de nombres, consulte [Automatización del acceso a los espacios de nombres mediante claves de API](#registry_api_key).
{: deprecated}

Cualquiera que tenga una señal de registro puede acceder a la información protegida. Si desea que los usuarios de fuera de su cuenta puedan acceder a todos los espacios de nombres que ha configurado en una región, puede crear una señal para su cuenta de {{site.data.keyword.Bluemix_notm}}. Cada usuario o app en posesión de esta señal puede enviar por push o extraer imágenes a espacios de nombres sin tener que instalar el plugin de CLI `container-registry`.

Cuando crea una señal para su cuenta de {{site.data.keyword.Bluemix_notm}}, puede decidir si dicha señal autoriza el acceso de sólo lectura (extraer) o el acceso de escritura (enviar por push y extraer) para el
registro. También puede especificar si una señal es permanente o si ésta caduca después de 24 horas. Puede crear y utilizar varias señales para controlar los diferentes tipos de acceso.

Si inicia la sesión en {{site.data.keyword.registrylong_notm}} utilizando una señal de registro, las políticas de acceso de IAM no se imponen. Si desea restringir el acceso a uno o varios espacios de nombres para un ID que se utiliza en la automatización, tenga en cuenta la posibilidad de utilizar una clave de API de ID de servicio de IAM en lugar de una señal de registro. Para obtener más información sobre cómo crear una clave de API y utilizarla con {{site.data.keyword.registrylong_notm}}, consulte [Automatización del acceso a los espacios de nombres mediante claves de API](#registry_api_key).

Utilice las siguientes tareas para gestionar sus señales:

- [Creación de una señal para su cuenta de {{site.data.keyword.Bluemix_notm}}](#registry_tokens_create)
- [Utilización de una señal para automatizar el acceso a su espacio de nombres](#registry_tokens_use)
- [Eliminación de una señal de su cuenta de {{site.data.keyword.Bluemix_notm}}](#registry_tokens_remove)

### Creación de una señal para su cuenta de {{site.data.keyword.Bluemix_notm}} (en desuso)
{: #registry_tokens_create}

Puede crear una señal para otorgar acceso a todos los espacios de nombres {{site.data.keyword.registrylong_notm}} en una región.
{:shortdesc}

Utilizar señales para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres está en desuso. Utilice claves de API para automatizar el acceso al espacio de nombres, consulte [Automatización del acceso a los espacios de nombres mediante claves de API](#registry_api_key).
{: deprecated}

1. Cree una señal. En el ejemplo siguiente se crea una señal que no caduca que tiene acceso de lectura y escritura a todos los espacios de nombres que se encuentran configurados en una región.

   ```
   ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
   ```
   {: pre}

   <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="light bulb icon"/> Descripción de los componentes de este mandato</th>
        </thead>
          <caption>Tabla 1. Los componentes del mandato `ibmcloud cr token-add`</caption>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>Opcional. Utilice esta opción para describir la señal para que pueda identificarla más fácilmente más tarde.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>Opcional. Utilice esta opción para crear una señal que no caduca. Si no especifica esta opción, la señal se convierte en no válida después de 24 horas. <br> **Consejo:** Cuando ya no necesite una señal que no caduca para bloquear el acceso a los espacios de nombres, recuerde eliminar la señal.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>Opcional. Utilice esta opción para crear una señal que permite a los usuarios enviar por push y extraer imágenes a y desde los espacios de nombres. Si no especifica esta opción, la señal se puede utilizar para extraer sólo imágenes.</td>
        </tr>
        </tbody>
   </table>

   Su salida de CLI tiene un aspecto similar a la salida siguiente:

   ```
   Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad
   Token              eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJpYm0uY29tIiwibmFtZSI6Ikdpbm5pIFJvbWV0dHkiLCJpYXQiOjE1NDYzMDA4MDB9.wYMmTPHmrqhyHtgw5T8lbl1hxr2ykHq5T5s3mvMxjDw
   ```
   {: screen}

2. Verifique que la señal se ha creado.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

### Utilización de una señal para automatizar el acceso a su espacio de nombres (en desuso)
{: #registry_tokens_use}

Puede utilizar una señal en su mandato `login docker` para automatizar el acceso a sus espacios de nombres en {{site.data.keyword.registrylong_notm}}. Dependiendo de si establece un acceso de sólo lectura o de lectura/escritura para la señal, los usuarios pueden enviar por push y extraer imágenes a y desde los espacios de nombres.
{:shortdesc}

Utilizar señales para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres está en desuso. Utilice claves de API para automatizar el acceso al espacio de nombres, consulte [Automatización del acceso a los espacios de nombres mediante claves de API](#registry_api_key).
{: deprecated}

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

2. Enumere todas las señales de la cuenta de {{site.data.keyword.Bluemix_notm}} y tenga en cuenta el ID de señal que desea utilizar.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. Recupere el valor de la señal para la señal. Sustituya `<token_id>` por el ID de la señal.

   ```
   ibmcloud cr token-get <token_id>
   ```
   {: pre}

    Su valor de la señal se muestra en **Señal** de la salida de la CLI.

4. Utilice la señal como parte del mandato `docker login`. Sustituya `<token_value>` por el valor de la señal que ha recuperado en el paso anterior y `<registry_url>` por el URL del registro en el que están configurados sus espacios de nombres.

   - Para espacios de nombres configurados en AP-North, utilice `jp.icr.io`
   - Para espacios de nombres configurados en AP sur, utilice `au.icr.io`
   - Para espacios de nombres configurados en UE central, utilice `de.icr.io`
   - Para espacios de nombres configurados en Reino Unido sur, utilice `uk.icr.io`
   - Para espacios de nombres configurados en EE.UU. sur, utilice `us.icr.io`

   ```
   docker login -u token -p <token_value> <registry_url>
   ```
   {: pre}

   Para el parámetro `-u`, asegúrese de que escribe la serie `token` y no el ID de la señal.
   {: tip}

   Después de que haya iniciado una sesión en Docker utilizando la señal, puede enviar por push o extraer imágenes a y desde el espacio de nombres.

### Eliminación de una señal desde su cuenta de {{site.data.keyword.Bluemix_notm}} (en desuso)
{: #registry_tokens_remove}

Elimine una señal de {{site.data.keyword.registrylong_notm}} cuando ya no la necesite.
{:shortdesc}

Utilizar señales para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres está en desuso. Utilice claves de API para automatizar el acceso al espacio de nombres, consulte [Automatización del acceso a los espacios de nombres mediante claves de API](#registry_api_key).
{: deprecated}

Las señales caducadas de {{site.data.keyword.registrylong_notm}} se eliminan automáticamente desde su cuenta de {{site.data.keyword.Bluemix_notm}} y no es necesario eliminarlas manualmente.
{:tip}

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

2. Enumere todas las señales de la cuenta de {{site.data.keyword.Bluemix_notm}} y tenga en cuenta el ID de señal que desea eliminar.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. Eliminar la señal.

   ```
   ibmcloud cr token-rm <token_id>
   ```
   {: pre}

## Opciones de autenticación para todos los clientes
{: #registry_authentication}

Puede autenticarse mediante el mandato `docker login` u otros clientes de registro.
{:shortdesc}

La mayoría de los usuarios pueden utilizar el mandato `ibmcloud cr login` para simplificar `docker login`, pero si está implementando la automatización o está utilizando un cliente diferente, es posible que quiera autenticarse manualmente. Debe presentar un nombre de usuario y una contraseña. En {{site.data.keyword.registrylong_notm}}, el nombre de usuario indica el tipo de secreto que se presenta en la contraseña.

Son válidos los siguientes nombres de usuarios:

- `iambearer` La contraseña contiene un señal de acceso a IAM. Este tipo de autenticación es de corta duración, pero puede derivarse de todos los tipos de identidad IAM.
- `iamrefresh` La contraseña debe contener un señal de actualización de IAM que se utiliza internamente para generar y actualizar un señal de acceso a IAM. Este tipo de autenticación es más duradero y es utilizado por el mandato `ibmcloud cr login`.
- `iamapikey` La contraseña es una clave de API de IAM. Este tipo de autenticación es el preferido para la automatización. Puede utilizar una clave de API de usuario o de ID de servicio, consulte [Creación de una clave de API](#registry_api_key_create).
- `token` La contraseña es una señal de registro (en desuso). Puede utilizar este nombre de usuario para la automatización.

  Utilizar señales para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres está en desuso. Utilice claves de API para automatizar el acceso al espacio de nombres, consulte [Automatización del acceso a los espacios de nombres mediante claves de API](#registry_api_key).
  {: deprecated}

No es necesario utilizar el mandato `docker` para autenticarse con el registro. Por ejemplo, puede iniciar apps de Cloud Foundry desde las imágenes del registro utilizando la CLI de Cloud Foundry:

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Sustituya `<apikey>` por su clave de API, `<region>` por el nombre de su [región](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` por su espacio de nombres y `<image_repo>` por el repositorio.

Para obtener más información, consulte [Uso de un registro de imagen privado](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
