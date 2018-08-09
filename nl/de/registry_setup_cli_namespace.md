---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.registrylong_notm}}-CLI und eigenen Registry-Namensbereich einrichten
{: #registry_setup_cli_namespace}

Bevor Sie die Docker-Images in {{site.data.keyword.registrylong}} speichern können, müssen Sie die {{site.data.keyword.Bluemix_notm}}-CLI und das Container-Registry-Plug-in installieren und anschließend einen Registry-Namensbereich einrichten, um ein eigenes Image-Repository in {{site.data.keyword.registrylong_notm}} zu erstellen.
{:shortdesc}

Beziehen Sie keine personenbezogenen Daten in Ihre Container-Images, Namensbereichsnamen, Beschreibungsfelder (z. B. in Registry-Tokens) oder in Image-Konfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) ein.
{:tip}

Bevor Sie beginnen, installieren Sie die [{{site.data.keyword.Bluemix_notm}}-CLI ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://clis.ng.bluemix.net/ui/home.html).


## {{site.data.keyword.registrylong_notm}}-CLI installieren (Container-Registry-Plug-in)
{: #registry_cli_install}

Installieren Sie die {{site.data.keyword.registrylong_notm}}-CLI, um Ihre Namensbereiche und Docker-Images in der privaten Registry von {{site.data.keyword.Bluemix_notm}} über die Befehlszeile zu verwalten.
{:shortdesc}

1.  [Installieren Sie das Container-Registry-Plug-in.](index.html#registry_cli_install)
2.  Optional: [Konfigurieren Sie den Docker-Client für die Ausführung von Befehlen ohne Rootberechtigungen](https://docs.docker.com/engine/installation/linux/linux-postinstall). Falls Sie diesen Schritt nicht ausführen, müssen Sie die Befehle `ibmcloud login`, `ibmcloud cr login`, `docker pull` und `docker push` mit **sudo** oder als Root ausführen.

Sie können jetzt Ihren eigenen Namensbereich in der privaten {{site.data.keyword.registrylong_notm}}-Registry einrichten.

## Container-Registry-Plug-in aktualisieren
{: #registry_cli_update}

Es kann sinnvoll sein, die {{site.data.keyword.registrylong_notm}}-CLI regelmäßig zu aktualisieren, um die neuen Funktionen nutzen zu können.
{:shortdesc}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Aktualisieren Sie das Container-Registry-Plug-in.

    ```
    ibmcloud plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  Stellen Sie sicher, dass das Plug-in erfolgreich aktualisiert wurde.

    ```
    ibmcloud plugin list
    ```
     {: pre}


## Container-Registry-Plug-in deinstallieren
{: #registry_cli_uninstall}

Wenn Sie das Container-Registry-Plug-in nicht mehr benötigen, können Sie es deinstallieren.
{:shortdesc}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Deinstallieren Sie das Container-Registry-Plug-in.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

3.  Stellen Sie sicher, dass das Plug-in erfolgreich deinstalliert wurde.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    Das Container-Registry-Plug-in wird in den Ergebnissen nicht angezeigt.


## Namensbereich einrichten
{: #registry_namespace_add}

Um Ihre Docker-Images sicher zu speichern, müssen Sie in der privaten {{site.data.keyword.registrylong_notm}}-Registry einen Namensbereich erstellen.
{:shortdesc}

Führen Sie zuvor Folgendes aus:

-   [Installieren Sie die {{site.data.keyword.Bluemix_notm}}-CLI und das Container-Registry-Plug-in](#registry_cli_install).
-   [Planen Sie, wie Sie Ihre Registry-Namensbereiche verwenden und benennen](registry_overview.html#registry_namespaces).

Erstellen Sie einen Namensbereich. Informationen dazu finden Sie im Abschnitt [Namensbereich konfigurieren](index.html#registry_namespace_add) in der Dokumentation zur Einführung.

Sie können jetzt [Docker-Images in den eigenen Namensbereich der {{site.data.keyword.Bluemix_notm}}-Registry mit Push-Operationen übertragen](registry_images_.html#registry_images_pushing) und diese Images mit anderen Benutzern in Ihrem Konto gemeinsam nutzen.

## Namensbereiche entfernen
{: #registry_remove}

Falls Sie einen Registry-Namensbereich nicht mehr benötigen, können Sie ihn aus Ihrem {{site.data.keyword.Bluemix_notm}}-Konto entfernen.
{:shortdesc}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Listen Sie die verfügbaren Namensbereiche auf.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3.  Entfernen Sie einen Namensbereich.

    **Achtung:** Wenn Sie einen Namensbereich entfernen, werden alle in diesem Namensbereich gespeicherten Images ebenfalls gelöscht. Diese Aktion kann nicht rückgängig gemacht werden.

    Ersetzen Sie im entsprechenden Befehl _&lt;eigener_namensbereich&gt;_ durch den Namensbereich, den Sie entfernen wollen.

    ```
    ibmcloud cr namespace-rm <eigener_namensbereich>
    ```
    {: pre}

    Nachdem Sie einen Namensbereich gelöscht haben, kann es abhängig von der Anzahl der darin gespeicherten Images einige Minuten dauern, bevor dieser Namensbereich für eine Wiederverwendung erneut zur Verfügung steht.
