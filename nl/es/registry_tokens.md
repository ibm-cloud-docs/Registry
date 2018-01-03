---

copyright:
  years: 2017
lastupdated: "2017-12-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Automatización del acceso a {{site.data.keyword.registrylong_notm}}
{: #registry_access}

Puede utilizar elementos de registro o una clave API (IAM) de {{site.data.keyword.iamlong}} para automatizar el acceso a sus nombres de espacios de {{site.data.keyword.registrylong_notm}} para poder enviar por push y extraer imágenes.
{:shortdesc}

Las claves API están enlazadas a su cuenta y pueden utilizarse en {{site.data.keyword.Bluemix_notm}} sin que necesite distintas credenciales para cada servicio. Puede utilizar la clave de API en el CLI o como parte de la automatización para iniciar sesión como su identidad de usuario.

Los elementos de registro solo abarcan {{site.data.keyword.registrylong_notm}}. Puede limitarlos a un acceso de sólo lectura y puede seleccionar si caducan o no caducan.

Para obtener más información acerca de las claves de API de {{site.data.keyword.registrylong_notm}}, consulte [Trabajar con claves API](../../iam/apikeys.html#manapikey).

Antes de empezar, [instale {{site.data.keyword.registrylong_notm}} y la CLI de Docker](registry_setup_cli_namespace.html#registry_cli_install).


## Acceso automático a sus espacios de nombres mediante el uso de claves API
{: #registry_api_key}

Puede utilizar claves API para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres.
{:shortdesc}

### Creación de una clave API
{: #registry_api_key_create}

Puede crear un clave API que puede utilizar para iniciar sesión en su registro.
{:shortdesc} 

Cree una clave API IAM. consulte  [Creación de una clave API](../../iam/userid_keys.html#creating-an-api-key). 

### Utilización de una clave API para automatizar el acceso
{: #registry_api_key_use}

Puede utilizar una clave API para automatizar el acceso a sus espacios de nombres en {{site.data.keyword.registrylong_notm}}.
{:shortdesc} 

Utilice la clave API para iniciar sesión en su registro mediante la ejecución del siguiente mandato Docker. Substituya &lt;your_apikey&gt; por su clave API, y sustituya &lt;registry_url&gt; con la URL del registro en el que está configurado sus espacios de nombres.

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}


Para obtener información acerca del mandato, consulte [Cree una nueva clave API de plataforma {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_api_key_create).


## Automatizando acceso a sus nombres de espacios utilizando señales
{: #registry_tokens}

Puede utilizar señales para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres {{site.data.keyword.registrylong_notm}}.{:shortdesc}

Cualquiera que tenga una señal de registro puede acceder a la información protegida. Mediante la creación de una señal para su cuenta de {{site.data.keyword.Bluemix_notm}}, se puede otorgar acceso a todos los espacios de nombres que ha configurado en una región para los usuarios fuera de su cuenta de {{site.data.keyword.Bluemix_notm}}. Cada usuario o app en posesión de esta señal puede enviar por push o extraer imágenes a espacios de nombres sin tener que instalar el plug-in container-registry. 

Cuando crea una señal para su cuenta de {{site.data.keyword.Bluemix_notm}}, puede decidir si dicha señal autoriza el acceso de sólo lectura (extraer) o el acceso de escritura (enviar por push y extraer) para el
registro. También puede especificar si una señal es permanente o si ésta caduca después de 24 horas. Puede crear y utilizar varias señales para controlar los diferentes tipos de acceso.

Utilice las siguientes tareas para gestionar sus señales:

-  [Creación de una señal para su cuenta{{site.data.keyword.Bluemix_notm}} ](#registry_tokens_create)
-  [Utilización de una señal para automatizar el acceso a su espacio de nombres ](#registry_tokens_use)
-  [Eliminación de una señal desde su cuenta {{site.data.keyword.Bluemix_notm}}](#registry_tokens_remove)


### Creación de una señal para su cuenta de {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_create}

Puede crear una señal para otorgar acceso a todos los espacios de nombres {{site.data.keyword.registrylong_notm}} en una región. {:shortdesc}

1.  Cree una señal. En el ejemplo siguiente se crea una señal que no caduca que tiene acceso de lectura y escritura a todos los espacios de nombres que se encuentran configurados en una región.

    ```
    bx cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="light bulb icon"/> Descripción de los componentes de este mandato </th>
        </thead>
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
    Identificador de la señal   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad
    Señal              <token_value>
    ```
    {: screen}

2.  Verifique que la señal se ha creado.

    ```
    bx cr token-list
    ```
    {: pre}


### Utilización de una señal para automatizar el acceso a su espacio de nombres 
{: #registry_tokens_use}

Puede utilizar una señal en su mandato `login docker` para automatizar el acceso a sus espacios de nombres en {{site.data.keyword.registrylong_notm}}. Dependiendo de si establece un acceso de sólo lectura o de sólo escritura para la señal, los usuarios pueden enviar por push y extraer imágenes a y desde los espacios de nombres.
{:shortdesc}

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Enumere todas las señales de la cuenta de {{site.data.keyword.Bluemix_notm}} y tenga en cuenta el ID de señal que desea utilizar.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Recupere el valor de la señal para la señal. Sustituya &lt;id_señal&gt; con el ID de la señal.

    ```
    bx cr token-get <token_id>
    ```
    {: pre}

    Su valor de la señal se muestra en **Señal** de la salida de la CLI.

4.  Utilice la señal como parte del mandato `docker login`. Sustituya &lt;valor_señal&gt; por el valor de la señal que ha recuperado en el paso anterior y &lt;url_registro&gt; por el URL en el registro donde los espacios de nombres está configurado.

    -   Para espacios de nombres configurados en EE.UU. Sur: registry.ng.bluemix.net
    -   Para espacios de nombres configurados en UK-Sur: registry.eu-gb.bluemix.net
    -   Para espacios de nombres configurados en EU-Central: registry.eu-de.bluemix.net
    -   Para espacios de nombres configurados en AP Sur: registry.au-syd.bluemix.net

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}

    Después de que haya iniciado una sesión en Docker utilizando la señal, puede enviar por push o extraer imágenes a y desde el espacio de nombres.


### Eliminación de una señal de su cuenta de {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_remove}

Elimina una señal de {{site.data.keyword.registrylong_notm}} cuando ya no se necesita.
{:shortdesc}

**Nota: Las señales ** caducadas {{site.data.keyword.registrylong_notm}} se eliminan automáticamente desde su cuenta de {{site.data.keyword.Bluemix_notm}} y no es necesario eliminarlas manualmente.

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Enumere todas las señales de la cuenta de {{site.data.keyword.Bluemix_notm}} y tenga en cuenta el ID de señal que desea eliminar.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Eliminar la señal.

    ```
    bx cr token-rm <token_id>
    ```
    {: pre}
    


