---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

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

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

Sie können die {{site.data.keyword.registrylong}}-CLI, die im `container-registry`-CLI-Plug-in bereitgestellt wird, verwenden, um Ihre Registry und die zugehörigen Ressourcen für Ihr {{site.data.keyword.cloud_notm}}-Konto zu verwalten.
{: shortdesc}

**Voraussetzungen**

* Installieren Sie die {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle (CLI). Informationen finden Sie im Abschnitt [Einführung in die Befehlszeilenschnittstelle von {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started). Das Präfix für die Ausführung von Befehlen unter Verwendung der {{site.data.keyword.cloud_notm}}-CLI lautet `ibmcloud`.
* Bevor Sie die Registry-Befehle ausführen, melden Sie sich bei {{site.data.keyword.cloud_notm}} an, wobei Sie den Befehl `ibmcloud login` verwenden, um ein Zugriffstoken zu generieren und Ihre Sitzung zu authentifizieren.

Sobald Aktualisierungen für die `ibmcloud`-CLI und `container-registry`-CLI-Plug-ins verfügbar sind, erhalten Sie eine Benachrichtigung über die Befehlszeile. Stellen Sie sicher, dass Sie Ihre CLI aktuell halten, damit Sie alle verfügbaren Befehle und Flags verwenden können.

Führen Sie den Befehl `ibmcloud plugin list` aus, wenn Sie die aktuelle Version des `container-registry`-CLI-Plug-ins anzeigen möchten.

Informationen zur Verwendung der {{site.data.keyword.registrylong_notm}}-CLI finden Sie unter [Erste Schritte mit {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started).

Weitere Informationen zur IAM-Plattform und zu den Servicezugriffsrollen, die für einige Befehle erforderlich sind, finden Sie unter [Benutzerzugriff mit Identity and Access Management verwalten](/docs/services/Registry?topic=registry-iam#iam).

Beziehen Sie keine personenbezogenen Daten in Ihre Container-Images, Namensbereichsnamen, Beschreibungsfelder oder in Image-Konfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) ein.
{: important}

## `ibmcloud cr api`
{: #bx_cr_api}

Gibt die Details zum Registry-API-Endpunkt zurück, für den die Befehle ausgeführt werden.

```
ibmcloud cr api
```
{: codeblock}

**Voraussetzungen**

Keine

## `ibmcloud cr build`
{: #bx_cr_build}

Erstellt ein Docker-Image in {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`DIRECTORY`</dt>
<dd>Die Position für Ihren Buildkontext, der Ihre Dockerfile und vorausgesetzte Dateien enthält. Wenn Sie den Befehl ausführen, während das Arbeitsverzeichnis auf das Verzeichnis eingestellt ist, in dem Ihr Buildkontext gespeichert ist, können Sie `verzeichnis` durch einen Punkt (.) ersetzen.</dd>
<dt>`--no-cache`</dt>
<dd>(Optional)  Ist dies angegeben, werden zwischengespeicherte Image-Ebenen aus vorherigen Builds nicht in diesem Build verwendet.</dd>
<dt>`--pull`</dt>
<dd>(Optional) Ist dies angegeben, werden die Basisimages auch dann mit Pull-Operation extrahiert, wenn ein Image mit einem übereinstimmenden Tag bereits im Build-Host vorhanden ist.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Ist dies angegeben, wird die Buildausgabe unterdrückt, solange kein Fehler auftritt.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(Optional) Geben Sie ein zusätzliches Buildargument im Format `'KEY=VALUE'` an. Mehrere Buildargumente können angegeben werden, indem dieser Parameter mehrfach eingeschlossen wird. Der Wert jedes Buildarguments ist als Umgebungsvariable verfügbar, wenn Sie eine ARG-Zeile angeben, die mit dem Schlüssel in Ihrer Dockerfile übereinstimmt.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(Optional)  Wenn Sie dieselben Dateien für mehrere Builds verwenden, können Sie einen Pfad zu einer anderen Dockerfile wählen. Geben Sie die Position der Dockerfile relativ zum Buildkontext an. Wenn nicht angegeben, wird standardmäßig `PATH/Dockerfile` verwendet, wobei PATH der Root des Buildkontextes ist.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>Der vollständige Name für das zu erstellende Image, in dem die Registry-URL und der Namensbereich enthalten sind.</dd>
</dl>

**Beispiel**

Erstellen Sie ein Docker-Image, das keinen Build-Cache aus vorherigen Builds verwendet, wobei die Buildausgabe unterdrückt wird, der Tag *`us.icr.io/birds/bluebird:1`* lautet und das Verzeichnis Ihr Arbeitsverzeichnis ist.

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Erstellt eine Freistellung für ein Sicherheitsproblem. Sie können eine Freistellung für ein Sicherheitsproblem erstellen, das für verschiedene Bereiche gilt. Der Bereich kann das Konto, der Namensbereich, das Repository oder der Tag sein.

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Um Ihr Konto als Bereich zu definieren, verwenden Sie `"*"` als Wert. Um einen Namensbereich, ein Repository oder Tag als Bereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namespace`, `namespace/repository`, `namespace/repository:tag`.
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Der Typ des Sicherheitsproblems, das Sie freistellen möchten. Um nach gültigen Problemtypen zu suchen, führen Sie den Befehl `ibmcloud cr exemption-types` aus.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>Die ID des Sicherheitsproblems, das Sie freistellen möchten. Um nach einer Problem-ID zu suchen, führen Sie den Befehl `ibmcloud cr va <image>`, wobei `<image>` der Name des Images ist. Verwenden Sie dabei den entsprechenden Wert aus der Spalte mit der **Schwachstellen-ID** oder der Spalte mit der **Konfigurationsproblem-ID**.
</dd>
</dl>

**Beispiele**

Erstellen Sie eine CVE-Freistellung für CVE mit der ID `CVE-2018-17929` für alle Images im Repository `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Erstellen Sie eine kontoweite CVE-Freistellung für CVE mit der ID `CVE-2018-17929`.

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Erstellen Sie eine Konfigurationsproblemfreistellung für das Problem `application_configuration:nginx.ssl_protocols` für ein einzelnes Image mit dem Tag `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

Listet die Freistellungen für Sicherheitsprobleme auf.

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(Optional) Listet nur die Freistellungen auf, die für diesen Bereich gelten. Um einen Namensbereich, ein Repository oder Tag als Bereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namespace`, `namespace/repository`, `namespace/repository:tag`.
</dd>
</dl>

**Beispiel**

Listet alle Freistellungen für Sicherheitsprobleme auf, die für Images im Repository *`birds/bluebird`* gelten. Die Ausgabe enthält kontoweite Freistellungen, Freistellungen für den Namensbereich *`birds`* und Freistellungen für das Repository *`birds/bluebird`*, aber keine Freistellungen für spezifische Tags innerhalb des Repositorys *`birds/bluebird`*.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Löscht eine Freistellung für ein Sicherheitsproblem. Um Ihre vorhandenen Freistellungen anzuzeigen, führen Sie den Befehl `ibmcloud cr exemption-list` aus.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Um Ihr Konto als Bereich zu definieren, verwenden Sie `"*"` als Wert. Um einen Namensbereich, ein Repository oder Tag als Bereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namespace`, `namespace/repository`, `namespace/repository:tag`.
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Der Problemtyp der Freistellung für das Sicherheitsproblem, das Sie entfernen möchten. Um nach den Problemtyp für Ihre Freistellungen zu suchen, führen Sie den Befehl `ibmcloud cr exemption-list` aus.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>Die ID der Freistellung für das Sicherheitsproblem, das Sie entfernen möchten. Um nach den Problem-IDs für Ihre Freistellungen zu suchen, geben Sie den Befehl `ibmcloud cr exemption-list` ein.
</dd>
</dl>

**Beispiele**

Löschen Sie eine CVE-Freistellung für CVE mit der ID `CVE-2018-17929` für alle Images im Repository `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Löschen Sie eine kontoweite CVE-Freistellung für CVE mit der ID `CVE-2018-17929`.

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Löschen Sie eine Konfigurationsproblemfreistellung für das Problem `application_configuration:nginx.ssl_protocols` für ein einzelnes Image mit dem Tag `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Listet die Typen der Sicherheitsprobleme auf, die Sie freistellen können.

```
ibmcloud cr exemption-types
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

Wenn Sie die IAM-Authentifizierung verwenden, ermöglicht dieser Befehl eine differenzierte Berechtigung. Weitere Informationen finden Sie unter [Benutzerzugriff mit Identity and Access Management verwalten](/docs/services/Registry?topic=registry-iam#iam) und [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

Zeigt den IAM-Richtlinienstatus des anvisierten {{site.data.keyword.registryshort_notm}}-Kontos an. Weitere Informationen finden Sie unter [Benutzerzugriff mit Identity and Access Management verwalten](/docs/services/Registry?topic=registry-iam#iam) und [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Zeigt Details zu einem bestimmten Image an.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen finden Sie unter [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`IMAGE`</dt>
<dd>Der Name des Images, für das ein Bericht erstellt werden soll. Sie können mehrere Images untersuchen, indem Sie die einzelnen Images im Befehl mit einem Leerzeichen zwischen den einzelnen Namen auflisten.

<p>Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Wenn im Imagenamen kein Tag angegeben ist, wird das Image mit dem Tag `latest` untersucht. </p>

</dd>
</dl>

**Beispiel**

Zeigen Sie Details zu den zugänglichen Ports für das Image *`us.icr.io/birds/bluebird:1`* an. Verwenden Sie dazu die Formatierungsanweisung *`"{{ .Config.ExposedPorts }}"`*.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Zeigt alle Images in Ihrem {{site.data.keyword.cloud_notm}}-Konto an.

Der Imagename ist eine Kombination des Inhalts der Spalten **Repository** und **Tag** im Format `repository:tag`.
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`--no-trunc`</dt>
<dd>(Optional) Schneidet die Image-Auszüge nicht ab.</dd>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen finden Sie unter [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Jedes Image wird im Format `repository:tag` aufgelistet.</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Optional) Begrenzen Sie die Ausgabe, sodass nur Images im angegebenen Namensbereich oder Namensbereich und Repository angezeigt werden. </dd>
<dt>`--include-ibm`</dt>
<dd>(Optional) Enthält von {{site.data.keyword.IBM_notm}} bereitgestellte öffentliche Images in der Ausgabe. Ohne diese Option werden standardmäßig nur private Images aufgelistet.</dd>
</dl>

**Beispiel**

Zeigen Sie die Images im Namensbereich *`birds`* im Format `repository:tag` an, ohne dass die Image-Auszüge abgeschnitten werden.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Löschen Sie ein angegebenes Image oder mehrere angegebene Images aus {{site.data.keyword.registrylong_notm}}.

Wenn im selben Image-Auszug in einem Repository mehrere Tags vorhanden sind, entfernt der Befehl `ibmcloud cr image-rm` das zugrunde liegende Image und alle seine Tags. Wenn dasselbe Image in einem anderen Repository oder Namensbereich vorhanden ist, wird diese Kopie des Images nicht entfernt. Wenn Sie ein Tag aus einem Image entfernen möchten, das zugrunde liegende Image und alle anderen Tags jedoch beibehalten möchten, verwenden Sie den Befehl [`ibmcloud cr image-untag`](#bx_cr_image_untag).
{: tip}

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**

<dl>
<dt>`IMAGE`</dt>
<dd>Der Name des Images, das gelöscht werden soll. Sie können mehrere Images gleichzeitig löschen, indem Sie jedes Image im Befehl mit einem Leerzeichen zwischen den einzelnen Namen auflisten. `IMAGE` muss dasselbe Format wie `repository:tag` haben, z. B. `us.icr.io/namespace/image:latest`.

<p>Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Wenn im Imagenamen kein Tag angegeben ist, wird das Image mit dem Tag `latest` gelöscht.</p>

</dd>
</dl>

**Beispiel**
Image `us.icr.io/birds/bluebird:1` löschen.

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

Fügen Sie einem vorhandenen Image ein Tag hinzu, das Sie im Befehl angegeben haben, kopieren Sie das Tag in ein anderes Repository oder kopieren Sie das Tag in ein Repository in einem anderen Namensbereich. Das Zielimage `TARGET_IMAGE` ist das neue Image und das Quellimage `SOURCE_IMAGE` ist das vorhandene Image in {{site.data.keyword.registrylong_notm}}. Die Quellen- und Zielimages müssen sich in derselben Region befinden.

Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen.
{: tip}

```
ibmcloud cr image-tag [QUELLENIMAGE] [ZIELIMAGE]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>Der Name des Quellenimages. `SOURCE_IMAGE` muss dasselbe Format wie `repository:tag` haben, z. B. `us.icr.io/namespace/image:latest`.

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>Der Name des Zielimages. `TARGET_IMAGE` muss dasselbe Format wie `repository:tag` haben, z. B. `us.icr.io/namespace/image:latest`.

</dd>
</dl>

**Beispiele**

Fügen Sie einen weiteren Tagverweis, `latest`, zum Image `us.icr.io/birds/bluebird:1` hinzu.

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

Kopieren Sie das Image `us.icr.io/birds/bluebird:peck` in ein anderes Repository im selben Namensbereich `birds/pigeon`.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

Kopieren Sie das Image `us.icr.io/birds/bluebird:peck` in einen anderen Namensbereich `animals`, auf den Sie zugreifen können.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr image-untag`
{: #bx_cr_image_untag}

Entfernen Sie ein Tag oder mehrere Tags aus jedem angegebenen Image in {{site.data.keyword.registrylong_notm}}.

Um ein Tag aus einem Image zu entfernen, das zugrunde liegende Image und alle anderen Tags jedoch beibehalten möchten, verwenden Sie den Befehl `ibmcloud cr image-untag`. Wenn Sie das zugrunde liegende Image und alle seine Tages löschen möchten, verwenden Sie stattdessen den Befehl [`ibmcloud cr image-rm`](#bx_cr_image_rm).
{: tip}

```
ibmcloud cr image-untag IMAGE [IMAGE...]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**

<dl>
<dt>`IMAGE`</dt>
<dd>Der Name des Images, aus dem Sie ein Tag entfernen möchten. Sie können ein Tag aus mehreren Images gleichzeitig löschen, indem Sie jedes Image im Befehl mit einem Leerzeichen zwischen den einzelnen Namen auflisten. `IMAGE` muss dasselbe Format wie `repository:tag` haben, z. B. `us.icr.io/namespace/image:latest`.

<p>Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Wenn im Imagenamen kein Tag angegeben ist, schlägt der Befehl fehl.</p>

</dd>
</dl>

**Beispiel**

Entfernen Sie das Tag `1` aus dem Image `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-untag us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

Zeigt den Namen und das Konto der Registry an, bei der Sie angemeldet sind.

```
ibmcloud cr info
```
{: codeblock}

**Voraussetzungen**

Keine

## `ibmcloud cr login`
{: #bx_cr_login}

Dieser Befehl führt den Befehl `docker login` für die Registry aus. Der Befehl `docker login` muss den Befehl `docker push` oder `docker pull` für die Registry ausführen können. Dieser Befehl ist nicht erforderlich, um andere `ibmcloud cr`-Befehle auszuführen. Wenn Docker nicht installiert ist, gibt dieser Befehl eine Fehlernachricht zurück.

```
ibmcloud cr login
```
{: codeblock}

**Voraussetzungen**

Keine

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Wählen Sie einen Namen für Ihren Namensbereich aus und fügen Sie ihn Ihrem {{site.data.keyword.cloud_notm}}-Konto hinzu.

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Der hinzuzufügende Namensbereich. Der Namensbereich muss in allen {{site.data.keyword.cloud_notm}}-Konten derselben Region eindeutig sein. Namensbereiche müssen 4 bis 30 Zeichen lang sein und dürfen nur Kleinbuchstaben, Zahlen, Bindestriche (-) und Unterstreichungszeichen (_) enthalten. Namensbereiche müssen mit einem Buchstaben oder einer Zahl beginnen und enden.
  
<p>  
<strong>Wichtig</strong> Beziehen Sie keine personenbezogenen Daten in Ihre Namensbereichsnamen ein.
</p>
  
</dd>
</dl>

**Beispiel**

Erstellen Sie einen Namensbereich mit dem Namen *`birds`*.

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Zeigt alle Namensbereiche an, die Ihrem {{site.data.keyword.cloud_notm}}-Konto eigen sind.

```
ibmcloud cr namespace-list
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Entfernt einen Namensbereich aus Ihrem {{site.data.keyword.cloud_notm}}-Konto. Images in diesem Namensbereich werden gelöscht, wenn der Namensbereich entfernt wird.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Der zu entfernende Namensbereich.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Optional) Ausführung des Befehls ohne Benutzereingabeaufforderungen erzwingen.</dd>
</dl>

**Beispiel**

Entfernen Sie den Namensbereich *`birds`*.

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

Zeigt Ihren Preistarif für die von Ihnen anvisierte Registry-Region an.

```
ibmcloud cr plan
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Führt ein Upgrade auf den Standardplan für die von Ihnen anvisierte Registry-Region durch.

Weitere Informationen zu den Plänen finden Sie unter [Registry-Pläne](/docs/services/Registry?topic=registry-registry_overview#registry_plans).

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`PLAN`</dt>
<dd>(Optional) Der Name des Preisstrukturplans, auf den Sie ein Upgrade durchführen möchten. Wenn `PLAN` nicht angegeben ist, wird standardmäßig `standard` verwendet.</dd>
</dl>

**Beispiel**

Führen Sie ein Upgrade auf den Standardpreisstrukturplan durch.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

Importiert {{site.data.keyword.IBM_notm}} Software, die von [IBM Passport Advantage Online für Kunden ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/pao_customer.html) heruntergeladen und für die Verwendung mit Helm paketiert wurde, in den {{site.data.keyword.registrylong_notm}}-Namensbereich.

Container-Images werden mit Push-Operation in Ihren privaten {{site.data.keyword.registryshort_notm}}-Namensbereich übertragen. Helm-Diagramme werden in ein Verzeichnis `ppa-import` geschrieben, das in dem Verzeichnis erstellt wird, in dem Sie den Befehl ausführen. Optional können Sie das [Open-Source-Projekt ChartMuseum ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/helm/charts/tree/master/stable/chartmuseum) verwenden, um Helm-Diagramme zu hosten.

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>Der Pfad zu der komprimierten Datei, die von IBM Passport Advantage heruntergeladen wird.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>Einer Ihrer Namensbereiche. Container-Images aus der komprimierten Datei werden mit Push-Operation in diesen Namensbereich übertragen. Zum Auflisten von Namensbereichen führen Sie den Befehl `ibmcloud cr namespace-list` aus.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Optional) Die eindeutige Ressourcen-ID für Ihr [ChartMuseum ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(Optional) Der Benutzername für Ihr [ChartMuseum ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(Optional) Das Kennwort für Ihr [ChartMuseum ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
</dl>

**Beispiel**

Importieren Sie IBM Software und packen Sie sie für die Verwendung mit Helm in den {{site.data.keyword.registrylong_notm}}-Namensbereich *`birds`*, wobei der Pfad der komprimierten Datei *`downloads/komprimierte_datei.tgz`* lautet.

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

Zeigt Ihre aktuellen Kontingente für Datenverkehr und Speicher sowie Informationen zu diesen Kontingenten für die Registry-Region an, die Sie anvisieren.

```
ibmcloud cr quota
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Ändern Sie das angegebene Kontingent für die von Ihnen anvisierte Registry-Region.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(Optional) Ändert das Kontingent für Ihren Datenverkehr in den angegebenen Wert in Megabyte. Die Operation schlägt fehl, wenn Sie zum Festlegen des Datenverkehrs nicht berechtigt sind oder wenn Sie einen Wert festlegen, der Ihren aktuellen Preisstrukturplan übersteigt.</dd>
<dt>`--storage STORAGE`</dt>
<dd>(Optional) Ändert das Kontingent für Ihren Speicher in den angegebenen Wert in Megabyte. Die Operation schlägt fehl, wenn Sie zum Festlegen des Speichers nicht berechtigt sind oder wenn Sie einen Wert festlegen, der Ihren aktuellen Preisstrukturplan übersteigt.</dd>
</dl>

**Beispiel**

Legen Sie Ihren Grenzwert für das Pull-Datenverkehrskontingent auf *7000* MB fest und für den Speicher auf *600* MB.

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

Zeigt die als Ziel gewählte Region und Registry an.

```
ibmcloud cr region
```
{: codeblock}

**Voraussetzungen**

Keine

Weitere Informationen finden Sie unter [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Legt eine Zielregion für die {{site.data.keyword.registrylong_notm}}-Befehle fest. Um die verfügbaren Regionen aufzulisten, führen Sie den Befehl ohne Parameter aus.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**Voraussetzungen**

Keine

**Befehlsoptionen**
<dl>
<dt>`REGION`</dt>
<dd>(Optional) Der Name Ihrer Zielregion, z. B. `us-south`.

Weitere Informationen finden Sie unter [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

</dd>
</dl>

**Beispiel**

Richten Sie die Region 'Vereinigte Staaten (Süden)' (us-south) als Zielregion ein.

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

Ruft das angegebene Token aus der Registry ab.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**Voraussetzungen**

[Plattformmanagementrollen](/docs/services/Registry?topic=registry-iam#platform_management_roles) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`TOKEN`</dt>
<dd>Die eindeutige ID des Tokens, das abgerufen werden soll. Zum Auflisten Ihrer Tokens führen Sie den Befehl `ibmcloud cr token-list` aus.</dd>
</dl>

**Beispiel**

Rufen Sie das Token *1010101010-101x-1x10-x1xx-x10xx10xxx10* ab.

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

Zeigt alle Tokens an, die für Ihr {{site.data.keyword.cloud_notm}}-Konto vorhanden sind.

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**Voraussetzungen**

[Plattformmanagementrollen](/docs/services/Registry?topic=registry-iam#platform_management_roles) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen finden Sie unter [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
</dl>

**Beispiel**

Zeigen Sie alle Token an, die schreibgeschützt sind, indem Sie die Formatierungsanweisung *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`* verwenden.

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

In diesem Beispiel wird eine Ausgabe im folgenden Format erzeugt.

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

Ein oder mehrere angegebene Registry-Tokens entfernen.

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**Voraussetzungen**

[Plattformmanagementrollen](/docs/services/Registry?topic=registry-iam#platform_management_roles) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`TOKEN`</dt>
<dd>(Optional) TOKEN kann entweder das Token selbst oder die eindeutige ID des Tokens sein, wie in `ibmcloud cr token-list` dargestellt. Mehrere Tokens können angegeben werden, wobei sie durch ein Leerzeichen getrennt sein müssen.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Optional) Ausführung des Befehls ohne Benutzereingabeaufforderungen erzwingen.</dd>
</dl>

**Beispiel**

Entfernen Sie das Token *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

Zeigt einen Schwachstellenanalysebericht für Ihre Images an.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Voraussetzungen**

[Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using) enthält weitere Informationen zu den erforderlichen Berechtigungen.

**Befehlsoptionen**
<dl>
<dt>`IMAGE`</dt>
<dd>Der Name des Images, für das ein Bericht erstellt werden soll. Der Bericht enthält Informationen darüber, ob das Image-Paket bekannte Sicherheitslücken aufweist. Sie können Berichte für mehrere Images gleichzeitig anfordern, indem Sie jedes Image im Befehl mit einem Leerzeichen zwischen den einzelnen Namen auflisten.

<p>Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Wenn im Imagenamen kein Tag angegeben ist, beurteilt der Bericht das Image mit dem Tag `latest`.</p>

<p>Folgende Betriebssysteme werden unterstützt:

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

Weitere Informationen finden Sie unter [Imagesicherheit mit Vulnerability Advisor verwalten](/docs/services/va?topic=va-va_index).

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Optional) Die Befehlsausgabe zeigt zusätzliche Informationen zu Fixes für anfällige Pakete an.</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Optional) Die Befehlsausgabe ist auf die Anzeige von Sicherheitslücken beschränkt.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Optional) Die Befehlsausgabe ist auf die Anzeige von Konfigurationsproblemen beschränkt.</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(Optional) Die Befehlsausgabe wird im ausgewählten Format zurückgegeben. Das Standardformat ist `text`. Folgende Formate werden unterstützt:

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**Beispiele**

Zeigt einen standardmäßigen Schwachstellenanalysebericht für Ihr Image an.

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

Zeigen Sie einen Schwachstellenanalysebericht für Ihr Image `us.icr.io/birds/bluebird:1` im JSON-Format an, der nur Sicherheitslücken angibt.

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
