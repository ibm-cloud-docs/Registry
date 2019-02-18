---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolución de problemas
{: #ts_index}

Aquí encontrará las respuestas a las preguntas más comunes sobre la resolución de problemas acerca de cómo utilizar {{site.data.keyword.registrylong}}.
{:shortdesc}

## Obtención de ayuda y soporte para {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Si tiene problemas o preguntas cuando utiliza {{site.data.keyword.registrylong_notm}}, puede obtener ayuda buscando información o planteando preguntas a través de un foro. También puede abrir una incidencia de soporte de {{site.data.keyword.IBM_notm}}.

Cuando utilice los foros para formular una pregunta, etiquete la pregunta de manera que la vea el equipo de desarrollo de {{site.data.keyword.registrylong_notm}}.

- Si tiene preguntas técnica sobre cómo desarrollar o desplegar una app con {{site.data.keyword.registrylong_notm}}, publique su pregunta en [Stack Overflow ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://stackoverflow.com/search?q=+ibm-bluemix) y etiquete la pregunta con `ibm-bluemix` y `container-registry`.
- Para formular preguntas sobre el servicio y obtener instrucciones de iniciación, utilice el foro [IBM developerWorks dW Answers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Incluya las etiquetas `bluemix` y `container-registry`.

Consulte [Utilización del Centro de soporte](/docs/get-support/howtogetsupport.html#using-avatar) para obtener más detalles sobre el uso de los foros.

Para obtener información sobre cómo abrir una incidencia de soporte de {{site.data.keyword.IBM_notm}} o sobre los niveles de soporte y las gravedades de las incidencias, consulte [¿Cómo puedo obtener la ayuda que necesito?](/docs/get-support/howtogetsupport.html#getting-customer-support)

## Falla el inicio de sesión en {{site.data.keyword.registrylong_notm}}
{: #ts_login}

No se puede iniciar la sesión en {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
El mandato `ibmcloud cr login` falla.

{: tsCauses}

- El plugin de CLI `container-registry` no está actualizado y debe actualizarse.
- Docker no está instalado en el sistema local o no está en ejecución.
- Han caducado sus credenciales de inicio de sesión en {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
Puede solucionar este problema de las siguientes maneras:

- Actualice a la versión más reciente del plugin de CLI `container-registry`, consulte [Actualización del plugin de CLI `container-registry`](/docs/services/Registry/registry_setup_cli_namespace.html#registry_cli_update).
- Asegúrese de que Docker esté instalado en el sistema. Si ya está instalado, reinicie el daemon de Docker.
- Vuelva a ejecutar el mandato `ibmcloud login` para renovar las credenciales de inicio de sesión en {{site.data.keyword.Bluemix_notm}}.

## La ejecución de cualquier mandato para {{site.data.keyword.registrylong_notm}} falla con `FAILED You are not logged in to IBM Cloud. `
{: #ts_login_cloud}

No puede ejecutar ningún mandato en {{site.data.keyword.registrylong_notm}}, aunque haya iniciado sesión en {{site.data.keyword.Bluemix_notm}}.

{: tsSymptoms}
Todos los mandatos `ibmcloud cr` fallarán.

{: tsCauses}

- El plugin de CLI `container-registry` no está actualizado y debe actualizarse.

{: tsResolve}
Puede solucionar este problema de la siguiente manera:

- Actualice a la versión más reciente del plugin de CLI `container-registry`, consulte [Actualización del plugin de CLI `container-registry`](/docs/services/Registry/registry_setup_cli_namespace.html#registry_cli_update).

## Los mandatos de {{site.data.keyword.registrylong_notm}} fallan con `'cr' no es un mandato registrado. Consulte 'ibmcloud help'. `
{: #ts_login_error}

No puede ejecutar un mandato `ibmcloud cr` porque `cr` no es un mandato `ibmcloud` registrado.

{: tsSymptoms}
Puede ver un error similar a uno de los mensajes de error siguientes:

```
ibmcloud cr login
'cr' no es un mandato registrado. Consulte 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' no es un mandato registrado. Consulte 'ibmcloud help'.
```
{: pre}

{: tsCauses}

- El plugin de CLI `container-registry` no está instalado.

{: tsResolve}
Puede solucionar este problema de la siguiente manera:

- Instale el plugin de CLI `container-registry`. Consulte [Instalación del plugin de CLI `container-registry`](/docs/services/Registry/registry_setup_cli_namespace.html#registry_cli_install).

## El mandato `ibmcloud cr build` falla
{: #ts_build_fails}

{: tsSymptoms}
El mandato de construcción falla.

{: tsCauses}
Puede que el servidor esté inactivo o que haya problemas con el Dockerfile.

{: tsResolve}
Para averiguar la causa, ejecute `docker build` localmente con las opciones correspondientes de [`docker build` ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.docker.com/engine/reference/commandline/build/):

```
docker build --no-cache .
```
{:  pre}

- Si la compilación local no funciona, compruebe si existe algún problema con el Dockerfile.
- Si la compilación local funciona, [póngase en contacto con el equipo de soporte de {{site.data.keyword.Bluemix_notm}}](/docs/get-support/howtogetsupport.html#getting-customer-support).

## Error de configuración de un espacio de nombres
{: #ts_problem}

{: tsSymptoms}
Cuando ejecuta `ibmcloud cr namespace-add`, no puede establecer el valor especificado como el espacio de nombres.

{: tsCauses}

- Ha especificado un valor de espacio de nombres que ya está siendo utilizado por otra organización de {{site.data.keyword.Bluemix_notm}}.
- Un espacio de nombres se ha suprimido recientemente y está reutilizando su nombre. Si el espacio de nombres suprimido contenía muchos recursos, es posible que {{site.data.keyword.registrylong_notm}} no haya procesado por completo la supresión.
- Ha utilizado caracteres no válidos en el valor del espacio de nombres.

{: tsResolve}
Puede solucionar este problema de las siguientes maneras:

- Siga las instrucciones que aparecen en el mensaje de error devuelto.
- Compruebe que ha especificado un espacio de nombres válido:
  - Su espacio de nombres debe tener entre 4 y 30 caracteres.
  - El espacio de nombres debe empezar por al menos una letra o un número.
  - Su espacio de nombres debe contener letras minúsculas, números, o subrayados (_) sólo.
- Elija otro valor para el espacio de nombres.
- Si va a volver a crear un espacio de nombres que se ha suprimido y que contenía muchas imágenes, inténtelo de nuevo más tarde.

## La transferencia o extracción de una imagen de Docker falla
{: #ts_pushpull}

{: tsSymptoms}
Cuando ejecuta mandatos para transferir o extraer imágenes de Docker, recibe un mensaje de error. El mensaje de error varía en función de la causa raíz. Los mensajes de error pueden ser:

```
Ha superado la cuota de almacenamiento. Suprima una o varias imágenes, o bien revise su cuota de almacenamiento y el plan de precios
```
{: screen}

```
Ha superado la cuota de tráfico de extracción para el mes actual.
Revise la cuota del tráfico de extracción y el plan de precios
```
{: screen}

```
no autorizado: se necesita autenticación
```
{: screen}

```
denegado: se ha denegado el acceso al recurso
```
{: screen}

{: tsCauses}

- Docker no está instalado.
- El cliente de Docker no ha iniciado sesión en {{site.data.keyword.registrylong_notm}}.
- Es posible que la señal de acceso a {{site.data.keyword.Bluemix_notm}} haya caducado.
- Ha superado el límite de cuota para almacenamiento o tráfico de extracción establecido para su cuenta de {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
Puede solucionar este problema de las siguientes maneras:

- [Asegúrese de que Docker esté instalado en el sistema](/docs/services/Registry/index.html#registry_cli_install).
- Compruebe la vía de acceso de instalación de Docker.
- Inicie una sesión en {{site.data.keyword.Bluemix_notm}} con el mandato `ibmcloud login`. Luego inicie una sesión en la CLI de {{site.data.keyword.registrylong_notm}} con el mandato `ibmcloud cr login`.
- [Revisión de los límites de cuota y del uso para almacenar y extraer imágenes de Docker en {{site.data.keyword.registrylong_notm}}](/docs/services/Registry/registry_quota.html#registry_quota_get).

## No se puede extraer la imagen más reciente utilizando la etiqueta `latest`
{: #ts_docker_latest}

{: tsSymptoms}
Está intentando ejecutar el mandato `docker pull`, pero devuelve una versión de la imagen que no es la más reciente.

{: tsCauses}
La etiqueta `latest` se aplica de forma predeterminada para hacer referencia a una imagen cuando se ejecutan mandatos de Docker sin especificar el valor de etiqueta. La etiqueta `latest` se aplica al mandato `docker build` o `docker tag` más reciente que se ha ejecutado sin un valor de etiqueta establecido de forma explícita. Por lo tanto, se pueden ejecutar mandatos `docker` desordenados o establecer de forma explícita etiquetas sobre algunas imágenes y la etiqueta `latest` para hacer referencia a una compilación que no se sea la más reciente.

{: tsResolve}
Generalmente es mejor definir de forma explícita una etiqueta secuencial para las imágenes cada vez, y no confiar en la etiqueta `latest`.

## No se pueden añadir otras imágenes de IBM al registro
{: #ts_ppa}

{: tsSymptoms}
Al intentar importar contenido utilizado en otros productos de IBM, como por ejemplo {{site.data.keyword.Bluemix_notm}} Private, no podrá almacenar las imágenes y otro software bajo licencia de [IBM Passport Advantage ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/software/passportadvantage/index.html) en el registro.

{: tsCauses}
Los paquetes de software como las imágenes y las gráficas de Helm de IBM Passport Advantage deben importarse en el registro con el mandato `ibmcloud cr ppa-archive-load`.

{: tsResolve}
**Antes de empezar**

- Inicie sesión en {{site.data.keyword.Bluemix_notm}} con el mandato `ibmcloud login [--sso]`.
- Inicie sesión en {{site.data.keyword.registrylong_notm}} con el mandato `ibmcloud cr login`.
- [Establezca la CLI de `kubectl`](/docs/containers/cs_cli_install.html#cs_cli_configure) en el clúster.
- Si aún no ha establecido Helm en el clúster, [configure Helm en el clúster ahora](/docs/containers/cs_integrations.html#helm).
- Si desea compartir las gráficas dentro de la organización, puede instalar el [proyecto de código abierto de Chart Museum ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum). Para obtener instrucciones, consulte este [enlace de developerWorks ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/).

### Importación de productos de IBM Passport Advantage para utilizarlos en {{site.data.keyword.Bluemix_notm}}
{: #ts_ppa_import}

1. Obtenga el archivo comprimido que desea importar de [IBM Passport Advantage![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/software/passportadvantage/index.html).

2. Establezca la región que desee utilizar. Si no sabe el nombre de la región, ejecute el mandato sin la región y luego elija una.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

3. Importe el archivo de archivado comprimido. Especifique la vía de acceso al archivo comprimido y el espacio de nombres de registro al que desea enviar las imágenes.

   ```
   ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
   ```
   {: pre}

   Este mandato expande el archivo comprimido, carga cualquier imagen contenida en el cliente de Docker local, y a continuación envía las imágenes al espacio de nombres del registro.

   Si desea cargar las gráficas de Helm desde el archivado de IBM Passport Advantage a un museo de gráficas, incluya las opciones siguientes en el mandato: `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
   {: tip}

   **Salida de ejemplo**

   ```
   user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
   Found 1 image(s) and 1 chart(s) to import.
   Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
   Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
   369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

   Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

   OK
   ```
   {: screen}

4. Si los archivos comprimidos contienen gráficas de Helm, estas se colocarán en un directorio de archivado denominado `ppa-import` que se crea en el directorio de trabajo actual. Abra el directorio para obtener el nombre de la gráfica de Helm, `<helm_chart>`, y a continuación inspeccione sus valores.

   ```
   helm inspect values ppa-import/charts/<helm_chart>.tgz
   ```
   {: pre}

   Si ha cargado gráficas en un museo de gráficas en el paso anterior, puede utilizar `helm inspect` para inspeccionar la gráfica en el museo de gráficas.
   {: tip}

5. Configure la gráfica de Helm, `<helm_chart>`, según los valores que da como resultado el mandato `helm inspect values`.

6. Despliegue la gráfica de Helm, `<helm_chart>`, utilizando el mandato `helm install`. Puede alterar temporalmente los valores de la gráfica como sea necesario mediante la opción `--set`.

   ```
   helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
   ```
   {: pre}

## El acceso al registro con un cortafuegos personalizado falla
{: #ts_firewall}

{: tsSymptoms}
Configure un cortafuegos adicional en su entorno de desarrollo con valores personalizados
para el tráfico de red entrante y saliente. Al intentar acceder a {{site.data.keyword.registrylong_notm}}, la conexión falla.

{: tsCauses}
El cortafuegos personalizado requiere que se abran determinados grupos de red para el tráfico de red entrante y saliente
para permitir la comunicación a y desde el registro.

{: tsResolve}

Deje que el clúster acceda a los servicios y recursos de la infraestructura desde detrás de un cortafuegos; consulte [Cómo permitir al clúster acceder a recursos de infraestructura y otros servicios](/docs/containers/cs_firewall.html#firewall_outbound).

Para la conectividad ENTRANTE a su sistema, permita el tráfico de red entrante desde los
grupos de red de origen a la dirección IP pública de destino del sistema.

Para la conectividad SALIENTE desde el sistema, utilice los mismos grupos de red y permita el tráfico de red saliente
desde la dirección IP pública de origen del sistema a los grupos de red.

## Recuperación de claves perdidas o en peligro
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
Al utilizar [contenido de confianza](/docs/services/Registry/registry_trusted_content.html#registry_trustedcontent), ya no podrá gestionar las imágenes de confianza porque sus claves de firma están perdidas o en peligro.

{: tsCauses}
Su repositorio o clave raíz está perdido o en peligro.

{: tsResolve}
Las opciones para recuperar claves perdidas o afectadas dependen del tipo de clave: repositorio o raíz:

- Para [claves de repositorio](#trustedcontent_lostrepokey), puede generar un nuevo conjunto de claves de firma para el repositorio.
- Para [claves raíz](#trustedcontent_lostrootkey), puede solicitar que el repositorio se suprima y crear uno nuevo.

### Claves de repositorio
{: #trustedcontent_lostrepokey}

Si su clave de repositorio está perdida o en peligro, genere un nuevo conjunto de claves de firma para el repositorio.
{:shortdesc}

El único rol de firma que puede rotar es `targets`, que es el administrador del repositorio. Si hay otros roles afectados, genere claves nuevas para dichas funciones, elimine las antiguas y añada las nuevas como firmantes.
{:tip}

Antes de empezar, recupere la frase de contraseña de clave raíz que ha creado al [enviar una imagen firmada](/docs/services/Registry/registry_trusted_content.html#trustedcontent_push) en primer lugar.

1. Instale la versión de CLI del [proyecto Notary ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli).

2. [Configure su entorno de contenido de confianza](/docs/services/Registry/registry_trusted_content.html#trustedcontent_setup).

3. Anota el URL desde el mandato export en el paso anterior. Por ejemplo, `https://registry.ng.bluemix.net:4443`.

4. Genere una señal de registro.

   ```
   ibmcloud cr token-add --readwrite
   ```
   {: pre}

5. Rote las claves para que el contenido que se ha firmado con dichas claves ya no sea fiable. Sustituya _&lt;URL&gt;_ por el URL del mandato export que ha anotado en el Paso 2, e _&lt;image&gt;_ con la imagen cuya clave de repositorio está afectada.

   ```
   notary -s <URL> -d ~/.docker/trust key rotate <image> targets
   ```
   {: pre}

6. Si se le solicita, especifique la frase de contraseña de clave raíz. A continuación, especifique una nueva frase de contraseña de clave raíz para la nueva clave de repositorio cuando se le solicite.

7. [Envíe una imagen firmada](/docs/services/Registry/registry_trusted_content.html#trustedcontent_push) que utilice las nuevas claves de firma.

### Claves raíz
{: #trustedcontent_lostrootkey}

Si la clave raíz se ha perdido o está en peligro, no podrá actualizar ningún repositorio de contenido de confianza que haya utilizado dicha clave raíz.
{:shortdesc}

Puede [suprimir los espacios de nombres](/docs/services/Registry/registry_setup_cli_namespace.html#registry_remove) que tengan repositorios que utilicen la clave raíz afectada, lo que suprime las imágenes y los datos de confianza.

Si el espacio de nombres contiene repositorios con las claves raíz sin afectar, como un espacio de nombres para imágenes de producción, es posible que desee suprimir solo los datos de confianza asociados con la clave raíz afectada. Abra una incidencia de soporte.

1. [Póngase en contacto con el soporte de {{site.data.keyword.Bluemix_notm}}](/docs/get-support/howtogetsupport.html#getting-customer-support). Incluya una breve descripción del problema, el ID de la cuenta y una lista de los espacios de nombres que contienen los repositorios de imágenes con las claves raíz afectadas.

2. Una vez que {{site.data.keyword.Bluemix_notm}} resuelva el problema, suprima el repositorio Docker Content Trust en su sistema local.

   - Directorio de Linux y Mac: `~/.docker/trust/private` y `~/.docker/trust/tuf`

   - Directorio de Windows: `%HOMEPATH%\.docker\trust\private` y `%HOMEPATH%\.docker\trust\tuf`

   Puesto que la clave raíz está afectada, este paso suprime todas las claves de firma, incluso para otros servidores de confianza.
   {:tip}

3. Si utiliza [{{site.data.keyword.Bluemix_notm}} Image Enforcement](/docs/services/Registry/registry_security_enforce.html#security_enforce) en el clúster de {{site.data.keyword.containershort_notm}}, reinicie todos los pods de imposición de imágenes. Para hacer que Kubernetes realice un reinicio continuo de los pods automáticamente, puede cambiar algunos metadatos en el pod. Por ejemplo, [apunte la CLI de Kubernetes al clúster](/docs/containers/cs_cli_install.html#cs_cli_configure) y modifique el despliegue.

   ```
   kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
   ```
   {: pre}

4. Genere repositorios de contenido de confianza.

    - Si desea crear nuevo contenido de confianza, [envíe nuevas imágenes firmadas](/docs/services/Registry/registry_trusted_content.html#trustedcontent_push).

    - Si no desea cambiar el contenido de confianza anterior, añada una firma a las imágenes más recientes del registro.

      ```
      docker trust sign <image>:<tag>
      ```
      {: pre}

## La instalación de Container Image Security Enforcement fallará con `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists`
{: #ts_install_cise_fail}

{: tsSymptoms}
La instalación de Container Image Security Enforcement ha fallado y ha recibido el mensaje siguiente:

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
La instalación anterior ha fallado y la desinstalación subsiguiente no ha eliminado todos los trabajos de Kubernetes asociados con la instalación.

{: tsResolve}
Elimine los trabajos restantes de Kubernetes ejecutando el mandato siguiente:

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}

## Los pods no se reinician después de que todos los trabajadores hayan estado inactivos
{: #ts_pods}

{: tsSymptoms}
Los pods no se reinician después de que todos los trabajadores del clúster hayan estado inactivos. Se despliega Container Image Security Enforcement. Los trabajadores del clúster tienen buen estado, pero no hay nada planificado.

{: tsCauses}
De forma predeterminada, Container Image Security Enforcement añade un webhook de admisión cerrado. Si todos los pods de Container Image Security Enforcement están inactivos, los pods no estarán disponibles para aprobar su propia recuperación.

{: tsResolve}
Para recuperar el clúster cuando se encuentra en este estado, debe cambiar la configuración del webhook para se quede abierto en lugar de cerrado.

Debe tener suficientes privilegios de control de accesos basado en roles (RBAC) para utilizar los verbos siguientes:

- `GET`
- `PATCH`

en estos recursos:

- `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
- `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration`

Para obtener más información sobre RBAC, consulte [Autorización de usuarios con roles de RBAC de Kubernetes personalizados](/docs/containers/cs_users.html#rbac) y [Kubernetes: Utilización de la autorización de RBAC
![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

Complete los pasos siguientes para cambiar la configuración de webhook para dejarla abierta en lugar de cerrada y, a continuación, con al menos un pod de Container Image Security Enforcement en ejecución, restaure la configuración del webhook para que se quede cerrado:

1. Actualice `MutatingWebhookConfiguration` ejecutando el mandato siguiente:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Cambie `failurePolicy` a `Ignore`, guarde y cierre.

2. Actualice `ValidatingWebhookConfiguration` ejecutando el mandato siguiente:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Cambie `failurePolicy` a `Ignore`, guarde y cierre.

3. Espere a que se inicien algunos pods de Container Image Security Enforcement. Puede comprobar si los pods se han iniciado ejecutando el mandato siguiente hasta que vea la columna **ESTADO**, ya que al menos un pod está mostrando `En ejecución`:

   ```
   kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
   ```
   {: pre}

4. Cuando se esté ejecutando al menos un pod de Container Image Security Enforcement, actualice `MutatingWebhookConfiguration` ejecutando el mandato siguiente:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Cambie `failurePolicy` a `Fail`, guarde y cierre.

5. Actualice `ValidatingWebhookConfiguration` ejecutando el mandato siguiente:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Cambie `failurePolicy` a `Fail`, guarde y cierre.

## Error de manifiesto: `The manifest type for this image is not supported for tagging.`
{: #ts_manifest_error_type}

{: tsSymptoms}
Ha intentado etiquetar la imagen, pero recibe el mensaje de error siguiente: `The manifest type for this image is not supported for tagging.`.

{: tsCauses}
No se admite el tipo de manifiesto.

{: tsResolve}
Para solucionar el problema, realice los pasos siguientes:

1. Extraiga la imagen que ha intentado etiquetar con el mandato siguiente, donde `<source_image>` es el nombre de la imagen de origen:

   ```
   docker pull <source_image>
   ```
   {: pre}

2. Etiquete la copia local de la imagen que ha extraído en el paso anterior con el mandato siguiente, donde `<target_image>` es el nombre de la imagen nueva:

   ```
   docker tag <source_image> <target_image>
   ```
   {: pre}

3. Envíe por push la imagen que ha etiquetado en el paso anterior con el mandato siguiente:

   ```
   docker push <target_image>
   ```
   {: pre}

## Error de manifiesto: `The manifest version for this image is not supported for tagging.`
{: #ts_manifest_error_version}

{: tsSymptoms}
Ha intentado etiquetar la imagen, pero recibe el mensaje de error siguiente: `The manifest version for this image is not supported for tagging. Para actualizar a una versión de manifiesto admitida, extraiga y envíe por push esta imagen mediante la versión 1.12 o posterior de Docker y, a continuación, ejecute el mandato 'ibmcloud cr image-tag' de nuevo.`

{: tsCauses}
No se admite la versión del manifiesto.

{: tsResolve}
Para solucionar el problema, realice los pasos siguientes:

1. Actualice a la versión 1.12 o posterior de Docker Engine.

2. Extraiga la imagen que ha intentado etiquetar con el mandato siguiente, donde `<source_image>` es el nombre de la imagen de origen:

   ```
   docker pull <source_image>
   ```
   {: pre}

3. Para actualizar la versión de manifiesto, envíe por push la imagen con el siguiente mandato:

   ```
   docker push <source_image>
   ```
   {: pre}

4. Etiquete la imagen mediante el mandato `ibmcloud cr image-tag`. Consulte [Creación de imágenes nuevas que hacen referencia a una imagen de origen](/docs/services/Registry/registry_images_.html#registry_images_source).
  
