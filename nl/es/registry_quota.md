---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: IBM Cloud Container Registry, quota limits, custom quota limits, pull traffic, quotas, storage,

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

# Gestión de los límites de cuota para almacenamiento y tráfico de extracción
{: #registry_quota}

Puede limitar la cantidad de almacenamiento y de tráfico de extracción que se pueda utilizar en su cuenta de {{site.data.keyword.cloud}} estableciendo y gestionando límites de cuota personalizados.
{:shortdesc}

## Establecimiento de límites de cuota para almacenar y extraer imágenes
{: #registry_quota_set}

Puede limitar la cantidad de almacenamiento y de tráfico de extracción de sus imágenes privadas estableciendo sus propios límites de cuota.
{:shortdesc}

Cuando actualice al plan estándar de {{site.data.keyword.registryshort_notm}},
benefíciese de una cantidad ilimitada de almacenamiento y tráfico de extracción para sus imágenes privadas. Para no superar el nivel de pago que elija, puede establecer cuotas individuales para la cantidad de almacenamiento y el tráfico de extracción. Los límites de cuota se aplican a todos los espacios de nombres que haya configurado en {{site.data.keyword.registrylong_notm}}. Si utiliza el plan de servicio gratuito, también puede establecer cuotas personalizadas dentro de la cantidad gratuita de almacenamiento y tráfico de extracción.

Para establecer una cuota:

1. Inicie una sesión en {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Revise los límites de cuota actuales correspondientes a almacenamiento y tráfico de extracción.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    La salida es parecida a la siguiente.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

3. Cambie el límite de cuota para almacenamiento y tráfico de extracción. Para cambiar el uso de tráfico de extracción, especifique la opción **traffic** y sustituya
`<traffic_quota>` por el valor en megabytes que desea establecer para la cuota del tráfico de extracción. Si desea cambiar la cantidad de almacenamiento de su cuenta, especifique la opción **storage** y sustituya `<storage_quota>` por el valor en megabytes que desea establecer.

    Si tiene el plan gratuito, no puede establecer su cuota en una cantidad que supere el nivel gratuito. La concesión del nivel gratuito para el almacenamiento es de 512 MB y, para el tráfico, de 5120 MB.
    {:tip}

    ```
    ibmcloud cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    Ejemplo para establecer su límite de cuota para el almacenamiento en 600 megabytes y el tráfico de extracción en 7000 megabytes:

    ```
    ibmcloud cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}

## Revisión de los límites de cuota y del uso para almacenar y extraer imágenes
{: #registry_quota_get}

Puede revisar los límites de cuota y comprobar el almacenamiento actual y el uso de tráfico de extracción correspondiente a su cuenta.
{:shortdesc}

1. Inicie una sesión en {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Revise los límites de cuota actuales correspondientes a almacenamiento y tráfico de extracción.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    La salida es parecida a la siguiente.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

## Liberación de almacenamiento utilizado y cambio de planes de servicio o de límites de cuota para mantenerse dentro de los límites de cuota
{: #registry_quota_freeup}

Si ha superado los límites de cuota establecidos para su cuenta de {{site.data.keyword.cloud_notm}}, puede liberar almacenamiento y cambiar el plan de servicio o los límites de cuota para seguir transfiriendo y extrayendo imágenes del espacio de nombres.
{:shortdesc}

Para liberar almacenamiento de imágenes en la cuenta de {{site.data.keyword.cloud_notm}}:

1. Obtenga una lista de todas las imágenes de todos los espacios de nombres de la cuenta de {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud cr images
    ```
    {: pre}

2. Elimine una imagen del espacio de nombres. Sustituya Replace `<image_name>` por el nombre de la imagen que desea eliminar.

    ```
    ibmcloud cr image-rm <image_name>
    ```
    {: pre}

    En función del tamaño de la imagen, es posible que la imagen tarde un rato en eliminarse y en dejar almacenamiento disponible.
    {:tip}

3. Revise el uso de la cuota de almacenamiento.

    ```
    ibmcloud cr quota
    ```
    {: pre}

4. No puede reducir el uso del tráfico de extracción en un periodo de facturación.
   {:tip}

    Para seguir extrayendo imágenes de los espacios de nombres, elija una de las siguientes opciones.

    - Espere a que comience el siguiente ciclo de facturación.
    - Si tiene un plan gratuito, [actualice al plan de servicio estándar](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade).
    - Si ya tiene un plan estándar, [establezca nuevos límites de cuota para el tráfico de extracción](#registry_quota_set).
