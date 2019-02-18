---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Sicherheitslücken bei Images überwachen
{: #registry_ui}

Sie können Informationen zu potenziellen Sicherheitslücken sowie zur Sicherheit der Images in den öffentlichen und privaten {{site.data.keyword.registrylong}}-Repositorys mithilfe der {{site.data.keyword.Bluemix_notm}}-Konsole anzeigen.
{:shortdesc}

Die Spalte **Sicherheitsstatus** enthält die folgenden Informationen zum Image:

- `Sicher` Es wurden keine Sicherheitsproblem festgestellt.
- `Gefährdet` Es wurden Sicherheits- oder Konfigurationsprobleme festgestellt, die behoben werden müssen, bevor das Image bereitgestellt werden kann.
- `Unvollständig` Der Scan ist nicht vollständig. Die Ausführung des Scans ist noch nicht abgeschlossen oder das Betriebssystem des Image ist möglicherweise nicht kompatibel. Warten Sie und wiederholen Sie dann den Scan. Wenn der Scan weiterhin nicht abgeschlossen werden kann, führen Sie erneut eine Push-Operation für das Image aus, um einen neuen Scan zu starten. Images mit unvollständigen Scans werden nicht für die Bereitstellung blockiert.
- `Nicht unterstütztes Betriebssystem` Das Betriebssystem im Image wird nicht unterstützt.

Führen Sie die folgenden Schritte aus, um die grafische Benutzerschnittstelle anzuzeigen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole ([https://console.bluemix.net ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net)) mit Ihrer IBMid an.
2. Wenn Sie über mehrere {{site.data.keyword.Bluemix_notm}}-Konten verfügen, wählen Sie das Konto und die Region im Kontomenü aus, die Sie verwenden möchten.
3. Klicken Sie auf **Katalog**.
4. Wählen Sie die Kategorie **Container** aus und klicken Sie auf die Kachel **Container Registry**.
5. Zum Anzeigen von Informationen zu Images in Ihren privaten Repositorys klicken Sie auf **Images**. Es wird eine Liste von Images in Ihren privaten Repositorys und der Sicherheitsstatus für die einzelnen Images angezeigt.
6. Weitere Informationen zu potenziellen Sicherheitslücken, einschließlich Tags und Image-Auszüge, können Sie aufrufen, indem Sie auf die Zeile für das Image in der Tabelle klicken. Die Registerkarte **Imagedetails** wird geöffnet.
7. Klicken Sie auf die Registerkarte **Probleme nach Typ**, um Informationen zu den Problemen nach Typ des Problems zu erhalten.
8. Klicken Sie auf die Registerkarte **Zugeordnete Container**, um Informationen zu den zugeordneten Containern zu erhalten.

Eine Erläuterung zu den Informationen im Sicherheitsbericht finden Sie in [Imagesicherheit mit Vulnerability Advisor verwalten](/docs/services/va/va_index.html).
