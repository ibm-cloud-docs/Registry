---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: IBM Cloud Container Registry, Docker Content Trust, keys, trusted content, signing, signing images, repository keys, 

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

# Firma di immagini per contenuti attendibili
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} fornisce una tecnologia di contenuti attendibili che ti permette di firmare le immagini per garantirne l'integrità nel tuo spazio dei nomi del registro. Mediante l'esecuzione del pull e del push delle immagini firmate, puoi verificare che le tue immagini siano state trasmesse dalla parte giusta, come i tuoi strumenti di integrazione continua (CI). Per utilizzare questa funzione, devi avere Docker versione 18.03 o successive. Per ulteriori informazioni, consulta la documentazione di [Docker Content Trust ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/engine/security/trust/content_trust/) e del [progetto Notary ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/theupdateframework/notary).
{:shortdesc}

Quando esegui il push della tua immagine con i contenuti attendibili abilitati, il tuo client Docker esegue anche il push di un oggetto di metadati firmato nel server di attendibilità {{site.data.keyword.Bluemix_notm}}. Quando esegui il pull di un'immagine con tag con il Docker Content Trust abilitato, il tuo client Docker contatta il server di attendibilità per stabilire l'ultima versione firmata della tag che hai richiesto, verifica la firma del contenuto e scarica l'immagine firmata.

Un nome immagine è costituito da un repository e una tag. Quando utilizzi contenuto attendibile, ciascun repository utilizza una chiave di firma univoca. Ogni tag all'interno di un repository utilizza la chiave che appartiene al repository. Se ci sono più team che pubblicano dei contenuti, ciascuno nel proprio repository all'interno dei tuoi spazi dei nomi di {{site.data.keyword.registrylong_notm}}, ogni team può utilizzare le proprie chiavi per firmare i propri contenuti, in modo che tu possa verificare che ogni immagine sia prodotta dal team appropriato.

Un repository può contenere sia contenuti firmati che non firmati. Se hai abilitato Docker Content Trust, puoi accedere ai contenuti firmati in un repository, anche se ci sono altri contenuti non firmati al suo interno.

Le immagini hanno firme separate per il vecchio nome del dominio (`registry.bluemix.net`) e quello nuovo (`icr.io`). Le firme esistenti funzionano quando viene eseguito il pull dell'immagine dal vecchio nome del dominio. Se vuoi eseguire il pull del contenuto firmato dal nuovo nome del dominio, devi rifirmare l'immagine sul nuovo nome del dominio, `icr.io`, consulta [Rifirmare un'immagine per il nuovo nome del dominio](#trustedcontent_resign).
{: note}

Docker Content Trust usa un modello di sicurezza di "attendibilità al primo utilizzo". La chiave di repository viene estratta dal server di attendibilità quando esegui per la prima volta il pull di un'immagine firmata da un repository e tale chiave viene utilizzata per verificare le immagini da quel repository in futuro. Devi verificare di considerare attendibile il server di attendibilità o l'immagine e il relativo editore prima di eseguire il pull dal repository per la prima volta. Se le informazioni sull'attendibilità nel server sono compromesse e non hai ancora eseguito il pull di un'immagine dal repository, il client Docker potrebbe estrarre le informazioni compromesse dal server di attendibilità. Se i dati di attendibilità vengono compromessi dopo che hai eseguito il pull dell'immagine per la prima volta, durante i pull successivi, il client Docker non riesce a verificare i dati compromessi e non esegue il pull dell'immagine. Per ulteriori informazioni su come controllare i dati di attendibilità per un'immagine, vedi [Visualizzazione delle immagini firmate](#trustedcontent_viewsigned).

Per ulteriori informazioni sul modello di sicurezza di "attendibilità al primo utilizzo" vedi [The Update Framework (TUF) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://theupdateframework.github.io/).

## Configurazione del tuo ambiente di contenuti attendibili
{: #trustedcontent_setup}

Per impostazione predefinita, Docker Content Trust è disabilitato. Abilita l'ambiente Content Trust prima di accedere a {{site.data.keyword.registrylong_notm}} e di lavorare con le immagini firmate.
{:shortdesc}

1. Abilita la variabile di ambiente Docker Content Trust nel tuo terminale.

   Per Linux o Mac:

   ```
   export DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

   Per Windows:

   ```
   set DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

2. Accedi alla CLI di {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login [--sso]
   ```
   {: pre}

   Se hai un ID federato, utilizza `ibmcloud login --sso` per eseguire l'accesso. Immetti il tuo nome utente e usa
l'URL fornito nell'output della CLI per richiamare la tua passcode monouso. Sai di avere un ID federato se l'accesso non riesce senza `--sso` e riesce con l'opzione `--sso`.
   {: tip}

3. Specifica la regione che vuoi utilizzare come destinazione. Se non conosci il nome della regione, puoi eseguire il comando senza la regione e sceglierne una.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

4. Accedi a {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

   L'output ti indica di esportare la variabile di ambiente Docker Content Trust.

   **Esempio**

   ```
   user:~ user$ ibmcloud cr login
   Logging in to 'us.icr.io'...
   Logged in to 'us.icr.io'.

   To set up your Docker client with content trust,
   export the following environment variable:
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: screen}

5. Copia e incolla il comando della variabile di ambiente nel tuo terminale. Ad esempio:

   ```
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: pre}

Ora sei pronto per il push, il pull e la gestione delle immagini firmate attendibili.

Durante la tua sessione con Docker Content Trust abilitato, se vuoi eseguire un'operazione con i contenuti attendibili disabilitati (ad esempio, per eseguire il pull di un'immagine non firmata), utilizza l'indicatore `--disable-content-trust` con il comando.
{: tip}

## Esecuzione del push di un'immagine firmata
{: #trustedcontent_push}

Quando esegui per la prima volta il push di un'immagine firmata, Docker crea automaticamente una coppia di chiavi di firma: root e repository. Per firmare un'immagine in un repository in cui sono state già inserite immagini firmate, è necessario che la chiave di firma del repository corretta sia caricata sulla macchina che esegue il push dell'immagine.
{:shortdesc}

Prima di iniziare, [configura il tuo spazio dei nomi del registro](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add).

1. [Configura il tuo ambiente di contenuti attendibili](#trustedcontent_setup).

2. [Esegui il push della tua immagine](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing). La tag è obbligatoria per il contenuto attendibile. Nell'output del comando vedi:

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

3. **Esecuzione del push di un repository firmato per la prima volta.** Quando esegui il push di un'immagine firmata in un nuovo repository, il comando crea due chiavi di firma, chiave root e chiave di repository, e le memorizza nella tua macchina locale. Immetti e salva passphrase sicure per ogni chiave, quindi [esegui il backup delle tue chiavi](#trustedcontent_backupkeys). Il backup delle tue chiavi è fondamentale perché le [opzioni di ripristino](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent) sono limitate.

## Esecuzione del pull di un'immagine firmata
{: #trustedcontent_pull}

La prima volta che esegui il pull di un'immagine firmata con Docker Content Trust abilitato, il tuo client Docker riconosce la firma come attendibile. Il client Docker esegue il pull dell'ultima versione firmata dell'immagine che hai specificato. Non viene eseguito il pull di immagini non firmate o di contenuti non attendibili.
{:shortdesc}

1. [Configura il tuo ambiente di contenuti attendibili](#trustedcontent_setup).

2. Esegui il pull della tua immagine. Sostituisci `<source_image>` con il repository dell'immagine e `<tag>` con la tag dell'immagine che vuoi utilizzare, come ad esempio _latest_. Per elencare le immagini disponibili per il pull, esegui `ibmcloud cr image-list`.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    Specifica la tag quando esegui il push o il pull di un'immagine firmata. La tag `latest` assume il valore predefinito solo quando l'attendibilità dei contenuti è disabilitata.
    {: tip}

## Rifirmare un'immagine per il nuovo nome del dominio
{: #trustedcontent_resign}

Per rifirmare l'immagine per il nuovo nome del dominio, `icr.io`, devi eseguire il pull, contrassegnare ed eseguire il push dell'immagine.
{:shortdesc}

1. Esegui il pull della tua immagine firmata dal vecchio nome del dominio. Sostituisci `<source_image>` con il repository dell'immagine e `<tag>` con la tag dell'immagine che vuoi utilizzare, come ad esempio _latest_. Per elencare le immagini disponibili per il pull, esegui `ibmcloud cr image-list`.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    Specifica la tag quando esegui il push o il pull di un'immagine firmata. La tag `latest` assume il valore predefinito solo quando l'attendibilità dei contenuti è disabilitata.
    {: tip}

2. Esegui il comando `docker tag` per il nuovo nome del dominio. Sostituisci `<old_domain_name>` con il tuo vecchio nome del dominio, `<new_domain_name>` con il tuo nuovo nome del dominio, `<repository>` con il nome del tuo repository e `<tag>` con il nome della tua tag.

   ```
   docker tag <old_domain_name>/<repository>:<tag> <new_domain_name>/<repository>:t<tag>
   ```
   {: pre}

3. Esegui il push della tua immagine utilizzando il nuovo nome del dominio, consulta [Esegui il push delle immagini Docker nel tuo spazio dei nomi](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing). La tag è obbligatoria per il contenuto attendibile. Nell'output del comando vedi:

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

## Gestione dei contenuti attendibili
{: #trustedcontent_managetrust}

Utilizzando i comandi `docker trust`, puoi vedere chi ha firmato le immagini e revocare lo stato di contenuti attendibili. Per eseguire i comandi `docker trust`, hai bisogno di Docker 18.03 o superiore.
{:shortdesc}

### Visualizzazione delle immagini firmate
{: #trustedcontent_viewsigned}

Puoi esaminare le versioni firmate di un repository o una tag di immagini, incluse le informazioni sull'ID chiave e sul firmatario.
{:shortdesc}

1. [Configura il tuo ambiente di contenuti attendibili](#trustedcontent_setup).

2. Esamina le informazioni su tag, digest e firmatario per ciascuna immagine.

   (Facoltativo) Specifica la tag, `<tag>`, per vedere le informazioni su quella versione dell'immagine.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### Revoca dell'attendibilità
{: #trustedcontent_revoketrust}

Puoi revocare lo stato di contenuti attendibili di un'immagine.
{:shortdesc}

Prima di iniziare, richiama la passphrase della chiave di repository che hai salvato quando hai [eseguito per la prima volta il push del repository attendibile](#trustedcontent_push). Se devi identificare quale chiave viene utilizzata per l'immagine attendibile, utilizza il [comando](#trustedcontent_viewsigned) `docker view`.

1. [Configura il tuo ambiente di contenuti attendibili](#trustedcontent_setup).

2. Rimuovi tutti i metadati attendibili per il repository di immagini. Immetti la passphrase della chiave di repository quando richiesto.

   (Facoltativo) Specifica una tag per revocare i metadati attendibili solo per quella versione dell'immagine.

   ```
   docker trust revoke <image>:<tag>
   ```
   {: pre}

3. Verifica che l'attendibilità sia stata revocata nell'elenco di contenuti attendibili.

   (Facoltativo) Se vuoi verificare il contenuto revocato per un'immagine contrassegnata con una tag, includi la tag.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   Output dal precedente comando:

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## Backup delle chiavi di firma
{: #trustedcontent_backupkeys}

Quando esegui per la prima volta il push di un'immagine firmata in un nuovo repository, Docker Content Trust crea due chiavi di firma, la chiave root e la chiave di repository, e le memorizza nella tua macchina locale:

- Directory Linux e Mac: `~/.docker/trust/private`

- Directory Windows: `%HOMEPATH%\.docker\trust\private`

   Se hai modificato la tua directory di configurazione Docker, cerca lì la sottodirectory `trust`.
   {: tip}

Devi eseguire il backup di tutte le chiavi, in particolare della chiave root. Se una chiave viene persa o compromessa, le tue [opzioni di ripristino](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent) sono limitate.

Per eseguire il backup delle tue chiavi, consulta la [documentazione Docker Content Trust ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys).

## Gestione dei firmatari attendibili
{: #trustedcontent_signers}

Puoi aggiungere e rimuovere firmatari dalla firma di immagini in un repository.
{:shortdesc}

### Aggiunta di firmatari a un repository attendibile
{: #trustedcontent_addsigners}

Per consentire ad altri utenti di firmare le immagini in un repository, aggiungi le chiavi di firma per quegli utenti al repository.
{:shortdesc}

**Prima di iniziare**

- I firmatari di immagini devono disporre dell'autorizzazione per eseguire il push delle immagini nello spazio dei nomi.
- I proprietari del repository e i firmatari aggiuntivi devono avere installato Docker 18.03 o successive.
- Crea un repository di contenuti attendibili [eseguendo il push di un'immagine firmata](#trustedcontent_push). I proprietari del repository devono disporre delle chiavi di amministratore del repository disponibili nella cartella di attendibilità Docker sulla propria macchina locale. Se non disponi della chiave di amministratore del repository, contatta il proprietario affinché esegua questa attività.

Quando aggiungi un firmatario, non puoi più utilizzare la chiave di amministratore del repository per firmare le immagini in tale repository. Devi mantenere la chiave privata affinché uno dei firmatari approvati possa firmare. Per conservare la possibilità di firmare le immagini dopo aver aggiunto un firmatario, segui di nuovo queste istruzioni per generare e aggiungere un ruolo di firmatario per te stesso.
{:tip}

Per condividere le chiavi di firma:

1. Se il nuovo firmatario non ha ancora generato una coppia di chiavi, è necessario generare e caricare una coppia di chiavi.
  
    a. Genera la chiave. Puoi immettere qualsiasi nome per `<NAME>`, tuttavia, il nome da te selezionato è visibile quando qualcuno ispeziona l'attendibilità sul repository. . Collabora con il proprietario del repository per soddisfare eventuali convenzioni di denominazione che potrebbero essere utilizzate dall'organizzazione e per selezionare un nome che sia identificabile per tale firmatario.

      ```
      docker trust key generate <NOME>
      ```
      {: pre}
  
    b. Immetti una passphrase per la chiave privata. Viene generata una chiave pubblica (`.pub`) e la chiave privata corrispondente viene caricata automaticamente nella configurazione di attendibilità Docker.
  
    c. Il nuovo firmatario deve inviare la chiave pubblica al proprietario del repository.

2. Il proprietario del repository deve aggiungere la chiave del firmatario al repository.

    a. [Configura l'ambiente di contenuti attendibili](#trustedcontent_setup).

    b. Aggiungi la chiave del firmatario al repository.

      ```
      docker trust signer add --key <NOME>.pub <NOME> <repository>
      ```
      {: pre}

3. Il firmatario può configurare il proprio ambiente e firmare un'immagine.

    a. [Configura l'ambiente di contenuti attendibili](#trustedcontent_setup).

    b. Il firmatario deve firmare un'immagine. Quando richiesto, immetti la passphrase per la chiave privata.

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4. Per verificare che il firmatario sia stato aggiunto, vedi [Visualizzazione delle immagini firmate](#trustedcontent_viewsigned).

### Rimozione di un firmatario da un repository
{: #trustedcontent_removesigner}

Se non vuoi più che un firmatario sia in grado di firmare le immagini nel tuo repository, puoi rimuoverlo come firmatario.
{:shortdesc}

Prima di iniziare, i proprietari del repository e i firmatari aggiuntivi devono avere installato Docker 18.03 o successive.

Se rimuovi un firmatario, il server di attendibilità non ritiene attendibili le sue versioni firmate dell'immagine. Per garantire di poter eseguire il pull dell'immagine dopo la rimozione del firmatario, assicurati che il firmatario non abbia firmato la versione più recente dell'immagine. Se il firmatario ha firmato la versione più recente dell'immagine, invia un aggiornamento all'immagine e firmala utilizzando la tua chiave prima di continuare.
{:tip}

Per rimuovere un firmatario:

1. [Configura il tuo ambiente di contenuti attendibili](#trustedcontent_setup).

2. Rimuovi il firmatario.

   ```
   docker trust signer remove <NOME> <repository>
   ```
   {: pre}

3. Per verificare che il firmatario sia stato rimosso, visualizza i dati di attendibilità per l'immagine e verifica che il firmatario non sia più elencato. Per ulteriori informazioni sulla visualizzazione dei dati di attendibilità, vedi [Visualizzazione delle immagini firmate](#trustedcontent_viewsigned).
