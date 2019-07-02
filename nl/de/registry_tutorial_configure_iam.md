---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-19"

keywords: IBM Cloud Container Registry, user access, tutorial, access control, 

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

# Lernprogramm: Zugriff auf {{site.data.keyword.registrylong_notm}}-Ressourcen erteilen
{: #iam_access}

Verwenden Sie dieses Lernprogramm, um zu erfahren, wie Sie Zugriff auf Ihre Ressourcen erteilen, indem Sie {{site.data.keyword.iamlong}} (IAM) for {{site.data.keyword.registrylong_notm}} konfigurieren.
{:shortdesc}

Dieses Lernprogramm dauert ca. Minuten.

**Vorbereitung**

- Führen Sie die Anweisungen im Abschnitt [Erste Schritte mit {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started) aus.

- Stellen Sie sicher, dass Sie über die neueste Version des `container-registry`-CLI-Plug-ins für die {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle verfügen. Weitere Informationen finden Sie in [`container-registry`-CLI-Plug-in aktualisieren](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).

- Sie müssen über Zugriff auf zwei [{{site.data.keyword.cloud_notm}}-Konten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/login) verfügen, die Sie für dieses Lernprogramm verwenden können, eines für Benutzer A und eines für Benutzer B. Diese müssen jeweils eine eindeutige E-Mail-Adresse verwenden. Sie arbeiten in Ihrem eigenen Konto, als Benutzer A, und laden einen anderen Benutzer, Benutzer B, ein, Ihr Konto zu verwenden. Sie können entweder ein zweites {{site.data.keyword.cloud_notm}}-Konto erstellen oder mit einem Kollegen arbeiten, der bereits ein {{site.data.keyword.cloud_notm}}-Konto besitzt.

- Wenn Sie mit der Verwendung von {{site.data.keyword.registrylong_notm}} in Ihrem Konto vor dem 4. Oktober 2018 begonnen haben, müssen Sie die IAM-Richtliniendurchsetzung aktivieren, indem Sie den Befehl `ibmcloud cr iam-policies-enable` ausführen. Wenn Sie andere Benutzer, die Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche verwenden, in Ihr IBM Cloud-Konto eingeladen haben, verwenden Sie ein anderes Konto als Benutzer A, um deren Zugriff nicht zu unterbrechen.

## Schritt 1: Benutzer berechtigen, die Registry zu konfigurieren
{: #configure_registry}

In diesem Abschnitt fügen Sie einen zweiten Benutzer zu Ihrem Konto hinzu und geben ihm die Möglichkeit, {{site.data.keyword.registrylong_notm}} zu konfigurieren.
{:shortdesc}

1. Fügen Sie Benutzer B zum Konto von Benutzer A hinzu:

    1. Melden Sie sich beim Konto von Benutzer A an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Laden Sie Benutzer B ein, auf das Konto von Benutzer A zuzugreifen, indem er den folgenden Befehl ausführt, wobei _`<user.b@example.com>`_ die E-Mail-Adresse von Benutzer B ist:

        ```
        ibmcloud account user-invite <benutzer.b@beispiel.com>
        ```
        {: pre}

    3. Rufen Sie die Konto-ID von Benutzer A ab, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud target
        ```
        {: pre}

        Notieren Sie sich die Konto-ID in den runden Klammern () in der Zeile 'Konto'.

2. Überprüfen Sie, dass Benutzer B das Konto von Benutzer A erreichen kann, aber noch nichts weiter mit {{site.data.keyword.registrylong_notm}} tun kann:

    1. Melden Sie sich als Benutzer B an und führen Sie den folgenden Befehl aus, um das Konto von Benutzer A zu erreichen, wobei _`<YourAccountID>`_ die Konto-ID von Benutzer A ist:

        ```
        ibmcloud login -c <ihre_konto-id>
        ```
        {: pre}

    2. Versuchen Sie, Ihr Registry-Kontingent auf 4 GB des Datenverkehrs zu ändern, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        Der Befehl schlägt fehl, da Benutzer B nicht die erforderlichen Zugriffsrechte hat.

3. Ordnen Sie Benutzer B die Rolle 'Manager' zu, sodass er {{site.data.keyword.registrylong_notm}} konfigurieren kann:

    1. Melden Sie sich als Benutzer A mit dem folgenden Befehl wieder bei Ihrem Konto an:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Erstellen Sie eine Richtlinie, die Benutzer B die Rolle 'Manager' zuordnet, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam user-policy-create <benutzer.b@beispiel.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. Überprüfen Sie, dass Benutzer B jetzt Kontingente im Konto von Benutzer A ändern kann:

    1. Melden Sie sich als Benutzer B an und erreichen Sie das Konto von Benutzer A, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login -c <ihre_konto-id>
        ```
        {: pre}

    2. Versuchen Sie, Ihr Registry-Kontingent auf 4 GB des Datenverkehrs zu ändern, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        Das funktioniert, weil Benutzer B über den richtigen Typ von Zugriff verfügt.

    3. Ändern Sie jetzt das Kontingent zurück, indem Sie den folgenden Befehl ausführen:
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. Räumen Sie auf:

    1. Melden Sie sich als Benutzer A mit dem folgenden Befehl wieder bei Ihrem Konto an:
  
        ```
        ibmcloud login
        ```
        {: pre}
  
    2. Listen Sie die Richtlinien für Benutzer B auf, suchen Sie nach der Richtlinie, die Sie gerade erstellt haben, indem Sie den folgenden Befehl ausführen, und notieren Sie sich die ID:
  
        ```
        ibmcloud iam user-policies <benutzer.b@beispiel.com>
        ```
        {: pre}
  
    3. Löschen Sie die Richtlinie, indem Sie den folgenden Befehl ausführen, wobei _`<Policy_ID>`_ Ihre Richtlinien-ID ist:
  
        ```
        ibmcloud iam user-policy-delete <benutzer.b@beispiel.com> <richtlinien-id>
        ```
        {: pre}

## Schritt 2: Benutzer berechtigen, auf bestimmte Namensbereiche zuzugreifen
{: #access_resources}

In diesem Abschnitt erstellen Sie einige Namensbereiche mit Beispiel-Images und gewähren Zugriff darauf. Sie erstellen Richtlinien, um den einzelnen Namensbereichen unterschiedliche Rollen zuzuordnen und zu sehen, welche Auswirkungen das hat.
{:shortdesc}

1. Erstellen Sie drei neue Namensbereiche im Konto von Benutzer A. Diese Namensbereiche müssen in der gesamten Region eindeutig sein. Wählen Sie daher Ihre eigenen Namen für die Namensbereiche aus. In diesem Lernprogramm werden jedoch `namensbereich_a`, `namensbereich_b` und `namensbereich_c` beispielhaft verwendet:

    1. Melden Sie sich als Benutzer A an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Erstellen Sie `namespace_a`, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr namespace-add namespace_a
        ```
        {: pre}

        Der Namensbereich muss in allen {{site.data.keyword.cloud_notm}}-Konten derselben Region eindeutig sein. Namensbereiche müssen 4 bis 30 Zeichen lang sein und dürfen nur Kleinbuchstaben, Zahlen, Bindestriche (-) und Unterstreichungszeichen (_) enthalten. Namensbereiche müssen mit einem Buchstaben oder einer Zahl beginnen und enden.
        {: tip}

    3. Erstellen Sie `namespace_b`, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr namespace-add namensbereich_b
        ```
        {: pre}
            
    4. Erstellen Sie `namespace_c`, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr namespace-add namensbereich_c
        ```
        {: pre}

2. Überprüfen Sie, dass Benutzer B nichts sehen kann:

    1. Melden Sie sich als Benutzer B an und erreichen Sie das Konto von Benutzer A, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login -c <ihre_konto-id>
        ```
        {: pre}

    2. Versuchen Sie als Benutzer B, Images aufzulisten, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr images
        ```
        {: pre}

        Es wird eine leere Liste zurückgegeben, da Benutzer B keinen Zugriff auf Namensbereiche hat.

3. Erstellen Sie Richtlinien, um Benutzer B die Möglichkeit zu geben, mit den Namensbereichen zu interagieren, indem Sie den folgenden Befehl ausführen:

    1. Melden Sie sich als Benutzer A an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Überprüfen Sie, dass mindestens drei Namensbereiche aufgelistet sind, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        Die drei Namensbereiche, die Sie in diesem Lernprogramm erstellt haben (`namensbereich_a`, `namensbereich_b` und `namensbereich_c`), werden angezeigt. Wenn diese Namensbereiche nicht angezeigt werden, gehen Sie zurück und führen Sie erneut die Anweisungen zu ihrer Erstellung aus.

    3. Erstellen Sie eine Richtlinie, die Benutzer B die Rolle 'Leseberechtigter' für `namensbereich_b` zuordnet, indem Sie den folgenden Befehl ausführen, wobei _`<Region>`_ der Name Ihrer [Region](/docs/services/Registry?topic=registry-registry_overview#registry_regions) ist, z. B. `us-south`:

        ```
        ibmcloud iam user-policy-create <benutzer.b@beispiel.com> --service-name container-registry --region <region> --resource-type namensbereich --resource namensbereich_b --roles Leseberechtigter
        ```
        {: pre}

    4. Erstellen Sie eine zweite Richtlinie, die Benutzer B die Rollen 'Leseberechtigter' und 'Schreibberechtigter' für `namensbereich_c` zuordnet, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam user-policy-create <benutzer.b@beispiel.com> --service-name container-registry --region <region> --resource-type namensbereich --resource namensbereich_c --roles Leseberechtigter,Schreibberechtigter
        ```
        {: pre}

        Mit diesem Befehl werden zwei Rollen zu derselben Ressource in derselben Richtlinie hinzugefügt.
        {: tip}

4. Übertragen Sie die Images per Push-Operation in `namensbereich_a` und `namensbereich_b`:

    1. Extrahieren Sie das Image `hello-world`, indem Sie den folgenden Befehl ausführen:

        ```
        docker pull hello-world
        ```
        {: pre}

    2. Kennzeichnen Sie das Image für `namensbereich_a`, indem Sie den folgenden Befehl ausführen:

        ```
        docker tag hello-world <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Kennzeichnen Sie das Image für `namensbereich_b`, indem Sie den folgenden Befehl ausführen:

        ```
        docker tag hello-world <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. Melden Sie sich bei {{site.data.keyword.registrylong_notm}} an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Übertragen Sie das Image per Push-Operation an `namensbereich_a`, indem Sie den folgenden Befehl ausführen:

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. Übertragen Sie das Image per Push-Operation an `namensbereich_b`, indem Sie den folgenden Befehl ausführen:

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

5. Überprüfen Sie, dass Benutzer B mit `namensbereich_b` und `namensbereich_c`, aber nicht mit `namensbereich_a` interagieren kann:

    1. Melden Sie sich als Benutzer B an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login -c <ihre_konto-id>
        ```
        {: pre}

    2. Zeigen Sie, dass Benutzer B `namensbereich_b` und `namensbereich_c` anzeigen kann, aber nicht `namensbereich_a`, weil Benutzer B keinen Zugriff auf `namensbereich_a` hat, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. Listen Sie Ihre Images auf, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr images
        ```
        {: pre}

        Das Image in `namensbereich_b` wird in der Liste angezeigt, das Image in `namensbereich_a` jedoch nicht, da Benutzer B keinen Zugriff auf `namensbereich_a` hat.

    4. Melden Sie sich bei {{site.data.keyword.registrylong_notm}} an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Extrahieren Sie das Image, indem Sie den folgenden Befehl ausführen:

        ```
        docker pull <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. Übertragen Sie das Image per Push-Operation an `namensbereich_b`, indem Sie den folgenden Befehl ausführen:

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        Dieser Befehl schlägt fehl, da Benutzer B in `namensbereich_b` nicht über die Rolle 'Schreibberechtigter' verfügt.

    7. Kennzeichnen Sie das Image mit `namensbereich_c`, indem Sie den folgenden Befehl ausführen:

        ```
        docker tag hello-world <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. Übertragen Sie das Image per Push-Operation an `namensbereich_c`, indem Sie den folgenden Befehl ausführen:

        ```
        docker push <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        Der Befehl funktioniert, weil Benutzer B in `namensbereich_c` über die Rolle 'Schreibberechtigter' verfügt.

    9. Führen Sie eine Pull-Operation aus `namensbereich_c` durch, indem Sie den folgenden Befehl ausführen:

        ```
        docker pull <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        Der Befehl funktioniert, weil Benutzer B in `namensbereich_c` über die Rolle 'Leseberechtigter' verfügt.

6. Räumen Sie auf:

    1. Melden Sie sich wieder beim Konto von Benutzer A an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Listen Sie die Richtlinien für Benutzer B auf, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam user-policies <benutzer.b@beispiel.com>
        ```
        {: pre}

        Suchen Sie nach den Richtlinien, die Sie gerade erstellt haben, und notieren Sie die Richtlinien-IDs.

    3. Löschen Sie die Richtlinien, die Sie gerade erstellt haben, indem Sie den folgenden Befehl eingeben, wobei _`<Policy_ID>`_ die Richtlinien-ID ist:

        ```
        ibmcloud iam user-policy-delete <benutzer.b@beispiel.com> <richtlinien-id>
        ```
        {: pre}

## Schritt 3: Service-ID erstellen und Zugriff auf eine Ressource erteilen
{: #service_id}

In diesem Abschnitt konfigurieren Sie eine Service-ID und erteilen ihr Zugriff auf Ihren {{site.data.keyword.registrylong_notm}}-Namensbereich.
{:shortdesc}

1. Richten Sie eine Service-ID mit Zugriff auf {{site.data.keyword.registrylong_notm}} ein und erstellen Sie einen API-Schlüssel dafür:

    1. Melden Sie sich beim Konto von Benutzer A an, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Erstellen Sie eine Service-ID namens `cr-roles-tutorial` mit der Beschreibung `"Während des Zugriffssteuerungs-Lernprogramms für Container-Registry erstellt"`, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Während des Zugriffssteuerungs-Lernprogramms für Container-Registry erstellt"
        ```
        {: pre}

    3. Erstellen Sie eine Servicerichtlinie für die Service-ID, die die Rolle 'Leseberechtigter' für `namensbereich_a` zuordnet, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <region> --resource-type namensbereich --resource namensbereich_a --roles Leseberechtigter
        ```
        {: pre}

    4. Erstellen Sie eine zweite Servicerichtlinie, die die Rolle 'Schreibberechtigter' für `namensbereich_b` zuordnet, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <region> --resource-type namensbereich --resource namensbereich_b --roles Schreibberechtigter
        ```
        {: pre}

    5. Erstellen Sie einen API-Schlüssel für die Service-ID, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Verwenden Sie Docker, um sich mit dem API-Schlüssel der Service-ID anzumelden, wobei _`<API_Key>`_ Ihr API-Schlüssel ist, und um mit der Registry zu interagieren:

    1. Melden Sie sich bei {{site.data.keyword.registrylong_notm}} an, indem Sie den folgenden Befehl ausführen:

        ```
        docker login -u iamapikey -p <API_Key> <Region>.icr.io
        ```
        {: pre}

    2. Extrahieren Sie Ihr Image, indem Sie den folgenden Befehl ausführen:

        ```
        docker pull <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Übertragen Sie Ihr Image per Push-Operation an `namensbereich_a`, indem Sie den folgenden Befehl ausführen:

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        Dieser Befehl funktioniert nicht, da der Benutzer in `namensbereich_a` nicht über die Rolle 'Schreibberechtigter' verfügt.

    4. Übertragen Sie Ihr Image per Push-Operation an `namensbereich_b`, indem Sie den folgenden Befehl ausführen:

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        Der Befehl funktioniert, weil der Benutzer in `namensbereich_b` über die Rolle 'Schreibberechtigter' verfügt.

3. Räumen Sie auf:

    1. Listen Sie Ihre Servicerichtlinien auf, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        Notieren Sie Ihre Richtlinien-IDs.

    2. Löschen Sie Ihre Servicerichtlinien, indem Sie den folgenden Befehl für jede Richtlinie ausführen:

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <richtlinien-id>
        ```
        {: pre}

    3. Löschen Sie Ihre Service-ID, indem Sie den folgenden Befehl ausführen:

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. Melden Sie sich bei {{site.data.keyword.registrylong_notm}} wieder als Benutzer A an:

        ```
        ibmcloud cr login
        ```
        {: pre}

## Schritt 4: Aufräumen
{: #clean_up}

In diesem Abschnitt entfernen Sie die Ressourcen, die Sie in den vorherigen Abschnitten erstellt haben, um Ihren Account so zu belassen, wie er zu Beginn dieses Lernprogramms war.
{:shortdesc}

1. Melden Sie sich bei Ihrem Konto an, indem Sie den folgenden Befehl ausführen:

    ```
    ibmcloud login
    ```
    {: pre}

2. Löschen Sie `namensbereich_a`, `namensbereich_b` und `namensbereich_c`, indem Sie die folgenden Befehle ausführen:

    ```
    ibmcloud cr namespace-rm namensbereich_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namensbereich_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namensbereich_c
    ```
    {: pre}

3. Entfernen Sie Benutzer B aus Ihrem Konto, indem Sie den folgenden Befehl ausführen:

   ```
   ibmcloud account user-remove <benutzer.b@beispiel.com>
   ```
   {: pre}

Gut gemacht! Sie haben dieses Lernprogramm erfolgreich abgeschlossen.
