---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

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

La console {{site.data.keyword.Bluemix_notm}} inclut une brève section Démarrage rapide. Pour plus d'informations sur l'utilisation de la console {{site.data.keyword.Bluemix_notm}}, voir [Surveillance de la vulnérabilité des images](registry_ui.html).

Ne placez pas d'informations personnelles dans vos images de conteneur, noms d'espace de nom, zones de description (par exemple, dans des jetons de registre), ou dans des données de configuration d'image (par exemple, dans des noms d'image ou des libellés d'image).
{:tip}



## Installez l'interface de ligne de commande d'{{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1.  Installez l'[interface de ligne de commande d'{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://clis.ng.bluemix.net/ui/home.html) pour pouvoir exécuter les commandes {{site.data.keyword.Bluemix_notm}} `ibmcloud`. 
2.  Installez le plug-in container-registry :

    ```
    ibmcloud plugin install container-registry -r Bluemix
    ```
    {: pre}


## Configurez un espace de nom
{: #registry_namespace_add}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Ajoutez un espace de nom pour créer votre propre registre d'images. Remplacez
_&lt;my_namespace&gt;_ par l'espace de nom de votre choix.

    ```
    ibmcloud cr namespace-add <my_namespace>
    ```
    {: pre}

3.  Pour vérifier que votre espace de nom a bien été créé, exécutez la commande `ibmcloud cr namespace-list`.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}




## Extrayez vers votre machine locale des images d'un autre registre
{: #registry_images_pulling}

1.  [Installez l'interface de ligne de commande de Docker ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.docker.com/community-edition#/download). Si
vous utilisez Windows 8, ou OS X Yosemite 10.10.x ou une version antérieure, installez [Docker Toolbox ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/toolbox/) à la place.

2.  Téléchargez (par commande _pull_) l'image vers votre machine locale. Remplacez
_&lt;source_image&gt;_ par le référentiel de l'image et
_&lt;tag&gt;_ par l'étiquette de l'image que vous désirez utiliser (par exemple, _latest_).

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    Exemple, où _&lt;source_image&gt;_ correspond à `hello-world` et _&lt;tag&gt;_ à `latest` :

    ```
    docker pull hello-world:latest
    ```
    {: pre}

3.  Attribuez une étiquette à l'image. Remplacez _&lt;source_image&gt;_ par le référentiel et
_&lt;tag&gt;_ par celle de l'image locale extraite auparavant. Remplacez _&lt;region&gt;_ par le nom de votre [région](registry_overview.html#registry_regions). Remplacez _&lt;my_namespace&gt;_ par l'espace de nom que vous avez créé lors de la tâche [Configuration d'un espace de nom](index.html#registry_namespace_add). Définissez le référentiel et l'étiquette de l'image que vous désirez utiliser dans votre espace de nom en remplaçant
_&lt;new_image_repo&gt;_ et _&lt;new_tag&gt;_.

    ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
    ```
    {: pre}

    Exemple, où _&lt;source_image&gt;_ correspond à `hello-world`, _&lt;tag&gt;_ à `latest`, _&lt;region&gt;_ à `eu-gb`, _&lt;my_namespace&gt;_ à `namespace1`, _&lt;new_image_repo&gt;_ à `hw_repo` et _&lt;new_tag&gt;_ à `1`:

    ```
    docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
    ```
    {: pre}



## Transférez (par commande push) des images Docker vers votre espace de nom
{: #registry_images_pushing}

1.  Exécutez la commande `ibmcloud cr login` pour connecter votre démon Docker local à {{site.data.keyword.registrylong_notm}}.

    ```
    ibmcloud cr login
    ```
    {: pre}

2.  Téléchargez (par commande _push_) l'image vers votre espace de nom. Remplacez _&lt;my_namespace&gt;_ par l'espace de nom que vous avez créé lors de la tâche [Configuration d'un espace de nom](index.html#registry_namespace_add) et _&lt;image_repo&gt;_ et _&lt;tag&gt;_ par le référentiel et l'étiquette de l'image choisie lorsque vous l'avez libellée.

    ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
    ```
    {: pre}

    Exemple, où _&lt;region&gt;_ correspond à `eu-gb`, _&lt;my_namespace&gt;_ à `namespace1`, _&lt;image_repo&gt;_ à `hw_repo` et _&lt;tag&gt;_ à `1`:

    ```
    docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
    ```
    {: pre}

3.  Vérifiez que le transfert de l'image a abouti en exécutant la commande suivante.

    ```
    ibmcloud cr image-list
    ```
    {: pre}


Bien joué ! Vous avez configuré un espace de nom dans
{{site.data.keyword.registrylong_notm}} et avez
envoyé par commande push votre première image vers votre espace de nom.


**Etape suivante ?**

-   [Gérez la sécurité des images avec Vulnerability Advisor](../va/va_index.html).
-   [Examinez vos plans de service et leur utilisation](registry_overview.html#registry_plans)
-   [Stockez et gérez davantage d'images dans votre espace de nom](registry_images_.html).
-   [Configurez des clusters et des noeuds worker](/docs/containers/cs_clusters.html#clusters).


