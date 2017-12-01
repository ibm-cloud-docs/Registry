---

copyright:
  years: 2017
lastupdated: "2017-10-30"

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

Pour plus
d'informations sur l'utilisation des forums, voir [Comment obtenir de l'aide](../../support/index.html#getting-help).

Pour des informations sur l'ouverture d'un ticket de demande de service {{site.data.keyword.IBM_notm}} ou sur les niveaux de support et les gravités de ticket, voir [Contacter le service de support](../../support/index.html#contacting-support).

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

