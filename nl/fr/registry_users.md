---

copyright:
  years: 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Définition des règles de rôle d'accès utilisateur
{: #user access}

En tant qu'administrateur, vous pouvez définir des règles d'accès pour votre registre afin de créer différents niveaux d'accès pour différents utilisateurs. Par exemple, vous pouvez autoriser certains utilisateurs à définir des quotas tandis que d'autres utilisateurs peuvent uniquement afficher des quotas.
{: shortdesc}

Vous devez définir des règles d'accès pour tous les utilisateurs qui utilisent {{site.data.keyword.registrylong}}. La portée d'une règle d'accès est basée sur le ou les rôles définis d'un utilisateur qui déterminent les actions qu'ils sont autorisés à effectuer. Certaines règles sont prédéfinies, mais d'autres peuvent être personnalisées.

Si vous avez commencé à utiliser {{site.data.keyword.registrylong_notm}} avant le 4 octobre 2018, vous devez activer l'application des règles pour que vos règles puissent être effectives. Voir [Activation de l'application des règles pour des utilisateurs existants](#existing_users).
{: tip}

Pour en savoir plus sur les règles de rôle d'accès IAM ({{site.data.keyword.iamlong}}), voir [{{site.data.keyword.iamshort}}](/docs/iam/index.html#iamoverview).

## Création de règles
{: #create}

Si vous souhaitez contrôler l'accès à des ressources, vous devez affecter des rôles à des utilisateurs ou des ID de service. L'accès aux ressources {{site.data.keyword.registrylong_notm}} peut être accordé à la ressource d'espace de nom par nom ou à l'ensemble du service, autrement dit, à tous les espaces de nom du compte. 

Si vous souhaitez accorder un accès à tout, ne spécifiez pas un type de ressource ou une ressource. Si vous souhaitez accorder un accès à un espace de nom spécifique, spécifiez `namespace` comme type de ressource et utilisez le nom d'espace de nom comme ressource. 

**Avant de commencer**

- Déterminez les rôles à affecter à chaque utilisateur et sur quelles ressources {{site.data.keyword.registrylong_notm}}. Voir [Rôles IAM](/docs/services/Registry/iam.html#iam). Tenez compte du fait que vous pouvez créer plusieurs règles, par exemple, vous pouvez accorder des droits d'accès en écriture sur une ressource, accorder des droits d'accès en lecture seule sur une autre ressource, et n'accorder aucun droit d'accès sur une autre ressource. Les règles s'additionnent, ce qui signifie qu'une règle d'accès en lecture globale et une règle d'accès en écriture limitée à une ressource octroient des droits d'accès en lecture et en écriture sur cette ressource. 

- [Invitez des utilisateurs et affectez des droits d'accès](/docs/iam/iamuserinv.html#iamuserinv). 

  Si vous souhaitez que des utilisateurs puissent créer des clusters dans {{site.data.keyword.containerlong_notm}}, prenez soin d'affecter le rôle Administrateur pour {{site.data.keyword.registrylong_notm}} à ces utilisateurs et n'affectez pas un groupe de ressources. Voir [Préparation à la création de clusters](/docs/containers/cs_clusters.html#cluster_prepare).
  {: tip}

Pour que des règles puissent être créées pour {{site.data.keyword.registrylong_notm}}, la zone Nom de service doit contenir la valeur `container-registry`.

* Pour créer une règle pour des utilisateurs, consultez la rubrique [Gestion des droits d'accès à des ressources](/docs/iam/mngiam.html#iammanidaccser).
* Pour créer une règle pour les ID de service, exécutez la commande `ibmcloud iam service-policy-create` ou utilisez l'interface graphique afin de lier des rôles à vos ID de service. Pour créer des règles, vous devez disposer du rôle Administrateur. Vous disposez automatiquement du rôle Administrateur sur votre propre compte. Pour plus d'informations, voir [Création et gestion des ID de service](/docs/iam/serviceid.html#serviceids) and [Gestion des règles d'accès d'ID de service](/docs/iam/serviceidaccess.html#serviceidpolicy).

## Activation de l'application des règles pour des utilisateurs existants
{: #existing_users}

Pour les utilisateurs dont les accès ont été configurés après le 4 octobre 2018, les règles IAM sont activées par défaut. Pour les utilisateurs dont les accès ont été configurés avant le 4 octobre 2018, une fois vos règles créées, vous devez activer leur application pour qu'elles puissent être effectives. 

1. [Créez des règles](#create) pour vos utilisateurs et vos ID de service. 

2. Pour activer l'application des règles, exécutez la commande [`bx cr iam-policies-enable`](/docs/services/Registry/registry_cli.html#bx_cr_iam_policies_enable). 

    Vous devez disposer du rôle Responsable sur le compte afin de pouvoir exécuter la commande `ibmcloud cr iam-policies-enable`. Vous disposez automatiquement du rôle Responsable sur votre propre compte. {: tip}
