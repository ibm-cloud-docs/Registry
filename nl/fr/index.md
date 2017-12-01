---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}


# Initiation à {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}}
fournit un registre d'images privées à service partagé que vous pouvez utiliser pour
stocker et partager de manière sécurisée vos images Docker avec les utilisateurs de
votre compte {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La console {{site.data.keyword.Bluemix_notm}} inclut une brève section Démarrage rapide. Pour plus d'informations sur l'utilisation de la console {{site.data.keyword.Bluemix_notm}}, voir [Affichage d'informations sur les images dans la console {{site.data.keyword.Bluemix_notm}}](registry_ui.html).


## Installez l'interface de ligne de commande (CLI) de {{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1.  Installez l'interface de ligne de commande [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://clis.ng.bluemix.net/ui/home.html) pour
pouvoir exécuter les commandes {{site.data.keyword.Bluemix_notm}} **bx**.
2.  Installez le plug-in container-registry :

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}


## Configurez un espace de nom
{: #registry_namespace_add}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Ajoutez un espace de nom pour créer votre propre registre d'images. Remplacez
_&lt;my_namespace&gt;_ par l'espace de nom de votre choix.

    ```
    bx cr namespace-add <my_namespace>
    ```
    {: pre}


## Extrayez vers votre machine locale des images d'un autre registre
{: #registry_images_pulling}

1.  [Installez l'interface de ligne de commande de Docker ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.docker.com/community-edition#/download). Si
vous utilisez Windows 8, ou OS X Yosemite 10.10.x ou une version antérieure, installez [Docker Toolbox ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.docker.com/products/docker-toolbox) à la place.

2.  Connectez-vous à l'interface de ligne de commande (CLI) :

    ```
    bx cr login
    ```
    {: pre}

    **Remarque :** vous devez vous connecter si vous extrayez une image depuis votre registre {{site.data.keyword.registrylong_notm}} privé.

3.  Téléchargez (par commande _pull_) l'image vers votre machine locale. Remplacez
_&lt;source_image&gt;_ par le référentiel de l'image et
_&lt;tag&gt;_ par l'étiquette de l'image que vous désirez utiliser (par exemple, _latest_).

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Exemple :

    ```
    docker pull hello-world:latest
    ```
    {: pre}

4.  Attribuez une étiquette à l'image. Remplacez _&lt;source_image&gt;_ par le référentiel et
_&lt;tag&gt;_ par celle de l'image locale extraite auparavant. Définissez le référentiel et l'étiquette de l'image que vous désirez utiliser dans votre espace de nom en remplaçant
_&lt;new_image_repo&gt;_ et _&lt;new_tag&gt;_.

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    Exemple :

    ```
    docker tag hello-world:latest registry.<region>.bluemix.net/my_namespace/hw_repo:1
    ```
    {: pre}


## Transférez (par commande Push) des images Docker vers votre espace de nom
{: #registry_images_pushing}

1.  Téléchargez (par commande _push_) l'image vers votre espace de nom. Remplacez
_&lt;my_namespace&gt;_ par l'espace de nom où vous désirez télécharger l'image et _&lt;image_repo&gt;_ et _&lt;tag&gt;_ par le référentiel et l'étiquette de l'image choisis lorsque vous lui avez attribué une étiquette.

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    Exemple :

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/hw_repo:1
    ```
    {: pre}

2.  Vérifiez que le transfert de l'image a abouti en exécutant la commande suivante.

    ```
    bx cr image-list
    ```
    {: pre}


Bien joué ! Vous avez configuré un espace de nom dans
{{site.data.keyword.registrylong_notm}} et avez
envoyé par commande push votre première image vers votre espace de nom.

**Etape suivante ?**

-   [Gestion de la sécurité des images avec Vulnerability Advisor](../va/va_index.html).
-   [Examinez vos plans de service et leur utilisation](registry_overview.html#registry_plans)
-   [Stockez et gérez davantage d'images dans votre espace de nom](registry_images_.html).
-   [Créez et déployez un conteneur vers un cluster Kubernetes à partir de votre image](../../containers/cs_cluster.html).

