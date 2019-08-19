---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-05"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, 

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

# {{site.data.keyword.registrylong_notm}}-CLI und eigenen Registry-Namensbereich einrichten
{: #registry_setup_cli_namespace}

Um Ihre Docker-Images in {{site.data.keyword.registrylong}} verwalten zu können, müssen Sie das CLI-Plug-in `container-registry` installieren und einen Namensbereich erstellen.
{:shortdesc}

Beziehen Sie keine personenbezogenen Daten in Ihre Container-Images, Namensbereichsnamen, Beschreibungsfelder oder in Image-Konfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) ein.
{: important}

Bevor Sie beginnen, installieren Sie die Befehlszeilenschnittstelle (CLI) von {{site.data.keyword.cloud_notm}}. Informationen finden Sie im Abschnitt [Einführung in die Befehlszeilenschnittstelle von {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started).

## `container-registry`-CLI-Plug-in installieren
{: #cli_namespace_registry_cli_install}

Installieren Sie das `container-registry`-CLI-Plug-in, um Namensbereiche und Docker-Images in {{site.data.keyword.registrylong_notm}} über die Befehlszeile zu verwalten.
{:shortdesc}

1. [Installieren Sie das `container-registry`-CLI-Plug-in. ](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Optional: [Konfigurieren Sie den Docker-Client für die Ausführung von Befehlen ohne Rootberechtigungen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.docker.com/install/linux/linux-postinstall/). Falls Sie diesen Schritt nicht ausführen, müssen Sie die Befehle `ibmcloud login`, `ibmcloud cr login`, `docker pull` und `docker push` mit `sudo` oder als Root ausführen.

Sie können jetzt einen eigenen [Namensbereich](#registry_namespace_setup) in {{site.data.keyword.registrylong_notm}} einrichten.

## `container-registry`-CLI-Plug-in aktualisieren
{: #registry_cli_update}

Sie können das `container-registry`-CLI-Plug-in regelmäßig aktualisieren, um neue Features zu nutzen.
{:shortdesc}

1. Aktualisieren Sie das `container-registry`-CLI-Plug-in.

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. Stellen Sie sicher, dass das `container-registry`-CLI-Plug-in erfolgreich aktualisiert wurde.

    ```
    ibmcloud plugin list
    ```
     {: pre}

## `container-registry`-CLI-Plug-in deinstallieren
{: #registry_cli_uninstall}

Wenn Sie das `container-registry`-CLI-Plug-in nicht mehr benötigen, können Sie es deinstallieren.
{:shortdesc}

1. Deinstallieren Sie das `container-registry`-CLI-Plug-in.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. Stellen Sie sicher, dass das `container-registry`-CLI-Plug-in erfolgreich deinstalliert wurde.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    Das `container-registry`-CLI-Plug-in wird in den Ergebnissen nicht angezeigt.

## Namensbereiche planen
{: #registry_setup_cli_namespace_plan}

{{site.data.keyword.registrylong_notm}} bietet eine private Multi-Tenant-Registry für Images, die von IBM gehostet und verwaltet wird. In dieser Registry können Sie Ihre Docker-Images speichern, indem Sie einen Registrynamensbereich einrichten.
{:shortdesc}

Wenn Sie separate Repositorys verwenden möchten (beispielsweise für Ihre Produktions- und Ihre Staging-Umgebungen), können Sie mehrere Namensbereiche einrichten. Falls Sie die Registry in mehreren {{site.data.keyword.cloud_notm}}-Regionen verwenden möchten, müssen Sie für jede Region einen eigenen Namensbereich einrichten. Namensbereiche sind innerhalb Regionen eindeutig. Sie können denselben Namensbereichsnamen für jede Region verwenden, solange niemand anderes einen Namensbereich mit diesem Namen in dieser Region eingerichtet hat.

Sie können den Zugriff auf Ihre Namensbereiche mithilfe von IAM-Richtlinien steuern. Weitere Informationen finden Sie unter [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry?topic=registry-user#user).

Wenn Sie ausschließlich mit den von IBM bereitgestellten öffentlichen Images arbeiten möchten, ist die Einrichtung eines Namensbereichs nicht erforderlich.

Wenn Sie sich nicht sicher sind, ob bereits ein Namensbereich für Ihr Konto eingerichtet ist, führen Sie den Befehl `ibmcloud cr namespace-list` aus, um vorhandene Namensbereichsinformationen abzurufen.
{:tip}

Beachten Sie bei der Wahl eines Namens für den Namensbereich die folgenden Regeln:

- Ihr Namensbereich muss in allen {{site.data.keyword.cloud_notm}}-Konten derselben Region eindeutig sein.
- Ihr Namensbereich muss 4 bis 30 Zeichen lang sein.
- Ihr Namensbereich muss mit einem Buchstaben oder einer Zahl beginnen und enden.
- Ihr Namensbereich darf ausschließlich Kleinbuchstaben, Zahlen, Bindestriche (-) und Unterstreichungszeichen (_) enthalten.

Beziehen Sie keine personenbezogenen Daten in Ihre Namensbereichsnamen ein.
{: important}

Nachdem Sie Ihren ersten Namensbereich eingerichtet haben, werden Sie dem kostenfreien Serviceplan für {{site.data.keyword.registrylong_notm}} zugewiesen, wenn Sie noch kein [Upgrade für Ihren Plan](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade) durchgeführt haben.

## Namensbereich einrichten
{: #registry_namespace_setup}

Sie müssen einen Namensbereich erstellen, um Docker-Images in {{site.data.keyword.registrylong_notm}} zu speichern.
{:shortdesc}

Führen Sie die folgenden Tasks aus, bevor Sie beginnen:

- [{{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle und das Plug-in `container-registry` der Befehlszeilenschnittstelle installieren](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Verwendung und Benennung der Registry-Namensbereiche planen](#registry_setup_cli_namespace_plan).

Informationen zum Erstellen eines Namensbereichs finden Sie im Abschnitt [Namensbereich konfigurieren](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add) in der Dokumentation zur Einführung.

Der Namensbereich muss in allen {{site.data.keyword.cloud_notm}}-Konten derselben Region eindeutig sein. Namensbereiche müssen 4 bis 30 Zeichen lang sein und dürfen nur Kleinbuchstaben, Zahlen, Bindestriche (-) und Unterstreichungszeichen (_) enthalten. Namensbereiche müssen mit einem Buchstaben oder einer Zahl beginnen und enden.
{: tip}

Sie können nun [Docker-Images per Push-Operation in Ihren Namensbereich in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) übertragen und diese Images mit anderen Benutzern in Ihrem Konto gemeinsam nutzen. Informationen zur Steuerung des Zugriffs auf Namensbereich in {{site.data.keyword.cloud_notm}} IAM finden Sie in [Richtlinien erstellen](/docs/services/Registry?topic=registry-user#create).

## Namensbereiche entfernen
{: #registry_remove}

Falls Sie einen Registry-Namensbereich nicht mehr benötigen, können Sie ihn aus Ihrem {{site.data.keyword.cloud_notm}}-Konto entfernen.
{:shortdesc}

1. Melden Sie sich bei {{site.data.keyword.cloud_notm}} an.

    ```
    ibmcloud login
    ```
    {: pre}

2. Listen Sie die verfügbaren Namensbereiche auf.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. Entfernen Sie einen Namensbereich.

    **Achtung:** Wenn Sie einen Namensbereich entfernen, werden alle in diesem Namensbereich gespeicherten Images ebenfalls gelöscht. Diese Aktion kann nicht rückgängig gemacht werden.

    Ersetzen Sie `<my_namespace>` durch den Namensbereich, der entfernt werden soll.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    Nachdem Sie einen Namensbereich gelöscht haben, kann es einige Minuten dauern, bis dieser Namensbereich wieder zur erneuten Verwendung verfügbar ist.
