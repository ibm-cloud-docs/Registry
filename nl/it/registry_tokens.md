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






# Automazione dell'accesso agli spazi dei nomi in {{site.data.keyword.registrylong_notm}} utilizzando i token
{: #registry_tokens}

Puoi utilizzare i token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi.
{:shortdesc}

Prima di iniziare, [installa la
CLI {{site.data.keyword.registrylong_notm}} e Docker](registry_setup_cli_namespace.html#registry_cli_install).

Un token di sicurezza consente a tutti i possessori del token di accedere alle informazioni protette. I token
vengono utilizzati in modo simile alle chiavi API. Creando un token per il tuo account {{site.data.keyword.Bluemix_notm}}, puoi concedere l'accesso a tutti i tuoi spazi dei nomi configurati in una regione per gli utenti esterni al tuo account {{site.data.keyword.Bluemix_notm}}. Ogni utente o applicazione in possesso
di questo token, può eseguire il push e il pull di immagini da e verso i tuoi spazi dei nomi senza dover installare il plug-in container-registry.

Quando crei un token per il tuo account {{site.data.keyword.Bluemix_notm}}, puoi decidere se tale token autorizza l'accesso in sola lettura (pull) o in scrittura (push e pull) al registro. Inoltre, puoi specificare se il token è permanente o se scade dopo 24 ore. Puoi creare
e utilizzare più token per controllare i diversi tipi di accesso.


## Creazione di un token per il tuo account {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_create}

Puoi creare un token per concedere l'accesso a tutti i tuoi spazi dei nomi {{site.data.keyword.registrylong_notm}} di una regione.
{:shortdesc}

1.  Crea un token. Nel seguente esempio viene creato un token senza scadenza che ha l'accesso in lettura e scrittura a tutti gli spazi dei nomi configurati in una regione.

    ```
    bx cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png"/> Descrizione dei componenti di questo comando</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>Facoltativo. Utilizza questa opzione per descrivere il token in modo da poterlo identificare più
facilmente in un secondo momento.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>Facoltativo. Utilizza questa opzione per creare un token senza scadenza. Se non specifichi questa opzione,
il token non sarà più valido dopo 24 ore. <br> **Suggerimento:** quando non hai più bisogno di un token senza scadenza per bloccare l'accesso ai tuoi spazi dei nomi, ricorda di rimuovere il token.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>Facoltativo. Utilizza questa opzione per creare un token che consenta agli utenti di eseguire il push e il pull di immagini da e verso
i tuoi spazi dei nomi. Se non specifichi questa opzione, il token può essere utilizzato solo per eseguire il pull delle immagini.</td>
        </tr>
        </tbody>
        </table>

    L'output della CLI sarà simile al seguente:

    ```
    Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad
    Token              <valore_token>
    ```
    {: screen}

2.  Verifica che il token sia stato creato.

    ```
    bx cr token-list
    ```
    {: pre}


## Utilizzo di un token per automatizzare l'accesso ai tuoi spazi dei nomi
{: #registry_tokens_use}

Puoi utilizzare un token nel tuo comando `docker login` per automatizzare l'accesso ai tuoi spazi dei nomi in {{site.data.keyword.registrylong_notm}}. A seconda che l'accesso impostato per il token sia di sola lettura o di lettura-scrittura, gli utenti possono eseguire il push e il pull delle immagini da e verso i tuoi spazi dei nomi.
{:shortdesc}

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Elenca tutti i token nel tuo account {{site.data.keyword.Bluemix_notm}} e prendi nota dell'ID token che vuoi utilizzare.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Richiama il valore per il token. Sostituisci &lt;id_token&gt; con
l'ID del token.

    ```
    bx cr token-get <id_token>
    ```
    {: pre}

    Il valore del token viene visualizzato in **Token** nell'output della CLI.

4.  Utilizza il token come parte del tuo comando `docker login`. Sostituisci &lt;valore_token&gt; con il valore del token richiamato nel passo precedente e &lt;url_registro&gt; con l'URL del registro in cui sono configurati i tuoi spazi dei nomi.

    -   Per gli spazi dei nomi configurati in Stati Uniti Sud: registry.ng.bluemix.net
    -   Per gli spazi dei nomi configurati in Regno Unito Sud: registry.eu-gb.bluemix.net
    -   Per gli spazi dei nomi configurati in Europa centrale: registry.eu-de.bluemix.net
    -   Per gli spazi dei nomi configurati in AP del sud: registry.au-syd.bluemix.net

    ```
    docker login -u token -p <valore_token> <url_registro>
    ```
    {: pre}

    Dopo aver effettuato l'accesso a Docker utilizzando il token, puoi eseguire il push o il pull delle immagini da e verso i tuoi spazi dei nomi.


## Rimozione di un token dal tuo account {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_remove}

Rimuovi un token {{site.data.keyword.registrylong_notm}} quando non ne hai più bisogno.
{:shortdesc}

**Nota:** i token {{site.data.keyword.registrylong_notm}} scaduti vengono rimossi automaticamente dal tuo account {{site.data.keyword.Bluemix_notm}} e non è necessario rimuoverli manualmente.

1.  Accedi a {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Elenca tutti i token nel tuo account {{site.data.keyword.Bluemix_notm}} e prendi nota dell'ID token che vuoi rimuovere.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Rimuovi il token.

    ```
    bx cr token-rm <id_token>
    ```
    {: pre}


