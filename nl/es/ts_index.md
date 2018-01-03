---

copyright:
  years: 2017
lastupdated: "2017-10-30"

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

Aquí encontrará las respuestas a las preguntas más comunes sobre la resolución de problemas acerca
de cómo utilizar {{site.data.keyword.registrylong}}.
{:shortdesc}


## Obtención de ayuda y soporte para {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Si tiene problemas o preguntas cuando utiliza {{site.data.keyword.registrylong_notm}}, puede obtener ayuda buscando información o planteando preguntas a través de un foro. También puede abrir una incidencia de soporte de {{site.data.keyword.IBM_notm}}.

Cuando utilice los foros para formular una pregunta, etiquete la pregunta de manera que la vea el equipo de desarrollo de {{site.data.keyword.registrylong_notm}}.

-   Si tiene preguntas técnica sobre cómo desarrollar o desplegar una app con {{site.data.keyword.registrylong_notm}}, publique su pregunta en [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) y etiquete la pregunta con `ibm-bluemix` y `container-registry`.
-   Para preguntas sobre el servicio y para obtener instrucciones para empezar, utilice el foro [dW Answers de IBM
developerWorks](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Incluya las etiquetas bluemix y container-registry.

Consulte [Obtención de ayuda](../../support/index.html#getting-help)
para obtener más detalles sobre la utilización de los foros.

Para obtener información sobre cómo abrir una incidencia de soporte de {{site.data.keyword.IBM_notm}}, o sobre los niveles de soporte y las gravedades de las incidencias, consulte [Cómo obtener soporte](../../support/index.html#contacting-support).

## Falla el inicio de sesión en {{site.data.keyword.registrylong_notm}}
{: #ts_login}

No se puede iniciar la sesión en {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
El mandato `bx cr login` falla.

{: tsCauses}
-   El plug-in container-registry no está actualizado y debe actualizarse.
-   Docker no está instalado en la máquina local o no está en ejecución.
-   Han caducado sus credenciales de inicio de sesión en {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
Puede solucionar este problema de las siguientes maneras:

-   Actualice a la versión más reciente del plug-in de {{site.data.keyword.registryshort_notm}}, consulte [Actualización del plugin de {{site.data.keyword.registrylong_notm}} (`bx cr`)](registry_setup_cli_namespace.html#registry_cli_update).
-   Asegúrese de que Docker esté instalado en la máquina. Si ya está instalado, reinicie el daemon de Docker.
-   Vuelva a ejecutar el mandato `bx login` para renovar las credenciales de inicio de sesión en {{site.data.keyword.Bluemix_notm}}.


## Los mandatos de {{site.data.keyword.registrylong_notm}} fallan con `'cr' no es un mandato registrado. Consulte 'bx help'. `
{: #ts_login_error}

No puede ejecutar un mandato `bx cr` porque `cr` no es un mandato `bx` registrado.

{: tsSymptoms}
Puede ver un error similar a uno de los mensajes de error siguientes: 

```
bx cr login
'cr' no es un mandato registrado. Consulte 'bx help'. 
```
{: pre}

```
bx cr namespace
'cr' no es un mandato registrado. Consulte 'bx help'. 
```
{: pre}

{: tsCauses}
-   El plug-in container-registry no está instalado.


{: tsResolve}
Puede solucionar este problema de la siguiente manera:

-   Instale el plugin container-registry, consulte [Instalación del plugin de la CLI de {{site.data.keyword.registryshort_notm}} (bx cr)](registry_setup_cli_namespace.html#registry_cli_install).


## Error de configuración de un espacio de nombres
{: #ts_problem}

{: tsSymptoms}
Cuando ejecuta `bx cr namespace-add`, no puede establecer el valor especificado como el espacio de nombres.

{: tsCauses}
-   Ha especificado un valor de espacio de nombres que ya está siendo utilizado por otra organización de {{site.data.keyword.Bluemix_notm}}.
-   Un espacio de nombres se ha suprimido recientemente y está reutilizando su nombre. Si el espacio de nombres suprimido contenía muchos recursos, es posible que {{site.data.keyword.registrylong_notm}} no haya procesado por completo la supresión.
-   Ha utilizado caracteres no válidos en el valor del espacio de nombres.

{: tsResolve}
Puede solucionar este problema de las siguientes maneras:

-   Siga las instrucciones que aparecen en el mensaje de error devuelto.
-   Compruebe que ha especificado un espacio de nombres válido:
    -   Su espacio de nombres debe tener entre 4 y 30 caracteres.
    -   El espacio de nombres debe empezar por al menos una letra o un número.
    -   Su espacio de nombres debe contener letras minúsculas, números, o subrayados (_) sólo.
-   Elija otro valor para el espacio de nombres.
-   Si va a volver a crear un espacio de nombres que se ha suprimido y que contenía muchas imágenes, inténtelo de nuevo más tarde.

## La transferencia o extracción de una imagen de Docker falla
{: #ts_pushpull}

{: tsSymptoms}
Cuando ejecuta mandatos para transferir o extraer imágenes de Docker, recibe un mensaje de error. El mensaje de error varía en función de la causa raíz. Los mensajes de error pueden ser:

```
Ha superado la cuota de almacenamiento. Suprima una o varias imágenes, o bien revise su cuota de almacenamiento y el plan de precios
```
{: screen}

```
Ha superado la cuota de tráfico de extracción para el mes actual. Revise la cuota del tráfico de extracción y el plan de precios
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
-   Docker no está instalado.
-   El cliente de Docker no ha iniciado sesión en {{site.data.keyword.registrylong_notm}}.
-   Es posible que la señal de acceso a {{site.data.keyword.Bluemix_notm}} haya caducado.
-   Ha superado el límite de cuota para almacenamiento o tráfico de extracción establecido para su cuenta de {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
Puede solucionar este problema de las siguientes maneras:

-   [Asegúrese de que Docker esté instalado en la máquina](index.html#registry_cli_install).
-   Compruebe la vía de acceso de instalación de Docker.
-   Inicie una sesión en {{site.data.keyword.Bluemix_notm}} con el mandato
`bx login`. Luego inicie una sesión en la CLI de {{site.data.keyword.registrylong_notm}} con el mandato `bx cr
login`.
-   [Revisión de los límites de cuota y del uso para almacenar y extraer imágenes de Docker en {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).

## No se puede extraer la última imagen utilizando la etiqueta más reciente
{: #ts_docker_latest}

{: tsSymptoms}
Intenta ejecuta el mandato `docker pull`, pero devuelve una versión de la imagen que no es la más reciente.

{: tsCauses}
La etiqueta `latest` se aplica de forma predeterminada para hacer referencia a una imagen cuando se ejecutan mandatos de Docker sin especificar el valor de etiqueta. La etiqueta `latest` se aplica al último mandato `docker build` o `docker tag` que se ha ejecutado sin un valor de etiqueta establecido de forma explícita. Por lo tanto, se pueden ejecutar mandatos `docker` desordenados o establecer de forma explícita etiquetas sobre algunas imágenes y la etiqueta `latest` para hacer referencia a una compilación que no se sea la más reciente.

{: tsResolve}
Generalmente es mejor definir de forma explícita una etiqueta secuencial para las imágenes cada vez, y no confiar en la etiqueta `latest`.

## El acceso al registro con un cortafuegos personalizado falla
{: #ts_firewall}

{: tsSymptoms}
Configure un cortafuegos adicional en su entorno de desarrollo con valores personalizados
para el tráfico de red entrante y saliente. Al intentar acceder a {{site.data.keyword.registrylong_notm}}, la conexión falla.

{: tsCauses}
El cortafuegos personalizado requiere que se abran determinados grupos de red para el tráfico de red entrante y saliente
para permitir la comunicación a y desde el registro.

{: tsResolve}
Abra los siguientes grupos de red en su cortafuegos personalizado.

1.  Anote la dirección IP pública de la máquina que desea utilizar para conectarse a {{site.data.keyword.registrylong_notm}}. Si está utilizando Kubernetes, utilice la
dirección IP pública del nodo de trabajador. Recupere la dirección IP pública del nodo de trabajador ejecutando `bx cs workers <cluster_name_or_id>`, donde *&lt;cluster_name_or_id&gt;* es el nombre o el ID de su clúster.
2.  En el cortafuegos, permita las siguientes conexiones a y desde la máquina:
    -   Para la conectividad ENTRANTE a su máquina, permita el tráfico de red entrante desde los siguientes
grupos de red de origen a la dirección IP pública de destino de la máquina.

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   Para la conectividad SALIENTE desde la máquina, utilice los mismos grupos de red y permita el tráfico de red saliente
desde la dirección IP pública de origen de la máquina a estos grupos de red.

