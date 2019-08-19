---

copyright:
  years: 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# Releaseinformationen
{: #registry_release_notes}

Hier erfahren Sie mehr über die neuesten Änderungen bei {{site.data.keyword.registrylong}} und Vulnerability Advisor. Die Änderungen sind nach Datum gruppiert.
{:shortdesc}

## 1. August 2019
{: #01aug2019}

<dl>
  <dt>Der Befehl `ibmcloud cr retention-run` ist verfügbar</dt>
  <dd>Der Befehl `ibmcloud cr retention-run` bereinigt Ihre Namensbereiche durch Aufbewahren von Images für jedes Repository innerhalb eines Namensbereichs in {{site.data.keyword.registrylong_notm}} durch Anwenden angegebener Kriterien. Alle anderen Images im Namensbereich werden gelöscht.
  
  Weitere Informationen finden Sie in [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) und in [Images aufbewahren](/docs/services/Registry?topic=registry-registry_retention).</dd>
</dl>

## 25. Juli 2019
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.at_full_notm}} verfügbar für {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Verwenden Sie den {{site.data.keyword.at_full_notm}}-Service, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.registrylong_notm}}-Service in {{site.data.keyword.cloud}} interagieren.

  Weitere Informationen finden Sie in [Activity Tracker-Ereignisse](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>

## 1. Juli 2019
{: #1jul2019}

<dl>
  <dt>Der Befehl `ibmcloud cr token-add` ist nicht mehr verfügbar</dt>
  <dd>Die Unterstützung für den Befehl `ibmcloud cr token-add` wird eingestellt. Sie können weder in der CLI noch in der API weiterhin Registry-Tokens hinzufügen.</dd>
</dl>

## 27. Juni 2019
{: #27jun2019}

<dl>
  <dt>Container Scanner ist nicht mehr verfügbar</dt>
  <dd>Die Unterstützung für den Container Scanner wird eingestellt. Mit dem Vulnerability Advisor können weiterhin Images gescannt werden, die per Push-Operation an {{site.data.keyword.registrylong_notm}} übertragen werden.</dd>
</dl>

## 13. Juni 2019
{: #13jun2019}

<dl>
  <dt>Tags aus Images entfernen</dt>
  <dd>Entfernen Sie ein Tag oder mehrere Tags aus jedem angegebenen Image in {{site.data.keyword.registrylong_notm}}.

  Um ein Tag aus einem Image zu entfernen, das zugrunde liegende Image und alle anderen Tags jedoch beibehalten möchten, verwenden Sie den Befehl [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag). Wenn Sie das zugrunde liegende Image und alle seine Tages löschen möchten, verwenden Sie stattdessen den Befehl [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm).

  Weitere Informationen finden Sie im Abschnitt [Tags aus Images in Ihrem privaten {{site.data.keyword.cloud_notm}}-Repository entfernen](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag).</dd>
</dl>

## 13. Mai 2019
{: #13may2019}

<dl>
  <dt>Ende der Unterstützung für Container Scanner</dt>
  <dd>Container Scanner ist nun veraltet und kann nicht mehr verwendet werden.

  Weitere Informationen finden Sie in [Container Scanner installieren (veraltet)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 2. April 2019
{: #2apr2019}

<dl>
  <dt>Allgemeine Verfügbarkeit von Container Image Security Enforcement</dt>
  <dd>Mit Container Image Security Enforcement können Sie Ihre Container-Images überprüfen, bevor Sie sie in Ihrem Cluster in {{site.data.keyword.containerlong_notm}} bereitstellen. Sie können steuern, von wo aus Images bereitgestellt werden, Vulnerability Advisor-Richtlinien durchsetzen und sicherstellen, dass [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) korrekt auf das Image angewendet wird.

  Weitere Informationen finden Sie in [Sicherheit des Container-Image durchsetzen](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 14. März 2019
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} verfügbar für {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Verwenden Sie den {{site.data.keyword.cloudaccesstraillong_notm}}-Service, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.registrylong_notm}}-Service in {{site.data.keyword.cloud}} interagieren.

  Weitere Informationen finden Sie in [Activity Tracker-Ereignisse](/docs/services/Registry?topic=registry-at_events#at_events).
</dd>
</dl>

## 25. Februar 2019
{: #25feb2019}

<dl>
  <dt>Neue Domänennamen</dt>
  <dd>{{site.data.keyword.registrylong_notm}} übernimmt neue Domänennamen. Die neuen Domänennamen sind in der Konsole und in der CLI verfügbar. Sie können jetzt die neuen `icr.io`-Domänennamen verwenden. Die bereits vorhandenen Domänennamen des Typs `registry.bluemix.net` sind zwar veraltet, doch Sie können sie noch bis zum Datum, an dem die Unterstützung endet, nutzen. Allerdings ist noch kein Datum bekannt, an dem die Unterstützung endet. Weitere Informationen finden Sie in [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions) und [Einführung neuer IBM Cloud Container Registry-Domänennamen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  Signaturen gelten für den gesamten Imagenamen; dieser schließt den Domänennamen ein. Wenn Sie Content Trust verwenden, müssen Sie neue Signaturen hinzufügen, damit Sie Content Trust unter dem neuen Domänennamen verwenden können. Weitere Informationen zu Content Trust finden Sie unter [Images für vertrauenswürdige Inhalte signieren](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

<dl>
  <dt>Geheime Schlüssel für {{site.data.keyword.containerlong_notm}}-Cluster mit einem IAM-API-Schlüssel mittels Pull-Operation extrahieren</dt>
  <dd>Das Extrahieren geheimer Schlüssel für Cluster mittels Pull-Operation für die `icr.io`-Domänen wird mithilfe eines IAM-API-Schlüssels ({{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM)) autorisiert. Wenn Sie also mehr Kontrolle über den Zugriff auf Ihre {{site.data.keyword.registrylong_notm}}-Ressourcen benötigen, können Sie IAM-Richtlinien hinzufügen. Beispielsweise können Sie die API-Schlüsselrichtlinien im extrahierten geheimen Schlüssel des Clusters so ändern, dass Images nur aus einer bestimmten Registry-Region oder aus einem bestimmten Namensbereich abgerufen werden.
  
  Weitere Informationen finden Sie in der Beschreibung der [Vorgehensweise, wie Ihr Cluster autorisiert wird, um Images von {{site.data.keyword.registrylong_notm}} mittels Pull-Operation zu extrahieren](/docs/containers?topic=containers-images#cluster_registry_auth).</dd>
</dl>

<dl>
  <dt>Neue Region in Asien-Pazifik (Norden)</dt>
  <dd>Eine neue Region ist in `ap-north` (Asien-Pazifik (Norden)) verfügbar. Sie können die neue Region verwenden, indem Sie den Domänennamen `jp.icr.io` verwenden.
  
  Weitere Informationen finden Sie unter [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions).</dd>
</dl>

## 21. Februar 2019
{: #21feb2019}

<dl>
  <dt>Zugriff auf eigene Namensbereiche automatisieren</dt>
  <dd>Die Verwendung von Tokens zur Automatisierung von Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre Namensbereiche ist veraltet. Sie müssen jetzt API-Schlüssel verwenden, um den Zugriff auf Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche zu automatisieren, um so Push- und Pull-Operationen für Images auszuführen.

  Weitere Informationen finden Sie in [Zugriff auf eigene Namensbereiche mithilfe von API-Schlüsseln automatisieren](/docs/services/Registry?topic=registry-registry_access#registry_api_key).</dd>
</dl>

## 8. Januar 2019
{: #8jan2019}

 <dl>
  <dt>Ende der Unterstützung für Vulnerability Advisor - API-Version 2</dt>
  <dd>Die API-Version 2 von Vulnerability Advisor ist veraltet und wird nicht mehr weiterentwickelt. Verwenden Sie die Version 3 der API, siehe [Vulnerability Advisor für {{site.data.keyword.registrylong_notm}}-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/container-registry/va).

  Weitere Informationen finden Sie in [Vulnerability Advisor - Version 2-API veraltet ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/).</dd>
</dl>

## 4. Oktober 2018
{: #4oct2018}

<dl>
  <dt>Benutzerzugriff verwalten</dt>
  <dd>Verwenden Sie {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM), um den Zugriff von Benutzern in Ihrem Konto auf {{site.data.keyword.registrylong_notm}} zu verwalten. Wenn IAM-Richtlinien für Ihr Konto in {{site.data.keyword.registrylong_notm}} aktiviert sind, muss jedem Benutzer, der auf den Service in Ihrem Konto zugreift, eine Zugriffsrichtlinie mit einer definierten IAM-Benutzerrolle zugewiesen werden. Diese Richtlinie bestimmt, welche Rolle der Benutzer im Kontext des Service hat, und welche Aktionen der Benutzer ausführen kann.

  Weitere Informationen finden Sie in [Benutzerzugriff mit {{site.data.keyword.iamshort}} verwalten](/docs/services/Registry?topic=registry-iam#iam), [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry?topic=registry-user#user) und [Lernprogramm: Zugriff auf IBM Cloud Container Registry-Ressourcen erteilen](/docs/services/Registry?topic=registry-iam_access#iam_access).</dd>
</dl>

## 7. August 2018
{: #7aug2018}

<dl>
  <dt>Verfügbare Freistellungsrichtlinien in Vulnerability Advisor</dt>
  <dd>Wenn Sie die Sicherheit einer {{site.data.keyword.cloud_notm}}-Organisation verwalten möchten, können Sie anhand Ihrer Richtlinieneinstellung feststellen, ob ein Problem freigestellt wurde. Sie können Container Image Security Enforcement verwenden, um sicherzustellen, dass die Bereitstellung nur für Images zulässig ist, die keine Sicherheitsprobleme enthalten, nachdem alle Probleme berücksichtigt wurden, die von Ihrer Richtlinie freigestellt sind.

  Weitere Informationen finden Sie in der Beschreibung der [Einstellung von Freistellungsrichtlinien für Organisationen](/docs/services/Registry?topic=va-va_index#va_managing_policy).</dd>
</dl>

## 25. Juli 2018
{: #25jul2018}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} verfügbar für Vulnerability Advisor</dt>
  <dd>Verwenden Sie den {{site.data.keyword.cloudaccesstrailfull_notm}}-Service, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.registrylong_notm}}-Service in {{site.data.keyword.cloud}} interagieren.

  Weitere Informationen finden Sie in [Activity Tracker-Ereignisse](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>
  
## 12. Juli 2018
{: #12jul2018}

<dl>
  <dt>Vulnerability Advisor - API-Version 3</dt>
  <dd>Version 3 der API ändert das Verhalten der API-Endpunkte, die zum Auflisten von Freistellungen verwendet werden. Stellen Sie sicher, dass die Verwendung Ihrer API nicht vom Verhalten von Version 2 abhängt.

  Weitere Informationen finden Sie in [Vulnerability Advisor für {{site.data.keyword.registrylong_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/container-registry/va).</dd>
</dl>

## 31. Mai 2018
{: #31may2018}

<dl>
  <dt>Helm für Passport Advantage-Images verwenden</dt>
  <dd>Importieren Sie {{site.data.keyword.IBM_notm}} Software, die von [IBM Passport Advantage Online für Kunden ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/pao_customer.html) heruntergeladen und für die Verwendung mit Helm paketiert wurde, in den {{site.data.keyword.registrylong_notm}}-Namensbereich.

  Weitere Informationen finden Sie in [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).</dd>
</dl>

## 21. März 2018
{: #21mar2018}

<dl>
  <dt>Container Scanner</dt>
  <dd>Mit Container Scanner kann Vulnerability Advisor alle Probleme melden, die beim Ausführen von Containern festgestellt wurden, die nicht im Basisimage des Containers enthalten sind.

  Weitere Informationen finden Sie in [Container Scanner installieren](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 16. März 2018
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement - Betaversion</dt>
  <dd>Mit der Betaversion von Container Image Security Enforcement können Sie Ihre Container-Images überprüfen, bevor Sie sie in Ihrem Cluster in {{site.data.keyword.containerlong_notm}} bereitstellen. Sie können steuern, von wo aus Images bereitgestellt werden, Vulnerability Advisor-Richtlinien durchsetzen und sicherstellen, dass [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) korrekt auf das Image angewendet wird.

  Weitere Informationen finden Sie in [Sicherheit des Container-Image durchsetzen](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 20. Februar 2018
{: #20feb2018}

<dl>
  <dt>Vertrauenswürdige Inhalte</dt>
  <dd>{{site.data.keyword.registrylong_notm}} bietet eine Technologie für vertrauenswürdige Inhalte, sodass Sie Images signieren können, um die Integrität von Images in Ihrem Registry-Namensbereich sicherzustellen. Durch Extrahieren von signierten Images mit Pull-Operation und ihre Übertragung mit Push-Operation können Sie sicherstellen, dass Ihre Images vom richtigen Teilnehmer, z. B. Ihren Tools für kontinuierliche Integration (Continuous Integration, CI), mit Push-Operation übertragen wurden.

  Weitere Informationen finden Sie in [Images für vertrauenswürdige Inhalte signieren](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

## 6. November 2017
{: #6nov2017}

<dl>
  <dt>Globale Registry</dt>
  <dd>Es ist eine globale Registry verfügbar. In deren Domänenname ist keine Region integriert (`icr.io`). Nur von IBM bereitgestellte öffentliche Images befinden sich in dieser Registry.

  Weitere Informationen finden Sie in [Globale Registry](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).</dd>
</dl>

## 29. September 2017
{: #29sep2017}

<dl>
  <dt>Docker-Images erstellen</dt>
  <dd>Der Befehl `ibmcloud cr build` kann jetzt zum Ausführen von Container-Builds verwendet werden. Sie können ein Docker-Image direkt in {{site.data.keyword.cloud_notm}} erstellen oder ein eigenes Docker-Image auf Ihrem lokalen Computer erstellen und es in Ihren Namensbereich in {{site.data.keyword.registrylong_notm}} hochladen (Push-Operation).

  Weitere Informationen finden Sie in [Docker-Images für die Verwendung mit dem eigenen Namensbereich erstellen](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) und [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).</dd>
</dl>

## 24. August 2017
{: #24aug2017}

<dl>
  <dt>Grafische Benutzerschnittstelle freigegeben</dt>
  <dd>Die grafische Benutzerschnittstelle von {{site.data.keyword.registrylong_notm}} ist im Katalog verfügbar (siehe [Container-Registry ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/kubernetes/catalog/registry)).</dd>
</dl>

## 27. Juni 2017
{: #27jun2017}

<dl>
  <dt>Allgemeine Verfügbarkeit von {{site.data.keyword.registrylong_notm}}</dt>
  <dd>{{site.data.keyword.registrylong_notm}} ist in der Regel als Service in {{site.data.keyword.cloud_notm}} verfügbar. {{site.data.keyword.registrylong_notm}} unterstützt {{site.data.keyword.containerlong_notm}}.

  Weitere Informationen zu {{site.data.keyword.containerlong_notm}} finden Sie in [Lernprogramm zur Einführung](/docs/containers?topic=containers-getting-started).</dd>
</dl>
