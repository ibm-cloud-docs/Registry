---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-21"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

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

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

Puoi utilizzare la CLI {{site.data.keyword.registrylong}}, che è fornita nel plug-in CLI `container-registry`, per gestire il tuo registro e le relative risorse per il tuo account {{site.data.keyword.cloud_notm}}.
{: shortdesc}

**Prerequisiti**

* Installa la CLI {{site.data.keyword.cloud_notm}}, vedi [Introduzione alla CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started). Il prefisso per l'esecuzione dei comandi utilizzando la CLI {{site.data.keyword.cloud_notm}} è `ibmcloud`.
* Prima di eseguire i comandi del registro, effettua l'accesso a {{site.data.keyword.cloud_notm}}
 con il comando `ibmcloud login` per generare un token di accesso e autenticare la tua sessione.

Nella riga di comando, vieni avvisato quando sono disponibili gli aggiornamenti alla CLI `ibmcloud` e ai plug-in CLI `container-registry`. Assicurati di mantenere la CLI aggiornata in modo da poter utilizzare tutti i comandi e gli indicatori disponibili.

Se desideri visualizzare la versione corrente del tuo plugin CLI `container-registry`, esegui `ibmcloud plugin list`.

Per informazioni su come utilizzare la CLI {{site.data.keyword.registrylong_notm}}, vedi [Introduzione a {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started).

Per ulteriori informazioni sui ruoli della piattaforma IAM e di accesso al servizio necessari per alcuni comandi, consulta [Gestione dell'accesso utente con Identity and Access Management (IAM)](/docs/services/Registry?topic=registry-iam#iam).

Non inserire informazioni personali nelle immagini del contenitore, nei nomi degli spazi dei nomi, nei campi di descrizione (ad esempio, nei token di registro) o in qualsiasi dato di configurazione dell'immagine (ad esempio, nomi o etichette dell'immagine).
{: important}

## `ibmcloud cr api`
{: #bx_cr_api}

Restituisce i dettagli sull'endpoint API del registro in cui vengono eseguiti i comandi.

```
ibmcloud cr api
```
{: codeblock}

**Prerequisiti**

Nessun valore

## `ibmcloud cr build`
{: #bx_cr_build}

Crea un'immagine Docker in {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
<dt>`DIRECTORY`</dt>
<dd>L'ubicazione del tuo contesto di build, che contiene i tuoi file Dockerfile e prerequisiti. Se esegui il comando quando la tua directory di lavoro è impostata sulla posizione in cui è memorizzato il contesto di build, puoi sostituire `DIRECTORY` con un punto (.).</dd>
<dt>`--no-cache`</dt>
<dd>(Facoltativo)  Se specificato, i livelli di immagine memorizzati in cache dalle build precedenti non vengono utilizzati in questa build.</dd>
<dt>`--pull`</dt>
<dd>(Facoltativo) Se specificato, le immagini di base vengono estratte, anche se sull'host di build esiste già un'immagine con una tag corrispondente.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Facoltativo) Se specificato, l'output di build viene eliminato a meno che non si verifichi un errore.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(Facoltativo) Specifica un argomento di build aggiuntivo nel formato `'CHIAVE=VALORE'`. È possibile specificare più argomenti di build includendo questo parametro più volte. Il valore di ogni argomento di build è disponibile come variabile di ambiente quando specifichi una riga ARG che corrisponde alla chiave nel tuo Dockerfile.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(Facoltativo) Se utilizzi gli stessi file per più build, puoi scegliere un percorso di un Dockerfile diverso. Specifica la posizione del Dockerfile in relazione al contesto di build. Se non specificato, il valore predefinito è `PATH/Dockerfile`, dove PATH è la root del contesto di build.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>Il nome completo dell'immagine che desideri creare, che include lo spazio dei nomi e l'URL del registro.</dd>
</dl>

**Esempio**

Crea un'immagine Docker che non utilizza una cache di compilazione da compilazioni precedenti, dove l'output di compilazione è soppresso, la tag è *`us.icr.io/birds/bluebird:1`* e la directory è la tua directory di lavoro.

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Crea un'esenzione per un problema di sicurezza. Puoi creare un'esenzione per un problema di sicurezza che si applica a diversi ambiti. L'ambito può essere l'account, lo spazio dei nomi, il repository o una tag.

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opzioni del comando**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Per impostare il tuo account come ambito, utilizza `"*"` come valore. Per impostare uno spazio dei nomi, un repository o una tag come ambito, immetti il valore in uno dei seguenti formati: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Il tipo di problema di sicurezza che vuoi esentare. Per trovare i tipi di problema validi, esegui `ibmcloud cr exemption-types`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>L'ID del problema di sicurezza che vuoi esentare. Per trovare un ID problema, esegui `ibmcloud cr va <image>`, dove `<image>` è il nome della tua immagine, e usa il valore pertinente dalla colonna **Vulnerability ID** o **Configuration Issue ID**.
</dd>
</dl>

**Esempi**

Crea un'esenzione CVE per CVE con ID `CVE-2018-17929` per tutte le immagini nel repository `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Crea un'esenzione CVE al livello dell'account per CVE con ID `CVE-2018-17929`.

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Crea un'esenzione del problema di configurazione per il problema `application_configuration:nginx.ssl_protocols` per una sola immagine con la tag `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

Elenca le tue esenzioni per i problemi di sicurezza.

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opzioni del comando**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(Facoltativo) Elenca solo le esenzioni che si applicano a questo ambito. Per impostare uno spazio dei nomi, un repository o una tag come ambito, immetti il valore in uno dei seguenti formati: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
</dl>

**Esempio**

Elenca tutte le tue esenzioni per i problemi di sicurezza che si applicano alle immagini nel repository *`birds/bluebird`*. L'output include le esenzioni al livello dell'account, le esenzioni associate allo spazio dei nomi *`birds`* e le esenzioni associate al repository *`birds/bluebird`* ma senza alcuna tag specifica associata all'interno del repository *`birds/bluebird`*.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Elimina un'esenzione per un problema di sicurezza. Per visualizzare le tue esenzioni esistenti, esegui `ibmcloud cr exemption-list`.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opzioni del comando**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>Per impostare il tuo account come ambito, utilizza `"*"` come valore. Per impostare uno spazio dei nomi, un repository o una tag come ambito, immetti il valore in uno dei seguenti formati: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>Il tipo di problema dell'esenzione per il problema di sicurezza che vuoi rimuovere. Per trovare i tipi di problema per le tue esenzioni, esegui `ibmcloud cr exemption-list`.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>L'ID dell'esenzione per il problema di sicurezza che vuoi rimuovere. Per trovare gli ID sicurezza per le tue esenzioni, esegui `ibmcloud cr exemption-list`.
</dd>
</dl>

**Esempi**

Elimina un'esenzione CVE per CVE con ID `CVE-2018-17929` per tutte le immagini nel repository `us.icr.io/birds/bluebird`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Elimina un'esenzione CVE al livello dell'account per CVE con ID `CVE-2018-17929`.

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Elimina un'esenzione del problema di configurazione per il problema `application_configuration:nginx.ssl_protocols` per una sola immagine con la tag `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Elenca i tipi di problemi di sicurezza che puoi esentare.

```
ibmcloud cr exemption-types
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

Se stai utilizzando l'autenticazione IAM, questo comando abilita l'autorizzazione dettagliata. Per ulteriori informazioni, consulta [Gestione dell'accesso utente con Identity and Access Management (IAM)](/docs/services/Registry?topic=registry-iam#iam) e [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

Visualizza lo stato della politica IAM dell'account {{site.data.keyword.registryshort_notm}} di destinazione. Per ulteriori informazioni, consulta [Gestione dell'accesso utente con Identity and Access Management (IAM)](/docs/services/Registry?topic=registry-iam#iam) e [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Visualizza i dettagli di una specifica immagine.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Facoltativo) Formatta gli elementi di output utilizzando un template Go.

Per ulteriori informazioni, vedi [Formattazione e filtro dell'output della CLI per i comandi {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`IMAGE`</dt>
<dd>Il nome dell'immagine per cui vuoi ottenere un report. Puoi analizzare più immagini elencando ogni immagine nel comando con uno spazio tra ciascun nome.

<p>Per trovare i nomi delle tue immagini, esegui `ibmcloud cr image-list`. Combina il contenuto delle colonne **Repository** e **Tag** per creare il nome dell'immagine nel formato `repository:tag`. Se nel nome immagine non è specificata alcuna tag, viene analizzata l'immagine contrassegnata con la tag `latest`. </p>

</dd>
</dl>

**Esempio**

Visualizza i dettagli sulle porte esposte per l'immagine *`us.icr.io/birds/bluebird:1`*, utilizzando la direttiva di formattazione *`"{{ .Config.ExposedPorts }}"`*.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Visualizza tutte le immagini nel tuo account {{site.data.keyword.cloud_notm}}.

Il nome dell'immagine è la combinazione del contenuto delle colonne **Repository** e **Tag** nel formato: `repository:tag`
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
<dt>`--no-trunc`</dt>
<dd>(Facoltativo) Non troncare i digest immagine.</dd>
<dt>`--format FORMAT`</dt>
<dd>(Facoltativo) Formatta gli elementi di output utilizzando un template Go.

Per ulteriori informazioni, vedi [Formattazione e filtro dell'output della CLI per i comandi {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Facoltativo) Ogni immagine viene elencata nel formato: `repository:tag`</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(Facoltativo) Limita l'output per visualizzare solo le immagini nello spazio dei nomi o nello spazio dei nomi e nel repository specificati. </dd>
<dt>`--include-ibm`</dt>
<dd>(Facoltativo) Include le immagini pubbliche fornite da {{site.data.keyword.IBM_notm}} nell'output. Senza questa opzione, vengono elencate solo le immagini private per impostazione predefinita.</dd>
</dl>

**Esempio**

Visualizza le immagini nello spazio dei nomi *`birds`* nel formato `repository:tag`, senza troncare i digest immagine.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Elimina una o più immagini specificate da {{site.data.keyword.registrylong_notm}}.

Dove sono presenti più tag per lo stesso digest immagine all'interno di un repository, il comando `ibmcloud cr image-rm` rimuove l'immagine sottostante e tutte le relative tag. Se la stessa immagine è presente in uno spazio dei nomi o repository diversi, tale copia dell'immagine non viene rimossa. Se vuoi rimuovere una tag da un'immagine e lasciare in vigore l'immagine sottostante e tutte le altre tag, utilizza il [comando `ibmcloud cr image-untag`](#bx_cr_image_untag).
{: tip}

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**

<dl>
<dt>`IMAGE`</dt>
<dd>Il nome dell'immagine che desideri eliminare. Puoi eliminare più immagini contemporaneamente elencando ogni immagine nel comando con uno spazio tra ciascun nome. `IMMAGE` deve essere nel formato `repository:tag`, ad esempio: `us.icr.io/namespace/image:latest`

<p>Per trovare i nomi delle tue immagini, esegui `ibmcloud cr image-list`. Combina il contenuto delle colonne **Repository** e **Tag** per creare il nome dell'immagine nel formato `repository:tag`. Se nel nome immagine non è specificata alcuna tag, per impostazione predefinita viene eliminata l'immagine contrassegnata con la tag `latest`.</p>

</dd>
</dl>

**Esempio**
Elimina l'immagine `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

Aggiungi una tag che specifichi nel comando a un'immagine esistente, copia la tag in un altro repository oppure in un repository in uno spazio dei nomi diverso. L'immagine di destinazione, `TARGET_IMAGE`, è la nuova immagine e l'immagine di origine, `SOURCE_IMAGE`, è l'immagine esistente in {{site.data.keyword.registrylong_notm}}. Le immagini di origine e di destinazione devono essere nella stessa regione.

Per trovare i nomi delle tue immagini, esegui `ibmcloud cr image-list`. Combina il contenuto delle colonne **Repository** e **Tag** per creare il nome dell'immagine nel formato `repository:tag`.
{: tip}

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>Il nome dell'immagine di origine. `SOURCE_IMAGE` deve essere nel formato `repository:tag`, ad esempio: `us.icr.io/namespace/image:latest`

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>Il nome dell'immagine di destinazione. `TARGET_IMAGE` deve essere nel formato `repository:tag`, ad esempio: `us.icr.io/namespace/image:latest`

</dd>
</dl>

**Esempi**

Aggiungi un altro riferimento tag, `latest`, all'immagine `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

Copia l'immagine `us.icr.io/birds/bluebird:peck` in un altro repository nello stesso spazio dei nomi `birds/pigeon`.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

Copia l'immagine `us.icr.io/birds/bluebird:peck` in un altro spazio dei nomi `animals` a cui hai accesso.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr image-untag`
{: #bx_cr_image_untag}

Rimuove una tag o delle tag da ogni immagine specificata in {{site.data.keyword.registrylong_notm}}.

Per rimuovere una specifica tag da un'immagine e lasciare in vigore l'immagine sottostante e tutte le altre tag, utilizza il comando `ibmcloud cr image-untag`. Se vuoi eliminare l'immagine sottostante e tutte le relative tag, utilizza invece il [comando `ibmcloud cr image-rm`](#bx_cr_image_rm).
{: tip}

```
ibmcloud cr image-untag IMAGE [IMAGE...]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**

<dl>
<dt>`IMAGE`</dt>
<dd>Il nome dell'immagine per cui vuoi rimuovere la tag. Puoi eliminare la tag da più immagini contemporaneamente elencando ogni immagine nel comando con uno spazio tra ciascun nome. `IMMAGE` deve essere nel formato `repository:tag`, ad esempio: `us.icr.io/namespace/image:latest`

<p>Per trovare i nomi delle tue immagini, esegui `ibmcloud cr image-list`. Combina il contenuto delle colonne **Repository** e **Tag** per creare il nome dell'immagine nel formato `repository:tag`. Se nel nome immagine non è specificata alcuna tag, il comando ha esito negativo.</p>

</dd>
</dl>

**Esempio**

Rimuovi la tag `1` dall'immagine `us.icr.io/birds/bluebird:1`.

```
ibmcloud cr image-untag us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

Visualizza il nome e l'account del registro a cui sei collegato.

```
ibmcloud cr info
```
{: codeblock}

**Prerequisiti**

Nessun valore

## `ibmcloud cr login`
{: #bx_cr_login}

Questo comando esegue il comando `docker login` nel registro. Il comando `docker login` è obbligatorio per abilitare l'esecuzione dei comandi `docker push` o `docker pull` per il registro. Questo comando non è obbligatorio per eseguire altri comandi `ibmcloud cr`. Se Docker non è installato, questo comando restituisce un messaggio di errore.

```
ibmcloud cr login
```
{: codeblock}

**Prerequisiti**

Nessun valore

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Scegli un nome per il tuo spazio dei nomi e aggiungilo al tuo account {{site.data.keyword.cloud_notm}}.

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Lo spazio dei nomi che desideri aggiungere. Lo spazio dei nomi deve essere univoco tra tutti gli account {{site.data.keyword.cloud_notm}} nella stessa regione. Gli spazi dei nomi devono avere tra i 4 e i 30 caratteri e contenere solo lettere minuscole, numeri, trattini (-) e caratteri di sottolineatura (_). Gli spazi dei nomi devono iniziare e terminare con una lettera o un numero.
  
<p>  
<strong>Importante</strong> non inserire informazioni personali nei tuoi nomi dello spazio dei nomi.
</p>
  
</dd>
</dl>

**Esempio**

Crea uno spazio dei nomi con il nome *`birds`*.

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Visualizza tutti gli spazi dei nomi che appartengono al tuo account {{site.data.keyword.cloud_notm}}.

```
ibmcloud cr namespace-list
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Rimuove uno spazio dei nomi dal tuo account {{site.data.keyword.cloud_notm}}. Le immagini in questo spazio dei nomi vengono eliminate quando si rimuove lo spazio dei nomi.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
<dt>`NAMESPACE`</dt>
<dd>Lo spazio dei nomi che desideri rimuovere.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Facoltativo) Forza l'esecuzione del comando senza alcun prompt utente.</dd>
</dl>

**Esempio**

Rimuovi lo spazio dei nomi *`birds`*.

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

Visualizza il piano dei prezzi.

```
ibmcloud cr plan
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Esegue il tuo upgrade al piano standard.

Per ulteriori informazioni sui piani, vedi [Piani del registro](/docs/services/Registry?topic=registry-registry_overview#registry_plans).

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opzioni del comando**
<dl>
<dt>`PLAN`</dt>
<dd>(Facoltativo) Il nome del piano dei prezzi a cui desideri eseguire l'upgrade. Se `PLAN` non viene specificato, il valore predefinito è `standard`.</dd>
</dl>

**Esempio**

Esegui l'upgrade al piano dei prezzi standard.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

Importa il software {{site.data.keyword.IBM_notm}} scaricato da [IBM Passport Advantage Online for customers ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/passportadvantage/pao_customer.html) e impacchettato per essere utilizzato con Helm nel tuo spazio dei nomi {{site.data.keyword.registrylong_notm}}.

Le immagini del contenitore vengono trasmesse al tuo spazio dei nomi {{site.data.keyword.registryshort_notm}} privato. I grafici Helm sono scritti in una directory `ppa-import` che viene creata nella directory da cui esegui il comando. Facoltativamente, puoi utilizzare il [progetto open source Chart Museum ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/helm/charts/tree/master/stable/chartmuseum) per ospitare i grafici Helm.

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>Il percorso del file compresso scaricato da IBM Passport Advantage.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>Uno dei tuoi spazi dei nomi. Le immagini del contenitore nel file compresso vengono trasmesse a questo spazio dei nomi. Per elencare gli spazi dei nomi, esegui `ibmcloud cr namespace-list`.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Facoltativo) L'identificativo di risorsa univoco per [Chart Museum ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-user UTENTE`</dt>
  <dd>(Facoltativo) Il tuo nome utente di [Chart Museum ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(Facoltativo) La tua password di [Chart Museum ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/helm/charts/tree/master/stable/chartmuseum).</dd>
</dl>

**Esempio**

Importa il software IBM e impacchettalo per l'utilizzo con Helm nel tuo spazio dei nomi {{site.data.keyword.registrylong_notm}} *`birds`*, in cui il percorso al file compresso è *`downloads/compressed_file.tgz`*.

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

Visualizza le tue quote correnti per traffico e archiviazione e le informazioni di utilizzo rispetto a tali quote.

```
ibmcloud cr quota
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Modifica la quota specificata.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per la configurazione di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Opzioni del comando**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(Facoltativo) Modifica la tua quota di traffico sul valore specificato in megabyte. L'operazione non riesce se non sei autorizzato a impostare il traffico o se imposti un valore che supera il tuo piano dei prezzi corrente.</dd>
<dt>`--storage STORAGE`</dt>
<dd>(Facoltativo) Modifica la tua quota di archiviazione sul valore specificato in megabyte. L'operazione non riesce se non sei autorizzato a impostare le quote di archiviazione o se imposti un valore che supera il tuo piano dei prezzi corrente.</dd>
</dl>

**Esempio**

Imposta il tuo limite di quota per il pull del traffico su *7000* megabyte e l'archiviazione su *600* megabyte.

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

Visualizza la regione di destinazione e il registro.

```
ibmcloud cr region
```
{: codeblock}

**Prerequisiti**

Nessun valore

Per ulteriori informazioni, vedi [Regioni](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Imposta una regione di destinazione per i comandi {{site.data.keyword.registrylong_notm}}. Per elencare le regioni disponibili, esegui il comando senza parametri.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**Prerequisiti**

Nessun valore

**Opzioni del comando**
<dl>
<dt>`REGION`</dt>
<dd>(Facoltativo) Il nome della tua regione di destinazione, ad esempio, `us-south`.

Per ulteriori informazioni, vedi [Regioni](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

</dd>
</dl>

**Esempio**

Specifica la regione Stati Uniti Sud

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-add` (obsoleto)
{: #bx_cr_token_add}

Aggiungi un token che puoi utilizzare per controllare l'accesso a un registro.

L'utilizzo dei token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi è obsoleto. Utilizza invece le chiavi API per automatizzare l'accesso ai tuoi spazi dei nomi, consulta [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](/docs/services/Registry?topic=registry-registry_access#registry_api_key).
{: deprecated}

```
ibmcloud cr token-add [--description DESCRIPTION] [--quiet | -q] [--non-expiring] [--readwrite]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di gestione della piattaforma](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Opzioni del comando**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>(Facoltativo) Specifica il valore come una descrizione per il token, che viene visualizzata quando esegui `ibmcloud cr token-list`. Se il tuo token viene creato automaticamente da {{site.data.keyword.containerlong_notm}}, la descrizione viene impostata sul nome del tuo cluster Kubernetes. In questo caso, il token viene rimosso automaticamente alla rimozione del cluster.
  
<p> 
  <strong>Importante</strong> non inserire informazioni personali nella tua descrizione del token.
</p>

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Facoltativo) Visualizza solo il token, senza alcun testo circostante.</dd>
<dt>`--non-expiring`</dt>
<dd>(Facoltativo) Crea un token con l'accesso che non scade. Se questo parametro non è impostato, l'accesso da un token scade dopo 24 ore per impostazione predefinita.</dd>
<dt>`--readwrite`</dt>
<dd>(Facoltativo) Crea un token che concede l'accesso in lettura e scrittura. Senza questa opzione, l'accesso è di sola lettura per impostazione predefinita.</dd>
</dl>

**Esempio**

Aggiungi un token con la descrizione *Token for my account* che non scade e ha l'accesso di lettura/scrittura.

```
ibmcloud cr token-add --description "Token for my account" --non-expiring --readwrite
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

Richiama il token specificato dal registro.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di gestione della piattaforma](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Opzioni del comando**
<dl>
<dt>`TOKEN`</dt>
<dd>L'identificativo univoco del token che desideri richiamare. Per elencare i tuoi token, esegui `ibmcloud cr token-list`.</dd>
</dl>

**Esempio**

Richiama il token *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

Visualizza tutti i token esistenti per il tuo account {{site.data.keyword.cloud_notm}}.

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di gestione della piattaforma](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Opzioni del comando**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Facoltativo) Formatta gli elementi di output utilizzando un template Go.

Per ulteriori informazioni, vedi [Formattazione e filtro dell'output della CLI per i comandi {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_cli_list).

</dd>
</dl>

**Esempio**

Visualizza tutti i token in sola lettura, utilizzando la direttiva di formattazione *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`*.

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

Questo esempio produce l'output nel seguente formato:

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

Rimuovi uno o più token di registro specificati.

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di gestione della piattaforma](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Opzioni del comando**
<dl>
<dt>`TOKEN`</dt>
<dd>TOKEN può essere il token stesso o l'identificativo univoco del token, come mostrato in `ibmcloud cr token-list`. È possibile specificare più token e devono essere separati da uno spazio.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Facoltativo) Forza l'esecuzione del comando senza alcun prompt utente.</dd>
</dl>

**Esempio**

Rimuovi il token *10101010-101x-1x10-x1xx-x10xx10xxx10*.

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

Visualizza un report di valutazione delle vulnerabilità per le tue immagini.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Prerequisiti**

Per trovare delle informazioni sulle autorizzazioni necessarie, consulta [Ruoli di accesso per l'utilizzo di {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Opzioni del comando**
<dl>
<dt>`IMAGE`</dt>
<dd>Il nome dell'immagine per cui vuoi ottenere un report. Il report indica se l'immagine ha delle vulnerabilità di pacchetto note. Puoi richiedere report per più immagini contemporaneamente elencando ogni immagine nel comando con uno spazio tra ciascun nome.

<p>Per trovare i nomi delle tue immagini, esegui `ibmcloud cr image-list`. Combina il contenuto delle colonne **Repository** e **Tag** per creare il nome dell'immagine nel formato `repository:tag`. Se nel nome immagine non è specificata alcuna tag, il report valuta l'immagine contrassegnata con la tag `latest`.</p>

<p>Sono supportati i seguenti sistemi operativi:

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>RHEL (Red Hat Enterprise Linux)</li>
<li>Ubuntu</li>
</ul>
</p>

Per ulteriori informazioni, vedi [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](/docs/services/va?topic=va-va_index).

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Facoltativo) L'output del comando mostra informazioni aggiuntive sulle correzioni per i pacchetti vulnerabili.</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Facoltativo) L'output del comando è limitato per mostrare solo le vulnerabilità.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Facoltativo) L'output del comando è limitato per mostrare solo i problemi di configurazione.</dd>
<dt>`--output FORMATO`, `-o FORMATO`</dt>
<dd>(Facoltativo) L'output del comando viene restituito nel formato scelto. Il formato predefinito è `text`. Sono supportati i seguenti formati:

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**Esempi**

Visualizza un report di valutazione delle vulnerabilità standard per la tua immagine.

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

Visualizza un report di valutazione delle vulnerabilità per la tua immagine `us.icr.io/birds/bluebird:1` in formato JSON, che mostra solo le vulnerabilità.

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
