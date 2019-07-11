---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker events, Activity Tracker events, events, track,

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

# Evénements {{site.data.keyword.cloudaccesstrailshort}}
{: #at_events}

Utilisez le service {{site.data.keyword.cloudaccesstrailfull}} pour savoir comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.registrylong}} dans {{site.data.keyword.cloud}}.
{:shortdesc}

Le service {{site.data.keyword.cloudaccesstrailfull_notm}} enregistre des activités initiées par l'utilisateur qui change l'état d'un service dans {{site.data.keyword.cloud_notm}}.
Pour plus d'informations, voir [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

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
    <td>`container-registry.image.delete`</td>
	  <td>Supprime une image depuis {{site.data.keyword.registrylong_notm}}.</td>
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
	  <td>Ajoute une nouvelle étiquette qui fait référence à une image {{site.data.keyword.registrylong_notm}} préexistante.</td>
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
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Affiche des informations relatives au plan de tarification actuel.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Effectuez une mise à niveau vers le plan standard.</td>
  </tr>
 </table>

## Où rechercher les événements ?
{: #ui}

Les événements {{site.data.keyword.cloudaccesstrailshort}} sont disponibles dans le **domaine de compte** {{site.data.keyword.cloudaccesstrailshort}} qui se trouve dans la région {{site.data.keyword.cloud_notm}} où les événements sont générés, sauf pour la région `ap-north`. Les événements pour `ap-north` s'affichent dans `ap-south`.

La [région](/docs/services/Registry?topic=registry-registry_overview#registry_regions) dans laquelle un événement {{site.data.keyword.registrylong_notm}} ou Vulnerability Advisor est disponible correspond à la région du registre {{site.data.keyword.registrylong_notm}} dans lequel la ressource (image ou espace de nom, par exemple) est disponible.
