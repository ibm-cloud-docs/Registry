---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing

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

# Configuration de l'interface de ligne de commande
d'{{site.data.keyword.registrylong_notm}} et de
l'espace de nom du registre
{: #registry_setup_cli_namespace}

Avant de pouvoir stocker vos images Docker dans {{site.data.keyword.registrylong}}, vous devez créer un espace de nom. Pour gérer des espaces de nom, installez le plug-in d'interface de ligne de commande `container-registry`.
{:shortdesc}

Ne placez pas d'informations personnelles dans vos images de conteneur, noms d'espace de nom, zones de description (par exemple, dans des jetons de registre), ou dans des données de configuration d'image (par exemple, dans des noms d'image ou des libellés d'image).
{:tip}

Avant de commencer, installez l'[interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

## Installation du plug-in d'interface de ligne de commande `container-registry`
{: #cli_namespace_registry_cli_install}

Installez le plug-in d'interface de ligne de commande `container-registry` afin d'utiliser la ligne de commande pour gérer vos espaces de nom et vos images Docker dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Installez le plug-in d'interface de ligne de commande `container-registry`.](/docs/services/Registry?topic=registry-index#registry_cli_install)
2. Facultatif : [Configurez votre client Docker pour exécuter des commandes sans autorisations de niveau root![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/engine/installation/linux/linux-postinstall). Si vous n'effectuez pas cette étape, vous devez exécuter les commandes `ibmcloud login`, `ibmcloud cr login`, `docker pull` et `docker push` avec **sudo** ou en tant qu'utilisateur root.

Vous pouvez à présent configurer votre propre espace de nom dans {{site.data.keyword.registrylong_notm}}.

## Mise à jour du plug-in d'interface de ligne de commande `container-registry`
{: #registry_cli_update}

Vous souhaiterez peut-être mettre à jour le plug-in d'interface de ligne de commande `container-registry` régulièrement afin de bénéficier de nouvelles fonctionnalités.
{:shortdesc}

1. Mettez à jour le fichier de plug-in d'interface de ligne de commande `container-registry`.

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. Vérifiez que le plug-in d'interface de ligne de commande `container-registry` a bien été mis à jour.

    ```
    ibmcloud plugin list
    ```
     {: pre}

## Désinstallation du plug-in d'interface de ligne de commande `container-registry`
{: #registry_cli_uninstall}

Si vous n'avez plus besoin du plug-in d'interface de ligne de commande `container-registry`, vous pouvez le désinstaller.
{:shortdesc}

1. Désinstallez le plug-on d'interface de ligne de commande `container-registry`.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. Vérifiez que le plug-in d'interface de ligne de commande `container-registry` a bien été désinstallé.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    Le plug-in d'interface de ligne de commande `container-registry` n'apparaît pas dans les résultats.

## Configuration d'un espace de nom
{: #registry_namespace_setup}

Vous devez créer un espace de nom pour stocker vos images Docker dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Avant de commencer**

- [Installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} et le plug-in d'interface de ligne de commande `container-registry`](/docs/services/Registry?topic=registry-index#registry_cli_install).
- [Planifiez comment utiliser et nommer vos espaces de nom du registre](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces).

Créez un espace de nom, voir [Configuration d'un espace de nom](/docs/services/Registry?topic=registry-index#registry_namespace_add) dans la documentation d'initiation.

Vous pouvez à présent [envoyer par commande push des images Docker à votre espace de nom dans {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) et partager ces images avec d'autres utilisateurs dans votre compte.

## Retrait d'espaces de nom
{: #registry_remove}

Si vous n'avez plus besoin d'un espace de nom de registre, vous pouvez le retirer de votre compte {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Répertoriez les espaces de nom disponibles.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. Supprimez un espace de nom.

    **Attention :** quand vous retirez un espace de nom, les images qui y étaient stockées sont également supprimées. Cette action est irréversible.

    Remplacez `<my_namespace>` par l'espace de nom que vous souhaitez retirer.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    Après que vous avez supprimé un espace de nom, quelques minutes peuvent s'écouler avant qu'il ne redevienne disponible pour une réutilisation.
