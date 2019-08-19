---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# Images aufbewahren
{: #registry_retention}

Sie können darüber entscheiden, ob Images gelöscht oder beibehalten werden sollen.
{:shortdesc}

## Aufbewahrung planen
{: #retention_plan}

Der Befehl [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) wird auf einer Basis pro Namensbereich ausgeführt. Daher bedeutet dies, dass Sie verschiedene Aufbewahrungskriterien für Ihre Anforderungen anwenden können, wenn Sie mehrere Namensbereiche in Ihrer Pipeline verwenden.

Ziehen Sie eine typische Bereitstellungspipeline mit Entwicklungs-, Staging- und Produktionsumgebungen in Betracht. Bei der Codebereitstellung werden Images durch kontinuierliche Integration und kontinuierliche Bereitstellung per Push-Operation in die Registry gestellt und anschließend direkt in der Entwicklungsumgebung bereitgestellt. Nach dem Testen werden einige Builds von der Entwicklung zum Staging und dann möglicherweise in die Produktion hochgestuft. In diesem Szenario ist die Rate des Imagewechsels in der Entwicklung am schnellsten und in der Produktion am langsamsten. Wenn all Ihre Umgebungen Images per Pull-Operation aus demselben Namensbereich extrahieren, ist eine Auswahl der entsprechenden Anzahl an aufzubewahrenden Images wegen dieses Geschwindigkeitsunterschieds möglicherweise schwierig.

Eine gute Strategie ist die Lieferung aller Images an einen Entwicklungsnamensbereich, z. B. `project-development`, und die anschließende Verwendung des Befehls [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag), um das Image für einen anderen Namensbereich zu taggen, sobald es in eine höhere Stage der Pipeline umgestuft wird. Im vorherigen Beispiel sind drei Namensbereich möglich: Entwicklung, `project-development`, Staging, `project-staging`, und Produktion, `project-production`. Wenn Sie eine Umstufung von der Entwicklung zum Staging durchführen, werden die Images aus dem Namensbereich `project-development` in den Namensbereich `project-staging` getaggt; die Images aus dem Namensbereich `project-staging` werden für die Bereitstellung genutzt. Ähnlich ist es bei der Umstufung vom Staging zur Produktion; dabei werden Images aus dem Namensbereich `project-staging` in den Namensbereich `project-production` getaggt; die Namensbereichsimages des Typs `project-production` werden in der Produktionsbereitstellung verwendet.

Wenn Sie diese Technik anwenden, haben Sie den folgenden Nutzen:

* Sie können verschiedene Aufbewahrungseinstellungen für Entwicklungs-, Staging- und Produktionsnamensbereiche auswählen.
* Im Vergleich zur Verwendung eines einzigen Namensbereichs für alle Images minimieren Sie die Wahrscheinlichkeit, dass versehentlich ein Image entfernt wird, das möglicherweise in Ihren Staging- oder Produktionsumgebungen verwendet wird.
* Sie können verschiedene [IAM](/docs/services/Registry?topic=registry-iam)-Richtlinien verwenden. Sie haben z. B. einen eingeschränkteren Zugriff auf Produktionsimages.
* Sie können Produktionsimages signieren und Entwicklungs- und Staging-Images unsigniert lassen.

## Bereinigen Sie Ihre Namensbereiche, indem Sie nur Images beibehalten, die Ihren Kriterien entsprechen.
{: #retention_images}

Bewahren Sie Images für jedes Repository innerhalb eines Namensbereichs in {{site.data.keyword.registrylong_notm}} durch Anwenden angegebener Kriterien auf. Alle anderen Images im Namensbereich werden gelöscht.
{:shortdesc}

Mit dem Befehl [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) werden die Images aufgeführt, die gelöscht werden, und Sie erhalten die Möglichkeit, die Aktion vor dem Löschen abzubrechen.

Wenn ein Image in einem Repository von mehreren Tags referenziert wird, wird dieses Image nur einmal gezählt. Es werden die neuesten Images aufbewahrt. Der Zeitpunkt der Erstellung und nicht der Zeitpunkt der Push-Operation für das Image in die Registry bestimmt das Alter des Image.
{: tip}

Das Löschen eines Images kann nicht rückgängig gemacht werden. Das Löschen eines Images, das von einer vorhandenen Bereitstellung verwendet wird, kann zu einem Scale-up, einem neuen Zeitplan oder beidem führen, um fehlzuschlagen.
{: important}

Führen Sie die folgenden Schritte aus, um die Anzahl der Images in jedem Repository innerhalb Ihres Namensbereichs durch Verwendung der Befehlszeilenschnittstelle zu reduzieren:

1. Melden Sie sich bei {{site.data.keyword.cloud_notm}} an, indem Sie den Befehl `ibmcloud login` ausführen.
2. Wählen Sie die Registry aus, in der Sie Ihre Images bereinigen möchten, indem Sie den folgenden Befehl ausführen und die entsprechende Region auswählen:

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. Führen Sie den folgenden Befehl aus, wenn Sie einige Images beibehalten und andere löschen möchten:

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   Dabei ist `IMAGECOUNT` die Anzahl der Images, die Sie für jedes Repository in Ihrem Namensbereich `NAMESPACE` beibehalten möchten.

3. Überprüfen Sie, ob die Images gelöscht wurden, indem Sie den folgenden Befehl ausführen, und stellen Sie sicher, dass die Images nicht in der Liste angezeigt werden.

   ```
   ibmcloud cr image-list
   ```
   {: pre}
