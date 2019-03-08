---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-27"

keywords: IBM Cloud Container Registry, private Docker images, scalable private image registry, regions, plans, billing, registry

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

# Informazioni su {{site.data.keyword.registrylong_notm}}
{: #registry_overview}

Utilizza {{site.data.keyword.registrylong}} per memorizzare e accedere alle immagini Docker private in un'architettura scalabile e altamente disponibile.
{:shortdesc}

{{site.data.keyword.registrylong_notm}} fornisce un registro delle immagini privato a più tenant, altamente disponibile e scalabile che viene ospitato e gestito da {{site.data.keyword.IBM_notm}}. Puoi utilizzare {{site.data.keyword.registrylong_notm}} configurando il tuo spazio dei nomi di immagini ed eseguendo il push delle immagini Docker al tuo spazio dei nomi.

<img src="images/registry_architecture1.svg" alt="Immagine che mostra come puoi interagire con IBM Cloud Container Registry. Container Registry contiene sia il repository pubblico che privato che le API per interagire con il servizio. Il tuo client Docker locale può ricevere e trasmettere le immagini dai tuoi repository privati al registro e può eseguire il pull dei repository privati. L'IU web (console) di IBM Cloud interagisce con l'API Container Registry per elencare le immagini. La CLI Container Registry interagisce con l' API per elencare, creare, ispezionare e rimuovere le immagini, così come per altre funzioni di gestione. Il tuo client Docker locale può anche ricevere e trasmettere le immagini dal tuo archivio delle immagini locale ad altri registri."/>

**Figura 1. Come {{site.data.keyword.registrylong_notm}} interagisce con le tue immagini Docker**

Un'immagine Docker è la base per ogni contenitore che crei. Un'immagine viene creata da un
Dockerfile, che è un file che contiene le istruzioni su come creare l'immagine. Nelle sue istruzioni, un Dockerfile
potrebbe fare riferimento alle risorse di build che vengono memorizzate separatamente, quali ad esempio un'applicazione, la configurazione
dell'applicazione e le relative dipendenze. Le immagini sono generalmente memorizzate in un registro che può essere accessibile al pubblico (registro
pubblico) o configurato con un accesso limitato per un piccolo gruppo di utenti (registro privato). Utilizzando {{site.data.keyword.registrylong_notm}}, solo gli utenti che dispongono dell'accesso al tuo account {{site.data.keyword.Bluemix_notm}} possono accedere alle tue immagini.

Quando esegui il push delle immagini a {{site.data.keyword.registrylong_notm}}, usufruisci delle funzioni integrate del Controllo vulnerabilità
che esegue la scansione per ricercare potenziali problemi di sicurezza e vulnerabilità. Il Controllo vulnerabilità
cerca i pacchetti vulnerabili in specifiche immagini di base Docker e le vulnerabilità note nelle impostazioni di configurazione
dell'applicazione. Se vengono trovate delle vulnerabilità, vengono fornite le informazioni
relative. Puoi utilizzare queste informazioni per risolvere i problemi di sicurezza in modo che i contenitori non vengano distribuiti da immagini vulnerabili.

Esamina la seguente tabella per una panoramica dei vantaggi dell'utilizzo di {{site.data.keyword.registrylong_notm}}.

|Vantaggio|Descrizione|
|-------|-----------|
|Registro privato altamente disponibile e scalabile|<ul><li>Configura il tuo spazio dei nomi di immagini in un registro privato a più tenant, altamente disponibile e scalabile che viene ospitato e gestito da {{site.data.keyword.IBM_notm}}.</li><li>Memorizza le tue immagini Docker private e condividile con gli utenti nel tuo account {{site.data.keyword.Bluemix_notm}}.</li></ul>|
|Conformità della sicurezza dell'immagine con il Controllo vulnerabilità|<ul><li>Vantaggio della scansione automatica delle immagini nel tuo spazio dei nomi.</li><li>Riesamina i suggerimenti specifici del sistema operativo per risolvere le vulnerabilità potenziali ed
evitare che i tuoi contenitori vengano compromessi.</li></ul>|
|Limiti di quota per l'archiviazione e il traffico di pull|<ul><li>Vantaggio dell'archiviazione e del traffico di pull gratuiti per le tue immagini private fino al raggiungimento
della tua quota gratuita.</li><li>Imposta limiti di quota personalizzati per la quantità mensile di archiviazione e di traffico di pull per evitare di superare
il tuo livello di pagamento preferito.</li></ul>|
{: caption="Tabella 1. Vantaggi di {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Piani di servizio
{: #registry_plans}

Puoi scegliere tra i piani di servizio {{site.data.keyword.registrylong_notm}} gratuito e standard per memorizzare le tue immagini Docker
e renderle disponibili agli utenti nel tuo account {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Il piano di servizio {{site.data.keyword.registrylong_notm}} determina
la quantità di archiviazione e di traffico di pull che puoi utilizzare per le tue immagini private. Il piano di servizio è
associato al tuo account {{site.data.keyword.Bluemix_notm}}
e limita l'archiviazione e il traffico di pull da applicare a tutti gli spazi dei nomi che hai configurato nel tuo
account.

La seguente tabella mostra i piani di servizio {{site.data.keyword.registrylong_notm}} disponibili e le relative caratteristiche. Per ulteriori informazioni su come funziona la fatturazione e su cosa succede se superi i limiti del piano di servizio, vedi [Limiti di quota e fatturazione in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).

|Caratteristiche|Gratuito|Standard|
|---------------|----|--------|
|Descrizione|Prova {{site.data.keyword.registrylong_notm}} per memorizzare e condividere le tue immagini Docker. Questo è il piano di servizio predefinito quando configuri il tuo primo spazio dei nomi in {{site.data.keyword.registrylong_notm}}.|Beneficia di un utilizzo illimitato di archiviazione e di traffico di pull per gestire le immagini Docker per tutti gli spazi
dei nomi nel tuo account
{{site.data.keyword.Bluemix_notm}}.|
|Quantità di archiviazione per le immagini|500 MB|Senza limiti|
|Traffico di pull|5 GB al mese|Senza limiti|
|Fatturazione|Se superi i tuoi limiti di archiviazione e traffico di pull, non puoi eseguire il push o il pull delle immagini
da e verso il tuo spazio dei nomi. Per ulteriori informazioni, vedi [Limiti di quota e fatturazione in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).|<ul><li>Archiviazione: il tuo addebito si basa sui Gigabyte di utilizzo al mese. I primi 0,5 GB al mese sono gratuiti. Quindi,
ti verrà addebitato secondo quanto indicato nel calcolatore prezzi.</li><li>Traffico di pull: il tuo addebito si basa sui Gigabyte di utilizzo al mese. I primi 5 GB sono gratuiti. Quindi, ti verrà addebitato secondo quanto indicato nel calcolatore prezzi. Se superi i tuoi limiti di archiviazione e traffico di pull, non puoi eseguire il push o il pull delle immagini
da e verso il tuo spazio dei nomi. Per ulteriori informazioni su archiviazione, traffico di pull e calcolatore prezzi, vedi [Limiti di quota e fatturazione in {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).</li></ul>|
{: caption="Tabella 2. Piani {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Limiti di quota e fatturazione
{: #registry_plan_billing}

Trova informazioni ed esempi sul funzionamento del processo di fatturazione e dei limiti di quota in
{{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Ogni immagine viene creata a partire da un certo numero di livelli che rappresentano ciascuno un cambiamento incrementale dall'immagine di base. Quando esegui il push o il pull di un'immagine, la quantità di archiviazione e di traffico di pull necessaria per ogni livello viene aggiunta al tuo utilizzo mensile. I livelli identici vengono condivisi automaticamente tra le immagini nel tuo account
{{site.data.keyword.Bluemix_notm}} e vengono riutilizzati quando crei altre immagini. L'archiviazione per ogni livello identico viene addebitata solo una volta, a prescindere dal numero di immagini nel tuo account che si riferiscono al livello.

Esempio per il push di immagini:

> Esegui il push di un'immagine al tuo spazio dei nomi che si basa sull'immagine Ubuntu. L'immagine Ubuntu contiene diversi livelli. Poiché nel tuo account non hai ancora questi livelli, la quantità di archiviazione richiesta dai livelli viene aggiunta al tuo utilizzo mensile.
>
> Successivamente, crea una seconda immagine basata sull'immagine Ubuntu. Modifica l'immagine di base Ubuntu, ad esempio aggiungendo ulteriori comandi o file al tuo Dockerfile. Ogni modifica rappresenta un nuovo livello dell'immagine. Quando esegui il push della seconda immagine, {{site.data.keyword.registrylong_notm}} riconosce che tutti i livelli dell'immagine Ubuntu di base sono già memorizzati nel tuo account. La seconda volta che memorizzi questi livelli non ti viene addebitato nulla, anche se hai eseguito il push della tua immagine in un altro spazio dei nomi. {{site.data.keyword.registrylong_notm}} determina la dimensione di tutti i nuovi livelli e aggiunge la quantità di archiviazione al tuo utilizzo mensile.

### Fatturazione per l'archiviazione e il traffico di pull
{: #registry_billing_traffic}

A seconda del piano di servizio scelto, gli addebiti a tuo carico sono basati sull'archiviazione e sul traffico di
pull che utilizzi al mese.
{:shortdesc}

**Archiviazione: **

  Ogni piano di servizio {{site.data.keyword.registrylong_notm}} viene fornito con una certa quantità di archiviazione che puoi utilizzare per memorizzare le tue immagini Docker negli spazi dei nomi del tuo account {{site.data.keyword.Bluemix_notm}}. Se utilizzi il piano standard, il tuo addebito si basa sui GB al mese di utilizzo. I primi 0,5 GB al mese sono gratuiti. Se utilizzi il piano gratuito, puoi memorizzare gratuitamente le tue immagini in {{site.data.keyword.registrylong_notm}} finché non raggiungi i limiti di quota per tale piano. Un GB al mese è una media di 1 GB di archiviazione al mese (730 ore).

  Esempio per il piano standard:

  > Utilizzi 5 GB per esattamente mezzo mese e quindi trasmetti diverse immagini al tuo spazio dei nomi e utilizzi 10 GB per il resto del mese. Il tuo utilizzo mensile viene calcolato come segue:
  >
  > (5 GB x 0.5 (mesi)) + (10 GB x 0.5 (mesi)) = 2,5 + 5 = 7,5 GB al mese
  >
  > Nel piano standard, i primi 0,5 GB al mese sono gratuiti, pertanto ti vengono addebitati 7 GB al mese (7,5 GB al mese - 0,5 GB al mese).

  

**Traffico di pull: **

  Ogni piano di servizio {{site.data.keyword.registrylong_notm}} include una certa quantità di traffico di pull gratuito per le tue immagini private memorizzate nel tuo spazio dei nomi. Il traffico di pull è la larghezza di banda che utilizzi quando esegui il pull di un livello di un'immagine dal tuo spazio dei nomi alla tua macchina locale. Se utilizzi il piano standard, il tuo addebito si basa sui GB di utilizzo al mese. I primi 5 GB al mese sono gratuiti. Se utilizzi il piano gratuito, puoi eseguire il pull di immagini dal tuo spazio dei nomi finché non raggiungi il limite di quota previsto per tale piano.

  Esempio per il piano standard:

  > Nel mese, hai eseguito il pull di immagini che contengono dei livelli con una dimensione totale di 14 GB. Il tuo utilizzo mensile viene calcolato come segue:
  >
  > Nel piano standard, i primi 5 GB al mese sono gratuiti, pertanto ti vengono addebitati 9 GB (14 GB - 5 GB).

  

### Limiti di quota per l'archiviazione e il traffico di pull
{: #registry_quota_limits}

A seconda del piano di servizio scelto, puoi eseguire il push e il pull di immagini da e verso
il tuo spazio dei nomi finché non raggiungi i tuoi limiti di quota specifici del piano o personalizzati.
{:shortdesc}

**Archiviazione: **

  Quando raggiungi o superi i limiti di quota per il tuo piano, non puoi eseguire il push di alcuna immagine agli spazi dei nomi nel tuo account {{site.data.keyword.Bluemix_notm}} finché non [liberi dello spazio rimuovendo le immagini](/docs/services/Registry?topic=registry-registry_quota#registry_quota_freeup) dai tuoi spazi dei nomi o [esegui l'upgrade al piano standard](#registry_plan_upgrade). Se imposti dei limiti di quota per l'archiviazione nel tuo piano gratuito o standard, puoi anche [aumentare questo limite di quota](/docs/services/Registry?topic=registry-registry_quota#registry_quota_set) per riabilitare il push di nuove immagini.

  Esempio per il piano standard:

  > Il tuo limite di quota corrente per l'archiviazione è impostato su 1 GB. Tutte le immagini private che sono memorizzate negli spazi dei nomi del tuo account {{site.data.keyword.Bluemix_notm}} utilizzano già 900 MB di questa archiviazione. Hai a disposizione 100 MB di archiviazione fino al raggiungimento del tuo limite di quota. Un utente vuole eseguire il push di un'immagine con una dimensione di 2 GB sulla macchina locale. Poiché il limite di quota non è stato ancora raggiunto, {{site.data.keyword.registrylong_notm}} consente all'utente di eseguire il push di questa immagine.
  >
  > Dopo il push, {{site.data.keyword.registrylong_notm}} determina la dimensione effettiva dell'immagine nel tuo spazio dei nomi, che può variare dalla dimensione sulla tua macchina locale, e controlla se viene raggiunto il limite per l'archiviazione. In questo esempio, l'utilizzo dell'archiviazione aumenta da 900 MB a 2 GB. Con il tuo limite di quota corrente impostato su 1 GB, {{site.data.keyword.registrylong_notm}} ti impedisce di eseguire il push di altre immagini al tuo spazio dei nomi.

**Traffico di pull: **

  Quando raggiungi o superi i limiti di quota per il tuo piano, non puoi eseguire il pull di alcuna immagine dagli
spazi dei nomi nel tuo account {{site.data.keyword.Bluemix_notm}}
finché non attendi che inizi il periodo di fatturazione successivo, [esegui l'upgrade al piano standard](#registry_plan_upgrade) o [aumenti i tuoi limiti
di quota per il traffico di pull](/docs/services/Registry?topic=registry-registry_quota#registry_quota_set).

  Esempio per il piano standard:

  > Nel mese, il
tuo limite di quota per il traffico di pull è impostato su 5 GB. Hai già eseguito il pull di immagini dai tuoi spazi dei nomi e hai utilizzato
4,5 GB di questo traffico di pull. Hai a disposizione 0,5 GB di traffico di pull fino al raggiungimento del tuo limite di quota. Un utente vuole eseguire il pull di un'immagine con una dimensione di 1 GB dal tuo spazio dei nomi. Poiché il limite di
quota non è stato ancora raggiunto, {{site.data.keyword.registrylong_notm}} consente
all'utente di eseguire il pull di questa immagine.
  >
  > Una volta eseguito il pull dell'immagine, {{site.data.keyword.registrylong_notm}} determina la larghezza di banda che hai utilizzato
durante il pull e controlla se è stato raggiunto il limite per il traffico di pull. In questo esempio, l'utilizzo del traffico di pull aumenta da 4,5 GB a 5,5 GB. Con il tuo limite di quota corrente impostato su 5 GB, {{site.data.keyword.registrylong_notm}} ti impedisce di eseguire il pull delle immagini
dal tuo spazio dei nomi.

### Stima dei costi
{: #registry_estimating_costs}

Utilizza il calcolatore del prezzo {{site.data.keyword.Bluemix_notm}} per stimare il costo del tuo piano.
{:shortdesc}

Puoi dare un prezzo alla tua applicazione utilizzando i calcolatori dei costi forniti da {{site.data.keyword.Bluemix_notm}}.

1. Apri il listino prezzi, vedi [Prezzi di {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/pricing).
2. Nella sezione **Pagamento a consumo**, fai clic su **Stima i tuoi costi con i nostri calcolatori**. Viene aperto il calcolatore.
3. Scorri fino alla sezione **Registro contenitore** nella sezione **Addebiti contenitore**.
4. Immetti le tue stime di traffico e archiviazione nei campi forniti.

I tuoi costi stimati vengono visualizzati nel calcolatore.

## Aggiornamento del tuo piano di servizio
{: #registry_plan_upgrade}

Puoi eseguire l'upgrade del tuo piano di servizio per beneficiare di un utilizzo illimitato di
archiviazione e di traffico di pull per gestire le immagini Docker per tutti gli spazi dei nomi nel tuo account {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Se desideri conoscere qual è il piano dei servizi di cui disponi, esegui il comando `ibmcloud cr plan`.

1. Accedi a {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

   Se hai un ID federato, utilizza `ibmcloud login --sso` per eseguire l'accesso alla CLI {{site.data.keyword.Bluemix_notm}}. Immetti il tuo nome utente e usa
l'URL fornito nell'output della CLI per richiamare la tua passcode monouso. Sai di avere un ID federato se l'accesso non riesce senza `--sso` e riesce con l'opzione `--sso`.
    {:tip}

2. Esegue l'upgrade al piano standard.

   ```
   ibmcloud cr plan-upgrade standard
   ```
   {: pre}

   Se hai un account {{site.data.keyword.Bluemix_notm}} Lite, devi eseguire l'upgrade a un account Pagamento a consumo o Sottoscrizione {{site.data.keyword.Bluemix_notm}} prima di eseguire `ibmcloud cr plan-upgrade`.
   {:tip}

## Apprendimento delle nozioni di base
{: #registry_planning}

Preparati per memorizzare e condividere le tue immagini Docker con {{site.data.keyword.registrylong_notm}} apprendendo le basi del registro.
{:shortdesc}

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione (ad esempio, nei token di registro) o in qualsiasi dato di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{:tip}

### Comprendere i termini utilizzati in {{site.data.keyword.registrylong_notm}}
{: #terms}

<dl>
  <dt>Dockerfile</dt>
  <dd>Un Dockerfile è un file di testo che contiene le istruzioni per creare un'immagine Docker. Normalmente, un'immagine viene creata basandosi su un'immagine che contiene un sistema operativo di base, come ad esempio Ubuntu. Puoi modificare in modo incrementale l'immagine di base con le tue istruzioni del Dockerfile per definire l'ambiente in cui deve essere eseguita l'applicazione. Ogni modifica all'immagine di base descrive un nuovo livello dell'immagine e puoi effettuare più modifiche in una sola riga del Dockerfile. Le istruzioni in un Dockerfile potrebbero inoltre fare riferimento alle risorse utente di build archiviate separatamente, come un'applicazione, la configurazione dell'applicazione e le sue dipendenze.</dd>
</dl>

<dl>
  <dt>Immagine</dt>
  <dd>Un file system e i relativi parametri di esecuzione utilizzati all'interno di un runtime del contenitore per creare un contenitore. Il file system è costituito da una serie di livelli, combinati al runtime, che vengono creati mentre l'immagine viene creata da aggiornamenti successivi. L'immagine non conserva lo stato mentre il contenitore viene eseguito.</dd>
</dl>

<dl>
  <dt>Spazio dei nomi</dt>
  <dd>Gli spazi dei nomi sono un modo per organizzare i repository delle tue immagini all'interno di {{site.data.keyword.registrylong_notm}}. Lo spazio dei nomi è associato al tuo account
{{site.data.keyword.Bluemix_notm}}. Quando configuri il tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}, lo spazio dei nomi viene aggiunto all'URL del registro nel seguente modo: <code><em>&lt;region&gt;</em>.icr.io/my_namespace</code>.

  Ogni utente nel tuo account {{site.data.keyword.Bluemix_notm}} può visualizzare e gestire le immagini
memorizzate nel tuo spazio dei nomi del registro. Puoi configurare più spazi dei nomi per avere, ad esempio, repository separati per i tuoi
ambienti di produzione e di preparazione.</dd>
</dl>

<dl>
  <dt>Immagini contenitore OCI</dt>
  <dd>Le immagini del contenitore che sono conformi a [OCI Image Format Specification ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/opencontainers/image-spec).</dd>
</dl>

<dl>
  <dt>Registro</dt>
  <dd>Un registro è un servizio che fornisce l'archiviazione per le immagini OCI (conosciute anche come immagini Docker). I client OCI possono accedere o "passare" le immagini OCI che utilizzano un nome del dominio del registro appropriato. Le immagini possono essere accessibili a chiunque (immagini pubbliche) oppure l'accesso può essere limitato a un gruppo (immagini private). {{site.data.keyword.registrylong_notm}} fornisce un registro delle immagini privato a più tenant altamente disponibile che viene ospitato e gestito da {{site.data.keyword.IBM_notm}}. Puoi utilizzare il registro per aggiungere uno spazio dei nomi al tuo account e poi passare le immagini al tuo spazio dei nomi.</dd>
</dl>

<dl>
  <dt>Repository</dt>
  <dd>Un repository di immagini è una raccolta di immagini correlate, contrassegnate con tag nel registro. Il repository viene spesso utilizzato in modo intercambiabile con l'immagine, ma un repository potenzialmente contiene più varianti di un'immagine con tag.</dd>
</dl>

<dl>
  <dt>Tag</dt>
  <dd>Una tag è un identificativo di un'immagine in un repository. Puoi utilizzare le tag per distinguere diverse versioni della stessa immagine di base in un repository. Quando esegui un comando Docker e non specifichi una tag di una immagine del repository, viene utilizzata per impostazione predefinita l'immagine contrassegnata con <code>ultima</code>.</dd>
</dl>

Per ulteriori informazioni sui termini specifici Docker, [consulta il glossario Docker ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.docker.com/glossary/).

### Pianificazione degli spazi dei nomi
{: #registry_namespaces}

{{site.data.keyword.registrylong_notm}} fornisce un registro delle immagini privato
a più tenant che viene ospitato e gestito da IBM. Puoi memorizzare e condividere le tue immagini Docker in questo registro configurando uno spazio dei nomi del registro.
{:shortdesc}

Puoi configurare più spazi dei nomi per avere, ad esempio, repository separati per i tuoi
ambienti di produzione e di preparazione. Se vuoi utilizzare il registro in più regioni {{site.data.keyword.Bluemix_notm}}, devi configurare uno spazio dei nomi per
ogni regione. I nomi degli spazi dei nomi sono univoci nelle regioni. Puoi utilizzare lo stesso nome dello spazio dei nomi per ogni regione, a meno che
qualcun altro abbia già configurato uno spazio dei nomi con quel nome in tale regione.

Puoi controllare l'accesso ai tuoi spazi dei nomi utilizzando le politiche IAM. Per ulteriori informazioni, consulta [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry?topic=registry-user#user).

Per lavorare solo con le immagini pubbliche fornite da IBM, non hai bisogno di configurare uno
spazio dei nomi.

Se non sei sicuro che uno spazio dei nomi sia già impostato per il tuo account, esegui il comando `ibmcloud cr namespace-list` per richiamare le informazioni sugli spazi dei nomi esistenti.
{:tip}

Quando scegli uno spazio dei nomi, considera le seguenti regole:

- Il tuo spazio dei nomi deve essere univoco in una regione {{site.data.keyword.Bluemix_notm}}.
- Il tuo spazio dei nomi deve avere una lunghezza compresa tra 4 e 30 caratteri.
- Il tuo spazio dei nomi deve iniziare con almeno una lettera o un numero.
- Il tuo spazio dei nomi deve contenere solo lettere minuscole, numeri o caratteri di sottolineatura (_).

Non inserire informazioni personali nei tuoi nomi dello spazio dei nomi.
{:tip}

Dopo aver impostato il tuo primo spazio dei nomi, ti verrà assegnato il piano di servizio {{site.data.keyword.registrylong_notm}}
gratuito se non hai già [eseguito l'upgrade del tuo piano](#registry_plan_upgrade).

## Regioni
{: #registry_regions}

I registri di {{site.data.keyword.registrylong_notm}} sono disponibili in diverse regioni.
{:shortdesc}

### Regioni locali
{: #registry_regions_local}

Una regione locale è un'area geografica a cui si accede da un endpoint dedicato. I nomi del dominio {{site.data.keyword.registrylong_notm}} per le regioni sono stati modificati. I nuovi nomi del dominio sono disponibili nella console e nella CLI.

I nomi del dominio vengono mostrati nella seguente tabella.

| Regione del registro locale | Nuovo nome del dominio | Nome del dominio obsoleto |
|-----|----|-----------|
| `ap-north` | `jp.icr.io` | Non applicabile |
| `ap-south` | `au.icr.io` | `registry.au-syd.bluemix.net` |
| `eu-central` | `de.icr.io` | `registry.eu-de.bluemix.net` |
| `uk-south` | `uk.icr.io` | `registry.eu-gb.bluemix.net` |
| `us-south` | `us.icr.io` | `registry.ng.bluemix.net` |
{: caption="Tabella 3. Nomi del dominio per le regioni locali." caption-side="top"}

I nomi del dominio `bluemix.net` esistenti sono obsoleti, ma puoi continuare ad utilizzarli per il momento e la data di termine del supporto sarà annunciata più avanti.
{: deprecated}

**Nomi del dominio del controllo vulnerabilità**

I nomi del dominio del controllo vulnerabilità per le regioni sono stati modificati. I nuovi nomi del dominio sono disponibili nella console e nella CLI.

I nuovi nomi del dominio vengono mostrati nella seguente tabella.

| Regione del controllo vulnerabilità locale | Nuovo nome del dominio | Nome del dominio obsoleto |
|-----|----|-----------|
| `ap-north` | `jp.icr.io/va` | Non applicabile |
| `ap-south` | `au.icr.io/va` | `va.au-syd.bluemix.net` |
| `eu-central` | `de.icr.io/va` | `va.eu-de.bluemix.net` |
| `uk-south` | `uk.icr.io/va` | `va.eu-gb.bluemix.net` |
| `us-south` | `us.icr.io/va` | `va.ng.bluemix.net` |
{: caption="Tabella 4. Nomi del dominio per le regioni locali." caption-side="top"}

I nomi del dominio `bluemix.net` esistenti sono obsoleti, ma puoi continuare ad utilizzarli per il momento e la data di termine del supporto sarà annunciata più avanti.
{: deprecated}

Tutte le risorse del registro sono associate al registro regionale specifico con cui stai attualmente lavorando. Ad esempio, spazi dei nomi, immagini, token, impostazioni di quote e impostazioni dei piani devono essere gestiti separatamente per ogni registro regionale.

Se vuoi utilizzare una regione diversa dalla tua regione locale, puoi scegliere come destinazione la regione a cui desideri accedere eseguendo il comando `ibmcloud cr region-set`. Puoi eseguire il comando senza parametri per ottenere un elenco delle regioni disponibili o puoi specificare la regione come un parametro.

Per eseguire il comando con i parametri, sostituisci `<region>` con il nome della regione, ad esempio `eu-central`.

```
ibmcloud cr region-set <region>
```
{: pre}

Ad esempio, per scegliere la regione eu-central, immetti il seguente comando:

```
ibmcloud cr region-set eu-central
```
{: pre}

Dopo aver specificato una diversa regione di destinazione, effettua nuovamente l'accesso al registro: `ibmcloud cr login`.

### Registro globale
{: #registry_regions_global}

È disponibile un registro globale, senza alcuna regione inclusa nel proprio nome (`icr.io`). Solo le immagini pubbliche fornite da IBM sono ospitate in questo registro. Per gestire le tue immagini, ad esempio configurando gli spazi dei nomi o inserendo tag e trasmettendo le immagini a un registro, utilizza un [registro regionale locale](#registry_regions_local).
{:shortdesc}

Il nome del dominio per il registro globale è stato modificato. Il nuovo nome del dominio è disponibile nella console e nella CLI. 

Il nuovo nome del dominio viene mostrato nella seguente tabella.

| Registro | Nuovo nome del dominio | Nome del dominio obsoleto |
|-----|----|-----------|
| Globale | `icr.io` | `registry.bluemix.net` |
{: caption="Tabella 5. Nome del dominio per il registro globale." caption-side="top"}

I nomi del dominio `bluemix.net` esistenti sono obsoleti, ma puoi continuare ad utilizzarli per il momento e la data di termine del supporto sarà annunciata più avanti.
{: deprecated}

Puoi indicare come destinazione il registro locale eseguendo il comando `ibmcloud cr region-set`.

Ad esempio, per specificare il registro globale, immetti il seguente comando:

```
ibmcloud cr region-set global
```
{: pre}

Per ulteriori informazioni sul comando `ibmcloud cr region-set`, vedi [CLI di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set).

Dopo aver specificato come destinazione il registro globale, esegui il comando `ibmcloud cr login` per registrare il tuo daemon Docker locale nel registro globale in modo da poter eseguire il pull delle immagini pubbliche fornite da {{site.data.keyword.IBM_notm}}.

**Nomi del dominio del controllo vulnerabilità**

Il nome del dominio del controllo vulnerabilità globale è stato modificato. Il nuovo nome del dominio è disponibile nella console e nella CLI. 

Il nuovo nome del dominio viene mostrato nella seguente tabella.

| Controllo vulnerabilità | Nuovo nome del dominio | Nome del dominio obsoleto |
|-----|----|-----------|
| Globale | `icr.io/va` | `va.bluemix.net` |
{: caption="Tabella 6. Nome del dominio per il registro globale per il controllo vulnerabilità." caption-side="top"}

I nomi del dominio `bluemix.net` esistenti sono obsoleti, ma puoi continuare ad utilizzarli per il momento e la data di termine del supporto sarà annunciata più avanti.
{: deprecated}

## Supporto per Docker
{: #docker}

{{site.data.keyword.registrylong_notm}} supporta Docker Engine v1.12.6 o successive.

Docker è necessario solo se vuoi eseguire il push o il pull delle immagini o se vuoi eseguire il comando `ibmcloud cr ppa-archive-load`.
