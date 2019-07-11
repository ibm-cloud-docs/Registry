---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, commands, format commands, filter command output, private registry, registry commands, formatting output, filtering output, output, Go template options, data types, 

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

# Formattazione e filtro dell'output della CLI per i comandi {{site.data.keyword.registrylong_notm}}
{: #registry_cli_list}

Puoi formattare e filtrare l'output della CLI per i comandi {{site.data.keyword.registrylong_notm}} supportati.
{:shortdesc}

Per impostazione predefinita, l'output della CLI viene visualizzato in un formato leggibile. Tuttavia, questa vista potrebbe limitare la tua capacità di utilizzare l'output, in particolare se il comando viene eseguito a livello di programmazione. Ad esempio, nell'output della CLI `ibmcloud cr image-list`, potresti voler ordinare il campo `Size` per dimensione numerica, ma il comando restituisce una descrizione della dimensione in formato stringa. Il plug-in CLI `container-registry` fornisce l'opzione formato che puoi utilizzare per applicare un template Go all'output della CLI. Il template Go è una funzione del [Linguaggio di programmazione Go ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://golang.org/pkg/text/template/) che puoi utilizzare per personalizzare l'output della CLI.

Puoi modificare l'output della CLI applicando l'opzione formato in due modi diversi:

1. Formatta i dati nel tuo output della CLI. Ad esempio, modifica l'output del campo `Created` dall'ora UNIX all'ora standard.
2. Filtra i dati nel tuo output della CLI. Ad esempio, filtra in base ai dettagli dell'immagine per visualizzare un sottoinsieme specifico di immagini utilizzando la condizione `if gt` del template Go.

Puoi utilizzare l'opzione formato con i seguenti comandi {{site.data.keyword.registrylong_notm}}. Fai clic su un comando per visualizzare un elenco di campi disponibili e i relativi tipi di dati.

- [`ibmcloud cr image-list`](#registry_cli_list_imagelist)
- [`ibmcloud cr image-inspect`](#registry_cli_list_imageinspect)
- [`ibmcloud cr token-list`](#registry_cli_list_tokenlist)

I seguenti esempi di codice illustrano come utilizzare le opzioni di formattazione e di filtro.

- Esegui il comando `ibmcloud cr image-list` per visualizzare il repository, la tag e lo stato di sicurezza di tutte le immagini che hanno una dimensione superiore a 1 MB:

  ```
  ibmcloud cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
  ```
  {: pre}

  **Output di esempio**

  ```
  example-<region>.icr.io/user1/ibmliberty:latest No Issues
  example-<region>.icr.io/user1/ibmnode:1 2 Issues
  example-<region>.icr.io/user1/ibmnode:test1 1 Issue
  example-<region>.icr.io/user1/ibmnode2:test2 7 Issues
  ```
  {: screen}

- Esegui il seguente comando `ibmcloud cr image-inspect` per visualizzare dove è ospitata la documentazione IBM per un'immagine pubblica IBM specificata:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"
  ```
  {: pre}

  **Output di esempio**

  ```
  map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
  ```
  {: screen}

- Esegui il seguente comando `ibmcloud cr image-inspect` per visualizzare le porte esposte per un'immagine specificata:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"
  ```
  {: pre}

  **Output di esempio**

  ```
  map[9080/tcp: 9443/tcp:]
  ```
  {: screen}

- Esegui il seguente comando `ibmcloud cr token-list` per visualizzare tutti i token di sola lettura:

  ```
  ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
  ```
  {: pre}

  **Output di esempio**

  ```
  0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
  ```
  {: screen}

## Opzioni e tipi di dati del template Go nel comando `ibmcloud cr image-list`
{: #registry_cli_list_imagelist}

Riesamina la seguente tabella per trovare le opzioni e i tipi di dati del template Go disponibili per il comando `ibmcloud cr image-list`.
{:shortdesc}

|Campo|Tipo|Descrizione|
|-----|----|-----------|
|`Created`|Numero intero (64 bit)|Visualizza quando è stata creata l'immagine, espresso in numero di secondi in [UNIX time ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/Unix_time).|
|`Digest`|Stringa|Visualizza l'identificativo univoco per un'immagine.|
|`Namespace`|Stringa|Visualizza lo spazio dei nomi in cui è memorizzata l'immagine.|
|`Repository`|Stringa|Visualizza il repository dell'immagine.|
|`Size`|Numero intero (64 bit)|Visualizza la dimensione dell'immagine in byte.|
|`Tag`|Stringa|Visualizza la tag dell'immagine.|
|`SecurityStatus`|Struct|Visualizza lo stato di vulnerabilità per l'immagine. Puoi filtrare e formattare i seguenti valori: *Status*  `string`, *IssueCount*  `int` e *ExemptionCount*  `int`. Gli stati possibili sono descritti in [Revisione di un report di vulnerabilità utilizzando la CLI](/docs/services/Registry?topic=va-va_index#va_registry_cli).|
{: caption="Tabella 1. Campi e tipi di dati disponibili nel comando <codeibmcloud cr image-list</code>." caption-side="top"}>

## Opzioni e tipi di dati del template Go nel comando `ibmcloud cr image-inspect`
{: #registry_cli_list_imageinspect}

Riesamina la seguente tabella per trovare le opzioni e i tipi di dati del template Go disponibili per il comando `ibmcloud cr image-inspect`.
{:shortdesc}

|Campo|Tipo|Descrizione|
|-----|----|-----------|
|`ID`|Stringa|Visualizza l'identificativo univoco per un'immagine.|
|`Parent`|Stringa|Visualizza l'ID dell'immagine principale utilizzata per creare questa immagine.|
|`Comment`|Stringa|Visualizza la descrizione dell'immagine.|
|`Created`|Stringa|Visualizza la [UNIX timestamp ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/Unix_time) in cui è stata creata l'immagine.|
|`Container`|Stringa|Visualizza l'ID del contenitore che ha creato l'immagine.|
|`ContainerConfig`|Oggetto|Visualizza la configurazione predefinita per i contenitori avviati da questa immagine. Vedi i dettagli del campo in [`Config`](#registry_cli_list_imageinspect_config).|
|`DockerVersion`|Stringa|Visualizza la versione Docker utilizzata per creare questa immagine.|
|`Author`|Stringa|Visualizza l'autore dell'immagine.|
|`Config`|Oggetto|Visualizza i metadati di configurazione per l'immagine. Vedi i dettagli del campo in [`Config`](#registry_cli_list_imageinspect_config).|
|`Architecture`|Stringa|Visualizza l'architettura del processore utilizzata per costruire questa immagine e che è necessaria per eseguire l'immagine.|
|`Os`|Stringa|Visualizza la famiglia di sistemi operativi utilizzata per creare questa immagine e che è necessaria per eseguire l'immagine.|
|`OsVersion`|Stringa|Visualizza la versione del sistema operativo utilizzato per creare questa immagine.|
|`Size`|Numero intero (64 bit)|Visualizza la dimensione dell'immagine in byte.|
|`VirtualSize`|Numero intero (64 bit)|Visualizza la somma delle dimensioni di ogni livello nell'immagine in byte.|
|`RootFS`|Oggetto|Visualizza i metadati che descrivono il file system root per l'immagine. Vedi i dettagli del campo in [`RootFS`](#registry_cli_list_imageinspect_rootfs).|
{: caption="Tabella 2. Campi e tipi di dati disponibili nel comando <codeibmcloud cr image-inspect</code>." caption-side="top"}>

### `Config`
{: #registry_cli_list_imageinspect_config}

|Campo|Tipo|Descrizione|
|-----|----|-----------|
|`Hostname`|Stringa|Visualizza il nome host del contenitore.|
|`Domainname`|Stringa|Visualizza il nome dominio completo del contenitore.|
|`User`|Stringa|Visualizza l'utente che esegue i comandi all'interno del contenitore in cui viene utilizzata l'immagine.|
|`AttachStdin`|Booleano|Visualizza _true_ se il flusso di input standard è collegato al contenitore e _false_ in caso contrario.|
|`AttachStdout`|Booleano|Visualizza _true_ se il flusso di output standard è collegato al contenitore e _false_ in caso contrario.|
|`AttachStderr`|Booleano|Visualizza _true_ se il flusso di errore standard è collegato al contenitore e _false_ in caso contrario.|
|`ExposedPorts`|Associazione chiave-valore|Visualizza l'elenco di porte esposte nel formato `[123:,456:]`.|
|`Tty`|Booleano|Visualizza _true_ se uno `pseudo-tty` è assegnato al contenitore e _false_ in caso contrario.|
|`OpenStdin`|Booleano|Visualizza _true_ se il flusso di input standard è aperto e _false_ se il flusso di input standard è chiuso.|
|`StdinOnce`|Booleano|Visualizza _true_ se il flusso di input standard viene chiuso dopo che il client collegato si disconnette e _false_ se il flusso di input standard rimane aperto.|
|`Env`|Array di stringhe|Visualizza l'elenco di variabili di ambiente in forma di coppie chiave-valore.|
|`Cmd`|Array di stringhe|Descrive i comandi e gli argomenti passati a un contenitore che devono essere eseguiti all'avvio del contenitore.|
|`Healthcheck`|Oggetto|Descrive come controllare che il contenitore sta funzionando correttamente. Vedi i dettagli del campo in [`Healthcheck`](#registry_cli_list_imageinspect_healthcheck).|
|`ArgsEscaped`|Booleano|Visualizza true se il comando è già con escape (specifico di Windows).|
|`Image`|Stringa|Visualizza il nome dell'immagine che è stata passata dall'operatore.|
|`Volumes`|Associazione chiave-valore|Visualizza l'elenco di montaggi di volume che sono montati in un contenitore.|
|`WorkingDir`|Stringa|Visualizza la directory di lavoro all'interno del contenitore in cui vengono eseguiti i comandi specificati.|
|`Entrypoint`|Array di stringhe|Descrive il comando che viene eseguito all'avvio del contenitore.|
|`NetworkDisabled`|Booleano|Visualizza _true_ se la rete è disabilitata per il contenitore e _false_ se la rete è abilitata per il contenitore.|
|`MacAddress`|Stringa|Visualizza l'indirizzo MAC assegnato al contenitore.|
|`OnBuild`|Array di stringhe|Visualizza i metadati `ONBUILD` definiti nel Dockerfile dell'immagine.|
|`Labels`|Associazione chiave-valore|Visualizza l'elenco di etichette che sono state aggiunte all'immagine come coppie chiave/valore.|
|`StopSignal`|Stringa|Descrive il segnale di arresto UNIX da inviare all'arresto del contenitore.|
|`StopTimeout`|Numero intero|Visualizza il timeout in secondi per arrestare un contenitore.|
|`Shell`|Array di stringhe|Visualizza il formato shell di RUN, CMD, ENTRYPOINT.|
{: caption="Tabella 3. Campi e tipi di dati disponibili in <codeConfig</code>. " caption-side="top"}>

### `Healthcheck`
{: #registry_cli_list_imageinspect_healthcheck}

|Campo|Tipo|Descrizione|
|-----|----|-----------|
|`Test`|Array di stringhe|Visualizza come eseguire il test del controllo di integrità. Le opzioni disponibili sono:<ul><li>`{}`: ereditare il controllo di integrità</li><li>`{"NONE"}`: il controllo di integrità è disabilitato</li><li>`{"CMD", args...}`: eseguire gli argomenti direttamente</li><li>`{"CMD-SHELL", command}`: eseguire il comando con la shell predefinita del sistema</li></ul>|
|`Interval`|Numero intero (64 bit)|Visualizza il tempo di attesa tra due controlli di integrità in nanosecondi.|
|`Timeout`|Numero intero (64 bit)|Visualizza il tempo di attesa prima di considerare come non riuscito il controllo di integrità in nanosecondi.|
|`Retries`|Numero intero|Visualizza il numero di errori consecutivi necessari per considerare un contenitore come non funzionante correttamente.|
{: caption="Tabella 4. Campi e tipi di dati disponibili nella struttura <codeHealthcheck</code>." caption-side="top"}>

### `RootFS`
{: #registry_cli_list_imageinspect_rootfs}

|Opzione|Tipo|Descrizione|
|------|----|-----------|
|`Tipo`|Stringa|Visualizza il tipo di filesystem.|
|`Layers`|Array di stringhe|Visualizza i descrittori di ogni livello dell'immagine.|
|`BaseLayer`|Stringa|Visualizza il descrittore per il livello di base nell'immagine.|
{: caption="Tabella 5. Campi e tipi di dati disponibili nella struttura <codeRootFS</code>." caption-side="top"}>

## Opzioni e tipi di dati del template Go nel comando `ibmcloud cr token-list`
{: #registry_cli_list_tokenlist}

Riesamina la seguente tabella per trovare le opzioni e i tipi di dati del template Go disponibili per il comando `ibmcloud cr token-list`.
{:shortdesc}

|Campo|Tipo|Descrizione|
|-----|----|-----------|
|`ID`|Stringa|Visualizza l'identificativo univoco per un token.|
|`Expiry`|Numero intero (64 bit)|Visualizza la [UNIX timestamp ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/Unix_time) in cui scade il token.|
|`ReadOnly`|Booleano|Visualizza _true_ quando puoi eseguire solo il pull delle immagini e _false_ quando puoi eseguire il push e il pull di immagini da e verso il tuo spazio dei nomi.|
|`Descrizione`|Stringa|Visualizza la descrizione del token.|
{: caption="Tabella 6. Campi e tipi di dati disponibili nel comando <codeibmcloud cr token-list</code>." caption-side="top"}>
