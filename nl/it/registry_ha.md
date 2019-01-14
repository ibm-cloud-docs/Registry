---

copyright:
  years: 2018
lastupdated: "2018-09-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# Alta disponibilità e ripristino di emergenza
{: #ha-dr}

Il servizio {{site.data.keyword.registrylong}} è un servizio regionale altamente disponibile.
{:shortdesc}

* In ogni regione supportata, viene bilanciato il carico del traffico nell'infrastruttura del registro in più zone di disponibilità, senza alcun singolo punto di errore.

* Viene regolarmente eseguito il backup dei dati archiviati in {{site.data.keyword.registrylong_notm}}, fornendo ulteriore resilienza.

* Se sei preoccupato per la disponibilità della tua immagine nel caso in cui un'intera regione non sia disponibile, puoi scegliere di passare le tue immagini a più registri regionali. 
  
  Potresti anche scegliere di passare le tue immagini a più registri nel caso elimini o sovrascrivi accidentalmente le tue immagini.

  Per ulteriori informazioni sulle regioni, vedi [Regioni](/docs/services/Registry/registry_overview.html#registry_regions).
