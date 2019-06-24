---

copyright:
  years: 2019
lastupdated: "2019-05-17"

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

In diesen Releaseinformationen erfahren Sie mehr über die neuesten Änderungen bei {{site.data.keyword.registrylong}} und Vulnerability Advisor. Die Änderungen sind nach Datum gruppiert.
{:shortdesc}

## 13. Mai 2019
{: #13may2019}

- **Ende der Unterstützung für Container Scanner**

  Container Scanner ist nun veraltet und kann nicht mehr verwendet werden. 

  Weitere Informationen finden Sie in [Container Scanner installieren (veraltet)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).

## 2. April 2019
{: #2apr2019}

- **Allgemeine Verfügbarkeit von Container Image Security Enforcement**

  Mit Container Image Security Enforcement können Sie Ihre Container-Images überprüfen, bevor Sie sie in Ihrem Cluster in {{site.data.keyword.containerlong_notm}} bereitstellen. Sie können steuern, von wo aus Images bereitgestellt werden, Vulnerability Advisor-Richtlinien durchsetzen und sicherstellen, dass [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) korrekt auf das Image angewendet wird.

  Weitere Informationen finden Sie in [Sicherheit des Container-Image durchsetzen](/docs/services/Registry?topic=registry-security_enforce#security_enforce).

## 14. März 2019
{: #14mar2019}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} verfügbar für {{site.data.keyword.registrylong_notm}}**

  Verwenden Sie den {{site.data.keyword.cloudaccesstraillong_notm}}-Service, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.registrylong_notm}}-Service in {{site.data.keyword.cloud}} interagieren.

  Weitere Informationen finden Sie in [Activity Tracker-Ereignisse](/docs/services/Registry?topic=registry-at_events#at_events).

## 25. Februar 2019
{: #25feb2019}

- **Neue DNS-Namen**

  {{site.data.keyword.registrylong_notm}} übernimmt neue Domänennamen. Die neuen Domänennamen sind in der Konsole und in der CLI verfügbar. Sie können jetzt die neuen `icr.io`-Domänennamen verwenden. Die bereits vorhandenen Domänennamen des Typs `registry.bluemix.net` sind zwar veraltet, doch Sie können sie noch nutzen; ein Datum, an dem die Unterstützung endet, wird zu einem späteren Zeitpunkt bekannt gegeben. Weitere Informationen finden Sie in [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions) und [Einführung neuer IBM Cloud Container Registry-Domänennamen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  Wenn Sie Content Trust verwenden, müssen Sie neue Signaturen hinzufügen, damit Sie Content Trust unter dem neuen Domänennamen verwenden können, da Signaturen für den gesamten Imagenamen einschließlich des Domänennamens gelten. Weitere Informationen zu Content Trust finden Sie unter [Images für vertrauenswürdige Inhalte signieren](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).

- **Geheime Schlüssel für {{site.data.keyword.containerlong_notm}}-Clusters mit einem IAM-API-Schlüssel mittels Push-Operation extrahieren**

  Das Extrahieren geheimer Schlüssel für Cluster mittels Push-Operation für die `icr.io`-Domänen werden mithilfe eines IAM-API-Schlüssels autorisiert. Wenn Sie also mehr Kontrolle über den Zugriff auf Ihre {{site.data.keyword.registrylong_notm}}-Ressourcen benötigen, können Sie IAM-Richtlinien hinzufügen. Beispielsweise können Sie die API-Schlüsselrichtlinien im extrahierten geheimen Schlüssel des Clusters so ändern, dass Images nur aus einer bestimmten Registry-Region oder aus einem bestimmten Namensbereich abgerufen werden.
  
  Weitere Informationen finden Sie in der Beschreibung der [Vorgehensweise, wie Ihr Cluster autorisiert wird, um Images von {{site.data.keyword.registrylong_notm}} mittels Pull-Operation zu extrahieren](/docs/containers?topic=containers-images#cluster_registry_auth).

- **Neue Region in Asien-Pazifik (Norden)**

  Eine neue Region ist in `ap-north` (Asien-Pazifik (Norden)) verfügbar. Sie können die neue Region verwenden, indem Sie den Domänennamen `jp.icr.io` verwenden.
  
  Weitere Informationen finden Sie unter [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## 21. Februar 2019
{: #21feb2019}

- **Zugriff auf eigene Namensbereiche automatisieren**

  Die Verwendung von Tokens zur Automatisierung von Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre Namensbereiche ist veraltet. Sie müssen jetzt API-Schlüssel verwenden, um den Zugriff auf Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche zu automatisieren, um so Push- und Pull-Operationen für Images auszuführen.

  Weitere Informationen finden Sie in [Zugriff auf eigene Namensbereiche mithilfe von API-Schlüsseln automatisieren](/docs/services/Registry?topic=registry-registry_access#registry_api_key).

## 8. Januar 2019
{: #8jan2019}

- **Ende der Unterstützung für Vulnerability Advisor - API-Version 2**

  Die API-Version 2 von Vulnerability Advisor ist veraltet und wird nicht mehr weiterentwickelt. Verwenden Sie die Version 3 der API, siehe [Vulnerability Advisor für {{site.data.keyword.registrylong_notm}}-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/container-registry/va).

  Weitere Informationen finden Sie in [Vulnerability Advisor - Version 2-API veraltet ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/12/vulnerability-advisor-v2-api-deprecation/).

## 4. Oktober 2018
{: #4oct2018}

- **Benutzerzugriff verwalten**

  Verwenden Sie {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM), um den Zugriff von Benutzern in Ihrem Konto auf {{site.data.keyword.registrylong_notm}} zu verwalten. Wenn IAM-Richtlinien für Ihr Konto in {{site.data.keyword.registrylong_notm}} aktiviert sind, muss jedem Benutzer, der auf den {{site.data.keyword.registrylong_notm}}-Service in Ihrem Konto zugreift, eine Zugriffsrichtlinie mit einer definierten IAM-Benutzerrolle zugewiesen werden. Diese Richtlinie bestimmt, welche Rolle der Benutzer im Kontext des Service hat, und welche Aktionen der Benutzer ausführen kann.

  Weitere Informationen finden Sie in [Benutzerzugriff mit {{site.data.keyword.iamshort}} verwalten](/docs/services/Registry?topic=registry-iam#iam), [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry?topic=registry-user#user) und [Lernprogramm: Zugriff auf IBM Cloud Container Registry-Ressourcen erteilen](/docs/services/Registry?topic=registry-iam_access#iam_access).

## 7. August 2018
{: #7aug2018}

- **Verfügbare Freistellungsrichtlinien in Vulnerability Advisor**

  Wenn Sie die Sicherheit einer {{site.data.keyword.cloud_notm}}-Organisation verwalten möchten, können Sie anhand Ihrer Richtlinieneinstellung feststellen, ob ein Problem freigestellt wurde. Sie können die Durchsetzung der Container-Image-Sicherheit verwenden, um sicherzustellen, dass die Bereitstellung nur für Images zulässig ist, die keine Sicherheitsprobleme enthalten, nachdem alle Probleme berücksichtigt wurden, die von Ihrer Richtlinie freigestellt sind.

  Weitere Informationen finden Sie in der Beschreibung der [Einstellung von Freistellungsrichtlinien für Organisationen](/docs/services/Registry?topic=va-va_index#va_managing_policy).

## 25. Juli 2018
{: #25jul2018}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} verfügbar für Vulnerability Advisor**

  Verwenden Sie den {{site.data.keyword.cloudaccesstrailfull_notm}}-Service, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.registrylong_notm}}-Service in {{site.data.keyword.cloud}} interagieren.

  Weitere Informationen finden Sie in [Activity Tracker-Ereignisse](/docs/services/Registry?topic=registry-at_events#at_events).
  
## 12. Juli 2018
{: #12jul2018}

- **Vulnerability Advisor - API-Version 3**

  Version 3 der API ändert das Verhalten der API-Endpunkte, die zum Auflisten von Freistellungen verwendet werden. Prüfen Sie, dass die Verwendung Ihrer API nicht vom Verhalten von Version 2 abhängt.

  Weitere Informationen finden Sie in [Vulnerability Advisor für {{site.data.keyword.registrylong_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/container-registry/va).

## 31. Mai 2018
{: #31may2018}

- **Helm für Passport Advantage-Images verwenden**

  Importieren Sie {{site.data.keyword.IBM_notm}} Software, die von [IBM Passport Advantage Online für Kunden ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/pao_customer.html) heruntergeladen und für die Verwendung mit Helm paketiert wurde, in den {{site.data.keyword.registrylong_notm}}-Namensbereich.

  Weitere Informationen finden Sie in [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).

## 21. März 2018
{: #21mar2018}

- **Container Scanner**

  Mit Container Scanner kann Vulnerability Advisor alle Probleme melden, die beim Ausführen von Containern festgestellt wurden, die nicht im Basisimage des Containers enthalten sind.

  Weitere Informationen finden Sie in [Container Scanner installieren](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).

## 16. März 2018
{: #16mar2018}

- **Container Image Security Enforcement - Betaversion**

  Mit der Betaversion von Container Image Security Enforcement können Sie Ihre Container-Images überprüfen, bevor Sie sie in Ihrem Cluster in {{site.data.keyword.containerlong_notm}} bereitstellen. Sie können steuern, von wo aus Images bereitgestellt werden, Vulnerability Advisor-Richtlinien durchsetzen und sicherstellen, dass [content trust](/docs/services/Registry?topic=registry-registry_trustedcontent) korrekt auf das Image angewendet wird.

  Weitere Informationen finden Sie in [Sicherheit des Container-Image durchsetzen](/docs/services/Registry?topic=registry-security_enforce#security_enforce).

## 20. Februar 2018
{: #20feb2018}

- **Vertrauenswürdige Inhalte**

  {{site.data.keyword.registrylong_notm}} bietet eine Technologie für vertrauenswürdige Inhalte, sodass Sie Images signieren können, um die Integrität von Images in Ihrem Registry-Namensbereich sicherzustellen. Durch Extrahieren von signierten Images mit Pull-Operation und ihre Übertragung mit Push-Operation können Sie sicherstellen, dass Ihre Images vom richtigen Teilnehmer, z. B. Ihren Tools für kontinuierliche Integration (Continuous Integration, CI), mit Push-Operation übertragen wurden.

  Weitere Informationen finden Sie in [Images für vertrauenswürdige Inhalte signieren](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).

## 6. November 2017
{: #6nov2017}

- **Globale Registry**

  Es ist eine globale Registry ist verfügbar; in deren Name ist keine Region integriert (`icr.io`). Nur von IBM bereitgestellte öffentliche Images befinden sich in dieser Registry.

  Weitere Informationen finden Sie in [Globale Registry](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## 29. September 2017
{: #29sep2017}

- **Docker-Images erstellen**

  Der Befehl `ibmcloud cr build` kann jetzt zum Ausführen von Container-Builds verwendet werden. Sie können ein Docker-Image direkt in {{site.data.keyword.cloud_notm}} erstellen oder ein eigenes Docker-Image auf Ihrem lokalen Computer erstellen und es in Ihren Namensbereich in {{site.data.keyword.registrylong_notm}} hochladen (Push-Operation).

  Weitere Informationen finden Sie in [Docker-Images für die Verwendung mit dem eigenen Namensbereich erstellen](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) und [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).

## 24. August 2017
{: #24aug2017}

- **Grafische Benutzerschnittstelle freigegeben**

  Die grafische Benutzerschnittstelle von {{site.data.keyword.registrylong_notm}} ist im Katalog verfügbar, siehe [Container-Registry ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/kubernetes/catalog/registry).

## 27. Juni 2017
{: #27jun2017}

- **Allgemeine Verfügbarkeit von {{site.data.keyword.registrylong_notm}}**

  {{site.data.keyword.registrylong_notm}} ist in der Regel als Service in {{site.data.keyword.cloud_notm}} verfügbar. {{site.data.keyword.registrylong_notm}} unterstützt {{site.data.keyword.containerlong_notm}}.

  Weitere Informationen zu {{site.data.keyword.containerlong_notm}} finden Sie in [Lernprogramm zur Einführung](/docs/containers?topic=containers-getting-started).
