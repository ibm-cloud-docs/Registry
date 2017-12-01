---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}






# Zugriff auf eigene Namensbereiche in {{site.data.keyword.registrylong_notm}} durch Tokens automatisieren
{: #registry_tokens}

Durch die Verwendung von Tokens können Sie Push- und Pull-Operationen für Docker-Images in Bezug auf Ihre Namensbereiche automatisieren.
{:shortdesc}

Bevor Sie beginnen, müssen Sie zunächst [{{site.data.keyword.registrylong_notm}} und die Docker-CLI installieren](registry_setup_cli_namespace.html#registry_cli_install).

Ein Sicherheitstoken ermöglicht jedem Benutzer, der im Besitz des Tokens ist, den Zugriff auf geschützte Daten. Token werden auf ähnliche Weise wie API-Schlüssel verwendet. Indem Sie ein Token für Ihr {{site.data.keyword.Bluemix_notm}}-Konto erstellen, können Sie allen Benutzern außerhalb Ihres {{site.data.keyword.Bluemix_notm}}-Kontos den Zugriff auf alle Ihre Namensbereiche erteilen, die Sie in einer Region eingerichtet haben. Jeder Benutzer bzw. jede App, der/die dieses Token besitzt, kann Push- und Pull-Operationen in Bezug auf Ihre Namensbereiche ausführen, ohne das Container-Registry-Plug-in zu installieren.

Wenn Sie ein Token für Ihr {{site.data.keyword.Bluemix_notm}}-Konto erstellen, können Sie entscheiden, ob das Token zum Lesezugriff (Pull-Operation) oder zum Schreibzugriff (Push- und Pull-Operation) auf die Registry berechtigen soll. Außerdem können Sie angeben, ob das Token permanent gültig sein oder nach 24 Stunden ablaufen soll. Sie können mehrere Token erstellen und verwenden, um unterschiedliche Zugriffstypen zu steuern.


## Token für {{site.data.keyword.Bluemix_notm}}-Konto erstellen
{: #registry_tokens_create}

Sie können ein Token erstellen, um den Zugriff auf alle Ihre {{site.data.keyword.registrylong_notm}}-Namensbereiche einer Region zu erteilen.
{:shortdesc}

1.  Erstellen Sie ein Token. Im folgenden Beispiel wird ein nicht ablaufendes Token erstellt, das über Lese- und Schreibzugriff auf alle Namensbereiche verfügt, die in einer Region eingerichtet wurden.

    ```
    bx cr token-add --description "Dies ist ein Token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png"/> Beschreibung der Befehlskomponenten</th>
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


## Zugriff auf Namensbereiche mit einem Token automatisieren
{: #registry_tokens_use}

Durch die Verwendung eines Tokens in Ihrem `docker login`-Befehl können Sie den Zugriff auf Ihre Namensbereiche in {{site.data.keyword.registrylong_notm}} automatisieren. Abhängig davon, ob Sie für Ihr Token einen schreibgeschützten Zugriff oder einen Schreib-/Lesezugriff festgelegt haben, können Benutzer Push- und Pull-Operationen für Images in Bezug auf Ihre Namensbereiche ausführen.
{:shortdesc}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    bx login
    ```
    {: pre}

2.  Listen Sie alle Token in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto auf und merken Sie sich die ID des Tokens, das Sie verwenden möchten.

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


## Token aus einem {{site.data.keyword.Bluemix_notm}}-Konto entfernen
{: #registry_tokens_remove}

Entfernen Sie ein {{site.data.keyword.registrylong_notm}}-Token, wenn Sie es nicht mehr benötigen.
{:shortdesc}

**Hinweis:** Abgelaufene {{site.data.keyword.registrylong_notm}}-Token werden automatisch aus Ihrem {{site.data.keyword.Bluemix_notm}}-Konto entfernt und müssen nicht manuell entfernt werden.

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    bx login
    ```
    {: pre}

2.  Listen Sie alle Token in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto auf und merken Sie sich die ID des Tokens, das Sie entfernen möchten.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Entfernen Sie das Token.

    ```
    bx cr token-rm <token_id>
    ```
    {: pre}


