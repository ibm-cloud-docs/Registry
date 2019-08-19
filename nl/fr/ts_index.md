---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, troubleshooting, support, help, errors, error messages, failure, fails, lost keys, firewall, Docker manifest errors,

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Traitement des incidents
{: #ts_index}

Vous trouverez ici les réponses aux questions fréquentes liées au traitement des incidents concernant l'utilisation d'{{site.data.keyword.registrylong}}.
{:shortdesc}

## Aide et support pour {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Si vous rencontrez des problèmes ou des questions lors de l'utilisation d'{{site.data.keyword.registrylong_notm}}, vous pouvez rechercher des informations ou poser des questions via un forum. Vous pouvez également ouvrir un ticket de demande de service {{site.data.keyword.IBM_notm}}.

Lorsque vous posez une question sur un forum, marquez votre question à l'aide d'une étiquette pour qu'elle soit vue par l'équipe de développement d'{{site.data.keyword.registrylong_notm}}.

- Si vous avez une question technique sur le développement ou le déploiement d'une application avec {{site.data.keyword.registrylong_notm}}, publiez-la sur [Stack Overflow ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://stackoverflow.com/search?q=+ibm-cloud+container-registry) en y ajoutant les balises `ibm-cloud` et `container-registry`.
- Pour toute question sur le service et les instructions de mise en route, utilisez le forum [IBM Developer Answers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/answers/topics/container-registry.html). Ajoutez les balises `ibm-cloud` et `container-registry`.

Voir [Utilisation du centre de support](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) pour plus de détails sur l'utilisation des forums.

Pour obtenir des informations sur l'ouverture d'un ticket de demande de service {{site.data.keyword.IBM_notm}} ou sur les niveaux de support et les degrés de gravité des tickets, voir [Comment obtenir l'aide dont j'ai besoin ?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).

## La connexion à {{site.data.keyword.registrylong_notm}} échoue
{: #ts_login}

Vous ne parvenez pas à vous connecter à {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
La commande `ibmcloud cr login` échoue.

{: tsCauses}
Les alternatives suivantes sont des causes possibles :

- Le plug-in d'interface de ligne de commande `container-registry` est périmé et doit être mis à jour.
- Docker n'est pas installé ou n'est pas en cours d'exécution sur votre ordinateur local.
- Vos données d'identification {{site.data.keyword.cloud_notm}} ont expiré.

{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

- Effectuez une mise à niveau vers la version la plus récente du plug-in d'interface de ligne de commande `container-registry`. Voir [Mise à jour du plug-in d'interface de ligne de commande `container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).
- Assurez-vous que Docker est installé sur votre ordinateur. S'il est déjà installé, redémarrez le démon Docker.
- Exécutez à nouveau la commande `ibmcloud login` pour actualiser vos données d'identification de connexion à {{site.data.keyword.cloud_notm}}.

## L'exécution d'une commande pour {{site.data.keyword.registrylong_notm}} échoue avec `ECHEC Vous n'êtes pas connecté à IBM Cloud.`
{: #ts_login_cloud}

Vous ne pouvez pas exécuter de commandes dans {{site.data.keyword.registrylong_notm}}, même si vous êtes connecté à {{site.data.keyword.cloud_notm}}.

{: tsSymptoms}
Toutes les commandes `ibmcloud cr` échouent.

{: tsCauses}
Le plug-in d'interface de ligne de commande `container-registry` est périmé et doit être mis à jour.

{: tsResolve}
Effectuez une mise à niveau vers la version la plus récente du plug-in d'interface de ligne de commande `container-registry`. Voir [Mise à jour du plug-in d'interface de ligne de commande `container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).

## Les commandes {{site.data.keyword.registrylong_notm}} échouent avec le message `'cr' is not a registered command. See 'ibmcloud help'. `
{: #ts_login_error}

Vous ne pouvez pas exécuter une commande `ibmcloud cr` car `cr` n'est pas une commande `ibmcloud` enregistrée.

{: tsSymptoms}
Vous recevez un message d'erreur similaire à l'un des messages d'erreur suivants :

```
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

{: tsCauses}
Le plug-in d'interface de ligne de commande `container-registry` n'est pas installé.

{: tsResolve}
Installez le plug-in d'interface de ligne de commande `container-registry`. Voir [Installation du plug-in d'interface de ligne de commande`container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## La commande `ibmcloud cr build` échoue.
{: #ts_build_fails}

{: tsSymptoms}
La commande build échoue.

{: tsCauses}
Il se peut que le serveur soit en panne ou que d'autres problèmes se soient produits avec votre fichier Dockerfile.

{: tsResolve}
Pour trouver la cause, exécutez `docker build` localement avec les options [`docker build` appropriées ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/engine/reference/commandline/build/):

```
docker build --no-cache .
```
{:  pre}

- Si la génération locale ne fonctionne pas, vérifiez votre fichier Dockerfile.
- Si la génération locale fonctionne, [contactez le support {{site.data.keyword.cloud_notm}}](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).

## Echec de la configuration d'un espace de nom
{: #ts_problem}

{: tsSymptoms}
Lorsque vous exécutez `ibmcloud cr namespace-add`, vous ne parvenez pas à définir la valeur que vous avez entrée en tant qu'espace de nom.

{: tsCauses}
Les alternatives suivantes sont des causes possibles :

- Vous avez entré une valeur d'espace de nom qui est déjà utilisée par une autre organisation {{site.data.keyword.cloud_notm}}.
- Un espace de nom a récemment été supprimé et vous réutilisez son nom. Si l'espace de nom supprimé contenait de nombreuses ressources, la suppression n'a peut-être pas été entièrement traitée par {{site.data.keyword.registrylong_notm}}.
- Vous avez utilisé des caractères non valides dans la valeur de l'espace de nom.

{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

- Suivez les instructions contenues dans le message d'erreur renvoyé.
- Vérifiez que vous avez saisi un espace de nom valide :
  - Votre espace de nom doit être unique sur tous les comptes {{site.data.keyword.cloud_notm}} d'une même région.
  - Votre espace de nom doit comporter de 4 à 30 caractères.
  - Votre espace de nom doit commencer et se terminer par une lettre ou un chiffre.
  - Votre espace de nom ne doit comporter que des lettres en minuscules, des chiffres, des tirets (-) et des traits de soulignement (_).
- Choisissez une autre valeur pour votre espace de nom.
- Si vous recréez un espace de nom qui a été supprimé, et que ce dernier contenait de nombreuses images, faites une nouvelle tentative ultérieurement.

## Echec de l'envoi par commande push ou de l'extraction (pull) d'une image Docker
{: #ts_pushpull}

{: tsSymptoms}
Lorsque vous exécutez des commandes pour transférer ou extraire des images Docker, vous rencontrez un message d'erreur. Le message d'erreur varie selon la cause première. Les messages d'erreur potentiels sont les suivants :

```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan
```
{: screen}

```
You have exceeded your pull traffic quota for the current month.
Review your pull traffic quota and pricing plan
```
{: screen}

```
unauthorized: authentication required
```
{: screen}

```
denied: requested access to the resource is denied
```
{: screen}

{: tsCauses}
Les alternatives suivantes sont des causes possibles :

- Docker n'est pas installé.
- Le client Docker n'est pas connecté à {{site.data.keyword.registrylong_notm}}.
- Il se peut que votre jeton d'accès {{site.data.keyword.cloud_notm}} ait expiré.
- Vous avez dépassé la limite de quota pour le stockage ou le trafic d'extraction (pull) défini pour votre compte {{site.data.keyword.cloud_notm}}.

{: tsResolve}
Vous pouvez corriger ce problème en procédant ainsi :

- [Assurez-vous que Docker est installé sur votre ordinateur](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- Vérifiez votre chemin d'installation Docker.
- Connectez-vous à {{site.data.keyword.cloud_notm}} en exécutant `ibmcloud login`. Connectez-vous ensuite à l'interface de ligne de commande d'{{site.data.keyword.registrylong_notm}} en exécutant `ibmcloud cr login`.
- [Examinez les limites de quota et l'utilisation du stockage et de l'extraction des images Docker dans {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_quota#registry_quota_get).

## Impossible d'extraire l'image la plus récente avec l'étiquette `latest`
{: #ts_docker_latest}

{: tsSymptoms}
Vous tentez d'exécuter la commande `docker pull`, mais celle-ci renvoie une version de l'image qui n'est pas la version la plus récente générée.

{: tsCauses}
L'étiquette `latest` est appliquée par défaut pour référencer une image lorsque vous exécutez des commandes Docker sans spécifier de valeur pour l'étiquette. L'étiquette `latest` est appliquée à la commande `docker build` ou `docker tag` la plus récente exécutée sans qu'une étiquette n'ait été spécifiée explicitement. Il est donc possible d'exécuter les commandes `docker` dans le désordre ou de définir des balises de manière explicite sur certaines images, la balise `latest` désignant une génération qui n'est pas la plus récente.

{: tsResolve}
En général, il est préférable de définir explicitement chaque fois une balise séquentielle différente pour vos images et de ne pas vous en remettre à la balise `latest`.

## Impossible d'ajouter d'autres images IBM au registre
{: #ts_ppa}

{: tsSymptoms}
Lorsque vous tentez d'importer du contenu que vous avez utilisé dans d'autres produits IBM tels que {{site.data.keyword.cloud_notm}} Private, vous ne parvenez pas à stocker vos images et autres logiciels sous licence depuis [IBM Passport Advantage ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/passportadvantage/index.html) dans le registre.

{: tsCauses}
Les progiciels tels que les images et les chartes Helm provenant d'IBM Passport Advantage doivent être importés dans le registre à l'aide de la commande `ibmcloud cr ppa-archive-load`.

{: tsResolve}
Avant de commencer à importer le produit d'IBM Passport Advantage, exécutez les tâches suivantes :

1. Connectez-vous à {{site.data.keyword.cloud_notm}} en exécutant `ibmcloud login [--sso]`.
2. Connectez-vous à {{site.data.keyword.registrylong_notm}} en exécutant `ibmcloud cr login`.
3. [Ciblez l'interface de ligne de commande `kubectl`](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) sur votre cluster.
4. Si vous n'avez pas déjà configuré Helm dans votre cluster, [configurez Helm dans votre cluster maintenant](/docs/containers?topic=containers-helm#helm).
5. Si vous souhaitez partager les chartes au sein de votre organisation, vous pouvez installer le [projet open source Chart Museum ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/helm/charts/tree/master/stable/chartmuseum). Pour obtenir des instructions, voir cette [recette developerWorks ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/).

### Importation de produits IBM Passport Advantage à utiliser dans {{site.data.keyword.cloud_notm}}
{: #ts_ppa_import}

1. Procurez-vous le fichier compressé à importer depuis [IBM Passport Advantage![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/passportadvantage/index.html).

2. Ciblez la région à utiliser. Si vous ne connaissez pas le nom de la région, exécutez la commande sans la région, puis sélectionnez-en une.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

3. Importez le fichier archive compressé. Indiquez le chemin d'accès au fichier compressé ainsi que l'espace de nom de registre auquel envoyer les images par commande push.

   ```
   ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
   ```
   {: pre}

   Cette commande développe le fichier compressé, charge les images contenues dans votre client Docker local puis envoie par commande push les images à l'espace de nom de votre registre.

   Si vous souhaitez télécharger des chartes Helm depuis l'archive IBM Passport Advantage dans un référentiel de type chartmuseum, incluez les options suivantes dans la commande : `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
   {: tip}

   Le message suivant est un exemple de sortie de la commande :

   ```
   user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
   Found 1 image(s) and 1 chart(s) to import.
   Importing 'iib-prod:10.0.0.10' and pushing it to 'us.icr.io/mynamespace/iib-prod:10.0.0.10'...
   Loaded image: iib-prod:10.0.0.10
   The push refers to repository [us.icr.io/mynamespace/iib-prod]
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

4. Si le fichier compressé contient des chartes Helm, celles-ci sont placées dans un répertoire d'archivage appelé `ppa-import`, qui est créé dans votre répertoire de travail en cours. Ouvrez le répertoire pour obtenir le nom de la charge Helm, `<helm_chart>`, puis vérifiez-en les valeurs.

   ```
   helm inspect values ppa-import/charts/<helm_chart>.tgz
   ```
   {: pre}

   Si vous avez téléchargé des chartes dans un référentiel de type chartmuseum à l'étape précédente, vous pouvez utiliser `helm inspect` pour inspecter la charte dans le référentiel de type chartmuseum.
   {: tip}

5. Configurez la charte Helm, `<helm_chart>`, en fonction des valeurs générées par la commande `helm inspect values`.

6. Déployez la charte Helm, `<helm_chart>`, en utilisant la commande `helm install`. Vous pouvez remplacer les valeurs de la charte selon les besoins, en utilisant l'option `--set`.

   ```
   helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
   ```
   {: pre}

## J'ai utilisé la commande `ibmcloud cr image-rm` pour supprimer une image et toutes les étiquettes qui font référence à cette image ont également été supprimées
{: #ts_image-rm}

{: tsSymptoms}
Vous avez supprimé une image en utilisant la commande `ibmcloud cr image-rm` et toutes les étiquettes qui se trouvent dans le même référentiel et qui font référence à l'image ont également été supprimées.

{: tsCauses}
Lorsqu'un référentiel contient plusieurs étiquettes pour le même historique des images, la commande [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) supprime l'image sous-jacente ainsi que toutes ses étiquettes. Si la même image existe dans un autre référentiel ou espace de nom, cette copie de l'image n'est pas supprimée.

{: tsResolve}
Si vous voulez supprimer une étiquette d'une image mais conserver l'image sous-jacente ainsi que toutes les autres étiquettes, utilisez la commande [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag). Pour plus d'informations, voir [Suppression d'étiquettes d'images dans votre référentiel {{site.data.keyword.cloud_notm}} privé](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag) et[Suppression d'images de votre référentiel {{site.data.keyword.cloud_notm}} privé](/docs/services/Registry?topic=registry-registry_images_#registry_images_remove).

## L'accès au registre avec un pare-feu personnalisé échoue
{: #ts_firewall}

{: tsSymptoms}
Vous configurez dans votre environnement de développement un pare-feu supplémentaire avec des paramètres personnalisés pour le trafic réseau entrant et sortant. Lorsque vous tentez d'accéder à {{site.data.keyword.registrylong_notm}}, la connexion échoue.

{: tsCauses}
Votre pare-feu personnalisé requiert que certains groupes réseau soient ouverts au trafic réseau entrant et sortant pour permettre la communication vers et depuis le registre.

{: tsResolve}
Laissez votre cluster accéder aux ressources d'infrastructure et à des services depuis l'arrière d'un pare-feu. Reportez-vous à la rubrique [Permettre au cluster d'accéder aux ressources d'infrastructure et à d'autres services](/docs/containers?topic=containers-firewall#firewall_outbound).

Pour la connectivité ENTRANTE vers votre ordinateur, autorisez le trafic réseau entrant depuis les groupes réseau source vers l'adresse IP publique de destination de votre ordinateur.

Pour la connectivité SORTANTE depuis votre ordinateur, utilisez les mêmes groupes réseau et autorisez le trafic réseau sortant depuis l'adresse IP publique source de votre ordinateur vers les groupes réseau.

## Récupération de clés perdues ou compromises
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
Alors que vous utilisez du [contenu sécurisé](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent), vous ne pouvez plus gérer des images sécurisées parce que vos clés de signature sont perdues ou compromises.

{: tsCauses}
Votre clé de référentiel ou racine (root) est perdue ou compromise.

{: tsResolve}
Les options dont vous disposez pour récupérer des clés perdues ou compromises dépendent du type de clé : de référentiel ou racine :

- Pour des [clés de référentiel](#trustedcontent_lostrepokey), vous pouvez générer un nouvel ensemble de clés de signature pour le référentiel.
- Pour des [clés racine](#trustedcontent_lostrootkey), vous pouvez demander la suppression du référentiel et la création d'un nouveau référentiel.

### Clés de référentiel
{: #trustedcontent_lostrepokey}

Si votre clé de référentiel est perdue ou compromise, générez un nouvel ensemble de clés de signature pour votre référentiel.
{:shortdesc}

Le seul rôle de signature que vous pouvez faire pivoter est `targets`, c'est-à-dire l'administrateur du référentiel. Si d'autres rôles sont affectés, générez de nouvelles clés pour ces rôles, retirez les anciennes, puis ajoutez les nouvelles en tant que signataires.
{:tip}

Avant de commencer, récupérez la phrase passe de clé racine que vous avez créée la première fois que vous avez [envoyé par commande push une image signée](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_push).

1. Installez la version d'interface de ligne de commande du [projet Notary ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli).

2. [Configurez votre environnement de contenu sécurisé](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_setup).

3. Créez une clé d'API IAM :

   ```
   ibmcloud iam api-key-create notary-auth --file notary-auth
   ```
   {: pre}

4. Définissez le paramètre NOTARY_AUTH :

   ```
   export NOTARY_AUTH="iamapikey:$(jq -r .apikey notary-auth)"
   ```
   {: pre}

5. Faites pivoter ces clés afin que le contenu signé à l'aide de ces clés ne soit plus sécurisé. Utilisez la variable du serveur d'accréditation que vous avez définie à l'étape 2 et remplacez `<image>` par l'image dont la clé de référentiel est affectée.

   ```
   notary -s "$DOCKER_CONTENT_TRUST_SERVER" -d ~/.docker/trust key rotate <image> targets
   ```
   {: pre}

6. Si vous y êtes invité, entrez la phrase passe de clé racine. Entrez ensuite une nouvelle phrase passe pour la nouvelle clé de référentiel lorsque vous y êtes invité.

7. [Envoyez par commande push une image signée](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_push) qui utilise les nouvelles clés de signature.

8.  (Facultatif) Lorsque vous avez terminé, si vous souhaitez révoquer votre clé d'API, exécutez la commande suivante :

    ```
    ibmcloud iam api-key-delete notary-auth
    ```
    {:pre}

### Clés racine (root)
{: #trustedcontent_lostrootkey}

Si votre clé racine est perdue ou compromise, vous ne pouvez pas mettre à jour des référentiels de contenu sécurisé qui utilisaient cette clé racine.
{:shortdesc}

Vous pouvez [supprimer les espaces de nom](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_remove) dont les référentiels utilisent la clé racine affectée, ce qui supprimera vos images et données sécurisées.

Si l'espace de nom contient des référentiels dont les clés racine ne sont pas affectées, comme un espace de nom pour des images de production, vous souhaiterez peut-être ne supprimer que les données sécurisées associées à la clé racine affectée. Ouvrez un ticket de demande de service.

1. [Contactez le support {{site.data.keyword.cloud_notm}}](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support). Incluez une brève description de votre problème, l'ID compte, ainsi que la liste des espaces de nom contenant les référentiels d'images avec les clés racine affectées.

2. Une fois qu'{{site.data.keyword.cloud_notm}} a traité le problème, supprimez le référentiel Docker Content Trust sur votre ordinateur local.

   - Répertoire Linux et Mac : `~/.docker/trust/private` et `~/.docker/trust/tuf`

   - Répertoire Windows : `%HOMEPATH%\.docker\trust\private` et `%HOMEPATH%\.docker\trust\tuf`

   Etant donné que la clé racine est affectée, cette étape supprime toutes les clés de signature, y compris pour les autres serveurs d'accréditation.
   {:tip}

3. Si vous utilisez [{{site.data.keyword.cloud_notm}} Image Enforcement](/docs/services/Registry?topic=registry-security_enforce#security_enforce) dans votre cluster {{site.data.keyword.containershort_notm}}, redémarrez chaque pod de mise en application d'image. Pour déclencher Kubernetes afin d'effectuer automatiquement un redémarrage séquentiel des pods, vous pouvez changer certaines métadonnées sur le pod. Par exemple, [ciblez votre interface de ligne de commande Kubernetes sur votre cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) et modifiez le déploiement.

   ```
   kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
   ```
   {: pre}

4. Générez des référentiels de contenu sécurisé.

    - Si vous souhaitez créer un nouveau contenu sécurisé, [envoyez par commande push de nouvelles images signées](/docs/services/Registry?topic=registry-registry_trustedcontent#trustedcontent_push).

    - Si vous ne voulez pas changer le contenu sécurisé précédent, ajoutez une signature aux images les plus récentes du registre.

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

## Les pods ne redémarrent pas si tous vos agents se sont arrêtés
{: #ts_pods}

{: tsSymptoms}
Les pods ne redémarrent pas si tous vos agents de cluster se sont arrêtés. Container Image Security Enforcement est déployé. Les agents de cluster sont sains mais rien n'est planifié.

{: tsCauses}
Par défaut, Container Image Security Enforcement ajoute un webhook d'admission pour la fermeture en cas d'échec (fail closed). Si tous les pods Container Image Security Enforcement sont arrêtés, ils ne sont pas disponibles pour approuver leur propre reprise.

{: tsResolve}
Pour reprendre le cluster alors qu'il se trouve dans cet état, vous devez changer la configuration de webhook pour ignorer l'échec (fail open) au lieu de procéder à la fermeture en cas d'échec (fail closed).

Vous devez disposer de privilèges de contrôle d'accès à base de rôles suffisants pour pouvoir utiliser les instructions suivantes :

- `GET`
- `PATCH`

sur les ressources suivantes :

- `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
- `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration`

Pour plus d'informations sur RBAC, voir [Autorisation des utilisateurs avec des droits RBAC Kubernetes personnalisés](/docs/containers?topic=containers-users#rbac) et [Kubernetes - Using RBAC Authorization ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

Procédez comme suit pour changer la configuration de webhook afin d'ignorer l'échec (fail open) au lieu de procéder à la fermeture en cas d'échec (fail closed) ; puis, lorsqu'au moins un pod Container Image Security Enforcement est en cours d'exécution, restaurez la configuration de webhook pour une fermeture en cas d'échec :

1. Mettez à jour `MutatingWebhookConfiguration` avec la commande suivante :

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Pour `failurePolicy`, définissez `Ignore`, puis sauvegardez et fermez.

2. Mettez à jour `ValidatingWebhookConfiguration` avec la commande suivante :

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Pour `failurePolicy`, définissez `Ignore`, puis sauvegardez et fermez.

3. Attendez que des pods Container Image Security Enforcement démarrent. Vous pouvez vérifier que les pods ont démarré avec la commande suivante jusqu'à ce que la colonne **STATUS** affiche `Running` pour une colonne au moins :

   ```
   kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
   ```
   {: pre}

4. Lorsqu'un pod Container Image Security Enforcement au moins est en cours d'exécution, mettez à jour `MutatingWebhookConfiguration` avec la commande suivante :

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Pour `failurePolicy`, définissez `Fail`, puis sauvegardez et fermez.

5. Mettez à jour `ValidatingWebhookConfiguration` avec la commande suivante :

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Pour `failurePolicy`, définissez `Fail`, puis sauvegardez et fermez.

## Erreur de manifeste : `The manifest type for this image is not supported for tagging.`
{: #ts_manifest_error_type}

{: tsSymptoms}
Vous avez essayé d'étiqueter votre image, mais vous recevez le message d'erreur suivant : `The manifest type for this image is not supported for tagging.`.

{: tsCauses}
Le type de manifeste n'est pas pris en charge.

{: tsResolve}
Pour résoudre le problème, procédez comme suit :

1. Procédez à l'extraction de l'image que vous avez essayé d'étiqueter en exécutant la commande suivante, où `<source_image>` correspond au nom de votre image source.

   ```
   docker pull <source_image>
   ```
   {: pre}

2. Etiquetez votre copie locale de l'image que vous avez extraite à l'étape précédente en exécutant la commande suivante, où `<target_image>` correspond au nom de votre nouvelle image :

   ```
   docker tag <source_image> <target_image>
   ```
   {: pre}

3. Envoyez l'image que vous avez étiquetée à l'étape précédente en exécutant la commande suivante :

   ```
   docker push <target_image>
   ```
   {: pre}

## Erreur de manifeste : `The manifest version for this image is not supported for tagging.`
{: #ts_manifest_error_version}

{: tsSymptoms}
Vous avez essayé d'étiqueter votre image, mais vous recevez le message d'erreur suivant : `The manifest version for this image is not supported for tagging. Pour mettre à jour une version de manifeste prise en charge, extrayez et envoyez cette image à l'aide de Docker version 1.12 ou ultérieure, puis relancez l'exécution de la commande 'ibmcloud cr image-tag'.`

{: tsCauses}
La version de manifeste n'est pas pris en charge.

{: tsResolve}
Pour résoudre le problème, procédez comme suit :

1. Effectuez une mise à niveau vers Docker Engine version 1.12 ou ultérieure.

2. Procédez à l'extraction de l'image que vous avez essayé d'étiqueter en exécutant la commande suivante, où `<source_image>` correspond au nom de votre image source.

   ```
   docker pull <source_image>
   ```
   {: pre}

3. Pour mettre à niveau la version de manifeste, envoyez l'image en exécutant la commande suivante :

   ```
   docker push <source_image>
   ```
   {: pre}

4. Etiquetez l'image en exécutant la commande `ibmcloud cr image-tag`. Consultez la rubrique [Création de nouvelles images qui font référence à une image source](/docs/services/Registry?topic=registry-registry_images_#registry_images_source).

## Echec de connexion à Docker sur Mac avec le message suivant : `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`
{: #ts_docker_mac}

{: tsSymptoms}
Vous recevez le message d'erreur suivant lorsque vous tentez d'exécuter la commande `ibmcloud cr login` sur Mac : `Error saving credentials: error storing credentials - err: exit status 1, out: 'The user name or passphrase you entered is not correct.'`

{: tsCauses}
Un problème lié à Docker pour Mac empêche le stockage de vos données d'identification dans la chaîne de certificats macOS.

{: tsResolve}
Vous devriez résoudre ce problème en réamorçant votre Mac. Si le problème persiste malgré le réamorçage de votre Mac, désactivez le stockage des connexions dans votre chaîne de certificats Mac :

1. Dans votre menu, cliquez sur l'icône **Docker**, puis sélectionnez **Préférences**.
2. Désactivez la case **Securely store Docker logins in macOS keychain**.
