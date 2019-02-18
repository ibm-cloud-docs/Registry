---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Zugriff auf {{site.data.keyword.registrylong_notm}} automatisieren
{: #registry_access}

Sie können entweder Registry-Tokens oder einen {{site.data.keyword.iamlong}}-API-Schlüssel (IAM-API-Schlüssel) verwenden, um den Zugriff auf die {{site.data.keyword.registrylong_notm}}-Namensbereiche zu automatisieren, um so Push- und Pull-Operationen für Images auszuführen.
{:shortdesc}

Versuchen Sie, Ihre Registry-Images in Kubernetes-Implementierungen zu verwenden? Erfahren Sie, wie Sie [auf Images in anderen Kubernetes-Namensbereichen, {{site.data.keyword.Bluemix_notm}}-Regionen und -Konten](/docs/containers/cs_images.html#other) zugreifen.
{: tip}

API-Schlüssel sind mit Ihrem Konto verknüpft und können im gesamten {{site.data.keyword.Bluemix_notm}} verwendet werden, sodass Sie nicht für jeden Service unterschiedliche Berechtigungsnachweise benötigen. Sie können den API-Schlüssel in der CLI oder als Teil der Automatisierung zur Anmeldung mit Ihrer Benutzeridentität verwenden.

Registry-Tokens sind ausschließlich für {{site.data.keyword.registrylong_notm}} bereichsorientiert festgelegt. Sie können sie auf Lesezugriff begrenzen und Sie können auswählen, ob ein Ablaufdatum gelten soll.

Wenn Sie einen API-Schlüssel verwenden, können Sie den Zugriff auf Ihre Namensbereiche mithilfe von IAM-Richtlinien steuern. Weitere Informationen finden Sie unter [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry/registry_users.html#user).

Weitere Informationen zu API-Schlüsseln für {{site.data.keyword.registrylong_notm}} finden Sie in [Mit API-Schlüsseln arbeiten](/docs/iam/apikeys.html#manapikey).

Bevor Sie beginnen, müssen Sie die [{{site.data.keyword.registrylong_notm}}- und Docker-CLI](/docs/services/Registry/registry_setup_cli_namespace.html#registry_cli_install) installieren. 

## Zugriff auf eigene Namensbereiche mithilfe von API-Schlüsseln automatisieren
{: #registry_api_key}

Durch die Verwendung von API-Schlüsseln können Sie Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre Namensbereiche automatisieren.
{:shortdesc}

### API-Schlüssel erstellen
{: #registry_api_key_create}

Sie können einen API-Schlüssel erstellen, mit dem Sie sich dann bei Ihrer Registry anmelden können.
{:shortdesc}

Sie können API-Schlüssel für Benutzer und API-Schlüssel für Service-IDs erstellen.

- Informationen zum Erstellen eines API-Schlüssels für Service-IDs finden Sie unter [API-Schlüssel für Service-ID erstellen](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id).
- Informationen zum Erstellen eines API-Schlüssels für Benutzer finden Sie unter [API-Schlüssel erstellen](/docs/iam/userid_keys.html#creating-an-api-key).

### Zugriff mithilfe eines API-Schlüssels automatisieren
{: #registry_api_key_use}

Sie können den Zugriff auf Ihre Namensbereiche in {{site.data.keyword.registrylong_notm}} mithilfe eines API-Schlüssels automatisieren.
{:shortdesc}

Verwenden Sie den API-Schlüssel für die Anmeldung bei Ihrer Registry, indem Sie den folgenden Docker-Befehl ausführen. Ersetzen Sie &lt;eigener API-Schlüssel&gt; durch Ihren API-Schlüssel und ersetzen Sie &lt;Registry-URL&gt; durch die URL der Registry, in der Ihre Namensbereiche eingerichtet sind.

- Verwenden Sie für Namensbereiche in der Region 'Vereinigte Staaten (Süden)': `registry.ng.bluemix.net`
- Verwenden Sie für Namensbereiche in der Region 'Großbritannien (Süden)': `registry.eu-gb.bluemix.net`
- Verwenden Sie für Namensbereiche in der Region 'Mitteleuropa': `registry.eu-de.bluemix.net`
- Verwenden Sie für Namensbereiche in der Region 'Asien-Pazifik (Süden)': `registry.au-syd.bluemix.net`

```
docker login -u iamapikey -p <eigener API-Schlüssel> <Registry-URL>
```
{: pre}

Referenzinformationen zu diesem Befehl finden Sie in [Neuen API-Schlüssel für die {{site.data.keyword.Bluemix_notm}}-Plattform erstellen](/docs/cli/reference/ibmcloud/cli_api_policy.html#ibmcloud_iam_api_key_create).

## Zugriff auf eigene Namensbereiche durch Tokens automatisieren
{: #registry_tokens}

Durch die Verwendung von Tokens können Sie Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche automatisieren.
{:shortdesc}

Jeder Benutzer, der über ein Registry-Token verfügt, kann auf auf geschützte Informationen zugreifen. Wenn Sie möchten, dass Benutzer außerhalb Ihres Kontos auf alle Ihre Namensbereiche zugreifen können, die Sie in einer Region eingerichtet haben, können Sie ein Token für Ihr {{site.data.keyword.Bluemix_notm}}-Konto erstellen. Jeder Benutzer bzw. jede App, der/die über dieses Token verfügt, kann Images per Push-Operation in Ihre Namensbereiche übertragen und Images per Pull-Operation aus Ihren Namensbereichen abrufen, ohne dass das `container-registry`-CLI-Plug-in installiert werden muss. 

Wenn Sie ein Token für Ihr {{site.data.keyword.Bluemix_notm}}-Konto erstellen, können Sie entscheiden, ob das Token zum Lesezugriff (Pull-Operation) oder zum Schreibzugriff (Push- und Pull-Operation) auf die Registry berechtigen soll. Außerdem können Sie angeben, ob das Token permanent gültig sein oder nach 24 Stunden ablaufen soll. Sie können mehrere Tokens erstellen und verwenden, um unterschiedliche Zugriffstypen zu steuern.

Wenn Sie sich mithilfe eines Registry-Tokens bei {{site.data.keyword.registrylong_notm}} anmelden, werden Ihre IAM-Zugriffsrichtlinien nicht umgesetzt. Wenn Sie den Zugriff auf einen oder mehrere Namensbereiche für eine ID beschränken möchten, die bei der Automatisierung verwendet wird, sollten Sie die Verwendung eines API-Schlüssels der IAM-Service-ID anstelle eines Registry-Tokens in Betracht ziehen. Weitere Informationen zum Erstellen eines API-Schlüssels und zum Verwenden des Schlüssels mit {{site.data.keyword.registrylong_notm}} finden Sie unter [Zugriff auf eigene Namensbereiche mithilfe von API-Schlüsseln automatisieren](#registry_api_key).

Mit den folgenden Tasks können Sie Ihre Tokens verwalten:

- [Token für das {{site.data.keyword.Bluemix_notm}}-Konto erstellen](#registry_tokens_create)
- [Zugriff auf Namensbereiche mit einem Token automatisieren](#registry_tokens_use)
- [Token vom {{site.data.keyword.Bluemix_notm}}-Konto entfernen](#registry_tokens_remove)

### Token für {{site.data.keyword.Bluemix_notm}}-Konto erstellen
{: #registry_tokens_create}

Sie können ein Token erstellen, um den Zugriff auf alle Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche in einer Region zu erteilen.
{:shortdesc}

1. Erstellen Sie ein Token. Im folgenden Beispiel wird ein nicht ablaufendes Token erstellt, das über Lese- und Schreibzugriff auf alle Namensbereiche verfügt, die in einer Region eingerichtet wurden.

   ```
   ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
   ```
   {: pre}

   <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="Glühlampensymbol"/> Beschreibung der Befehlskomponenten</th>
        </thead>
          <caption>Tabelle 1. Die Komponenten des Befehls `ibmcloud cr token-add`. </caption>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>Optional. Verwenden Sie diese Option, um das Token zu beschreiben, damit Sie es später einfacher erkennen können.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>Optional. Verwenden Sie diese Option, um ein nicht ablaufendes Token zu erstellen. Falls Sie diese Option nicht angeben, wird das Token nach 24 Stunden ungültig. <br> **Tipp:** Denken Sie daran, ein nicht ablaufendes Token zu entfernen, wenn Sie es nicht mehr zur Sperrung des Zugriffs auf Ihre Namensbereiche benötigen.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>Optional. Verwenden Sie diese Option, um ein Token zu erstellen, das Benutzern Push- und Pull-Operationen für Images in Bezug auf Ihren Namensbereich ermöglicht. Falls Sie diese Option nicht angeben, kann das Token nur zu Pull-Operationen für Images verwendet werden.</td>
        </tr>
        </tbody>
   </table>

   Die CLI-Ausgabe sieht in etwa wie folgt aus:

   ```
   Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad
   Token              eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJpYm0uY29tIiwibmFtZSI6Ikdpbm5pIFJvbWV0dHkiLCJpYXQiOjE1NDYzMDA4MDB9.wYMmTPHmrqhyHtgw5T8lbl1hxr2ykHq5T5s3mvMxjDw
   ```
   {: screen}

2. Überprüfen Sie, ob das Token erstellt wurde.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

### Zugriff auf Namensbereiche mit einem Token automatisieren
{: #registry_tokens_use}

Durch die Verwendung eines Tokens in Ihrem `docker login`-Befehl können Sie den Zugriff auf Ihre Namensbereiche in {{site.data.keyword.registrylong_notm}} automatisieren. Abhängig davon, ob Sie für Ihr Token einen schreibgeschützten Zugriff oder einen Schreib-/Lesezugriff festgelegt haben, können Benutzer Push- und Pull-Operationen für Images in Bezug auf Ihre Namensbereiche ausführen.
{:shortdesc}

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

   ```
   ibmcloud login
   ```
   {: pre}

2. Listen Sie alle Tokens in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto auf und merken Sie sich die ID des Tokens, das Sie verwenden möchten.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. Rufen Sie den Tokenwert für das Token ab. Ersetzen Sie im folgenden Befehl &lt;token-id&gt; durch die ID des Tokens.

   ```
   ibmcloud cr token-get <token-id>
   ```
   {: pre}

    Ihr Tokenwert wird im Feld **Token** in der CLI-Ausgabe angezeigt.

4. Verwenden Sie das Token als Bestandteil des Befehls `docker login`. Ersetzen Sie &lt;tokenwert&gt; durch den im vorherigen Schritt abgerufenen Tokenwert und &lt;registry_url&gt; durch die URL der Registry, in der Ihre Namensbereiche eingerichtet wurden.

   - Verwenden Sie für Namensbereiche in der Region 'Vereinigte Staaten (Süden)': `registry.ng.bluemix.net`
   - Verwenden Sie für Namensbereiche in der Region 'Großbritannien (Süden)': `registry.eu-gb.bluemix.net`
   - Verwenden Sie für Namensbereiche in der Region 'Mitteleuropa': `registry.eu-de.bluemix.net`
   - Verwenden Sie für Namensbereiche in der Region 'Asien-Pazifik (Süden)': `registry.au-syd.bluemix.net`

   ```
   docker login -u token -p <tokenwert> <registry_url>
   ```
   {: pre}

   Stellen Sie für den Parameter `-u` sicher, dass Sie die Zeichenfolge `token` eingeben und nicht die Token-ID.
   {: tip}

   Nachdem Sie sich unter Verwendung des Tokens bei Docker angemeldet haben, können Sie Push- oder Pull-Operationen für Images in Bezug auf Ihre Namensbereiche ausführen.

### Token aus einem {{site.data.keyword.Bluemix_notm}}-Konto entfernen
{: #registry_tokens_remove}

Entfernen Sie ein {{site.data.keyword.registrylong_notm}}-Token, wenn Sie es nicht mehr benötigen.
{:shortdesc}

Abgelaufene {{site.data.keyword.registrylong_notm}}-Tokens werden automatisch aus Ihrem {{site.data.keyword.Bluemix_notm}}-Konto entfernt und müssen nicht manuell entfernt werden.
{:tip}

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

   ```
   ibmcloud login
   ```
   {: pre}

2. Listen Sie alle Tokens in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto auf und merken Sie sich die ID des Tokens, das Sie entfernen möchten.

   ```
   ibmcloud cr token-list
   ```
   {: pre}

3. Entfernen Sie das Token.

   ```
   ibmcloud cr token-rm <token-id>
   ```
   {: pre}

## Authentifizierungsoptionen für alle Clients
{: #registry_authentication}

Sie können die Authentifizierung mit dem Befehl `docker login` oder mit anderen Registry-Clients durchführen.
{:shortdesc}

Die meisten Benutzer können den Befehl `ibmcloud cr login` verwenden, um den Befehl `docker login` zu vereinfachen; wenn Sie jedoch Automatisierung implementieren oder einen anderen Client verwenden, ist es möglicherweise empfehlenswert, die Authentifizierung manuell durchzuführen. Sie müssen einen Benutzernamen und ein Kennwort angeben. In {{site.data.keyword.registrylong_notm}} gibt der Benutzername den Typ des geheimen Schlüssels an, der im Kennwort angegeben wird.

Die folgenden Benutzernamen sind gültig:

- `iambearer`: Das Kennwort enthält ein IAM-Zugriffstoken. Diese Art der Authentifizierung ist nur kurze Zeit gültig, kann aber aus allen Typen der IAM-Identität abgeleitet werden.
- `iamrefresh`: Das Kennwort muss ein IAM-Aktualisierungstoken enthalten, das intern verwendet wird, um ein IAM-Zugriffstoken zu generieren und zu aktualisieren. Diese Art der Authentifizierung ist länger gültig und wird vom Befehl `ibmcloud cr login` verwendet.
- `iamapikey`: Das Kennwort ist ein IAM-API-Schlüssel. Diese Art der Authentifizierung wird für die Automatisierung bevorzugt. Sie können einen API-Schlüssel für Benutzer oder für Service-IDs verwenden; weitere Informationen finden Sie unter [API-Schlüssel erstellen](#registry_api_key_create).
- `token`: Das Kennwort ist ein Registry-Token. Dieser Benutzername kann für die Automatisierung verwendet werden.

Für die Authentifizierung bei der Registry muss nicht der Befehl `docker` verwendet werden. Beispielsweise können Sie Cloud Foundry-Apps aus Images in der Registry über die Cloud Foundry-Befehlszeilenschnittstelle starten.

```
export CF_DOCKER_PASSWORD=<api-schlüssel>
ibmcloud cf push appname  -o registry.<region>.bluemix.net/<eigener_namensbereich>/<image-repository> --docker-username iamapikey
```
{: pre}

Ersetzen Sie _&lt;api-schlüssel&gt;_ durch Ihren API-Schlüssel, _&lt;region&gt;_ durch den Namen Ihrer
[Region](/docs/services/Registry/registry_overview.html#registry_regions), _&lt;eigener_namensbereich&gt;_ durch Ihren Namensbereich und _&lt;image-repository&gt;_ durch das Repository.

Weitere Informationen finden Sie unter [Private Image-Registry verwenden](/docs/services/ContinuousDelivery/pipeline_custom_docker_images.html#private_image_registry).
