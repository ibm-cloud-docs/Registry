---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker with LogDNA events, Activity Tracker events, events, track,

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

# Evénements d'Activity Tracker
{: #at_events}

Suivez l'interaction des utilisateurs et des applications avec le service {{site.data.keyword.registrylong}} dans {{site.data.keyword.cloud}}.
{:shortdesc}

Le service {{site.data.keyword.at_full_notm}} ou (pour les utilisateurs existants uniquement) le service {{site.data.keyword.cloudaccesstrailfull_notm}} enregistre les activités lancées par les utilisateurs qui modifient l'état d'un service dans {{site.data.keyword.cloud_notm}}.
Pour plus d'informations, voir [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started) ou, pour les utilisateurs existants, [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

Le tableau suivant répertorie les méthodes d'API générant un événement lorsqu'elles sont appelées :

<table>
  <caption>Tableau 1. Actions qui génèrent des événements</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Crée une exemption Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Supprime une exemption Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>Génère une image Docker dans {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.bulkdelete`</td>
	  <td>Supprime plusieurs images d'{{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>Supprime une image d'{{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>Affiche les détails d'une image.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>Répertorie les images de votre compte {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>Extrait une image d'{{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>Envoie une image par commande push vers {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>Supprime une ou plusieurs images spécifiées de votre registre {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Ajoute une étiquette qui fait référence à une image {{site.data.keyword.registrylong_notm}} préexistante.</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>Supprime une ou plusieurs étiquettes de chaque image spécifiée dans {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>Ajoute un espace de nom à {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>Supprime un espace d'{{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>Répertorie les espaces de nom de votre compte {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>Affiche les quotas actuels de trafic et de stockage ainsi que les informations d'utilisation de ces quotas.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>Modifie les quotas.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>Supprime un jeton de registre.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>Extrait des informations relatives à un jeton de registre.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>Répertorie les jetons de registre de votre compte {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>Supprime des jetons de registre multiples.</td>
  </tr><tr>
    <td>`container-registry.retentionanalysis`</td>
	  <td>Nettoie vos espaces de nom en conservant uniquement les images qui répondent à vos critères. Conserve les images pour chaque référentiel au sein d'un espace de nom dans {{site.data.keyword.registrylong_notm}} en appliquant les critères spécifiés. Toutes les autres images dans l'espace de nom sont supprimées. </br> La demande d'obtention de la liste d'images à supprimer est une action `post` à un type d'événement `retentionanalysis`. La suppression est une action `bulkdelete` unique à un type d'événement `images` et également une action `delete` pour chaque image individuelle.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Affiche des informations relatives au plan de tarification actuel.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Effectue une mise à niveau vers le plan standard.</td>
  </tr>
 </table>

## Où rechercher les événements ?
{: #ui}

### Evénements {{site.data.keyword.at_full_notm}}
{: #ui_atlogdna}

Les événements {{site.data.keyword.at_full_notm}} sont disponibles dans le **domaine de compte** {{site.data.keyword.at_full_notm}} qui est disponible dans la région {{site.data.keyword.cloud_notm}} dans laquelle les événements sont générés, à l'exception de `ap-south`. Les événements de `ap-south` s'affichent dans `Tokyo (jp-tok)`.

La [région](/docs/services/Registry?topic=registry-registry_overview#registry_regions) dans laquelle un événement {{site.data.keyword.registrylong_notm}} ou Vulnerability Advisor est disponible correspond à la région {{site.data.keyword.registrylong_notm}} dans laquelle la ressource est disponible. Les images et les espaces de nom sont des exemples de ressources.

| Région de votre registre de compte | Nom de domaine de votre registre | Emplacement des événements {{site.data.keyword.at_full_notm}} |
|:-----------------|:-----------------|:-----------------|
| `us-south` | `us.icr.io` | `Dallas (us-south)` |
| `eu-central` | `de.icr.io` | `Francfort (eu-de)` |
| `uk-south` | `uk.icr.io` | `Londres (eu-gb)` |
| `ap-south` | `au.icr.io` | `Tokyo (jp-tok)` |
| `ap-north` | `jp.icr.io` | `Tokyo (jp-tok)` |
{: caption="Tableau 2. Emplacements des événements {{site.data.keyword.at_full_notm}} " caption-side="top"}

| Registre | Base de registre globale | Emplacement des événements {{site.data.keyword.at_full_notm}} |
|:-----------------|:-----------------|:-----------------|
| Global | `icr.io` | `Dallas (us-south)` |
{: caption="Tableau 3. Emplacement des événements {{site.data.keyword.at_full_notm}} de la base de registre globale" caption-side="top"}

### Evénements {{site.data.keyword.cloudaccesstraillong_notm}}
{: #ui_at}

Les événements {{site.data.keyword.cloudaccesstraillong_notm}}, pour les utilisateurs existants uniquement, sont disponibles dans le **domaine de compte** {{site.data.keyword.cloudaccesstraillong_notm}} qui est disponible dans la région {{site.data.keyword.cloud_notm}} dans laquelle les événements sont générés, à l'exception de `ap-north`. Les événements de `ap-north` s'affichent dans `ap-south`.

{{site.data.keyword.cloudaccesstrailfull_notm}} est obsolète. A compter du 9 mai 2019, vous ne pourrez plus mettre à disposition de nouvelles instances {{site.data.keyword.cloudaccesstrailshort}}. Les instances existantes du plan premium sont prises en charge jusqu'au 30 septembre 2019. Pour continuer à surveiller l'activité de votre compte {{site.data.keyword.cloud_notm}}, mettez à disposition une instance [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).
{: deprecated}

La [région](/docs/services/Registry?topic=registry-registry_overview#registry_regions) dans laquelle un événement {{site.data.keyword.registrylong_notm}} ou Vulnerability Advisor est disponible correspond à la région du {{site.data.keyword.registrylong_notm}} dans lequel la ressource est disponible. Les images et les espaces de nom sont des exemples de ressources.
