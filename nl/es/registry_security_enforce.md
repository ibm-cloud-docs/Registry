---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Imposición de seguridad de imagen de contenedor (beta)
{: #security_enforce}

Con IBM Container Image Security Enforcement (beta), puede verificar las imágenes de contenedor antes de desplegarlas en el clúster en {{site.data.keyword.containerlong}}. Puede controlar desde dónde se despliegan las imágenes, forzar políticas de Vulnerability Advisor y asegurarse de que el [contenido de confianza](registry_trusted_content.html) esté aplicado correctamente a la imagen. Si un pod no cumple los requisitos la política, el clúster no se modificará.
{:shortdesc}

IBM Container Image Security Enforcement obtiene la información sobre la confianza del contenido de las imágenes y las vulnerabilidades desde {{site.data.keyword.registrylong}}. Puede elegir si desea bloquear o permitir imágenes de otros registros en las políticas, pero no puede utilizar la imposición de la vulnerabilidad ni de la confianza para estas imágenes.


## Instalación de Container Image Security Enforcement en el clúster
{: #sec_enforce_install}

Antes de empezar:
* [Cree](../../containers/cs_clusters.html#clusters_ui) o [actualice](../../containers/cs_cluster_update.html) el clúster que desee utilizar con **Kubernetes versión 1.9 o posterior**.
* [Establezca la CLI de `kubectl`](../../containers/cs_cli_install.html#cs_cli_configure) en el clúster.

Pasos:
1.  [Configure Helm en el clúster](../../containers/cs_integrations.html#helm).

1.  Añada el repositorio de gráficas de IBM en Helm.

    ```
    helm repo add ibm-incubator https://registry.bluemix.net/helm/ibm-incubator
    ```
    {: pre}

1.  Instale la gráfica de Helm de IBM Container Image Security Enforcement en el espacio de nombres del clúster `ibm-system`. Asígnele un nombre como `<cise>`.

    ```
    helm install --name=<cise> --namespace=ibm-system ibm-incubator/ibmcloud-image-enforcement
    ```
    {: pre}

IBM Container Image Security Enforcement está instalado ahora, y está aplicando la [política de seguridad predeterminada](#default_policies) para todos los espacios de nombres de Kubernetes del clúster. Para obtener información sobre cómo personalizar la política de seguridad para los espacios de nombres de Kubernetes en el clúster, o el clúster en general, consulte [Personalización de políticas](#customize_policies).

## Políticas predeterminadas
{: #default_policies}

IBM Container Image Security Enforcement instala algunas políticas de forma predeterminada para proporcionarle un punto de partida para crear la política de seguridad.
{:shortdesc}

Para alterar temporalmente estas políticas, utilice una de las siguientes opciones:
* Escriba un nuevo documento de políticas y aplíquelo al clúster mediante `kubectl apply`
* Edite la política predeterminada mediante `kubectl edit`

Para obtener más información sobre cómo escribir políticas de seguridad, consulte [Personalización de políticas](#customize_policies).

### Política de todo el clúster
{: #cluster-wide}

De forma predeterminada, una política de todo el clúster fuerza que todas las imágenes de todos los registros tengan información de confianza y no tengan vulnerabilidades de las que se haya informado en el Vulnerability Advisor.
{:shortdesc}

**Archivo `.yaml` de la política de todo el clúster predeterminado**:

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ClusterImagePolicy
metadata:
  name: ibmcloud-default-cluster-image-policy
spec:
   repositories:
    # This enforces that all images deployed to this cluster pass trust and VA
    # To override, set an ImagePolicy for a specific Kubernetes namespace or modify this policy
    - name: "*"
      policy:
        trust:
          enabled: true
        va:
          enabled: true
```

Al establecer `va` o `trust` en `enabled: true` para un registro de contenedor que no sea {{site.data.keyword.registrylong_notm}}, cualquier intento de desplegar pods desde imágenes de dicho registro se denegará. Si desea desplegar imágenes desde otros registros, elimine las políticas `va` y `trust`.
{:tip}

### Política de sistema kube
{: #kube-system}

De forma predeterminada, hay instalada una política de todo el espacio de nombres para el espacio de nombres de `kube-system`. Esta política permite que se desplieguen todas las imágenes de cualquier registro de contenedores en el `kube-system` sin imposición. También permite los repositorios utilizados para configurar el clúster.
{:shortdesc}

**Archivo `.yaml` de política `kube-system` predeterminado**:

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: kube-system
spec:
   repositories:
    # This policy allows all images to be deployed into this namespace. This policy prevents breaking any existing third party applications in this namespace.
    # IMPORTANT: Review this policy and replace it with one that meets your requirements. If you do not run any third party applications in this namespace, you can remove this policy entirely.
    - name: "*"
      policy:
    # These policies allow all IBM Cloud Container Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```

### Política de sistema IBM
{: #ibm-system}

De forma predeterminada, hay instalada una política de todo el espacio de nombres para el espacio de nombres `ibm-system`. Esta política permite que se desplieguen todas las imágenes de cualquier registro de contenedores en `ibm-system` sin imposición. También permite los repositorios utilizados para configurar el clúster, e instalar o actualizar Image Security Enforcement.
{:shortdesc}

**Archivo `.yaml` de la política `ibm-system` predeterminado**:

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: ibm-system
spec:
   repositories:
    # This policy allows all images to be deployed into this namespace. This policy prevents breaking any existing third party applications in this namespace.
    # IMPORTANT: Review this policy and replace it with one that meets your requirements. If you do not run any third party applications in this namespace, you can remove this policy entirely.
    - name: "*"
      policy:
    # These policies allow all IBM Cloud Container Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
    # This policy prevents Image Security Enforcement from blocking itself
    - name: "registry*.bluemix.net/ibm/ibmcloud-image-enforcement"
      policy:
    # This policy allows Image Security Enforcement to use Hyperkube to configure your cluster. This policy must exist if you uninstall Image Security Enforcement.
    - name: quay.io/coreos/hyperkube
      policies:
```

## Personalización de políticas
{: #customize_policies}

Puede cambiar la política que utiliza IBM Container Image Security Enforcement para permitir imágenes, ya sea en el clúster o en el nivel de espacio de nombres de Kubernetes. En la política, puede especificar distintas reglas de imposición para distintas imágenes.
{:shortdesc}

Debe tener algún conjunto de políticas. De lo contrario, los despliegues al clúster fallarán. Si no desea imponer ninguna política de seguridad de imágenes, [elimine la imposición de seguridad](#remove).
{:tip}

Cuando se aplica un despliegue, Container Image Security Enforcement comprueba si el espacio de nombres de Kubernetes al que está desplegando tiene una política para aplicar. Si no la tiene, Container Image Security Enforcement utilizará la política de todo el clúster. El despliegue se deniega si no existe ningún espacio de nombres ni ninguna política de todo el clúster.

Antes de empezar, [establezca la CLI de `kubectl`](../../containers/cs_cli_install.html#cs_cli_configure) en el clúster.

1.  Cree un archivo `.yaml` de <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">definición de recursos personalizados de Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

    ```yaml
    apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
    kind: <ClusterImagePolicy_or_ImagePolicy>
    metadata:
      name: <crd_name>
    spec:
       repositories:
        - name: <repository_name>
          policy:
            trust:
              enabled: <true_or_false>
              signerSecrets:
              - name: <secret_name>
            va:
              enabled: <true_or_false>
    ```

    <table>
    <caption>Tabla. Visión general de los componentes de YAML</caption>
    <thead>
    <th>Campo</th>
    <th>Descripción</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>Para una política de todo el clúster, especifique el `kind` como `ClusterImagePolicy`. Para una política de espacio de nombres de Kubernetes, especifíquela como `ImagePolicy`.</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>Denomine la definición de recursos personalizados.</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>Especifique los repositorios desde los que permitir imágenes. Los comodines (`*`) están permitidos en los nombres de repositorios. Los repositorios se niegan, a menos que una entrada coincidente de `repositories` los admita o se aplique una verificación mayor. Una lista de `repositories` vacía bloquea el despliegue de todas las imágenes. Para permitir todas las imágenes sin la verificación de ninguna política, establezca el nombre en `*` y omita las subsecciones de políticas.</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>Rellene las subsecciones para la imposición de `trust` y `va`. Si omite las subsecciones de la política, será equivalente a especificar `enabled: false` para cada una de ellas.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>Establézcalo como `true` para permitir solo imágenes que están [firmadas para que se despliegue la confianza de contenido](registry_trusted_content.html). Establézcalo como `false` para ignorar si las imágenes están firmadas.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>Si desea permitir solo imágenes que están firmadas por usuarios particulares, especifique el secreto de Kubernetes con el nombre del firmante. Omita esta sección o déjela vacía para verificar que las imágenes estén firmadas sin imponer firmantes en particular. Para obtener más información, consulte [Especificación de firmantes de contenido de confianza en políticas personalizadas](#signers).</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>Establézcalo como `true` para permitir solo imágenes que pasen la exploración de [Vulnerability Advisor](../va/va_index.html). Establézcalo como `false` para ignorar la exploración del Vulnerability Advisor.</td>
    </tr>
    </tbody>
    </table>

1.  Aplique el archivo `.yaml` al clúster.

    ```
    kubectl apply -f <filepath>
    ```
    {: pre}

### Especificación de firmantes de contenido de confianza en políticas personalizadas
{: #signers}

Si utiliza la confianza de contenido, puede verificar que las imágenes estén firmadas por firmantes particulares. El despliegue solo está permitido si la versión firmada más reciente está firmada por todos los firmantes listados. Para añadir un firmante a un repositorio, consulte [Gestión de firmantes de confianza](registry_trusted_content.html#trustedcontent_signers).
{:shortdesc}

Para configurar la política para verificar que una imagen esté firmada por un firmante en particular:

1.  Obtenga el nombre de firmante (el nombre que se ha utilizado en `docker trust signer add`), y la clave pública del firmante.
1.  Genere un secreto de Kubernetes con el nombre del firmante y su clave pública.
    ```
    kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
    ```
1.  Añada el secreto a la lista `signerSecrets` para el repositorio de la política.
    ```yaml
    - name: example
      policy:
        trust:
          enabled: true
          signerSecrets:
          - name: <secret_name>
    ```

## Cómo controlar quién puede personalizar las políticas
{: #assign_user_policy}

Si tiene el control de acceso basado en roles (RBAC) habilitado en el clúster de Kubernetes, puede crear un rol para controlar quién tiene la capacidad para administrar políticas de seguridad en el clúster. Para obtener más información sobre cómo aplicar reglas de RBAC al clúster, consulte [la documentación de IBM Cloud Container Service](../../containers/cs_users.html#rbac).
{:shortdesc}

En el rol, añada una regla para las políticas de seguridad:
```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```

Puede crear varios roles para controlar qué acciones pueden realizar los usuarios. Por ejemplo, cambie los `verbs` para que algunos usuarios solo tengan políticas `get` o `list`. Como alternativa, puede omitir `clusterimagepolicies` desde la lista `resources` para otorgar acceso solo a las políticas de espacio de nombres de Kubernetes.
{:tip}

Los usuarios que tienen acceso para suprimir definiciones de recursos personalizados (CRD) pueden suprimir la definición de recursos para políticas de seguridad, lo que también suprime las políticas de seguridad. Asegúrese de controlar quién puede suprimir CRD. Para otorgar acceso para suprimir CRD, añada una regla:

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```

**Nota**: Los usuarios y ServiceAccounts con el rol `cluster-admin` tienen acceso a todos los recursos. El rol cluster-admin otorga acceso para administrar políticas de seguridad, incluso aunque no edite el rol. Asegúrese de controlar quién tiene el rol `cluster-admin`, y otorgue acceso solo a las personas a las que desee permitir la modificación de las políticas de seguridad.

## Despliegue de imágenes de contenedor con seguridad impuesta
{: #deploy_containers}

Cuando se aplique una política, puede desplegar contenido en su clúster normalmente. La política se impone automáticamente mediante el clúster de Kubernetes. Si el despliegue coincide con una política y está permitido por dicha política, el clúster aceptará el despliegue y se aplicará.
{:shortdesc}

Si Container Image Security Enforcement deniega un Despliegue, este se creará, pero el ReplicaSet creado por él no podrá escalar, y no se creará ningún pod. Puede encontrar el ReplicaSet ejecutando `kubectl describe deployment <deployment-name>`, y a continuación vea el motivo por el que el despliegue se ha denegado ejecutando `kubectl describe rs <replicaset-name>`.

**Mensajes de error de muestra**:

*  Si la imagen no coincide con ninguna política, o si no hay políticas en el espacio de nombres o en el clúster.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

*  Si la imagen coincide con una política pero no satisface los requisitos de Vulnerability Advisor de dicha política.

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Refer to your image vulnerability report for more details by using the command `bx cr va`.
   ```
   {: screen}

*  Si la imagen coincide con una política pero no satisface los requisitos de confianza de dicha política.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

*  Si la política especifica la imposición de confianza para la imagen, pero la imagen no proviene de un registro soportado.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

Puede habilitar la opción `va` en su política para imponer que el Vulnerability Advisor pase antes de poder desplegar una imagen. Las imágenes que no están soportadas por Vulnerability Advisor están permitidas.

Puede habilitar la opción `trust` en la política para imponer la confianza de contenido. Si no especifica ningún `signerSecrets`, el despliegue se permitirá si la imagen está firmada por cualquier persona. Si especifica `signerSecrets`, todos los firmantes que especifique deben haber firmado la versión firmada más recientemente de la imagen. IBM Container Image Security Enforcement verifica que la clave pública proporcionada pertenezca al firmante. Para obtener más información sobre la confianza de contenido, consulte [Firma de imágenes para contenido de confianza](registry_trusted_content.html).

Solo se permite un despliegue si todas las imágenes pasan las comprobaciones de IBM Container Image Security Enforcement.

## Eliminación de Container Image Security Enforcement
{: #remove}

Antes de empezar, [establezca la CLI de `kubectl`](../../containers/cs_cli_install.html#cs_cli_configure) en el clúster.



1.  Inhabilite Container Image Security Enforcement.

    ```
    $ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config 
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config 
    ```
    {: codeblock}

2.  Elimine la gráfica.

    ```
    helm delete --purge cise
    ```
    {: pre}
