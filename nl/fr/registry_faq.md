---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, FAQ, Vulnerability Advisor,

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

## Comment doit-on répertorier les images publiques ?
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

## Peut-on utiliser des outils non Docker pour générer des images et les envoyer au registre ?
{: #faq_tools}
{: faq}

Oui, si l'outil prend en charge le protocole et le format d'image OCI.

## Comment utilise-t-on le contrôle d'accès avec {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} ?
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

Si vous obtenez le rapport de vulnérabilité immédiatement après avoir ajouté l'image au registre, il est possible que l'erreur suivante s'affiche :

```
BXNVA0009E:  <imagename> has not been scanned. Try again later.
If this issue persists, contact support for help;
see https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

Vous recevez ce message parce que les images sont analysées de manière asynchrone par rapport aux demandes de résultats, et l'exécution du processus d'analyse prend un certain temps. En mode de fonctionnement normal, l'analyse se termine dans les premières minutes qui suivent l'ajout de l'image au registre. Le temps qu'il faut pour terminer dépend de variables comme la taille de l'image et la quantité de trafic que le registre reçoit.

Si vous recevez ce message dans le cadre d'un pipeline de génération et que cette erreur se produit régulièrement, essayez de faire appel à une logique de relance qui comporte une courte pause.

Si les performances restent inacceptables, prenez contact avec le support. Voir [Aide et support pour {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-ts_index#gettinghelp).

## Comment une analyse Vulnerability Advisor est-elle déclenchée ?
{: #faq_va_trigger_scan}
{: faq}

L'analyse d'une image est déclenchée de l'une des façons suivantes :

- Si une nouvelle image est envoyée par commande push au registre.
- Si la dernière analyse remonte à plus de 7 jours, l'image est mise en file d'attente pour une nouvelle analyse, ce qui peut prendre un certain temps.
- Si un nouvel avis de sécurité est publié pour un paquet qui est installé dans l'image, l'image est mise en file d'attente pour une nouvelle analyse, ce qui peut prendre un certain temps. Les réanalyses déclenchées par l'édition de nouveaux avis de sécurité sont disponibles pour les images Ubuntu et Debian uniquement.

## A quelle fréquences les avis de sécurité sont-ils mis à jour ?
{: #faq_va_update_security_notice}
{: faq}

Les avis de sécurité de Vulnerability Advisor sont chargés depuis les sites de système d'exploitation des fournisseurs toutes les 12 heures environ.
