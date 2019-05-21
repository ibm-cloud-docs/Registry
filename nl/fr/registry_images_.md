---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-29"

keywords: IBM Cloud Container Registry, Docker build command, delete images, add images, pull images, push images, copy images, delete private repositories,

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

# Ajout d'images à votre espace de nom
{: #registry_images_}

Vous pouvez stocker et partager de manière sécurisée des images Docker avec d'autres utilisateurs en ajoutant ces images à votre espace de nom dans {{site.data.keyword.registrylong}}.
{:shortdesc}

Chaque image que vous voulez ajouter à votre espace de nom doit d'abord exister sur votre ordinateur local. Vous pouvez télécharger une image sur votre ordinateur local (par commande pull) depuis un autre référentiel ou générer votre propre image depuis un fichier Dockerfile à l'aide de la commande Docker `build`. Pour ajouter une image à votre espace de nom, vous devez la télécharger (par commande push) vers votre espace de nom dans {{site.data.keyword.registrylong_notm}}.

Ne placez pas d'informations personnelles dans vos images de conteneur, noms d'espace de nom, zones de description (par exemple, dans des jetons de registre), ou dans des données de configuration d'image (par exemple, dans des noms d'image ou des libellés d'image).
{: important}

## Extraction d'images depuis un autre registre
{: #registry_images_pulling_reg}

Vous pouvez extraire (par commande pull) une image depuis n'importe quelle source de registre privé ou public, puis lui attribuer une étiquette pour son utilisation ultérieure dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

<img src="images/images_pull.svg" width="800" style="width:800px;" alt="Extraction d'une image depuis un registre privé ou public vers votre ordinateur."/>

**Avant de commencer**

- [Installez l'interface de ligne de commande](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) pour utiliser des images présentes dans votre espace de nom.
- [Configurez votre propre espace de nom dans {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Vérifiez que vous pouvez utiliser des commandes Docker sans disposer pour autant d'autorisations de niveau root![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/install/linux/linux-postinstall/). Si votre client Docker est configuré pour exiger des autorisations root, vous devez exécuter les commandes `ibmcloud login`, `ibmcloud cr login`, `docker pull` et `docker push` avec `sudo`.

  Si vous modifiez vos autorisations pour pouvoir exécuter des commandes Docker sans privilèges d'utilisateur root, vous devez exécuter à nouveau la commande `ibmcloud login`.

Téléchargez l'image ; voir la rubrique relative à l'[extraction des images](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pulling) dans le guide de mise en route.

Si le message `unauthorized: authentication required` ou `denied: requested access to the resource is denied` s'affiche, exécutez la commande `ibmcloud cr login`.
{:tip}

Après avoir extrait une image et lui avoir attribué une étiquette pour votre espace de nom, vous pouvez la transférer (par commande push) depuis votre ordinateur local vers votre espace de nom.

## Envoi par commande push d'images Docker à votre espace de nom
{: #registry_images_pushing_namespace}

Vous pouvez transférer par commande push une image à votre espace de nom dans {{site.data.keyword.registrylong_notm}} pour la stocker et la partager avec d'autres utilisateurs.
{:shortdesc}

<img src="images/images_push.svg" width="800" style="width:800px;" alt="Transfert par commande push d'une image depuis votre ordinateur vers {{site.data.keyword.registrylong_notm}}."/>

**Avant de commencer**

- [Installez l'interface de ligne de commande](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) pour utiliser des images présentes dans votre espace de nom.
- [Configurez votre propre espace de nom dans {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Extrayez par commande pull](#registry_images_pulling_reg) ou [générez](#registry_images_creating) une image sur votre ordinateur local et étiquetez-la avec vos informations d'espace de nom.
- [Vérifiez que vous pouvez utiliser des commandes Docker sans disposer pour autant d'autorisations de niveau root![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/install/linux/linux-postinstall/). Si votre client Docker est configuré pour exiger des autorisations root, vous devez exécuter les commandes `ibmcloud login`, `ibmcloud cr login`, `docker pull` et `docker push` avec `sudo`.

  Si vous modifiez vos autorisations pour pouvoir exécuter des commandes Docker sans privilèges d'utilisateur root, vous devez exécuter à nouveau la commande `ibmcloud login`.

Pour télécharger (par push) une image, procédez comme suit :

1. Connectez-vous à l'interface de ligne de commande.

   ```
   ibmcloud cr login
   ```
   {: pre}

   Vous devez vous connecter si vous extrayez une image depuis votre registre {{site.data.keyword.registrylong_notm}} privé.
  {:tip}

2. Si vous désirez afficher tous les espaces de nom disponibles dans votre compte, exécutez la commande `ibmcloud cr namespace-list`.
3. [Téléchargez l'image par commande push vers votre espace de nom.](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)

   Si le message `unauthorized: authentication required` ou `denied: requested access to the resource is denied` s'affiche, exécutez la commande `ibmcloud cr login`.
   {:tip}

Après avoir envoyé à {{site.data.keyword.registrylong_notm}} l'image par commande push, vous pouvez effectuer l'une des tâches suivantes :

- [Gérer la sécurité avec Vulnerability Advisor](/docs/services/va?topic=va-va_index) pour rechercher des informations sur les vulnérabilités et les problèmes de sécurité potentiels.
- [Créer un cluster et utiliser cette image pour déployer un conteneur](/docs/containers?topic=containers-getting-started#getting-started) sur le cluster dans {{site.data.keyword.containerlong_notm}}.

## Copie d'images entre registres
{: #registry_images_copying}

Vous pouvez extraire une image depuis un registre dans une région donnée, puis la transférer par commande push vers une autre région afin de pouvoir partager l'image avec les utilisateurs dans les deux régions.
{:shortdesc}

<img src="images/images_copy.svg" width="800" style="width:800px;" alt="Copier une image depuis un registre privé ou public dans votre registre privé {{site.data.keyword.cloud_notm}}."/>

**Avant de commencer**

- [Installez l'interface de ligne de commande](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) pour utiliser des images présentes dans votre espace de nom.
- [Configurez votre propre espace de nom dans {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Vérifiez que vous pouvez utiliser des commandes Docker sans disposer pour autant d'autorisations de niveau root![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/install/linux/linux-postinstall/). Si votre client Docker est configuré pour exiger des autorisations root, vous devez exécuter les commandes `ibmcloud login`, `ibmcloud cr login`, `docker pull` et `docker push` avec `sudo`.

  Si vous modifiez vos autorisations pour pouvoir exécuter des commandes Docker sans privilèges d'utilisateur root, vous devez exécuter à nouveau la commande `ibmcloud login`.

Pour copier une image entre deux registres, procédez comme suit :

1. [Extrayez (par commande pull) une image d'un registre](#registry_images_pulling_reg).
2. [Envoyez (par commande push) l'image à un autre registre](#registry_images_pushing_namespace). Prenez soin d'utiliser le nom de domaine correct correspondant à la nouvelle région que vous ciblez.

Après avoir copié votre image, vous pouvez effectuer l'une des tâches suivantes :

- [Gérer la sécurité des images avec Vulnerability Advisor](/docs/services/va?topic=va-va_index) pour rechercher des informations sur les vulnérabilités et les problèmes de sécurité potentiels.
- [Créer un cluster et utiliser cette image pour déployer un conteneur](/docs/containers?topic=containers-getting-started#getting-started) sur le cluster dans {{site.data.keyword.containerlong_notm}}.

## Création de nouvelles images qui font référence à une image source
{: #registry_images_source}

Dans la région dans laquelle vous êtes connecté, créez une nouvelle image dans {{site.data.keyword.registrylong_notm}} qui fait référence à une image existante dans la même région. Cette action est prise en charge pour les images source créées à l'aide de Docker Engine version 1.12 ou ultérieure uniquement.

Les nouvelles images qui sont créées au moyen de ce mécanisme ne conservent pas de signatures. Si la nouvelle image doit être signée, n'utilisez pas ce mécanisme.
{: tip}

**Avant de commencer**

- [Installez l'interface de ligne de commande](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) pour utiliser des images présentes dans votre espace de nom.
- Assurez-vous que vous avez accès à un espace de nom privé dans {{site.data.keyword.registrylong_notm}} qui contient une image source à laquelle une autre image doit faire référence.

Pour plus d'informations sur la commande, voir [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag).

Pour créer une nouvelle image à partir d'une image source, procédez comme suit :

1. Connectez-vous à l'interface de ligne de commande.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Exécutez la commande suivante pour ajouter la nouvelle référence, où `SOURCE_IMAGE` est le nom de votre image source et `TARGET_IMAGE` est le nom de votre image cible. Les images source et cible doivent se trouver dans la même région. `SOURCE_IMAGE` et `TARGET_IMAGE` doivent être au format `<REPOSITORY>:<TAG>`, par exemple : `us.icr.io/namespace/image:latest`

   ```
   ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
   ```
   {: pre}

3. Vérifiez que la nouvelle image a été créée en exécutant la commande suivante, puis assurez-vous que l'image apparaît dans la liste avec le même historique des images que l'image source.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

## Génération d'images Docker pour les utiliser avec votre espace de nom
{: #registry_images_creating}

Vous pouvez générer une image Docker directement dans {{site.data.keyword.cloud_notm}} ou créer votre propre image Docker sur votre ordinateur local et la télécharger (par commande push) dans votre espace de nom dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Avant de commencer**

- [Installez l'interface de ligne de commande](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) pour utiliser des images présentes dans votre espace de nom.
- [Configurez votre propre espace de nom dans {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Vérifiez que vous pouvez utiliser des commandes Docker sans disposer pour autant d'autorisations de niveau root![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/install/linux/linux-postinstall/). Si votre client Docker est configuré pour exiger des autorisations root, vous devez exécuter les commandes `ibmcloud login`, `ibmcloud cr login`, `docker pull` et `docker push` avec `sudo`.

  Si vous modifiez vos autorisations pour pouvoir exécuter des commandes Docker sans privilèges d'utilisateur root, vous devez exécuter à nouveau la commande `ibmcloud login`.

Une image Docker est la base de chaque conteneur que vous créez. L'image est créée depuis un Dockerfile, lequel est un fichier contenant des instructions pour générer l'image. Un Dockerfile peut référencer dans ses instructions des artefacts de génération stockés séparément, comme une application, sa configuration, et ses dépendances.

Si vous voulez tirer profit des ressources de calcul d'{{site.data.keyword.cloud_notm}} ou d'une connexion internet ou si Docker n'est pas installé sur votre poste de travail, générez votre image directement sous {{site.data.keyword.cloud_notm}}. Si vous avez besoin d'accéder aux ressources de votre génération figurant sur des serveurs en dehors de votre pare-feu, générez votre image localement.

Pour générer votre propre image Docker, procédez comme suit :

1. Créez un répertoire local dans lequel stocker le contexte de génération. Ce dernier contient votre fichier Dockerfile et les artefacts de génération associés, comme le code d'application. Accédez à ce répertoire depuis une fenêtre de ligne de commande.
2. Créez un fichier Dockerfile.
    1. Créez un fichier Dockerfile sous votre répertoire local.

        ```
        touch Dockerfile
        ```
        {: pre}

    2. Utilisez un éditeur de texte pour ouvrir le Dockerfile. Au minimum, vous devez ajouter l'image de base depuis laquelle générer votre image. Remplacez `<source_image>` et `<tag>` par le référentiel d'images et la balise que vous voulez utiliser. Si vous utilisez une image d'un autre registre privé, définissez le chemin d'accès complet à l'image dans {{site.data.keyword.registrylong_notm}}.

       ```
       FROM <source_image>:<tag>
       ```
       {: pre}

       **Exemple**
     Pour créer un fichier Dockerfile basé sur l'image publique {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty (ibmliberty), utilisez le code suivant :

       ```
       FROM <region>.icr.io/ibmliberty:latest
       LABEL description="This is my test Dockerfile"
       EXPOSE 9080
       ```
       {: pre}

       Cet exemple ajoute un libellé aux métadonnées de l'image et expose le port 9080. Pour connaître les autres instructions Dockerfile que vous pouvez utiliser, voir le document [Dockerfile Reference![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/engine/reference/builder/).

3. Choisissez un nom pour votre image. Ce nom doit avoir le format suivant :

   ```
   <region>.icr.io/<my_namespace>/<repo_name>:<tag>
   ```
   {: pre}

   Où `<my_namespace>` correspond aux informations sur votre espace de nom, `<repo_name>` est le nom de votre référentiel et `<tag>` la version que vous voulez utiliser pour votre image. Pour identifier votre espace de nom, exécutez la commande `ibmcloud cr namespace-list`.

4. Prenez note du chemin d'accès au répertoire qui contient votre fichier Dockerfile. Si vous exécutez les commandes des procédures suivantes alors que votre répertoire de travail est défini sur l'emplacement où est stocké votre contexte de génération, vous pensez remplacer `<directory>` par un point (.).
5. Vous pouvez générer directement votre image dans
{{site.data.keyword.cloud_notm}} ou la générer et la tester localement avant de la transférer à
{{site.data.keyword.cloud_notm}}.
   - Pour générer l'image dans {{site.data.keyword.cloud_notm}}, exécutez la commande suivante :

     ```
     ibmcloud cr build -t <image_name> <directory>
     ```
     {: pre}

     où `<image_name>` est le nom de votre image et `<directory>` le chemin d'accès au répertoire. Si vous exécutez la commande alors que votre répertoire de travail est défini sur l'emplacement où est stocké votre contexte de génération, vous pensez remplacer `<directory>` par un point (.).
  
     Pour plus d'informations sur la commande `ibmcloud cr build`, voir [Interface de ligne de commande {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).

   - Pour générer et tester votre image localement avant de la transférer par push à {{site.data.keyword.cloud_notm}}, procédez comme suit :
      1. Générez l'image depuis votre fichier Dockerfile sur votre ordinateur local et étiquetez-la avec votre nom d'image.

         ```
         docker build -t <image_name> <directory>
         ```
         {: pre}

         où `<image_name>` est le nom de votre image et `<directory>` le chemin d'accès au répertoire. 

      2. Facultatif : testez votre image sur votre ordinateur local avant de la transférer par commande push vers votre espace de nom.

         ```
         docker run <image_name>
         ```
         {: pre}

         Remplacez `<image_name>` par le nom de votre image.

      3. Après avoir créé votre image et l'avoir étiquetée pour votre espace de nom, [vous pouvez l'envoyer par commande push dans {{site.data.keyword.registrylong_notm}}](#registry_images_pushing_namespace).

Pour utiliser Vulnerability Advisor pour vérifier la sécurité de votre image, voir [Gestion de la sécurité des images avec Vulnerability Advisor](/docs/services/va?topic=va-va_index).

## Envoi par commande push d'images à {{site.data.keyword.registrylong_notm}} en utilisant une clé d'API
{: #registry_api_key_push_image}

Créez un ID de service qui utilise une clé d'API pour envoyer des images par commande push à {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Créez un ID de service. Voir [Création et gestion des ID de service](/docs/iam?topic=iam-serviceids#serviceids).
2. Créez une règle donnant à l'ID de service le droit d'accéder au registre, par exemple les rôles `Administrator` et `Manager`. Voir [Gestion des accès utilisateur à l'aide d'Identity and Access Management](/docs/services/Registry?topic=registry-iam#iam).
3. Créez une clé d'API. Voir [Création d'une clé d'API pour un ID de service](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
4. Utilisez la clé d'API pour la connexion au registre afin de pouvoir envoyer par commande push des images au registre. Voir [Utilisation d'une clé d'API pour automatiser l'accès](/docs/services/Registry?topic=registry-registry_access#registry_api_key_use).
5. Envoyez vos images par commande push. Voir [Envoi par commande push d'images Docker à votre espace de nom](#registry_images_pushing_namespace).

Vous pouvez à présent utiliser des clusters pour extraire les images. Voir [Génération de conteneurs à partir d'images](/docs/containers?topic=containers-images#other_registry_accounts).

## Suppression d'images de votre référentiel {{site.data.keyword.cloud_notm}} privé
{: #registry_images_remove}

Vous pouvez supprimer des images non désirées de votre référentiel privé en utilisant l'interface graphique ou l'interface de ligne de commande.
{:shortdesc}

Si vous souhaitez supprimer un référentiel privé et les pages qui lui sont associées, voir [Suppression d'un référentiel privé et des pages qui lui sont associées](#registry_repo_remove).

Les images {{site.data.keyword.IBM_notm}} publiques ne peuvent pas être supprimées de votre référentiel {{site.data.keyword.cloud_notm}} privé, et elles ne sont pas décomptées de votre quota.

La suppression d'une image est irréversible. La suppression d'une image qui est utilisée par un déploiement existant peut entraîner l'échec d'une augmentation et/ou d'une replanification.
{:tip}

### Suppression d'images de votre référentiel {{site.data.keyword.cloud_notm}} privé à l'aide de l'interface de ligne de commande
{: #registry_images_remove_cli}

Vous pouvez supprimer des images non désirées de votre référentiel privé en utilisant l'interface de ligne de commande.
{:shortdesc}

La suppression d'une image est irréversible. La suppression d'une image qui est utilisée par un déploiement existant peut entraîner l'échec d'une augmentation et/ou d'une replanification.
{:tip}

Pour supprimer une image à l'aide de l'interface de ligne de commande, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.cloud_notm}} en exécutant la commande `ibmcloud login`.
2. Pour supprimer une image, exécutez la commande suivante :

   ```
   ibmcloud cr image-rm IMAGE
   ```
   {: pre}

   Où _IMAGE_ est le nom de l'image que vous souhaitez retirer, au format `repository:tag`.

   Si aucune étiquette n'est spécifiée dans le nom de l'image, l'image associée à l'étiquette `latest` est supprimée par défaut. Vous pouvez supprimer plusieurs images en listant dans la commande chaque chemin de registre {{site.data.keyword.cloud_notm}} privé et en les séparant par un espace.

   Pour trouver les noms de vos images, exécutez `ibmcloud cr image-list`. Associez le contenu des colonnes Repository et Tag pour créer le nom de l'image au format `repository:tag`.
   {:tip}

3. Vérifiez que l'image a bien été supprimée en exécutant la commande suivant, puis assurez-vous que l'image n'apparaît pas dans la liste :

   ```
   ibmcloud cr image-list
   ```
   {: pre}

### Suppression d'images de votre référentiel {{site.data.keyword.cloud_notm}} privé à l'aide de l'interface graphique
{: #registry_images_remove_gui}

Vous pouvez supprimer des images non désirées de votre référentiel d'images privé en utilisant l'interface graphique.
{:shortdesc}

La suppression d'une image est irréversible. La suppression d'une image qui est utilisée par un déploiement existant peut entraîner l'échec d'une augmentation et/ou d'une replanification.
{:tip}

Pour supprimer une image à l'aide de l'interface graphique, procédez comme suit :

1. Connectez-vous à la console {{site.data.keyword.cloud_notm}} ([https://cloud.ibm.com/login ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login)) avec votre IBMid.
2. Si vous disposez de plusieurs comptes {{site.data.keyword.cloud_notm}}, sélectionnez le compte et la région à utiliser dans le menu Compte.
3. Cliquez sur **Catalogue**.
4. Sélectionnez la catégorie **Conteneurs** et cliquez sur la vignette **Container Registry**.
5. Cliquez sur **Images**. La liste de vos images s'affiche.
6. Sur la ligne qui contient l'image à supprimer, cochez la case.

   Cette action ne peut pas être annulée, par conséquent, vérifiez que l'image sélectionnée est bien celle que vous souhaitez supprimer.
   {: tip}

7. Cliquez sur **Supprimer l'image**.

## Suppression d'un référentiel privé et des images qui lui sont associées
{: #registry_repo_remove}

Vous pouvez supprimer les référentiels privés dont vous n'avez plus besoin, ainsi que les images qui leur sont associées, en utilisant l'interface graphique.
{:shortdesc}

Lorsque vous supprimez un référentiel, toutes les images qu'il contient sont également supprimées. Cette action est irréversible.
{:tip}

**Avant de commencer**

Vous devez sauvegarder les images que vous souhaitez conserver.

Pour supprimer un référentiel privé à l'aide de l'interface graphique, procédez comme suit :

1. Connectez-vous à la console {{site.data.keyword.cloud_notm}} ([https://cloud.ibm.com/login ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login)) avec votre IBMid.
2. Si vous disposez de plusieurs comptes {{site.data.keyword.cloud_notm}}, sélectionnez le compte et la région à utiliser dans le menu Compte.
3. Cliquez sur **Catalogue**.
4. Sélectionnez la catégorie **Conteneurs** et cliquez sur la vignette **Container Registry**.
5. Cliquez sur **Référentiels**. La liste de vos référentiels privés s'affiche.
6. Sur la ligne qui contient le référentiel privé à supprimer, cochez la case.

    Cette action ne peut pas être annulée, par conséquent, vérifiez que le référentiel sélectionné est bien celui que vous souhaitez supprimer.
    {: tip}

7. Cliquez sur **Supprimer le référentiel**.
