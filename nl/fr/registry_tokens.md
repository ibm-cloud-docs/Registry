---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

# Automatisation de l'accès à {{site.data.keyword.registrylong_notm}}
{: #registry_access}

Vous pouvez utiliser une clé d'API {{site.data.keyword.iamlong}} (IAM) pour automatiser l'accès à vos espaces de nom {{site.data.keyword.registrylong_notm}} pour pouvoir y transférer ou en extraire des images.
{:shortdesc}

Essayez-vous d'utiliser vos images de registre dans des déploiements Kubernetes ? Consultez la rubrique [Accès aux images dans d'autres espaces de nom Kubernetes, régions et comptes {{site.data.keyword.cloud_notm}}](/docs/containers?topic=containers-images#other).
{: tip}

Les clés d'API sont liées à votre compte et peuvent être utilisées à travers {{site.data.keyword.cloud_notm}} de sorte que vous n'avez pas besoin de données d'identification différentes pour chaque service. Vous pouvez utiliser la clé d'API dans l'interface de ligne de commande ou dans le cadre de l'automatisation pour vous connecter sous votre identité utilisateur.

Si vous utilisez une clé d'API, vous pouvez contrôler l'accès à vos espaces de nom en utilisant des règles IAM. Pour plus d'informations, voir [Définition de règles de rôle d'accès utilisateur](/docs/services/Registry?topic=registry-user#user).

Pour plus d'informations sur les clés d'API {{site.data.keyword.registrylong_notm}}, voir [Utilisation des clés d'API](/docs/iam?topic=iam-manapikey#manapikey).

Avant de commencer, [installez l'interface de ligne de commande d'{{site.data.keyword.registrylong_notm}} et l'interface de ligne de commande de Docker](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Automatisation de l'accès à vos espaces de nom à l'aide de clés d'API
{: #registry_api_key}

Vous pouvez utiliser des clés d'API pour automatiser l'envoi et l'extraction d'images Docker vers et depuis vos espaces de nom.
{:shortdesc}

### Création d'une clé d'API
{: #registry_api_key_create}

Vous pouvez créer une clé d'API afin de l'utiliser pour vous connecter à votre registre.
{:shortdesc}

Vous pouvez créer des clés d'API d'utilisateur et des clés d'API d'ID de service.

- Pour créer une clé d'API d'ID de service, voir [Création d'une clé d'API pour un ID de service](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
- Pour créer une clé d'API d'utilisateur, voir [Création d'une clé d'API](/docs/iam?topic=iam-userapikey#create_user_key).

### Utilisation d'une clé d'API pour automatiser les accès
{: #registry_api_key_use}

Vous pouvez utiliser une clé d'API pour automatiser l'accès à vos espaces de nom dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Utilisez la clé d'API pour vous connecter à votre registre en exécutant la commande Docker suivante. Remplacez `<your_apikey>` par votre clé d'API et remplacez `<registry_url>` par l'adresse URL du registre où sont configurés vos espaces de nom.

- Pour les espaces de nom définis pour la région Nord de l'Asie Pacifique, utilisez `jp.icr.io`
- Pour les espaces de nom définis pour la région Sud de l'Asie Pacifique, utilisez `au.icr.io`
- Pour les espaces de nom définis pour la région Centre Europe, utilisez `de.icr.io`
- Pour les espaces de nom définis pour la région Sud du Royaume-Uni, utilisez `uk.icr.io`
- Pour les espaces de nom définis pour la région Sud des Etats-Unis, utilisez `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Pour des informations de référence sur la commande, voir [Créer une nouvelle clé d'API pour la plateforme {{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Options d'authentification pour tous les clients
{: #registry_authentication}

Vous pouvez authentifier à l'aide de la commande `docker login` ou d'autres clients de registre.
{:shortdesc}

La plupart des utilisateurs peuvent appliquer la commande `ibmcloud cr login` afin de simplifier `docker login`, mais si vous implémentez l'automatisation ou si vous utilisez un autre client, vous voudrez certainement effectuer une authentification manuelle. Vous devez fournir un nom d'utilisateur et un mot de passe. Dans {{site.data.keyword.registrylong_notm}}, le nom d'utilisateur indique le type de valeur confidentielle présentée dans le mot de passe.

Les noms d'utilisateur valides sont les suivants :

- `iambearer` Le mot de passe contient un jeton d'accès IAM. Ce type d'authentification a une courte durée de vie, mais peut être issue de tous types d'identité IAM.
- `iamrefresh` Le mot de passe doit contenir un jeton d'actualisation IAM utilisé en interne pour générer et actualiser un jeton d'accès IAM. Ce type d'authentification a une durée de vie plus longue et est utilisé par la commande `ibmcloud cr login`.
- `iamapikey` Le mot de passe est une clé d'API IAM. Ce type d'authentification est celui privilégié pour l'automatisation. Vous pouvez utiliser une clé d'API d'utilisateur ou d'ID de service (voir [Création d'une clé d'API](#registry_api_key_create)).

Vous n'avez pas besoin d'utiliser la commande `docker` pour l'authentification avec le registry. Par exemple, vous pouvez démarrer des applications Cloud Foundry à partir d'images du registre en utilisant l'interface de ligne de commande Cloud Foundry :

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Remplacez `<apikey>` par votre clé d'API, `<region>` par le nom de votre [région](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` par votre espace de nom, et `<image_repo>` par le référentiel.

Pour plus d'informations, voir [Utilisation d'un registre d'images privé](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
