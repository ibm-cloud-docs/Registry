---

copyright:
  years: 2017
lastupdated: "2017-10-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# Fehlerbehebung
{: #ts_index}

Hier finden Sie Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von {{site.data.keyword.registrylong}}.
{:shortdesc}


## Hilfe und Unterstützung für {{site.data.keyword.registrylong_notm}} anfordern
{: #gettinghelp}

Wenn bei der Verwendung von {{site.data.keyword.registrylong_notm}} Fragen oder Probleme auftreten, können Sie Hilfe erhalten, indem Sie nach Informationen suchen oder Fragen über ein Forum stellen. Sie können auch ein {{site.data.keyword.IBM_notm}} Support-Ticket öffnen.

Wenn Sie eine Frage in einem Forum stellen, kennzeichnen Sie Ihre Frage, sodass sie von den {{site.data.keyword.registrylong_notm}}-Entwicklungsteams gesehen wird.

-   Wenn Sie technische Fragen zur Entwicklung oder Bereitstellung einer App mit {{site.data.keyword.registrylong_notm}} haben, posten Sie Ihre Frage unter [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) und kennzeichnen Sie Ihre Frage mit `ibm-bluemix` und `container-registry`.
-   Bei Fragen zum Service sowie zu einführenden Anweisungen nutzen Sie das Forum [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Schließen Sie die Tags `bluemix` und `container-registry` dabei ein.

Weitere Informationen zur Verwendung der Foren finden Sie unter [Hilfe aufrufen](../../support/index.html#getting-help).

Informationen zum Öffnen eines {{site.data.keyword.IBM_notm}} Support-Tickets oder zu Supportstufen und Prioritätsstufen von Tickets finden Sie unter [Support kontaktieren](../../support/index.html#contacting-support).

## Anmeldung bei {{site.data.keyword.registrylong_notm}} fehlgeschlagen
{: #ts_login}

Sie können sich bei {{site.data.keyword.registrylong_notm}} nicht anmelden.

{: tsSymptoms}
Der Befehl `bx cr login` ist fehlschlagen.

{: tsCauses}
-   Das Container-Registry-Plug-in ist veraltet und muss aktualisiert werden.
-   Docker ist auf Ihrer lokalen Maschine nicht installiert oder wird nicht ausgeführt.
-   Ihre {{site.data.keyword.Bluemix_notm}}-Anmeldeberechtigungsnachweise sind abgelaufen.

{: tsResolve}
Sie können dieses Problem wie folgt beheben:

-   Führen Sie ein Upgrade auf die neueste Version des {{site.data.keyword.registryshort_notm}}-Plug-ins durch. Informationen dazu enthält der Abschnitt [{{site.data.keyword.registrylong_notm}}-Plug-in (`bx cr`) aktualisieren](registry_setup_cli_namespace.html#registry_cli_update).
-   Stellen Sie sicher, dass Docker auf Ihrer Maschine installiert ist. Wenn das Programm bereits installiert ist, starten Sie den Docker-Dämon erneut.
-   Führen Sie den Befehl `bx login` erneut aus, um Ihre {{site.data.keyword.Bluemix_notm}}-Anmeldeberechtigungsnachweise zu aktualisieren.


## {{site.data.keyword.registrylong_notm}}-Befehle schlagen fehl mit der Nachricht `'cr' ist kein registrierter Befehl. Siehe 'bx help'. `
{: #ts_login_error}

Sie können einen `bx cr`-Befehl nicht ausführen, da `cr` kein registrierter `bx`-Befehl ist.

{: tsSymptoms}
Es wird eine Fehlernachricht ähnlich einer der folgenden Fehlernachrichten angezeigt: 

```
bx cr login
'cr' ist kein registrierter Befehl. Siehe 'bx help'.
```
{: pre}

```
bx cr namespace
'cr' ist kein registrierter Befehl. Siehe 'bx help'.
```
{: pre}

{: tsCauses}
-   Das Container-Registry-Plug-in ist nicht installiert.


{: tsResolve}
Sie können dieses Problem wie folgt beheben:

-   Installieren Sie das Container-Registry-Plug-in. Informationen dazu finden Sie im Abschnitt [CLI-Plug-in (bx cr) für {{site.data.keyword.registryshort_notm}} installieren](registry_setup_cli_namespace.html#registry_cli_install).


## Einrichtung eines Namensbereichs schlägt fehl
{: #ts_problem}

{: tsSymptoms}
Wenn Sie den Befehl `bx cr namespace-add` ausführen, können Sie Ihren eingegebenen Wert nicht als Namensbereich festlegen.

{: tsCauses}
-   Sie haben einen Namensbereichswert eingegeben, der bereits von einer anderen {{site.data.keyword.Bluemix_notm}}-Organisation verwendet wird.
-   Ein Namensbereich wurde kürzlich gelöscht und Sie verwenden seinen Namen wieder. Wenn der Namensbereich, der gelöscht wurde, viele Ressourcen enthielt, wurde die Löschung möglicherweise noch nicht vollständig von {{site.data.keyword.registrylong_notm}} verarbeitet.
-   Sie haben im Namensbereichswert ungültige Zeichen verwendet.

{: tsResolve}
Sie können dieses Problem wie folgt beheben:

-   Befolgen Sie die Anweisungen, die in der zurückgegebenen Fehlernachricht angezeigt werden.
-   Prüfen Sie, ob Sie einen gültigen Namensbereich eingegeben haben:
    -   Der Name muss 4 bis 30 Zeichen lang sein.
    -   Der Name muss mit mindestens einem Buchstaben bzw. einer Ziffer beginnen.
    -   Der Name darf ausschließlich Kleinbuchstaben, Ziffern oder Unterstreichungszeichen (_) enthalten.
-   Wählen Sie einen anderen Wert für Ihren Namensbereich.
-   Wenn Sie einen Namensbereich, der viele Images enthielt und gelöscht wurde, neu erstellen, versuchen Sie es zu einem späteren Zeitpunkt erneut.

## Push- oder Pull-Operation für ein Docker-Image schlägt fehl
{: #ts_pushpull}

{: tsSymptoms}
Wenn Sie Befehle für Push- oder Pull-Operationen für Docker-Images ausführen, erhalten Sie eine Fehlernachricht. Der Inhalt der Fehlernachricht richtet sich nach der Ursache. Mögliche Fehlernachrichten können sein:

```
Sie haben Ihr Speicherkontingent überschritten. Löschen Sie mindestens ein Image oder prüfen Sie Ihr Kontingent und Ihren Preistarif
```
{: screen}

```
Sie haben Ihr Pull-Datenverkehrkontingent für den aktuellen Monat überschritten. Prüfen Sie Ihr Pull-Datenverkehrkontingent und den Preistarif
```
{: screen}

```
Berechtigung nicht vorhanden: Authentifizierung erforderlich
```
{: screen}

```
Zugriff verweigert: Angeforderter Zugriff auf die Ressource wurde verweigert
```
{: screen}

{: tsCauses}
-   Docker ist nicht installiert.
-   Der Docker-Client ist nicht bei {{site.data.keyword.registrylong_notm}} angemeldet.
-   Ihr {{site.data.keyword.Bluemix_notm}}-Zugriffstoken ist möglicherweise abgelaufen.
-   Sie haben das Kontingent für den Speicher oder Pull-Datenverkehr überschritten, das für Ihr {{site.data.keyword.Bluemix_notm}}-Konto festgelegt ist.

{: tsResolve}
Sie können dieses Problem wie folgt beheben:

-   [Stellen Sie sicher, dass Docker auf Ihrer Maschine installiert ist](index.html#registry_cli_install).
-   Prüfen Sie Ihren Docker-Installationspfad.
-   Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an, indem Sie den Befehl `bx login` ausführen. Melden Sie sich anschließend bei der {{site.data.keyword.registrylong_notm}}-CLI an, indem Sie `bx cr login` ausführen.
-   [Überprüfen Sie Kontingente und Nutzung zum Speichern und für Pull-Operationen von Docker-Images in {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).

## Das neueste Image kann nicht mit dem neuesten Tag extrahiert werden
{: #ts_docker_latest}

{: tsSymptoms}
Sie versuchen, den Befehl `docker pull` auszuführen, aber er gibt eine Version Ihres Image zurück, die nicht die zuletzt erstellte Version darstellt.

{: tsCauses}
Der Tag `latest` wird standardmäßig für den Verweis auf ein Image angewandt, wenn Sie Docker-Befehle ausführen, ohne einen Tagwert anzugeben. Der Tag `latest` wird auf den letzten `docker build`- oder `docker tag`-Befehl angewandt, der ausgeführt wurde, ohne dass ein Tag explizit festgelegt wurde. Daher ist es möglich, `docker`-Befehle in falscher Reihenfolge auszuführen oder Tags für einige Images explizit festzulegen, und der Tag `latest` kann ein Build angeben, das nicht das aktuellste ist.

{: tsResolve}
In der Regel ist es besser, jedes Mal explizit einen anderen sequenziellen Tag für Ihre Images zu definieren und sich nicht auf den Tag `latest` zu verlassen.

## Zugriff auf die Registry über eine angepasste Firewall schlägt fehl
{: #ts_firewall}

{: tsSymptoms}
Sie haben in Ihrer Entwicklungsumgebung eine zusätzliche Firewall mit angepassten Einstellungen für den ankommenden und abgehenden Netzdatenverkehr eingerichtet. Beim Versuch, auf {{site.data.keyword.registrylong_notm}} zuzugreifen, schlägt die Verbindung fehl.

{: tsCauses}
Für die angepasste Firewall ist es erforderlich, dass bestimmte Netzgruppen für den ankommenden und abgehenden Netzdatenverkehr geöffnet werden, damit die Kommunikation mit der Registry möglich ist.

{: tsResolve}
Öffnen Sie die folgenden Netzgruppen in der angepassten Firewall.

1.  Notieren Sie sich die öffentliche IP-Adresse der Maschine, die für die Verbindung zu {{site.data.keyword.registrylong_notm}} verwendet werden soll. Wenn Sie Kubernetes nutzen, verwenden Sie die öffentliche IP-Adresse des Workerknotens. Rufen Sie die öffentliche IP-Adresse des Workerknotens ab, indem Sie `bx cs workers <cluster_name_or_id>` ausführen. Dabei steht *&lt;cluster_name_or_id&gt;* für den Namen oder die ID Ihres Clusters.
2.  Lassen Sie in der Firewall die folgenden Verbindungen zu und von der verwendeten Maschine zu:
    -   Für die Konnektivität der bei Ihrer Maschine ankommenden Daten lassen Sie den ankommenden Netzdatenverkehr von den folgenden Quellennetzgruppen zur öffentlichen Ziel-IP-Adresse Ihrer Maschine zu.

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   Für die Konnektivität der von Ihrer Maschine abgehenden Daten verwenden Sie dieselben Netzgruppen und lassen Sie den abgehenden Netzdatenverkehr von der öffentlichen Quellen-IP-Adresse Ihrer Maschine zu diesen Netzgruppen zu.

