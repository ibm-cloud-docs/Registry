---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Sicherheit des Container-Image durchsetzen (Beta)
{: #security_enforce}

Mit Container Image Security Enforcement (Beta) können Sie Ihre Container-Images überprüfen, bevor Sie sie in Ihrem Cluster in {{site.data.keyword.containerlong}} bereitstellen. Sie können steuern, von wo aus Images bereitgestellt werden, Vulnerability Advisor-Richtlinien durchsetzen und sicherstellen, dass [content trust](registry_trusted_content.html) korrekt auf das Image angewendet wird. Wenn ein Image Ihre Richtlinienanforderungen nicht erfüllt, wird die Pod-Datei nicht in Ihrem Cluster implementiert oder aktualisiert.
{:shortdesc}

Container Image Security Enforcement ruft die Informationen zu Content Trust für Images und zu Sicherheitslücken von {{site.data.keyword.registrylong}} ab. Sie können die Bereitstellung von Images, die in anderen Registrys gespeichert sind, blockieren oder zulassen. Für diese Images können Sie jedoch nicht die Prüfung auf Sicherheitslücken oder Durchsetzung der Vertrauensbeziehung verwenden.

## Container Image Security Enforcement in Ihrem Cluster
{: #sec_enforce_install}

**Vorbereitung**

* [Erstellen](/docs/containers/cs_clusters.html#clusters_ui) oder [aktualisieren](/docs/containers/cs_cluster_update.html#update) Sie den Cluster, den Sie mit **Kubernetes Version 1.9 oder höher** verwenden möchten.
* [Wählen Sie Ihre `kubectl`-CLI](/docs/containers/cs_cli_install.html#cs_cli_configure) als Ziel für den Cluster aus.

Führen Sie die folgenden Schritte aus:

1. [Richten Sie Helm in Ihrem Cluster ein](/docs/containers/cs_integrations.html#helm).

2. Fügen Sie das IBM Chart-Repository zu Ihrem Helm-Client hinzu.

   ```
   helm repo add ibm https://registry.bluemix.net/helm/ibm
   ```
   {: pre}

3. Installieren Sie das Helm-Diagramm für Container Image Security Enforcement in Ihrem Cluster. Geben Sie ihm einen Namen wie `cise`.

   ```
   helm install --name cise ibm/ibmcloud-image-enforcement
   ```
   {: pre}

Container Image Security Enforcement ist jetzt installiert und wendet die [Standardsicherheitsrichtlinie](#default_policies) auf alle Kubernetes-Namensbereiche in Ihrem Cluster an. Informationen zur Anpassung der Sicherheitsrichtlinie für Kubernetes-Namensbereiche in Ihrem Cluster oder den Cluster insgesamt finden Sie unter [Richtlinien anpassen](#customize_policies).

## Standardrichtlinien
{: #default_policies}

Container Image Security Enforcement installiert einige Richtlinien standardmäßig, um Ihnen einen Ausgangspunkt für das Erstellen Ihrer Sicherheitsrichtlinie zu geben.
{:shortdesc}

Diese Richtlinien können Sie mit einer der folgenden Optionen überschreiben:

* Schreiben Sie ein neues Richtliniendokument und wenden Sie es mit dem Befehl `kubectl apply` auf Ihren Cluster an.
* Bearbeiten Sie die Standardrichtlinie mit dem Befehl `kubectl edit`.

Weitere Informationen zum Schreiben von Sicherheitsrichtlinien finden Sie unter [Richtlinien anpassen](#customize_policies).

### Clusterweite Richtlinie
{: #cluster-wide}

Standardmäßig erzwingt eine clusterweite Richtlinie, dass alle Images in allen Registrys über vertrauenswürdige Inhalte verfügen und dass Vulnerability Advisor für sie keine Sicherheitslücken berichtet.
{:shortdesc}

**Standardmäßige clusterweite `.yaml`-Richtliniendatei**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ClusterImagePolicy
metadata:
  name: ibmcloud-default-cluster-image-policy
spec:
   repositories:
    # Setzt durch, dass alle in diesem Cluster bereitgestellten Images die Prüfung der Vertrauenswürdigkeit und VA bestehen
    # Zum Überschreiben eine Image-Richtlinie für einen bestimmten Kubernetes-Namensbereich festlegen oder diese Richtlinie ändern
    - name: "*"
      policy:
        trust:
          enabled: true
        va:
          enabled: true
```
{: codeblock}

Wenn Sie `va` oder `trust` auf `enabled: true` für eine andere Container-Registry als {{site.data.keyword.registrylong_notm}} festlegen, wird jeder Versuch, Pods aus Images in dieser Registry bereitzustellen, abgelehnt. Wenn Sie Images aus anderen Registrys bereitstellen möchten, entfernen Sie die Richtlinien `va` und `trust`.
{:tip}

### Kube-Systemrichtlinie
{: #kube-system}

Standardmäßig ist für den `kube-system`-Namensbereich eine namensbereichsweite Richtlinie installiert. Mit dieser Richtlinie können alle Images aus einer beliebigen Container-Registry ohne Durchsetzung im `kube-system` bereitgestellt werden; diesen Teil der Richtlinie können Sie jedoch ändern. Die Standardrichtlinie umfasst auch bestimmte Repositorys, die Sie an ihrer Position belassen müssen, damit der Cluster ordnungsgemäß konfiguriert wird.
{:shortdesc}

**Standardmäßige `.yaml`-Richtliniendatei für `kube-system`**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: kube-system
spec:
   repositories:
    # Mit dieser Richtlinie können alle Images in diesem Namensbereich bereitgestellt werden. Diese Richtlinie verhindert Beschädigungen von eventuell vorhandenen Anwendungen anderer Anbieter in diesem Namensbereich.
    # WICHTIG: Diese Richtlinie überprüfen und durch eine ersetzen, die Ihre Anforderungen erfüllt. Wenn Sie in diesem Namensbereich keine Anwendungen von anderen Anbietern ausführen, können Sie diese Richtlinie ganz entfernen.
    - name: "*"
      policy:
    # Diese Richtlinien lassen die Bereitstellung aller IBM Cloud Kubernetes Service-Images aus der globalen und allen regionalen Registrys in diesem Namensbereich zu.
    # WICHTIG: Wenn Sie in diesem Namensbereich Ihre eigene Richtlinie erstellen, achten Sie darauf, diese Repositorys einzubeziehen. Wenn Sie dies nicht tun, funktioniert der Cluster u. U. nicht ordnungsgemäß.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```
{: codeblock}

### Richtlinie für IBM-system
{: #ibm-system}

Standardmäßig ist für den `ibm-system`-Namensbereich eine namensbereichsweite Richtlinie installiert. Mit dieser Richtlinie können alle Images aus einer beliebigen Container-Registry ohne Durchsetzung im `ibm-system` bereitgestellt werden; diesen Teil der Richtlinie können Sie jedoch ändern. Die Standardrichtlinie umfasst auch bestimmte Repositorys, die Sie an ihrer Position belassen müssen, damit der Cluster ordnungsgemäß konfiguriert wird und Sie Container Image Security Enforcement installieren oder konfigurieren können.
{:shortdesc}

**Standardmäßige `.yaml`-Richtliniendatei für `ibm-system`**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: ibm-system
spec:
   repositories:
    # Mit dieser Richtlinie können alle Images in diesem Namensbereich bereitgestellt werden. Diese Richtlinie verhindert Beschädigungen von eventuell vorhandenen Anwendungen anderer Anbieter in diesem Namensbereich.
    # WICHTIG: Diese Richtlinie überprüfen und durch eine ersetzen, die Ihre Anforderungen erfüllt. Wenn Sie in diesem Namensbereich keine Anwendungen von anderen Anbietern ausführen, können Sie diese Richtlinie ganz entfernen.
    - name: "*"
      policy:
    # Diese Richtlinien lassen die Bereitstellung aller IBM Cloud Kubernetes Service-Images aus der globalen und allen regionalen Registrys in diesem Namensbereich zu.
    # WICHTIG: Wenn Sie in diesem Namensbereich Ihre eigene Richtlinie erstellen, achten Sie darauf, diese Repositorys einzubeziehen. Wenn Sie dies nicht tun, funktioniert der Cluster u. U. nicht ordnungsgemäß.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
    # Diese Richtlinie hindert Container Image Security Enforcement daran, sich selbst zu blockieren
    - name: "registry*.bluemix.net/ibm/ibmcloud-image-enforcement"
      policy:
    # Diese Richtlinie lässt zu, dass Container Image Security Enforcement für die Konfiguration Ihres Clusters Hyperkube verwendet. Diese Richtlinie muss vorhanden sein, wenn Container Image Security Enforcement deinstalliert wird.
    - name: quay.io/coreos/hyperkube
      policies:
```
{: codeblock}

## Richtlinien anpassen
{: #customize_policies}

Sie können die Richtlinie, mit der Container Image Security Enforcement Images erlaubt, entweder auf Clusterebene oder auf Ebene des Kubernetes-Namensbereichs ändern. In der Richtlinie können Sie verschiedene Durchsetzungsregeln für unterschiedliche Images angeben.
{:shortdesc}

Es muss eine Richtlinie festgelegt sein. Andernfalls schlagen Bereitstellungen auf Ihrem Cluster fehl. Wenn keine Sicherheitsrichtlinien für Images durchgesetzt werden sollen, [entfernen Sie Container Image Security Enforcement](#remove).
{:tip}

Wenn Sie eine Bereitstellung anwenden, prüft Container Image Security Enforcement, ob der Kubernetes-Namensbereich, den Sie bereitstellen, eine anzuwendende Richtlinie besitzt. Ist dies nicht der Fall, verwendet Container Image Security Enforcement die clusterweite Richtlinie. Ihre Bereitstellung wird verweigert, wenn kein Namensbereich und keine clusterweite Richtlinie existieren.

Bevor Sie anfangen, [wählen Sie Ihre `kubectl`-CLI](/docs/containers/cs_cli_install.html#cs_cli_configure) als Ziel für den Cluster aus. Führen Sie die dann folgenden Schritte aus: 

1. Erstellen Sie eine `.yaml`-Datei für die Definition einer angepassten <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">Kubernetes-Ressource <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

    ```yaml
    apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
    kind: <ClusterImagePolicy_or_ImagePolicy>
    metadata:
      name: <crd_name>
    spec:
       repositories:
        - name: <repository_name>
          policy:
            trust:
              enabled: <true_or_false>
              signerSecrets:
              - name: <secret_name>
            va:
              enabled: <true_or_false>
    ```
    {: codeblock}

    <table>
    <caption>Tabelle 1. Informationen zu YAML-Komponenten</caption>
    <thead>
    <th>Feld</th>
    <th>Beschreibung</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>Für eine clusterweite Richtlinie geben Sie `kind` mit `ClusterImagePolicy` an. Für eine Kubernetes-Namensbereichsrichtlinie geben Sie `ImagePolicy` an.</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>Benennen Sie die angepasste Ressourcendefinition.</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>Geben Sie die Repositorys an, aus denen Images zugelassen werden sollen. Platzhalter (`*`) sind in Repository-Namen zulässig. Repositorys werden verweigert, sofern sie nicht von einem entsprechenden Eintrag in `repositories` zugelassen oder einer weiteren Prüfung unterzogen werden. Eine leere Liste `repositories` blockiert die Bereitstellung aller Images. Um alle Images ohne Verifizierung von Richtlinien zuzulassen, legen Sie den Namen auf `*` fest und lassen Sie die Teilbereiche der Richtlinie aus.</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>Füllen Sie die Teilbereiche für die Durchsetzung von `trust` und `va` aus. Wenn Sie die Teilbereiche der Richtlinie auslassen, ist dies äquivalent zu der Angabe `enabled: false` für jeden dieser Abschnitte.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>Legen Sie dies mit `true` fest, um die Bereitstellung nur von Images zuzulassen, die [für Content Trust signiert](registry_trusted_content.html) sind. Legen Sie `false` fest, um zu ignorieren, ob Images signiert sind.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>Wenn Sie nur Images zulassen möchten, die von bestimmten Benutzern signiert wurden, geben Sie den geheimen Kubernetes-Schlüssel mit dem Unterzeichnernamen an. Lassen Sie diesen Abschnitt aus oder lassen Sie ihn leer, um zu verifizieren, ob Images signiert sind, ohne bestimmte Unterzeichner durchzusetzen. Weitere Informationen finden Sie unter [Unterzeichner für vertrauenswürdige Inhalte in angepassten Richtlinien angeben](#signers).</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>Legen Sie dies mit `true` fest, um nur Images zuzulassen, die die [Vulnerability Advisor](/docs/services/va/va_index.html)-Prüfung bestehen. Legen Sie `false` fest, um die Vulnerability Advisor-Prüfung zu ignorieren.</td>
    </tr>
    </tbody>
    </table>

2. Wenden Sie die `.yaml`-Datei auf Ihren Cluster an.

   ```
   kubectl apply -f <filepath>
   ```
   {: pre}

### Unterzeichner für vertrauenswürdige Inhalte in angepassten Richtlinien angeben
{: #signers}

Wenn Sie Content Trust verwenden, können Sie überprüfen, ob Images von bestimmten Unterzeichnern signiert wurden. Die Bereitstellung ist nur dann zulässig, wenn die neueste signierte Version von allen aufgelisteten Unterzeichnern signiert wurde. Anweisungen zum Hinzufügen eines Unterzeichners zu einem Repository finden Sie unter [Vertrauenswürdige Unterzeichner verwalten](registry_trusted_content.html#trustedcontent_signers).
{:shortdesc}

Gehen Sie folgendermaßen vor, um die Richtlinie so zu konfigurieren, dass sie überprüft, ob ein Image von einem bestimmten Unterzeichner signiert wurde:

1. Rufen Sie den Unterzeichnernamen (der Name, der in `docker trust signer add` verwendet wurde) und den öffentlichen Schlüssel des Unterzeichners ab.
2. Generieren Sie einen geheimen Kubernetes-Schlüssel mit dem Namen und dem öffentlichen Schlüssel des Unterzeichners.

   ```
   kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
   ```
   {: pre}

3. Fügen Sie den geheimen Schlüssel zur Liste `signerSecrets` für das Repository in Ihrer Richtlinie hinzu.

   ```yaml
   - name: example
     policy:
       trust:
         enabled: true
         signerSecrets:
         - name: <secret_name>
   ```
   {: codeblock}

## Steuern, wer Richtlinien anpassen darf
{: #assign_user_policy}

Wenn in Ihrem Kubernetes-Cluster die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) aktiviert ist, können Sie eine Rolle erstellen, die regelt, wer Sicherheitsrichtlinien in Ihrem Cluster verwalten kann. Weitere Informationen zur Anwendung von RBAC-Regeln auf Ihren Cluster finden Sie in der [Dokumentation zu {{site.data.keyword.containerlong_notm}}](/docs/containers/cs_users.html#rbac).
{:shortdesc}

Fügen Sie in Ihrer Rolle eine Regel für Sicherheitsrichtlinien hinzu:

```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```
{: codeblock}

Sie können mehrere Rollen erstellen, um zu steuern, welche Aktionen ein Benutzer ausführen kann. Zum Beispiel können Sie `verbs` so ändern, dass einige Benutzer nur die Richtlinien `get` oder `list` verwenden können. Alternativ können Sie `clusterimagepolicies` aus der Liste `resources` auslassen, um nur auf Kubernetes-Namensbereichsrichtlinien Zugriff zu erteilen.
{:tip}

Benutzer mit Zugriff für das Löschen angepasster Ressourcendefinitionen (Custom Resource Definitions, CRDs) können die Ressourcendefinition für Sicherheitsrichtlinien löschen, womit auch Ihre Sicherheitsrichtlinien gelöscht werden. Achten Sie darauf, festzulegen, wer CRDs löschen darf. Um Zugriff für das Löschen von CRDs zu erteilen, fügen Sie eine Regel hinzu:

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```
{: codeblock}

Benutzer und Servicekonten mit der Rolle `cluster-admin` haben Zugriff auf alle Ressourcen. Die Cluster-Administratorrolle gewährt Zugriff für die Verwaltung der Sicherheitsrichtlinie, selbst wenn Sie die Rolle nicht bearbeiten. Achten Sie darauf, festzulegen, wer die Rolle `cluster-admin` besitzt, und erteilen Sie nur solchen Personen Zugriff, denen das Ändern von Sicherheitsrichtlinien erlaubt sein soll.
{:tip}

## Container-Image mit erzwungener Sicherheit bereitstellen
{: #deploy_containers}

Wenn eine Richtlinie angewendet wird, können Sie normal Inhalt auf Ihrem Cluster bereitstellen. Ihre Richtlinie wird vom Kubernetes-Cluster automatisch durchgesetzt. Wenn Ihre Bereitstellung mit einer Richtlinie übereinstimmt und von dieser zugelassen wird, wird Ihre Bereitstellung vom Cluster akzeptiert und angewendet.
{:shortdesc}

Wenn Container Image Security Enforcement eine Bereitstellung verweigert, wird die Bereitstellung erstellt, aber die von ihr erstellte Replikatgruppe kann nicht skaliert werden und es werden keine Pods erstellt. Sie finden die Replikatgruppe, indem Sie folgenden Befehl ausführen: `kubectl describe deployment <deployment-name>`. Daraufhin können Sie die Begründung für die Ablehnung mit folgendem Befehl anzeigen: `kubectl describe rs <replicaset-name>`.

**Beispiele für Fehlernachrichten**

* Wenn Ihr Image mit keiner Richtlinie übereinstimmt oder wenn im Namensbereich oder im Cluster keine Richtlinien vorhanden sind.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

* Wenn Ihr Image mit einer Richtlinie übereinstimmt, aber nicht die Vulnerability Advisor-Anforderungen dieser Richtlinie erfüllt.

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Refer to your image vulnerability report 
   for more details by using the command `ibmcloud cr va`.
   ```
   {: screen}

* Wenn Ihr Image mit einer Richtlinie übereinstimmt, aber nicht die Vertrauensanforderungen dieser Richtlinie erfüllt.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

* Wenn Ihre Richtlinie die Prüfung auf Sicherheitslücken für Ihr Image angibt, aber Ihr Image nicht aus einer unterstützten Registry stammt.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

Sie können die Option `va` in Ihrer Richtlinie aktivieren, um durchzusetzen, dass Vulnerability Advisor bestanden wird, bevor ein Image bereitgestellt werden kann. Images, die von Vulnerability Advisor nicht unterstützt werden, sind zulässig.

Sie können die Option `trust` in Ihrer Richtlinie akzeptieren, um Content Trust durchzusetzen. Wenn Sie keine `signerSecrets` (geheime Schlüssel von Unterzeichnern) angeben, wird die Bereitstellung zugelassen, sofern das Image überhaupt signiert wurde. Wenn Sie `signerSecrets` angeben, muss die zuletzt signierte Version des Image von allen Unterzeichnern signiert worden sein, die Sie angegeben haben. Container Image Security Enforcement überprüft, ob der angegebene öffentliche Schlüssel dem Unterzeichner gehört. Weitere Informationen zu Content Trust finden Sie unter [Images für vertrauenswürdige Inhalte signieren](registry_trusted_content.html).

Eine Bereitstellung ist nur dann zulässig, wenn alle Images die Prüfungen von Container Image Security Enforcement bestehen.

## Container Image Security Enforcement entfernen
{: #remove}

Bevor Sie anfangen, [wählen Sie Ihre `kubectl`-CLI](/docs/containers/cs_cli_install.html#cs_cli_configure) als Ziel für den Cluster aus.



1. Inaktivieren Sie Container Image Security Enforcement.

   ```
   $ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config 
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config
   ```
   {: codeblock}

2. Entfernen Sie den Chart.

   ```
   helm delete --purge cise
   ```
   {: pre}
