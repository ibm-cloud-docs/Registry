---

copyright:
  years: 2017
lastupdated: "2017-12-08"

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

API-Schlüssel sind mit Ihrem Konto verknüpft und können im gesamten {{site.data.keyword.Bluemix_notm}} verwendet werden, sodass Sie nicht für jeden Service unterschiedliche Berechtigungsnachweise benötigen. Sie können den API-Schlüssel in der CLI oder als Teil der Automatisierung zur Anmeldung mit Ihrer Benutzeridentität verwenden.

Registry-Tokens sind ausschließlich für {{site.data.keyword.registrylong_notm}} bereichsorientiert festgelegt. Sie können sie auf Lesezugriff begrenzen und Sie können auswählen, ob ein Ablaufdatum gelten soll.

Weitere Informationen zu API-Schlüsseln für {{site.data.keyword.registrylong_notm}} finden Sie in [Mit API-Schlüsseln arbeiten](../../iam/apikeys.html#manapikey).

Bevor Sie beginnen, müssen Sie zunächst [{{site.data.keyword.registrylong_notm}} und die Docker-CLI installieren](registry_setup_cli_namespace.html#registry_cli_install).


## Zugriff auf eigene Namensbereiche mithilfe von API-Schlüsseln automatisieren
{: #registry_api_key}

Durch die Verwendung von API-Schlüsseln können Sie Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre Namensbereiche automatisieren.
{:shortdesc}

### API-Schlüssel erstellen
{: #registry_api_key_create}

Sie können einen API-Schlüssel erstellen, mit dem Sie sich dann bei Ihrer Registry anmelden können.
{:shortdesc} 

Informationen zum Erstellen eines IAM-API-Schlüssels finden Sie in [API-Schlüssel erstellen](../../iam/userid_keys.html#creating-an-api-key). 

### Zugriff mithilfe eines API-Schlüssels automatisieren
{: #registry_api_key_use}

Sie können den Zugriff auf Ihre Namensbereiche in {{site.data.keyword.registrylong_notm}} mithilfe eines API-Schlüssels automatisieren.
{:shortdesc} 

Verwenden Sie den API-Schlüssel für die Anmeldung bei Ihrer Registry, indem Sie den folgenden Docker-Befehl ausführen. Ersetzen Sie &lt;eigener API-Schlüssel&gt; durch Ihren API-Schlüssel und ersetzen Sie &lt;Registry-URL&gt; durch die URL der Registry, in der Ihre Namensbereiche eingerichtet sind.

```
docker login -u iamapikey -p <eigener API-Schlüssel> <Registry-URL>
```
{: pre}


Referenzinformationen zu diesem Befehl finden Sie in [Neuen API-Schlüssel für die {{site.data.keyword.Bluemix_notm}}-Plattform erstellen](../../cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_api_key_create).


## Zugriff auf eigene Namensbereiche durch Tokens automatisieren
{: #registry_tokens}

Durch die Verwendung von Tokens können Sie Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche automatisieren.
{:shortdesc}

Jeder Benutzer, der über ein Registry-Token verfügt, kann auf auf geschützte Informationen zugreifen. Indem Sie ein Token für Ihr {{site.data.keyword.Bluemix_notm}}-Konto erstellen, können Sie allen Benutzern außerhalb Ihres {{site.data.keyword.Bluemix_notm}}-Kontos den Zugriff auf alle Ihre Namensbereiche erteilen, die Sie in einer Region eingerichtet haben. Jeder Benutzer bzw. jede App, der/die dieses Token besitzt, kann Push- und Pull-Operationen in Bezug auf Ihre Namensbereiche ausführen, ohne das Container-Registry-Plug-in zu installieren. 

Wenn Sie ein Token für Ihr {{site.data.keyword.Bluemix_notm}}-Konto erstellen, können Sie entscheiden, ob das Token zum Lesezugriff (Pull-Operation) oder zum Schreibzugriff (Push- und Pull-Operation) auf die Registry berechtigen soll. Außerdem können Sie angeben, ob das Token permanent gültig sein oder nach 24 Stunden ablaufen soll. Sie können mehrere Tokens erstellen und verwenden, um unterschiedliche Zugriffstypen zu steuern.

Mit den folgenden Tasks können Sie Ihre Tokens verwalten:

-  [Token für das {{site.data.keyword.Bluemix_notm}}-Konto erstellen](#registry_tokens_create)
-  [Zugriff auf Namensbereiche mit einem Token automatisieren](#registry_tokens_use)
-  [Token vom {{site.data.keyword.Bluemix_notm}}-Konto entfernen](#registry_tokens_remove)


### Token für {{site.data.keyword.Bluemix_notm}}-Konto erstellen
{: #registry_tokens_create}

Sie können ein Token erstellen, um den Zugriff auf alle Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche in einer Region zu erteilen.
{:shortdesc}

1.  Erstellen Sie ein Token. Im folgenden Beispiel wird ein nicht ablaufendes Token erstellt, das über Lese- und Schreibzugriff auf alle Namensbereiche verfügt, die in einer Region eingerichtet wurden.

    ```
    bx cr token-add --description "Dies ist ein Token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="Glühlampensymbol"/> Beschreibung der Befehlskomponenten</th>
        </thead>
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
    Token              <tokenwert>
    ```
    {: screen}

2.  Überprüfen Sie, ob das Token erstellt wurde.

    ```
    bx cr token-list
    ```
    {: pre}


### Zugriff auf Namensbereiche mit einem Token automatisieren 
{: #registry_tokens_use}

Durch die Verwendung eines Tokens in Ihrem `docker login`-Befehl können Sie den Zugriff auf Ihre Namensbereiche in {{site.data.keyword.registrylong_notm}} automatisieren. Abhängig davon, ob Sie für Ihr Token einen schreibgeschützten Zugriff oder einen Schreib-/Lesezugriff festgelegt haben, können Benutzer Push- und Pull-Operationen für Images in Bezug auf Ihre Namensbereiche ausführen.
{:shortdesc}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    bx login
    ```
    {: pre}

2.  Listen Sie alle Tokens in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto auf und merken Sie sich die ID des Tokens, das Sie verwenden möchten.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Rufen Sie den Tokenwert für das Token ab. Ersetzen Sie im folgenden Befehl &lt;token-id&gt; durch die ID des Tokens.

    ```
    bx cr token-get <token_id>
    ```
    {: pre}

    Ihr Tokenwert wird im Feld **Token** in der CLI-Ausgabe angezeigt.

4.  Verwenden Sie das Token als Bestandteil des Befehls `docker login`. Ersetzen Sie &lt;tokenwert&gt; durch den im vorherigen Schritt abgerufenen Tokenwert und &lt;registry_url&gt; durch die URL der Registry, in der Ihre Namensbereiche eingerichtet wurden.

    -   Namensbereiche in der Region 'Vereinigte Staaten (Süden)': registry.ng.bluemix.net
    -   Namensbereiche in der Region 'Großbritannien (Süden)': registry.eu-gb.bluemix.net
    -   Namensbereiche in der Region 'Zentraleuropa': registry.eu-de.bluemix.net
    -   Namensbereiche in der Region 'Asien-Pazifik (Süden)': registry.au-syd.bluemix.net

    ```
    docker login -u token -p <tokenwert> <registry_url>
    ```
    {: pre}

    Nachdem Sie sich unter Verwendung des Tokens bei Docker angemeldet haben, können Sie Push- oder Pull-Operationen für Images in Bezug auf Ihre Namensbereiche ausführen.


### Token aus einem {{site.data.keyword.Bluemix_notm}}-Konto entfernen
{: #registry_tokens_remove}

Entfernen Sie ein {{site.data.keyword.registrylong_notm}}-Token, wenn Sie es nicht mehr benötigen.
{:shortdesc}

**Hinweis:** Abgelaufene {{site.data.keyword.registrylong_notm}}-Tokens werden automatisch aus Ihrem {{site.data.keyword.Bluemix_notm}}-Konto entfernt und müssen nicht manuell entfernt werden.

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    bx login
    ```
    {: pre}

2.  Listen Sie alle Tokens in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto auf und merken Sie sich die ID des Tokens, das Sie entfernen möchten.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Entfernen Sie das Token.

    ```
    bx cr token-rm <token_id>
    ```
    {: pre}
    


