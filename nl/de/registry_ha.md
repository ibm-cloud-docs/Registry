---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

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

# Hochverfügbarkeit und Disaster-Recovery
{: #ha-dr}

Der {{site.data.keyword.registrylong}}-Service ist ein hochverfügbarer regionaler Service.
{:shortdesc}

* In jeder unterstützten Region wird ein Lastausgleich für den Datenverkehr über die gesamte Registryinfrastruktur in mehreren Verfügbarkeitszonen durchgeführt, sodass kein einzelner Fehlerpunkt (Single Point of Failure) vorhanden ist.

* Die in {{site.data.keyword.registrylong_notm}} gespeicherten Daten werden regelmäßig gesichert, was zu zusätzlicher Ausfallsicherheit beiträgt.

* Wenn Sie befürchten, dass Ihre Images beim Ausfall einer gesamten Region nicht verfügbar sind, können Sie Ihre Images an Registrys in mehreren Regionen übertragen.
  
  Sie können Ihre Images auch an mehrere Registrys übertragen, um geschützt zu sein, falls die Images versehentlich gelöscht oder überschrieben werden.

  Weitere Informationen zu Regionen finden Sie unter [Regionen](/docs/services/Registry/registry_overview.html#registry_regions).
