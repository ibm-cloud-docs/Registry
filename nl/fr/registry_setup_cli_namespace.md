---

copyright:
  years: 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Configuration de l'interface de ligne de commande
d'{{site.data.keyword.registrylong_notm}} et de
l'espace de nom du registre
{: #registry_setup_cli_namespace}

Pour pouvoir stocker vos images Docker dans {{site.data.keyword.registrylong}}, vous devez installer l'interface de ligne de commande (CLI) de {{site.data.keyword.Bluemix_notm}} et le plug-in {{site.data.keyword.registrylong_notm}}, puis configurer un espace de nom de registre afin de créer votre propre registre d'images dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc}


## Installation du plug-in (`bx cr`) de l'interface de ligne de commande d'{{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

Installez l'interface de ligne de commande d'{{site.data.keyword.registrylong_notm}} afin d'utiliser la ligne de commande pour gérer vos espaces de nom et vos images Docker dans le registre {{site.data.keyword.Bluemix_notm}} privé.
{:shortdesc}

1.  [Installez le plug-in container-registry.](index.html#registry_cli_install)
2.  Facultatif : [configurez votre client Docker pour pouvoir exécuter les commandes sans autorisations de niveau root](https://docs.docker.com/engine/installation/linux/linux-postinstall). Si vous n'effectuez pas cette étape, vous devez exécuter les commandes `bx login`, `bx cr login`, `docker pull` et `docker push` avec **sudo** ou en tant que root.

Vous pouvez à présent configurer votre propre espace de nom dans le registre {{site.data.keyword.registrylong_notm}} privé.

## Mise à jour du plug-in {{site.data.keyword.registrylong_notm}} (`bx cr`)
{: #registry_cli_update}

Vous pouvez mettre à jour l'interface de ligne de commande
d'{{site.data.keyword.registrylong_notm}}
régulièrement afin de bénéficier des nouvelles fonctionnalités.
{:shortdesc}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Mettez à jour le plug-in container-registry.

    ```
    bx plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  Vérifiez que le plug-in a été correctement mis à jour.

    ```
    bx plugin list
    ```
     {: pre}


## Désinstallation du plug-in {{site.data.keyword.registrylong_notm}} (`bx cr`)
{: #registry_cli_uninstall}

Si vous n'avez plus besoin du plug-in container-registry, vous pouvez
le désinstaller.
{:shortdesc}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Désinstallez le plug-in container-registry.

    ```
    bx plugin uninstall container-registry
    ```
    {: pre}

3.  Vérifiez que le plug-in a été correctement désinstallé.

    ```
    bx plugin list
    ```
    {: pre}

    Le plug-in container-registry n'apparaît pas dans les
résultats.


## Configuration d'un espace de nom
{: #registry_namespace_add}

Pour stocker de manière sécurisée vos images Docker, vous devez créer un
espace de nom dans le registre
{{site.data.keyword.registrylong_notm}} privé.
{:shortdesc}

Avant de commencer :

-   [Installez l'interface de ligne de commande (CLI) de {{site.data.keyword.Bluemix_notm}} et le plug-in container-registry](#registry_cli_install).
-   [Planifiez comment utiliser et nommer vos espaces de nom du registre](registry_overview.html#registry_namespaces).

Créez un espace de nom, voir [Configurez un espace de nom](index.html#registry_namespace_add) dans la documentation Initiation.

Vous pouvez à présent [ envoyer par commande push des images Docker à votre espace de nom dans le registre {{site.data.keyword.Bluemix_notm}}](registry_images_.html#registry_images_pushing) et partager ces images avec d'autres utilisateurs dans votre compte.

## Retrait d'espaces de nom
{: #registry_remove}

Si vous n'avez plus besoin d'un espace de nom de registre, vous pouvez le retirer de votre compte {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Répertoriez les espaces de nom disponibles.

    ```
    bx cr namespace-list
    ```
    {: pre}

3.  Supprimez un espace de nom. 

    **Attention :** quand vous retirez un espace de nom, les images qui y étaient stockées sont également supprimées. Cette action est irréversible.
    
    Remplacez _&lt;my_namespace&gt;_ par l'espace de nom que vous désirez supprimer.

    ```
    bx cr namespace-rm <my_namespace>
    ```
    {: pre}

    Après que vous ayez supprimé un espace de nom, et selon le nombre d'images qui y étaient stockées, quelques minutes peuvent s'écouler avant qu'il ne redevienne disponible pour une réutilisation.
