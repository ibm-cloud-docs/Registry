---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, Vulnerability Advisor,

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
{:faq: data-hd-content-type='faq'}

# Foire aux questions
{: #registry_faq}

Foire aux questions concernant {{site.data.keyword.registrylong}}.
{: shortdesc}

## Comment établir la liste des images publiques ?
{: #faq_list_public_images}
{: faq}

Pour répertorier les images publiques, exécutez la commande `ibmcloud` suivante de manière à cibler la base de registre globale et à répertorier les images publiques fournies par IBM :

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Puis-je utiliser des outils non Docker pour générer mes images et les envoyer (push) au registre ?
{: #faq_tools}
{: faq}

Oui, sous réserve que l'outil prenne en charge le protocole et le format d'image OCI.

## Comment utiliser le contrôle d'accès avec IAM ?
{: #faq_access_control}
{: faq}

Vous pouvez créer des règles {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) pour contrôler l'accès à vos espaces de nom dans {{site.data.keyword.registrylong_notm}}. Pour plus d'informations, voir [Tutoriel : Octroi de droits d'accès aux ressources {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam_access) et [Gestion des accès utilisateur avec Identity and Access Management](/docs/services/Registry?topic=registry-iam).

## Quelles régions sont disponibles pour {{site.data.keyword.registrylong_notm}} ?
{: #faq_regions}
{: faq}

Vous pouvez héberger des images dans des [régions locales](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local). Les images publiques hébergées par IBM sont disponibles dans la [Base de registre globale](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## Pourquoi ai-je reçu un message d'erreur d'analyse introuvable pour une image nouvellement ajoutée ?
{: #faq_va_new_scan_error}
{: faq}

Si vous générez le rapport de vulnérabilité immédiatement après avoir ajout l'image au registre, il est possible que vous receviez l'erreur suivante :

```
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

Vous recevez ce message parce que les images sont analysées de manière asynchrone par rapport aux demandes de résultats, et l'exécution du processus d'analyse prend un certain temps. En fonctionnement normal, l'analyse se déroule durant les quelques minutes qui suivent l'ajout de l'image au registre, en fonction de variables telles que la taille d'image et la quantité de trafic reçue par le registre.

Si vous recevez ce message dans le cadre d'un pipeline de génération et que cette erreur se produit régulièrement, essayez d'ajouter de la logique de relance comportant une courte pause. 

Si les performances restent inacceptables, prenez contact avec le support. Voir [Aide et support pour {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-ts_index#gettinghelp).

## Comment une analyse Vulnerability Advisor est-elle déclenchée ?
{: #faq_va_trigger_scan}
{: faq}

L'analyse d'une image est déclenchée de l'une des façons suivantes :

- Si une nouvelle image est envoyée par commande push au registre.
- Si l'image n'a pas été analysée depuis 7 jours, elle est placée en file d'attente pour réanalyse, ce qui peut prendre un certain temps.
- Si un nouvel avis de sécurité est publié pour un module installé dans l'image, elle est placée en file d'attente pour réanalyse, ce qui peut prendre un certain temps. Les réanalyses déclenchées par l'édition de nouveaux avis de sécurité sont disponibles pour les images Ubuntu et Debian uniquement.

## A quelle fréquences les avis de sécurité sont-ils mis à jour ?
{: #faq_va_update_security_notice}
{: faq}

Les avis de sécurité pour Vulnerability Advisor sont chargés depuis les sites de système d'exploitation des fournisseurs toutes les 12 heures environ.
