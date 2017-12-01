---

copyright:
  years: 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Configuración de la CLI de {{site.data.keyword.registrylong_notm}} y del espacio de nombres de registro
{: #registry_setup_cli_namespace}

Para poder almacenar las imágenes de Docker en {{site.data.keyword.registrylong}}, debe instalar la CLI de {{site.data.keyword.Bluemix_notm}} y el plug-in de {{site.data.keyword.registrylong_notm}} y, a continuación, configurar un espacio de nombres de registro para crear su propio repositorio de imágenes en {{site.data.keyword.registrylong_notm}}.
{:shortdesc}


## Instalación del plug-in de CLI de {{site.data.keyword.registrylong_notm}} (`bx cr`)
{: #registry_cli_install}

Instale la CLI de {{site.data.keyword.registrylong_notm}} para utilizar la línea de mandatos para gestionar los espacios de nombres y las imágenes de Docker en el registro privado de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1.  [Instale el plug-in container-registry.](index.html#registry_cli_install)
2.  Opcional: [Configure su cliente de Docker para que ejecute mandatos sin permisos root](https://docs.docker.com/engine/installation/linux/linux-postinstall). Si no lleva a cabo este paso, debe ejecutar los mandatos `bx login`, `bx cr login`, `docker pull`, y `docker push` con **sudo** o como usuario root.

Ahora puede configurar su propio espacio de nombres en el registro privado de {{site.data.keyword.registrylong_notm}}.

## Actualización del plug-in de {{site.data.keyword.registrylong_notm}} (`bx
cr`)
{: #registry_cli_update}

Puede que desee actualizar la CLI de {{site.data.keyword.registrylong_notm}} de forma periódica para utilizar nuevas características.
{:shortdesc}

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Actualice el plug-in container-registry.

    ```
    bx plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  Verifique que el plug-in se ha actualizado correctamente.

    ```
    bx plugin list
    ```
     {: pre}


## Desinstalación del plug-in de {{site.data.keyword.registrylong_notm}} (`bx
cr`)
{: #registry_cli_uninstall}

Si ya no necesita el plug-in container-registry, puede desinstalarlo.
{:shortdesc}

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Desinstale el plug-in container-registry.

    ```
    bx plugin uninstall container-registry
    ```
    {: pre}

3.  Verifique que el plug-in se ha desinstalado correctamente.

    ```
    bx plugin list
    ```
    {: pre}

    El plug-in container-registry no se muestra en los resultados.


## Configuración de un espacio de nombres
{: #registry_namespace_add}

Para almacenar de forma segura las imágenes de Docker, debe crear un espacio de nombres en el registro privado de {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Antes de empezar:

-   [Instale la CLI de {{site.data.keyword.Bluemix_notm}} y el plug-in container-registry](#registry_cli_install).
-   [Planifique cómo utilizar y denominar los espacios de nombres de su registro](registry_overview.html#registry_namespaces).

Para crear un espacio de nombres, consulte [Configure un espacio de nombres](index.html#registry_namespace_add) en la documentación de iniciación.

Ahora puede [enviar por push imágenes de Docker a su espacio de nombres en el registro de {{site.data.keyword.Bluemix_notm}}](registry_images_.html#registry_images_pushing) y compartir estas imágenes con otros usuarios en su cuenta.

## Eliminación de espacios de nombres 
{: #registry_remove}

Si ya no necesita un espacio de nombres de registro, puede eliminar el espacio de nombres de su cuenta de {{site.data.keyword.Bluemix_notm}}.{:shortdesc}

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Enumere espacios de nombres disponibles.

    ```
    bx cr namespace-list
    ```
    {: pre}

3.  Elimine un espacio de nombres. 

    **Atención:** Al eliminar un espacio de nombres, cualquier imagen almacenada en dicho espacio de nombres también se suprimirá. Esta acción no se puede deshacer.
    
    Sustituya _&lt;mi_espaciodenombres&gt;_ por el espacio de nombres que desea eliminar.

    ```
    bx cr namespace-rm <my_namespace>
    ```
    {: pre}

    Después de suprimir un espacio de nombres, en función del número de imágenes que se han almacenado, puede tardar unos minutos antes de que dicho espacio de nombres pase a estar disponible de nuevo para volver a utilizarlo.
