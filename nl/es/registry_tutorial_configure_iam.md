---

copyright:
  years: 2018
lastupdated: "2018-10-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Guía de aprendizaje: Cómo otorgar acceso a los recursos de {{site.data.keyword.registrylong_notm}}
{: #iam_access}

Utilice esta guía de aprendizaje para ver cómo se otorgan acceso a sus recursos mediante la configuración de {{site.data.keyword.iamlong}} (IAM) para {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Esta guía de aprendizaje dura aproximadamente 45 minutos.

**Antes de empezar**

- Siga las instrucciones de [Iniciación a {{site.data.keyword.registrylong_notm}}](/docs/services/Registry/index.html#index).

- Asegúrese de que tiene la versión más reciente del plugin de registro de contenedor para la CLI de {{site.data.keyword.cloud_notm}}; consulte [Actualización del plugin de registro de contenedor](https://console.bluemix.net/docs/services/Registry/registry_setup_cli_namespace.html#registry_cli_update).

- Debe tener acceso a dos cuentas de [ {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/) que puede utilizar para esta guía de aprendizaje, una para el Usuario A y otra para el Usuario B, y cada una debe utilizar una dirección de correo electrónico exclusiva. Trabajará en su propia cuenta, Usuario A, e invitará a otro usuario, Usuario B, a utilizar su cuenta. Puede optar por crear una segunda cuenta de {{site.data.keyword.cloud_notm}}, o puede trabajar con un compañero que tenga una cuenta de {{site.data.keyword.cloud_notm}}.

- Si ha empezado a utilizar {{site.data.keyword.registrylong_notm}} en su cuenta antes del 4 de octubre de 2018, debe habilitar la imposición de políticas de IAM ejecutando el mandato `ibmcloud cr iam-policies-enable`. Si ha invitado a otros usuarios que utilizan sus espacios de nombres de {{site.data.keyword.registrylong_notm}} en su cuenta de IBM Cloud, utilice una cuenta distinta como Usuario A para evitar la interrupción de su acceso.

## Paso 1: Autorizar a un usuario a configurar el registro
{: #configure_registry}

En esta sección, añadirá un segundo usuario a su cuenta y le otorgará la posibilidad de configurar {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Añada el Usuario B a la cuenta del Usuario A:

    1. Inicie una sesión en la cuenta del Usuario A con el mandato siguiente:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Invite al Usuario B a acceder a la cuenta del Usuario A con el mandato siguiente, donde _ `<user.b@example.com>`_ es la dirección de correo electrónico del Usuario B:

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. Obtenga el ID de cuenta del Usuario A con el siguiente mandato:

        ```
        ibmcloud target
        ```
        {: pre}

        Anote el ID de cuenta que está entre paréntesis ( ) en la fila Cuenta.

2. Compruebe que el Usuario B puede dirigirse a la cuenta del Usuario A, pero que aún no puede hacer nada con {{site.data.keyword.registrylong_notm}}:

    1. Inicie una sesión como Usuario B y ejecute el siguiente mandato para elegir como destino la cuenta del Usuario A, donde _`<YourAccountID>`_ es el ID de la cuenta del Usuario A:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Intente editar la cuota de registro en 4 GB de tráfico con el mandato siguiente:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        El mandato falla porque el Usuario B no tiene el acceso adecuado.

3. Otorgue al Usuario B el rol de Gestor para que el Usuario B pueda configurar {{site.data.keyword.registrylong_notm}}:

    1. Vuelva a iniciar la sesión como usted mismo, Usuario A, con el siguiente mandato:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Cree una política que otorgue el rol de Gestor al Usuario B con el mandato siguiente:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. Compruebe que el Usuario B ahora puede cambiar las cuotas en la cuenta del Usuario A:

    1. Inicie una sesión como Usuario B y elija como destino la cuenta del Usuario A con el mandato siguiente:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Intente editar la cuota de registro en 4 GB de tráfico con el mandato siguiente:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        Funciona porque el Usuario B tiene el tipo de acceso adecuado.

    3. Ahora cambie la cuota de nuevo con el mandato siguiente:
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. Limpie:

    1. Vuelva a iniciar la sesión como usted mismo, Usuario A, con el siguiente mandato:
  
        ```
        ibmcloud login
        ```
        {: pre}
  
    2. Obtenga una lista de las políticas para el Usuario B, busque la política que acaba de crear con el siguiente mandato y anote el ID:
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. Suprima la política con el mandato siguiente, donde _ `<Policy_ID>`_ es su ID de política:
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Paso 2: Autorizar a un usuario a acceder a espacios de nombres específicos
{: #access_resources}

En esta sección, creará algunos espacios de nombres con imágenes de ejemplo y otorgará acceso a los mismos. Creará políticas para otorgar distintos roles a cada espacio de nombres y mostrará el efecto.
{:shortdesc}

1. Cree tres nuevos espacios de nombres en la cuenta del Usuario A. Estos espacios de nombres deben ser exclusivos en la región, de modo que utilice sus propios nombres de espacios de nombres; en esta guía de aprendizaje se utiliza `namespace_a`, `namespace_b` y `namespace_c` como ejemplos:

    1. Inicie una sesión como Usuario A con el mandato siguiente:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Cree un espacio de nombres, `namespace_b`, con el siguiente mandato:

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}

        Los nombres de los espacios de nombres deben ser exclusivos en la región.
        {: tip}

    3. Cree otro espacio de nombres, `namespace_c`, con el mandato siguiente:

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. Compruebe que el Usuario B no puede ver nada:

    1. Inicie una sesión como Usuario B y elija como destino la cuenta del Usuario A con el mandato siguiente:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Intente obtener una lista de imágenes como Usuario B con el mandato siguiente:

        ```
        ibmcloud cr images
        ```
        {: pre}

        Devuelve una lista vacía porque el Usuario B no tiene acceso a ninguno de los espacios de nombres.

3. Cree políticas para otorgar al Usuario B la capacidad de interactuar con los espacios de nombres con el mandato siguiente:

    1. Inicie una sesión en la cuenta del Usuario A con el mandato siguiente:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Compruebe que se listan al menos tres espacios de nombres con el mandato siguiente:

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        Se muestran los tres espacios de nombres que ha creado en esta guía de aprendizaje (`namespace_a`, `namespace_b` y `namespace_c`). Si no ve estos espacios de nombres, vuelva y siga las instrucciones para crearlos de nuevo.

    3. Cree una política que otorgue el rol de Lector sobre `namespace_b` al Usuario B con el siguiente mandato, donde _`<Region>`_ es el nombre abreviado de su [región](/docs/services/Registry/registry_overview.html#registry_regions), por ejemplo `us-south`:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource <namespace_b> --roles Reader
        ```
        {: pre}

    4. Cree una segunda política que otorgue los roles Lector y Escritor sobre `namespace_c` al Usuario B con el mandato siguiente:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        Este mandato añade dos roles al mismo recurso en la misma política.
        {: tip}

4. Envíe imágenes a `namespace_a` y a `namespace_b`:

    1. Envíe la imagen `hello-world` con el siguiente mandato:

        ```
        docker pull hello-world
        ```
        {: pre}

    2. Etiquete la imagen para `namespace_a` con el siguiente mandato:

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

    3. Etiquete la imagen para `namespace_b` con el siguiente mandato:

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

    4. Inicie una sesión en {{site.data.keyword.registrylong_notm}} con el siguiente mandato:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Envíe la imagen a `namespace_a` con el siguiente mandato:

        ```
        docker push registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

    6. Envíe la imagen a `namespace_b` con el siguiente mandato:

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

5. Compruebe que el Usuario B puede interactuar con `namespace_b` y con `namespace_c`, pero no con `namespace_a`:

    1. Inicie una sesión como Usuario B con el mandato siguiente:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Muestre que el Usuario B puede ver `namespace_b` y `namespace_c`, pero no `namespace_a` porque el Usuario B no tiene acceso a `namespace_a`, con el siguiente mandato:

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. Obtenga una lista de sus imágenes con el siguiente mandato:

        ```
        ibmcloud cr images
        ```
        {: pre}

        La imagen de `namespace_b` se muestra en la lista, pero la imagen de `namespace_a` no lo hace, porque el Usuario B no tiene acceso a `namespace_a`.

    4. Inicie una sesión en {{site.data.keyword.registrylong_notm}} con el siguiente mandato:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Extraiga la imagen con el siguiente mandato:

        ```
        docker pull registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

    6. Envíe la imagen a `namespace_b` con el siguiente mandato:

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

        Este mandato falla porque el Usuario B no tiene el rol de Escritor en `namespace_b`.

    7. Etiquete la imagen con `namespace_c` con el siguiente mandato:

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

    8. Envíe la imagen a `namespace_c` con el siguiente mandato:

        ```
        docker push registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

        El mandato funciona porque el Usuario B tiene el rol Escritor en `namespace_c`.

    9. Extraiga de `namespace_c` con el siguiente mandato:

        ```
        docker pull registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

        El mandato funciona porque el Usuario B tiene el rol Lector en `namespace_c`.

6. Limpie:

    1. Vuelva a iniciar una sesión en la cuenta del Usuario A con el mandato siguiente:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Obtenga una lista de las políticas para el Usuario B con el mandato siguiente:

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        Busque las políticas que acaba de crear y anote los ID de política.

    3. Suprima las políticas que acaba de crear con el mandato siguiente, donde _ `<Policy_ID>`_ es el ID de política:

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Paso 3: Crear un ID de servicio y otorgar acceso a un recurso
{: #service_id}

En esta sección, configurará un ID de servicio y le otorgará acceso al espacio de nombres de {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Configure un ID de servicio con acceso a {{site.data.keyword.registrylong_notm}} y cree una clave de API para el mismo:

    1. Inicie una sesión en la cuenta del Usuario A con el mandato siguiente:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Cree un ID de servicio llamado `cr-roles-tutorial` con la descripción `"Created during the access control tutorial for Container Registry"` con el siguiente mandato:

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. Cree una política de servicio para el ID de servicio que otorgue el rol de Lector sobre `namespace_a` con el siguiente mandato:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. Cree una segunda política de servicio que otorgue el rol de Escritor sobre `namespace_b` con el mandato siguiente:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. Cree una clave de API para el ID de servicio con el mandato siguiente:

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Utilice Docker para iniciar una sesión con la clave de API del ID de servicio, donde _`<API_Key>`_ es su clave de API, e interactúe con el registro:

    1. Inicie una sesión en {{site.data.keyword.registrylong_notm}} con el siguiente mandato:

        ```
        docker login -u iamapikey -p <API_Key> registry.<Region>.bluemix.net
        ```
        {: pre}

    2. Extraiga la imagen con el siguiente mandato:

        ```
        docker pull registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

        Este mandato funciona.

    3. Envíe su imagen a `namespace_a` con el siguiente mandato:

        ```
        docker push registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

        Este mandato no funciona porque el usuario no tiene el rol de Escritor en `namespace_a`.

    4. Envíe su imagen a `namespace_b` con el siguiente mandato:

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

        Este mandato funciona porque el usuario tiene el rol Escritor en `namespace_b`.

3. Limpie:

    1. Obtenga una lista de sus políticas de servicio con el siguiente mandato:

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        Anote los ID de política.

    2. Suprima las políticas de servicio ejecutando el mandato siguiente para cada política:

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. Suprima el ID de servicio con el mandato siguiente:

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. Vuelva a iniciar una sesión en {{site.data.keyword.registrylong_notm}} como Usuario A:

        ```
        ibmcloud cr login
        ```
        {: pre}

## Paso 4: Limpieza
{: #clean_up}

En esta sección, eliminará los recursos que ha creado en las secciones anteriores para dejar la cuenta tal como estaba al principio de esta guía de aprendizaje.
{:shortdesc}

1. Inicie una sesión en su cuenta con el mandato siguiente:

    ```
    ibmcloud login
    ```
    {: pre}

2. Suprima `namespace_a`, `namespace_b` y `namespace_c` ejecutando los mandatos siguientes:

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. Elimine el Usuario B de su cuenta con el mandato siguiente:

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

¡Enhorabuena! Ha completado correctamente esta guía de aprendizaje.
