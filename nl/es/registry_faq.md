---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, Vulnerability Advisor,

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
{:faq: data-hd-content-type='faq'}

# Preguntas frecuentes (FAQ)
{: #registry_faq}

Preguntas frecuentes sobre {{site.data.keyword.registrylong}}.
{: shortdesc}

## ¿Cómo listo imágenes públicas?
{: #faq_list_public_images}
{: faq}

Para listar imágenes públicas, ejecute los mandatos siguientes de `ibmcloud` para acceder al registro global y listar las imágenes públicas proporcionadas por IBM:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## ¿Puedo utilizar herramientas que no sean docker para crear mis imágenes y enviarlas por push al registro?
{: #faq_tools}
{: faq}

Sí, siempre que la herramienta admita el formato y el protocolo de la imagen OCI.

## ¿Cómo puedo utilizar el control de acceso con IAM?
{: #faq_access_control}
{: faq}

Puede crear políticas de {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) para controlar el acceso a sus espacios de nombres en {{site.data.keyword.registrylong_notm}}. Para obtener más información, consulte [Guía de aprendizaje: Cómo otorgar acceso a los recursos de {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam_access) y [Gestión del acceso de usuario con Identity and Access Management](/docs/services/Registry?topic=registry-iam).

## ¿Qué regiones hay disponibles para {{site.data.keyword.registrylong_notm}}?
{: #faq_regions}
{: faq}

Puede alojar imágenes en [regiones locales](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local). Las imágenes públicas alojadas por IBM están disponibles en el [registro global](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## ¿Por qué recibo el mensaje de error exploración no encontrada en una imagen recién añadida?
{: #faq_va_new_scan_error}
{: faq}

Si obtiene el informe de vulnerabilidades inmediatamente después de añadir una imagen al registro, es posible que reciba el siguiente error:

```
BXNVA0009E:  <imagename> no se ha explorado. Vuelva a intentarlo más tarde.
Si este problema persiste, póngase en contacto con soporte para obtener ayuda;
consulte https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

Este mensaje se recibe porque las imágenes se exploran de forma asíncrona a las solicitudes de resultados, y el proceso de exploración tarda un tiempo en completarse. En circunstancias normales, la exploración se completa unos minutos después de añadir la imagen en el registro, en función de variables como el tamaño de la imagen y la cantidad de tráfico que está recibiendo el registro.

Si recibe este mensaje como parte de un conducto de compilación y el error se produce regularmente, intente añadir alguna lógica de reintento que incluya una breve pausa.

Si sigue experimentando un rendimiento inaceptable, póngase en contacto con soporte, consulte [Obtención de ayuda y soporte para {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-ts_index#gettinghelp).

## ¿Cómo se desencadena una exploración de Vulnerability Advisor?
{: #faq_va_trigger_scan}
{: faq}

La exploración de una imagen se desencadena de una de las siguientes formas:

- Si se envía por push una nueva imagen al registro.
- Si la imagen no se ha explorado durante 7 días, se pone en cola para reexplorar, lo que puede tardar algún tiempo en completarse.
- Si se publica un aviso de seguridad para un paquete instalado en la imagen, se pone en cola para reexplorar, lo que puede tardar algún tiempo en completarse. Las reexploraciones que se desencadenan al publicarse nuevos avisos de seguridad solo están disponibles en imágenes de Ubuntu y Debian.

## ¿Con qué frecuencia se actualizan los avisos de seguridad?
{: #faq_va_update_security_notice}
{: faq}

Los avisos de seguridad para Vulnerability Advisor se cargan desde los sitios del sistema operativo de los proveedores aproximadamente cada 12 horas.
