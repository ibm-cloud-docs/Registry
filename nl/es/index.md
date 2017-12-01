---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Iniciación a {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}} proporciona un registro de imágenes privado multiarrendatario que puede utilizar para almacenar y compartir de forma segura sus imágenes de Docker con usuarios de su cuenta de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La consola de {{site.data.keyword.Bluemix_notm}} incluye una breve Guía de inicio rápido. Para obtener más información sobre cómo utilizar la consola de {{site.data.keyword.Bluemix_notm}}, consulte [Visualización de información sobre imágenes en la consola de {{site.data.keyword.Bluemix_notm}}](registry_ui.html).


## Instale de la CLI de {{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1.  Instale la CLI de [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://clis.ng.bluemix.net/ui/home.html) para que pueda ejecutar los mandatos de {{site.data.keyword.Bluemix_notm}} **bx**.
2.  Instale el plug-in container-registry:

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}


## Configure un espacio de nombres
{: #registry_namespace_add}

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Añada un espacio de nombres para crear su propio repositorio de imágenes. Sustituya _&lt;mi_espaciodenombres&gt;_ por el espacio de nombres preferido.

    ```
    bx cr namespace-add <my_namespace>
    ```
    {: pre}


## Extraiga imágenes de otro registro a su máquina local 
{: #registry_images_pulling}

1.  [Instale la CLI de Docker ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.docker.com/community-edition#/download). Para Windows 8 u OS X Yosemite 10.10.x o anterior, instale [Docker Toolbox ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.docker.com/products/docker-toolbox).

2.  Inicie la sesión en la CLI:

    ```
    bx cr login
    ```
    {: pre}

    **Nota:** Debe iniciar la sesión si extrae una imagen desde su {{site.data.keyword.registrylong_notm}} privado.

3.  Descargue (_pull_) la imagen en su máquina local. Sustituya _&lt;imagen_fuente&gt;_ por el repositorio de la imagen y _&lt;etiqueta&gt;_ por la etiqueta de la imagen que desea utilizar, por ejemplo, _latest_.

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Ejemplo:

    ```
    docker pull hello-world:latest
    ```
    {: pre}

4.  Etiquete la imagen. Sustituya _&lt;imagen_fuente&gt;_ por el repositorio y _&lt;etiqueta&gt;_ por la etiqueta de la imagen local que ha extraído anteriormente. Defina el repositorio y etiquete la imagen que desea utilizar en el espacio de nombres sustituyendo _&lt;nuevo_repo_imagen&gt;_ y _&lt;nueva_etiqueta&gt;_.

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    Ejemplo:

    ```
    docker tag hello-world:latest registry.<region>.bluemix.net/my_namespace/hw_repo:1
    ```
    {: pre}


## Envíe por push de imágenes de Docker a su espacio de nombres 
{: #registry_images_pushing}

1.  Cargue (_push_) la imagen a su espacio de nombres. Sustituya _&lt;mi_espaciodenombres&gt;_ por el espacio de nombres al que desea subir la imagen, y _&lt;repo_imagen&gt;_ y _&lt;etiqueta&gt;_ por el repositorio y la etiqueta de la imagen que ha elegido cuando se ha etiquetado la imagen.

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    Ejemplo:

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/hw_repo:1
    ```
    {: pre}

2.  Compruebe que la imagen se ha enviado por push satisfactoriamente ejecutando el siguiente mandato.

    ```
    bx cr image-list
    ```
    {: pre}


Enhorabuena. Ha configurado un espacio de nombres en {{site.data.keyword.registrylong_notm}} y ha transmitido su primera imagen al espacio de nombres.

**Qué hacer a continuación
**

-   [Gestión de la seguridad de imágenes con Vulnerability Advisor](../va/va_index.html).
-   [Revise sus planes de servicio y el uso de los mismos](registry_overview.html#registry_plans)
-   [Almacene y gestione más imágenes en el espacio de nombres](registry_images_.html).
-   [Cree y despliegue un
contenedor a partir de la imagen en un clúster Kubernetes](../../containers/cs_cluster.html).

