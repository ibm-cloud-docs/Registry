---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# Retención de imágenes
{: #registry_retention}

Puede decidir si suprimir o retener imágenes.
{:shortdesc}

## Planificar la retención
{: #retention_plan}

El mandato [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) opera para cada espacio de nombres, así pues, utilizar varios espacios de nombres en el conducto significa que puede aplicar criterios de retención distintos de la forma que mejor se ajuste a sus necesidades.

Imaginemos un conducto de entrega típico con entornos de desarrollo, transferencia y producción. A medida que se entrega el código, la integración continua y el despliegue continuo envía imágenes al registro y las despliega directamente en el entorno de desarrollo. Después del período de pruebas, algunas compilaciones ascienden del entorno de desarrollo al de transferencia y después, potencialmente, al de producción. Es este escenario, la velocidad de cambio de imágenes es más rápido en el entorno de desarrollo y más lento en el de producción. Si todos los entornos extraen imágenes del mismo espacio de nombres, puede resultar difícil elegir un número adecuado de imágenes a retener, debido a esta diferencia de velocidad.

Un buen método es entregar todas las imágenes en un espacio de nombres de desarrollo, por ejemplo `project-development`, y después utilizar el mandato [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) para etiquetar la imagen en otro espacio de nombres cuando ascienda a un estado más elevado del conducto. En el ejemplo anterior, puede tener tres espacios de nombres: desarrollo, `project-development`, transferencia, `project-staging`, y producción, `project-production`. Al ascender de desarrollo a transferencia, las imágenes se etiquetan, desde el espacio de nombres `project-development` al espacio de nombres `project-staging` y las imágenes del espacio de nombres `project-staging` se utilizan para el despliegue. De forma similar, al ascender de transferencia a producción, las imágenes se etiquetan desde el espacio de nombres `project-staging` al espacio de nombres `project-production` y las imágenes del espacio de nombres `project-production` se utilizan en el despliegue de producción.

Utilizando esta técnica obtiene las siguientes ventajas:

* Puede elegir distintos valores de retención para los espacios de nombres de desarrollo, transferencia y producción.
* Se minimizan las posibilidades de eliminar accidentalmente una imagen que se pueda estar utilizando en los entornos de transferencia o de producción, contrariamente a cuando se utiliza un solo espacio de nombres para todas las imágenes.
* Se pueden utilizar distintas políticas de [IAM](/docs/services/Registry?topic=registry-iam). Por ejemplo, puede tener un acceso más restrictivo para las imágenes de producción.
* Se pueden firmar imágenes de producción y dejar las imágenes de desarrollo y transferencia sin firmar.

## Limpiar los espacios de nombres reteniendo únicamente las imágenes que cumplan unos criterios
{: #retention_images}

Retener imágenes de cada uno de los repositorios de {{site.data.keyword.registrylong_notm}} según los criterios especificados. Todas las demás imágenes del espacio de nombres se suprimen.
{:shortdesc}

El mandato [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) da una lista de las imágenes que se van a suprimir y ofrece la opción de cancelar antes de la supresión.

Cuando se hace referencia a una imagen desde varias etiquetas, dentro de un mismo repositorio, esa imagen sólo se cuenta una vez. Se retienen las imágenes más nuevas. La antigüedad viene determinada por el momento en que se creó la imagen, no por el momento en que se envió al registro.
{: tip}

La supresión de una imagen no se puede deshacer. La supresión de una imagen que un despliegue existente utiliza puede provocar que un escalado, una replanificación, o ambas tareas, fallen.
{: important}

Para reducir el número imágenes de cada repositorio del espacio de nombres utilizando la CLI, complete los pasos siguientes:

1. Inicie sesión en {{site.data.keyword.cloud_notm}} con el mandato `ibmcloud login`.
2. Elija el registro en el que desea limpiar las imágenes ejecutando el mandato siguiente y seleccionando la región adecuada:

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. Para retener algunas imágenes y suprimir las demás, ejecute el mandato siguiente:

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   Donde `IMAGECOUNT` es el número de imágenes que desea retener para cada repositorio del espacio de nombres, `NAMESPACE`.

3. Verifique que las imágenes se han suprimido ejecutando el mandato siguiente y compruebe que no aparecen en la lista.

   ```
   ibmcloud cr image-list
   ```
   {: pre}
