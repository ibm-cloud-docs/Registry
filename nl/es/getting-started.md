---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security, cli, namespaces, tutorial, Docker, images, registry

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

# Guía de aprendizaje de iniciación
{: #getting-started}

{{site.data.keyword.registrylong}} proporciona un registro de imágenes privado multiarrendatario que puede utilizar para almacenar y compartir sus imágenes de Docker con usuarios de su cuenta de {{site.data.keyword.cloud_notm}}.
{:shortdesc}

La consola de {{site.data.keyword.cloud_notm}} incluye una breve Guía de inicio rápido. Para obtener más información sobre cómo utilizar la consola de {{site.data.keyword.cloud_notm}}, consulte [Gestión de la seguridad de imágenes con Vulnerability Advisor](/docs/services/va?topic=va-va_index).

No coloque información personal en las imágenes de contenedor, nombres de espacio de nombres, campos de descripción, o en cualesquiera datos de configuración de imágenes (por ejemplo, nombres de imágenes o etiquetas de imagen).
{: important}

## Instale de la CLI de {{site.data.keyword.registrylong_notm}}
{: #gs_registry_cli_install}

1. Instale la CLI de {{site.data.keyword.cloud_notm}} para poder ejecutar los mandatos de
{{site.data.keyword.cloud_notm}} `ibmcloud`; consulte [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started). Esta instalación también instala los plugins de CLI para {{site.data.keyword.containerlong_notm}} y {{site.data.keyword.registrylong_notm}}.

## Configure un espacio de nombres
{: #gs_registry_namespace_add}

1. Inicie una sesión en {{site.data.keyword.cloud_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

   Si tiene un ID federado, inicie sesión con el mandato siguiente:

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. Añada un espacio de nombres para crear su propio repositorio de imágenes. Sustituya `<my_namespace>` por el espacio de nombres que desee.

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

   El espacio de nombres debe ser exclusivo entre todas las cuentas de {{site.data.keyword.cloud_notm}} en la misma región. Los
espacios de nombres deben tener entre 4 y 30 caracteres y solo deben contener letras en minúsculas, números, guiones (-)
y guiones bajos (_). Los espacios de nombres deben empezar y finalizar con una letra o un número.
   {: tip}

3. Para asegurar que se ha creado su espacio de nombre, ejecute el mandato `ibmcloud cr namespace-list`.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Extraiga imágenes de otro registro a su máquina local
{: #gs_registry_images_pulling}

1. [Instale la CLI de Docker Engine ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.docker.com/products/container-runtime#/download). Para Windows 8 u OS X Yosemite 10.10.x o anterior, instale [Docker Toolbox ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.docker.com/toolbox/). {{site.data.keyword.registrylong_notm}} es compatible con Docker Engine v1.12.6 o posterior.

2. Descargue (_pull_) la imagen en su máquina local. Sustituya `<source_image>` por el repositorio de la imagen y `<tag>` por la etiqueta de la imagen que desea utilizar, como por ejemplo _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Ejemplo, donde `<source_image>` es `hello-world` y `<tag>` es `latest`:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Etiquete la imagen. Sustituya `<source_image>` por el repositorio y `<tag>` por la etiqueta de la imagen local que ha extraído antes. Sustituya `<region>` por el nombre de su [región](/docs/services/Registry?topic=registry-registry_overview#registry_regions). Sustituya `<my_namespace>` por el espacio de nombres que ha creado en el apartado [Configurar un espacio de nombres](#gs_registry_namespace_add). Defina el repositorio y la etiqueta de la imagen que desea utilizar en el espacio de nombres sustituyendo `<new_image_repo>` y `<new_tag>`.

   ```
   docker tag <source_image>:<tag> <region>.icr.io/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Para encontrar el nombre de su región, ejecute el mandato `ibmcloud cr region`.
   {: tip}

   Ejemplo, donde `<source_image>` es `hello-world`, `<tag>` es `latest`, `<region>` es `uk`, `<my_namespace>` es `namespace1`, `<new_image_repo>` es `hw_repo` y `<new_tag>` es `1`:

   ```
   docker tag hello-world:latest uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

## Envíe por push de imágenes de Docker a su espacio de nombres
{: #gs_registry_images_pushing}

1. Ejecute el mandato `ibmcloud cr login` para conectar su daemon Docker local en {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Cargue (_push_) la imagen a su espacio de nombres. Sustituya `<my_namespace>` por el espacio de nombres que ha creado en el apartado [Configurar un espacio de nombres](#gs_registry_namespace_add) y `<image_repo>` y `<tag>` por el repositorio y la etiqueta de la imagen que ha elegido al etiquetar la imagen.

   ```
   docker push <region>.icr.io/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}
   
   Ejemplo, donde `<region>` es `uk`, `<my_namespace>` es `namespace1`, `<image_repo>` es `hw_repo` y `<tag>` es `1`:

   ```
   docker push uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

3. Compruebe que la imagen se ha enviado por push satisfactoriamente ejecutando el siguiente mandato.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Enhorabuena. Ha configurado un espacio de nombres en {{site.data.keyword.registrylong_notm}} y ha transmitido su primera imagen al espacio de nombres.

## Pasos siguientes
{: #gs_get_start_next}

- [Gestión de la seguridad de imágenes con Vulnerability Advisor](/docs/services/va?topic=va-va_index)
- [Revise sus planes de servicio y el uso de los mismos](/docs/services/Registry?topic=registry-registry_overview#registry_plans)
- [Almacene y gestione más imágenes en el espacio de nombres](/docs/services/Registry?topic=registry-registry_images_)
- [Definición de políticas de rol de acceso de usuario](/docs/services/Registry?topic=registry-user#user)
- [Configuración de clústeres y nodos de trabajador](/docs/containers?topic=containers-clusters#clusters)
