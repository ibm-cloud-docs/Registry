---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

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

La consola de {{site.data.keyword.Bluemix_notm}} incluye una breve Guía de inicio rápido. Para obtener más información para utilizar la consola {{site.data.keyword.Bluemix_notm}}, consulte la [Supervisión de la vulnerabilidad de las imágenes](registry_ui.html).

No coloque información personal en las imágenes de contenedor, nombres de espacio de nombres, campos de descripción (por ejemplo, en señales de registro), o en cualesquiera datos de configuración de imágenes (por ejemplo, nombres de imágenes o etiquetas de imagen).
{:tip}



## Instale de la CLI de {{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1.  Instale la CLI de [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://clis.ng.bluemix.net/ui/home.html) para que pueda ejecutar los mandatos de {{site.data.keyword.Bluemix_notm}} `ibmcloud`.
2.  Instale el plug-in container-registry:

    ```
    ibmcloud plugin install container-registry -r Bluemix
    ```
    {: pre}


## Configure un espacio de nombres
{: #registry_namespace_add}

1.  Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Añada un espacio de nombres para crear su propio repositorio de imágenes. Sustituya _&lt;my_namespace&gt;_ por el espacio de nombres preferido.

    ```
    ibmcloud cr namespace-add <my_namespace>
    ```
    {: pre}

3.  Para asegurar que se ha creado su espacio de nombre, ejecute el mandato `ibmcloud cr namespace-list`.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}




## Extraiga imágenes de otro registro a su máquina local
{: #registry_images_pulling}

1.  [Instale la CLI de Docker ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.docker.com/community-edition#/download). Para Windows 8 u OS X Yosemite 10.10.x o anterior, instale [Docker Toolbox ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.docker.com/toolbox/).

2.  Descargue (_pull_) la imagen en su máquina local. Sustituya _&lt;source_image&gt;_ por el repositorio de la imagen y _&lt;tag&gt;_ por la etiqueta de la imagen que desea utilizar, por ejemplo, _latest_.

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Ejemplo, donde _&lt;source_image&gt;_ es `hello-world` y _&lt;tag&gt;_ es `latest`:

    ```
    docker pull hello-world:latest
    ```
    {: pre}

3.  Etiquete la imagen. Sustituya _&lt;source_image&gt;_ por el repositorio y _&lt;tag&gt;_ por la etiqueta de la imagen local que ha extraído anteriormente. Sustituya _&lt;region&gt;_ por el nombre de su [región](registry_overview.html#registry_regions). Sustituya _&lt;my_namespace&gt;_ por el espacio de nombres que ha creado en [Configure un espacio de nombres](index.html#registry_namespace_add). Defina el repositorio y etiquete la imagen que desea utilizar en el espacio de nombres sustituyendo _&lt;new_image_repo&gt;_ y _&lt;new_tag&gt;_.

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    Ejemplo, donde _&lt;source_image&gt;_ es `hello-world`, _&lt;tag&gt;_ es `latest`, _&lt;region&gt;_ es `eu-gb`, _&lt;my_namespace&gt;_ es `namespace1`, _&lt;new_image_repo&gt;_ es `hw_repo` y _&lt;new_tag&gt;_ es `1`:

    ```
    docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
    ```
    {: pre}



## Envíe por push de imágenes de Docker a su espacio de nombres
{: #registry_images_pushing}

1.  Ejecute el mandato `ibmcloud cr login` para conectar su daemon Docker local en {{site.data.keyword.registrylong_notm}}.

    ```
    ibmcloud cr login
    ```
    {: pre}

2.  Cargue (_push_) la imagen a su espacio de nombres. Sustituya _&lt;my_namespace&gt;_ con el nombre del espacio que ha creado en [Configure un espacio de nombres](index.html#registry_namespace_add), y _&lt;image_repo&gt;_ y _&lt;tag&gt;_ con el repositorio y etiquete la imagen que ha elegido cuando ha etiquetado la imagen.

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    Ejemplo, donde _&lt;region&gt;_ es `eu-gb`, _&lt;my_namespace&gt;_ es `namespace1`, _&lt;image_repo&gt;_ es `hw_repo`, y _&lt;tag&gt;_ es `1`:

    ```
    docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
    ```
    {: pre}

3.  Compruebe que la imagen se ha enviado por push satisfactoriamente ejecutando el siguiente mandato.

    ```
    ibmcloud cr image-list
    ```
    {: pre}


Enhorabuena. Ha configurado un espacio de nombres en {{site.data.keyword.registrylong_notm}} y ha transmitido su primera imagen al espacio de nombres.


**Qué hacer a continuación
**

-   [Gestión de la seguridad de imágenes con Vulnerability Advisor](../va/va_index.html).
-   [Revise sus planes de servicio y el uso de los mismos](registry_overview.html#registry_plans)
-   [Almacene y gestione más imágenes en el espacio de nombres](registry_images_.html).
-   [Configuración de clústeres y nodos de trabajador](/docs/containers/cs_clusters.html#clusters).


