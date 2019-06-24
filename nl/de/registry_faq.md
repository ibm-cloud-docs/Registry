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

# Häufig gestellte Fragen (FAQs)
{: #registry_faq}

Häufig gestellte Fragen zu {{site.data.keyword.registrylong}}.
{: shortdesc}

## Wie liste ich öffentliche Images auf?
{: #faq_list_public_images}
{: faq}

Um öffentliche Images aufzulisten, können Sie die folgenden `ibmcloud`-Befehle ausführen, mit denen Sie die globale Registry als Ziel verwenden und die von IBM bereitgestellten öffentlichen Images auflisten können:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Kann ich Tools verwenden, die nicht von Docker bereitgestellt werden, um meine Images zu generieren und sie mit einer Push-Operation in der Registry zu speichern?
{: #faq_tools}
{: faq}

Ja, sofern diese Tools das OCI-Bildformat und das OCI-Protokoll unterstützen.

## Wie verwende ich die Zugriffssteuerung mit IAM?
{: #faq_access_control}
{: faq}

Sie können IAM-Richtlinien ({{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}) erstellen, um den Zugriff auf Ihre Namensbereiche in {{site.data.keyword.registrylong_notm}} zu steuern. Weitere Informationen finden Sie in [Lernprogramm: Zugriff auf {{site.data.keyword.registrylong_notm}}-Ressourcen erteilen](/docs/services/Registry?topic=registry-iam_access) und [Benutzerzugriff mit Identity and Access Management verwalten](/docs/services/Registry?topic=registry-iam).

## Welche Regionen sind für {{site.data.keyword.registrylong_notm}} verfügbar?
{: #faq_regions}
{: faq}

Images können in [lokalen Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local) gehostet werden. Von IBM gehostete öffentliche Images sind in der [Globalen Registry](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global) verfügbar. 

## Warum wird für ein neu hinzugefügtes Image eine Fehlernachricht bezüglich eines nicht gefundenen Scans ausgegeben?
{: #faq_va_new_scan_error}
{: faq}

Wenn unmittelbar nach dem Hinzufügen des Images zur Registry der Sicherheitslückenbericht abgerufen wird, wird möglicherweise die folgende Fehlernachricht ausgegeben: 

```
BXNVA0009E:  <Imagename> wurde nicht gescannt. Wiederholen Sie den Vorgang zu einem späteren Zeitpunkt.
Wenn dieses Problem weiterhin auftritt, wenden Sie sich an den Support:
https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

Sie erhalten diese Nachricht, da das Scannen der Images asynchron zu den Ergebnisabfragen verläuft und der Scanvorgang einige Zeit in Anspruch nimmt. Während des normalen Betriebs wird der Scan innerhalb der ersten Minuten nach dem Hinzufügen des Images zur Registry abgeschlossen, wobei die Imagegröße und die Menge des Datenverkehrs in der Registry eine Rolle spielen. 

Wenn diese Nachricht als Teil einer Build-Pipeline ausgegeben wird und dies regelmäßig der Fall ist, fügen Sie Wiederholungslogik hinzu, die eine kurze Pause enthält. 

Ist die Leistung weiterhin nicht akzeptabel, wenden Sie sich an den Support. Weitere Informationen finden Sie in [Unterstützung für {{site.data.keyword.registrylong_notm}} anfordern](/docs/services/Registry?topic=registry-ts_index#gettinghelp). 

## Wie wird ein Vulnerability Advisor-Scan ausgelöst?
{: #faq_va_trigger_scan}
{: faq}

Das Scannen eines Image wird in den folgenden Fällen ausgelöst: 

- Wenn ein neues Image mit einer Push-Operation in die Registry übertragen wird. 
- Wenn das Image über einen Zeitraum von 7 Tagen nicht gescannt wurde, wird es in die Warteschlange für das erneute Scannen gestellt. Dies kann einige Zeit in Anspruch nehmen. 
- Wenn für ein innerhalb des Images installiertes Paket ein neuer Sicherheitshinweis veröffentlicht wird, wird das Image in die Warteschlange für das erneute Scannen gestellt. Dies kann einige Zeit in Anspruch nehmen. Erneute Scans, die durch die Veröffentlichung neuer Sicherheitshinweise ausgelöst werden, stehen nur für Ubuntu- und Debian-Images zur Verfügung. 

## Wie häufig werden die Sicherheitshinweise aktualisiert?
{: #faq_va_update_security_notice}
{: faq}

Sicherheitshinweise für Vulnerability Advisor werden etwa alle 12 Stunden von den Betriebssystemsites der Anbieter hochgeladen. 
