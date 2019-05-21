---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

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

Bevor Sie Ihre Docker-Images in {{site.data.keyword.registrylong}} speichern können, müssen Sie einen Namensbereich erstellen. Installieren Sie das `container-registry`-CLI-Plug-in, um mit Namensbereichen zu arbeiten.
{:shortdesc}

Beziehen Sie keine personenbezogenen Daten in Ihre Container-Images, Namensbereichsnamen, Beschreibungsfelder (z. B. in Registry-Tokens) oder in Image-Konfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) ein.
{: important}

Bevor Sie beginnen, installieren Sie die Befehlszeilenschnittstelle (CLI) von [{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

## `container-registry`-CLI-Plug-in installieren
{: #cli_namespace_registry_cli_install}

Installieren Sie das `container-registry`-CLI-Plug-in, um Namensbereiche und Docker-Images in {{site.data.keyword.registrylong_notm}} über die Befehlszeile zu verwalten.
{:shortdesc}

1. [Installieren Sie das `container-registry`-CLI-Plug-in. ](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Optional: [Konfigurieren Sie den Docker-Client für die Ausführung von Befehlen ohne Rootberechtigungen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.docker.com/install/linux/linux-postinstall/). Falls Sie diesen Schritt nicht ausführen, müssen Sie die Befehle `ibmcloud login`, `ibmcloud cr login`, `docker pull` und `docker push` mit `sudo` oder als Root ausführen.

Sie können jetzt einen eigenen Namensbereich in {{site.data.keyword.registrylong_notm}} einrichten.

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

## Namensbereich einrichten
{: #registry_namespace_setup}

Sie müssen einen Namensbereich erstellen, um Docker-Images in {{site.data.keyword.registrylong_notm}} zu speichern.
{:shortdesc}

**Vorbereitung**

- [{{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle und das Plug-in `container-registry` der Befehlszeilenschnittstelle installieren](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Verwendung und Benennung der Registry-Namensbereiche planen](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces).

<br>
Informationen zum Erstellen eines Namensbereichs finden Sie im Abschnitt [Namensbereich konfigurieren](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add) in der Dokumentation zur Einführung.

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
