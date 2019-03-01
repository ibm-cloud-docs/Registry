---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, Vulnerability Advisor policies, container image security, policy requirements, policies, Container Image Security Enforcement

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

# Mise en application de la sécurité des images de conteneur (bêta)
{: #security_enforce}

Container Image Security Enforcement (bêta) vous permet de vérifier vos images de conteneur avant de les déployer dans votre cluster dans {{site.data.keyword.containerlong}}. Vous pouvez contrôler l'emplacement depuis lequel les images sont déployées, mettre en application des règles Vulnerability Advisor et vous assurer que la [sécurité du contenu](/docs/services/Registry/registry_trusted_content.html) est correctement appliquée à l'image. Si une image ne répond pas aux exigences de règle, le pod n'est pas déployé sur votre cluster ni mis à jour.
{:shortdesc}

Container Image Security Enforcement extrait les informations relatives à la sécurité du contenu d'image et aux vulnérabilités depuis {{site.data.keyword.registrylong}}. Vous pouvez choisir de bloquer ou d'autoriser le déploiement des images stockés dans d'autres registres, mais vous ne pouvez pas utiliser le contrôle de vulnérabilité ou de confiance pour ces images.

## Installation de Container Image Security Enforcement dans votre cluster
{: #sec_enforce_install}

**Avant de commencer**

* [Créez](/docs/containers/cs_clusters.html#clusters_ui) ou [mettez à jour](/docs/containers/cs_cluster_update.html#update) le cluster à utiliser avec **Kubernetes version 1.9 ou ultérieure**.
* [Ciblez votre interface de ligne de commande `kubectl`](/docs/containers/cs_cli_install.html#cs_cli_configure) sur le cluster.

Procédez comme suit :

1. [Configurez Helm dans votre cluster](/docs/containers/cs_integrations.html#helm).

2. Ajoutez le référentiel de chartes IBM à votre client Helm.

   ```
   helm repo add ibm  https://registry.bluemix.net/helm/ibm
   ```
   {: pre}

3. Installez la charte Helm Container Image Security Enforcement dans votre cluster. Donnez-lui un nom, par exemple, `cise`.

   ```
   helm install --name cise ibm/ibmcloud-image-enforcement
   ```
   {: pre}

Container Image Security Enforcement est maintenant installé et applique les [règles de sécurité par défaut](#default_policies) pour tous les espaces de nom Kubernetes de votre cluster. Pour plus d'informations sur la personnalisation des règles de sécurité pour les espaces de nom Kubernetes de votre cluster, ou pour l'ensemble du cluster, voir [Personnalisation des règles](#customize_policies).

## Règles par défaut
{: #default_policies}

Container Image Security Enforcement installe des règles par défaut afin que vous disposiez d'un point de départ pour créer vos règles de sécurité.
{:shortdesc}

Pour remplacer ces règles, utilisez l'une des options suivantes :

* Ecrivez un nouveau document de règle et appliquez-le à votre cluster en utilisant `kubectl apply`
* Editez la règle par défaut en utilisant `kubectl edit`

Pour plus d'informations sur l'écriture de règles de sécurité, voir [Personnalisation des règles](#customize_policies).

### Règles à l'échelle du cluster
{: #cluster-wide}

Par défaut, une règle à l'échelle du cluster est appliquée à l'ensemble des images de tous les registres comportant des informations de confiance et pour lesquels aucune vulnérabilité n'a été signalée dans Vulnerability Advisor.
{:shortdesc}

**Fichier `.yaml` de règle à l'échelle du cluster**

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
{: codeblock}

Lorsque vous définissez `va` ou `trust` sur `enabled: true` pour un registre de conteneur autre que {{site.data.keyword.registrylong_notm}}, toute tentative de déploiement de pods à partir d'images de ce registre est refusée. Si vous souhaitez déployer des images à partir d'autres registres, retirez les règles `va` et `trust`.
{:tip}

### Règles kube-system
{: #kube-system}

Par défaut, une règle à l'échelle de l'espace de nom est installée pour l'espace de nom `kube-system`. Elle permet à toutes les images d'un registre de conteneur d'être déployées sur le `kube-system` sans contrôle, mais vous pouvez modifier cette partie de la règle. La règle par défaut inclut également certains référentiels que vous devez conserver pour que votre cluster puisse être correctement configuré.
{:shortdesc}

**Fichier `.yaml` de règle `kube-system`**

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
    # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```
{: codeblock}

### Règles IBM-system
{: #ibm-system}

Par défaut, une règle à l'échelle de l'espace de nom est installée pour l'espace de nom `ibm-system`. Elle permet à toutes les images d'un registre de conteneur d'être déployées sur le `ibm-system` sans contrôle, mais vous pouvez modifier cette partie de la règle. La règle par défaut inclut également certains référentiels que vous devez conserver pour que votre cluster puisse être correctement configuré et puisse installer ou mettre à niveau Container Image Security Enforcement.
{:shortdesc}

**Fichier `.yaml` de règle `ibm-system`**

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
    # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
    # This policy prevents Container Image Security Enforcement from blocking itself
    - name: "registry*.bluemix.net/ibm/ibmcloud-image-enforcement"
      policy:
    # This policy allows Container Image Security Enforcement to use Hyperkube to configure your cluster. This policy must exist if you uninstall Container Image Security Enforcement.
    - name: quay.io/coreos/hyperkube
      policies:
```
{: codeblock}

## Personnalisation des règles
{: #customize_policies}

Vous pouvez changer la règle utilisée par Container Image Security Enforcement pour autoriser les images, que ce soit au niveau du cluster ou de l'espace de nom Kubernetes. Dans la règle, vous pouvez spécifier différentes règles de mise en application pour différentes images.
{:shortdesc}

Vous devez disposer d'un ensemble de règles. Dans le cas contraire, les déploiements sur votre cluster échoueront. Si vous ne voulez pas que des règles de sécurité des images soient appliquées, [retirez Container Image Security Enforcement](#remove).
{:tip}

Lorsque vous appliquez un déploiement, Container Image Security Enforcement vérifie si l'espace de nom Kubernetes que vous déployez dispose d'une règle à appliquer. Si ce n'est pas le cas, Container Image Security Enforcement utilise la règle à l'échelle du cluster. Votre déploiement est refusé s'il n'existe aucune règle au niveau de l'espace de nom ou à l'échelle du cluster.

Avant de commencer, [ciblez votre interface de ligne de commande `kubectl` sur le cluster](/docs/containers/cs_cli_install.html#cs_cli_configure) to the cluster. Procédez ensuite comme suit :

1. Créez un fichier `.yaml` de <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">définition de ressource personnalisée Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

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
    {: codeblock}

    <table>
    <caption>Tableau 1. Compréhension des composants YAML</caption>
    <thead>
    <th>Zone</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>Pour une règle à l'échelle du cluster, spécifiez `kind` comme `ClusterImagePolicy`. Pour une règle d'espace de nom Kubernetes, spécifiez le type (kind) comme `ImagePolicy`.</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>Nom de la définition de ressource personnalisée.</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>Spécifiez les référentiels à partir desquels autoriser les images. Les caractères génériques (`*`) sont autorisés dans les noms de référentiel. Les référentiels sont refusés à moins qu'une entrée correspondante dans `repositories` ne les autorise ou applique une vérification plus approfondie. Une liste `repositories` vide bloque le déploiement de toutes les images. Pour autoriser toutes les images sans vérification des règles, définissez le nom sur `*` et omettez les sous-section de règle.</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>Renseignez les sous-sections pour la mise en application de `trust` et `va`. Si vous omettez les sous-sections de règle, cela équivaut à spécifier `enabled: false` pour chacune d'elles.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>Définissez sur `true` pour autoriser uniquement les images qui sont [signées pour la vérification de contenu](/docs/services/Registry/registry_trusted_content.html) à être déployées. Définissez sur `false` pour ignorer le fait que les images soient ou non signées.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>Si vous souhaitez autoriser uniquement les images signées par des utilisateurs spécifiques, indiquez la valeur confidentielle (secret) Kubernetes avec le nom du signataire. Omettez cette section ou laissez-la vide pour vérifier que les images sont signées sans appliquer de signataires particuliers. Pour plus d'informations, voir [Spécification de signataires de contenu sécurisé dans des règles personnalisées](#signers).</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>Définissez sur `true` pour autoriser uniquement les images réussissant l'analyse [Vulnerability Advisor](/docs/services/va/va_index.html). Définissez sur `false` pour ignorer l'analyse Vulnerability Advisor.</td>
    </tr>
    </tbody>
    </table>

2. Appliquez le fichier `.yaml` à votre cluster.

   ```
   kubectl apply -f <filepath>
   ```
   {: pre}

### Spécification de signataires de contenu sécurisé dans des règles personnalisées
{: #signers}

Si vous utilisez la sécurité du contenu, vous pouvez vérifier que les images sont signées par des signataires particuliers. Le déploiement est autorisé uniquement si la version signée la plus récente est signée par tous les signataires répertoriés. Pour ajouter un signataire à un référentiel, voir [Gestion des signataires de confiance](/docs/services/Registry/registry_trusted_content.html#trustedcontent_signers).
{:shortdesc}

Pour configurer la règle destinée à vérifier qu'une image est signée par un signataire spécifique :

1. Procurez-vous le nom du signataire (ce nom a été utilisé dans `docker trust signer add`), ainsi que la clé publique du signataire.
2. Générez une valeur confidentielle (secret) Kubernetes avec le nom du signataire et sa clé publique.

   ```
   kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
   ```
   {: pre}

3. Ajoutez la valeur confidentielle à la liste `signerSecrets` pour le référentiel dans votre règle.

   ```yaml
   - name: example
     policy:
       trust:
         enabled: true
         signerSecrets:
         - name: <secret_name>
   ```
   {: codeblock}

## Contrôle des personnes pouvant personnaliser des règles
{: #assign_user_policy}

Si le contrôle d'accès basé sur les rôles (RBAC) est activé sur votre cluster Kubernetes, vous pouvez créer un rôle pour décider qui a la possibilité d'administrer les règles de sécurité sur votre cluster. Pour plus d'informations sur l'application de règles de contrôle d'accès à base de rôles à votre cluster, voir [la documentation d'{{site.data.keyword.containerlong_notm}}](/docs/containers/cs_users.html#rbac).
{:shortdesc}

Dans votre rôle, ajoutez une règle pour les règles de sécurité :

```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```
{: codeblock}

Vous pouvez créer plusieurs rôles afin de contrôler quelles actions les utilisateurs peuvent effectuer. Par exemple, changez les instructions (`verbs`) afin que certains utilisateurs puissent uniquement obtenir (`get`) ou répertorier (`list`) des règles. Ou bien, vous pouvez omettre des règles `clusterimagepolicies` provenant de la liste `resources` pour accorder l'accès uniquement aux règles d'espace de nom Kubernetes.
{:tip}

Les utilisateurs disposant d'un accès pour supprimer des définitions de ressource personnalisée (CRD) peuvent supprimer la définition de ressource pour des règles de sécurité, ce qui supprime également vos règles de sécurité. Veillez à contrôler qui est autorisé à supprimer des CRD. Pour accorder l'accès pour supprimer des CRD, ajoutez une règle :

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```
{: codeblock}

Les utilisateurs et comptes de service avec le rôle `cluster-admin` ont accès à l'ensemble des ressources. Le rôle cluster-admin accorde l'accès pour administrer des règles de sécurité, même si vous n'éditez pas le rôle. Veillez à contrôler qui dispose du rôle `cluster-admin`, et accordez l'accès uniquement aux personnes que vous souhaitez autoriser à modifier des règles de sécurité.
{:tip}

## Déploiement d'images de conteneur avec la sécurité appliquée
{: #deploy_containers}

Lorsqu'une règle est appliquée, vous pouvez déployer normalement du contenu sur votre cluster. Votre règle est automatiquement appliquée par le cluster Kubernetes. Si votre déploiement correspond à une règle et est autorisé par celle-ci, il est accepté par le cluster et est appliqué.
{:shortdesc}

Si Container Image Security Enforcement refuse un déploiement, le déploiement (Deployment) est créé mais le jeu de répliques (ReplicaSet) qu'il crée n'est pas mis à l'échelle et aucun pod n'est créé. Pour rechercher le ReplicaSet, exécutez `kubectl describe deployment <deployment-name>`, puis examinez la raison pour laquelle le déploiement a été refusé en exécutant `kubectl describe rs <replicaset-name>`.

**Exemples de message d'erreur**

* Si votre image ne correspond pas à une règle, ou s'il n'existe aucune règle dans l'espace de nom ou le cluster.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

* Si votre image correspond à une règle mais ne satisfait pas les exigences Vulnerability Advisor de la règle.

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Refer to your image vulnerability report 
   for more details by using the command `ibmcloud cr va`.
   ```
   {: screen}

* Si votre image correspond à une règle mais ne satisfait pas les exigences de confiance de la règle.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

* Si votre règle spécifie un contrôle de confiance pour votre image, mais que celle-ci ne provient pas d'un registre pris en charge.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

Vous pouvez activer l'option `va` dans votre règle afin d'imposer la réussite de l'analyse Vulnerability Advisor avant qu'une image ne puisse être déployée. Les images non prise en charge par Vulnerability Advisor sont autorisées.

Vous pouvez activer l'option `trust` dans votre règle afin d'imposer la sécurité du contenu. Si vous ne spécifiez pas `signerSecrets`, le déploiement est autorisé si l'image est signée par quelqu'un. Si vous spécifiez `signerSecrets`, la version signée la plus récente de l'image doit avoir été signée par tous les signataires spécifiés. Container Image Security Enforcement vérifie que la clé publique fournie appartient au signataire. Pour plus d'informations sur la sécurité du contenu, voir [Signature d'images pour du contenu sécurisé](/docs/services/Registry/registry_trusted_content.html).

Un déploiement est autorisé uniquement si toutes les images réussissent les vérifications de Container Image Security Enforcement.

## Retrait de Container Image Security Enforcement
{: #remove}

Avant de commencer, [ciblez votre interface de ligne de commande `kubectl` sur le cluster](/docs/containers/cs_cli_install.html#cs_cli_configure) to the cluster.



1. Désactivez Container Image Security Enforcement.

   ```
   $ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config 
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config
   ```
   {: codeblock}

2. Retirez la charte.

   ```
   helm delete --purge cise
   ```
   {: pre}
