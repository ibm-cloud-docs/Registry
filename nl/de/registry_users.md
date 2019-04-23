---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-27"

keywords: IBM Cloud Container Registry, user access role policies, access policies, policies, policy enforcement,

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

# Richtlinien für Benutzerzugriffsrollen definieren
{: #user access}

Als Administrator können Sie Zugriffsrichtlinien für Ihre Registry definieren, um unterschiedliche Zugriffsebenen für verschiedene Benutzer zu erstellen. Sie können beispielsweise bestimmten Benutzern die Berechtigung zum Festlegen von Kontingenten erteilen, während andere Benutzer Kontingente nur anzeigen können.
{: shortdesc}

Sie müssen Zugriffsrichtlinien für jeden Benutzer definieren, der mit {{site.data.keyword.registrylong}} arbeitet. Der Bereich einer Zugriffsrichtlinie basiert auf der definierten Rolle bzw. den definierten Rollen eines Benutzers, die bestimmen, welche Aktionen er ausführen darf. Einige Richtlinien sind vordefiniert, andere können jedoch angepasst werden.

Wenn Sie mit der Verwendung von {{site.data.keyword.registrylong_notm}} vor dem 4. Oktober 2018 begonnen haben, müssen Sie die Richtliniendurchsetzung aktivieren, bevor Ihre Richtlinien Wirkung zeigen können. Siehe [Richtliniendurchsetzung für vorhandene Benutzer aktivieren](#existing_users).
{: tip}

Weitere Informationen zu Richtlinien für Zugriffsrollen in {{site.data.keyword.iamlong}} (IAM) finden Sie unter [{{site.data.keyword.iamshort}}](/docs/iam?topic=iam-iamoverview#iamoverview).

## Richtlinien erstellen
{: #create}

Wenn Sie den Zugriff auf Ressourcen steuern möchten, müssen Sie Benutzern oder Service-IDs Rollen zuweisen. Der Zugriff auf {{site.data.keyword.registrylong_notm}}-Ressourcen kann der Namensbereichsressource nach Name oder dem gesamten Service, d. h. allen Namensbereichen im Konto, erteilt werden.

Wenn Sie Zugriff auf alles erteilen möchten, geben Sie keinen Ressourcentyp bzw. keine Ressource an. Wenn Sie Zugriff auf einen bestimmten Namensbereich erteilen möchten, geben Sie den Ressourcentyp als `namespace` an und verwenden Sie den Namen des Namensbereichs als Ressource.

Eine Organisation und Zuweisung von Zugriff zu Registry-Namensbereichen in Ressourcengruppen ist nicht möglich.
{: note}

**Vorbereitung**

- Entscheiden Sie, welche Rollen die einzelnen Benutzer benötigen und für welche Ressourcen in {{site.data.keyword.registrylong_notm}} sie diese benötigen. Siehe [IAM-Rollen](/docs/services/Registry?topic=registry-iam#iam). Bedenken Sie, dass Sie mehrere Richtlinien erstellen können. Sie können beispielsweise Schreibzugriff für eine Ressource erteilen, für eine andere Ressource nur Lesezugriff, und für eine dritte Ressource gar keinen Zugriff. Richtlinien sind additiv, d. h. dass mit einer globalen Leserichtlinie und einer ressourcenbezogenen Schreibrichtlinie sowohl Lese- als auch Schreibzugriff für eine bestimmte Ressource erteilt wird.

- [Laden Sie Benutzer ein und weisen Sie Zugriffsberechtigungen zu](/docs/iam?topic=iam-iamuserinv#iamuserinv).

  Wenn Benutzer in der Lage sein sollen, Cluster in {{site.data.keyword.containerlong_notm}} zu erstellen, müssen Sie sicherstellen, dass Sie diesen Benutzern die {{site.data.keyword.registrylong_notm}}-Rolle 'Administrator' und keine Ressourcengruppe zuweisen. Siehe [Erstellen von Clustern vorbereiten](/docs/containers?topic=containers-clusters#cluster_prepare).
  {: tip}

Um Richtlinien für {{site.data.keyword.registrylong_notm}} zu erstellen, muss das Feld mit dem Servicenamen `container-registry` lauten.

- Informationen zum Erstellen einer Richtlinie für Benutzer finden Sie unter [Zugriff auf Ressourcen verwalten](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).
- Zum Erstellen einer Richtlinie für Service-IDs führen Sie den Befehl `ibmcloud iam service-policy-create` aus oder verwenden die GUI, um Rollen an Ihre Service-IDs zu binden. Zum Erstellen von Richtlinien müssen Sie die Rolle 'Administrator' innehaben. In Ihrem eigenen Konto haben Sie automatisch die Rolle 'Administrator'. Weitere Informationen finden Sie in [Service-IDs erstellen und damit arbeiten](/docs/iam?topic=iam-serviceids#serviceids) und [Service-ID-Zugriffsrichtlinien verwalten](/docs/iam?topic=iam-serviceidpolicy#serviceidpolicy).

## Richtliniendurchsetzung für vorhandene Benutzer aktivieren
{: #existing_users}

Für Benutzer, die nach dem 4. Oktober 2018 bereitgestellt werden, sind IAM-Richtlinien standardmäßig aktiviert. Für Benutzer, die vor dem 4. Oktober 2018 bereitgestellt wurden, müssen Sie, nachdem Sie Ihre Richtlinien erstellt haben, die Richtliniendurchsetzung aktivieren, damit Ihre Richtlinien wirksam werden.

1. [Erstellen Sie Richtlinien](#create) für Ihre Benutzer und Service-IDs.

2. Zum Aktivieren der Richtliniendurchsetzung führen Sie den Befehl [`ibmcloud cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) aus.

    Sie müssen für das Konto die Rolle 'Manager' innehaben, um den Befehl `ibmcloud cr iam-policies-enable` ausführen zu können. In Ihrem eigenen Konto haben Sie automatisch die Rolle 'Manager'.
    {: tip}

3. Führen Sie den Befehl [`ibmcloud cr iam-policies-status`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_status) aus, um sicherzustellen, dass die IAM-Richtlinien aktiviert sind.
