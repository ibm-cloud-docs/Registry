---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security


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

# Initiation à {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}}
fournit un registre d'images privé à service partagé que vous pouvez utiliser pour
stocker et partager vos images Docker avec les utilisateurs de
votre compte {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La console {{site.data.keyword.Bluemix_notm}} inclut une brève section Démarrage rapide. Pour plus d'informations sur l'utilisation de la console {{site.data.keyword.Bluemix_notm}}, voir [Gestion de la sécurité des images avec Vulnerability Advisor](/docs/services/va/va_index.html).

Ne placez pas d'informations personnelles dans vos images de conteneur, noms d'espace de nom, zones de description (par exemple, dans des jetons de registre), ou dans des données de configuration d'image (par exemple, dans des noms d'image ou des libellés d'image).
{:tip}

## Installez l'interface de ligne de commande d'{{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1. Installez l'[interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview) pour pouvoir exécuter les commandes {{site.data.keyword.Bluemix_notm}} `ibmcloud`. Cette installation installe également les plug-in d'interface de ligne de commande pour {{site.data.keyword.containerlong_notm}} et {{site.data.keyword.registrylong_notm}}.

## Configurez un espace de nom
{: #registry_namespace_add}

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

## Extrayez vers votre machine locale des images d'un autre registre
{: #registry_images_pulling}

1. [Installez l'interface de ligne de commande de Docker ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.docker.com/community-edition#/download). Si
vous utilisez Windows 8, ou OS X Yosemite 10.10.x ou une version antérieure, installez [Docker Toolbox ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/toolbox/) à la place. {{site.data.keyword.registrylong_notm}} prend en charge Docker Engine v1.12.6 ou ultérieur.

2. Téléchargez (par commande _pull_) l'image vers votre machine locale. Remplacez `<source_image>` par le référentiel de l'image et `<tag>` par la balise de l'image que vous voulez utiliser, par exemple, _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Exemple, où `<source_image>` est `hello-world` et `<tag>` est `latest`:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Attribuez une étiquette à l'image. Remplacez `<source_image>` par le référentiel et `<tag>` par la balise de votre image locale extraite précédemment. Remplacez `<region>` par le nom de votre [région](/docs/services/Registry/registry_overview.html#registry_regions). Remplacez `<my_namespace>` par l'espace de nom que vous avez créé à l'étape [Configuration d'un espace de nom](/docs/services/Registry/index.html#registry_namespace_add). Définissez le référentiel et la balise que vous voulez utiliser dans votre espace de nom en remplaçant `<new_image_repo>` et `<new_tag>`.

   ```
   docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Exemple, où `<source_image>` est `hello-world`, `<tag>` est `latest`, `<region>` est `eu-gb`, `<my_namespace>` est `namespace1`, `<new_image_repo>` est `hw_repo` et `<new_tag>` est `1` :

   ```
   docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

## Transférez (par commande push) des images Docker vers votre espace de nom
{: #registry_images_pushing}

1. Exécutez la commande `ibmcloud cr login` pour connecter votre démon Docker local à {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Téléchargez (par commande _push_) l'image vers votre espace de nom. Remplacez `<my_namespace>` par l'espace de nom que vous avez créé à l'étape [Configuration d'un espace de nom](/docs/services/Registry/index.html#registry_namespace_add), et remplacez `<image_repo>` et `<tag>` par le référentiel et la balise de l'image choisie lorsque vous avez balisé l'image.

   ```
   docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}

   Exemple, où `<region>` est `eu-gb`, `<my_namespace>` est `namespace1`, `<image_repo>` est `hw_repo`et `<tag>` est `1`:

   ```
   docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
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

**Etape suivante ?**

- [Gestion de la sécurité des images avec Vulnerability Advisor](/docs/services/va/va_index.html)
- [Examen de vos plans de service et de leur utilisation](/docs/services/Registry/registry_overview.html#registry_plans)
- [Stockage et gestion davantage d'images dans votre espace de nom](/docs/services/Registry/registry_images_.html)
- [Définition des règles de rôle d'accès utilisateur](/docs/services/Registry/registry_users.html#user)
- [Configuration de clusters et de noeuds worker](/docs/containers/cs_clusters.html#clusters)
