---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

# Automatización del acceso a {{site.data.keyword.registrylong_notm}}
{: #registry_access}

Puede utilizar una clave de API de {{site.data.keyword.iamlong}} (IAM) para automatizar el acceso a sus espacios de nombres de {{site.data.keyword.registrylong_notm}} para poder enviar por push y extraer imágenes.
{:shortdesc}

¿Está intentando utilizar las imágenes de registro en despliegues de Kubernetes? Consulte [Acceso a imágenes en otros espacios de nombres de Kubernetes, regiones de {{site.data.keyword.cloud_notm}} y cuentas](/docs/containers?topic=containers-images#other).
{: tip}

Las claves de API están enlazadas a su cuenta y pueden utilizarse en {{site.data.keyword.cloud_notm}} sin que necesite distintas credenciales para cada servicio. Puede utilizar la clave de API en la CLI o como parte de la automatización para iniciar sesión como su identidad de usuario.

Si utiliza una clave de API, puede controlar el acceso a los espacios de nombres utilizando las políticas de IAM. Para obtener más información, consulte [Definición de políticas de rol de acceso de usuario](/docs/services/Registry?topic=registry-user#user).

Para obtener más información acerca de las claves de API de {{site.data.keyword.registrylong_notm}}, consulte [Cómo trabajar con claves de API](/docs/iam?topic=iam-manapikey#manapikey).

Antes de empezar, [instale {{site.data.keyword.registrylong_notm}} y la CLI de Docker](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Acceso automático a sus espacios de nombres mediante el uso de claves de API
{: #registry_api_key}

Puede utilizar claves de API para automatizar el envío por push y la extracción de imágenes Docker a y desde los espacios de nombres.
{:shortdesc}

### Creación de una clave de API
{: #registry_api_key_create}

Puede crear un clave de API que puede utilizar para iniciar sesión en su registro.
{:shortdesc}

Puede crear tanto claves de API de usuario como claves de API de ID de servicio.

- Para crear una clave de API de ID de servicio, consulte [Creación de una clave de API para un ID de servicio](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
- Para crear una clave de API de usuario, consulte [Creación de una clave de API](/docs/iam?topic=iam-userapikey#create_user_key).

### Utilización de una clave de API para automatizar el acceso
{: #registry_api_key_use}

Puede utilizar una clave de API para automatizar el acceso a sus espacios de nombres en {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Utilice la clave de API para iniciar sesión en su registro mediante la ejecución del siguiente mandato Docker. Substituya `<your_apikey>` por su clave de API y `<registry_url>` por el URL del registro en el que está configurado sus espacios de nombres.

- Para espacios de nombres configurados en AP-North, utilice `jp.icr.io`
- Para espacios de nombres configurados en AP sur, utilice `au.icr.io`
- Para espacios de nombres configurados en UE central, utilice `de.icr.io`
- Para espacios de nombres configurados en Reino Unido sur, utilice `uk.icr.io`
- Para espacios de nombres configurados en EE.UU. sur, utilice `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Para obtener información acerca del mandato, consulte [Creación de una nueva clave de API de plataforma {{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Opciones de autenticación para todos los clientes
{: #registry_authentication}

Puede autenticarse mediante el mandato `docker login` u otros clientes de registro.
{:shortdesc}

La mayoría de los usuarios pueden utilizar el mandato `ibmcloud cr login` para simplificar `docker login`, pero si está implementando la automatización o está utilizando un cliente diferente, es posible que quiera autenticarse manualmente. Debe presentar un nombre de usuario y una contraseña. En {{site.data.keyword.registrylong_notm}}, el nombre de usuario indica el tipo de secreto que se presenta en la contraseña.

Son válidos los siguientes nombres de usuarios:

- `iambearer` La contraseña contiene un señal de acceso a IAM. Este tipo de autenticación es de corta duración, pero puede derivarse de todos los tipos de identidad IAM.
- `iamrefresh` La contraseña debe contener un señal de actualización de IAM que se utiliza internamente para generar y actualizar un señal de acceso a IAM. Este tipo de autenticación es más duradero y es utilizado por el mandato `ibmcloud cr login`.
- `iamapikey` La contraseña es una clave de API de IAM. Este tipo de autenticación es el preferido para la automatización. Puede utilizar una clave de API de usuario o de ID de servicio, consulte [Creación de una clave de API](#registry_api_key_create).

No es necesario utilizar el mandato `docker` para autenticarse con el registro. Por ejemplo, puede iniciar apps de Cloud Foundry desde las imágenes del registro utilizando la CLI de Cloud Foundry:

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Sustituya `<apikey>` por la clave de API, `<region>` por el nombre de su [región](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` por su espacio de nombres y `<image_repo>` por el repositorio.

Para obtener más información, consulte [Uso de un registro de imagen privado](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
