---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# A propos d'{{site.data.keyword.registrylong_notm}}
{: #registry_overview}

Utilisez {{site.data.keyword.registrylong}} pour stocker vos images Docker privées et y accéder de manière sécurisée dans une architecture hautement disponible et évolutive.
{:shortdesc}

{{site.data.keyword.registrylong_notm}} fournit un registre d'images privé à service partagé, hautement disponible et évolutif, hébergé et géré par IBM. Vous pouvez utiliser le registre privé en configurant votre propre espace de nom d'images et en envoyant par push des images Docker vers votre espace de nom.

<img src="images/registry_architecture.png" alt="Image décrivant comment vous pouvez interagir avec IBM Cloud Container Registry. Container Registry contient à la fois des référentiels privés et publics et des API pour interaction avec le service. Votre client Docker local peut envoyer et extraire des images vers et depuis vos référentiels privés dans le registre et extraire des images depuis les référentiels publics. L'interface utilisateur Web d'IBM Cloud (console) interagit avec l'API Container Registry pour recenser les images. L'interface de ligne de commande de Container Registry interagit avec l'API pour recenser, créer, inspecter et retirer des images, ainsi que pour d'autres fonctions d'administration. Votre client Docker local peut également envoyer et extraire des images depuis votre magasin d'images local vers d'autres registres."/>

**Figure 1. Comment {{site.data.keyword.registrylong_notm}} interagit avec vos images Docker**

Une image Docker est la base de chaque conteneur que vous créez. L'image est créée depuis un Dockerfile, lequel est un fichier contenant des instructions pour générer l'image. Un Dockerfile peut référencer dans ses instructions des artefacts de génération stockés séparément, comme une application, sa configuration, et ses dépendances. Les images sont généralement stockées dans un registre qui peut être accessible au public (registre public) ou configuré de sorte à limiter l'accès à un petit groupe d'utilisateurs (registre privé). Lorsque vous utilisez {{site.data.keyword.registrylong_notm}}, seuls les utilisateurs habilités à accéder à votre compte {{site.data.keyword.Bluemix_notm}} peuvent accéder à vos images.

Lorsque vous envoyez des images par commande push au registre, {{site.data.keyword.registrylong_notm}}, vous pouvez exploiter les fonctionnalités intégrées de Vulnerability Advisor qui les sonde pour détecter des vulnérabilités et des problèmes de sécurité potentiels. Vulnerability Advisor recherche les packages vulnérables dans des images de base Docker spécifiques et des vulnérabilités connues dans les paramètres de configuration des applications. Lorsque des vulnérabilités sont détectées, il fournit les informations correspondantes. Vous pouvez utiliser ces informations pour résoudre des problèmes de sécurité afin d'éviter le déploiement de conteneurs à partir d'images vulnérables.

Consultez le tableau suivant pour avoir une présentation des avantages liés à l'utilisation d'{{site.data.keyword.registrylong_notm}}.

|Avantage|Description|
|-------|-----------|
|Registre privé hautement disponible et évolutif|<ul><li>Configurez votre propre espace de nom d'images dans un registre privé à service partagé, hautement disponible et évolutif, hébergé et géré par IBM.</li><li>Stockez vos images Docker privées de manière sécurisée et partagez-les avec les utilisateurs de votre compte {{site.data.keyword.Bluemix_notm}}.</li></ul>|
|Conformité en matière de sécurité d'image avec Vulnerability Advisor|<ul><li>Bénéficiez d'une analyse automatique des images dans votre espace de nom.</li><li>Consultez les recommandations spécifiques au système d'exploitation pour résoudre d'éventuelles vulnérabilité et protéger vos conteneurs contre la compromission.</li></ul>|
|Limites de quota pour le stockage et le trafic d'extraction (pull)|<ul><li>Bénéficiez d'un stockage gratuit et d'un trafic d'extraction (pull) vers vos images privées jusqu'à ce que vous atteigniez votre quota gratuit.</li><li>Définissez des limites de quota personnalisées pour le volume de stockage et le trafic d'extraction (pull) par mois afin d'éviter de dépasser le niveau de paiement indiqué dans vos préférences.</li></ul>|
{: caption="Table 1. Avantages d'{{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Plans de service
{: #registry_plans}

Vous pouvez choisir le plan de service {{site.data.keyword.registrylong_notm}} gratuit ou le plan standard pour stocker vos images Docker et les rendre disponibles aux utilisateurs dans votre compte
{{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Le plan de service {{site.data.keyword.registrylong_notm}} détermine le volume de stockage et le trafic d'envoi d'images (commande pull) que vous pouvez utiliser pour vos images privées. Le plan de service est associé à votre compte {{site.data.keyword.Bluemix_notm}} et les limites de stockage et de trafic d'envoi d'images (commande pull) s'appliquent à tous les espaces de nom définis dans votre compte.

Le tableau suivant décrit les plans de service {{site.data.keyword.registrylong_notm}} disponibles et leurs caractéristiques. Pour plus d'informations sur la facturation et sur les conséquences du dépassement des limites du plan de service, voir [Limites de quota et facturation dans {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).

|Caractéristiques|Gratuit|Standard|
|---------------|----|--------|
|Description|Essayez le registre privé dans {{site.data.keyword.registrylong_notm}} pour stocker de manière sécurisée et partager vos images Docker. Il s'agit du plan de service par défaut lorsque vous configurez votre premier espace de nom dans {{site.data.keyword.registrylong_notm}}.|Tirez parti d'un stockage et d'un trafic d'envoi d'images (commande pull) illimités pour gérer les images Docker pour tous les espaces de nom dans votre compte {{site.data.keyword.Bluemix_notm}}.|
|Volume de stockage pour les images|500 Mo|Illimité|
|Trafic d'extraction (pull)|5 Go par mois|Illimité|
|Facturation|Si vous dépassez vos limites de stockage ou de trafic pull, vous ne pouvez plus transférer ou extraire d'images de votre espace de nom. Pour plus d'informations, voir [Limites de quota et facturation dans {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).|<ul><li>Stockage : vous êtes facturé par Go/mois d'utilisation. Le premier demi-Go/mois est gratuit. Vous êtes ensuite facturé comme indiqué dans la calculatrice de prix.</li><li>Trafic d'extraction (pull) : vous êtes facturé par gigaoctets utilisés par mois. Les 5 premiers Go sont gratuits. Vous êtes ensuite facturé comme indiqué dans la calculatrice de prix. Si vous dépassez vos limites de stockage ou de trafic pull, vous ne pouvez plus transférer ou extraire d'images de votre espace de nom. Pour plus d'informations sur le stockage, le trafic d'extraction (pull) et la calculatrice de prix, voir [Limites de quota et facturation dans {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).</li></ul>|
{: caption="Tableau 2. Plans {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Limites de quota et facturation
{: #registry_plan_billing}

Cette rubrique fournit des informations et des exemples de fonctionnement du processus de facturation et des limites de quota dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Chaque image est générée à partir de plusieurs couches, chacune d'entre elles représentant un changement incrémentiel à partir de l'image de base. Lorsque vous envoyez une image par commande push ou lorsque vous procédez à son extraction par commande pull, le volume de stockage et le trafic d'extraction (pull) nécessaires pour chaque couche sont ajoutés à votre utilisation mensuelle. Les couches identiques sont automatiquement partagées entre les images de votre compte {{site.data.keyword.Bluemix_notm}} et sont réutilisées lorsque vous créez d'autres images. Le stockage de chaque couche identique n'est facturé qu'une seule fois, quel que soit le nombre d'images de votre compte faisant référence à la couche.

Exemple d'envoi d'images par commande push :

> Vous envoyez une image par commande push à votre espace de nom basé sur l'image Ubuntu. L'image Ubuntu contient plusieurs couches. Comme vous ne disposez pas encore de ces couches dans votre compte, le volume de stockage requis pour ces couches est ajouté à votre utilisation mensuelle.
>
> Plus tard, vous créez une seconde image basée sur l'image. Vous apportez des changements à l'image de base Ubuntu, en ajoutant, par exemple, des commandes ou des fichiers supplémentaires à votre fichier Dockerfile. Chaque changement représente une nouvelle couche d'image. Lorsque vous envoyez la seconde image par commande push, {{site.data.keyword.registrylong_notm}} reconnaît que toutes les couches de l'image Ubuntu de base sont déjà stockées dans votre compte. Vous n'êtes alors pas facturé pour le stockage de ces couches une seconde fois, même si vous avez envoyé votre image par commande push à un autre espace de nom. {{site.data.keyword.registrylong_notm}} détermine la taille de toutes les nouvelles couches et ajoute le volume de stockage à votre utilisation mensuelle.

### Facturation du stockage et du trafic d'extraction (pull)
{: #registry_billing_traffic}

En fonction du plan de service que vous choisissez, vous êtes facturé pour le stockage et le trafic d'extraction (pull) que vous utilisez par mois.
{:shortdesc}

**Stockage : **

  Chaque plan de service {{site.data.keyword.registrylong_notm}} inclut un certain volume de stockage que vous pouvez utiliser pour stocker de manière sécurisée vos images Docker dans les espaces de nom de votre compte {{site.data.keyword.Bluemix_notm}}. Si vous bénéficiez du plan standard, vous êtes facturé en Go/mois d'utilisation. Le premier demi-Go/mois est gratuit. Si vous bénéficiez du plan gratuit, vous pouvez stocker vos images dans {{site.data.keyword.registrylong_notm}} gratuitement jusqu'à ce que vous atteigniez les limites de quota du plan gratuit. Un Go/mois correspond à une moyenne d'1 Go de stockage pour un mois (730 heures).

  Exemple pour le plan standard :

  > Vous utilisez 5 Go pour exactement la moitié du mois, puis envoyez par commande push plusieurs images dans votre espace de nom et utilisez 10 Go pour le reste du mois. Votre utilisation mensuelle est calculée comme suit :
  >
  > (5 Go x 0,5 (mois)) + (10 Go x 0,5 (mois)) = 2,5 + 5 = 7,5 Go/mois
  >
  > Avec le plan standard, le premier demi-Go/mois est gratuit ; par conséquent, vous ne payez que 7 Go/mois (7,5 Go/mois - 0,5 Go/mois).

  

**Trafic d'extraction (Pull) : **

  Chaque plan de service {{site.data.keyword.registrylong_notm}} inclut une certaine quantité de trafic d'extraction (pull) gratuite vers vos images privées stockées dans votre espace de nom. Le trafic d'extraction (pull) est la bande passante que vous utilisez lorsque vous procédez à l'extraction par commande pull d'une image à partir de votre espace de nom vers votre machine locale. Si vous bénéficiez du plan standard, vous êtes facturé en Go d'utilisation par mois. Les 5 premiers Go de chaque mois sont gratuits. Si vous bénéficiez du plan gratuit, vous pouvez extraire des images à partir de votre espace de nom jusqu'à ce que vous atteigniez la limite de quota du plan gratuit.

  Exemple pour le plan standard :

  > Au cours du mois, vous avez extrait des images qui contenaient des couches d'une taille totale de 14 Go. Votre utilisation mensuelle est calculée comme suit :
  >
  > Dans le plan standard, les 5 premiers Go par mois sont gratuits ; vous êtes donc facturés pour 9 Go (14 Go - 5 Go).

  

### Limites de quota pour le stockage et le trafic d'extraction (pull)
{: #registry_quota_limits}

En fonction du plan de service que vous choisissez, vous pouvez envoyer des images par commande push et en extraire par commande pull vers et depuis votre espace de nom jusqu'à ce que vous atteigniez vos limites de quota personnalisées ou spécifiques à votre plan.
{:shortdesc}

**Stockage : **

  Lorsque vous atteignez et dépassez les limites de quota de votre plan, vous ne pouvez pas envoyer d'image par commande push aux espaces de nom dans votre compte {{site.data.keyword.Bluemix_notm}} tant que vous n'avez pas [libéré d'espace en supprimant des images](registry_quota.html#registry_quota_freeup) de vos espaces de nom ou que vous n'avez pas [procédé à une mise à niveau vers le plan standard](#registry_plan_upgrade). Si vous définissez des limites de quota pour le stockage dans votre plan gratuit ou standard, vous pouvez aussi [augmenter cette limite de quota](registry_quota.html#registry_quota_set) pour réactiver l'envoi de nouvelles images par commande push.

  Exemple pour le plan standard :

  > Votre limite de quota en cours pour le stockage est définie sur 1 Go. Toutes les images privées stockées dans les espaces de nom de votre compte {{site.data.keyword.Bluemix_notm}} utilisent déjà 900 Mo de ce stockage. Vous disposez de 100 Mo de stockage disponible jusqu'à ce que vous atteigniez cette limite de quota. Un utilisateur souhaite envoyer par commande push une image de 2 Go située sur la machine locale. Puisque la limite de quota n'est pas encore atteinte, {{site.data.keyword.registrylong_notm}} autorise l'utilisateur à envoyer cette image par commande push.
  >
  > Une fois la commande push
terminée, {{site.data.keyword.registrylong_notm}}
détermine la taille réelle de l'image dans votre espace de nom, qui peut varier de la
taille sur la machine locale, et vérifie si la limite du stockage est atteinte. Dans cet
exemple, l'utilisation du stockage passe de 900 Mo à 2 Go. La limite de quota en cours
étant définie sur 1 Go,
{{site.data.keyword.registrylong_notm}} vous
empêche d'envoyer des images supplémentaires par commande push à l'espace de nom.

**Trafic d'extraction (Pull) : **

  Lorsque vous atteignez et dépassez les limites de quota de votre plan, vous ne pouvez
pas extraire d'image par commande pull à partir des espaces de nom de votre compte
{{site.data.keyword.Bluemix_notm}}, sauf si
vous patientez jusqu'au début de la période de facturation suivante, si vous
[procédez à la mise à niveau vers le plan
standard](#registry_plan_upgrade) ou si vous [augmentez vos
limites de quota pour le trafic d'extraction (pull)](registry_quota.html#registry_quota_set).

  Exemple pour
le plan standard :

  > Pour le mois, votre limite de quota pour le trafic
d'extraction
(pull) est définie sur 5 Go. Vous avez déjà extrait des images depuis vos espaces de nom
et avez utilisé 4,5 Go de ce trafic d'extraction (pull). Vous disposez de 0,5 Go de trafic d'extraction (pull) disponible avant d'atteindre votre limite de quota. Un utilisateur souhaite
extraire une image d'une taille de 1 Go depuis votre espace de nom. Puisque la limite de
quota n'est pas encore atteinte,
{{site.data.keyword.registrylong_notm}} autorise
l'utilisateur à extraire cette image par commande pull.
  >
  > Une fois l'image extraite,
{{site.data.keyword.registrylong_notm}} détermine la
bande passante que vous avez utilisée lors de l'extraction (pull) et vérifie si la limite
du trafic d'extraction (pull) est atteinte. Dans cet exemple, l'utilisation du trafic d'extraction (pull) passe de 4,5 Go à 5,5 Go. Votre limite de quota en cours étant définie sur 5
Go, {{site.data.keyword.registrylong_notm}}
vous empêche d'extraire des images par commande pull à partir de votre espace de nom.

### Estimation des coûts
{: #registry_estimating_costs}

Utilisez la calculatrice de prix {{site.data.keyword.Bluemix_notm}} pour estimer le coût de votre plan.
{:shortdesc}

Vous pouvez estimer le coût de votre application à l'aide des calculatrices de prix fournies par {{site.data.keyword.Bluemix_notm}}.

1.  Ouvrez la fiche de prix, voir la rubrique relative à la [tarification {{site.data.keyword.Bluemix_notm}}](https://www.ibm.com/cloud-computing/bluemix/pricing).
2.  Dans la section **Paiement à la carte**, cliquez sur **Estimez vos coûts avec notre calculatrice**. La calculatrice s'ouvre.
3.  Accédez à la section **Container Registry** sous **Prix des conteneurs**.
4.  Entrez vos estimations de stockage et de trafic dans les zones à cet effet.

L'estimation de vos coûts est affichée dans la calculatrice.

## Mise à niveau de votre plan de service
{: #registry_plan_upgrade}

Vous pouvez mettre à niveau votre plan de service afin
de tirer parti d'un stockage et d'un trafic d'extraction d'images (commande pull) illimités
pour gérer les images Docker de tous les espaces de nom dans votre compte
{{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Si vous ne connaissez pas le plan de service dont vous disposez, exécutez la commande `ibmcloud cr plan`.

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

    Si vous disposez d'un ID fédéré, utilisez `ibmcloud login --sso` pour vous connecter à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. Entrez votre nom d'utilisateur et utilisez l'URL fournie dans votre sortie d'interface de ligne de commande pour extraire votre code d'accès à usage unique. Si la connexion échoue alors que vous omettez l'option `--sso`
et aboutit en incluant l'option `--sso`, ceci indique que votre ID est fédéré.
    {:tip}

2.  Effectuez une mise à niveau vers le plan standard.

    ```
    ibmcloud cr plan-upgrade standard
    ```
    {: pre}

    Si vous disposez d'un compte {{site.data.keyword.Bluemix_notm}} Lite, vous devez effectuer une mise à niveau vers un compte {{site.data.keyword.Bluemix_notm}} de type Paiement à la carte ou Abonnement avant d'exécuter la commande `ibmcloud cr plan-upgrade`.{:tip}


## Notions élémentaires
{: #registry_planning}

Préparez-vous à stocker en sécurité et à partager vos images Docker avec {{site.data.keyword.registrylong_notm}} en vous familiarisant avec les notions élémentaires du registre.
{:shortdesc}

Ne placez pas d'informations personnelles dans vos images de conteneur, noms d'espace de nom, zones de description (par exemple, dans des jetons de registre), ou dans des données de configuration d'image (par exemple, dans des noms d'image ou des libellés d'image).{:tip}


### Explication des termes utilisés dans {{site.data.keyword.registrylong_notm}}
{: #terms}


<dl>
  <dt>Registre</dt>
  <dd>Un registre est un service qui fournit l'infrastructure où seront stockées des images Docker et qui sera accessible via l'URL de l'hôte du registre et un port facultatif. Les registres peuvent être soit accessibles au public (registre public), soit configurés de sorte que l'accès soit limité à un petit groupe d'utilisateurs (registre privé). {{site.data.keyword.registrylong_notm}} fournit
un registre d'images privé à service partagé, hautement disponible, hébergé et géré par
IBM. Vous pouvez utiliser le registre privé en configurant votre propre espace de
nom d'images et commencer à envoyer par commande push des images Docker vers votre
espace de nom.</dd>
</dl>

<dl>
  <dt>Espace de nom</dt>
  <dd>Les espaces de nom sont une façon d'organiser les référentiels de vos images dans {{site.data.keyword.registrylong_notm}}. L'espace de nom est associé à votre compte
{{site.data.keyword.Bluemix_notm}}. Quand vous configurez votre propre espace de nom dans {{site.data.keyword.registrylong_notm}}, l'espace de nom est ajouté à l'URL du registre comme suit : <code>registry.<em>&lt;region&gt;</em>.bluemix.net/my_namespace</code>.

  Chaque utilisateur dans votre compte {{site.data.keyword.Bluemix_notm}} peut visualiser et utiliser les images stockées dans l'espace de nom de votre registre. Vous pouvez définir plusieurs espaces de nom, par exemple pour disposer de référentiels distincts pour votre environnement de production et votre
environnement de transfert.</dd>
</dl>

<dl>
  <dt>Référentiel</dt>
  <dd>Un référentiel d'images est une collection d'images associées et étiquetées dans le registre. Les termes "référentiel" et "image" sont souvent utilisés pour exprimer la même notion mais un référentiel peut héberger plusieurs variantes étiquetées d'une même image.</dd>
</dl>

<dl>
  <dt>Image</dt>
  <dd>Il s'agit d'un système de fichiers et des paramètres d'exécution correspondants qui sont utilisés dans un module d'exécution de conteneur pour créer un conteneur. Le système de fichiers se compose d'une série de couches, combinées lors de l'exécution, qui sont créées à mesure que l'image est générée par des mises à jour successives. L'image ne conserve pas l'état lors de l'exécution du conteneur. </dd>
</dl>

<dl>
  <dt>Etiquette</dt>
  <dd>Une étiquette est l'identificateur d'une image dans le référentiel. Vous pouvez utiliser des étiquettes pour différencier plusieurs versions d'une même image de base dans un référentiel. Lorsque vous exécutez une commande Docker sans spécifier l'étiquette d'une image du référentiel, celle associée à l'étiquette <code>latest</code> (dernière) est utilisée par défaut.</dd>
</dl>

<dl>
  <dt>Dockerfile</dt>
  <dd>Un Dockerfile est un fichier texte contenant des instructions pour la construction d'une image Docker. Généralement, l'image est construite à partir d'une image de base contenant un système d'exploitation de base, comme Ubuntu. Vous pouvez modifier incrémentiellement l'image de base avec des instructions Dockerfile définissant l'environnement où doit s'exécuter l'application. Chaque modification de l'image de base décrit une nouvelle couche de l'image et vous pouvez apporter plusieurs modifications au même fichier Dockerfile. Les instructions dans un Dockerfile peuvent également référencer des artefacts de construction qui sont stockés séparément, tels qu'une application, sa configuration, et ses dépendances.</dd>
</dl>

Pour en savoir plus sur des termes spécifiques à Docker, consultez le [Glossaire Docker](https://docs.docker.com/glossary/).


### Planification d'espaces de nom
{: #registry_namespaces}

{{site.data.keyword.registrylong_notm}} fournit un registre d'images privé à service partagé qui est hébergé et géré par IBM. Vous pouvez stocker en sécurité et partager vos images Docker
dans ce registre en configurant un espace de nom du registre.
{:shortdesc}

Vous pouvez définir plusieurs espaces de nom, par exemple pour disposer de référentiels distincts pour votre environnement de production et votre
environnement de transfert. Si vous désirez utiliser le registre dans plusieurs régions {{site.data.keyword.Bluemix_notm}}, vous devez définir un espace de nom pour chaque région. Les noms d'espace de nom sont uniques dans chaque région. Vous pouvez utiliser le même nom d'espace de nom dans chaque région, sauf si quelqu'un d'autre l'a déjà utilisé pour définir un espace de nom dans la région concernée.

Si vous comptez utiliser seulement les images publiques fournies par IBM, vous n'avez pas besoin de définir un espace de nom.

Si vous ne savez pas si un espace de nom a déjà été défini pour votre compte, exécutez la commande `ibmcloud cr namespace-list` afin d'extraire les informations sur les espaces de nom existants. Si vous êtes un client existant d'{{site.data.keyword.containerlong_notm}}  qui utilise des [groupes de conteneurs uniques et évolutifs](../../containers/cs_classic.html),
vous disposez déjà d'un espace de nom. Vous pouvez en créer d'autres, mais vous ne pouvez exécuter la commande `cf ic namespace set` que pour un seul espace de nom à la fois.
{:tip}

Prenez en compte les règles suivantes lorsque vous choisissez un espace de nom :

-   Votre espace de nom doit être unique dans une région {{site.data.keyword.Bluemix_notm}}.
-   Votre espace de nom doit comporter de 4 à 30 caractères.
-   Votre espace de nom doit débuter par au moins une lettre ou un nombre.
-   Votre espace de nom ne doit comporter que des lettres en minuscules, des chiffres ou des traits de soulignement (_).

Ne placez pas d'informations personnelles dans vos noms d'espace de nom.
{:tip}

Après avoir configuré votre premier espace de nom, le plan de service {{site.data.keyword.registrylong_notm}} gratuit vous est affecté si vous n'avez pas encore [procédé à une mise à niveau de votre plan](#registry_plan_upgrade).

## Régions
{: #registry_regions}

Les registres {{site.data.keyword.registrylong_notm}} sont disponibles dans plusieurs régions.
{:shortdesc}

### Régions locales
{: #registry_regions_local}

Une région est une zone géographique dont l'accès s'effectue par un noeud final dédié. Des registres {{site.data.keyword.registrylong_notm}} sont disponibles dans les régions suivantes :

-   Sud de l'Asie Pacifique : `registry.au-syd.bluemix.net`
-   Europe centrale : `registry.eu-de.bluemix.net`
-   Sud du Royaume-Uni : `registry.eu-gb.bluemix.net`
-   Sud des Etats-Unis : `registry.ng.bluemix.net`

La portée de tous les artefacts de registre est celle du registre régional spécifique avec lequel vous travaillez actuellement. Ainsi, les espaces de nom, les images, les jetons, les paramètres de quota et de plan doivent tous être gérés séparément pour chaque registre régional.

Si vous désirez utiliser une région autre que votre région locale, vous pouvez cibler la région à laquelle accéder en exécutant la commande `ibmcloud cr region-set`. Vous pouvez exécuter la commande sans spécifier de paramètres afin d'obtenir la liste de toutes les régions disponibles ou spécifier la région comme paramètre.

Pour exécuter la commande avec des paramètres, remplacez _&lt;region&gt;_ par le nom de la région. Par exemple, `eu-central`.

```
ibmcloud cr region-set <region>
```
{: pre}

Pour cibler, par exemple, la région eu-central (Europe centrale), exécutez la commande suivante :

```
ibmcloud cr region-set eu-central
```
{: pre}

Après avoir ciblé une région différente, connectez-vous à nouveau au registre : `ibmcloud cr login`.

### Base de registre globale
{: #registry_regions_global}

Une base de registre globale est disponible, qui ne comporte aucune région dans son nom (`registry.bluemix.net`). Seules des images publiques fournies par IBM sont hébergées dans ce registre. Pour gérer vos propres images, par exemple pour définir des espaces de nom ou baliser et envoyer des images par commande push à un registre, utilisez un [registre régional local](#registry_regions_local).
{:shortdesc}

Vous pouvez cibler la base de registre globale en exécutant la commande `ibmcloud cr region-set`.

Ainsi, pour cibler la base de registre globale, exécutez la commande suivante :

```
ibmcloud cr region-set global
```
{: pre}

Pour plus d'informations sur la commande `ibmcloud cr region-set`, voir [Interface de ligne de commande {{site.data.keyword.registrylong_notm}}](registry_cli.html#bx_cr_region_set).

Une fois la base de registre globale ciblée, exécutez la commande `ibmcloud cr login` pour connecter votre démon Docker local à la base de registre globale afin de pouvoir extraire des images publiques fournies par {{site.data.keyword.IBM_notm}}.
