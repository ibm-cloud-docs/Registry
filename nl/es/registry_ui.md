---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Supervisión de la vulnerabilidad de las imágenes
{: #registry_ui}

Puede ver información sobre vulnerabilidades potenciales y la seguridad de las imágenes de los repositorios privados y públicos {{site.data.keyword.registrylong}} utilizando la consola de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La columna **INFORME DE SEGURIDAD** muestra la siguiente información acerca de la imagen:
-   `Seguro` No se han encontrado problemas de seguridad.
-   `Vulnerable` Se han encontrado problemas de seguridad o de configuración y deben corregirse antes de que pueda desplegar la imagen.
-   `Incompleto` La exploración no se ha completado. Es posible que la exploración todavía se esté ejecutando o que el sistema operativo de la imagen no sea compatible. Espere y vuelva a intentar realizar la exploración. Si la exploración no se ha completado aún, envíe por push la imagen de nuevo para iniciar una nueva exploración. Las imágenes con exploraciones incompletas no se bloquean para el despliegue.
-   `SO no soportado` El sistema operativo en la imagen no está soportado.

Para visualizar la interfaz gráfica de usuario, siga los siguientes pasos:

1.  Inicie la sesión en la consola de {{site.data.keyword.Bluemix_notm}} ([https://console.bluemix.net](https://console.bluemix.net)) con su IBMid.
2.  Si tiene varias cuentas de {{site.data.keyword.Bluemix_notm}}, seleccione la cuenta y región que desea utilizar desde el menú de la cuenta.
3.  Pulse **Catálogo**.
4.  Seleccione la categoría **Contenedores** y pulse el mosaico **Container Registry**.
5.  Para ver información sobre las imágenes de los repositorios privados, pulse **Repositorios privados**. Se muestra una lista de imágenes de sus repositorios privados y el estado del informe de seguridad de cada imagen. Para obtener más información sobre las vulnerabilidades potenciales, incluidas las etiquetas y el resumen de imágenes, pulse en la fila de la tabla.
6.  Para ver información sobre las imágenes de los repositorios públicos, pulse **Repositorios públicos**. Se muestra una lista de imágenes en los repositorios públicos con un enlace a la documentación y el informe de seguridad de cada imagen. Para obtener más información sobre vulnerabilidades potenciales, incluidas las etiquetas y el resumen de imágenes, pulse en la fila de la tabla.

Para obtener más información sobre el significado de la información reflejada en el informe de seguridad,
consulte [Gestión de la seguridad de imágenes con Vulnerability Advisor](../va/va_index.html).
