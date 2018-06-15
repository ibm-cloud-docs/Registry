---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# Traitement des incidents
{: #ts_index}

Vous trouverez ici les réponses aux questions fréquentes liées au traitement
des incidents concernant l'utilisation d'{{site.data.keyword.registrylong}}.
{:shortdesc}


## Aide et support pour {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Si vous rencontrez des problèmes ou des questions lors de l'utilisation
d'{{site.data.keyword.registrylong_notm}}, vous
pouvez rechercher des informations ou poser des questions via un forum. Vous pouvez également ouvrir un ticket de demande de service {{site.data.keyword.IBM_notm}}.

Lorsque vous posez une question sur un forum, marquez votre question à l'aide d'une
étiquette pour qu'elle soit vue par l'équipe de développement d'{{site.data.keyword.registrylong_notm}}.

-   Si vous avez des questions techniques sur le développement ou le déploiement d'une application avec
{{site.data.keyword.registrylong_notm}}, publiez votre question sur
[Stack
Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) et marquez votre question avec les étiquettes ibm-bluemix et container-registry.
-   Pour des questions relatives au service et aux instructions de mise en route, utilisez le forum [IBM developerWorks - dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Ajoutez
les étiquettes `bluemix` et `container-registry`.

Voir [Utilisation du centre de support](../../get-support/howtogetsupport.html#using-avatar) pour plus de détails sur l'utilisation des forums.
Pour des informations sur l'ouverture d'un ticket de demande de service {{site.data.keyword.IBM_notm}}, ou sur les niveaux de support et les degrés de gravité des tickets, voir [Ouverture d'un ticket de demande de service](../../get-support/howtogetsupport.html#open-ticket).

## La connexion à {{site.data.keyword.registrylong_notm}} échoue
{: #ts_login}

Vous ne parvenez pas à vous connecter à {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
La commande `bx cr login` échoue.

{: tsCauses}
-   Le plug-in container-registry est périmé et doit être mis à jour.
-   Docker n'est pas installé ou n'est pas en exécution sur votre machine locale.
-   Vos données d'identification {{site.data.keyword.Bluemix_notm}} ont expiré.

{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

-   Effectuez une mise à niveau vers la version la plus récente du plug-in {{site.data.keyword.registryshort_notm}}, voir [Mise à jour du plug-in {{site.data.keyword.registrylong_notm}} (`bx cr`)](registry_setup_cli_namespace.html#registry_cli_update).
-   Vérifiez que Docker est installé sur votre machine. S'il est déjà installé, redémarrez le démon Docker.
-   Exécutez à nouveau la commande `bx login` pour actualiser vos données d'identification de connexion à {{site.data.keyword.Bluemix_notm}}.
  
## L'exécution d'une commande pour {{site.data.keyword.registrylong_notm}} échoue avec `ECHEC Vous n'êtes pas connecté à IBM Cloud.` 
{: #ts_login_cloud}

Vous ne pouvez pas exécuter de commandes dans {{site.data.keyword.registrylong_notm}}, même si vous êtes connecté à {{site.data.keyword.Bluemix_notm}}.

{: tsSymptoms}
Toutes les commandes `bx cr` échouent.

{: tsCauses}
-   Le plug-in container-registry est périmé et doit être mis à jour.

{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

-   Effectuez une mise à niveau vers la version la plus récente du plug-in {{site.data.keyword.registryshort_notm}}, voir [Mise à jour du plug-in {{site.data.keyword.registrylong_notm}} (`bx cr`)](registry_setup_cli_namespace.html#registry_cli_update).



## Les commandes {{site.data.keyword.registrylong_notm}} échouent avec le message `'cr' is not a registered command. See 'bx help'. `
{: #ts_login_error}

Vous ne pouvez pas exécuter une commande `bx cr`, car `cr` n'est pas une commande `bx` enregistrée.

{: tsSymptoms}
Vous recevez un message d'erreur similaire à l'un des messages d'erreur suivants :

```
bx cr login 
'cr' is not a registered command. See 'bx help'.
```
{: pre}

```
bx cr namespace 
'cr' is not a registered command. See 'bx help'.
```
{: pre}

{: tsCauses}
-   Le plug-in container-registry n'est pas installé.


{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

-   Installez le plug-in container-registry, voir [Installation du plug-in (bx cr) de {{site.data.keyword.registryshort_notm}}](registry_setup_cli_namespace.html#registry_cli_install).


## Echec de la configuration d'un espace de nom
{: #ts_problem}

{: tsSymptoms}
Quand vous exécutez `bx cr namespace-add`, vous ne parvenez pas à définir la valeur que vous avez entrée en tant qu'espace de nom.

{: tsCauses}
-   Vous avez entré une valeur d'espace de nom qui est déjà utilisée par une autre
organisation {{site.data.keyword.Bluemix_notm}}.
-   Un espace de nom a récemment été supprimé et vous réutilisez son nom. Si l'espace de
nom supprimé contenait de nombreuses ressources, la suppression n'a peut-être pas été
entièrement traitée par {{site.data.keyword.registrylong_notm}}.
-   Vous avez utilisé des caractères non valides dans la valeur de l'espace de nom.

{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

-   Suivez les instructions affichées dans le message d'erreur renvoyé.
-   Vérifiez que vous avez saisi un espace de nom valide :
    -   Votre espace de nom doit comporter de 4 à 30 caractères.
    -   Votre espace de nom doit débuter par au moins une lettre ou un nombre.
    -   Votre espace de nom ne doit comporter que des lettres en minuscules, des chiffres ou des traits de soulignement (_).
-   Choisissez une autre valeur pour votre espace de nom.
-   Si vous recréez un espace de nom qui a été supprimé, et que ce dernier contenait de
nombreuses images, faites une nouvelle tentative ultérieurement.

## Echec de l'envoi par commande push ou de l'extraction (pull) d'une image Docker
{: #ts_pushpull}

{: tsSymptoms}
Lorsque vous exécutez des commandes pour transférer ou extraire des images Docker, vous rencontrez un message d'erreur. Le
message d'erreur varie selon la cause première. Les messages d'erreur potentiels sont les
suivants :

```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan
```
{: screen}

```
Vous
avez dépassé votre quota de trafic d'extraction (pull) pour le mois en cours. Consultez
votre quota de trafic d'extraction (pull) et votre plan de tarification.
```
{: screen}

```
Non autorisé : authentification requise
```
{: screen}

```
Refusé : l'accès demandé à la ressource a été refusé
```
{: screen}

{: tsCauses}
-   Docker n'est pas installé.
-   Le client Docker n'est pas connecté à {{site.data.keyword.registrylong_notm}}.
-   Il se peut que votre jeton d'accès {{site.data.keyword.Bluemix_notm}} ait expiré.
-   Vous avez dépassé la limite de quota pour le stockage ou le trafic d'extraction
(pull) défini pour votre compte {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

-   [Vérifiez que Docker est installé sur votre machine](index.html#registry_cli_install).
-   Vérifiez votre chemin d'installation Docker.
-   Connectez-vous à
{{site.data.keyword.Bluemix_notm}} en exécutant `bx login`. Connectez-vous
ensuite à l'interface de ligne de commande
d'{{site.data.keyword.registrylong_notm}} en
exécutant `bx cr login`.
-   [Examinez les limites de quota et l'utilisation du stockage et de
l'extraction des images Docker dans {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).

## Impossible d'extraire l'image la plus récente avec l'étiquette latest
{: #ts_docker_latest}

{: tsSymptoms}
Vous tentez d'exécuter la commande `docker pull`, mais celle-ci renvoie une
version de l'image qui n'est pas la version la plus récente générée.

{: tsCauses}
L'étiquette
`latest` est appliquée par défaut pour référencer une image lorsque vous
exécutez des commandes Docker sans spécifier de valeur pour l'étiquette. L'étiquette `latest` est appliquée à la commande
`docker build` ou `docker tag` la plus récente exécutée
sans qu'une étiquette n'ait été spécifiée explicitement. Il est donc possible
d'exécuter les commandes `docker` dans le désordre ou de définir des
étiquettes de manière explicite sur certaines images, l'étiquette `latest`
désignant une génération qui n'est pas la plus récente.

{: tsResolve}
En
général, il est préférable de définir explicitement chaque fois une étiquette séquentielle différente pour vos images et de ne pas
vous en remettre à l'étiquette `latest`.


## Impossible d'ajouter d'autres images IBM au registre
{: #ts_ppa}


{: tsSymptoms}
Lorsque vous tentez d'importer du contenu que vous avez utilisé dans d'autres produits IBM tels que {{site.data.keyword.Bluemix_notm}} Private, vous ne parvenez pas à stocker vos images et autres logiciels sous licence depuis [IBM Passport Advantage ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www-01.ibm.com/software/passportadvantage/index.html) dans le registre.

{: tsCauses}
Les progiciels tels que les images et les chartes Helm provenant d'IBM Passport Advantage doivent être importés dans le registre à l'aide de la commande `bx cr ppa-archive-load`.

{: tsResolve}
Avant de commencer :
* Connectez-vous à {{site.data.keyword.Bluemix_notm}} en exécutant `bx login [--sso]`.
* Connectez-vous à {{site.data.keyword.registrylong_notm}} en exécutant `bx cr login`.
* [Ciblez l'interface CLI `kubectl`](../../containers/cs_cli_install.html#cs_cli_configure) sur votre cluster.
* Si vous n'avez pas déjà configuré Helm dans votre cluster, [configurez Helm dans votre cluster maintenant](../../containers/cs_integrations.html#helm).
* Si vous souhaitez partager les chartes au sein de votre organisation, vous pouvez installer le [projet open source Chart Museum ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).

### Importation de produits IBM Passport Advantage à utiliser dans {{site.data.keyword.Bluemix_notm}}

1.  Procurez-vous le fichier compressé à importer depuis [IBM Passport Advantage![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www-01.ibm.com/software/passportadvantage/index.html).

2.  Ciblez la région à utiliser. Si vous ne connaissez pas le nom de la région, exécutez la commande sans la région, puis sélectionnez-en une.

    ```
    bx cr region-set <region>
    ```
    {: pre}

3.  Importez le fichier archive compressé. Indiquez le chemin d'accès au fichier compressé ainsi que l'espace de nom de registre auquel envoyer les images par commande push. 

    ```
    bx cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
    ```
    {: pre}

    Cette commande développe le fichier compressé, charge les images contenues dans votre client Docker local puis envoie par commande push les images à l'espace de nom de votre registre.
    
    Si vous souhaitez télécharger des chartes Helm depuis l'archive IBM Passport Advantage dans un chart museum, incluez les options suivantes dans la commande : `bx cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **Exemple de sortie** :
    ```
    user:~ user$ bx cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

    OK
    ```
    {: screen}

4.  Si le fichier compressé contient des chartes Helm, celles-ci sont placées dans un répertoire d'archivage appelé `ppa-import`, qui est créé dans votre répertoire de travail en cours. Ouvrez le répertoire pour obtenir le nom de la charge Helm, `<helm_chart>`, puis vérifiez-en les valeurs.

    ```
    helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    Si vous avez téléchargé des chartes dans un chart museum à l'étape précédente, vous pouvez utiliser `helm inspect` pour inspecter la charte dans le chart museum.
    {: tip}

5.  Configurez la charte Helm, `<helm_chart>`, en fonction des valeurs générées par la commande `helm inspect values`.

6.  Déployez la charte Helm, `<helm_chart>`, en utilisant la commande `helm install`. Vous pouvez remplacer les valeurs de la charte selon les besoins, en utilisant l'option `--set`.

    ```
    helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## L'accès au registre avec un pare-feu personnalisé échoue
{: #ts_firewall}

{: tsSymptoms}
Vous configurez dans votre environnement de développement un pare-feu supplémentaire avec des paramètres personnalisés pour le trafic réseau entrant et sortant. Lorsque vous tentez d'accéder à {{site.data.keyword.registrylong_notm}}, la connexion échoue.

{: tsCauses}
Votre pare-feu personnalisé requiert que certains groupes réseau soient ouverts au trafic réseau entrant et sortant pour permettre la communication vers et depuis le registre.

{: tsResolve}
Ouvrez les groupes réseau suivants dans votre pare-feu personnalisé.

1.  Notez l'adresse IP publique de la machine que vous désirez utiliser pour vous connecter à {{site.data.keyword.registrylong_notm}}. Si vous utilisez Kubernetes, utilisez l'adresse
IP publique de votre noeud d'agent. Extrayez l'adresse IP publique de votre noeud d'agent en exécutant la commande `bx cs workers <cluster_name_or_id>`, où *&lt;cluster_name_or_id&gt;* est le nom ou l'ID de votre cluster.
2.  Dans votre pare-feu, autorisez les connexions suivantes vers et depuis votre machine :
    -   Pour connectivité ENTRANTE vers votre machine, autorisez le trafic réseau depuis les groupes réseau source suivants vers l'adresse IP publique de destination de votre machine.

        `registry.bluemix.net`:

        ```
        169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   Pour connectivité SORTANTE depuis votre machine, utilisez les mêmes groupes réseau et autorisez le trafic réseau sortant depuis l'adresse IP publique source vers ces groupes réseau.

## Récupération de clés perdues ou compromises
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
Alors que vous utilisez du [contenu sécurisé](registry_trusted_content.html), vous ne pouvez plus gérer des images sécurisées parce que vos clés de signature sont perdues ou compromises.

{: tsCauses}
Votre clé de référentiel ou racine (root) est perdue ou compromise.

{: tsResolve}
Les options dont vous disposez pour récupérer des clés perdues ou compromises dépendent du type de clé : de référentiel ou racine :

*  Pour des [clés de référentiel](#trustedcontent_lostrepokey), vous pouvez générer un nouvel ensemble de clés de signature pour le référentiel.
*  Pour des [clés racine (root)](#trustedcontent_lostrootkey), vous pouvez demander la suppression du référentiel et la création d'un nouveau référentiel.

### Clés de référentiel
{: #trustedcontent_lostrepokey}

Si votre clé de référentiel est perdue ou compromise, générez un nouvel ensemble de clés de signature pour votre référentiel.
{:shortdesc}

**Remarque** : Le seul rôle de signature que vous pouvez faire pivoter est `targets`, c'est-à-dire l'administrateur du référentiel. Si d'autres rôles sont affectés, générez de nouvelles clés pour ces rôles, retirez les anciennes, puis ajoutez les nouvelles en tant que signataires.

Avant de commencer, récupérez la phrase passe de clé racine que vous avez créée la première fois que vous avez [envoyé par commande push une image signée](registry_trusted_content.html#trustedcontent_push).

1.  Installez la version d'interface CLI du [projet Notary](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli).

2.  [Configurez votre environnement de contenu sécurisé](registry_trusted_content.html#trustedcontent_setup).

3.  Notez l'URL figurant dans la commande d'exportation à l'étape précédente. Par exemple, `https://registry.ng.bluemix.net:4443`.

4.  Générez un jeton de registre.

    ```
    bx cr token-add --readwrite
    ```
    {: pre}

5.	Faites pivoter ces clés afin que le contenu signé à l'aide de ces clés ne soit plus sécurisé. Remplacez _&lt;URL&gt;_ par l'URL de la commande d'exportation notée à l'étape 2, puis _&lt;image&gt;_ par l'image dont la clé de référentiel est affectée.

    ```
    notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	Si vous y êtes invité, entrez la phrase passe de clé racine. Entrez ensuite une nouvelle phrase passe pour la nouvelle clé de référentiel lorsque vous y êtes invité. 

7.	[Envoyez par commande push une image signée](registry_trusted_content.html#trustedcontent_push) qui utilise les nouvelles clés de signature.

### Clés racine (root)
{: #trustedcontent_lostrootkey}

Si votre clé racine est perdue ou compromise, vous ne pouvez pas mettre à jour des référentiels de contenu sécurisé qui utilisaient cette clé racine.
{:shortdesc}

Vous pouvez [supprimer les espaces de nom](registry_setup_cli_namespace.html#registry_remove) dont les référentiels utilisent la clé racine affectée, ce qui supprimera vos images et données sécurisées.

Si l'espace de nom contient des référentiels dont les clés racine ne sont pas affectées, comme un espace de nom pour des images de production, vous souhaiterez peut-être ne supprimer que les données sécurisées associées à la clé racine affectée. Ouvrez un ticket de demande de service.

1.  [Contactez le support {{site.data.keyword.Bluemix_notm}}](../../get-support/howtogetsupport.html). Incluez une brève description de votre problème, l'ID compte, ainsi que la liste des espaces de nom contenant les référentiels d'images avec les clés racine affectées.

2.  Après que {{site.data.keyword.Bluemix_notm}} a adressé le problème, supprimez le référentiel Docker Content Trust sur votre machine locale.

    * Répertoire Linux et Mac : `~/.docker/trust/private` et `~/.docker/trust/tuf`

    * Répertoire Windows : `%HOMEPATH%\.docker\trust\private` et `%HOMEPATH%\.docker\trust\tuf`

    **Remarque** : Parce que la clé racine est affectée, cette étape supprime toutes les clés de signature, y compris pour les autres serveurs d'accréditation.

3.  Si vous utilisez [{{site.data.keyword.Bluemix_notm}} Image Enforcement](registry_security_enforce.html) dans votre cluster {{site.data.keyword.containershort_notm}}, redémarrez chaque pod de mise en application d'image. Pour déclencher Kubernetes pour effectuer automatiquement un redémarrage d'annulation des pods, vous pouvez changer certaines métadonnées sur le pod. Par exemple, [ciblez votre interface CLI Kubernetes sur votre cluster](../../containers/cs_cli_install.html#cs_cli_configure) et modifiez le déploiement.
    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  Générez des référentiels de contenu sécurisé.

    *  Si vous souhaitez créer un nouveau contenu sécurisé, [envoyez par commande push de nouvelles images signées](registry_trusted_content.html#trustedcontent_push).

    *  Si vous ne souhaitez pas changer le contenu sécurisé précédent, ajoutez une signature aux images les plus récentes du registre.

       ```
       docker trust sign <image>:<tag>
       ```
       {: pre}
       

## L'installation de Container Image Security Enforcement échoue avec `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists`
{: #ts_install_cise_fail}


{: tsSymptoms}
Votre installation de Container Image Security Enforcement a échoué et vous avez reçu le message suivant :

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
L'installation précédente a échoué et la désinstallation qui suit n'a pas retiré chaque travail (job) Kubernetes associé à l'installation.

{: tsResolve}
Retirez les travaux Kubernetes restants en exécutant la commande suivante :

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}
