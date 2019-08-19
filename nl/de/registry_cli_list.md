---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-08"

keywords: IBM Cloud Container Registry, commands, format commands, filter command output, private registry, registry commands, formatting output, filtering output, output, Go template options, data types, 

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

# CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern
{: #registry_cli_list}

Sie können die CLI-Ausgabe für unterstützte {{site.data.keyword.registrylong}}-Befehle formatieren und filtern.
{:shortdesc}

Standardmäßig wird die CLI-Ausgabe in einem lesbaren Format angezeigt. Diese Ansicht kann jedoch Ihre Möglichkeit, die Ausgabe zu verwenden, einschränken, besonders wenn der Befehl programmgesteuert ausgeführt wird. Beispiel: Sie möchten in der CLI-Ausgabe `ibmcloud cr image-list` das Feld `Size` nach numerischer Größe sortieren, der Befehl gibt jedoch einen beschreibenden Text der Größe zurück. Das `container-registry`-CLI-Plug-in enthält die Formatoption, die Sie verwenden können, um eine Go-Vorlage für die Ausgabe der Befehlszeilenschnittstelle anzuwenden. Die Go-Vorlage ist ein Feature der [Go-Programmiersprache ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://golang.org/pkg/text/template/), mit der Sie die Ausgabe der Befehlszeilenschnittstellen anpassen können.

Sie können die CLI-Ausgabe ändern, indem Sie die Option 'format' auf zwei verschiedene Arten anwenden:

1. Formatieren von Daten in Ihrer CLI-Ausgabe. Ändern Sie beispielsweise die Ausgabe des Feldes `Created` von UNIX-Zeit in Standardzeit.
2. Filtern von Daten in Ihrer CLI-Ausgabe. Filtern Sie beispielsweise nach Details zum Image, um eine bestimmte Untergruppe von Images mithilfe der Bedingung `if gt` der Go-Vorlagendatei anzuzeigen.

Sie können die Option 'format' mit den folgenden {{site.data.keyword.registrylong_notm}}-Befehlen verwenden. Klicken Sie auf einen Befehl, um eine Liste der verfügbaren Felder und ihrer Datentypen anzuzeigen.

- [`ibmcloud cr image-list`](#registry_cli_list_imagelist)
- [`ibmcloud cr image-inspect`](#registry_cli_list_imageinspect)
- [`ibmcloud cr token-list`](#registry_cli_list_tokenlist)

Die folgenden Codebeispiele zeigen, wie Sie die Formatierungs- und Filteroptionen verwenden können.

- Führen Sie den folgenden Befehl `ibmcloud cr image-list` aus, um Repository, Tag und Sicherheitsstatus aller Images mit einer Größe von über 1 MB anzuzeigen:

  ```
  ibmcloud cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
  ```
  {: pre}

  Die folgende Nachricht ist ein Beispiel für die Ausgabe des Befehls:

  ```
  example-<region>.icr.io/user1/ibmliberty:latest No Issues
  example-<region>.icr.io/user1/ibmnode:1 2 Issues
  example-<region>.icr.io/user1/ibmnode:test1 1 Issue
  example-<region>.icr.io/user1/ibmnode2:test2 7 Issues
  ```
  {: screen}

- Führen Sie den folgenden Befehl des Typs `ibmcloud cr image-inspect` aus, um anzuzeigen, wo die {{site.data.keyword.IBM_notm}} Dokumentation für ein angegebenes öffentliches {{site.data.keyword.IBM_notm}} Image gehostet wird:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"
  ```
  {: pre}

  Die folgende Nachricht ist ein Beispiel für die Ausgabe des Befehls:

  ```
  map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
  ```
  {: screen}

- Führen Sie den folgenden Befehl `ibmcloud cr image-inspect` aus, um die verfügbaren Ports für ein angegebenes Image anzuzeigen:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"
  ```
  {: pre}

  Die folgende Nachricht ist ein Beispiel für die Ausgabe des Befehls:

  ```
  map[9080/tcp: 9443/tcp:]
  ```
  {: screen}

- Führen Sie den folgenden Befehl `ibmcloud cr token-list` aus, um alle schreibgeschützten Tokens anzuzeigen:

  ```
  ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
  ```
  {: pre}

  Die folgende Nachricht ist ein Beispiel für die Ausgabe des Befehls:

  ```
  0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
  ```
  {: screen}

## Go-Vorlagenoptionen und Datentypen im Befehl `ibmcloud cr image-list`
{: #registry_cli_list_imagelist}

In der folgenden Tabelle finden Sie die verfügbaren Go-Vorlagenoptionen und Datentypen für den Befehl [`ibmcloud cr image-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list).
{:shortdesc}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`Created`|Ganzzahl (64-Bit)|Zeigt den Erstellungszeitpunkt des Images als Sekundenanzahl in [UNIX-Zeit ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/Unix_time) an.|
|`Digest`|Zeichenfolge|Zeigt die eindeutige ID für ein Image an.|
|`Namespace`|Zeichenfolge|Zeigt den Namensbereich an, in dem das Image gespeichert ist.|
|`Repository`|Zeichenfolge|Zeigt das Repository des Image an.|
|`SecurityStatus`|Struct|Zeigt den Sicherheitsstatus für das Image an. Sie können folgende Werte filtern und formatieren: *Status* `string`, *IssueCount* `int` und *ExemptionCount* `int`. Die möglichen Status sind in [Sicherheitslückenbericht mittels CLI prüfen](/docs/services/Registry?topic=va-va_index#va_registry_cli) beschrieben.|
|`Size`|Ganzzahl (64-Bit)|Zeigt die Größe des Image in Byte an.|
|`Tag`|Zeichenfolge|Zeigt den Tag für das Image an.|
{: caption="Tabelle 1. Verfügbare Felder und Datentypen im Befehl <codeibmcloud cr image-list</code>." caption-side="top"}>

## Go-Vorlagenoptionen und Datentypen im Befehl `ibmcloud cr image-inspect`
{: #registry_cli_list_imageinspect}

In der folgenden Tabelle finden Sie die verfügbaren Go-Vorlagenoptionen und Datentypen für den Befehl [`ibmcloud cr image-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect).
{:shortdesc}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`Architecture`|Zeichenfolge|Zeigt die Prozessorarchitektur an, die verwendet wurde, um dieses Image zu erstellen, und die erforderlich ist, um das Image auszuführen.|
|`Author`|Zeichenfolge|Zeigt den Autor des Image an.|
|`Comment`|Zeichenfolge|Zeigt die Beschreibung des Image an.|
|`Config`|Objekt|Zeigt Konfigurationsmetadaten für das Image an. Siehe Felddetails in [`Config`](#registry_cli_list_imageinspect_config).|
|`Container`|Zeichenfolge|Zeigt die ID des Containers an, der das Image erstellt hat.|
|`ContainerConfig`|Objekt|Zeigt die Standardkonfiguration für Container an, die über dieses Image gestartet werden. Siehe Felddetails in [`Config`](#registry_cli_list_imageinspect_config).|
|`Created`|Zeichenfolge|Zeigt die [UNIX-Zeitmarke ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/Unix_time) für den Erstellungszeitpunkt des Images an.|
|`DockerVersion`|Zeichenfolge|Zeigt die Docker-Version an, die zum Erstellen dieses Image verwendet wurde.|
|`ID`|Zeichenfolge|Zeigt die eindeutige ID für ein Image an.|
|`Os`|Zeichenfolge|Zeigt die Betriebssystemfamilie, die verwendet wurde, um dieses Image zu erstellen, und die zur Ausführung des Image erforderlich ist.|
|`OsVersion`|Zeichenfolge|Zeigt die Version des Betriebssystems an, die verwendet wurde, um dieses Image zu erstellen.|
|`Parent`|Zeichenfolge|Zeigt die ID des übergeordneten Image an, das verwendet wurde, um dieses Image zu erstellen.|
|`RootFS`|Objekt|Zeigt Metadaten an, die das Stammdateisystem für das Image beschreiben. Siehe Felddetails in [`RootFS`](#registry_cli_list_imageinspect_rootfs).|
|`Size`|Ganzzahl (64-Bit)|Zeigt die Größe des Image in Byte an.|
|`VirtualSize`|Ganzzahl (64-Bit)|Zeigt die summierte Größe der einzelnen Ebenen des Image in Byte an.|
{: caption="Tabelle 2. Verfügbare Felder und Datentypen im Befehl <codeibmcloud cr image-inspect</code>." caption-side="top"}>

### `Config`
{: #registry_cli_list_imageinspect_config}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`ArgsEscaped`|Boolesch|Zeigt 'true' an, wenn der Befehl bereits mit Escapezeichen versehen ist (Windows-spezifisch).|
|`AttachStderr`|Boolesch|Zeigt _true_ an, wenn der Standardfehlerdatenstrom an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`AttachStdin`|Boolesch|Zeigt _true_ an, wenn der Standardeingabedatenstrom an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`AttachStdout`|Boolesch|Zeigt _true_ an, wenn der Standardausgabedatenstrom an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`Cmd`|Array von Zeichenfolgen|Beschreibt die Befehle und Argumente, die an einen Container übergeben werden, um beim Starten des Containers ausgeführt zu werden.|
|`Domainname`|Zeichenfolge|Zeigt den vollständig qualifizierten Domänennamen des Containers an.|
|`Entrypoint`|Array von Zeichenfolgen|Beschreibt den Befehl, der beim Starten des Containers ausgeführt wird.|
|`Env`|Array von Zeichenfolgen|Zeigt die Liste der Umgebungsvariablen in Form von Schlüssel-Wert-Paaren an.|
|`ExposedPorts`|Schlüssel-Wert-Zuordnung|Zeigt die Liste der zugänglichen Ports im Format `[123:,456:]` an.|
|`Healthcheck`|Objekt|Beschreibt, wie Sie überprüfen, ob der Container korrekt ausgeführt wird. Siehe Felddetails in [`Healthcheck`](#registry_cli_list_imageinspect_healthcheck).|
|`Hostname`|Zeichenfolge|Zeigt den Hostnamen des Containers an.|
|`Image`|Zeichenfolge|Zeigt den Namen des Image an, das vom Operator übergeben wurde.|
|`Labels`|Schlüssel-Wert-Zuordnung|Zeigt die Liste von Bezeichnungen an, die dem Image als Schlüssel-Wert-Paare hinzugefügt wurden.|
|`MacAddress`|Zeichenfolge|Zeigt die MAC-Adresse an, die dem Container zugewiesen ist.|
|`NetworkDisabled`|Boolesch|Zeigt _true_ an, wenn Netzbetrieb für den Container inaktiviert ist, und _false_, wenn Netzbetrieb für den Container aktiviert ist.|
|`OnBuild`|Array von Zeichenfolgen|Zeigt die `ONBUILD`-Metadaten an, die für die Image-Dockerfile definiert wurden.|
|`OpenStdin`|Boolesch|Zeigt _true_ an, wenn der Standardeingabedatenstrom geöffnet ist, und _false_, wenn er geschlossen ist.|
|`Shell`|Array von Zeichenfolgen|Zeigt die Shell-Formen RUN, CMD und ENTRYPOINT an.|
|`StdinOnce`|Boolesch|Zeigt _true_ an, wenn der Standardeingabedatenstrom nach dem Trennen des angefügten Clients geschlossen wird, und _false_, wenn er geöffnet bleibt.|
|`StopSignal`|Zeichenfolge|Beschreibt das UNIX-Stoppsignal, das zu senden ist, wenn der Container gestoppt werden soll.|
|`StopTimeout`|Ganzzahl|Zeigt das Zeitlimit in Sekunden an, innerhalb dessen ein Container gestoppt werden soll.|
|`Tty`|Boolesch|Zeigt _true_ an, wenn ein `Pseudo-TTY` an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`User`|Zeichenfolge|Zeigt den Benutzer an, der Befehle in dem Container ausführt, in dem das Image verwendet wird.|
|`Volumes`|Schlüssel-Wert-Zuordnung|Zeigt die Liste der Datenträgermounts an, die an einen Container angehängt sind.|
|`WorkingDir`|Zeichenfolge|Zeigt das Arbeitsverzeichnis in dem Container an, in dem angegebene Befehle ausgeführt werden.|
{: caption="Tabelle 3. Verfügbare Felder und Datentypen in <codeConfig</code>. " caption-side="top"}>

### `Healthcheck`
{: #registry_cli_list_imageinspect_healthcheck}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`Interval`|Ganzzahl (64-Bit)|Zeigt die Zeit in Nanosekunden an, die zwischen zwei Statusprüfungen gewartet werden soll.|
|`Retries`|Ganzzahl|Zeigt die Anzahl der aufeinanderfolgenden Fehlversuche an, die erforderlich sind, damit die Ausführung eines Containers als nicht korrekt eingestuft wird.|
|`Test`|Array von Zeichenfolgen|Zeigt an, wie die Statusprüfung ausgeführt wird. Verfügbare Optionen:<ul><li>`{}`: Statusprüfung übernehmen</li><li>`{"NONE"}`: Statusprüfung ist inaktiviert</li><li>`{"CMD", args...}`: Argumente direkt ausführen</li><li>`{"CMD-SHELL", command}`: den Befehl mit der Standard-Shell des Systems ausführen</li></ul>|
|`Timeout`|Ganzzahl (64-Bit)|Zeigt die Zeit in Nanosekunden an, die gewartet werden soll, bevor die Statusprüfung als fehlgeschlagen eingestuft wird.|
{: caption="Tabelle 4. Verfügbare Felder und Datentypen im <codeHealthcheck</code>-Konstrukt." caption-side="top"}>

### `RootFS`
{: #registry_cli_list_imageinspect_rootfs}

|Option|Typ|Beschreibung|
|------|----|-----------|
|`BaseLayer`|Zeichenfolge|Zeigt den Deskriptor für die Basisebene im Image an.|
|`Layers`|Array von Zeichenfolgen|Zeigt die Deskriptoren der einzelnen Image-Ebenen an.|
|`Type`|Zeichenfolge|Zeigt den Typ des Dateisystems an.|
{: caption="Tabelle 5. Verfügbare Felder und Datentypen im <codeRootFS</code>-Konstrukt." caption-side="top"}>

## Go-Vorlagenoptionen und Datentypen im Befehl `ibmcloud cr token-list`
{: #registry_cli_list_tokenlist}

In der folgenden Tabelle finden Sie die verfügbaren Go-Vorlagenoptionen und Datentypen für den Befehl [`ibmcloud cr token-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_list).
{:shortdesc}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`Beschreibung`|Zeichenfolge|Zeigt die Beschreibung des Tokens an.|
|`Expiry`|Ganzzahl (64-Bit)|Zeigt die [UNIX-Zeitmarke ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/Unix_time) für den Zeitpunkt an, an dem das Token abläuft.|
|`ID`|Zeichenfolge|Zeigt die eindeutige ID für ein Token an.|
|`ReadOnly`|Boolesch|Zeigt _true_ an, wenn für Images nur Pull-Operationen durchgeführt werden können, und _false_, wenn für Images Push- und Pull-Operationen in und aus Ihrem Namensbereich durchgeführt werden können.|
{: caption="Tabelle 6. Verfügbare Felder und Datentypen im Befehl <codeibmcloud cr token-list</code>." caption-side="top"}>
