---

copyright:
  years: 2017, 2018
lastupdated: "2017-12-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Monitoraggio della vulnerabilità delle immagini
{: #registry_ui}

Puoi visualizzare informazioni sulle potenziali vulnerabilità e sulla sicurezza delle immagini nei repository pubblici e privati di {{site.data.keyword.registrylong}} utilizzando la console {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La colonna **REPORT SICUREZZA** ti mostra le seguenti informazioni sull'immagine:
-   `Sicuro` nessun problema di sicurezza trovato.
-   `Vulnerabile` sono stati trovati dei problemi di sicurezza o configurazione e devono essere risolti prima che tu possa distribuire l'immagine.
-   `Incompleto` la scansione non è completa. La scansione potrebbe essere ancora in esecuzione oppure il sistema operativo dell'immagine potrebbe non essere compatibile. Attendi e prova di nuovo a eseguire la scansione. Se la scansione non
viene ancora completata, distribuisci nuovamente l'immagine e avvia una nuova scansione. Le immagini con scansioni incomplete non vengono bloccate per la distribuzione.
-   `SO non supportato` il sistema operativo nell'immagine non è supportato.

Per visualizzare l'interfaccia utente grafica, utilizza la seguente procedura:

1.  Accedi alla console {{site.data.keyword.Bluemix_notm}} ([https://console.bluemix.net](https://console.bluemix.net)) con il tuo ID IBM.
2.  Se hai più account {{site.data.keyword.Bluemix_notm}}, seleziona l'account e la regione che desideri utilizzare dal menu dell'account.
3.  Fai clic su **Catalogo**.
4.  Seleziona la categoria **Contenitori** e fai clic sul tile **Registro contenitore**.
5.  Per visualizzare le informazioni sulle immagini nel tuo repository privato, fai clic su **Repository privati**. Viene visualizzato un elenco delle immagini nei tuoi repository privati e lo stato del report di sicurezza di ogni immagine. Per trovare ulteriori informazioni sulle vulnerabilità potenziali, inclusi il digest dell'immagine e le tag, fai clic sulla riga nella tabella.
6.  Per visualizzare le informazioni sulle immagini nei tuoi repository pubblici, fai clic su **Repository pubblici**. Viene visualizzato un elenco delle immagini nei repository pubblici con un link alla documentazione e il report di sicurezza di ogni immagine. Per trovare ulteriori informazioni sulle vulnerabilità potenziali, inclusi il digest dell'immagine e le tag, fai clic sulla riga nella tabella.

Per trovare informazioni sul significato di ogni informazione nel report di sicurezza, consulta [Gestione della sicurezza delle immagini con il Controllo vulnerabilità](../va/va_index.html).
