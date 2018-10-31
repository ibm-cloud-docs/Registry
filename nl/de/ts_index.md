---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-07"

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

Weitere Informationen zur Verwendung der Foren finden Sie unter [Support Center nutzen](/docs/get-support/howtogetsupport.html#using-avatar).

Informationen zum Öffnen eines {{site.data.keyword.IBM_notm}} Support-Tickets oder zu Supportstufen und Prioritätsstufen von Tickets finden Sie unter [Benötigte Unterstützung anfordern](/docs/get-support/howtogetsupport.html#getting-customer-support). 

## Anmeldung bei {{site.data.keyword.registrylong_notm}} fehlgeschlagen
{: #ts_login}

Sie können sich bei {{site.data.keyword.registrylong_notm}} nicht anmelden.

{: tsSymptoms}
Der Befehl `ibmcloud cr login` schlägt fehl.

{: tsCauses}
-   Das Container-Registry-Plug-in ist veraltet und muss aktualisiert werden.
-   Docker ist auf dem lokalen Computer nicht installiert oder wird nicht ausgeführt.
-   Ihre {{site.data.keyword.Bluemix_notm}}-Anmeldeberechtigungsnachweise sind abgelaufen.

{: tsResolve}
Sie können dieses Problem wie folgt beheben:

-   Führen Sie ein Upgrade auf die neueste Version des Container-Registry-Plug-ins durch. Informationen hierzu finden Sie im Abschnitt [Container-Registry-Plug-in aktualisieren](registry_setup_cli_namespace.html#registry_cli_update).
-   Stellen Sie sicher, dass Docker auf Ihrem Computer installiert ist. Wenn das Programm bereits installiert ist, starten Sie den Docker-Dämon erneut.
-   Führen Sie den Befehl `ibmcloud login` erneut aus, um Ihre {{site.data.keyword.Bluemix_notm}}-Anmeldeberechtigungsnachweise zu aktualisieren.
  
## Die Ausführung jedes Befehls für {{site.data.keyword.registrylong_notm}} schlägt fehl mit der Meldung `FAILED You are not logged in to IBM Cloud. ` (FEHLGESCHLAGEN Sie sind nicht bei der IBM Cloud angemeldet). 
{: #ts_login_cloud}

Sie können in {{site.data.keyword.registrylong_notm}} keine Befehle ausführen, obwohl Sie bei {{site.data.keyword.Bluemix_notm}} angemeldet sind.

{: tsSymptoms}
Alle `ibmcloud cr`-Befehle schlagen fehl.

{: tsCauses}
-   Das Container-Registry-Plug-in ist veraltet und muss aktualisiert werden.

{: tsResolve}
Sie können dieses Problem wie folgt beheben:

-   Führen Sie ein Upgrade auf die neueste Version des Container-Registry-Plug-ins durch. Informationen hierzu finden Sie im Abschnitt [Container-Registry-Plug-in aktualisieren](registry_setup_cli_namespace.html#registry_cli_update).



## {{site.data.keyword.registrylong_notm}}-Befehle schlagen fehl mit der Nachricht `'cr' ist kein registrierter Befehl. Siehe 'ibmcloud help'. `
{: #ts_login_error}

Sie können einen `ibmcloud cr`-Befehl nicht ausführen, da `cr` kein registrierter `ibmcloud`-Befehl ist.

{: tsSymptoms}
Es wird eine Fehlernachricht ähnlich einer der folgenden Fehlernachrichten angezeigt:

```
ibmcloud cr login
'cr' ist kein registrierter Befehl. Siehe 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' ist kein registrierter Befehl. Siehe 'ibmcloud help'.
```
{: pre}

{: tsCauses}
-   Das Container-Registry-Plug-in ist nicht installiert.


{: tsResolve}
Sie können dieses Problem wie folgt beheben:

-   Installieren Sie das Container-Registry-Plug-in. Informationen hierzu finden Sie im Abschnitt [{{site.data.keyword.registryshort_notm}}-CLI installieren (Container-Registry-Plug-in)](registry_setup_cli_namespace.html#registry_cli_install).


## Einrichtung eines Namensbereichs schlägt fehl
{: #ts_problem}

{: tsSymptoms}
Wenn Sie `ibmcloud cr namespace-add` ausführen, können Sie den eingegebenen Wert nicht als Namensbereich festlegen.

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
Sie haben Ihr Speicherkontingent überschritten. Löschen Sie mindestens ein Image oder prüfen Sie Ihr Kontingent und Ihren Preisstrukturplan.
```
{: screen}

```
Sie haben Ihr Pull-Datenverkehrkontingent für den aktuellen Monat überschritten. 
Prüfen Sie Ihr Pull-Datenverkehrkontingent und den Preisstrukturplan.
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

-   [Stellen Sie sicher, dass Docker auf Ihrem Computer installiert ist](index.html#registry_cli_install).
-   Prüfen Sie Ihren Docker-Installationspfad.
-   Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an, indem Sie den Befehl `ibmcloud login` ausführen. Melden Sie sich anschließend bei der {{site.data.keyword.registrylong_notm}}-CLI an, indem Sie `ibmcloud cr login` ausführen.
-   [Überprüfen Sie Kontingente und Nutzung zum Speichern und für Pull-Operationen von Docker-Images in {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).


## Das neueste Image kann nicht mit dem Tag `latest` abgerufen werden
{: #ts_docker_latest}

{: tsSymptoms}
Sie versuchen, den Befehl `docker pull` auszuführen, aber er gibt eine Version Ihres Image zurück, die nicht die zuletzt erstellte Version darstellt.

{: tsCauses}
Der Tag `latest` wird standardmäßig für den Verweis auf ein Image angewandt, wenn Sie Docker-Befehle ausführen, ohne einen Tagwert anzugeben. Der Tag `latest` wird auf den `docker build`- oder `docker tag`-Befehl angewandt, der zuletzt ausgeführt wurde, ohne dass ein Tag explizit festgelegt wurde. Daher ist es möglich, `docker`-Befehle in falscher Reihenfolge auszuführen oder Tags für einige Images explizit festzulegen, und der Tag `latest` kann ein Build angeben, das nicht das aktuellste ist.

{: tsResolve}
In der Regel ist es besser, jedes Mal explizit einen anderen sequenziellen Tag für Ihre Images zu definieren und sich nicht auf den Tag `latest` zu verlassen.


## Es können keine weiteren IBM Images zur Registry hinzugefügt werden
{: #ts_ppa}


{: tsSymptoms}
Wenn Sie versuchen, Inhalt zu importieren, den Sie in anderen IBM Produkten verwendet haben, z. B. {{site.data.keyword.Bluemix_notm}} Private, können Sie Ihre Images und andere lizenzierte Software nicht von [IBM Passport Advantage ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/index.html) in der Registry speichern.

{: tsCauses}
Softwarepakete wie Images und Helm-Diagramme von IBM Passport Advantage müssen mit dem Befehl `ibmcloud cr ppa-archive-load` in die Registry importiert werden.

{: tsResolve}
Führen Sie zuvor Folgendes aus:
* Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an, indem Sie den Befehl `ibmcloud login [--sso]` ausführen.
* Melden Sie sich bei {{site.data.keyword.registrylong_notm}} an, indem Sie den Befehl `ibmcloud cr login` ausführen.
* [Wählen Sie die `kubectl`-CLI](/docs/containers/cs_cli_install.html#cs_cli_configure) als Ziel für Ihren Cluster aus.
* Wenn Sie Helm noch nicht in Ihrem Cluster eingerichtet haben, [richten Sie Helm jetzt in Ihrem Cluster ein](/docs/containers/cs_integrations.html#helm).
* Wenn Sie die Charts innerhalb Ihrer Organisation gemeinsam nutzen möchten, können Sie das [Open-Source-Projekt ChartMuseum ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) installieren. Anweisungen hierzu finden Sie in dieser [developerWorks-Anleitung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/).


### IBM Passport Advantage-Produkte für die Verwendung in {{site.data.keyword.Bluemix_notm}} importieren

1.  Rufen Sie die komprimierte Datei ab, die Sie von [IBM Passport Advantage![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/index.html) importieren möchten.

2.  Wählen Sie die Region aus, die Sie als Ziel verwenden möchten. Wenn Sie den Regionsnamen nicht kennen, führen Sie den Befehl ohne die Region aus und wählen Sie danach eine Region.

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

3.  Importieren Sie die komprimierte Archivdatei. Geben Sie den Pfad zur komprimierten Datei und den Registry-Namensbereich an, an den die Images mit Push-Operation übertragen werden sollen.

    ```
    ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namensbereich>
    ```
    {: pre}

    Dieser Befehl erweitert die komprimierte Datei, lädt enthaltene Images in Ihren lokalen Docker-Client und überträgt die Images dann mit Push-Operation an den Namensbereich in Ihrer Registry.
    
    Wenn Sie die Helm-Diagramme vom IBM Passport Advantage-Archiv in ein ChartMuseum hochladen möchten, schließen Sie die folgenden Optionen in den Befehl ein: `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **Beispielausgabe**
    
    ```
    user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

    OK
    ```
    {: screen}

4.  Wenn die komprimierte Datei Helm-Diagramme enthält, werden diese Diagramme in einem Archivverzeichnis mit dem Namen `ppa-import` angeordnet, das in Ihrem aktuellen Arbeitsverzeichnis erstellt wird. Öffnen Sie das Verzeichnis, um den Namen des Helm-Diagramms, `<helm_chart>`, abzurufen, und überprüfen Sie dann seine Werte.

    ```
    helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    Wenn Sie im vorherigen Schritt Charts in ein ChartMuseum hochgeladen haben, können Sie `helm inspect` zum Prüfen des Charts im ChartMuseum verwenden.
    {: tip}

5.  Konfigurieren Sie das Helm-Diagramm `<helm_chart>` entsprechend den Werten, die von dem Befehl `helm inspect values` ausgegeben werden.

6.  Implementieren Sie das Helm-Diagramm `<helm_chart>`, indem Sie den Befehl `helm install` verwenden. Bei Bedarf können Sie Werte im Chart überschreiben, indem Sie die Option `--set` verwenden.

    ```
    helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## Zugriff auf die Registry über eine angepasste Firewall schlägt fehl
{: #ts_firewall}

{: tsSymptoms}
Sie haben in Ihrer Entwicklungsumgebung eine zusätzliche Firewall mit angepassten Einstellungen für den ankommenden und abgehenden Netzdatenverkehr eingerichtet. Beim Versuch, auf {{site.data.keyword.registrylong_notm}} zuzugreifen, schlägt die Verbindung fehl.

{: tsCauses}
Für die angepasste Firewall ist es erforderlich, dass bestimmte Netzgruppen für den ankommenden und abgehenden Netzdatenverkehr geöffnet werden, damit die Kommunikation mit der Registry möglich ist.

{: tsResolve}
Öffnen Sie die folgenden Netzgruppen in der angepassten Firewall.

1.  Notieren Sie sich die öffentliche IP-Adresse des Computers, der für die Verbindung zu {{site.data.keyword.registrylong_notm}} verwendet werden soll. Wenn Sie Kubernetes nutzen, verwenden Sie die öffentliche IP-Adresse des Workerknotens. Rufen Sie die öffentliche IP-Adresse des Workerknotens ab, indem Sie `ibmcloud ks workers <cluster_name_or_id>` ausführen. Dabei steht *&lt;cluster_name_or_id&gt;* für den Namen oder die ID Ihres Clusters.
2.  Lassen Sie in der Firewall die folgenden Verbindungen zum und vom verwendeten Computer zu:
    -   Für die Konnektivität der bei Ihrem Computer ankommenden Daten lassen Sie den ankommenden Netzdatenverkehr von den folgenden Quellennetzgruppen zur öffentlichen Ziel-IP-Adresse Ihres Computers zu.

        `registry.bluemix.net`:

        ```
        169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

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

    -   Für die Konnektivität der von Ihrem Computer abgehenden Daten verwenden Sie dieselben Netzgruppen und lassen Sie den abgehenden Netzdatenverkehr von der öffentlichen Quellen-IP-Adresse Ihres Computers zu diesen Netzgruppen zu.


## Verlorene oder beeinträchtigte Schlüssel wiederherstellen
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
Wenn Sie [vertrauenswürdige Inhalte](registry_trusted_content.html) verwenden, können Sie vertrauenswürdige Images nicht mehr verwalten, weil Ihre Signierschlüssel verloren gegangen oder beeinträchtigt sind.

{: tsCauses}
Ihr Repository oder Rootschlüssel ist verloren gegangen oder beeinträchtigt.

{: tsResolve}
Ihre Optionen für die Wiederherstellung von verlorenen oder beeinträchtigten Schlüsseln sind vom Typ des Schlüssels abhängig - Repository oder Root:

*  Bei [Repository-Schlüsseln](#trustedcontent_lostrepokey) können Sie einen neuen Satz von Signierschlüsseln für das Repository generieren.
*  Bei [Rootschlüsseln](#trustedcontent_lostrootkey) können Sie die Löschung des Repositorys anfordern und ein neues Repository erstellen.


### Repository-Schlüssel
{: #trustedcontent_lostrepokey}

Wenn Ihr Repository-Schlüssel nicht mehr vorhanden oder beeinträchtigt ist, generieren Sie einen neuen Satz von Signierschlüsseln für Ihr Repository.
{:shortdesc}

Die einzige Signierrolle, die Sie turnusmäßig wechseln können, ist `targets`, der Repository-Administrator. Sind andere Rollen betroffen, generieren Sie neue Schlüssel für diese Rollen, entfernen Sie die alten und fügen Sie die neuen als Unterzeichner hinzu.
{:tip}

Bevor Sie anfangen, rufen Sie die Rootschlüssel-Kennphrase ab, die Sie erstellt haben, als Sie erstmalig [ein signiertes Image mit Push-Operation übertragen](registry_trusted_content.html#trustedcontent_push) haben.

1.  Installieren Sie die Befehlszeilenschnittstellenversion von [Notary Project ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli).

2.  [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](registry_trusted_content.html#trustedcontent_setup).

3.  Vermerken Sie die URL aus dem Exportbefehl im vorherigen Schritt. Beispiel: `https://registry.ng.bluemix.net:4443`.

4.  Generieren Sie ein Registry-Token.

    ```
    ibmcloud cr token-add --readwrite
    ```
    {: pre}

5.	Rotieren Sie Ihre Schlüssel, sodass Inhalte, die mit diesen Schlüsseln signiert wurden, nicht länger vertrauenswürdig sind. Ersetzen Sie die _&lt;URL&gt;_ durch die URL des Exportbefehls, die Sie in Schritt 2 vermerkt haben, und _&lt;image&gt;_ durch das Image, dessen Repository-Schlüssel beeinträchtigt ist.

    ```
    notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	In der Eingabeaufforderung geben Sie die Kennphrase des Rootschlüssels ein. Anschließend geben Sie in die Eingabeaufforderung eine neue Rootschlüssel-Kennphrase für das neue Repository ein.

7.	[Übertragen Sie mit Push-Operation ein signiertes Image](registry_trusted_content.html#trustedcontent_push), das die neuen Signierschlüssel verwendet.


### Rootschlüssel
{: #trustedcontent_lostrootkey}

Wenn Ihr Rootschlüssel verloren gegangen oder beeinträchtigt ist, können Sie Repositorys mit vertrauenswürdigen Inhalten, die diesen Rootschlüssel verwendet haben, nicht aktualisieren.
{:shortdesc}

Sie können [Namensbereiche löschen](registry_setup_cli_namespace.html#registry_remove), deren Repositorys den betroffenen Rootschlüssel verwenden, womit Ihre Images und Trust-Daten gelöscht werden.

Enthält der Namensbereich Repositorys mit nicht betroffenen Rootschlüsseln, z. B. ein Namensbereich für Produktions-Images, kann es sinnvoll sein, nur diejenigen Trust-Daten zu löschen, die dem betroffenen Rootschlüssel zugehörig sind. Öffnen Sie ein Support-Ticket.

1.  [Wenden Sie sich an den {{site.data.keyword.Bluemix_notm}} Support](/docs/get-support/howtogetsupport.html#getting-customer-support). Schließen Sie eine Kurzbeschreibung Ihres Problems, die Konto-ID und eine Liste der Namensbereiche ein, die die Image-Repositorys mit den betroffenen Rootschlüsseln enthalten.

2.  Nachdem sich {{site.data.keyword.Bluemix_notm}} mit dem Problem befasst hat, löschen Sie das Docker Content Trust-Repository auf Ihrem lokalen Computer.

    * Linux- oder Mac-Verzeichnis: `~/.docker/trust/private` und `~/.docker/trust/tuf`

    * Windows-Verzeichnis: `%HOMEPATH%\.docker\trust\private` und `%HOMEPATH%\.docker\trust\tuf`

    Da der Rootschlüssel betroffen ist, werden mit diesem Schritt alle Signierschlüssel, auch die für andere Trust-Server, gelöscht.
    {:tip}

3.  Wenn Sie [{{site.data.keyword.Bluemix_notm}} Image Enforcement](registry_security_enforce.html) in Ihrem {{site.data.keyword.containershort_notm}}-Cluster verwenden, starten Sie jeden Image Enforcement-Pod neu. Um Kubernetes zu veranlassen, automatisch einen sequenziellen Neustart der Pods durchzuführen, können Sie einige Metadaten am Pod ändern. Zum Beispiel [wählen Sie Ihre Kubernetes-CLI als Ziel für Ihren Cluster](/docs/containers/cs_cli_install.html#cs_cli_configure) aus und modifizieren Sie die Implementierung.

    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  Generieren Sie Repositorys mit vertrauenswürdigen Inhalten.

    *  Wenn Sie neue vertrauenswürdige Inhalte erstellen möchten, [übertragen Sie die neuen signierten Images mit Push-Operation](registry_trusted_content.html#trustedcontent_push).

    *  Wenn Sie die vorherigen vertrauenswürdigen Inhalte nicht ändern möchten, fügen Sie den neuesten Images in der Registry eine Signatur hinzu.

       ```
       docker trust sign <image>:<tag>
       ```
       {: pre}
       

## Die Installation von Container Image Security Enforcement schlägt mit `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists` fehl.
{: #ts_install_cise_fail}

{: tsSymptoms}
Ihre Installation von Container Image Security Enforcement ist fehlgeschlagen und Sie haben die folgende Nachricht erhalten:

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
Die vorherige Installation ist fehlgeschlagen und die nachfolgende Deinstallation hat nicht alle Kubenetes-Jobs entfernt, die der Installation zugehörig waren.

{: tsResolve}
Entfernen Sie die verbleibenden Kubenetes-Jobs mit dem folgenden Befehl:

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}


## Pods können nicht erneut gestartet werden, nachdem alle Worker inaktiv waren
{: #ts_pods}


{: tsSymptoms}
Pods können nicht erneut gestartet werden, nachdem alle Cluster-Worker inaktiv waren. Container Image Security Enforcement ist bereitgestellt. Der Status der Cluster-Worker wird als einwandfrei angezeigt, es findet jedoch keine Planung statt.

{: tsCauses}
Standardmäßig fügt Container Image Security Enforcement einen Zugangswebhook 'fail closed' hinzu. Wenn alle Container Image Security Enforcement-Pods inaktiv sind, stehen die Pods nicht für die Bestätigung der eigenen Wiederherstellung zur Verfügung.

{: tsResolve}
Damit der Cluster wiederhergestellt werden kann, wenn er sich in diesem Status befindet, müssen Sie die Webhookkonfiguration von 'fail closed' in 'fail open' ändern. 

Sie benötigen ausreichende RBAC-Berechtigungen (RBAC = Role-Based Access Control, rollenbasierte Zugriffssteuerung) für die Verwendung der folgenden Verben:
*  `GET`
*  `PATCH`

Für die folgenden Ressourcen:
*  `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
*  `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration` 

Weitere Informationen zu RBAC finden Sie in [Benutzern Berechtigungen mithilfe angepasster Kubernetes-RBAC-Rollen zuweisen](/docs/containers/cs_users.html#rbac) und [Kubernetes: RBAC-Berechtigung verwenden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

Führen Sie die folgenden Schritte aus, um die Webhookkonfiguration von 'fail closed' in 'fail open' zu ändern und sie dann, wenn mindestens ein Container Image Security Enforcement-Pod aktiv ist, wieder auf 'fail closed' zurückzusetzen:

1.  Aktualisieren Sie `MutatingWebhookConfiguration`, indem Sie den folgenden Befehl ausführen:

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Ändern Sie `failurePolicy` in `Ignore`, speichern Sie die Einstellung und schließen Sie sie.

2.  Aktualisieren Sie `ValidatingWebhookConfiguration`, indem Sie den folgenden Befehl ausführen:

    ``>
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Ändern Sie `failurePolicy` in `Ignore`, speichern Sie die Einstellung und schließen Sie sie.

3.  Warten Sie, bis einige Container Image Security Enforcement-Pods gestartet werden. Sie können überprüfen, ob die Pods gestartet wurden, indem Sie den folgenden Befehl ausführen, bis in der Spalte **Status** für mindestens einen Pod `Running` angezeigt wird:

    ```
    kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
    ```
    {: pre}

4.  Wenn mindestens ein Container Image Security Enforcement-Pod aktiv ist, aktualisieren Sie `MutatingWebhookConfiguration`, indem Sie den folgenden Befehl ausführen:

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Ändern Sie `failurePolicy` in `Fail`, speichern Sie die Einstellung und schließen Sie sie.

5.  Aktualisieren Sie `ValidatingWebhookConfiguration`, indem Sie den folgenden Befehl ausführen:

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Ändern Sie `failurePolicy` in `Fail`, speichern Sie die Einstellung und schließen Sie sie.
