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


# Commandes {{site.data.keyword.registrylong_notm}} (`ibmcloud cr`) pour la gestion des images Docker dans votre espace de nom
{: #registry_cli_reference}

Vous pouvez utiliser le plug-in container-registry pour configurer votre propre espace de nom d'images dans un registre privé, hébergé et géré par IBM, dans lequel vous pouvez stocker et partager de manière sécurisée des images Docker avec tous les utilisateurs de votre compte {{site.data.keyword.Bluemix}}.
{:shortdesc}


## Commandes `ibmcloud cr`
{: #registry_cli_reference_bxcr}

Exécutez les commandes `ibmcloud cr` dans l'interface de ligne de commande d'{{site.data.keyword.registryshort_notm}}.
{:shortdesc}
  
Pour connaître les commandes prises en charge, voir [Interface de ligne de commande {{site.data.keyword.registrylong_notm}}](registry_cli.html).

## Formatage et filtrage de la sortie de l'interface de ligne de commande pour les commandes {{site.data.keyword.registrylong_notm}}
{: #registry_cli_listing}

Vous pouvez formater et filtrer la sortie de l'interface de ligne de commande des commandes {{site.data.keyword.registrylong_notm}} prises en charge.
{:shortdesc}

Par défaut, la sortie de l'interface de ligne de commande s'affiche dans un format lisible par l'utilisateur. Cependant, cette vue risque de limiter votre capacité à utiliser la sortie, particulièrement si la commande est exécutée à l'aide d'un programme. Ainsi, dans la sortie de l'interface de ligne de commande `ibmcloud cr image-list`, vous souhaiterez peut-être trier la zone `Size` par ordre de taille numérique, mais la commande renvoie une description de la taille sous forme de chaîne. Le plug-in container-registry fournit l'option format qui vous permet d'appliquer un modèle Go à la sortie de l'interface de ligne de commande. Le modèle Go est une fonction du [langage de programmation Go](https://golang.org/pkg/text/template/) que vous pouvez utiliser pour personnaliser la sortie de l'interface de ligne de commande.

Vous pouvez modifier la sortie de l'interface de ligne de commande en appliquant l'option format de deux façons différentes :

1.  En formatant les données de la sortie de l'interface de ligne de commande. Ainsi, vous pouvez remplacer le format de temps UNIX de la sortie de la zone `Created` par le format de temps standard.
2.  En filtrant les données de la sortie de l'interface de ligne de commande. Vous pouvez, par exemple, filtrer les détails de l'image et afficher un sous-ensemble spécifique d'images à l'aide de la condition `if gt` du modèle Go.

Vous pouvez utiliser l'option format avec les commandes {{site.data.keyword.registrylong_notm}} suivantes. Cliquez sur une commande pour afficher la liste de zones disponibles et des types de données associés.

-   [`ibmcloud cr image-list`](registry_cli_reference.html#registry_cli_listing_imagelist)
-   [`ibmcloud cr image-inspect`](registry_cli_reference.html#registry_cli_listing_imageinspect)
-   [`ibmcloud cr token-list`](registry_cli_reference.html#registry_cli_listing_tokenlist)

Les exemples de code suivants illustrent la manière dont vous pouvez utiliser les options de formatage et de filtrage.

-   Exécutez la commande `ibmcloud cr image-list` suivante pour afficher le référentiel, l'étiquette et le statut de sécurité de toutes les images dont la taille dépasse 1 Mo :

    ```
    ibmcloud cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
    ```
    {: pre}

    **Exemple de sortie**

    ```
    example-registry.<region>.bluemix.net/user1/ibmliberty:latest No Issues
    example-registry.<region>.bluemix.net/user1/ibmnode:1 2 Issues
    example-registry.<region>.bluemix.net/user1/ibmnode:test1 1 Issue
    example-registry.<region>.bluemix.net/user1/ibmnode2:test2 7 Issues
    ```
    {: screen}


-   Exécutez la commande `ibmcloud cr image-inspect` suivante pour afficher l'emplacement d'hébergement de la documentation IBM pour une image publique IBM spécifique :

    ```
    ibmcloud cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"

    ```
    {: pre}

    **Exemple de sortie**

    ```
    map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
    ```
    {: screen}

-   Exécutez la commande `ibmcloud cr image-inspect` suivante afin d'afficher les ports exposés pour une image spécifiée :

    ```
    ibmcloud cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"
    ```
    {: pre}

    **Exemple de sortie**

    ```
    map[9080/tcp: 9443/tcp:]
    ```
    {: screen}

-   Exécutez la commande `ibmcloud cr token-list` suivante pour afficher tous les jetons en lecture seule :

    ```
    ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
    {: pre}

    **Exemple de sortie**

    ```
    0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
    ```
    {: screen}


### Options du modèle Go et types de données dans la commande `ibmcloud cr image-list`
{: #registry_cli_listing_imagelist}

Consultez le tableau suivant pour connaître les options du modèle Go et les types de données disponibles pour la commande `ibmcloud cr image-list`.
{:shortdesc}

|Zone|Type|Description|
|-----|----|-----------|
|`Created`|Entier (64 bits)|Affiche la date de création de l'image, en nombre de secondes au [format de temps UNIX](https://en.wikipedia.org/wiki/Unix_time).|
|`Digest`|Chaîne|Affiche l'identificateur unique de l'image.|
|`Namespace`|Chaîne|Affiche l'espace de nom dans lequel l'image est stockée.|
|`Repository`|Chaîne|Affiche le référentiel de l'image.|
|`Size`|Entier (64 bits)|Affiche la taille de l'image en octets.|
|`Tag`|Chaîne|Affiche l'étiquette de l'image.|
|`SecurityStatus`|Struct|Affiche le statut de vulnérabilité de l'image. Vous pouvez filtrer et mettre en forme les valeurs suivantes : Status  `string`, IssueCount  `int` et ExemptionCount  `int`. Les statuts possibles sont décrits dans [Examen d'un rapport de vulnérabilité via l'interface de ligne de commande](../va/va_index.html#va_registry_cli).|
{: caption="Tableau 1. Zones et types de données disponibles dans la commande <codeibmcloud cr image-list</code>." caption-side="top"}

### Options du modèle Go et types de données dans la commande `ibmcloud cr image-inspect`
{: #registry_cli_listing_imageinspect}

Consultez le tableau suivant pour connaître les options du modèle Go et les types de données disponibles pour la commande `ibmcloud cr image-inspect`.
{:shortdesc}

|Zone|Type|Description|
|-----|----|-----------|
|`ID`|Chaîne|Affiche l'identificateur unique de l'image.|
|`Parent`|Chaîne|Affiche l'ID de l'image parent qui a été utilisée pour la génération de cette image.|
|`Comment`|Chaîne|Affiche la description de l'image.|
|`Created`|Chaîne|Affiche l'[horodatage UNIX](https://en.wikipedia.org/wiki/Unix_time) de la création de l'image.|
|`Container`|Chaîne|Affiche l'ID du conteneur ayant créé l'image.|
|`ContainerConfig`|Objet|Affiche la configuration par défaut des conteneurs démarrés à partir de cette image. Pour plus de détails sur cette zone, voir [Config](registry_cli_reference.html#config).|
|`DockerVersion`|Chaîne|Affiche la version de Docker utilisée pour la génération de cette image.|
|`Author`|Chaîne|Affiche l'auteur de l'image.|
|`Config`|Objet|Affiche les métadonnées de configuration de l'image. Pour plus de détails sur cette zone, voir [Config](registry_cli_reference.html#config).|
|`Architecture`|Chaîne|Affiche l'architecture de processeur utilisée pour la génération de cette image et requise pour son exécution.|
|`Os`|Chaîne|Affiche la famille de système d'exploitation utilisée pour la génération de cette image et requise pour son exécution.|
|`OsVersion`|Chaîne|Affiche la version du système d'exploitation utilisé pour la génération de cette image.|
|`Size`|Entier (64 bits)|Affiche la taille de l'image en octets.|
|`VirtualSize`|Entier (64 bits)|Affiche la somme des tailles de chaque couche de l'image en octets.|
|`RootFS`|Objet|Affiche les métadonnées qui décrivent le système de fichiers racine de l'image. Pour plus de détails sur cette zone, voir [RootFS](registry_cli_reference.html#rootfs).|
{: caption="Tableau 2. Zones et types de données disponibles dans la commande <codeibmcloud cr image-inspect</code>." caption-side="top"}

#### Config

|Zone|Type|Description|
|-----|----|-----------|
|`Hostname`|Chaîne|Affiche le nom d’hôte du conteneur.|
|`Domainname`|Chaîne|Affiche le nom de domaine complet du conteneur.|
|`User`|Chaîne|Affiche l'utilisateur qui exécute les commandes dans le conteneur dans lequel l'image est utilisée.|
|`AttachStdin`|Booléen|Affiche _true_ si le flux d'entrée standard est associé au conteneur, et _false_ dans le cas contraire.|
|`AttachStdout`|Booléen|Affiche _true_ si le flux de sortie standard est associé au conteneur, et _false_ dans le cas contraire.|
|`AttachStderr`|Booléen|Affiche _true_ si le flux d'erreur standard est associé au conteneur, et _false_ dans le cas contraire.|
|`ExposedPorts`|Mappe de valeur de clé|Affiche la liste des ports exposés au format `[123:,456:]`.|
|`Tty`|Booléen|Affiche _true_ si une unité pseudo-tty est allouée au conteneur, et _false_ dans le cas contraire.|
|`OpenStdin`|Booléen|Affiche _true_ si le flux d'entrée standard est ouvert, et _false_ si le flux d'entrée standard est fermé.|
|`StdinOnce`|Booléen|Affiche _true_ si le flux d'entrée standard est fermé après la déconnexion du client associé, et _false_ si le flux d'entrée standard reste ouvert.|
|`Env`|Tableau de chaînes|Affiche la liste des variables d'environnement sous la forme de paires clé-valeur.|
|`Cmd`|Tableau de chaînes|Décrit les commandes et les arguments transmis à un conteneur et à exécuter au démarrage de ce dernier.|
|`Healthcheck`|Objet|Décrit comment vérifier que le conteneur fonctionne correctement. Pour plus de détails sur cette zone, voir [Healthcheck](registry_cli_reference.html#healthcheck).|
|`ArgsEscaped`|Booléen|Affiche true si la commande fait déjà l'objet d'un échappement (spécifique à Windows).|
|`Image`|Chaîne|Affiche le nom de l'image transmise par l'opérateur.|
|`Volumes`|Mappe de valeur de clé|Affiche la liste des montages de volume montés sur un conteneur.|
|`WorkingDir`|Chaîne|Affiche le répertoire de travail au sein du conteneur dans lequel les commandes spécifiées sont exécutées.|
|`=Entrypoint`|Tableau de chaînes|Décrit la commande exécutée au démarrage du conteneur.|
|`NetworkDisabled`|Booléen|Affiche _true_ si la mise en réseau est désactivée pour le conteneur, et _false_ si la mise en réseau est activée pour le conteneur.|
|`MacAddress`|Chaîne|Affiche l'adresse MAC affectée au conteneur.|
|`OnBuild`|Tableau de chaînes|Affiche les métadonnées ONBUILD définies sur le fichier Dockerfile de l'image.|
|`Labels`|Mappe de valeur de clé|Affiche la liste des libellés ajoutés à l'image sous forme de paires clé-valeur.|
|`StopSignal`|Chaîne|Décrit le signal d'arrêt UNIX à envoyer lorsqu'il faut arrêter le conteneur.|
|`StopTimeout`|Entier|Affiche le délai en secondes avant l'arrêt d'un conteneur.|
|`Shell`|Tableau de chaînes|Affiche le format shell de RUN, CMD, ENTRYPOINT.|
{: caption="Tableau 3. Zones et types de données disponibles dans Config. " caption-side="top"}

#### Healthcheck

|Zone|Type|Description|
|-----|----|-----------|
|`Test`|Tableau de chaînes|Affiche le mode d'exécution du diagnostic d'intégrité. Options disponibles :<ul><li>{} : hérite du diagnostic d'intégrité</li><li>{"NONE"} : le diagnostic d'intégrité est désactivé</li><li>{"CMD", args...} : arguments exec directement</li><li>{"CMD-SHELL", command} : exécute la commande avec le shell par défaut du système</li></ul>|
|`Interval`|Entier (64 bits)|Affiche la durée d'attente entre deux diagnostics d'intégrité en nanosecondes.|
|`Timeout`|Entier (64 bits)|Affiche la durée d'attente avant que le diagnostic d'intégrité ne soit considéré comme ayant échoué en nanosecondes.|
|`Retries`|Entier|Affiche le nombre d'échecs consécutifs à prendre en compte pour déterminer qu'un conteneur ne fonctionne pas correctement.|
{: caption="Tableau 4. Zones et types de données disponibles dans Healthcheck struct." caption-side="top"}

#### RootFS

|Option|Type|Description|
|------|----|-----------|
|`Type`|Chaîne|Affiche le type du système de fichiers.|
|`Layers`|Tableau de chaînes|Affiche les descripteurs de chaque couche de l'image.|
|`BaseLayer`|Chaîne|Affiche le descripteur de la couche de base de l'image.|
{: caption="Tableau 5. Zones et types de données disponibles dans RootFS struct." caption-side="top"}

### Options du modèle Go et types de données dans la commande `ibmcloud cr token-list`
{: #registry_cli_listing_tokenlist}

Consultez le tableau suivant pour connaître les options du modèle Go et les types de données disponibles pour la commande `ibmcloud cr token-list`.
{:shortdesc}

|Zone|Type|Description|
|-----|----|-----------|
|`ID`|Chaîne|Affiche l'identificateur unique d'un jeton.|
|`Expiry`|Entier (64 bits)|Affiche l'[horodatage UNIX](https://en.wikipedia.org/wiki/Unix_time) de l'expiration du jeton.|
|`ReadOnly`|Booléen|Affiche _true_ lorsque vous pouvez uniquement extraire des images, et _false_ lorsque vous pouvez envoyer des images par commande push et en extraire vers et depuis votre espace de nom.|
|`Description`|Chaîne|Affiche la description du jeton.|
{: caption="Tableau 6. Zones et types de données disponibles dans la commande <codeibmcloud cr token-list</code>." caption-side="top"}
