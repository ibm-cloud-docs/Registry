---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

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

# Interface de ligne de commande {{site.data.keyword.registrylong_notm}}
{: #containerregcli}

Vous pouvez utiliser l'interface de ligne de commande d'{{site.data.keyword.registrylong}}, fournie dans le plug-in d'interface de ligne de commande `container-registry`, afin de gérer votre registre et ses ressources pour votre compte {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

**Prérequis**

* Installez l'interface de ligne de commande [{{site.data.keyword.Bluemix_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli). Le préfixe pour l'exécution de commandes via l'interface CLI d'{{site.data.keyword.Bluemix_notm}} est `ibmcloud`.

* Avant d'exécuter les commandes de registre, connectez-vous à {{site.data.keyword.Bluemix_notm}} à l'aide de la commande `ibmcloud login` pour générer un jeton d'accès et authentifier votre session.

En ligne de commande, vous êtes averti lorsque les mises à jour de l'interface de ligne de commande `ibmcloud` et des plug-in d'interface de ligne de commande `container-registry` sont disponibles. Prenez soin de maintenir votre interface de ligne de commande à jour afin de pouvoir utiliser toutes les commandes et options disponibles.

Si vous souhaitez afficher la version en cours de votre plug-in d'interface de ligne de commande `container-registry`, exécutez `ibmcloud plugin list`.

Pour vous familiariser avec l'utilisation de l'interface de ligne de commande {{site.data.keyword.registrylong_notm}}, voir [Initiation à {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started).

Pour plus d'informations sur les rôles d'accès aux services et aux plateformes IAM qui sont requis pour certaines commandes, voir [Gestion des accès utilisateur à l'aide d'Identity and Access Management](/docs/services/Registry?topic=registry-iam#iam).

Ne placez pas d'informations personnelles dans vos images de conteneur, noms d'espace de nom, zones de description (par exemple, dans des jetons de registre), ou dans des données de configuration d'image (par exemple, dans des noms d'image ou des libellés d'image).
{:tip}

## `ibmcloud cr api`
{: #bx_cr_api}

Renvoie les informations sur le noeud final de l'API de registre face auquel les commandes sont exécutées.

```
ibmcloud cr api
```
{: codeblock}

**Prérequis**

Néant

## `ibmcloud cr build`
{: #bx_cr_build}

Génère une image Docker dans {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
<dt>`DIRECTORY`</dt>
<dd>Emplacement de votre contexte de génération, qui contient votre fichier Dockerfile et les fichiers prérequis. Si vous exécutez la commande alors que votre répertoire de travail est défini sur l'emplacement où est stocké votre contexte de génération, vous pensez remplacer `DIRECTORY` par un point (.).</dd>
<dt>`--no-cache`</dt>
<dd>(Facultatif) Lorsque ce paramètre est spécifié, les couches d'image mises en cache à partir de générations précédentes ne sont pas utilisées dans cette génération.</dd>
<dt>`--pull`</dt>
<dd>(Facultatif) Si ce paramètre est spécifié, les images de base sont extraites même si une image dotée d'une étiquette correspondante existe déjà sur l'hôte de génération.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Facultatif) Si ce paramètre est spécifié, la sortie de génération est supprimée sauf en cas d'erreur.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(Facultatif) Spécifiez un argument de génération supplémentaire au format `'KEY=VALUE'`. Vous avez la possibilité d'indiquer plusieurs arguments de génération en ajoutant ce paramètre plusieurs fois. La valeur de chaque argument de génération est disponible en tant que variable d'environnement quand vous spécifiez une ligne ARG qui correspond à la clé dans votre Dockerfile.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(Facultatif) Si vous utilisez les mêmes fichiers pour plusieurs générations, vous pouvez sélectionner un chemin vers un fichier Dockerfile différent. Indiquez l'emplacement du fichier Dockerfile par rapport au contexte de génération. Si vous ne l'indiquez pas, la valeur par défaut est `PATH/Dockerfile`, où PATH correspond à la racine du contexte de génération.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>Nom complet de l'image à générer, qui inclut l'URL et l'espace de nom de registre.</dd>
</dl>

**Exemple**

Générez une image Docker n'utilisant pas de cache de génération des précédentes générations, où la sortie de génération est supprimée, où la balise est *`us.icr.io/birds/bluebird:1`* et où le répertoire est votre répertoire de travail.

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Crée une exemption pour un problème de sécurité. Vous pouvez créer une exemption pour une question de sécurité qui s'applique à différentes portées. La portée peut être le compte, l'espace de nom, le référentiel ou la balise.

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Options de commande**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Pour définir votre compte comme portée, utilisez la valeur `"*"`. Pour définir un espace de nom, un référentiel ou une balise comme portée, entrez la valeur dans l'un des formats suivants : `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Type de problème de sécurité que vous voulez exempter. Pour connaître les types de problème valides, exécutez `ibmcloud cr exemption-types`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>ID de problème de sécurité que vous voulez exempter. Pour trouver un ID de problème, exécutez `ibmcloud cr va <image>`, où `<image>` est le nom de votre image, et utilisez la valeur pertinente de la colonne **Vulnerability ID** ou **Configuration Issue ID**.
</dd>
</dl>

**Exemples**

Créez une exemption CVE pour le CVE dont l'ID est `CVE-2018-17929` pour toutes les images du référentiel `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Créez une exemption CVE à l'échelle du compte pour le CVE dont l'ID est `CVE-2018-17929`.

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Créez une exemption d'erreur de configuration pour l'erreur `application_configuration:nginx.ssl_protocols` pour une image avec la balise `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

Répertorie vos exemptions pour les problèmes de sécurité.

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Options de commande**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(Facultatif) Répertorie uniquement les exemptions qui s'appliquent à cette portée. Pour définir un espace de nom, un référentiel ou une balise comme portée, entrez la valeur dans l'un des formats suivants : `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
</dl>

**Exemple**

Répertoriez toutes les exemptions pour les problèmes de sécurité qui s'appliquent aux images du référentiel *`birds/bluebird`*. La sortie inclut les exemptions à l'échelle du compte, les exemptions dont la portée est l'espace de nom *`birds`* et les exemptions dont la portée est le référentiel *`birds/bluebird`* mais pas certaines balises dans le référentiel *`birds/bluebird`*.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Supprime une exemption pour un problème de sécurité. Pour afficher vos exemptions existantes, exécutez la commande `ibmcloud cr exemption-list`.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Options de commande**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Pour définir votre compte comme portée, utilisez la valeur `"*"`. Pour définir un espace de nom, un référentiel ou une balise comme portée, entrez la valeur dans l'un des formats suivants : `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Type de problème de l'exemption pour le problème de sécurité que vous voulez supprimer. Pour trouver les types de problème pour vos exemptions, exécutez la commande `ibmcloud cr exemption-list`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>ID de l'exemption pour le problème de sécurité que vous voulez supprimer. Pour trouver les ID de problème pour vos exemptions, exécutez la commande `ibmcloud cr exemption-list`.
</dd>
</dl>

**Exemples**

Supprimez une exemption CVE pour le CVE dont l'ID est `CVE-2018-17929` pour toutes les images du référentiel `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Supprimez une exemption CVE à l'échelle du compte pour le CVE dont l'ID est `CVE-2018-17929`.

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Supprimez une exemption d'erreur de configuration pour l'erreur `application_configuration:nginx.ssl_protocols` pour une image avec la balise `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Répertorie les types de problèmes de sécurité que vous pouvez exempter.

```
ibmcloud cr exemption-types
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

Si vous utilisez l'authentification IAM, cette commande active l'autorisation à granularité fine. Pour plus d'informations, voir [Gestion des accès utilisateur à l'aide d'Identity and Access Management](/docs/services/Registry?topic=registry-iam#iam) et [Définition de règles de rôle d'accès utilisateur](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Affichez les détails d'une image spécifique.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go.

Pour plus d'informations, voir [Formatage et filtrage de la sortie de l'interface de ligne de commande pour les commandes {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing).

</dd>
<dt>`IMAGE`</dt>
<dd>Nom de l'image pour laquelle vous voulez obtenir un rapport. Vous pouvez inspecter plusieurs images en les répertoriant dans la commande, séparées les unes des autres par un espace.

<p>Pour trouver les noms de vos images, exécutez `ibmcloud cr image-list`. Associez le contenu des colonnes **Repository** et **Tag** pour créer le nom de l'image au format `repository:tag`. Si aucune étiquette n'est spécifiée dans le nom de l'image, l'image associée à l'étiquette `latest` est inspectée. </p>

</dd>
</dl>

**Exemple**

Affichez les détails sur les ports exposés pour l'image *`us.icr.io/birds/bluebird:1`*, en utilisant la directive de formatage *`"{{ .Config.ExposedPorts }}"`*.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Affiche toutes les images de votre compte {{site.data.keyword.Bluemix_notm}}.

Le nom de l'image est la combinaison du contenu des colonnes **Repository** et **Tag** au format `repository:tag`.
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
<dt>`--no-trunc`</dt>
<dd>(Facultatif) Permet de ne pas tronquer l'historique des images.</dd>
<dt>`--format FORMAT`</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go.

Pour plus d'informations, voir [Formatage et filtrage de la sortie de l'interface de ligne de commande pour les commandes {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing).

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Facultatif) Chaque image est répertoriée au format `repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Facultatif) Limite la sortie pour n'afficher que les images dans l'espace de nom spécifié ou dans l'espace de nom et le référentiel. </dd>
<dt>`--include-ibm`</dt>
<dd>(Facultatif) Inclut dans la sortie les images publiques fournies par {{site.data.keyword.IBM_notm}}. Sans cette option, seules les images privées sont répertoriées par défaut.</dd>
</dl>

**Exemple**

Affichez les images dans l'espace de nom *`birds`* au format `repository:tag`, sans tronquer l'historique des images.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Supprime une ou plusieurs images spécifiées de votre registre {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**

<dl>
<dt>`IMAGE`</dt>
<dd>Nom de l'image que vous souhaitez supprimer. Vous pouvez supprimer plusieurs images en même temps en les répertoriant dans la commande, séparées les unes des autres par un espace. `IMAGE` doit être au format `repository:tag`, par exemple : `us.icr.io/namespace/image:latest`

<p>Pour trouver les noms de vos images, exécutez `ibmcloud cr image-list`. Associez le contenu des colonnes **Repository** et **Tag** pour créer le nom de l'image au format `repository:tag`. Si aucune étiquette n'est spécifiée dans le nom de l'image, l'image associée à l'étiquette `latest` est supprimée par défaut.</p>

</dd>
</dl>

**Exemple**
Supprimez l'image `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

Crée une nouvelle image, TARGET_IMAGE, qui fait référence à une image source, SOURCE_IMAGE, dans {{site.data.keyword.registrylong_notm}}. Les images source et cible doivent se trouver dans la même région.

Pour trouver les noms de vos images, exécutez `ibmcloud cr image-list`. Associez le contenu des colonnes **Repository** et **Tag** pour créer le nom de l'image au format `repository:tag`.
{: tip}

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>Nom de l'image source. `SOURCE_IMAGE` doit être au format `repository:tag`, par exemple : `us.icr.io/namespace/image:latest`

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>Nom de l'image cible. `TARGET_IMAGE` doit être au format `repository:tag`, par exemple : `us.icr.io/namespace/image:latest`

</dd>
</dl>

**Exemples**

Ajoutez une autre référence d'étiquette, `latest`, à l'image `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

Copiez l'image `us.icr.io/birds/bluebird:peck` dans un autre référentiel du même espace de nom `birds/pigeon`.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

Copiez l'image `us.icr.io/birds/bluebird:peck` dans un autre espace de nom `animals` auquel vous avez accès.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

Affiche le nom et le compte du registre auquel vous êtes connecté.

```
ibmcloud cr info
```
{: codeblock}

**Prérequis**

Néant

## `ibmcloud cr login`
{: #bx_cr_login}

Cette commande exécute la commande `docker login` sur le registre. La commande `docker login` est requise pour pouvoir exécuter les commandes `docker push` ou `docker pull` pour le registre. Cette commande n'est pas requise pour exécuter d'autres commandes `ibmcloud cr`. Si Docker n'est pas installé, cette commande renvoie un message d'erreur.

```
ibmcloud cr login
```
{: codeblock}

**Prérequis**

Néant

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Choisit un nom pour votre espace de nom et l'ajoute à votre compte {{site.data.keyword.Bluemix_notm}}.

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Espace de nom à ajouter. Il doit être unique sur tous les comptes {{site.data.keyword.Bluemix_notm}} d'une même région. Les espaces de nom doivent comporter entre 4 et 30 caractères et contenir uniquement des lettres minuscules, des chiffres, des tirets et des traits de soulignement. Les espaces de nom doivent commencer et se terminer par une lettre ou un chiffre.
  
<p>  
<strong>Astuce</strong> ne placez pas d'informations personnelles dans vos noms d'espace de nom.
</p>
  
</dd>
</dl>

**Exemple**

Créez un espace de nom avec le nom *`birds`*.

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Affiche tous les espaces de nom détenus par votre compte {{site.data.keyword.Bluemix_notm}}.

```
ibmcloud cr namespace-list
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Retire un espace de nom de votre compte {{site.data.keyword.Bluemix_notm}}. Les images dans cet espace de nom sont supprimées lorsque l'espace de nom est retiré.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Espace de nom que vous désirez supprimer.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Facultatif) Force l'exécution de la commande sans invites utilisateur.</dd>
</dl>

**Exemple**

Retirez l'espace de nom *`birds`*.

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

Affiche votre plan de tarification.

```
ibmcloud cr plan
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Effectue une mise à niveau vers le plan standard.

Pour plus d'information sur les plans, voir [Plans de registre](/docs/services/Registry?topic=registry-registry_overview#registry_plans).

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Options de commande**
<dl>
<dt>`PLAN`</dt>
<dd>(Facultatif) Nom du plan de tarification vers lequel vous souhaitez effectuer une mise à niveau. Si `PLAN` n'est pas spécifié, la valeur par défaut est `standard`.</dd>
</dl>

**Exemple**

Effectuez une mise à niveau vers le plan de tarification standard.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

Importe le logiciel {{site.data.keyword.IBM_notm}} qui est téléchargé depuis [IBM Passport Advantage Online pour les clients ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/passportadvantage/pao_customer.html) et conditionné pour une utilisation avec Helm dans votre espace de nom {{site.data.keyword.registrylong_notm}}.

Les images de conteneur sont envoyées par commande push à votre espace de nom {{site.data.keyword.registryshort_notm}} privé. Les chartes Helm sont écrites dans un répertoire `ppa-import` créé dans le répertoire à partir duquel vous exécutez la commande. Vous avez la possibilité d'utiliser le [projet open source Chart Museum ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) pour héberger des chartes Helm.

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>Chemin d'accès au fichier compressé téléchargé depuis IBM Passport Advantage.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>Un de vos espaces de nom. Les images de conteneur du fichier compressé sont envoyées par commande push vers cet espace de nom. Pour répertorier les espaces de nom, exécutez `ibmcloud cr namespace-list`.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Facultatif) Votre ID ressource unique [Chart Museum ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(Facultatif) Votre nom d'utilisateur [Chart Museum ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(Facultatif) Votre mot de passe [Chart Museum ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
</dl>

**Exemple**

Importez le logiciel IBM et conditionnez-le pour une utilisation avec Helm dans votre espace de nom {{site.data.keyword.registrylong_notm}} *`birds`*, où le chemin d'accès au fichier compressé est *`downloads/compressed_file.tgz`*.

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

Affiche vos quotas actuels de trafic et de stockage, ainsi que les informations d'utilisation de ces quotas.

```
ibmcloud cr quota
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Modifie le quota spécifié.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Options de commande**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(Facultatif) Remplace votre quota de trafic par la valeur spécifiée en mégaoctets. L'opération échoue si vous n'êtes pas habilité à définir le trafic ou si vous définissez une valeur au-delà de votre plan de tarification.</dd>
<dt>`--storage STORAGE`</dt>
<dd>(Facultatif) Remplace votre quota de stockage par la valeur spécifiée en mégaoctets. L'opération échoue si vous n'êtes pas habilité à définir les quotas de stockage ou si vous définissez une valeur au-delà de votre plan de tarification.</dd>
</dl>

**Exemple**

Définissez votre limite de quota pour le trafic d'extraction à *7000* mégaoctets pour le stockage à *600* mégaoctets.

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

Affiche les régions cible et le registre.

```
ibmcloud cr region
```
{: codeblock}

**Prérequis**

Néant

Pour plus d'informations, voir
[Régions](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Définit une région cible pour les commandes {{site.data.keyword.registrylong_notm}}. Pour répertorier les régions disponibles, exécutez la commande sans paramètres.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**Prérequis**

Néant

**Options de commande**
<dl>
<dt>`REGION`</dt>
<dd>(Facultatif) Le nom de votre région cible, par exemple, `us-south`.

Pour plus d'informations, voir
[Régions](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

</dd>
</dl>

**Exemple**

Ciblez la région Sud des Etats-Unis.

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-add`
{: #bx_cr_token_add}

Ajoute un jeton que vous pouvez utiliser pour contrôler l'accès à un registre.

```
ibmcloud cr token-add [--description DESCRIPTION] [--quiet | -q] [--non-expiring] [--readwrite]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles de gestion de plateforme](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Options de commande**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>(Facultatif) Permet de spécifier la description du jeton qui s'affiche lorsque vous exécutez `ibmcloud cr token-list`. Si votre jeton est créé automatiquement par {{site.data.keyword.containerlong_notm}}, la description est définie sur votre nom de cluster Kubernetes. Dans ce cas, le jeton est retiré automatiquement lorsque votre cluster est retiré.
  
<p> 
  <strong>Astuce</strong> : ne placez pas d'informations personnelles dans votre description de jeton.
</p>

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Facultatif) Affiche le jeton uniquement, sans aucun autre texte.</dd>
<dt>`--non-expiring`</dt>
<dd>(Facultatif) Crée un jeton dont l'accès n'expire jamais. Si ce paramètre n'est pas défini, l'accès à l'aide d'un jeton expire au bout de 24 heures par défaut.</dd>
<dt>`--readwrite`</dt>
<dd>(Facultatif) Crée un jeton qui accorde l'accès en lecture et en écriture. Sans cette option, l'accès est en lecture seule par défaut.</dd>
</dl>

**Exemple**

Ajoutez un jeton avec la description *Token for my account* qui n'expire pas et qui dispose de droits d'accès en lecture/écriture.

```
ibmcloud cr token-add --description "Token for my account" --non-expiring --readwrite
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

Extrait le jeton spécifié du registre.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles de gestion de plateforme](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Options de commande**
<dl>
<dt>`TOKEN`</dt>
<dd>Identificateur unique du jeton à extraire. Pour répertorier vos jetons, exécutez `ibmcloud cr token-list`.</dd>
</dl>

**Exemple**

Extrayez le jeton *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

Affiche tous les jetons qui existent pour votre compte {{site.data.keyword.Bluemix_notm}}.

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles de gestion de plateforme](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Options de commande**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go.

Pour plus d'informations, voir [Formatage et filtrage de la sortie de l'interface de ligne de commande pour les commandes {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing).

</dd>
</dl>

**Exemple**

Affichez tous les jetons accessibles en lecture seule, en utilisant la directive de formatage *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`*.

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

Cet exemple produit une sortie au format suivant :

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

Supprime un ou plusieurs des jetons de registre spécifiés.

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles de gestion de plateforme](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Options de commande**
<dl>
<dt>`TOKEN`</dt>
<dd>TOKEN peut correspondre au jeton proprement dit ou à l'identificateur unique du jeton, comme indiqué dans `ibmcloud cr token-list`. Vous pouvez spécifier plusieurs jetons en les séparant par un espace.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Facultatif) Force l'exécution de la commande sans invites utilisateur.</dd>
</dl>

**Exemple**

Retirez le jeton *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

Affiche un rapport d'évaluation des vulnérabilités pour vos images.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Prérequis**

Pour en savoir plus sur les droits requis, voir [Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Options de commande**
<dl>
<dt>`IMAGE`</dt>
<dd>Nom de l'image pour laquelle vous voulez obtenir un rapport. Le rapport vous signale si l'image comporte des vulnérabilités de package connues. Vous pouvez demander des rapports pour plusieurs images en même temps en les répertoriant dans la commande, séparées les unes des autres par un espace.

<p>Pour trouver les noms de vos images, exécutez `ibmcloud cr image-list`. Associez le contenu des colonnes **Repository** et **Tag** pour créer le nom de l'image au format `repository:tag`. Si aucune étiquette n'est spécifiée dans le nom de l'image, le rapport évalue l'image associée à l'étiquette `latest`.</p>

<p>Les systèmes d'exploitation suivants sont pris en charge :

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

Pour plus d'informations, voir la rubrique relative à la [gestion de la sécurité des images avec l'assistant de détection des vulnérabilités](/docs/services/va?topic=va-va_index).

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Facultatif) La sortie de la commande affiche des informations supplémentaires sur les correctifs pour les packages vulnérables.</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Facultatif) La sortie de la commande est restreinte pour n'afficher que les vulnérabilités.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Facultatif) La sortie de la commande est restreinte pour n'afficher que les problèmes de configuration.</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(Facultatif) La sortie de la commande est retournée dans le format choisi. Le format par défaut est `text`. Les formats suivants sont pris en charge :

<ul>
<li>`texte`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**Exemples**

Affiche un rapport d'évaluation des vulnérabilités standard pour votre image.

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

Affichez un rapport d'évaluation des vulnérabilités pour votre image `us.icr.io/birds/bluebird:1` au format JSON, avec uniquement les vulnérabilités.

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
