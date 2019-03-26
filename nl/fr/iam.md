---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, user access, Identity and Access Management, policies, user roles, access policies, platform management roles, service access roles, access roles,

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

# Gestion des accès utilisateur avec Identity and Access Management
{: #iam}

L'accès çà {{site.data.keyword.registrylong}} pour les utilisateurs de votre compte est contrôlé par {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM).
{: shortdesc}

Lorsque des règles IAM sont activées pour votre compte dans {{site.data.keyword.registrylong_notm}}, chaque utilisateur qui accède au service {{site.data.keyword.registrylong_notm}} dans votre compte doit se voir affecter une règle d'accès avec un rôle utilisateur IAM défini. Cette règle détermine le rôle de l'utilisateur dans le contexte du service, ainsi que les actions qu'il peut exécuter. Chaque action dans {{site.data.keyword.registrylong_notm}} est mappée à un ou plusieurs [rôles utilisateur IAM](/docs/iam?topic=iam-userroles).

Les règles IAM ne sont appliquées que lorsque vous utilisez IAM pour vous connecter à {{site.data.keyword.registrylong_notm}}. Si vous vous connectez à {{site.data.keyword.registrylong_notm}} à l'aide d'une autre méthode, par exemple, un jeton de registre, vos règles ne sont pas appliquées. Si vous souhaitez limiter l'accès à un ou plusieurs espaces de nom pour un ID que vous utilisez pour l'automatisation, pensez à utiliser un ID de service IAM à la place d'un jeton de registre. Pour plus d'informations sur les ID de service, voir [Création et gestion des ID de service](/docs/iam?topic=iam-serviceids#serviceids).

Pour plus d'informations sur IAM, voir [IBM Cloud Access and Management](/docs/iam?topic=iam-iamoverview#iamoverview).

Pour obtenir des informations sur l'activation de règles pour {{site.data.keyword.registrylong_notm}}, voir [Définition de règles de rôle d'accès utilisateur](/docs/services/Registry?topic=registry-user#user).

Les règles permettent d'activer les accès à différents niveaux. Certaines des options incluent les niveaux d'accès suivants :

* Accès au service dans votre compte
* Accès à une ressource spécifique dans le service
* Accès à tous les services activés par IAM dans votre compte

Après avoir défini la portée de la règle d'accès, vous lui affectez un rôle. Consultez les tableaux suivants qui décrivent les actions que chaque rôle permet d'effectuer au sein du service {{site.data.keyword.registrylong_notm}} .

Pour plus d'informations sur l'affectation de rôles utilisateur dans l'interface utilisateur, voir [Gestion de l'accès IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

Essayez le tutoriel intitulé [Tutoriel : Octroi de droits d'accès aux ressources{{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam_access#iam_access).
{: tip}

## Rôles de gestion de plateforme
{: #platform_management_roles}

Le tableau suivant détaille les actions mappées sur les rôles de gestion de plateforme. Les rôles de gestion de plateforme permettent aux utilisateurs d'effectuer des tâches sur les ressources de service au niveau plateforme, par exemple, affecter des accès utilisateur pour le service et créer ou supprimer des ID de service.

| Rôle de gestion de plateforme | Description des actions | Exemples d'action|
|:-----------------|:-----------------|:-----------------|
| Afficheur | Non pris en charge | |
| Editeur | Non pris en charge | |
| Opérateur | Non pris en charge | |
| Administrateur | <ul><li>Configurer l'accès pour les autres utilisateurs</li><li>Configurer des jetons de registre</li><li>Créer des clusters</li></ul> | <ul><li>Pour plus d'informations sur l'affectation de rôles utilisateur dans l'interface utilisateur, voir [Gestion de l'accès IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).</li><li>Ajouter, répertorier, extraire et retirer des jetons de registre</li><li>Pour créer des clusters dans {{site.data.keyword.containerlong_notm}}, vous devez affecter le rôle Administrateur pour {{site.data.keyword.registrylong_notm}} à l'utilisateur. Voir [Préparation à la création de clusters](/docs/containers?topic=containers-clusters#cluster_prepare).</li></ul> |
{: caption="Tableau 1. Rôles et actions des utilisateurs IAM" caption-side="top"}

Pour {{site.data.keyword.registrylong_notm}}, les actions suivantes existent :

| Action| Opération sur le service | Rôle
|:-----------------|:-----------------|:--------------|
| `container-registry.registrytoken.create` | [`ibmcloud cr token-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_add) Ajoute un jeton que vous pouvez utiliser pour contrôler l'accès à un registre. | Administrateur |
| `container-registry.registrytoken.delete` | [`ibmcloud cr token-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_rm) Retire un ou plusieurs jetons spécifiés. | Administrateur |
| `container-registry.registrytoken.get` | [`ibmcloud cr token-get`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_get) Extrait le jeton spécifié du registre. | Administrateur |
| `container-registry.registrytoken.list` | [`ibmcloud cr token-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_list) Affiche tous les jetons qui existent pour votre compte {{site.data.keyword.Bluemix_notm}}. | Administrateur |
{: caption="Tableau 2. Actions de plateforme et opérations de configuration d'{{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Rôles d'accès au service
{: #service_access_roles}

Le tableau ci-dessous détaille les actions qui sont mappées aux rôles d'accès de service. Les rôles d'accès aux services permettent aux utilisateurs d'accéder à {{site.data.keyword.registrylong_notm}} ainsi que la possibilité d'appeler l'API {{site.data.keyword.registrylong_notm}}.

| Rôle Accès au service | Description des actions | Exemples d'action|
|:-----------------|:-----------------|:-----------------|
| Lecteur | Peut afficher des informations. | <ul><li>Afficher, inspecter et extraire les images</li><li>Afficher les espaces de nom</li><li>Afficher les quotas</li><li>Afficher les rapports de vulnérabilité</li><li>Afficher les signatures d'image</li></ul>|
| Auteur | Peut éditer des informations. |<ul><li>Générer, envoyer et supprimer des images</li><li>Afficher les quotas</li><li>Signer les images</li><li>Ajouter et retirer des espaces de nom</li></ul> |
| Responsable | Peut effectuer toutes les actions. | <ul><li>Afficher, inspecter, extraire, générer, envoyer et supprimer des images</li><li>Afficher, ajouter et retirer des espaces de nom</li><li>Afficher des définir des quotas</li><li>Afficher les rapports de vulnérabilité</li><li>Afficher et créer des signatures d'image</li><li>Réviser et modifier les plans de tarification</li><li>Activer l'application des règles IAM</li><li>Gérer des exemptions Vulnerability Advisor</li></ul> |
{: caption="Tableau 3. Rôles et actions d'accès au service IAM" caption-side="top"}

 Pour les commandes {{site.data.keyword.registrylong_notm}}, vous devez disposer au minimum de l'un des rôles spécifiés, comme indiqué dans les tableaux ci-après. Dans le cadre de la création d'une règle qui permet d'accéder à {{site.data.keyword.registrylong_notm}}, cette règle doit comporter le nom de service `container-registry`, l'instance de service doit être vide et la région doit être celle à laquelle vous souhaitez autoriser l'accès, ou elle doit être vide si vous souhaitez accorder l'accès à toutes les régions.

### Rôles d'accès pour la configuration d'{{site.data.keyword.registrylong_notm}}
{: #access_roles_configure}

Pour accorder à un utilisateur les droits nécessaires pour configurer votre {{site.data.keyword.registrylong_notm}} dans votre compte, vous devez créer une règle qui accorde un ou plusieurs des rôles répertoriés dans le tableau ci-après. Lorsque vous créez votre règle, vous ne devez pas spécifier un élément `resource type` ni un élément `resource`.

**Exemple**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

| Action| Opération sur le service | Rôle
|:-----------------|:-----------------|:--------------|
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) Activer l'application des règles IAM. | Responsable |
| `container-registry.exemption.manager` | <ul><li>[`ibmcloud cr exemption-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add) Créer une exemption pour un problème de sécurité.</li><li>[`ibmcloud cr exemption-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list) Répertorier vos exemptions pour les problèmes de sécurité.</li><li>[`ibmcloud cr exemption-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm) Supprimer une exemption pour un problème de sécurité.</li><li>[`ibmcloud cr exemption-types`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types) Répertorier les types de problèmes de sécurité que vous pouvez exempter.</li></ul> | Responsable |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan) Afficher le plan de tarification. | Responsable |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade) Effectuer une mise à niveau vers le plan standard. | Responsable |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota) Afficher vos quotas actuels de trafic et de stockage, ainsi que les informations d'utilisation de ces quotas. | Lecteur, Editeur, Responsable |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set) Modifier le quota spécifié. | Responsable |
{: caption="Tableau 4. Actions de service et opérations de configuration d'{{site.data.keyword.registrylong_notm}}" caption-side="top"}

### Rôles d'accès pour l'utilisation d'{{site.data.keyword.registrylong_notm}}
{: #access_roles_using}

Pour accorder à un utilisateur les droits nécessaires pour accéder au contenu {{site.data.keyword.registrylong_notm}} dans votre compte, vous devez créer une règle qui accorde un ou plusieurs des rôles répertoriés dans le tableau ci-après. Lorsque vous créez votre règle, vous pouvez limiter l'accès à un espace de nom spécifique en spécifiant le type de ressource `namespace` et le nom de l'espace de nom comme ressource. Si vous ne spécifiez pas un élément `resource-type` ni un élément `resource`, la règle accorde l'accès à toutes les ressources du compte.

**Exemple**

```
bx iam user-policy-create <user_email> --service-name container-registry --region <us-south> --roles <Reader> [--resource-type namespace --resource <namespace_name>]
```
{: pre}

| Action | Opération sur le service | Rôle
|:-----------------|:-----------------|:--------------|
| `container-registry.image.build` | [`ibmcloud cr build`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build) Générer une image de conteneur. | Editeur, Responsable |
| `container-registry.image.delete` | <ul><li> [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) Supprimer une ou plusieurs images.</li><li>`docker trust revoke` Supprimer la signature. </li></ul> | Editeur, Responsable |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect) Afficher les détails d'une image spécifique. | Lecteur, Responsable |
| `container-registry.image.list` | [`ibmcloud cr image-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list) Répertorier les images de votre conteneur. | Lecteur, Responsable |
| `container-registry.image.pull` | <ul><li>`docker pull` Extraire l'image. </li><li>`docker trust inspect` Inspecter la signature. </li></ul> | Lecteur, Editeur, Responsable |
| `container-registry.image.push` | <ul><li>`docker push` Envoyer l'image.</li><li>`docker trust sign` Signer l'image.</li><li>[`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load) Importer le logiciel IBM qui est téléchargé depuis [IBM Passport Advantage Online pour les clients ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/passportadvantage/pao_customer.html) et conditionné pour une utilisation avec Helm dans votre espace de nom d'{{site.data.keyword.registrylong_notm}}.</li></ul> | Editeur, Responsable |
| `container-registry.image.tag` | [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) Créer une nouvelle image qui fait référence à une image source. Les images source et cible doivent se trouver dans la même région. | Lecteur, auteur ou responsable pour l'image source ; auteur ou responsable pour l'image cible |
| `container-registry.image.vulnerabilities` | [`ibmcloud cr vulnerability-assessment`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va) Afficher un rapport d'évaluation des vulnérabilités pour votre image. | Lecteur, Responsable |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add) Ajouter un espace de nom. | Editeur, Responsable |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm) Retirer un espace de nom. | Editeur, Responsable |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list) Afficher vos espaces de nom. | Lecteur, Responsable |
{: caption="Tableau 5. Actions de service et opérations d'utilisation d'{{site.data.keyword.registrylong_notm}}" caption-side="top"}
