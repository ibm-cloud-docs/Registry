---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.registrylong_notm}}-Befehle (`bx cr`) zum Verwalten von Docker-Images im Namensbereich
{: #registry_cli_reference}

Sie können das Container-Registry-Plug-in dazu verwenden, Ihren eigenen Imagenamensbereich in einer von IBM gehosteten und verwalteten privaten Registry einzurichten, in der Sie Docker-Images sicher speichern und gemeinsam mit allen Benutzern in Ihrem {{site.data.keyword.Bluemix}}-Konto nutzen können.
{:shortdesc}


## bx cr-Befehle
{: #registry_cli_reference_bxcr}

Führen Sie die `bx cr`-Befehle in der {{site.data.keyword.registryshort_notm}}-CLI aus.
{:shortdesc}
  
Informationen zu den unterstützten Befehlen finden Sie unter [{{site.data.keyword.registrylong_notm}}-CLI](registry_cli.html).

## CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern
{: #registry_cli_listing}

Sie können die CLI-Ausgabe für unterstützte {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern.
{:shortdesc}

Standardmäßig wird die CLI-Ausgabe in einem lesbaren Format angezeigt. Diese Ansicht kann jedoch Ihre Möglichkeit, die Ausgabe zu verwenden, einschränken, besonders wenn der Befehl programmgesteuert ausgeführt wird. Beispiel: Sie möchten in der CLI-Ausgabe `bx cr image-list` das Feld `Size` nach numerischer Größe sortieren, der Befehl gibt jedoch einen beschreibenden Text der Größe zurück. Das Container-Registry-Plug-in stellt die Option 'format' bereit, mit der Sie eine Go-Vorlage auf die CLI-Ausgabe anwenden können. Die Go-Vorlage ist eine Komponente der [Programmiersprache Go](https://golang.org/pkg/text/template/), mit der Sie die CLI-Ausgabe anpassen können.

Sie können die CLI-Ausgabe ändern, indem Sie die Option 'format' auf zwei verschiedene Arten anwenden:

1.  Formatieren von Daten in Ihrer CLI-Ausgabe. Ändern Sie beispielsweise die Ausgabe des Feldes `Created` von Unix-Zeit in Standardzeit.
2.  Filtern von Daten in Ihrer CLI-Ausgabe. Filtern Sie beispielsweise nach Details zum Image, um eine bestimmte Untergruppe von Images mithilfe der Bedingung `if gt` der Go-Vorlagendatei anzuzeigen.

Sie können die Option 'format' mit den folgenden {{site.data.keyword.registrylong_notm}}-Befehlen verwenden. Klicken Sie auf einen Befehl, um eine Liste der verfügbaren Felder und ihrer Datentypen anzuzeigen.

-   [`bx cr image-list`](registry_cli_reference.html#registry_cli_listing_imagelist)
-   [`bx cr image-inspect`](registry_cli_reference.html#registry_cli_listing_imageinspect)
-   [`bx cr token-list`](registry_cli_reference.html#registry_cli_listing_tokenlist)

Die folgenden Codebeispiele zeigen, wie Sie die Formatierungs- und Filteroptionen verwenden können.

-   Führen Sie den folgenden Befehl `bx cr image-list` aus, um Repository, Tag und Sicherheitsstatus aller Images mit einer Größe von über 1 MB anzuzeigen:

    ```
    bx cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
    ```
    {: pre}

    Beispielausgabe:

    ```
    example-registry.<region>.bluemix.net/user1/ibmliberty:latest No Issues
    example-registry.<region>.bluemix.net/user1/ibmnode:1 2 Issues
    example-registry.<region>.bluemix.net/user1/ibmnode:test1 1 Issue
    example-registry.<region>.bluemix.net/user1/ibmnode2:test2 7 Issues
    ```
    {: screen}


-   Führen Sie den folgenden Befehl `bx cr image-inspect` aus, um anzuzeigen, wo die IBM Dokumentation für ein angegebenes öffentliches IBM Image gehostet wird:

    ```
    bx cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"

    ```
    {: pre}

    Beispielausgabe:

    ```
    map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
    ```
    {: screen}

-   Führen Sie den folgenden Befehl `bx cr image-inspect` aus, um die verfügbaren Ports für ein angegebenes Image anzuzeigen:

    ```
    bx cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"

    ```
    {: pre}

    Beispielausgabe:

    ```
    map[9080/tcp: 9443/tcp:]
    ```
    {: screen}

-   Führen Sie den folgenden Befehl `bx cr token-list` aus, um alle schreibgeschützten Tokens anzuzeigen:

    ```
    bx cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
    {: pre}

    Beispielausgabe:

    ```
    0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
    ```
    {: screen}


### Go-Vorlagenoptionen und Datentypen im Befehl `bx cr image-list`
{: #registry_cli_listing_imagelist}

In der folgenden Tabelle finden Sie die verfügbaren Go-Vorlagenoptionen und Datentypen für den Befehl `bx cr image-list`.
{:shortdesc}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`Created`|Ganzzahl (64-Bit)|Wird angezeigt, wenn das Image erstellt wurde, ausgedrückt als Anzahl Sekunden in [UNIX-Zeit](https://en.wikipedia.org/wiki/Unix_time).|
|`Digest`|Zeichenfolge|Zeigt die eindeutige Kennung für ein Image an.|
|`Namespace`|Zeichenfolge|Zeigt den Namensbereich an, in dem das Image gespeichert ist.|
|`Repository`|Zeichenfolge|Zeigt das Repository des Image an.|
|`Size`|Ganzzahl (64-Bit)|Zeigt die Größe des Image in Byte an.|
|`Tag`|Zeichenfolge|Zeigt den Tag für das Image an.|
|`SecurityStatus`|Struct|Zeigt den Sicherheitsstatus für das Image an. Sie können folgende Werte filtern und formatieren: Status  `string`, IssueCount `int` und ExemptionCount `int`. Die möglichen Status sind in [Sicherheitslückenbericht mittels CLI prüfen](../va/va_index.html#va_registry_cli) beschrieben.|
{: caption="Tabelle 1. Verfügbare Felder und Datentypen im Befehl 'bx cr image-list'." caption-side="top"}

### Go-Vorlagenoptionen und Datentypen im Befehl `bx cr image-inspect`
{: #registry_cli_listing_imageinspect}

In der folgenden Tabelle finden Sie die verfügbaren Go-Vorlagenoptionen und Datentypen für den Befehl `bx cr image-inspect`.
{:shortdesc}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`ID`|Zeichenfolge|Zeigt die eindeutige Kennung für ein Image an.|
|`Parent`|Zeichenfolge|Zeigt die ID des übergeordneten Image an, das verwendet wurde, um dieses Image zu erstellen.|
|`Comment`|Zeichenfolge|Zeigt die Beschreibung des Image an.|
|`Created`|Zeichenfolge|Zeigt die [UNIX-Zeitmarke](https://en.wikipedia.org/wiki/Unix_time) an, zu der das Image erstellt wurde.|
|`Container`|Zeichenfolge|Zeigt die ID des Containers an, der das Image erstellt hat.|
|`ContainerConfig`|Objekt|Zeigt die Standardkonfiguration für Container an, die über dieses Image gestartet werden. Siehe Felddetails in [Config](registry_cli_reference.html#config).|
|`DockerVersion`|Zeichenfolge|Zeigt die Docker-Version an, die zum Erstellen dieses Image verwendet wurde.|
|`Author`|Zeichenfolge|Zeigt den Autor des Image an.|
|`Config`|Objekt|Zeigt Konfigurationsmetadaten für das Image an. Siehe Felddetails in [Config](registry_cli_reference.html#config).|
|`Architecture`|Zeichenfolge|Zeigt die Prozessorarchitektur an, die verwendet wurde, um dieses Image zu erstellen, und die erforderlich ist, um das Image auszuführen.|
|`Os`|Zeichenfolge|Zeigt die Betriebssystemfamilie, die verwendet wurde, um dieses Image zu erstellen, und die zur Ausführung des Image erforderlich ist.|
|`OsVersion`|Zeichenfolge|Zeigt die Version des Betriebssystems an, die verwendet wurde, um dieses Image zu erstellen.|
|`Size`|Ganzzahl (64-Bit)|Zeigt die Größe des Image in Byte an.|
|`VirtualSize`|Ganzzahl (64-Bit)|Zeigt die summierte Größe der einzelnen Ebenen des Image in Byte an.|
|`RootFS`|Objekt|Zeigt Metadaten an, die das Stammdateisystem für das Image beschreiben. Siehe Felddetails in [RootFS](registry_cli_reference.html#rootfs).|
{: caption="Tabelle 2. Verfügbare Felder und Datentypen im Befehl 'bx cr image-inspect'." caption-side="top"}

#### Config

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`Hostname`|Zeichenfolge|Zeigt den Hostnamen des Containers an.|
|`Domainname`|Zeichenfolge|Zeigt den vollständig qualifizierten Domänennamen des Containers an.|
|`User`|Zeichenfolge|Zeigt den Benutzer an, der Befehle in dem Container ausführt, in dem das Image verwendet wird.|
|`AttachStdin`|Boolesch|Zeigt _true_ an, wenn der Standardeingabedatenstrom an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`AttachStdout`|Boolesch|Zeigt _true_ an, wenn der Standardausgabedatenstrom an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`AttachStderr`|Boolesch|Zeigt _true_ an, wenn der Standardfehlerdatenstrom an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`ExposedPorts`|Schlüssel-Wert-Zuordnung|Zeigt die Liste der zugänglichen Ports im Format `[123:,456:]` an.|
|`Tty`|Boolesch|Zeigt _true_ an, wenn ein Pseudo-TTY an den Container angefügt ist, und _false_, wenn dies nicht der Fall ist.|
|`OpenStdin`|Boolesch|Zeigt _true_ an, wenn der Standardeingabedatenstrom geöffnet ist, und _false_, wenn er geschlossen ist.|
|`StdinOnce`|Boolesch|Zeigt _true_ an, wenn der Standardeingabedatenstrom nach dem Trennen des angefügten Clients geschlossen wird, und _false_, wenn er geöffnet bleibt.|
|`Env`|Array von Zeichenfolgen|Zeigt die Liste der Umgebungsvariablen in Form von Schlüssel-Wert-Paaren an.|
|`Cmd`|Array von Zeichenfolgen|Beschreibt die Befehle und Argumente, die an einen Container übergeben werden, um beim Starten des Containers ausgeführt zu werden.|
|`Healthcheck`|Objekt|Beschreibt, wie Sie überprüfen, ob der Container in einwandfreiem Zustand ist. Siehe Felddetails in [Healthcheck](registry_cli_reference.html#healthcheck).|
|`ArgsEscaped`|Boolesch|Zeigt 'true' an, wenn der Befehl bereits mit Escapezeichen versehen ist (Windows-spezifisch).|
|`Image`|Zeichenfolge|Zeigt den Namen des Image an, das vom Operator übergeben wurde.|
|`Volumes`|Schlüssel-Wert-Zuordnung|Zeigt die Liste der Datenträgermounts an, die an einen Container angehängt sind.|
|`WorkingDir`|Zeichenfolge|Zeigt das Arbeitsverzeichnis in dem Container an, wo angegebene Befehle ausgeführt werden.|
|`Entrypoint`|Array von Zeichenfolgen|Beschreibt den Befehl, der beim Starten des Containers ausgeführt wird.|
|`NetworkDisabled`|Boolesch|Zeigt _true_ an, wenn Netzbetrieb für den Container inaktiviert ist, und _false_, wenn Netzbetrieb für den Container aktiviert ist.|
|`MacAddress`|Zeichenfolge|Zeigt die MAC-Adresse an, die dem Container zugeordnet ist.|
|`OnBuild`|Array von Zeichenfolgen|Zeigt die ONBUILD-Metadaten an, die für die Image-Dockerfile definiert wurden.|
|`Labels`|Schlüssel-Wert-Zuordnung|Zeigt die Liste von Bezeichnungen an, die dem Image als Schlüssel-Wert-Paare hinzugefügt wurden.|
|`StopSignal`|Zeichenfolge|Beschreibt das UNIX-Stoppsignal, das zu senden ist, wenn der Container gestoppt werden soll.|
|`StopTimeout`|Ganzzahl|Zeigt das Zeitlimit in Sekunden an, innerhalb dessen ein Container gestoppt werden soll.|
|`Shell`|Array von Zeichenfolgen|Zeigt die Shell-Formen RUN, CMD und ENTRYPOINT an.|
{: caption="Tabelle. " caption-side="top"}

#### Healthcheck

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`Test`|Array von Zeichenfolgen|Zeigt an, wie die Statusprüfung ausgeführt wird. Verfügbare Optionen:<ul><li>{}: Statusprüfung übernehmen</li><li>{"NONE"}: Statusprüfung ist inaktiviert</li><li>{"CMD", args...}: Argumente direkt ausführen</li><li>{"CMD-SHELL", command}: den Befehl mit der Standard-Shell des Systems ausführen</li></ul>|
|`Interval`|Ganzzahl (64-Bit)|Zeigt die Zeit in Nanosekunden an, die zwischen zwei Statusprüfungen gewartet werden soll.|
|`Timeout`|Ganzzahl (64-Bit)|Zeigt die Zeit in Nanosekunden an, die gewartet werden soll, bevor die Statusprüfung als fehlgeschlagen eingestuft wird.|
|`Retries`|Ganzzahl|Zeigt die Anzahl der aufeinanderfolgenden Fehlversuche an, die erforderlich sind, damit der Status eines Containers als gestört betrachtet wird.|
{: caption="Tabelle 4. Verfügbare Felder und Datentypen im Healthcheck-Struct." caption-side="top"}

#### RootFS

|Option|Typ|Beschreibung|
|------|----|-----------|
|`Type`|Zeichenfolge|Zeigt den Typ des Dateisystems an.|
|`Layers`|Array von Zeichenfolgen|Zeigt die Deskriptoren der einzelnen Image-Ebenen an.|
|`BaseLayer`|Zeichenfolge|Zeigt den Deskriptor für die Basisebene im Image an.|
{: caption="Tabelle 5. Verfügbare Felder und Datentypen im RootFS-Struct." caption-side="top"}

### Go-Vorlagenoptionen und Datentypen im Befehl `bx cr token-list`
{: #registry_cli_listing_tokenlist}

In der folgenden Tabelle finden Sie die verfügbaren Go-Vorlagenoptionen und Datentypen für den Befehl `bx cr token-list`.
{:shortdesc}

|Feld|Typ|Beschreibung|
|-----|----|-----------|
|`ID`|Zeichenfolge|Zeigt die eindeutige Kennung für ein Token an.|
|`Expiry`|Ganzzahl (64-Bit)|Zeigt die [UNIX-Zeitmarke](https://en.wikipedia.org/wiki/Unix_time) des Zeitpunkts an, an dem das Token abläuft.|
|`ReadOnly`|Boolesch|Zeigt _true_ an, wenn für Images nur Pull-Operationen durchgeführt werden können, und _false_, wenn für Images Push- und Pull-Operationen in und aus Ihrem Namensbereich durchgeführt werden können.|
|`Beschreibung`|Zeichenfolge|Zeigt die Beschreibung des Tokens an.|
{: caption="Tabelle 6. Verfügbare Felder und Datentypen im Befehl 'bx cr token-list'." caption-side="top"}
