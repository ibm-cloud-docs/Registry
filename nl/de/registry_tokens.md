---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

# Zugriff auf {{site.data.keyword.registrylong_notm}} automatisieren
{: #registry_access}

Sie können einen {{site.data.keyword.iamlong}}-API-Schlüssel (IAM-API-Schlüssel) verwenden, um den Zugriff auf die {{site.data.keyword.registrylong_notm}}-Namensbereiche zu automatisieren, um so Push- und Pull-Operationen für Images auszuführen.
{:shortdesc}

Versuchen Sie, Ihre Registry-Images in Kubernetes-Implementierungen zu verwenden? Erfahren Sie, wie Sie [auf Images in anderen Kubernetes-Namensbereichen, {{site.data.keyword.cloud_notm}}-Regionen und -Konten](/docs/containers?topic=containers-images#other) zugreifen.
{: tip}

API-Schlüssel sind mit Ihrem Konto verknüpft und können im gesamten {{site.data.keyword.cloud_notm}} verwendet werden, sodass Sie nicht für jeden Service unterschiedliche Berechtigungsnachweise benötigen. Sie können den API-Schlüssel in der CLI oder als Teil der Automatisierung zur Anmeldung mit Ihrer Benutzeridentität verwenden.

Wenn Sie einen API-Schlüssel verwenden, können Sie den Zugriff auf Ihre Namensbereiche mithilfe von IAM-Richtlinien steuern. Weitere Informationen finden Sie unter [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry?topic=registry-user#user).

Weitere Informationen zu API-Schlüsseln für {{site.data.keyword.registrylong_notm}} finden Sie in [Mit API-Schlüsseln arbeiten](/docs/iam?topic=iam-manapikey#manapikey).

Bevor Sie beginnen, müssen Sie die [Befehlszeilenschnittstellen von {{site.data.keyword.registrylong_notm}} und Docker installieren](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Zugriff auf eigene Namensbereiche mithilfe von API-Schlüsseln automatisieren
{: #registry_api_key}

Durch die Verwendung von API-Schlüsseln können Sie Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre Namensbereiche automatisieren.
{:shortdesc}

### API-Schlüssel erstellen
{: #registry_api_key_create}

Sie können einen API-Schlüssel erstellen, mit dem Sie sich dann bei Ihrer Registry anmelden können.
{:shortdesc}

Sie können API-Schlüssel für Benutzer und API-Schlüssel für Service-IDs erstellen.

- Informationen zum Erstellen eines API-Schlüssels für Service-IDs finden Sie unter [API-Schlüssel für Service-ID erstellen](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
- Informationen zum Erstellen eines API-Schlüssels für Benutzer finden Sie unter [API-Schlüssel erstellen](/docs/iam?topic=iam-userapikey#create_user_key).

### Zugriff mithilfe eines API-Schlüssels automatisieren
{: #registry_api_key_use}

Sie können den Zugriff auf Ihre Namensbereiche in {{site.data.keyword.registrylong_notm}} mithilfe eines API-Schlüssels automatisieren.
{:shortdesc}

Verwenden Sie den API-Schlüssel für die Anmeldung bei Ihrer Registry, indem Sie den folgenden Docker-Befehl ausführen. Ersetzen Sie `<your_apikey>` durch Ihren API-Schlüssel und ersetzen Sie `<registry_url>` durch die URL der Registry, in der Ihre Namensbereiche eingerichtet sind.

- Verwenden Sie für Namensbereiche in der Region 'Asien-Pazifik (Norden)': `jp.icr.io`
- Verwenden Sie für Namensbereiche in der Region 'Asien-Pazifik (Süden)': `au.icr.io`
- Verwenden Sie für Namensbereiche in der Region 'Mitteleuropa': `de.icr.io`
- Verwenden Sie für Namensbereiche in der Region 'Großbritannien (Süden)': `uk.icr.io`
- Verwenden Sie für Namensbereiche in der Region 'Vereinigte Staaten (Süden)': `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Referenzinformationen zu diesem Befehl finden Sie in [Neuen API-Schlüssel für die {{site.data.keyword.cloud_notm}}-Plattform erstellen](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Authentifizierungsoptionen für alle Clients
{: #registry_authentication}

Sie können die Authentifizierung mit dem Befehl `docker login` oder mit anderen Registry-Clients durchführen.
{:shortdesc}

Die meisten Benutzer können den Befehl `ibmcloud cr login` verwenden, um den Befehl `docker login` zu vereinfachen; wenn Sie jedoch Automatisierung implementieren oder einen anderen Client verwenden, ist es möglicherweise empfehlenswert, die Authentifizierung manuell durchzuführen. Sie müssen einen Benutzernamen und ein Kennwort angeben. In {{site.data.keyword.registrylong_notm}} gibt der Benutzername den Typ des geheimen Schlüssels an, der im Kennwort angegeben wird.

Die folgenden Benutzernamen sind gültig:

- `iambearer`: Das Kennwort enthält ein IAM-Zugriffstoken. Diese Art der Authentifizierung ist nur kurze Zeit gültig, kann aber aus allen Typen der IAM-Identität abgeleitet werden.
- `iamrefresh`: Das Kennwort muss ein IAM-Aktualisierungstoken enthalten, das intern verwendet wird, um ein IAM-Zugriffstoken zu generieren und zu aktualisieren. Diese Art der Authentifizierung ist länger gültig und wird vom Befehl `ibmcloud cr login` verwendet.
- `iamapikey`: Das Kennwort ist ein IAM-API-Schlüssel. Diese Art der Authentifizierung wird für die Automatisierung bevorzugt. Sie können einen API-Schlüssel für Benutzer oder für Service-IDs verwenden; weitere Informationen finden Sie unter [API-Schlüssel erstellen](#registry_api_key_create).

Für die Authentifizierung bei der Registry muss nicht der Befehl `docker` verwendet werden. Beispielsweise können Sie Cloud Foundry-Apps aus Images in der Registry über die Cloud Foundry-Befehlszeilenschnittstelle starten.

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Ersetzen Sie `<apikey>` durch den API-Schlüssel, `<region>` durch den Namen Ihrer [Region](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` durch Ihren Namensbereich und `<image_repo>` durch das Repository.

Weitere Informationen finden Sie unter [Private Image-Registry verwenden](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
