---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-19"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, 

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

# Configuración de la CLI de {{site.data.keyword.registrylong_notm}} y del espacio de nombres de registro
{: #registry_setup_cli_namespace}

Para gestionar sus imágenes de Docker en {{site.data.keyword.registrylong}}, debe instalar el plugin de la CLI de `container-registry` y crear un espacio de nombres.
{:shortdesc}

No coloque información personal en las imágenes de contenedor, nombres de espacio de nombres, campos de descripción (por ejemplo, en señales de registro), o en cualesquiera datos de configuración de imágenes (por ejemplo, nombres de imágenes o etiquetas de imagen).
{: important}

Antes de empezar, instale la CLI de {{site.data.keyword.cloud_notm}}; consulte [Guía de inicio de la CLI de {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started).

## Instalación del plugin de CLI `container-registry`
{: #cli_namespace_registry_cli_install}

Instale el plugin de CLI `container-registry` para utilizar la línea de mandatos para gestionar los espacios de nombres y las imágenes de Docker en {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Instale el plugin de CLI `container-registry`.](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Opcional: [Configure su cliente de Docker para que ejecute mandatos sin permisos root ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.docker.com/install/linux/linux-postinstall/). Si no lleva a cabo este paso, debe ejecutar los mandatos `ibmcloud login`, `ibmcloud cr login`, `docker pull` y `docker push` con `sudo` o como root.

Ahora puede [configurar su propio [espacio de nombres](#registry_namespace_setup) en {{site.data.keyword.registrylong_notm}}.

## Actualización del plugin de CLI `container-registry`
{: #registry_cli_update}

Puede que desee actualizar el plugin de CLI `container-registry` de forma periódica para utilizar nuevas características.
{:shortdesc}

1. Actualice el plugin de CLI `container-registry`.

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. Verifique que el plugin de CLI `container-registry` se ha actualizado correctamente.

    ```
    ibmcloud plugin list
    ```
     {: pre}

## Desinstalación del plugin de CLI `container-registry`
{: #registry_cli_uninstall}

Si ya no necesita el plugin de CLI `container-registry`, puede desinstalarlo.
{:shortdesc}

1. Desinstale el plugin de CLI `container-registry`.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. Verifique que el plugin de CLI `container-registry` se ha desinstalado correctamente.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    El plugin de CLI `container-registry` no se muestra en los resultados.

## Configuración de un espacio de nombres
{: #registry_namespace_setup}

Debe crear un espacio de nombres para almacenar las imágenes de Docker en {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Antes de empezar**

- [Instale la CLI de {{site.data.keyword.cloud_notm}} y el plugin de CLI `container-registry`](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Planifique cómo utilizar y denominar los espacios de nombres de su registro](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces).

Para crear un espacio de nombres, consulte [Configure un espacio de nombres](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add) en la documentación de iniciación.

El espacio de nombres debe ser exclusivo entre todas las cuentas de {{site.data.keyword.cloud_notm}} en la misma región. Los espacios de nombres deben tener entre 4 y 30 caracteres y solo deben contener letras en minúsculas, números, guiones (-) y guiones bajos (_). Los espacios de nombres deben empezar y finalizar con una letra o un número.
{: tip}

Ahora puede [enviar por push imágenes de Docker a su espacio de nombres en {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) y compartir estas imágenes con otros usuarios en su cuenta. Para controlar el acceso a los espacios de nombres en {{site.data.keyword.cloud_notm}} IAM, consulte [Creación de políticas](/docs/services/Registry?topic=registry-user#create).

## Eliminación de espacios de nombres
{: #registry_remove}

Si ya no necesita un espacio de nombres de registro, puede eliminar el espacio de nombres de su cuenta de {{site.data.keyword.cloud_notm}}.
{:shortdesc}

1. Inicie una sesión en {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Enumere espacios de nombres disponibles.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. Elimine un espacio de nombres.

    **Atención:** Al eliminar un espacio de nombres, cualquier imagen almacenada en dicho espacio de nombres también se suprimirá. Esta acción no se puede deshacer.

    Sustituya `<my_namespace>` por el espacio de nombres que desea eliminar.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    Después de suprimir un espacio de nombres, puede tardar unos minutos antes de que dicho espacio de nombres pase a estar disponible de nuevo para volver a utilizarlo.
