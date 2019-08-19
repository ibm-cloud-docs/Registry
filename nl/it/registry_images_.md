---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-06"

keywords: IBM Cloud Container Registry, Docker build command, delete images, add images, pull images, push images, copy images, delete private repositories,

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

# Aggiunta di immagini al tuo spazio dei nomi
{: #registry_images_}

Puoi memorizzare e condividere in modo sicuro le immagini Docker con altri utenti aggiungendo le immagini al tuo
spazio dei nomi in {{site.data.keyword.registrylong}}.
{:shortdesc}

Ogni immagine che vuoi aggiungere al tuo spazio dei nomi deve essere innanzitutto presente nel tuo computer locale. Puoi
scaricare (pull) un'immagine da un altro repository al tuo computer locale o puoi creare la tua propria
immagine da un Dockerfile utilizzando il comando `build` di Docker. Per aggiungere un'immagine al tuo
spazio dei nomi, devi caricare (push) l'immagine locale nel tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}.

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione o nei dati di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{: important}

## Esecuzione del pull di immagini da un altro registro
{: #registry_images_pulling_reg}

Puoi eseguire il pull (scaricare) di un'immagine da una qualsiasi origine di registro privato o pubblico e contrassegnarla con una tag
per un uso successivo in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

<img src="images/images_pull.svg" width="800" style="width:800px;" alt="Passa un'immagine da un registro pubblico o privato al tuo computer."/>

Prima di cominciare, completa le seguenti attività:

- [Installa la CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) per lavorare con le immagini nel tuo
spazio dei nomi.
- [Configura il tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Assicurati di poter eseguire i comandi Docker senza autorizzazioni root![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/install/linux/linux-postinstall/). Se
il tuo client Docker è configurato per richiedere le autorizzazioni root, devi eseguire i comandi `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` con `sudo`.

  Se modifichi le tue autorizzazioni per eseguire i comandi Docker senza i privilegi root, devi eseguire di nuovo il comando `ibmcloud login`.

1. Scarica l'immagine; consulta [Esegui il pull di un'immagine](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pulling) nella documentazione introduttiva.

   Se ricevi un messaggio del tipo `unauthorized: authentication required` o `denied: requested access to the resource is denied`, esegui il comando `ibmcloud cr login`.
   {:tip}

Dopo aver eseguito il pull di un'immagine e averla contrassegnata con una tag per il tuo spazio dei nomi, puoi caricare (push) l'immagine dal tuo computer locale al tuo spazio dei nomi.

## Esecuzione del push di immagini Docker al tuo spazio dei nomi
{: #registry_images_pushing_namespace}

Puoi eseguire il push (caricare) di un'immagine nel tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}} per memorizzare e condividere la tua immagine con altri utenti.
{:shortdesc}

<img src="images/images_push.svg" width="800" style="width:800px;" alt="Push di un'immagine dal tuo computer a {{site.data.keyword.registrylong_notm}}."/>

Prima di cominciare, completa le seguenti attività:

- [Installa la CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) per lavorare con le immagini nel tuo
spazio dei nomi.
- [Configura il tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Esegui il pull](#registry_images_pulling_reg) o [crea](#registry_images_creating) un'immagine sul tuo computer locale e contrassegna l'immagine tramite tag con le informazioni sul tuo spazio dei nomi.
- [Assicurati di poter eseguire i comandi Docker senza autorizzazioni root![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/install/linux/linux-postinstall/). Se
il tuo client Docker è configurato per richiedere le autorizzazioni root, devi eseguire i comandi `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` con `sudo`.

  Se modifichi le tue autorizzazioni per eseguire i comandi Docker senza i privilegi root, devi eseguire di nuovo il comando `ibmcloud login`.

Per caricare (push) un'immagine, completa le seguenti istruzioni:

1. Accedi alla CLI.

   ```
   ibmcloud cr login
   ```
   {: pre}

   Devi effettuare l'accesso se esegui il pull di un'immagine dal tuo {{site.data.keyword.registrylong_notm}} privato.
  {:tip}

2. Per visualizzare tutti gli spazi dei nomi disponibili nel tuo account, esegui il comando `ibmcloud cr namespace-list`.
3. [Carica l'immagine nel tuo spazio dei nomi.](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)

   Se ricevi un messaggio del tipo `unauthorized: authentication required` o `denied: requested access to the resource is denied`, esegui il comando `ibmcloud cr login`.
   {:tip}

Dopo aver eseguito il push della tua immagine a {{site.data.keyword.registrylong_notm}}, puoi effettuare una delle seguenti azioni:

- [Gestisci la sicurezza con il Controllo vulnerabilità](/docs/services/va?topic=va-va_index) per trovare informazioni su possibili vulnerabilità e problemi di sicurezza.
- [Creare un cluster
e utilizzare questa immagine per distribuire un contenitore](/docs/containers?topic=containers-getting-started#getting-started) al cluster in {{site.data.keyword.containerlong_notm}}.

## Copia di immagini tra i registri
{: #registry_images_copying}

Puoi eseguire il pull di un'immagine da un registro in una regione e trasmetterla a un registro in un'altra regione in modo da poter
condividere l'immagine in entrambe le regioni.
{:shortdesc}

<img src="images/images_copy.svg" width="800" style="width:800px;" alt="Copia un'immagine da un qualsiasi registro privato o pubblico nel tuo registro {{site.data.keyword.cloud_notm}} privato."/>

Prima di cominciare, completa le seguenti attività:

- [Installa la CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) per lavorare con le immagini nel tuo
spazio dei nomi.
- [Configura il tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Assicurati di poter eseguire i comandi Docker senza autorizzazioni root![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/install/linux/linux-postinstall/). Se
il tuo client Docker è configurato per richiedere le autorizzazioni root, devi eseguire i comandi `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` con `sudo`.

  Se modifichi le tue autorizzazioni per eseguire i comandi Docker senza i privilegi root, devi eseguire di nuovo il comando `ibmcloud login`.

Per copiare un'immagine tra due registri, completa le seguenti istruzioni:

1. [Esegui il pull di un'immagine da un registro](#registry_images_pulling_reg).
2. [Esegui il push dell'immagine a un altro
registro](#registry_images_pushing_namespace). Assicurati di utilizzare il nome del dominio corretto per la nuova regione di destinazione.

Dopo aver copiato la tua immagine, puoi effettuare una delle seguenti attività:

- [Gestire la sicurezza delle immagini con il Controllo vulnerabilità](/docs/services/va?topic=va-va_index) per trovare informazioni su potenziali vulnerabilità e problemi di sicurezza.
- [Creare un cluster
e utilizzare questa immagine per distribuire un contenitore](/docs/containers?topic=containers-getting-started#getting-started) al cluster in {{site.data.keyword.containerlong_notm}}.

## Creazione di nuove immagini che fanno riferimento a un'immagine di origine
{: #registry_images_source}

Nella regione in cui hai eseguito l'accesso, crea una nuova immagine in {{site.data.keyword.registrylong_notm}} che fa riferimento a un'immagine esistente nella stessa regione. Questa azione è supportata solo per le immagini di origine create utilizzando Docker Engine versione 1.12 o successive.

Le nuove immagini create utilizzando questo meccanismo non conservano le firme. Se hai bisogno che la nuova immagine sia firmata, non utilizzare questo meccanismo.
{: tip}

Prima di cominciare, completa le seguenti attività:

- [Installa la CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) per lavorare con le immagini nel tuo
spazio dei nomi.
- Assicurati di avere accesso a uno spazio dei nomi privato in {{site.data.keyword.registrylong_notm}} che contiene un'immagine di origine a cui vuoi che un'altra immagine faccia riferimento.

Per ulteriori informazioni sul comando, consulta [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag).

Per creare una nuova immagine da un'immagine di origine, completa la seguente procedura:

1. Accedi alla CLI.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Immetti il seguente comando per aggiungere un nuovo riferimento, dove `SOURCE_IMAGE` è il nome della tua immagine di origine e `TARGET_IMAGE` è il nome della tua immagine di destinazione. Le immagini di origine e di destinazione devono essere nella stessa regione. `SOURCE_IMAGE` e `TARGET_IMAGE` devono essere nel formato `<REPOSITORY>:<TAG>`, ad esempio: `us.icr.io/namespace/image:latest`

   ```
   ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
   ```
   {: pre}

3. Verifica che la nuova immagine sia stata creata immettendo il seguente comando e controlla che l'immagine venga mostrata nell'elenco con lo stesso digest immagine di quella di origine.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

## Creazione di immagini Docker da utilizzare con il tuo spazio dei nomi
{: #registry_images_creating}

Puoi creare un'immagine Docker direttamente in {{site.data.keyword.cloud_notm}} o creare la tua propria immagine Docker sul tuo computer locale e caricarla nel tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Prima di cominciare, completa le seguenti attività:

- [Installa la CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install) per lavorare con le immagini nel tuo
spazio dei nomi.
- [Configura il tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup).
- [Assicurati di poter eseguire i comandi Docker senza autorizzazioni root![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/install/linux/linux-postinstall/). Se
il tuo client Docker è configurato per richiedere le autorizzazioni root, devi eseguire i comandi `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` con `sudo`.

  Se modifichi le tue autorizzazioni per eseguire i comandi Docker senza i privilegi root, devi eseguire di nuovo il comando `ibmcloud login`.

Un'immagine Docker è la base per ogni contenitore che crei. Un'immagine viene creata da un
Dockerfile, che è un file che contiene le istruzioni su come creare l'immagine. Nelle sue istruzioni, un Dockerfile
potrebbe fare riferimento alle risorse di build che vengono memorizzate separatamente, quali ad esempio un'applicazione, la configurazione
dell'applicazione e le relative dipendenze.

Se vuoi usufruire delle risorse di calcolo di {{site.data.keyword.cloud_notm}} e la connessione Internet o Docker non è disponibile sulla tua workstation, crea la tua immagine direttamente in {{site.data.keyword.cloud_notm}}. Se hai bisogno di accedere alle risorse della tua build che si trovano su server dietro il tuo firewall, crea l'immagine localmente.

Per creare la tua immagine Docker, completa la seguente procedura:

1. Crea una directory locale in cui memorizzare il contesto di build. Il contesto di build contiene il tuo Dockerfile e le risorse di build correlate, come il codice dell'applicazione. Passa a questa directory in una finestra della riga di comando.
2. Crea un Dockerfile.
    1. Crea un Dockerfile nella tua directory locale.

        ```
        touch Dockerfile
        ```
        {: pre}

    2. Utilizza un editor di testo per aprire il Dockerfile. Come minimo, devi aggiungere l'immagine di base da cui creare la tua immagine. Sostituisci `<source_image>` e `<tag>` con il repository di immagini e la tag che vuoi utilizzare. Se stai utilizzando un'immagine proveniente da un altro registro privato, definisci il percorso completo all'immagine in {{site.data.keyword.registrylong_notm}}.

       ```
       FROM <source_image>:<tag>
       ```
       {: pre}

       Ad esempio, per creare un Dockerfile basato sull'immagine pubblica {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty (ibmliberty), utilizza il seguente comando:

       ```
       FROM <region>.icr.io/ibmliberty:latest
       LABEL description="This is my test Dockerfile"
       EXPOSE 9080
       ```
       {: pre}

       Questo esempio aggiunge un'etichetta ai metadati dell'immagine ed espone la porta 9080. Per ulteriori istruzioni sui Dockerfile che puoi utilizzare, vedi [Dockerfile Reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/engine/reference/builder/).

3. Scegli un nome per la tua immagine. Il nome immagine deve avere il seguente formato:

   ```
   <region>.icr.io/<my_namespace>/<repo_name>:<tag>
   ```
   {: pre}

   dove `<my_namespace>` indica le informazioni sul tuo spazio dei nomi, `<repo_name>` è il nome del tuo repository e `<tag>` è la versione che vuoi utilizzare per la tua immagine. Per trovare il tuo spazio dei nomi, esegui il comando `ibmcloud cr namespace-list`.

4. Prendi nota del percorso della directory che contiene il tuo Dockerfile. Se esegui i comandi indicati nella seguente procedura mentre la tua directory di lavoro è impostata sulla posizione in cui è memorizzato il contesto di build, puoi sostituire `<directory>` con un punto (.).
5. Scegli se creare la tua immagine direttamente in {{site.data.keyword.cloud_notm}} oppure se creare e testare la tua immagine in locale prima di eseguirne il push a {{site.data.keyword.cloud_notm}}.
   - Per creare l'immagine direttamente in {{site.data.keyword.cloud_notm}}, esegui questo comando:

     ```
     ibmcloud cr build -t <image_name> <directory>
     ```
     {: pre}

     dove `<image_name>` è il nome della tua immagine e `<directory>` è il percorso della directory. Se esegui il comando quando la tua directory di lavoro è impostata sulla posizione in cui è memorizzato il contesto di build, puoi sostituire `<directory>` con un punto (.).
  
     Per ulteriori informazioni sul comando `ibmcloud cr build`, vedi [CLI di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).

   - Per creare e testare la tua immagine in locale prima di eseguirne il push a {{site.data.keyword.cloud_notm}}, completa la seguente procedura:
      1. Crea l'immagine dal Dockerfile sul tuo computer locale e contrassegnala tramite tag con il tuo nome immagine.

         ```
         docker build -t <image_name> <directory>
         ```
         {: pre}

         dove `<image_name>` è il nome della tua immagine e `<directory>` è il percorso della directory.

      2. Facoltativo: testa la tua immagine nel tuo computer locale prima di eseguirne il push al tuo spazio dei nomi.

         ```
         docker run <image_name>
         ```
         {: pre}

         Sostituisci `<image_name>` con il nome della tua immagine.

      3. Dopo aver creato la tua immagine e averla contrassegnata con una tag per il tuo spazio dei nomi, [puoi eseguire il push della tua immagine al tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}](#registry_images_pushing_namespace).

Per utilizzare il Controllo vulnerabilità per verificare la sicurezza della tua immagine, vedi [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](/docs/services/va?topic=va-va_index).

## Push delle immagini a {{site.data.keyword.registrylong_notm}} utilizzando una chiave API
{: #registry_api_key_push_image}

Crea un ID servizio che utilizza una chiave API per eseguire il push dell'immagine a {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Completa la seguente procedura:

1. Crea un ID servizio, vedi [Creazione e gestione degli ID servizio](/docs/iam?topic=iam-serviceids#serviceids).
2. Crea una politica che fornisce l'autorizzazione all'ID servizio per accedere al registro, ad esempio, i ruoli `Administrator` e `Manager`, vedi [Gestione dell'accesso utente con Identity and Access Management (IAM)](/docs/services/Registry?topic=registry-iam#iam).
3. Crea una chiave API, consulta [Creazione di una chiave API per un ID servizio](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
4. Utilizza la chiave API per accedere al registro in modo da poter eseguire il push delle immagini al registro, vedi [Utilizzo di una chiave API per automatizzare l'accesso](/docs/services/Registry?topic=registry-registry_access#registry_api_key_use).
5. Esegui il push delle tue immagini, vedi [Esecuzione del push di immagini Docker al tuo spazio dei nomi](#registry_images_pushing_namespace).

Puoi ora utilizzare i cluster per eseguire il pull delle immagini, vedi [Creazione dei contenitori dalle immagini](/docs/containers?topic=containers-images#other_registry_accounts).

## Rimozione delle tag dalle immagini nel tuo repository {{site.data.keyword.cloud_notm}} privato
{: #registry_images_untag}

Puoi rimuovere una tag o delle tag da un'immagine e lasciare in vigore l'immagine sottostante e tutte le altre tag, utilizzando il comando [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag).
{:shortdesc}

Dove sono presenti più tag per lo stesso digest immagine all'interno di un repository, per rimuovere l'immagine sottostante e tutte le relative tag, vedi [Eliminazione di immagini dal tuo repository {{site.data.keyword.cloud_notm}} privato](#registry_images_remove).
{: tip}

Per rimuovere una tag o delle tag utilizzando la CLI, completa la seguente procedura:

1. Effettua l'accesso a {{site.data.keyword.cloud_notm}} eseguendo il comando `ibmcloud login`.
2. Per rimuovere una tag, esegui questo comando:

   ```
   ibmcloud cr image-untag IMAGE
   ```
   {: pre}

   Dove `IMMAGINE` è il nome dell'immagine che vuoi rimuovere, nel formato `repository:tag`.

   Se nel nome immagine non è specificata alcuna tag, il comando ha esito negativo. Puoi eliminare le tag per più immagini elencando ogni percorso del registro {{site.data.keyword.cloud_notm}} privato nel comando con uno spazio tra ogni percorso.

   Per trovare i nomi delle tue immagini, esegui `ibmcloud cr image-list`. Combina il contenuto delle colonne **Repository** e **Tag** per creare il nome dell'immagine nel formato `repository:tag`.
   {:tip}

3. Verifica che la tag sia stata rimossa immettendo il seguente comando e controlla che l'immagine non sia visualizzata nell'elenco.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

## Eliminazione di immagini dal tuo repository {{site.data.keyword.cloud_notm}} privato
{: #registry_images_remove}

Puoi eliminare le immagini non desiderate dal tuo repository privato utilizzando la GUI (graphical user interface) o la CLI.
{:shortdesc}

Se vuoi eliminare un repository privato e le relative immagini associate, consulta [Eliminazione di un repository privato e delle eventuali immagini associate](#registry_repo_remove).

Le immagini {{site.data.keyword.IBM_notm}} pubbliche non possono essere eliminate dal tuo repository {{site.data.keyword.cloud_notm}} privato e non vengono conteggiate nella tua quota.

L'eliminazione di un'immagine non può essere annullata. L'eliminazione di un'immagine utilizzata da una distribuzione esistente potrebbe causare la mancata riuscita di un ridimensionamento, di una ripianificazione o di entrambe le operazioni.
{: important}

Dove sono presenti più tag per lo stesso digest immagine all'interno di un repository, il [comando `ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) rimuove l'immagine sottostante e tutte le relative tag. Se la stessa immagine è presente in uno spazio dei nomi o repository diversi, tale copia dell'immagine non viene rimossa. Se vuoi rimuovere una tag da un'immagine e lasciare in vigore l'immagine sottostante e tutte le altre tag, vedi il comando [Rimozione delle tag dalle immagini nel tuo repository {{site.data.keyword.cloud_notm}} privato](#registry_images_untag).
{: tip}

### Eliminazione di immagini dal tuo repository {{site.data.keyword.cloud_notm}} privato utilizzando la CLI
{: #registry_images_remove_cli}

Puoi eliminare le immagini e tutte le relative tag indesiderate dal tuo repository privato utilizzando la CLI.
{:shortdesc}

L'eliminazione di un'immagine non può essere annullata. L'eliminazione di un'immagine utilizzata da una distribuzione esistente potrebbe causare la mancata riuscita di un ridimensionamento, di una ripianificazione o di entrambe le operazioni.
{: important}

Per eliminare un'immagine utilizzando la CLI, completa la seguente procedura:

1. Effettua l'accesso a {{site.data.keyword.cloud_notm}} eseguendo il comando `ibmcloud login`.
2. Per eliminare un'immagine, esegui questo comando:

   ```
   ibmcloud cr image-rm IMMAGINE
   ```
   {: pre}

   Dove `IMMAGINE` è il nome dell'immagine che vuoi rimuovere, nel formato `repository:tag`.

   Se nel nome dell'immagine non è specificata alcuna tag, per impostazione predefinita verrà eliminata l'immagine con tag `latest`. Puoi eliminare più immagini elencando ogni percorso del registro {{site.data.keyword.cloud_notm}} privato nel comando con uno spazio tra ogni percorso.

   Per trovare i nomi delle tue immagini, esegui `ibmcloud cr image-list`. Combina il contenuto delle colonne **Repository** e **Tag** per creare il nome dell'immagine nel formato `repository:tag`.
   {:tip}

3. Verifica che l'immagine sia stata eliminata immettendo il seguente comando e controlla che l'immagine non sia visualizzata nell'elenco.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

### Eliminazione di immagini dal tuo repository {{site.data.keyword.cloud_notm}} privato utilizzando la GUI
{: #registry_images_remove_gui}

Puoi eliminare le immagini e tutte le relative tag indesiderate dal tuo repository di immagini privato utilizzando la GUI (graphical user interface).
{:shortdesc}

L'eliminazione di un'immagine non può essere annullata. L'eliminazione di un'immagine utilizzata da una distribuzione esistente potrebbe causare la mancata riuscita di un ridimensionamento, di una ripianificazione o di entrambe le operazioni.
{: important}

Per eliminare un'immagine utilizzando la GUI, completa la seguente procedura:

1. Accedi alla console {{site.data.keyword.cloud_notm}} ([https://cloud.ibm.com/login ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login)) con il tuo ID IBM.
2. Se hai più account {{site.data.keyword.cloud_notm}}, seleziona l'account e la regione che desideri utilizzare dal menu dell'account.
3. Fai clic su **Catalogo**.
4. Seleziona la categoria **Contenitori** e fai clic sul tile **Registro contenitore**.
5. Fai clic su **Immagini**. Viene visualizzato un elenco delle tue immagini.
6. Nella riga che contiene l'immagine che vuoi eliminare, seleziona la casella di spunta.

   Assicurati di aver selezionato l'immagine corretta perché questa azione non può essere annullata.
   {: important}

7. Fai clic su **Elimina immagine**.

## Eliminazione di un repository privato e delle eventuali immagini associate
{: #registry_repo_remove}

Puoi eliminare i repository privati che non sono più necessari, e le eventuali immagini associate, utilizzando la GUI (graphical user interface).
{:shortdesc}

Quando elimini un repository, tutte le immagini in tale repository vengono eliminate. Questa azione non può essere annullata.
{: important}

Prima di cominciare, devi eseguire il backup di tutte immagini che vuoi conservare.
{: tip}

Per eliminare un repository privato utilizzando la GUI, completa la seguente procedura:

1. Accedi alla console {{site.data.keyword.cloud_notm}} ([https://cloud.ibm.com/login ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login)) con il tuo ID IBM.
2. Se hai più account {{site.data.keyword.cloud_notm}}, seleziona l'account e la regione che desideri utilizzare dal menu dell'account.
3. Fai clic su **Catalogo**.
4. Seleziona la categoria **Contenitori** e fai clic sul tile **Registro contenitore**.
5. Fai clic su **Repository**. Viene visualizzato un elenco dei tuoi repository privati.
6. Nella riga che contiene il repository privato che vuoi eliminare, seleziona la casella di spunta.

    Assicurati di aver selezionato il repository corretto perché questa azione non può essere annullata.
    {: important}

7. Fai clic su **Elimina repository**.
