---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Informationen zu {{site.data.keyword.registrylong_notm}}
{: #registry_overview}

Verwenden Sie {{site.data.keyword.registrylong}}, um Docker-Images in einer hoch verfügbaren und skalierbaren Architektur sicher zu speichern und auf sie zuzugreifen.
{:shortdesc}

{{site.data.keyword.registrylong_notm}} bietet eine hoch verfügbare, skalierbare private Multi-Tenant-Registry für Images, die von IBM gehostet und verwaltet wird. Sie können die private Registry verwenden, indem Sie Ihren eigenen Image-Namensbereich einrichten und Docker-Images mit Push-Operation an Ihren Namensbereich übertragen.

Jeder von Ihnen erstellte Container basiert auf einem Docker-Image. Ein Image wird aus einer Dockerfile erstellt, die Anweisungen zum Erstellen des Images enthält. Eine Dockerfile kann in ihren Anweisungen Buildartefakte referenzieren, die separat gespeichert sind (z. B. eine App, die Konfiguration der App und die Abhängigkeiten der App). Images werden normalerweise in einer Registry gespeichert, die entweder öffentlich zugänglich ist (öffentliche Registry) oder mit einem eingeschränkten Zugriff für eine begrenzte Gruppe von Benutzern konfiguriert wird (private Registry). Wenn Sie {{site.data.keyword.registrylong_notm}} verwenden, können ausschließlich Benutzer mit Zugriff auf Ihr {{site.data.keyword.Bluemix_notm}}-Konto auf Ihre Images zugreifen.

Wenn Sie Images mit einer Push-Operation an {{site.data.keyword.registrylong_notm}} übertragen, profitieren Sie von den integrierten Vulnerability Advisor-Funktionen, die nach potenziellen Sicherheitsproblemen und Schwachstellen suchen. Vulnerability Advisor prüft auf gefährdete Pakete in bestimmten Basis-Docker-Images und bekannte Sicherheitslücken in App-Einstellungen. Werden Sicherheitslücken gefunden, so werden Informationen zu der Sicherheitslücke bereitgestellt. Sie können diese Informationen verwenden, um Sicherheitsprobleme zu beheben, sodass Container nicht über gefährdete Images bereitgestellt werden.

Die folgende Tabelle gibt eine Übersicht über den Nutzen der Verwendung von {{site.data.keyword.registrylong_notm}}.

|Nutzen|Beschreibung|
|-------|-----------|
|Hoch verfügbare und skalierbare private Registry|<ul><li>Einrichtung eines eigenen Image-Namensbereichs in einer hoch verfügbaren, skalierbaren privaten Multi-Tenant-Registry, die von IBM gehostet und verwaltet wird</li><li>Sicheres Speichern Ihrer privaten Docker-Images und deren gemeinsame Nutzung mit Benutzern in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto</li></ul>|
|Einhaltung von Sicherheitsbestimmungen für Images mit Vulnerability Advisor|<ul><li>Vorteil des automatischen Scannens von Images in Ihrem Namensbereich</li><li>Überprüfen von Betriebssystem-spezifischen Empfehlungen, um potenzielle Sicherheitslücken zu beheben und Ihre Container vor Schäden zu schützen</li></ul>|
|Kontingente für Speicher und Pull-Datenverkehr|<ul><li>Vorteil von kostenlosem Speicherplatz und Pull-Datenverkehr zu Ihren privaten Images bis zur Obergrenze des kostenlosen Kontingents</li><li>Festlegen angepasster Kontingente für Speicher und Pull-Datenverkehr pro Monat, um ein Überziehen Ihres bevorzugten Zahlungsbetrags zu vermeiden</li></ul>|
{: caption="Tabelle 1. Nutzen von {{site.data.keyword.registrylong_notm}}" caption-side="top"}


## Servicepläne
{: #registry_plans}

Sie können zwischen einem kostenlosen Serviceplan und einem Standardserviceplan von {{site.data.keyword.registrylong_notm}} wählen, um Ihre Docker-Images zu speichern und für Benutzer in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto zur Verfügung zu stellen.{:shortdesc}

Der Serviceplan von {{site.data.keyword.registrylong_notm}} legt die Speicherkapazität und den Umfang des Pull-Datenverkehrs fest, die/den Sie für Ihre privaten Images verwenden können. Der Serviceplan ist Ihrem {{site.data.keyword.Bluemix_notm}}-Konto zugeordnet. Die Begrenzungen für den Speicher und den Pull-Datenverkehr für Images gelten für alle Namensbereiche, die Sie in Ihrem Konto einrichten.

In der folgenden Tabelle sind die verfügbaren Servicepläne von {{site.data.keyword.registrylong_notm}} und deren Merkmale aufgeführt. Weitere Informationen zur Funktionsweise der Abrechnung und zu den Folgen einer Überschreitung von Serviceplangrenzwerten finden Sie im Abschnitt [Kontingente und Abrechnung in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).

|Merkmale|Kostenlos|Standard|
|---------------|----|--------|
|Beschreibung|Bei diesem Serviceplan können Sie die private Registry in {{site.data.keyword.registrylong_notm}} ausprobieren, um Ihre Docker-Images sicher zu speichern und gemeinsam zu nutzen. Dieser Plan ist der Standardserviceplan, wenn Sie Ihren ersten Namensbereich in {{site.data.keyword.registrylong_notm}} einrichten.|Bei diesem Serviceplan profitieren Sie von einer unbegrenzten Speichernutzung und einem unbegrenzten Pull-Datenverkehr bei der Verwaltung der Docker-Images für alle Namensbereiche in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto.|
|Speicherkapazität für Images|500 MB|Unbegrenzt|
|Pull-Datenverkehr|5 GB pro Monat|Unbegrenzt|
|Abrechnung|Falls Sie die Grenzwerte für den Speicher oder den Pull-Datenverkehr überschreiten, können Sie keine Push- oder Pull-Operationen für Images in Bezug auf Ihren Namensbereich ausführen. Weitere Informationen finden Sie im Abschnitt [Kontingente und Abrechnung in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).|<ul><li>Speicher: Die Abrechnung erfolgt auf der Grundlage der Nutzung von GB-Monaten. Die ersten 0,5 GB-Monate sind kostenfrei. Anschließend erfolgt die Abrechnung gemäß der Festlegung im Preisrechner.</li><li>Pull-Datenverkehr: Die Abrechnung erfolgt auf der Grundlage der Nutzung in GB pro Monat. Die ersten 5 GB sind kostenlos. Anschließend erfolgt die Abrechnung gemäß der Festlegung im Preisrechner. Falls Sie die Grenzwerte für den Speicher oder den Pull-Datenverkehr überschreiten, können Sie keine Push- oder Pulloperationen für Images in Bezug auf Ihren Namensbereich ausführen. Weitere Informationen zum Speicher, zu Pull-Datenverkehr und zum Preisrechner finden Sie im Abschnitt [Kontingente und Abrechnung in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).</li></ul>|
{: caption="Tabelle 2. Pläne in {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Kontingente und Abrechnung
{: #registry_plan_billing}

Hier finden Sie Informationen und Beispiele zur Funktionsweise der Abrechnung und der Kontingente in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Jedes Image ist aus einer Anzahl von Ebenen aufgebaut, von der jede eine inkrementelle Änderung ausgehend vom Basisimage darstellt. Wenn Sie eine Push- oder Pull-Operation für ein Image durchführen, wird der für jede Ebene benötigte Speicher und Pull-Datenverkehr auf Ihre monatliche Nutzung angerechnet. Identische Ebenen werden automatisch von den Images in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto gemeinsam genutzt und bei der Erstellung weiterer Images wiederverwendet. Der Speicher für jede identische Ebene wird nur einmal berechnet, unabhängig davon, wie viele Images in Ihrem Konto auf die Ebene verweisen.

Beispiel für Push-Operationen an Images:

> Sie führen eine Push-Operation für ein Image in Ihren Namensbereich durch, das auf dem Ubuntu-Image basiert. Das Ubuntu-Image enthält mehrere Ebenen. Da Sie diese Ebenen noch nicht in Ihrem Konto haben, wird der Speicher, den diese Ebenen erfordern, auf Ihre monatliche Nutzung angerechnet.
>
> Zu einem späteren Zeitpunkt erstellen Sie ein zweites Image, das auf dem Ubuntu-Image basiert. Sie nehmen Änderungen am Ubuntu-Basisimage vor, beispielsweise durch Hinzufügen zusätzlicher Befehle oder Dateien zu Ihrer Dockerfile. Jede Änderung stellt eine neue Image-Ebene dar. Wenn Sie das zweite Image mit Push-Operation übertragen, erkennt {{site.data.keyword.registrylong_notm}}, dass alle Ebenen des Basis-Ubuntu-Image bereits in Ihrem Konto gespeichert wurden. Das Speichern dieser Ebenen wird Ihnen kein zweites Mal in Rechnung gestellt, selbst wenn Sie Ihr Image mit Push-Operation in einen anderen Namensbereich übertragen haben. {{site.data.keyword.registrylong_notm}} bestimmt die Größe aller neuer Ebenen und rechnet den Speicher auf Ihre monatliche Nutzung an.

### Abrechnung für Speicher und Pull-Datenverkehr
{: #registry_billing_traffic}

Je nach dem Serviceplan, den Sie auswählen, wird Ihnen der monatlich genutzte Speicher und Pull-Datenverkehr in Rechnung gestellt.
{:shortdesc}

**Speicher: **

  Jeder {{site.data.keyword.registrylong_notm}}-Serviceplan beinhaltet ein bestimmtes Speicherkontingent, das Sie nutzen können, um Ihre Docker-Images sicher in den Namensbereichen Ihres {{site.data.keyword.Bluemix_notm}}-Kontos zu speichern. Wenn Sie den Standardplan verwenden, wird nach Nutzung pro GB-Monat abgerechnet. Die ersten 0,5 GB-Monate sind kostenfrei. Wenn Sie den kostenlosen Plan verwenden, können Sie Ihre Images kostenlos in {{site.data.keyword.registrylong_notm}} speichern, bis das Kontingent für den kostenlosen Plan erreicht ist. Ein GB-Monat ist der Durchschnittswert von 1 GB Speicher für einen Monat (730 Stunden).

  Beispiel für den Standardplan:

  > Sie nutzen 5 GB für genau die Hälfte des Monats, dann übertragen Sie einige Images per Push-Operation an Ihren Namensbereich und nutzen 10 GB für den Rest des Monats. Ihre monatliche Nutzung wird wie folgt berechnet:
  >
  > (5 GB x 0,5 (Monate)) + (10 GB x 0,5 (Monate)) = 2,5 + 5 = 7,5 GB-Monate
  >
  > Im Standardplan sind die ersten 0,5 GB-Monate kostenfrei, d. h., es werden 7 GB-Monate (7,5 GB-Monate - 0,5 GB-Monate) berechnet.

  

**Pull-Datenverkehr:**

  Jeder {{site.data.keyword.registrylong_notm}}-Serviceplan beinhaltet ein bestimmtes Kontingent an kostenlosem Pull-Datenverkehr zu Ihren privaten Images, die in Ihrem Namensbereich gespeichert sind. Pull-Datenverkehr ist die Bandbreite, die Sie verwenden, wenn Sie eine Ebene eines Image aus Ihrem Namensbereich mit Pull-Operation an Ihre lokale Maschine übertragen. Wenn Sie den Standardplan verwenden, wird nach Nutzung pro Monat in GB abgerechnet. Die ersten 5 GB jeden Monat sind kostenlos. Wenn Sie den kostenlosen Plan verwenden, können Sie Ihre Images mit Pull-Operation aus Ihrem Namensbereich übertragen, bis Sie das Kontingent für den kostenlosen Plan ausgeschöpft haben.

  Beispiel für den Standardplan:

  > In einem Monat haben Sie Images mit Ebenen von 14 GB Gesamtgröße extrahiert. Ihre monatliche Nutzung wird wie folgt berechnet:
  >
  > Im Standardplan sind die ersten 5 GB pro Monat kostenlos, sodass Ihnen 9 GB (14 GB - 5 GB) berechnet werden.

  

### Kontingente für Speicher und Pull-Datenverkehr
{: #registry_quota_limits}

Je nach dem Serviceplan, die Sie auswählen, können Sie Images mit Push-und Pull-Operationen in und aus Ihrem Namensbereich übertragen, bis Ihr planspezifisches oder angepasstes Kontingent erreicht ist.
{:shortdesc}

**Speicher: **

  Wenn Sie das Kontingent für Ihren Plan erreichen oder überschreiten, können Sie keine Images mehr mit Push-Operation in die Namensbereiche Ihres {{site.data.keyword.Bluemix_notm}}-Kontos übertragen, bis Sie entweder [Speicherplatz freigeben durch Entfernen von Images](registry_quota.html#registry_quota_freeup) aus Ihrem Namensbereich oder ein [Upgrade auf den Standard-Plan durchführen](#registry_plan_upgrade). Wenn Sie Kontingente für den Speicher in Ihrem kostenlosen oder Standardplan festlegen, können Sie auch [dieses Kontingent erhöhen](registry_quota.html#registry_quota_set), um Push-Operationen zu den neuen Images wieder zu ermöglichen.

  Beispiel für den Standardplan:

  > Ihr aktuelles Speicherkontingent ist auf 1 GB festgelegt. Alle privaten Images zusammen, die in den Namensbereichen Ihres {{site.data.keyword.Bluemix_notm}}-Kontos gespeichert sind, belegen bereits 900 MB dieses Speicherplatzes. Es stehen Ihnen 100 MB Speicherplatz zur Verfügung, bis Sie Ihr Kontingent ausgeschöpft haben. Ein Benutzer möchte ein Image mit einer Größe von 2 GB auf der lokalen Maschine mit Push-Operation übertragen. Da das Kontingentgrenze noch nicht erreicht ist, lässt {{site.data.keyword.registrylong_notm}} zu, dass der Benutzer dieses Image mit einer Push-Operation überträgt.
  >
  > Nach der Push-Operation bestimmt {{site.data.keyword.registrylong_notm}} die tatsächliche Größe des Image in Ihrem Namensbereich, die je nach Größe auf Ihrer lokalen Maschine variieren kann, und prüft, ob der Grenzwert für den Speicher erreicht ist. In diesem Beispiel erhöht sich die Speicherbelegung von 900 MB um 2 GB. Ist das aktuelle Kontingent auf 1 GB gesetzt, verhindert {{site.data.keyword.registrylong_notm}} die Push-Operation in den Namensbereich für weitere Images.

**Pull-Datenverkehr:**

  Wenn Sie das Kontingent für Ihren Plan erreichen oder überschreiten, können Sie keine Images mehr mit Pull-Operation aus den Namensbereichen in Ihr {{site.data.keyword.Bluemix_notm}}-Konto übertragen, bis entweder der nächste Abrechnungszeitraum beginnt, Sie ein [Upgrade auf den Standardplan durchführen](#registry_plan_upgrade) oder Sie Ihr [Kontingent für Pull-Datenverkehr erhöhen](registry_quota.html#registry_quota_set).

  Beispiel für den Standardplan:

  > In einem Monat ist Ihr Kontingent für Pull-Datenverkehr auf 5 GB festgelegt. Sie haben bereits Images mit Pull-Operation aus Ihren Namensbereichen übertragen und 4,5 GB dieses Pull-Datenverkehrs genutzt. Es stehen Ihnen 0,5 GB für den Pull-Datenverkehr zur Verfügung, bis das Kontingent ausgeschöpft ist. Ein Benutzer möchte ein Image aus Ihrem Namensbereich mit einer Größe von 1 GB mit Pull-Operation übertragen. Da die Kontingentgrenze noch nicht erreicht ist, lässt {{site.data.keyword.registrylong_notm}} zu, dass der Benutzer dieses Image mit einer Pull-Operation überträgt.
  >
  > Nachdem das Image mit Pull-Operation übertragen wurde, bestimmt {{site.data.keyword.registrylong_notm}} die Bandbreite, die Sie während der Pull-Operation verwendet haben, und prüft, ob der Grenzwert für den Pull-Datenverkehr erreicht ist. In diesem Beispiel erhöht sich der Pull-Datenverkehr von 4,5 GB auf 5,2 GB. Ist das aktuelle Kontingent auf 5 GB gesetzt, verhindert {{site.data.keyword.registrylong_notm}} die Pull-Operation aus Ihrem Namensbereich für weitere Images.

### Kosten schätzen
{: #registry_estimating_costs}

Verwenden Sie den {{site.data.keyword.Bluemix_notm}}-Preisrechner, um die Kosten für Ihren Plan zu schätzen.
{:shortdesc}

Sie können Ihre App mithilfe der Kostenberechnungsfunktionen, die von {{site.data.keyword.Bluemix_notm}} bereitgestellt wird, berechnen.

1.  Öffnen Sie die Preisliste im Abschnitt [{{site.data.keyword.Bluemix_notm}}-Preisstruktur](https://www.ibm.com/cloud-computing/bluemix/pricing).
2.  Im Abschnitt **Nutzungsabhängige Zahlung** klicken Sie auf **Kosten mit dem Preisrechner schätzen**. Der Preisrechner wird geöffnet.
3.  Blättern Sie zum Unterabschnitt **Container-Registry** im Abschnitt **Containergebühren**.
4.  Geben Sie die geschätzten Kosten für Speicher und Datenverkehr in die angezeigten Felder ein.

Ihre geschätzten Kosten werden im Preisrechner angezeigt.

## Upgrade für den Serviceplan durchführen
{: #registry_plan_upgrade}

Sie können ein Upgrade für Ihren Serviceplan durchführen, um von unbegrenztem Speicher und Pull-Datenverkehr zu profitieren und die Docker-Images für alle Namensbereiche in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto zu verwalten.
{:shortdesc}

Wenn Sie herausfinden möchten, welchen Serviceplan Sie verwenden, führen Sie den Befehl `bx cr plan` aus.

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    bx login
    ```
    {: pre}

    **Hinweis**: Wenn Sie über eine eingebundene ID verfügen, verwenden Sie `bx login --sso` zum Anmelden bei der {{site.data.keyword.Bluemix_notm}}-CLI. Geben Sie Ihren Benutzernamen ein und verwenden Sie die bereitgestellte URL in der CLI-Ausgabe zum Abrufen Ihres einmaligen Kenncodes. Sie erkennen, ob Sie über eine eingebundene ID verfügen, wenn die Anmeldung ohne die Option `--sso` fehlschlägt und mit der Option `--sso` erfolgreich ist.

2.  Führen Sie ein Upgrade auf den Standardplan durch.

    ```
    bx cr plan-upgrade standard
    ```
    {: pre}

    **Hinweis:** Wenn Sie über ein {{site.data.keyword.Bluemix_notm}}-Testkonto verfügen, müssen Sie zuerst ein Upgrade auf ein {{site.data.keyword.Bluemix_notm}}-Standardkonto durchführen, bevor Sie den Befehl `bx cr plan-upgrade` ausführen.


## Zentrale Aspekte
{: #registry_planning}

Bereiten Sie die sichere Speicherung und gemeinsame Nutzung Ihrer Docker-Images mit {{site.data.keyword.registrylong_notm}} vor, indem Sie sich mit grundlegenden Registry-Informationen vertraut machen.
{:shortdesc}

### Erläuterung zu den in {{site.data.keyword.registrylong_notm}} verwendeten Begriffen
{: #terms}


<dl>
  <dt>Registry</dt>
  <dd>Eine Registry ist ein Service, der die Infrastruktur zur Speicherung von Docker-Images bereitstellt und auf den mithilfe der Registry-Host-URL und eines optionalen Ports zugegriffen werden kann. Registrys sind entweder öffentlich zugänglich (öffentliche Registry) oder werden mit einem eingeschränkten Zugriff für eine begrenzte Gruppe von Benutzern konfiguriert (private Registry).{{site.data.keyword.registrylong_notm}} bietet eine hoch verfügbare private Multi-Tenant-Registry für Images, die von IBM gehostet und verwaltet wird. Sie können die private Registry verwenden, indem Sie Ihren eigenen Image-Namensbereich einrichten und damit beginnen, Docker-Images mit Push-Operation an Ihren Namensbereich zu übertragen.</dd>
</dl>

<dl>
  <dt>Namensbereich</dt>
  <dd>Namensbereiche sind eine Möglichkeit, Repositorys Ihrer Images innerhalb {{site.data.keyword.registrylong_notm}} zu organisieren. Der Namensbereich wird Ihrem {{site.data.keyword.Bluemix_notm}}-Konto zugeordnet. Wenn Sie in {{site.data.keyword.registrylong_notm}} einen eigenen Namensbereich einrichten, wird der Namensbereich wie folgt an die Registry-URL angehängt: <code>registry.<em>&lt;region&gt;</em>.bluemix.net/eigener_namensbereich</code>.

  Jeder Benutzer in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto kann Images, die in Ihrem Registry-Namensbereich gespeichert sind, anzeigen und mit ihnen arbeiten. Wenn Sie separate Repositorys verwenden möchten (beispielsweise für Ihre Produktions- und Ihre Staging-Umgebungen), können Sie mehrere Namensbereiche einrichten.</dd>
</dl>

<dl>
  <dt>Repository</dt>
  <dd>Ein Image-Repository ist eine Sammlung von zugehörigen, mit Tags versehenen Images im Registry. Repository wird oft synonym für Image verwendet. Ein Repository enthält jedoch potenziell mehrere mit Tags versehene Varianten eines Images. </dd>
</dl>

<dl>
  <dt>Image</dt>
  <dd>Ein Docker-Image wird, basierend auf den Anweisungen, die in der Dockerfile angegeben sind, erstellt und stellt die Basis eines Containers dar. Nachdem das Docker-Image erstellt ist, können Sie es für die Erstellung eines Containers zur Bereitstellung Ihrer App und deren Abhängigkeiten verwenden. Images werden in einer Registry gespeichert. Benutzer mit Zugriff auf Ihr {{site.data.keyword.Bluemix_notm}}-Konto können auf Ihre Images zugreifen.</dd>
</dl>

<dl>
  <dt>Tag</dt>
  <dd>Bei einem Tag handelt es sich um eine Kennung für ein Image innerhalb eines Repositorys. Sie können Tags verwenden, um verschiedene Versionen desselben Basisimage innerhalb eines Repositorys zu unterscheiden. Wenn Sie einen Docker-Befehl ausführen und den Tag eines Repository-Image nicht angeben, wird das Image, das mit dem Tag <code>latest</code> versehen ist, standardmäßig verwendet.</dd>
</dl>

<dl>
  <dt>Dockerfile</dt>
  <dd>Eine Dockerfile ist eine Textdatei, die Anweisungen zur Erstellung eines Docker-Image enthält. Typiscerweise wird ein Image auf einem Basisimage erstellt, das ein Basisbetriebssystem, z. B. Ubuntu enthält. Sie können mit den Dockerfile-Anweisungen schrittweise das Basisimage ändern, um die Umgebung zu definieren, die die App für die Ausführung benötigt. Jede Änderung am Basisimage beschreibt eine neue Imageebene und Sie können mehrere Änderungen in einer einzelnen Dockerfilezeile vornehmen. Die Anweisungen in einer Dockerfile können Buildartefakte referenzieren, die separat gespeichert sind (z. B. eine App, die Konfiguration der App und die Abhängigkeiten der App).</dd>
</dl>

Für weitere Informationen zu Docker-spezifischen Begriffen [ziehen Sie das Docker-Glossar zurate](https://docs.docker.com/glossary/).

### Namensbereiche planen
{: #registry_namespaces}

{{site.data.keyword.registrylong_notm}} bietet eine private Multi-Tenant-Registry für Images, die von IBM gehostet und verwaltet wird. In dieser Registry können Sie Ihre Docker-Images sicher speichern, indem Sie einen Registrynamensbereich einrichten.
{:shortdesc}

Wenn Sie separate Repositorys verwenden möchten (beispielsweise für Ihre Produktions- und Ihre Staging-Umgebungen), können Sie mehrere Namensbereiche einrichten. Falls Sie die Registry in mehreren {{site.data.keyword.Bluemix_notm}}-Regionen verwenden möchten, müssen Sie für jede Region einen eigenen Namensbereich einrichten. Namensbereiche sind innerhalb Regionen eindeutig. Sie können denselben Namensbereichsnamen für jede Region verwenden, solange niemand anderes einen Namensbereich mit diesem Namen in dieser Region eingerichtet hat.

Wenn Sie ausschließlich mit den von IBM bereitgestellten öffentlichen Images arbeiten möchten, ist die Einrichtung eines Namensbereichs nicht erforderlich.

**Hinweis:** Wenn Sie nicht sicher sind, ob bereits ein Namensbereich für Ihr Konto eingerichtet ist, führen Sie den Befehl `bx cr namespace-list` aus, um Informationen zu vorhandenen Namensbereichen abzurufen. Wenn Sie bereits {{site.data.keyword.containerlong_notm}}-Kunde sind und [ einzelne oder skalierbare Containergruppen verwenden](../../containers/cs_classic.html), verfügen Sie bereits über einen Namensbereich. Sie können zusätzliche Namensbereiche erstellen, aber den Befehl `cf ic namespace set` für mehr als einen Namensbereich nicht ausführen.

Beachten Sie bei der Wahl eines Namens für den Namensbereich die folgenden Regeln:

-   Ihr Namensbereich muss innerhalb einer {{site.data.keyword.Bluemix_notm}}-Region eindeutig sein.
-   Der Name muss 4 bis 30 Zeichen lang sein.
-   Der Name muss mit mindestens einem Buchstaben bzw. einer Ziffer beginnen.
-   Der Name darf ausschließlich Kleinbuchstaben, Ziffern oder Unterstreichungszeichen (_) enthalten.

Nachdem Sie Ihren ersten Namensbereich eingerichtet haben, werden Sie dem kostenlosen Serviceplan für {{site.data.keyword.registrylong_notm}} zugewiesen, wenn Sie noch kein [Upgrade für Ihren Plan](#registry_plan_upgrade) durchgeführt haben.

## {{site.data.keyword.registrylong_notm}}-Regionen
{: #registry_regions}

{{site.data.keyword.registrylong_notm}}-Registrys sind in mehreren Regionen verfügbar.
{:shortdesc}

### Lokale Regionen
{: #registry_regions_local}

Eine Region ist ein geografischer Bereich, auf den über einen dedizierten Endpunkt zugegriffen wird. {{site.data.keyword.registrylong_notm}}-Registrys sind in den folgenden Regionen verfügbar:

-   Asien-Pazifik (Süden): `registry.au-syd.bluemix.net`
-   Zentraleuropa: `registry.eu-de.bluemix.net`
-   Großbritannien (Süden): `registry.eu-gb.bluemix.net`
-   Vereinigte Staaten (Süden): `registry.ng.bluemix.net`

Alle Registry-Artefakte sind bereichsorientiert in Bezug auf die bestimmte regionale Registry, mit der Sie aktuell arbeiten. Namensbereiche, Images, Tokens, Kontingenteinstellungen und Planeinstellungen müssen beispielsweise für jede regionale Registry jeweils separat verwaltet werden.

Wenn Sie eine andere als Ihre lokale Region verwenden möchten, können Sie die Region, auf die Sie zugreifen möchten, ansteuern, indem Sie den Befehl `bx target` mit dem Flag `-r` ausführen. Dabei steht _&lt;region&gt;_ für den Namen der Region (`us-south`, `eu-de`, `eu-gb` oder `au-syd`).

```
bx target -r <region>
```
{: pre}

Wenn Sie beispielsweise zur Region 'Zentraleuropa' wechseln möchten, führen Sie den folgenden Befehl aus:

```
bx target -r eu-de
```
{: pre}


