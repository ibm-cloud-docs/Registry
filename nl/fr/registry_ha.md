---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, high availability


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

# Haute disponibilité et reprise après incident
{: #ha-dr}

Le service {{site.data.keyword.registrylong}} est un service régional, à haute disponibilité.
{:shortdesc}

* Dans chaque région prise en charge, la charge du trafic est répartie dans l'infrastructure de registre dans plusieurs zones de disponibilité, sans point de défaillance unique.

* Les données stockées dans {{site.data.keyword.registrylong_notm}} sont régulièrement sauvegardées, ce qui augmente la résilience.

* Si la disponibilité de vos images dans le cas où une région toute entière ne serait plus disponible vous préoccupe, vous pouvez décider d'envoyer (par commande push) vos images à plusieurs registres régionaux.
  
  Vous pouvez également choisir d'envoyer vos images à plusieurs registres pour le cas où elles seraient involontairement supprimées ou écrasées.

  Pour plus d'informations sur les régions, voir [Régions](/docs/services/Registry?topic=registry-registry_overview#registry_regions).
