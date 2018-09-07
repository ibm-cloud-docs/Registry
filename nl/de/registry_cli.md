---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-21"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

Sie können die {{site.data.keyword.registrylong}}-CLI, die im Container-Registry-Plug-in bereitgestellt wird, verwenden, um Ihre Registry und die zugehörigen Ressourcen für Ihr {{site.data.keyword.Bluemix_notm}}-Konto zu verwalten.
{: shortdesc}

**Voraussetzungen**
* Bevor Sie die Registry-Befehle ausführen, melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an, wobei Sie den Befehl `ibmcloud login` verwenden, um ein Zugriffstoken zu generieren und Ihre Sitzung zu authentifizieren.

Informationen zur Verwendung der {{site.data.keyword.registrylong_notm}}-CLI finden Sie unter [Erste Schritte mit {{site.data.keyword.registrylong_notm}}](index.html).

Beziehen Sie keine personenbezogenen Daten in Ihre Container-Images, Namensbereichsnamen, Beschreibungsfelder (z. B. in Registry-Tokens) oder in Image-Konfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) ein.
{:tip}


<table summary="{{site.data.keyword.registrylong_notm}}"> verwalten
<caption>Tabelle 1. Befehle für die Verwaltung von {{site.data.keyword.registrylong_notm}}
</caption>
 <thead>
 <th colspan="5">Befehle für die Verwaltung der Registry</th>
 </thead>
 <tbody>
 <tr>
 <td>[`ibmcloud cr api`](#bx_cr_api)</td>
 <td>[`ibmcloud cr build`](#bx_cr_build)</td>
 <td>[`ibmcloud cr exemption-add`](#bx_cr_exemption_add)</td>
 <td>[`ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)](#bx_cr_exemption_list)</td>
 <td>[`ibmcloud cr exemption-rm`](#bx_cr_exemption_rm)</td>
 </tr>
 <tr>
 <td>[`ibmcloud cr exemption-types`](#bx_cr_exemption_types)</td>
 <td>[`ibmcloud cr info`](#bx_cr_info)</td>
 <td>[`ibmcloud cr image-inspect`](#bx_cr_image_inspect)</td>
 <td>[`ibmcloud cr image-list` (`ibmcloud cr images`)](#bx_cr_image_list)</td>
 <td>[`ibmcloud cr image-rm`](#bx_cr_image_rm)</td>
  </tr>
 <tr>
 <td>[`ibmcloud cr login`](#bx_cr_login)</td>
 <td>[`ibmcloud cr namespace-add`](#bx_cr_namespace_add)</td>
 <td>[`ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)](#bx_cr_namespace_list)</td>
 <td>[`ibmcloud cr namespace-rm`](#bx_cr_namespace_rm)</td>
 <td>[`ibmcloud cr plan`](#bx_cr_plan)</td>
 </tr>
 <tr>
 <td>[`ibmcloud cr plan-upgrade`](#bx_cr_plan_upgrade)</td>
 <td>[`ibmcloud cr ppa-archive-load`](#bx_cr_ppa_archive_load)</td>
 <td>[`ibmcloud cr quota`](#bx_cr_quota)</td>
 <td>[`ibmcloud cr quota-set`](#bx_cr_quota_set)</td>
 <td>[`ibmcloud cr region`](#bx_cr_region)</td>
 </tr><tr>
 <td>[`ibmcloud cr region-set`](#bx_cr_region_set)</td>
 <td>[`ibmcloud cr token-add`](#bx_cr_token_add)</td>
 <td>[`ibmcloud cr token-get`](#bx_cr_token_get)</td>
 <td>[`ibmcloud cr token-list` (`ibmcloud cr tokens`)](#bx_cr_token_list)</td>
 <td>[`ibmcloud cr token-rm`](#bx_cr_token_rm)</td>
  </tr><tr>
  <td>[`ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)](#bx_cr_va)</td>
 </tr>
 </tbody></table>



## `ibmcloud cr api`
{: #bx_cr_api}

Gibt die Details zum Registry-API-Endpunkt zurück, für den die Befehle ausgeführt werden.

```
ibmcloud cr api
```
{: codeblock}


## `ibmcloud cr build`
{: #bx_cr_build}

Erstellt ein Docker-Image in {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Parameter**
<dl>
<dt>`DIRECTORY`</dt>
<dd>Die Position für Ihren Buildkontext, der Ihre Dockerfile und vorausgesetzte Dateien enthält.</dd>
<dt>`--no-cache`</dt>
<dd>(Optional)  Ist dies angegeben, werden zwischengespeicherte Image-Ebenen aus vorherigen Builds nicht in diesem Build verwendet.</dd>
<dt>`--pull`</dt>
<dd>(Optional) Ist dies angegeben, werden die Basisimages auch dann mit Pull-Operation extrahiert, wenn ein Image mit einem übereinstimmenden Tag bereits im Build-Host vorhanden ist.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Ist dies angegeben, wird die Buildausgabe unterdrückt, solange kein Fehler auftritt.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(Optional) Geben Sie ein zusätzliches Buildargument im Format 'KEY=VALUE' an. Mehrere Buildargumente können angegeben werden, indem dieser Parameter mehrfach eingeschlossen wird. Der Wert jedes Buildarguments ist als Umgebungsvariable verfügbar, wenn Sie eine ARG-Zeile angeben, die mit dem Schlüssel in Ihrer Dockerfile übereinstimmt.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(Optional)  Wenn Sie dieselben Dateien für mehrere Builds verwenden, können Sie einen Pfad zu einer anderen Dockerfile wählen. Geben Sie die Position der Dockerfile relativ zum Buildkontext an. Wenn nicht angegeben, wird standardmäßig `PATH/Dockerfile` verwendet, wobei PATH der Root des Buildkontextes ist.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>Der vollständige Name für das zu erstellende Image, in dem die Registry-URL und der Namensbereich enthalten sind.</dd>
</dl>


## `ibmcloud cr info`
{: #bx_cr_info}

Zeigt den Namen und das Konto der Registry an, bei der Sie angemeldet sind.

```
ibmcloud cr info
```
{: codeblock}


## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Erstellt eine Freistellung für ein Sicherheitsproblem. Sie können eine Freistellung für ein Sicherheitsproblem erstellen, das für verschiedene Bereiche gilt. Der Bereich kann das Konto, der Namensbereich, das Repository oder der Tag sein. 

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Parameter**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Um Ihr Konto als Bereich zu definieren, verwenden Sie `"*"` als Wert. Um einen Namensbereich, ein Repository oder Tag als Bereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namespace`, `namespace/repository`, `namespace/repository:tag`.
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Der Typ des Sicherheitsproblems, das Sie freistellen möchten. Um nach gültigen Problemtypen zu suchen, führen Sie den Befehl `ibmcloud cr exemption-types` aus.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>Die ID des Sicherheitsproblems, das Sie freistellen möchten. Um nach einer Problem-ID zu suchen, führen Sie den Befehl `ibmcloud cr va <image>`, wobei *&lt;image&gt;* der Name des Image ist. Verwenden Sie dabei den entsprechenden Wert aus der Spalte mit der **Schwachstellen-ID** oder der Spalte mit der **Konfigurationsproblem-ID**.
</dd>
</dl>


## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

Listet die Freistellungen für Sicherheitsprobleme auf. 

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**Parameter**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(Optional) Listet nur die Freistellungen auf, die für diesen Bereich gelten. Um einen Namensbereich, ein Repository oder Tag als Bereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namespace`, `namespace/repository`, `namespace/repository:tag`.
</dd>
</dl>


## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Löscht eine Freistellung für ein Sicherheitsproblem. Um Ihre vorhandenen Freistellungen anzuzeigen, führen Sie den Befehl `ibmcloud cr exemption-list` aus.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Parameter**
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


## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Listet die Typen der Sicherheitsprobleme auf, die Sie freistellen können.

```
ibmcloud cr exemption-types
```
{: codeblock}


## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Zeigt Details zu einem bestimmten Image an.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Parameter**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen finden Sie unter [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>`IMAGE`</dt>
<dd>Der Name des Image, für das ein Bericht erstellt werden soll. Sie können mehrere Images untersuchen, indem Sie die einzelnen Images im Befehl mit einem Leerzeichen zwischen den einzelnen Namen auflisten.

<p>Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Wenn im Imagenamen kein Tag angegeben ist, wird das Image mit dem Tag `latest` untersucht. </p>

</dd>
</dl>


## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Zeigt alle Images in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

Der Imagename ist eine Kombination des Inhalts der Spalten <strong>Repository</strong> und <strong>Tag</strong> im Format `repository:tag`.
{:tip}

```
 ibmcloud cr image-list [--no-trunc] [--format FORMAT] [-q, --quiet] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Parameter**
<dl>
<dt>`--no-trunc`</dt>
<dd>(Optional) Schneidet die Image-Auszüge nicht ab.</dd>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen finden Sie unter [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>`-q`, `--quiet`</dt>
<dd>(Optional) Jedes Image wird im Format `repository:tag` aufgelistet.</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Optional) Begrenzen Sie die Ausgabe, sodass nur Images im angegebenen Namensbereich oder Namensbereich und Repository angezeigt werden. </dd>
<dt>`--include-ibm`</dt>
<dd>(Optional) Enthält von {{site.data.keyword.IBM_notm}} bereitgestellte öffentliche Images in der Ausgabe. Ohne diese Option werden standardmäßig nur private Images aufgelistet.</dd>
</dl>



## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Löscht ein oder mehrere angegebene Images aus Ihrer Registry.

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Parameter**
<dl>
<dt>`IMAGE`</dt>
<dd>Der Name des Image, für das ein Bericht erstellt werden soll. Sie können mehrere Images gleichzeitig löschen, indem Sie jedes Image im Befehl mit einem Leerzeichen zwischen den einzelnen Namen auflisten.

<p>Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Wenn im Imagenamen kein Tag angegeben ist, wird das Image mit dem Tag `latest` gelöscht.</p>

</dd>
</dl>


## `ibmcloud cr login`
{: #bx_cr_login}

Dieser Befehl führt den Befehl `docker login` für die Registry aus. Der Befehl `docker login` muss den Befehl `docker push` oder `docker pull` für die Registry ausführen können. Dieser Befehl ist nicht erforderlich, um andere `ibmcloud cr`-Befehle auszuführen. Wenn Docker nicht installiert ist, gibt dieser Befehl eine Fehlernachricht zurück.

```
ibmcloud cr login
```
{: codeblock}


## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Fügt Ihrem {{site.data.keyword.Bluemix_notm}}-Konto einen Namensbereich hinzu.

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**Parameter**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Der hinzuzufügende Namensbereich. Der Namensbereich muss in allen {{site.data.keyword.Bluemix_notm}}-Konten derselben Region eindeutig sein.
  
<p>  
<strong>Tipp</strong>: Beziehen Sie keine personenbezogenen Daten in Ihre Namensbereichsnamen ein.
</p>
  
</dd>
</dl>


## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Zeigt alle Namensbereiche an, die Ihrem {{site.data.keyword.Bluemix_notm}}-Konto eigen sind.

```
ibmcloud cr namespace-list
```
{: codeblock}


## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Entfernt einen Namensbereich aus Ihrem {{site.data.keyword.Bluemix_notm}}-Konto. Images in diesem Namensbereich werden gelöscht, wenn der Namensbereich entfernt wird.

```
ibmcloud cr namespace-rm NAMESPACE
```
{: codeblock}

**Parameter**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Der zu entfernende Namensbereich.</dd>
</dl>


## `ibmcloud cr plan`
{: #bx_cr_plan}

Zeigt Ihren Preisstrukturplan an.

```
ibmcloud cr plan
```
{: codeblock}


## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Führt ein Upgrade auf den Standardplan durch.

Informationen zu den Plänen finden Sie unter [Registry-Pläne](registry_overview.html#registry_plans).

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**Parameter**
<dl>
<dt>`PLAN`</dt>
<dd>Der Name des Preisstrukturplans, auf den ein Upgrade durchgeführt werden soll. Wenn `PLAN` nicht angegeben ist, wird standardmäßig `standard` verwendet.</dd>
</dl>


## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

Importiert IBM Software, die von [IBM Passport Advantage Online für Kunden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/pao_customer.html) heruntergeladen und für die Verwendung mit Helm paketiert wurde, in den Namensbereich Ihrer privaten Registry.

Container-Images werden mit Push-Operation in Ihren privaten {{site.data.keyword.registryshort_notm}}-Namensbereich übertragen. Helm-Diagramme werden in ein Verzeichnis `ppa-import` geschrieben, das in dem Verzeichnis erstellt wird, in dem Sie den Befehl ausführen. Optional können Sie das [Open-Source-Projekt ChartMuseum ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) verwenden, um Helm-Diagramme zu hosten.

**Beispielbefehl**

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Parameter**:
<dl>
  <dt>`--archive FILE`</dt>
  <dd>Der Pfad zu der komprimierten Datei, die von IBM Passport Advantage heruntergeladen wird.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>Einer Ihrer Namensbereiche. Container-Images aus der komprimierten Datei werden mit Push-Operation in diesen Namensbereich übertragen. Zum Auflisten von Namensbereichen führen Sie den Befehl `ibmcloud cr namespace-list` aus.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Optional) Die eindeutige Ressourcen-ID für Ihr [ChartMuseum ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(Optional) Der Benutzername für Ihr [ChartMuseum ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(Optional) Das Kennwort für Ihr [ChartMuseum ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
</dl>


## `ibmcloud cr quota`
{: #bx_cr_quota}

Zeigt Ihre aktuellen Kontingente für Datenverkehr und Speicher sowie Informationen zu diesen Kontingenten an.

```
ibmcloud cr quota
```
{: codeblock}


## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Modifiziert das angegebene Kontingent.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Parameter**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(Optional) Ändert das Kontingent für Ihren Datenverkehr in den angegebenen Wert in Megabyte. Die Operation schlägt fehl, wenn Sie zum Festlegen des Datenverkehrs nicht berechtigt sind oder wenn Sie einen Wert festlegen, der Ihren aktuellen Preisstrukturplan übersteigt.</dd>
<dt>`--storage STORAGE`</dt>
<dd>(Optional) Ändert das Kontingent für Ihren Speicher in den angegebenen Wert in Megabyte. Die Operation schlägt fehl, wenn Sie zum Festlegen des Speichers nicht berechtigt sind oder wenn Sie einen Wert festlegen, der Ihren aktuellen Preisstrukturplan übersteigt.</dd>
</dl>


## `ibmcloud cr region`
{: #bx_cr_region}

Zeigt die als Ziel gewählte Region und Registry an.

```
ibmcloud cr region
```
{: codeblock}

Weitere Informationen finden Sie unter [Regionen](registry_overview.html#registry_regions).


## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Legt eine Zielregion für die {{site.data.keyword.registrylong_notm}}-Befehle fest. Um die verfügbaren Regionen aufzulisten, führen Sie den Befehl ohne Parameter aus.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**Parameter**
<dl>
<dt>`REGION`</dt>
<dd>(Optional) Der Name Ihrer Zielregion, z. B. `us-south`.

Weitere Informationen finden Sie unter [Regionen](registry_overview.html#registry_regions).

</dd>
</dl>


## `ibmcloud cr token-add`
{: #bx_cr_token_add}

Fügt ein Token hinzu, mit dem Sie den Zugriff auf eine Registry kontrollieren können.

```
ibmcloud cr token-add [--description DESCRIPTION] [-q, --quiet] [--non-expiring] [--readwrite]
```
{: codeblock}


**Parameter**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>(Optional) Gibt den Wert als Beschreibung für das Token an, das angezeigt wird, wenn Sie `ibmcloud cr token-list` ausführen. Wenn Ihr Token automatisch von {{site.data.keyword.containerlong_notm}} erstellt wird, wird die Beschreibung auf den Namen Ihres Kubernetes-Clusters festgelegt. In diesem Fall wird das Token automatisch entfernt, wenn Ihr Cluster entfernt wird.
  
<p> 
  <strong>Tipp</strong>: Beziehen Sie keine personenbezogenen Daten in Ihre Tokenbeschreibung ein.
</p>

  </dd>
<dt>`-q`, `--quiet`</dt>
<dd>(Optional) Zeigt nur das Token an, ohne einschließenden Text.</dd>
<dt>`--non-expiring`</dt>
<dd>(Optional) Erstellt ein Token mit zeitlich unbeschränkter Gültigkeit. Ist dieser Parameter nicht festgelegt, läuft der Zugriff von einem Token standardmäßig nach 24 Stunden ab.</dd>
<dt>`--readwrite`</dt>
<dd>(Optional) Erstellt ein Token, das Lese- und Schreibzugriff erteilt. Ohne diese Option ist der Zugriff standardmäßig schreibgeschützt.</dd>
</dl>


## `ibmcloud cr token-get`
{: #bx_cr_token_get}

Ruft das angegebene Token aus der Registry ab.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**Parameter**
<dl>
<dt>`TOKEN`</dt>
<dd>(Optional) Die eindeutige Kennung des Tokens, das abgerufen werden soll.</dd>
</dl>


## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

Zeigt alle Tokens an, die für Ihr {{site.data.keyword.Bluemix_notm}}-Konto vorhanden sind.

```
ibmcloud cr token-list --format FORMAT
```
{: codeblock}

**Parameter**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen finden Sie unter [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](registry_cli_reference.html#registry_cli_listing).

</dd>
</dl>


## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

Entfernt ein oder mehrere angegebene Tokens.

```
ibmcloud cr token-rm TOKEN [TOKEN...]
```
{: codeblock}

**Parameter**
<dl>
<dt>`TOKEN`</dt>
<dd>(Optional) TOKEN kann entweder das Token selbst oder die eindeutige Kennung des Tokens sein, wie in `ibmcloud cr token-list` dargestellt. Mehrere Tokens können angegeben werden, wobei sie durch ein Leerzeichen getrennt sein müssen.</dd>
</dl>


## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

Zeigt einen Schwachstellenanalysebericht für Ihre Images an.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Parameter**
<dl>
<dt>`IMAGE`</dt>
<dd>Der Name des Image, für das ein Bericht erstellt werden soll. Der Bericht enthält Informationen darüber, ob das Image-Paket bekannte Sicherheitslücken aufweist. Sie können Berichte für mehrere Images gleichzeitig anfordern, indem Sie jedes Image im Befehl mit einem Leerzeichen zwischen den einzelnen Namen auflisten.

<p>Um die Namen Ihrer Images zu ermitteln, führen Sie `ibmcloud cr image-list` aus. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Wenn im Imagenamen kein Tag angegeben ist, beurteilt der Bericht das Image mit dem Tag `latest`. </p>

<p>Folgende Betriebssysteme werden unterstützt:

<ul>

<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>

</p>

Weitere Informationen finden Sie unter [Imagesicherheit mit Vulnerability Advisor verwalten](/docs/services/va/va_index.html).

</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(Optional) Die Befehlsausgabe wird im ausgewählten Format zurückgegeben. Das Standardformat ist `text`. Folgende Formate werden unterstützt:

<ul>

<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Optional) Die Befehlsausgabe ist auf die Anzeige von Sicherheitslücken beschränkt.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Optional) Die Befehlsausgabe ist auf die Anzeige von Konfigurationsproblemen beschränkt.</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Optional) Die Befehlsausgabe zeigt zusätzliche Informationen zu Fixes für anfällige Pakete an.</dd>

</dl>
