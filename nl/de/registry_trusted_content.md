---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, Docker Content Trust, keys, trusted content, signing, signing images, repository keys, 

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

# Images für vertrauenswürdige Inhalte signieren
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} bietet eine Technologie für vertrauenswürdige Inhalte, sodass Sie Images signieren können, um die Integrität von Images in Ihrem Registry-Namensbereich sicherzustellen. Durch Extrahieren von signierten Images mit Pull-Operation und ihre Übertragung mit Push-Operation können Sie sicherstellen, dass Ihre Images vom richtigen Teilnehmer, z. B. Ihren Tools für kontinuierliche Integration (Continuous Integration, CI), mit Push-Operation übertragen wurden. Um diese Funktion verwenden zu können, müssen Sie über Docker Version 18.03 oder höher verfügen. Weitere Informationen finden Sie in der Dokumentation zu [Docker Content Trust ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.docker.com/engine/security/trust/content_trust/) und zum [Notary-Projekt ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/theupdateframework/notary).
{:shortdesc}

Wenn Sie Ihr Image mit Push-Operation und mit aktiviertem Content Trust übertragen, überträgt Ihr Docker-Client ebenfalls ein signiertes Metadatenobjekt mit Push-Operation an den {{site.data.keyword.Bluemix_notm}}-Trust-Server. Wird ein mit Tags versehenes Image bei aktiviertem Docker Content Trust mit Pull-Operation extrahiert, kontaktiert Ihr Docker-Client den Trust-Server, um die zuletzt signierte Version des von Ihnen angeforderten Tags festzustellen, überprüft die Inhaltssignatur und lädt das signierte Image herunter.

Ein Imagename setzt sich aus einem Repository und einem Tag zusammen. Bei Verwendung von vertrauenswürdigen Inhalten verwendet jedes Repository einen eindeutigen Signierschlüssel. Jeder Tag innerhalb eines Repositorys verwendet den Schlüssel, der dem Repository angehört. Wenn mehrere Ihrer Teams Inhalte veröffentlichen, jedes in das eigene Repository innerhalb Ihrer {{site.data.keyword.registrylong_notm}}-Namensbereiche, kann jedes Team seinen eigenen Schlüssel zum Signieren des eigenen Inhalts verwenden, sodass Sie überprüfen können, ob jedes Images vom richtigen Team erzeugt wurde.

Ein Repository kann sowohl signierten als auch nicht signierten Inhalt enthalten. Wenn Docker Content Trust aktiviert ist, können Sie auch dann auf den signierten Inhalt eines Repositorys zugreifen, wenn auch anderer nicht signierter Inhalt darin vorhanden ist.

Images weisen separate Signaturen für alte (`registry.bluemix.net`) und für neue (`icr.io`) Domänennamen auf. Bereits vorhandene Signaturen funktionieren, wenn das Image aus dem alten Domänennamen extrahiert wird. Wenn Sie signierten Inhalt per Pull-Operation aus dem neuen Domänennamen extrahieren möchten, müssen Sie das Image beim neuen Domänennamen `icr.io` erneut signieren; Informationen hierzu finden Sie im Abschnitt zum [Erneuten Signieren eines Image für den neuen Domänennamen](#trustedcontent_resign).
{: note}

Docker Content Trust verwendet ein "trust on first use"-Sicherheitsmodell ("Vertrauen bei erster Verwendung"). Der Repository-Schlüssel wird aus dem Trust-Server mit Pull-Operation extrahiert, wenn Sie erstmalig ein signiertes Image mit Pull-Operation aus einem Repository extrahieren, und dieser Schlüssel wird künftig verwendet, um Images aus diesem Repository zu überprüfen. Sie müssen darauf achten, entweder dem Trust-Server oder dem Image und seinem Veröffentlicher zu vertrauen, bevor Sie das Repository zum ersten Mal mit Pull-Operation extrahieren. Wenn die vertrauenswürdigen Informationen im Server beeinträchtigt sind und Sie vorher noch kein Image aus dem Repository mit Pull-Operation extrahiert haben, kann es sein, dass Ihr Docker-Client die beeinträchtigten Daten vom Trust-Server mit Pull-Operation extrahiert. Werden die Trust-Daten beschädigt, nachdem Sie das Image zum ersten Mal mit Pull-Operation extrahiert haben, kann Ihr Docker-Client bei späteren Extraktionen die beschädigten Daten nicht prüfen und extrahiert das Image nicht. Weitere Informationen dazu, wie Trust-Daten für ein Image untersucht werden, finden Sie unter [Signierte Images anzeigen](#trustedcontent_viewsigned).

Weitere Informationen zum Sicherheitsmodell "trust on first use" finden Sie in [The Update Framework (TUF) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://theupdateframework.github.io/).

## Umgebung mit vertrauenswürdigen Inhalten einrichten
{: #trustedcontent_setup}

Standardmäßig ist Docker Content Trust inaktiviert. Aktivieren Sie die Content Trust-Umgebung, bevor Sie sich bei {{site.data.keyword.registrylong_notm}} anmelden und mit signierten Images arbeiten.
{:shortdesc}

1. Aktivieren Sie die Umgebungsvariable Docker Content Trust in Ihrem Terminal.

   Für Linux oder Mac:

   ```
   export DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

   Für Windows:

   ```
   set DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

2. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-CLI an.

   ```
   ibmcloud login [--sso]
   ```
   {: pre}

   Wenn Sie über eine eingebundene ID verfügen, verwenden Sie `ibmcloud login --sso`, um sich anzumelden. Geben Sie Ihren Benutzernamen ein und verwenden Sie die bereitgestellte URL in der CLI-Ausgabe zum Abrufen Ihres einmaligen Kenncodes. Sie erkennen, ob Sie über eine eingebundene ID verfügen, wenn die Anmeldung ohne die Option `--sso` fehlschlägt und mit der Option `--sso` erfolgreich ist.
   {: tip}

3. Wählen Sie die Region aus, die Sie als Ziel verwenden möchten. Wenn Sie den Regionsnamen nicht kennen, führen Sie den Befehl ohne die Region aus und wählen Sie danach eine Region.

   ```
   ibmcloud cr region-set <Region>
   ```
   {: pre}

4. Melden Sie sich bei {{site.data.keyword.registrylong_notm}} an.

   ```
   ibmcloud cr login
   ```
   {: pre}

   Die Ausgabe weist Sie an, die Umgebungsvariable Docker Content Trust zu exportieren.

   **Beispiel**

   ```
   user:~ user$ ibmcloud cr login
   Logging in to 'us.icr.io'...
   Logged in to 'us.icr.io'.

   Um Ihren Docker-Client mit Content Trust einzurichten, exportieren Sie die folgende Umgebungsvariable:
    export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: screen}

5. Kopieren Sie den Befehl für die Umgebungsvariable und fügen Sie ihn in Ihr Terminal ein. Beispiel:

   ```
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: pre}

Jetzt können Sie vertrauenswürdige signierte Images mit Push-Operation übertragen, mit Pull-Operation extrahieren und verwalten.

Wenn Sie während Ihrer Sitzung mit aktiviertem Docker Content Trust eine Operation mit inaktivierten vertrauenswürdigen Inhalten (z. B. eine Pull-Operation für ein nicht signiertes Image) durchführen möchten, verwenden Sie das Flag `--disable-content-trust` mit dem Befehl.
{: tip}

## Signiertes Image mit Push-Operation übertragen
{: #trustedcontent_push}

Wenn Sie ein signiertes Image erstmalig mit Push-Operation übertragen, erstellt Docker automatisch ein Paar von Signierschlüsseln, den Root- und den Repository-Schlüssel. Um ein Image in einem Repository zu signieren, in das bereits zuvor signierte Images mit Push-Operation übertragen wurden, muss der richtige Repository-Signierschlüssel in dem System geladen sein, das das Image mit Push-Operation überträgt.
{:shortdesc}

Bevor Sie anfangen, [richten Sie Ihren Registry-Namensbereich ein](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add).

1. [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](#trustedcontent_setup).

2. [Übertragen Sie Ihr Image mit Push-Operation](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing). Der Tag ist für vertrauenswürdige Inhalte obligatorisch. Die Befehlsausgabe gibt Folgendes an:

   ```
   Image-Metadaten werden signiert und mit Push-Operation übertragen.
   ```
   {: screen}

3. **Erstmalige Übertragung eines signierten Repositorys mit Push-Operation.** Wenn Sie ein signiertes Image mit Push-Operation an ein neues Repository übertragen, erstellt der Befehl zwei Signierschlüssel, den Rootschlüssel und den Repository-Schlüssel, und speichert diese in Ihrem lokalen System. Geben Sie für jeden Schlüssel eine sichere Kennphrase ein und speichern Sie sie. Anschließend [erstellen Sie eine Sicherungskopie für Ihre Schlüssel](#trustedcontent_backupkeys). Das Erstellen einer Sicherungskopie Ihrer Schlüssel ist kritisch, da Ihre [Wiederherstellungsoptionen](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent) begrenzt sind.

## Signiertes Image mit Pull-Operation extrahieren
{: #trustedcontent_pull}

Beim erstmaligen Extrahieren eines signierten Image mit Pull-Operation bei aktiviertem Docker Content Trust erkennt Ihr Docker-Client die Signatur als vertrauenswürdig. Der Docker-Client extrahiert die zuletzt signierte Version des von Ihnen angegebenen Image mit Pull-Operation. Nicht signierte Images oder nicht vertrauenswürdige Inhalte werden nicht mit Pull-Operation extrahiert.
{:shortdesc}

1. [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](#trustedcontent_setup).

2. Extrahieren Sie Ihr Image mit Pull-Operation. Ersetzen Sie `<source_image>` durch das Repository des Images und `<tag>` durch den Tag des Images, das verwendet werden soll, z. B. _latest_. Zum Auflisten der für Pull-Operationen verfügbaren Images führen Sie den Befehl `ibmcloud cr image-list` aus.

   ```
   docker pull <quellenimage>:<tag>
   ```
   {: pre}

    Geben Sie den Tag an, wenn Sie an einem signierten Image Push- oder Pull-Operation durchführen. Der Tag ` latest` hat nur dann den Standardwert, wenn Content Trust inaktiviert ist.
    {: tip}

## Image für den neuen Domänennamen erneut signieren
{: #trustedcontent_resign}

Um das Image für den neuen Domänennamen `icr.io` erneut zu signieren, müssen Sie für das Image eine Pull-, Tag- und Push-Operation durchführen.
{:shortdesc}

1. Extrahieren Sie Ihr signiertes Image mit der Pull-Operation aus dem alten Domänennamen. Ersetzen Sie `<source_image>` durch das Repository des Images und `<tag>` durch den Tag des Images, das verwendet werden soll, z. B. _latest_. Zum Auflisten der für Pull-Operationen verfügbaren Images führen Sie den Befehl `ibmcloud cr image-list` aus.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    Geben Sie den Tag an, wenn Sie an einem signierten Image Push- oder Pull-Operation durchführen. Der Tag ` latest` hat nur dann den Standardwert, wenn Content Trust inaktiviert ist.
    {: tip}

2. Führen Sie den Befehl `docker tag` für den neuen Domänennamen aus. Ersetzen Sie `<old_domain_name>` durch den alten Domänennamen, `<new_domain_name>` durch den neuen Domänennamen, `<repository>` durch den Namen des Repositorys und `<tag>` durch den Namen des Tags. 

   ```
   docker tag <old_domain_name>/<repository>:<tag> <new_domain_name>/<repository>:t<tag>
   ```
   {: pre}

3. Führen Sie für Ihr Image eine Push-Operation durch, indem Sie den neuen Domänennamen verwenden; Informationen hierzu finden Sie im Abschnitt zum [Durchführen einer Push-Operation für Docker-Images in den eigenen Namensbereich](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing). Der Tag ist für vertrauenswürdige Inhalte obligatorisch. Die Befehlsausgabe gibt Folgendes an:

   ```
   Image-Metadaten werden signiert und mit Push-Operation übertragen.
   ```
   {: screen}

## Vertrauenswürdige Inhalte verwalten
{: #trustedcontent_managetrust}

Durch Verwendung von `docker trust`-Befehlen können Sie anzeigen, wer die Images signiert hat, und auch den Status für vertrauenswürdige Inhalte widerrufen. Um `docker trust`-Befehle ausführen zu können, benötigen Sie Docker 18.03 oder höher.
{:shortdesc}

### Signierte Images anzeigen
{: #trustedcontent_viewsigned}

Sie können signierte Versionen eines Image oder Tags und auch die Informationen zur Schlüssel-ID und zum Unterzeichner prüfen.
{:shortdesc}

1. [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](#trustedcontent_setup).

2. Prüfen Sie den Tag, den Auszug und die Unterzeichnerinformationen für jedes Image.

   (Optional) Den Tag, `<tag>`, angeben, um Informationen zu dieser Version des Images anzuzeigen.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### Vertrauensbeziehung widerrufen
{: #trustedcontent_revoketrust}

Sie können den Status des vertrauenswürdigen Inhalts eines Image widerrufen.
{:shortdesc}

Bevor Sie anfangen, rufen Sie die Kennphrase des Repository-Schlüssels ab, die Sie gespeichert haben, als Sie [erstmalig das vertrauenswürdige Repository mit Push-Operation übertragen](#trustedcontent_push) haben. Um zu ermitteln, welcher Schlüssel für das vertrauenswürdige Image verwendet wird, verwenden Sie den [Befehl](#trustedcontent_viewsigned) `docker view`.

1. [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](#trustedcontent_setup).

2. Entfernen Sie alle vertrauenswürdigen Metadaten für das Image-Repository. Geben Sie in die Eingabeaufforderung die Kennphrase Ihres Repository-Schlüssels ein.

   (Optional) Geben Sie einen Tag an, um vertrauenswürdige Metadaten nur für diese Version des Image zu widerrufen.

   ```
   docker trust revoke <image>:<tag>
   ```
   {: pre}

3. Überprüfen Sie, ob die Vertrauensbeziehung in der Liste der vertrauenswürdigen Inhalte widerrufen wurde.

   (Optional): Schließen Sie den Tag ein, wenn widerrufener Inhalt für ein getaggtes Image überprüft werden soll.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   Ausgabe des vorherigen Befehls:

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## Signierschlüssel sichern
{: #trustedcontent_backupkeys}

Wenn Sie ein signiertes Image erstmalig mit Push-Operation an ein neues Repository übertragen, erstellt Docker Content Trust zwei Signierschlüssel, den Rootschlüssel und den Repository-Schlüssel, und speichert diese in Ihrem lokalen System:

- Linux- oder Mac-Verzeichnis: `~/.docker/trust/private`

- Windows-Verzeichnis: `%HOMEPATH%\.docker\trust\private`

   Wenn Sie Ihr Docker-Konfigurationsverzeichnis geändert haben, suchen Sie dort nach dem `trust`-Unterverzeichnis.
   {: tip}

Sie müssen alle Ihre Schlüssel sichern, besonders den Rootschlüssel. Wenn ein Schlüssel verloren geht oder beeinträchtigt wird, sind Ihre [Wiederherstellungsoptionen](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent) begrenzt.

Hinweise zum Sichern Ihrer Schlüssel finden Sie in der Dokumentation zu [Docker Content Trust ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys).

## Vertrauenswürdige Unterzeichner verwalten
{: #trustedcontent_signers}

Sie können Unterzeichner zum Unterzeichnen von Images in einem Repository hinzufügen oder daraus entfernen.
{:shortdesc}

### Unterzeichner zu einem vertrauenswürdigen Repository hinzufügen
{: #trustedcontent_addsigners}

Damit andere Benutzer Images in einem Repository signieren können, fügen Sie die Signierschlüssel für diese Benutzer zu diesem Repository hinzu.
{:shortdesc}

**Vorbereitung**

- Image-Unterzeichner müssen über die Berechtigung zum Übertragen von Images an den Namensbereich mit Push-Operation verfügen.
- Für Repository-Eigner und zusätzliche Unterzeichner muss Docker 18.03 oder höher installiert sein.
- Erstellen Sie ein Repository für vertrauenswürdige Inhalte, indem Sie ein [signiertes Image mit Push-Operation übertragen](#trustedcontent_push). Repository-Eigner müssen über die Administratorschlüssel für das Repository verfügen, die im Docker-Vertrauensordner in ihrem lokalen System verfügbar sind. Wenn Sie nicht über den Administratorschlüssel für das Repository verfügen, kontaktieren Sie den Eigner, damit er diese Aufgabe für Sie durchführt.

Wenn Sie einen Unterzeichner hinzufügen, können Sie nicht mehr den Administratorschlüssel für das Repository verwenden, um Images in diesem Repository zu signieren. Sie müssen den privaten Schlüssel für einen der genehmigten Unterzeichner zum Signieren besitzen. Um die Fähigkeit zum Signieren von Images nach dem Hinzufügen eines Unterzeichners beizubehalten, folgen Sie diesen Anweisungen nochmals, um eine Unterzeichnerrolle für Sie selbst zu generieren und hinzuzufügen.
{:tip}

Zum Freigeben von Signierschlüsseln gehen Sie folgendermaßen vor:

1. Wenn der neue Unterzeichner noch kein Schlüsselpaar generiert hat, muss ein Schlüsselpaar generiert und geladen werden.
  
    a. Generieren Sie den Schlüssel. Es kann ein beliebiger Name für `<NAME>` eingegeben werden, der ausgewählte Name ist jedoch sichtbar, wenn die Vertrauensbeziehung im Repository überprüft wird. Arbeiten Sie mit dem Repository-Eigner zusammen, um alle Namenskonventionen zu erfüllen, die von der Organisation vielleicht verwendet werden, und um einen Namen auszuwählen, der für diesen Unterzeichner identifizierbar ist.

      ```
      docker trust key generate <NAME>
      ```
      {: pre}
  
    b. Geben Sie eine Kennphrase für den privaten Schlüssel ein. Ein öffentlicher Schlüssel (`.pub`) wird generiert und der entsprechende private Schlüssel wird automatisch in die Docker-Konfiguration für die Vertrauensbeziehung geladen.
  
    c. Der neue Unterzeichner muss dem Repository-Eigner den öffentlichen Schlüssel senden.

2. Der Repository-Eigner muss den Schlüssel des Unterzeichners zum Repository hinzufügen.

    a. [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](#trustedcontent_setup).

    b. Fügen Sie den Schlüssel des Unterzeichners zum Repository hinzu.

      ```
      docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}

3. Der Unterzeichner kann seine Umgebung einrichten und ein Image signieren.

    a. [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](#trustedcontent_setup).

    b. Der Unterzeichner muss ein Image signieren. In der Eingabeaufforderung geben Sie eine Kennphrase für den privaten Schlüssel ein.

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4. Informationen dazu, wie Sie überprüfen, ob der Unterzeichner hinzugefügt wurde, finden Sie unter [Signierte Images anzeigen](#trustedcontent_viewsigned).

### Unterzeichner aus einem Repository entfernen
{: #trustedcontent_removesigner}

Wenn ein Unterzeichner nicht mehr in der Lage sein soll, Images in Ihrem Repository zu signieren, können Sie ihn als Unterzeichner entfernen.
{:shortdesc}

Bevor Sie beginnen, muss für Repository-Eigner und zusätzliche Unterzeichner Docker 18.03 oder höher installiert sein.

Wenn Sie einen Unterzeichner entfernen, vertraut der Trust-Server den signierten Versionen des Images nicht mehr. Um sicherzustellen, dass das Image nach Entfernen des Unterzeichners noch mit Pull-Operation extrahiert werden kann, stellen Sie sicher, dass der Unterzeichner nicht die aktuellste Version des Image signiert hat, bevor Sie fortfahren. Hat der Unterzeichner die aktuellste Version des Image signiert, übertragen Sie eine Aktualisierung mit Push-Operation an das Image und signieren Sie es mit Ihrem Schlüssel, bevor Sie fortfahren.
{:tip}

Zum Entfernen eines Unterzeichners gehen Sie folgendermaßen vor:

1. [Richten Sie die Umgebung für vertrauenswürdige Inhalte ein](#trustedcontent_setup).

2. Entfernen Sie den Unterzeichner.

   ```
   docker trust signer remove <NAME> <repository>
   ```
   {: pre}

3. Um zu überprüfen, ob der Unterzeichner entfernt wurde, zeigen Sie die Trust-Daten für das Image an und stellen Sie sicher, dass der Unterzeichner nicht mehr aufgelistet wird. Weitere Informationen zum Anzeigen von Trust-Daten finden Sie unter [Signierte Images anzeigen](#trustedcontent_viewsigned).
