---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-19"


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

La columna **Estado de seguridad** muestra la siguiente información acerca de la imagen:
- `Seguro` No se han encontrado problemas de seguridad.
- `Vulnerable` Se han encontrado problemas de seguridad o de configuración y deben corregirse antes de que pueda desplegar la imagen.
- `Incompleto` La exploración no se ha completado. Es posible que la exploración todavía se esté ejecutando o que el sistema operativo de la imagen no sea compatible. Espere y vuelva a intentar realizar la exploración. Si la exploración no se ha completado aún, envíe por push la imagen de nuevo para iniciar una nueva exploración. Las imágenes con exploraciones incompletas no se bloquean para el despliegue.
- `SO no soportado` El sistema operativo en la imagen no está soportado.

Para visualizar la interfaz gráfica de usuario, siga los siguientes pasos:

1. Inicie la sesión en la consola de {{site.data.keyword.Bluemix_notm}} ([https://console.bluemix.net ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net)) con su IBMid.
2. Si tiene varias cuentas de {{site.data.keyword.Bluemix_notm}}, seleccione la cuenta y región que desea utilizar desde el menú de la cuenta.
3. Pulse **Catálogo**.
4. Seleccione la categoría **Contenedores** y pulse el mosaico **Container Registry**.
5. Para ver información sobre las imágenes de los repositorios privados, pulse **Imágenes**. Se muestra una lista de imágenes de sus repositorios privados y el estado de seguridad de cada imagen.
6. Para obtener más información sobre las vulnerabilidades potenciales, incluidas las etiquetas y el resumen de imágenes, pulse en la fila de la imagen en la tabla. Se abre el separador **Detalles de imagen**.
7. Para obtener información sobre los problemas por tipo, pulse el separador **Problemas por tipo**.
8. Para obtener información sobre los contenedores asociados, pulse el separador **Contenedores asociados**.

Para obtener más información sobre el significado de la información reflejada en el informe de seguridad,
consulte [Gestión de la seguridad de imágenes con Vulnerability Advisor](/docs/services/va/va_index.html).
