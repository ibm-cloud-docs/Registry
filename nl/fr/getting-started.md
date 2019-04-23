---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security, cli, namespaces, tutorial, Docker, images, registry

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

# Tutoriel d'initiation
{: #getting-started}

{{site.data.keyword.registrylong}} fournit un registre d'images privé à service partagé que vous pouvez utiliser pour stocker et partager vos images Docker avec les utilisateurs de votre compte {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La console {{site.data.keyword.Bluemix_notm}} inclut une brève section Démarrage rapide. Pour plus d'informations sur l'utilisation de la console {{site.data.keyword.Bluemix_notm}}, voir [Gestion de la sécurité des images avec Vulnerability Advisor](/docs/services/va?topic=va-va_index).

Ne placez pas d'informations personnelles dans vos images de conteneur, noms d'espace de nom, zones de description (par exemple, dans des jetons de registre), ou dans des données de configuration d'image (par exemple, dans des noms d'image ou des libellés d'image).
{: important}

## Installation de l'interface de ligne de commande {{site.data.keyword.registrylong_notm}}
{: #gs_registry_cli_install}

1. Installez l'[interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli) de manière à pouvoir exécuter les commandes {{site.data.keyword.Bluemix_notm}} `ibmcloud`. Cette installation installe également les plug-in d'interface de ligne de commande pour {{site.data.keyword.containerlong_notm}} et {{site.data.keyword.registrylong_notm}}.

## Configuration d'un espace de nom
{: #gs_registry_namespace_add}

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

   Si vous possédez un ID fédéré, connectez-vous à l'aide de la commande suivante :

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. Ajoutez un espace de nom pour créer votre propre registre d'images. Remplacez `<my_namespace>` par l'espace de nom de votre choix.

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

3. Pour vérifier que votre espace de nom a bien été créé, exécutez la commande `ibmcloud cr namespace-list`.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Extraction d'images d'un autre registre vers votre machine locale
{: #gs_registry_images_pulling}

1. [Installez l'interface de ligne de commande de Docker Engine ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.docker.com/products/docker-engine#/download). Si vous utilisez Windows 8, ou OS X Yosemite 10.10.x ou une version antérieure, installez [Docker Toolbox ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/toolbox/) à la place. {{site.data.keyword.registrylong_notm}} prend en charge Docker Engine v1.12.6 ou ultérieur.

2. Téléchargez (par commande _pull_) l'image vers votre machine locale. Remplacez `<source_image>` par le référentiel de l'image et `<tag>` par l'étiquette de l'image que vous voulez utiliser, par exemple, _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Exemple, où `<source_image>` est `hello-world` et `<tag>` est `latest` :

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Attribuez une étiquette à l'image. Remplacez `<source_image>` par le référentiel et `<tag>` par l'étiquette de votre image locale précédemment extraite. Remplacez `<region>` par le nom de votre [région](/docs/services/Registry?topic=registry-registry_overview#registry_regions). Remplacez `<my_namespace>` par l'espace de nom créé à l'étape [Configuration d'un espace de nom](/docs/services/Registry?topic=registry-index#registry_namespace_add). Définissez le référentiel et l'étiquette de l'image que vous voulez utiliser dans votre espace de nom en remplaçant `<new_image_repo>` et `<new_tag>`.

   ```
   docker tag <source_image>:<tag> <region>.icr.io/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Exemple, où `<source_image>` est `hello-world`, `<tag>` est `latest`, `<region>` est `uk`, `<my_namespace>` est `namespace1`, `<new_image_repo>` est `hw_repo` et `<new_tag>` est `1` :

   ```
   docker tag hello-world:latest uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

## Transfert d'images Docker (par commande Push) vers votre espace de nom
{: #gs_registry_images_pushing}

1. Exécutez la commande `ibmcloud cr login` pour connecter votre démon Docker local à {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Téléchargez (par commande _push_) l'image vers votre espace de nom. Remplacez `<my_namespace>` par l'espace de nom créé à l'étape [Configuration d'un espace de nom](/docs/services/Registry?topic=registry-index#registry_namespace_add) et `<image_repo>` et `<tag>` par le référentiel et l'étiquette de l'image sélectionnés lorsque vous avez étiqueté l'image.

   ```
   docker push <region>.icr.io/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}
   
   Exemple, où `<region>` est `uk`, `<my_namespace>` est `namespace1`, `<image_repo>` est `hw_repo` et `<tag>` est `1` :

   ```
   docker push uk.icr.io/namespace1/hw_repo:1
   ```
   {: pre}

3. Vérifiez que le transfert de l'image a abouti en exécutant la commande suivante.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Bien joué ! Vous avez configuré un espace de nom dans
{{site.data.keyword.registrylong_notm}} et avez
envoyé par commande push votre première image vers votre espace de nom.

## Etapes suivantes
{: #gs_get_start_next}

- [Gestion de la sécurité des images avec Vulnerability Advisor](/docs/services/va?topic=va-va_index)
- [Examen de vos plans de service et de leur utilisation](/docs/services/Registry?topic=registry-registry_overview#registry_plans)
- [Stockage et gestion davantage d'images dans votre espace de nom](/docs/services/Registry?topic=registry-registry_images_)
- [Définition des règles de rôle d'accès utilisateur](/docs/services/Registry?topic=registry-user#user)
- [Configuration de clusters et de noeuds worker](/docs/containers?topic=containers-clusters#clusters)
