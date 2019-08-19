---

copyright:
  years: 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# Note sulla release
{: #registry_release_notes}

Ottieni informazioni sulle ultime modifiche a {{site.data.keyword.registrylong}} e al Controllo vulnerabilità. Le modifiche sono raggruppate per data.
{:shortdesc}

## 1 agosto 2019
{: #01aug2019}

<dl>
  <dt>Il comando `ibmcloud cr retention-run` è disponibile</dt>
  <dd>Il comando `ibmcloud cr retention-run` ripulisce i tuoi spazi dei nomi conservando le immagini di ogni repository all'interno di uno spazio dei nomi in {{site.data.keyword.registrylong_notm}} applicando dei criteri specificati. Tutte le altre immagini nello spazio dei nomi vengono eliminate.
  
  Per ulteriori informazioni, vedi [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) e [Conservazione delle immagini](/docs/services/Registry?topic=registry-registry_retention).</dd>
</dl>

## 25 luglio 2019
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.at_full_notm}} disponibile per {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Utilizza il servizio {{site.data.keyword.at_full_notm}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.registrylong_notm}} in {{site.data.keyword.cloud}}.

  Per ulteriori informazioni, vedi [Eventi del Programma di traccia dell'attività](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>

## 1 luglio 2019
{: #1jul2019}

<dl>
  <dt>Il comando `ibmcloud cr token-add` non è più disponibile</dt>
  <dd>Il comando `ibmcloud cr token-add` è stato sospeso. Non puoi più aggiungere i token del registro alla CLI o all'API.</dd>
</dl>

## 27 giugno 2019
{: #27jun2019}

<dl>
  <dt>Lo Scanner contenitori non è più disponibile </dt>
  <dd>Lo Scanner contenitori è stato sospeso. Il Controllo vulnerabilità esegue ancora la scansione delle immagini di cui viene eseguito il push a {{site.data.keyword.registrylong_notm}}.</dd>
</dl>

## 13 giugno 2019
{: #13jun2019}

<dl>
  <dt>Rimuovi le tag dalle immagini </dt>
  <dd>Rimuovi una tag o delle tag da ogni immagine specificata in {{site.data.keyword.registrylong_notm}}.

  Per rimuovere una specifica tag da un'immagine e lasciare in vigore l'immagine sottostante e tutte le altre tag, utilizza il comando [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag). Se vuoi eliminare l'immagine sottostante e tutte le relative tag, utilizza invece il [comando `ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm).

  Per ulteriori informazioni, vedi [Rimozione delle tag dalle immagini nel tuo repository {{site.data.keyword.cloud_notm}} privato](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag).</dd>
</dl>

## 13 maggio 2019
{: #13may2019}

<dl>
  <dt>Fine del supporto per lo Scanner contenitori </dt>
  <dd>Lo Scanner contenitori è ora obsoleto e non è più utilizzabile.

  Per ulteriori informazioni, vedi [Installazione dello Scanner contenitori (obsoleto)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 2 aprile 2019
{: #2apr2019}

<dl>
  <dt>Disponibilità generale di Container Image Security Enforcement </dt>
  <dd>Utilizza Container Image Security Enforcement per verificare le tue immagini del contenitore prima di distribuirle al tuo cluster in {{site.data.keyword.containerlong_notm}}. Puoi controllare da dove vengono distribuite le immagini, applicare le politiche di Controllo vulnerabilità e garantire che l'[attendibilità dei contenuti](/docs/services/Registry?topic=registry-registry_trustedcontent) sia applicata correttamente all'immagine.

  Per ulteriori informazioni, vedi [Applicazione della sicurezza dell'immagine del contenitore](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 14 marzo 2019
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponibile per {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Utilizza il servizio {{site.data.keyword.cloudaccesstraillong_notm}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.registrylong_notm}} in {{site.data.keyword.cloud}}.

  Per ulteriori informazioni, vedi [Eventi del Programma di traccia dell'attività](/docs/services/Registry?topic=registry-at_events#at_events).
</dd>
</dl>

## 25 febbraio 2019
{: #25feb2019}

<dl>
  <dt>Nuovi nomi del dominio</dt>
  <dd>{{site.data.keyword.registrylong_notm}} utilizza dei nuovi nomi del dominio. I nuovi nomi del dominio sono disponibili nella console e nella CLI. Ora puoi utilizzare i nuovi nomi del dominio `icr.io`. I nomi del dominio `registry.bluemix.net` esistenti sono obsoleti, ma puoi continuare ad utilizzarli fino alla data di fine del supporto. Una data di fine del supporto non è ancora disponibile. Per ulteriori informazioni, vedi [Regioni](/docs/services/Registry?topic=registry-registry_overview#registry_regions) e [Introducing New IBM Cloud Container Registry Domain Names ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  Le firme si applicano al nome dell'immagine completo, il quale include il nome del dominio. Se stai utilizzando l'attendibilità dei contenuti, devi aggiungere delle nuove firme in modo da poter utilizzare l'attendibilità dei contenuti nel nuovo nome del dominio. Per ulteriori informazioni sulla firma delle immagini, vedi [Firma di immagini per contenuti attendibili](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

<dl>
  <dt>Segreti di pull della chiave API IAM per i cluster {{site.data.keyword.containerlong_notm}} </dt>
  <dd>I nuovi segreti di pull dell'immagine cluster per i domini `icr.io` vengono autorizzati utilizzando una chiave API {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM). Pertanto, se desideri avere maggior controllo riguardo l'accesso alle tue risorse {{site.data.keyword.registrylong_notm}}, puoi aggiungere delle politiche IAM. Ad esempio, puoi modificare le politiche della chiave API nel segreto di pull del cluster in modo che sia eseguito il pull delle immagini soltanto da una regione del registro o uno spazio dei nomi specifico.
  
  Per ulteriori informazioni, vedi [Descrizione di come il tuo cluster viene autorizzato ad eseguire il pull delle immagini da {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).</dd>
</dl>

<dl>
  <dt>Nuova regione in ap-north </dt>
  <dd>È disponibile una nuova regione in `ap-north`. Puoi utilizzare la nuova regione mediante il nome del dominio `jp.icr.io`.
  
  Per ulteriori informazioni, vedi [Regioni](/docs/services/Registry?topic=registry-registry_overview#registry_regions).</dd>
</dl>

## 21 febbraio 2019
{: #21feb2019}

<dl>
  <dt>Automazione dell'accesso ai tuoi spazi dei nomi </dt>
  <dd>L'utilizzo dei token per automatizzare l'esecuzione del push e del pull delle immagini Docker da e verso i tuoi spazi dei nomi è obsoleto. Ora devi utilizzare le chiavi API per automatizzare l'accesso ai tuoi spazi dei nomi {{site.data.keyword.registrylong_notm}} in modo da poter eseguire il push e il pull delle immagini.

  Per ulteriori informazioni, vedi [Automazione dell'accesso ai tuoi spazi dei nomi utilizzando le chiavi API](/docs/services/Registry?topic=registry-registry_access#registry_api_key).</dd>
</dl>

## 8 gennaio 2019
{: #8jan2019}

 <dl>
  <dt>Fine del supporto per l'API Controllo vulnerabilità versione 2 </dt>
  <dd>La versione 2 dell'API del Controllo vulnerabilità è obsoleta e non è più utilizzabile. Utilizza la versione 3 dell'API, vedi [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/container-registry/va).

  Per ulteriori informazioni, vedi [Vulnerability Advisor v2 API Deprecation ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/).</dd>
</dl>

## 4 ottobre 2018
{: #4oct2018}

<dl>
  <dt>Gestione dell'accesso utente</dt>
  <dd>Utilizza {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) per controllare l'accesso degli utenti nel tuo account a {{site.data.keyword.registrylong_notm}}. Quando le politiche IAM sono abilitate per il tuo account in {{site.data.keyword.registrylong_notm}}, ogni utente che accede al servizio nel tuo account deve avere assegnata una politica di accesso con un ruolo utente IAM definito. Questa politica determina il ruolo che l'utente ha all'interno del contesto del servizio e quali azioni può eseguire.

  Per ulteriori informazioni, vedi [Gestione dell'accesso utente con {{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam), [Definizione delle politiche del ruolo di accesso utente](/docs/services/Registry?topic=registry-user#user) e [Esercitazione: concedere l'accesso alle risorse IBM Cloud Container Registry](/docs/services/Registry?topic=registry-iam_access#iam_access).</dd>
</dl>

## 7 agosto 2018
{: #7aug2018}

<dl>
  <dt>Politiche di esenzione disponibili nel Controllo vulnerabilità </dt>
  <dd>Se vuoi gestire la sicurezza di un'organizzazione {{site.data.keyword.cloud_notm}}, puoi utilizzare la tua impostazione della politica per determinare se un problema è esente o meno. Puoi utilizzare Container Image Security Enforcement per garantire che la distribuzione sia consentita solo da immagini che non contengono alcun problema di sicurezza, una volta ignorati quelli esentati dalla tua politica.

  Per ulteriori informazioni, vedi [Impostazione delle politiche di esenzione organizzative](/docs/services/Registry?topic=va-va_index#va_managing_policy).</dd>
</dl>

## 25 luglio 2018
{: #25jul2018}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponibile per il Controllo vulnerabilità</dt>
  <dd>Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.registrylong_notm}} in {{site.data.keyword.cloud}}.

  Per ulteriori informazioni, vedi [Eventi del Programma di traccia dell'attività](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>
  
## 12 luglio 2018
{: #12jul2018}

<dl>
  <dt>API Controllo vulnerabilità versione 3 </dt>
  <dd>La versione 3 dell'API modifica il comportamento degli endpoint API utilizzati per elencare le esenzioni. Devi controllare che il tuo utilizzo dell'API non si basi sul comportamento della versione 2.

  Per ulteriori informazioni, vedi [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/container-registry/va).</dd>
</dl>

## 31 maggio 2018
{: #31may2018}

<dl>
  <dt>Utilizza Helm per le immagini Passport Advantage </dt>
  <dd>Importa il software {{site.data.keyword.IBM_notm}} scaricato da [IBM Passport Advantage Online for customers ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/passportadvantage/pao_customer.html) e impacchettato per essere utilizzato con Helm nel tuo spazio dei nomi {{site.data.keyword.registrylong_notm}}.

  Per ulteriori informazioni, vedi [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).</dd>
</dl>

## 21 marzo 2018
{: #21mar2018}

<dl>
  <dt>Scanner contenitori </dt>
  <dd>Lo Scanner contenitori abilita il Controllo vulnerabilità a segnalare gli eventuali problemi rilevati nei contenitori in esecuzione che non sono presenti nell'immagine di base del contenitore.

  Per ulteriori informazioni, vedi [Installazione dello Scanner contenitori](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 16 marzo 2018
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement beta </dt>
  <dd>Utilizza Container Image Security Enforcement beta per verificare le tue immagini del contenitore prima di distribuirle al tuo cluster in {{site.data.keyword.containerlong_notm}}. Puoi controllare da dove vengono distribuite le immagini, applicare le politiche di Controllo vulnerabilità e garantire che l'[attendibilità dei contenuti](/docs/services/Registry?topic=registry-registry_trustedcontent) sia applicata correttamente all'immagine.

  Per ulteriori informazioni, vedi [Applicazione della sicurezza dell'immagine del contenitore](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 20 febbraio 2018
{: #20feb2018}

<dl>
  <dt>Contenuti attendibili </dt>
  <dd>{{site.data.keyword.registrylong_notm}} fornisce una tecnologia di contenuti attendibili che ti permette di firmare le immagini per garantirne l'integrità nel tuo spazio dei nomi del registro. Mediante l'esecuzione del pull e del push delle immagini firmate, puoi verificare che le tue immagini siano state trasmesse dalla parte giusta, come i tuoi strumenti di integrazione continua (CI).

  Per ulteriori informazioni, vedi [Firma le immagini per i contenuti attendibili](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

## 6 novembre 2017
{: #6nov2017}

<dl>
  <dt>Registro globale</dt>
  <dd>È disponibile un registro globale. Non ha alcuna regione inclusa nel proprio nome del dominio (`icr.io`). Solo le immagini pubbliche fornite da IBM sono ospitate in questo registro.

  Per ulteriori informazioni, vedi [Registro globale](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).</dd>
</dl>

## 29 settembre 2017
{: #29sep2017}

<dl>
  <dt>Crea immagini Docker </dt>
  <dd>Il comando `ibmcloud cr build` è ora disponibile per l'esecuzione di build del contenitore. Puoi creare un'immagine Docker direttamente in {{site.data.keyword.cloud_notm}} o creare la tua propria immagine Docker sul tuo computer locale e caricarla nel tuo spazio dei nomi in {{site.data.keyword.registrylong_notm}}.

  Per ulteriori informazioni, vedi [Creazione di immagini Docker da utilizzare con il tuo spazio dei nomi](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) e [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).</dd>
</dl>

## 24 agosto 2017
{: #24aug2017}

<dl>
  <dt>Rilasciata interfaccia utente grafica </dt>
  <dd>L'interfaccia utente grafica {{site.data.keyword.registrylong_notm}} è disponibile nel catalogo, vedi [Container Registry ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/kubernetes/catalog/registry).</dd>
</dl>

## 27 giugno 2017
{: #27jun2017}

<dl>
  <dt>Disponibilità generale di {{site.data.keyword.registrylong_notm}}</dt>
  <dd>{{site.data.keyword.registrylong_notm}} è generalmente disponibile come un servizio in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.registrylong_notm}} supporta {{site.data.keyword.containerlong_notm}}.

  Per ulteriori informazioni su {{site.data.keyword.containerlong_notm}}, vedi [Esercitazione introduttiva](/docs/containers?topic=containers-getting-started).</dd>
</dl>
