---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security


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

# Erste Schritte mit {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}} bietet eine private Multi-Tenant-Registry für Images, mit der Sie Ihre Docker-Images speichern und mit Benutzern in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto gemeinsam nutzen können.
{:shortdesc}

Die {{site.data.keyword.Bluemix_notm}}-Konsole enthält eine kurze Anleitung zum Schnelleinstieg. Weitere Informationen zu Verwendung der {{site.data.keyword.Bluemix_notm}}-Konsole finden Sie unter [Imagesicherheit mit Vulnerability Advisor verwalten](/docs/services/va/va_index.html).

Beziehen Sie keine personenbezogenen Daten in Ihre Container-Images, Namensbereichsnamen, Beschreibungsfelder (z. B. in Registry-Tokens) oder in Image-Konfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) ein.
{:tip}

## {{site.data.keyword.registrylong_notm}}-CLI installieren
{: #registry_cli_install}

1. Installieren Sie die [Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview), damit Sie die `ibmcloud`-Befehle von {{site.data.keyword.Bluemix_notm}} ausführen können. Bei dieser Installation werden auch die Plug-ins der Befehlszeilenschnittstelle für {{site.data.keyword.containerlong_notm}} und {{site.data.keyword.registrylong_notm}} installiert.

## Namensbereich einrichten
{: #registry_namespace_add}

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

   ```
   ibmcloud login
   ```
   {: pre}

   Wenn Sie über eine föderierte ID verfügen, melden Sie sich mit dem folgenden Befehl an: 

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. Fügen Sie einen Namensbereich hinzu, um Ihr eigenes Image-Repository zu erstellen. Ersetzen Sie `<my_namespace>` durch den gewünschten Namensbereich. 

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

3. Führen Sie den Befehl `ibmcloud cr namespace-list` aus, um sicherzustellen, dass der Namensbereich erstellt wurde.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Images mit einer Pull-Operation aus einer anderen Registry auf die lokale Maschine mit Pull-Operation extrahieren
{: #registry_images_pulling}

1. [Installieren Sie die Docker-CLI ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.docker.com/community-edition#/download). Für Windows 8 oder OS X Yosemite 10.10.x oder frühere Versionen installieren Sie stattdessen die [Docker-Toolbox ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.docker.com/toolbox/). {{site.data.keyword.registrylong_notm}} unterstützt Docker Engine v1.12.6 oder eine höhere Version.

2. Laden Sie das Image auf Ihre lokale Maschine herunter (_mit Pull-Operation extrahieren_). Ersetzen Sie `<source_image>` durch das Repository des Images und `<tag>` durch den Tag des Images, das verwendet werden soll, z. B. _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Beispiel, bei dem für `<source_image>` der Wert `hello-world` und für `<tag>` der Wert `latest` verwendet wird:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Kennzeichnen Sie das Image. Ersetzen Sie `<source_image>` durch das Repository und `<tag>` durch den Tag des lokalen Image, das Sie zuvor mit einer Pull-Operation extrahiert haben. Ersetzen Sie `<region>` durch den Namen Ihrer [Region](/docs/services/Registry/registry_overview.html#registry_regions). Ersetzen Sie `<my_namespace>` durch den Namensbereich, den Sie in [Namensbereich einrichten](/docs/services/Registry/index.html#registry_namespace_add) erstellt haben. Definieren Sie das Repository und den Tag des Images, die Sie in Ihrem Namensbereich verwenden möchten. Ersetzen Sie dazu `<new_image_repo>` und `<new_tag>`.

   ```
   docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Beispiel, bei dem für `<source_image>` der Wert `hello-world`, für `<tag>` der Wert `latest`, für `<region>` der Wert `eu-gb`, für `<my_namespace>` der Wert `namespace1`, für `<new_image_repo>` der Wert `hw_repo` und für `<new_tag>` der Wert `1` verwendet wird:

   ```
   docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

## Docker-Images mit Push-Operation in den eigenen Namensbereich übertragen
{: #registry_images_pushing}

1. Führen Sie den Befehl `ibmcloud cr login` aus, um Ihren lokalen Docker-Dämon in {{site.data.keyword.registrylong_notm}} zu protokollieren.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Laden Sie das Image in Ihren Namensbereich hoch (_mit Push-Operation übertragen_). Ersetzen Sie `<my_namespace>` durch den Namensbereich, den Sie in [Namensbereich einrichten](/docs/services/Registry/index.html#registry_namespace_add) erstellt haben, und `<image_repo>` und `<tag>` durch das Repository und den Tag des Images, die Sie beim Tagging des Images ausgewählt haben. 

   ```
   docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}

   Beispiel, bei dem für `<region>` der Wert `eu-gb`, für `<my_namespace>` der Wert `namespace1`, für `<image_repo>` der Wert `hw_repo` und für `<tag>` der Wert `1` verwendet wird:

   ```
   docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}
   

3. Überprüfen Sie, ob das Image erfolgreich mit der Push-Operation übertragen wurde, indem Sie den folgenden Befehl ausführen.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Herzlichen Glückwunsch! Sie haben einen Namensbereich in {{site.data.keyword.registrylong_notm}} konfiguriert und mit Push-Operation Ihr erstes Image an Ihren Namensbereich übertragen.

**Wie geht es weiter?**

- [Imagesicherheit mit Vulnerability Advisor verwalten](/docs/services/va/va_index.html)
- [Servicepläne und Nutzung überprüfen](/docs/services/Registry/registry_overview.html#registry_plans).
- [Weitere Images in Ihrem Namensbereich speichern und verwalten](/docs/services/Registry/registry_images_.html)
- [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry/registry_users.html#user)
- [Cluster und Workerknoten einrichten](/docs/containers/cs_clusters.html#clusters)
