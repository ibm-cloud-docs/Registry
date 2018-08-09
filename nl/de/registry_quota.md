---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Kontingente für Speicher und Pull-Datenverkehr verwalten
{: #registry_quota}

Sie können den Speicherplatz und den Pull-Datenverkehr, den Sie in Ihrem {{site.data.keyword.Bluemix}}-Konto nutzen können, begrenzen, indem Sie angepasste Kontingente festlegen und verwalten.
{:shortdesc}


## Kontingente für Speicher und Pull-Datenverkehr für Images festlegen
{: #registry_quota_set}

Sie können die Größe des Speichers und den Pull-Datenverkehr zu Ihren privaten Images begrenzen, indem Sie Ihre eigenen Kontingente festlegen.
{:shortdesc}

Bevor Sie beginnen, stellen Sie sicher, dass Sie der [Eigner oder Abrechnungsmanger für das {{site.data.keyword.Bluemix_notm}}-Konto](../../iam/users_roles.html#userroles) sind, für das das Kontingent festgelegt werden soll.

Wenn Sie ein Upgrade auf den {{site.data.keyword.registryshort_notm}}-Standardplan durchführen, profitieren Sie von unbegrenztem Speicherplatz und Pull-Datenverkehr zu Ihren privaten Images. Um ein Überziehen Ihres bevorzugten Zahlungsbetrags zu vermeiden, können Sie die einzelnen Kontingente für den Speicherplatz und Pull-Datenverkehr festlegen. Die Kontingente werden auf alle Namensbereiche angewandt, die Sie in {{site.data.keyword.registrylong_notm}} einrichten. Wenn Sie den kostenlosen Serviceplan verwenden, können Sie auch die angepassten Kontingente innerhalb Ihres kostenlosen Speicherplatzes und Pull-Datenverkehrs festlegen.

Um ein Kontingent festzulegen, gehen Sie folgendermaßen vor:

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Überprüfen Sie Ihre aktuellen Kontingente für Speicher und Pull-Datenverkehr.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Die Ausgabe ähnelt der folgenden.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

3.  Ändern Sie die Kontingente für Speicher und Pull-Datenverkehr. Um die Nutzung des Pull-Datenverkehrs zu ändern, geben Sie die Option **traffic** an und ersetzen Sie _&lt;datenverkehrkontingent&gt;_ durch den Wert in Megabyte, den Sie für das Pull-Datenverkehrkontingent festlegen möchten. Um die Speicherkapazität für Ihr Konto zu ändern, geben Sie die Option **storage** an und ersetzen Sie _&lt;speicherkontingent&gt;_ durch den Wert in Megabyte, den Sie festlegen möchten.

    Bei der Verwendung des kostenfreien Plans können Sie das Kontingent nicht über die kostenfreie Stufe hinaus erhöhen. Die kostenfreie Stufe umfasst 512 MB an Speicher und 5120 MB an Datenverkehr.
    {:tip}

    ```
    ibmcloud cr quota-set --traffic <datenverkehrskontingent> --storage <speicherkontingent>
    ```
    {: pre}

    Beispiel für das Festlegen Ihres Kontingents für den Speicher auf 600 Megabyte und für den Pull-Datenverkehr auf 7000 MB:

    ```
    ibmcloud cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}


## Kontingente und Nutzung zum Speichern und für Pull-Operationen von Images überprüfen
{: #registry_quota_get}

Sie können Ihre Kontingente und Ihren aktuell genutzten Speicher sowie die Nutzung durch Pull-Datenverkehr für Ihr Konto überprüfen.
{:shortdesc}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Überprüfen Sie Ihre aktuellen Kontingente für Speicher und Pull-Datenverkehr.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Die Ausgabe ähnelt der folgenden.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}


## Belegten Speicher freigeben und Servicepläne oder Kontingente ändern, um innerhalb der jeweiligen Kontingente zu bleiben
{: #registry_quota_freeup}

Wenn Sie Ihre Kontingente überschritten haben, die für Ihr {{site.data.keyword.Bluemix_notm}}-Konto festgelegt sind, können Sie Speicher freigeben und den Serviceplan oder die Kontingente ändern, um weiterhin Images mit Push- und Pull-Operation in und aus Ihrem Namensbereich zu übertragen.
{:shortdesc}

Gehen Sie wie folgt vor, um Speicherplatz für Images in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto freizugeben:

1.  Listen Sie alle Images in allen Ihren Namensbereichen Ihres {{site.data.keyword.Bluemix_notm}}-Kontos auf.

    ```
    ibmcloud cr images
    ```
    {: pre}

2.  Entfernen Sie ein Image aus Ihrem Namensbereich. Ersetzen Sie _&lt;imagename&gt;_ durch den Namen des Images, das Sie entfernen möchten.

    ```
    ibmcloud cr image-rm <imagename>
    ```
    {: pre}

    Je nach Größe des Images kann es einige Zeit dauern, bis das Image entfernt und der Speicher verfügbar wird.
    {:tip}

3.  Prüfen Sie die Nutzung Ihres Speicherkontingents.

    ```
    ibmcloud cr quota
    ```
    {: pre}

4. Sie können Ihren Pull-Datenverkehr nicht in einem Abrechnungszeitraum reduzieren.
   {:tip}

    Um weitere Images mit einer Pull-Operation aus Ihrem Namensbereich zu extrahieren, können Sie eine der folgenden Optionen auswählen.

    -   Warten Sie, bis der nächste Abrechnungszyklus beginnt.
    -   Wenn Sie einen kostenfreien Plan verwenden, führen Sie ein [Upgrade auf den Standard-Serviceplan](registry_overview.html#registry_plan_upgrade) durch.
    -   Wenn Sie bereits einen Standardplan verwenden, [richten Sie neue Kontingente für den Pull-Datenverkehr ein](#registry_quota_set).
