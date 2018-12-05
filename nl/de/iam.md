---

copyright:
  years: 2018
lastupdated: "2018-11-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Benutzerzugriff mit Identity and Access Management verwalten
{: #iam}

Der Zugriff auf {{site.data.keyword.registrylong}} für Benutzer in Ihrem Konto wird von {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) gesteuert.
{: shortdesc}

Wenn IAM-Richtlinien für Ihr Konto in {{site.data.keyword.registrylong_notm}} aktiviert sind, muss jedem Benutzer, der auf den {{site.data.keyword.registrylong_notm}}-Service in Ihrem Konto zugreift, eine Zugriffsrichtlinie mit einer definierten IAM-Benutzerrolle zugeordnet werden. Diese Richtlinie bestimmt, welche Rolle der Benutzer im Kontext des Service hat, und welche Aktionen der Benutzer ausführen kann. Jede Aktion in {{site.data.keyword.registrylong_notm}} wird einer oder mehreren [IAM-Benutzerrollen](/docs/iam/users_roles.html) zugeordnet. 

IAM-Richtlinien werden nur umgesetzt, wenn Sie mit IAM bei {{site.data.keyword.registrylong_notm}} anmelden. Wenn Sie sich mit einer anderen Methode (z. B. einem Registry-Token) bei {{site.data.keyword.registrylong_notm}} anmelden, werden Ihre Richtlinien nicht umgesetzt. Wenn Sie den Zugriff auf einen oder mehrere Namensbereiche für eine ID beschränken möchten, die bei der Automatisierung verwendet wird, sollten Sie die Verwendung einer IAM-Service-ID anstelle eines Registry-Tokens in Betracht ziehen. Weitere Informationen zu Service-IDs finden Sie unter [Service-IDs erstellen und damit arbeiten](/docs/iam/serviceid.html#serviceids). 

Weitere Informationen zu IAM finden Sie unter [IBM Cloud - Zugriff und Verwaltung](/docs/iam/index.html#iamoverview). 

Informationen zum Aktivieren von Richtlinien für {{site.data.keyword.registrylong_notm}} finden Sie unter [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry/registry_users.html#user). 

Mit Richtlinien können Sie Zugriff auf unterschiedlichen Ebenen gewähren. Zu den Optionen gehören unter anderem die folgenden Zugriffsebenen: 

* Zugriff auf den Service in Ihrem Konto
* Zugriff auf eine spezifische Ressource innerhalb des Service
* Zugriff auf alle IAM-fähigen Services in Ihrem Konto

Nachdem Sie den Bereich der Zugriffsrichtlinie definiert haben, können Sie eine Rolle zuordnen. Sehen Sie sich die folgenden Tabellen an, in denen beschrieben ist, welche Aktionen die einzelnen Rollen innerhalb des {{site.data.keyword.registrylong_notm}}-Service zulassen. 

Informationen zum Verwalten von Benutzerrollen finden Sie unter [Mit Benutzern arbeiten](/docs/iam/iamusermanage.html#iamusermanage). 

Informationen zum Zuordnen von Benutzerrollen in der Benutzerschnittstelle finden Sie unter [IAM-Zugriff verwalten](/docs/iam/mngiam.html#iammanidaccser). 

Testen Sie das Lernprogramm [Lernprogramm: Zugriff auf {{site.data.keyword.registrylong_notm}}-Ressourcen gewähren](/docs/services/Registry/registry_tutorial_configure_iam.html#iam_access).
{: tip}

## Plattformmanagementrollen
{: #platform_management_roles}

In der folgenden Tabelle sind die Aktionen, die Plattformmanagementrollen zugeordnet sind, im Detail aufgeführt. Plattformmanagementrollen ermöglichen es Benutzern, Tasks für Serviceressourcen auf Plattformebene auszuführen, z. B. Benutzerzugriff für den Service zuordnen oder Service-IDs erstellen oder löschen. 

| Plattformmanagementrolle | Beschreibung der Aktionen | Beispielaktionen |
|:-----------------|:-----------------|:-----------------|
| Anzeigeberechtigter | Nicht unterstützt | |
| Editor | Nicht unterstützt | |
| Operator | Nicht unterstützt | |
| Administrator | <ul><li>Zugriff für andere Benutzer konfigurieren</li><li> Registry-Tokens konfigurieren</li><li>Cluster erstellen</li></ul> | <ul><li>Informationen zum Zuordnen von Benutzerrollen in der Benutzerschnittstelle finden Sie unter [IAM-Zugriff verwalten](/docs/iam/mngiam.html#iammanidaccser). </li><li>Registry-Tokens hinzufügen, auflisten, abrufen und entfernen</li><li>Zum Erstellen von Clustern in {{site.data.keyword.containerlong_notm}} müssen Sie dem Benutzer die Administratorrolle für {{site.data.keyword.registrylong_notm}} zuordnen. Siehe [Erstellen von Clustern vorbereiten](/docs/containers/cs_clusters.html#cluster_prepare). </ul> |
{: caption="Tabelle 1. IAM-Benutzerrollen und Aktionen" caption-side="top"}

Für {{site.data.keyword.registrylong_notm}} sind die folgenden Aktionen vorhanden: 

| Aktion| Operation für Service | Rolle
|:-----------------|:-----------------|:--------------|
| `container-registry.registrytoken.create` | [`ibmcloud cr token-add`](/docs/services/Registry/registry_cli.html#bx_cr_token_add) Hinzufügen eines Tokens zum Steuern des Zugriffs auf eine Registry. | Administrator |
| `container-registry.registrytoken.delete` | [`ibmcloud cr token-rm`](/docs/services/Registry/registry_cli.html#bx_cr_token_rm) Entfernen eines oder mehrerer angegebener Tokens. | Administrator |
| `container-registry.registrytoken.get` | [`ibmcloud cr token-get`](/docs/services/Registry/registry_cli.html#bx_cr_token_get) Abrufen des angegebenen Tokens aus der Registry. | Administrator |
| `container-registry.registrytoken.list` | [`ibmcloud cr token-list`](/docs/services/Registry/registry_cli.html#bx_cr_token_list) Anzeigen aller Tokens, die für Ihr {{site.data.keyword.Bluemix_notm}}-Konto vorhanden sind. | Administrator |
{: caption="Tabelle 2. Plattformaktionen und -operationen für die Konfiguration von {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Servicezugriffsrollen
{: #service_access_roles}

In der folgenden Tabelle sind die Aktionen, die Servicezugriffsrollen zugeordnet sind, im Detail aufgeführt. Servicezugriffsrollen ermöglichen es Benutzern, auf {{site.data.keyword.registrylong_notm}} zuzugreifen und die {{site.data.keyword.registrylong_notm}}-API aufzurufen. 

| Servicezugriffsrolle | Beschreibung der Aktionen | Beispielaktionen |
|:-----------------|:-----------------|:-----------------|
| Leseberechtigter | Die Rolle 'Leseberechtigter' kann Informationen anzeigen. | <ul><li>Images anzeigen, überprüfen und extrahieren</li><li>Namensbereiche anzeigen</li><li>Kontingente anzeigen</li><li>Sicherheitslückenberichte anzeigen</li><li>Imagesignaturen anzeigen</li></ul>|
| Schreibberechtigter | Die Rolle 'Schreibberechtigter' kann Informationen bearbeiten. |<ul><li>Images erstellen, mit Push-Operation übertragen und löschen</li><li>Kontingente anzeigen</li><li>Images signieren</li><li>Namensbereiche hinzufügen und entfernen</li></ul> |
| Manager | Die Rolle 'Manager' kann alle Aktionen ausführen. | <ul><li>Images anzeigen, extrahieren, erstellen, mit Push-Operation übertragen und löschen</li><li>Namensbereiche anzeigen, hinzufügen und entfernen</li><li>Kontingente anzeigen und festlegen</li><li>Sicherheitslückenberichte anzeigen</li><li>Imagesignaturen anzeigen und erstellen</li><li>Preisstrukturpläne überprüfen und ändern</li><li>IAM-Richtliniendurchsetzung aktivieren</li><li>Vulnerability Advisor-Ausnahmen verwalten</li></ul> |
{: caption="Tabelle 3. IAM-Servicezugriffsrollen und Aktionen" caption-side="top"}

 Für die folgenden {{site.data.keyword.registrylong_notm}}-Befehle muss Ihnen mindestens eine der angegebenen Rollen zugeordnet sein, wie in der folgenden Tabellen dargestellt. Zum Erstellen einer Richtlinie für den Zugriff auf {{site.data.keyword.registrylong_notm}}, müssen Sie eine Richtlinie erstellen, bei der der Servicename `container-registry` lautet, die Serviceinstanz leer ist und als Region die Region angegeben ist, für die Sie Zugriff erteilen möchten, bzw. bei der keine Region angegeben ist, um Zugriff auf alle Regionen zu erteilen. 

### Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}
{: #access_roles_configure}

Um einem Benutzer die Berechtigung zum Konfigurieren von {{site.data.keyword.registrylong_notm}} in Ihrem Account zu erteilen, müssen Sie eine Richtlinie erstellen, die eine oder mehrere der Rollen in der folgenden Tabelle zuordnet. Beim Erstellen Ihrer Richtlinie dürfen Sie keinen Ressourcentyp (`resource-type`) bzw. keine Ressource (`resource`) angeben. 

**Beispiel**

```
bx iam user-policy-create <benutzer-e-mail> --service-name container-registry --region <us-south> --roles <Manager>
```
{: pre}

| Aktion| Operation für Service | Rolle
|:-----------------|:-----------------|:--------------|
| `container-registry.auth.set` | [`ibmcloud cr iam-policies-enable`](/docs/services/Registry/registry_cli.html#bx_cr_iam_policies_enable) IAM-Richtliniendurchsetzung aktivieren. | Manager |
| `container-registry.exemption.manager` | <ul><li>[`ibmcloud cr exemption-add`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_add) Freistellung für ein Sicherheitsproblem erstellen. </li><li>[`ibmcloud cr exemption-list`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_list) Freistellungen für Sicherheitsprobleme auflisten. </li><li>[`ibmcloud cr exemption-rm`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_rm) Freistellung für ein Sicherheitsproblem löschen. </li><li>[`ibmcloud cr exemption-types`](/docs/services/Registry/registry_cli.html#bx_cr_exemption_types) Typen der Sicherheitsprobleme auflisten, die Sie freistellen können. </li></ul> | Manager |
| `container-registry.plan.get` | [`ibmcloud cr plan`](/docs/services/Registry/registry_cli.html#bx_cr_plan) Preisstrukturplan anzeigen. | Manager |
| `container-registry.plan.set` | [`ibmcloud cr plan-upgrade`](/docs/services/Registry/registry_cli.html#bx_cr_plan_upgrade) Upgrade auf den Standardplan durchführen. | Manager |
| `container-registry.quota.get` | [`ibmcloud cr quota`](/docs/services/Registry/registry_cli.html#bx_cr_quota) Ihre aktuellen Kontingente für Datenverkehr und Speicher sowie Informationen zu diesen Kontingenten anzeigen. | Leseberechtigter, Schreibberechtigter, Manager |
| `container-registry.quota.set` | [`ibmcloud cr quota-set`](/docs/services/Registry/registry_cli.html#bx_cr_quota_set) Angegebene Kontingente ändern. | Manager |
{: caption="Tabelle 4. Serviceaktionen und -operationen für die Konfiguration von {{site.data.keyword.registrylong_notm}}" caption-side="top"}

### Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}
{: #access_roles_using}

Um einem Benutzer die Berechtigung zum Zugriff auf {{site.data.keyword.registrylong_notm}}-Inhalte in Ihrem Account zu erteilen, müssen Sie eine Richtlinie erstellen, die eine oder mehrere der Rollen in der folgenden Tabelle zuordnet. Beim Erstellen Ihrer Richtlinie können Sie den Zugriff auf einen bestimmten Namensbereich einschränken, indem Sie den Ressourcentyp `namespace` und den Namen des Namensbereichs als Ressource angeben. Wenn Sie keinen Ressourcentyp (`resource-type`) und keine Ressource (`resource`) angeben, erteilt die Richtlinie Zugriff auf alle Ressourcen in dem Konto. 

**Beispiel**

```
bx iam user-policy-create <benutzer-e-mail> --service-name container-registry --region <us-south> --roles <Leseberechtigter> [--resource-type namespace --resource <name_von_namensbereich>]
```
{: pre}

| Aktion | Operation für Service | Rolle
|:-----------------|:-----------------|:--------------|
| `container-registry.image.build` | [`ibmcloud cr build`](/docs/services/Registry/registry_cli.html#bx_cr_build) Container-Image erstellen. | Schreibberechtigter, Manager |
| `container-registry.image.delete` | [`ibmcloud cr image-rm`](/docs/services/Registry/registry_cli.html#bx_cr_image_rm) Ein Image oder mehrere Images löschen. | Schreibberechtigter, Manager |
| `container-registry.image.inspect` | [`ibmcloud cr image-inspect`](/docs/services/Registry/registry_cli.html#bx_cr_image_inspect) Details zu einem bestimmten Image anzeigen. | Leseberechtigter, Manager |
| `container-registry.image.list` | [`ibmcloud cr image-list`](/docs/services/Registry/registry_cli.html#bx_cr_image_list) Container-Images auflisten. | Leseberechtigter, Manager |
| `container-registry.image.pull` | `docker pull` Image extrahieren. | Leseberechtigter, Schreibberechtigter, Manager |
| `container-registry.image.push` | <ul><li>`docker push` Image mit Push-Operation übertragen. </li><li>[`ibmcloud cr ppa-archive-load`](/docs/services/Registry/registry_cli.html#bx_cr_ppa_archive_load) Importiert IBM Software, die von [IBM Passport Advantage Online für Kunden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/pao_customer.html) heruntergeladen und für die Verwendung mit Helm paketiert wurde, in den Namensbereich Ihrer privaten Registry. </li></ul> | Schreibberechtigter, Manager |
| `container-registry.image.vulnerabilities` | [`ibmcloud cr vulnerability-assessment`](/docs/services/Registry/registry_cli.html#bx_cr_va) Schwachstellenanalysebericht für Ihr Image anzeigen. | Leseberechtigter, Manager |
| `container-registry.namespace.create` | [`ibmcloud cr namespace-add`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_add) Namensbereich hinzufügen. | Schreibberechtigter, Manager |
| `container-registry.namespace.delete` | [`ibmcloud cr namespace-rm`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_rm) Namensbereich entfernen. | Schreibberechtigter, Manager |
| `container-registry.namespace.list` | [`ibmcloud cr namespace-list`](/docs/services/Registry/registry_cli.html#bx_cr_namespace_list) Namensbereiche anzeigen. | Leseberechtigter, Manager |
| `container-registry.signature.create` | `docker trust sign` Image signieren. | Schreibberechtigter, Manager |
| `container-registry.signature.delete` | `docker trust revoke` Signatur löschen. | Schreibberechtigter, Manager |
| `container-registry.signature.get` | `docker trust inspect` Signatur überprüfen. | Leseberechtigter, Manager |
{: caption="Tabelle 5. Serviceaktionen und -operationen für die Verwendung von {{site.data.keyword.registrylong_notm}}" caption-side="top"}
