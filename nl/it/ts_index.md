---

copyright:
  years: 2017
lastupdated: "2017-10-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# Risoluzione dei problemi
{: #ts_index}

Qui troverai le risposte alle domande per la risoluzione dei problemi comuni relativi all'utilizzo di {{site.data.keyword.registrylong}}.
{:shortdesc}


## Come ottenere aiuto e supporto per {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Se hai delle domande o dei problemi quando utilizzi {{site.data.keyword.registrylong_notm}}, puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Puoi anche aprire un ticket di supporto {{site.data.keyword.IBM_notm}}.

Se utilizzi i forum per fare una domanda, contrassegna la tua domanda con una tag in modo che sia visualizzabile dal team di sviluppo {{site.data.keyword.registrylong_notm}}.

-   Se hai domande tecniche sullo sviluppo o sulla distribuzione di un'applicazione con {{site.data.keyword.registrylong_notm}}, inserisci la tua domanda in [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) e contrassegnala con le tag `ibm-bluemix` e `container-registry`.
-   Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Includi le tag `bluemix` e `container-registry`.

Consulta [Come ottenere supporto](../../support/index.html#getting-help) per ulteriori dettagli sull'utilizzo dei forum.

Per informazioni su come aprire un ticket di supporto {{site.data.keyword.IBM_notm}} o sui livelli di supporto e sulla gravità dei ticket, vedi [Come contattare il supporto](../../support/index.html#contacting-support).

## Accesso a {{site.data.keyword.registrylong_notm}} non riuscito
{: #ts_login}

Non puoi accedere a {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
Il comando `bx cr login` ha avuto esisto negativo.

{: tsCauses}
-   Il plug-in container-registry non è aggiornato e deve esserlo.
-   Docker non è installato sulla tua macchina locale o non è in esecuzione.
-   Le tue credenziali di accesso {{site.data.keyword.Bluemix_notm}} sono scadute.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

-   Esegui l'aggiornamento alla versione più recente del plug-in {{site.data.keyword.registryshort_notm}}; vedi [Aggiornamento del plug-in {{site.data.keyword.registrylong_notm}} (`bx cr`)](registry_setup_cli_namespace.html#registry_cli_update).
-   Assicurati che Docker sia installato sulla tua macchina. Se è già installato, riavvia il daemon Docker.
-   Riesegui il comando `bx login` per aggiornare le tue credenziali di accesso {{site.data.keyword.Bluemix_notm}}.


## I comandi {{site.data.keyword.registrylong_notm}} hanno esito negativo con `'cr' non è un comando registrato. Vedi 'bx help'. `
{: #ts_login_error}

Non puoi eseguire un comando `bx cr` perché `cr` non è un comando `bx` registrato.

{: tsSymptoms}
Vedi un messaggio di errore simile a uno dei seguenti: 

```
bx cr login
'cr' non è un comando registrato. Vedi 'bx help'. 
```
{: pre}

```
bx cr namespace
'cr' non è un comando registrato. Vedi 'bx help'. 
```
{: pre}

{: tsCauses}
-   Il plug-in container-registry non è installato.


{: tsResolve}
Puoi correggere questo problema nel seguente modo:

-   Installa il plug-in container-registry; vedi [Installazione del plug-in CLI di {{site.data.keyword.registryshort_notm}} (bx cr)](registry_setup_cli_namespace.html#registry_cli_install).


## Configurazione di uno spazio dei nomi non riuscita
{: #ts_problem}

{: tsSymptoms}
Quando esegui `bx cr namespace-add`, non riesci a impostare il tuo valore immesso come spazio dei nomi.

{: tsCauses}
-   Hai immesso un valore per lo spazio dei nomi che è già utilizzato da un'altra organizzazione {{site.data.keyword.Bluemix_notm}}.
-   Recentemente è stato eliminato uno spazio dei nomi e stai riutilizzando il suo nome. Se lo spazio dei nomi che è stato eliminato
conteneva molte risorse, è possibile che {{site.data.keyword.registrylong_notm}} non abbia ancora elaborato completamente l'eliminazione.
-   Hai utilizzato caratteri non validi per il valore dello spazio dei nomi.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

-   Segui le istruzioni visualizzate nel messaggio di errore restituito.
-   Controlla di aver immesso uno spazio dei nomi valido:
    -   Il tuo spazio dei nomi deve avere una lunghezza compresa tra 4 e 30 caratteri.
    -   Il tuo spazio dei nomi deve iniziare con almeno una lettera o un numero.
    -   Il tuo spazio dei nomi deve contenere solo lettere minuscole, numeri o caratteri di sottolineatura (_).
-   Scegli un valore diverso per il tuo spazio dei nomi.
-   Se stai ricreando uno spazio dei nomi che era stato eliminato e che conteneva molte immagini, riprova più tardi.

## L'esecuzione del push o del pull di un'immagine Docker non riesce
{: #ts_pushpull}

{: tsSymptoms}
Quando esegui i comandi per il push o il pull delle immagini Docker, ricevi un messaggio di errore. Il
messaggio di errore varia a seconda della causa principale. I messaggi di errore potenziali potrebbero essere:

```
Hai superato la tua quota di archiviazione. Elimina una o più immagini o riesamina la tua quota di archiviazione e il piano prezzi
```
{: screen}

```
Hai superato la tua quota di traffico di pull per il mese corrente. Riesamina la tua quota di traffico di pull e il piano prezzi
```
{: screen}

```
non autorizzato: autenticazione richiesta
```
{: screen}

```
negato: l'accesso richiesto alla risorsa è stato negato
```
{: screen}

{: tsCauses}
-   Docker non è installato.
-   Il client Docker non è collegato a {{site.data.keyword.registrylong_notm}}.
-   Il tuo token di accesso {{site.data.keyword.Bluemix_notm}} potrebbe essere scaduto.
-   Hai superato il limite di quota per l'archiviazione o il traffico di pull impostato per il tuo account {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
Puoi risolvere questo problema nei seguenti modi:

-   [Assicurati che Docker sia installato sulla tua macchina](index.html#registry_cli_install).
-   Controlla il tuo percorso di installazione Docker.
-   Accedi a {{site.data.keyword.Bluemix_notm}} eseguendo
`bx login`. Quindi, accedi alla CLI di {{site.data.keyword.registrylong_notm}} eseguendo `bx cr
login`.
-   [Riesamina i limiti e l'utilizzo della quota per l'archiviazione e il pull delle immagini Docker in {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).

## Impossibile eseguire il pull dell'ultima immagine utilizzando la tag latest
{: #ts_docker_latest}

{: tsSymptoms}
Stai tentando di eseguire il comando `docker pull`, ma viene restituita una
versione della tua immagine che non è l'ultima versione creata.

{: tsCauses}
Per impostazione predefinita, la tag `latest` viene applicata per fare riferimento a un'immagine quando esegui i comandi Docker
senza specificare il valore della tag. La tag `latest` viene applicata all'ultimo comando
`docker build` o `docker tag` che è stato eseguito senza un valore di
tag esplicitamente impostato. Pertanto, è possibile eseguire i comandi `docker` in ordine non valido
oppure impostare esplicitamente le tag su alcune immagini e la tag `latest` per fare riferimento a una creazione
che non è la più recente.

{: tsResolve}
In genere, è meglio definire ogni volta una tag sequenziale diversa per le tue immagini in modo esplicito
anziché affidarsi alla tag `latest`.

## Accesso al registro con un firewall personalizzato non riuscito
{: #ts_firewall}

{: tsSymptoms}
Hai configurato un firewall aggiuntivo nel tuo ambiente di distribuzione con impostazioni personalizzate
per il traffico di rete in entrata e in uscita. Quando provi ad accedere a {{site.data.keyword.registrylong_notm}}, il collegamento ha esito negativo.

{: tsCauses}
Il tuo firewall personalizzato richiede che alcuni gruppi di rete siano aperti per il traffico di rete in entrata e in uscita
per consentire la comunicazione in entrata e uscita dal registro.

{: tsResolve}
Apri i seguenti gruppi di rete nel tuo firewall personalizzato.

1.  Prendi nota dell'indirizzo IP pubblico della macchina che desideri utilizzare per il collegamento a {{site.data.keyword.registrylong_notm}}. Se stai utilizzando Kubernetes,
utilizza l'indirizzo IP pubblico del tuo nodo di lavoro. Richiama l'indirizzo IP pubblico del tuo nodo di lavoro eseguendo `bx cs workers <cluster_name_or_id>`, dove *&lt;nome_o_id_cluster&gt;* è il nome o l'ID del tuo cluster.
2.  Nel tuo firewall, consenti i seguenti collegamenti in entrata e uscita dalla tua macchina:
    -   Per la connettività IN ENTRATA alla tua macchina, consenti il traffico di rete in entrata dai seguenti gruppi di rete di origine
all'indirizzo IP pubblico di destinazione della tua macchina.

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   Per la connettività IN USCITA dalla tua macchina, utilizza gli stessi gruppi di rete e consenti il traffico di rete in uscita
dall'indirizzo IP pubblico di origine della tua macchina a tali gruppi di rete.

