---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Applicazione della sicurezza dell'immagine del contenitore (Beta)
{: #security_enforce}

Con Container Image Security Enforcement (Beta), puoi verificare le tue immagini del contenitore prima di distribuirle al tuo cluster in {{site.data.keyword.containerlong}}. Puoi controllare da dove vengono distribuite le immagini, applicare le politiche di Controllo vulnerabilità e garantire che l'[attendibilità dei contenuti](/docs/services/Registry/registry_trusted_content.html) sia applicata correttamente all'immagine. Se un'immagine non soddisfa i requisiti della tua politica, il pod non viene distribuito al tuo cluster o aggiornato.
{:shortdesc}

Container Image Security Enforcement richiama le informazioni sull'attendibilità dei contenuti e sulle vulnerabilità delle immagini da {{site.data.keyword.registrylong}}. Puoi scegliere di bloccare o di consentire la distribuzione di immagini memorizzate in altri registri ma non puoi utilizzare la vulnerabilità o l'applicazione dell'attendibilità per queste immagini.

## Installazione di Container Image Security Enforcement nel tuo cluster
{: #sec_enforce_install}

**Prima di iniziare**

* [Crea](/docs/containers/cs_clusters.html#clusters_ui) o [aggiorna](/docs/containers/cs_cluster_update.html#update) il cluster che vuoi utilizzare con **Kubernetes versione 1.9 o successive**.
* [Indirizza la tua CLI `kubectl`](/docs/containers/cs_cli_install.html#cs_cli_configure) al cluster.

Completa la seguente procedura:

1. [Configura Helm nel tuo cluster](/docs/containers/cs_integrations.html#helm).

2. Aggiungi il repository di grafici IBM al tuo client Helm.

   ```
   helm repo add ibm https://registry.bluemix.net/helm/ibm
   ```
   {: pre}

3. Installa il grafico Container Image Security Enforcement Helm nel tuo cluster. Denominalo come `cise`.

   ```
   helm install --name cise ibm/ibmcloud-image-enforcement
   ```
   {: pre}

Container Image Security Enforcement è ora installato e applica la [politica di sicurezza predefinita](#default_policies) per tutti gli spazi dei nomi Kubernetes nel tuo cluster. Per informazioni su come personalizzare la politica di sicurezza per gli spazi dei nomi Kubernetes nel tuo cluster o i cluster in generale, vedi [Personalizzazione delle politiche](#customize_policies).

## Politiche predefinite
{: #default_policies}

Container Image Security Enforcement installa alcune politiche per impostazione predefinita per fornirti un punto di partenza per la creazione della tua politica di sicurezza.
{:shortdesc}

Per sovrascrivere queste politiche, utilizza una delle seguenti opzioni:

* Scrivi un nuovo documento di politiche e applicalo al tuo cluster utilizzando `kubectl apply`
* Modifica la politica predefinita utilizzando `kubectl edit`

Per ulteriori informazioni su come scrivere le politiche di sicurezza, vedi [Personalizzazione delle politiche](#customize_policies).

### Politica a livello di cluster
{: #cluster-wide}

Per impostazione predefinita, una politica a livello di cluster impone che tutte le immagini in tutti i registri dispongano di informazioni sull'attendibilità e non abbiano vulnerabilità segnalate in Controllo vulnerabilità.
{:shortdesc}

**File `.yaml` della politica a livello di cluster predefinita**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ClusterImagePolicy
metadata:
  name: ibmcloud-default-cluster-image-policy
spec:
   repositories:
    # This enforces that all images deployed to this cluster pass trust and VA
    # To override, set an ImagePolicy for a specific Kubernetes namespace or modify this policy
    - name: "*"
      policy:
        trust:
          enabled: true
        va:
          enabled: true
```
{: codeblock}

Quando imposti `va` o `trust` su `enabled: true` per un registro contenitori diverso da {{site.data.keyword.registrylong_notm}}, tutti i tentativi di distribuire i pod dalle immagini presenti in quel registro vengono negati. Se vuoi distribuire immagini da altri registri, rimuovi le politiche `va` e `trust`.
{:tip}

### Politica di sistema Kube
{: #kube-system}

Per impostazione predefinita, una politica a livello di spazio dei nomi viene installata per lo spazio dei nomi `kube-system`. Questa politica consente la distribuzione di tutte le immagini da qualsiasi registro contenitori in `kube-system` senza applicazione, ma puoi modificare questa parte della politica. La politica predefinita include anche dei repository che è necessario lasciare al proprio posto in modo che il tuo cluster sia configurato correttamente.
{:shortdesc}

**File `.yaml` della politica di `kube-system` predefinita**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: kube-system
spec:
   repositories:
    # This policy allows all images to be deployed into this namespace. This policy prevents breaking any existing third party applications in this namespace.
    # IMPORTANT: Review this policy and replace it with one that meets your requirements. If you do not run any third party applications in this namespace, you can remove this policy entirely.
    - name: "*"
      policy:
    # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```
{: codeblock}

### Politica di sistema IBM
{: #ibm-system}

Per impostazione predefinita, una politica a livello di spazio dei nomi viene installata per lo spazio dei nomi `ibm-system`. Questa politica consente la distribuzione di tutte le immagini da qualsiasi registro contenitori in `ibm-system` senza applicazione, ma puoi modificare questa parte della politica. La politica predefinita include anche dei repository che è necessario lasciare al proprio posto in modo che il tuo cluster sia configurato correttamente e possa installare o eseguire l'upgrade di Container Image Security Enforcement.
{:shortdesc}

**File `.yaml` della politica di `ibm-system` predefinita**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: ibm-system
spec:
   repositories:
    # This policy allows all images to be deployed into this namespace. This policy prevents breaking any existing third party applications in this namespace.
    # IMPORTANT: Review this policy and replace it with one that meets your requirements. If you do not run any third party applications in this namespace, you can remove this policy entirely.
    - name: "*"
      policy:
    # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
    # This policy prevents Container Image Security Enforcement from blocking itself
    - name: "registry*.bluemix.net/ibm/ibmcloud-image-enforcement"
      policy:
    # This policy allows Container Image Security Enforcement to use Hyperkube to configure your cluster. This policy must exist if you uninstall Container Image Security Enforcement.
    - name: quay.io/coreos/hyperkube
      policies:
```
{: codeblock}

## Personalizzazione delle politiche
{: #customize_policies}

Puoi modificare la politica utilizzata da Container Image Security Enforcement per consentire le immagini, a livello di cluster o di spazio dei nomi Kubernetes. Nella politica, puoi specificare diverse regole di applicazione per le diverse immagini.
{:shortdesc}

Devi disporre di una serie di politiche. In caso contrario, le distribuzioni al tuo cluster non riescono. Se non vuoi applicare alcuna politica di sicurezza dell'immagine, [rimuovi Container Image Security Enforcement](#remove).
{:tip}

Quando applichi una distribuzione, Container Image Security Enforcement verifica se lo spazio dei nomi Kubernetes in cui stai distribuendo ha una politica da applicare. Se non ce l'ha, Container Image Security Enforcement utilizza la politica a livello di cluster. La tua distribuzione viene negata se non esistono politiche a livello di spazio dei nomi o di cluster.

Prima di iniziare, [indirizza la tua CLI `kubectl`](/docs/containers/cs_cli_install.html#cs_cli_configure) al cluster. Successivamente, completa la seguente procedura:

1. Crea un file `.yaml` di <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">definizione di risorsa personalizzata Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

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
    <caption>Tabella 1. Descrizione dei componenti di YAML</caption>
    <thead>
    <th>Campo</th>
    <th>Descrizione</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>Per una politica a livello di cluster, specifica il `kind` come `ClusterImagePolicy`. Per una politica dello spazio dei nomi Kubernetes, specificalo come `ImagePolicy`.</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>Assegna un nome alla definizione di risorsa personalizzata.</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>Specifica i repository da cui consentire le immagini. Nei nomi di repository sono consentiti i caratteri jolly (`*`). I repository vengono negati a meno che una voce corrispondente `repositories` lo consenta o applichi un'ulteriore verifica. Un elenco `repositories` vuoto blocca la distribuzione di tutte le immagini. Per consentire tutte le immagini senza la verifica di alcuna politica, imposta il nome su `*` e ometti le sottosezioni della politica.</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>Completa le sottosezioni per l'applicazione di `trust` e `va`. L'omissione delle sottosezioni della politica equivale a specificare `enabled: false` per ognuna di esse.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>Imposta come `true` per consentire di distribuire solo le immagini [firmate per l'attendibilità dei contenuti](/docs/services/Registry/registry_trusted_content.html). Imposta come `false` per ignorare se le immagini sono firmate.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>Se vuoi consentire solo le immagini firmate da determinati utenti, specifica il segreto Kubernetes con il nome del firmatario. Ometti questa sezione o lasciala vuota per verificare che le immagini siano firmate senza imporre particolari firmatari. Per ulteriori informazioni, vedi [Specifica dei firmatari di contenuti attendibili nelle politiche personalizzate](#signers).</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>Imposta come `true` per consentire solo le immagini che superano la scansione di [Controllo vulnerabilità](/docs/services/va/va_index.html). Imposta come `false` per ignorare la scansione di Controllo vulnerabilità.</td>
    </tr>
    </tbody>
    </table>

2. Applica il file `.yaml` al tuo cluster.

   ```
   kubectl apply -f <filepath>
   ```
   {: pre}

### Specifica dei firmatari di contenuti attendibili nelle politiche personalizzate
{: #signers}

Se utilizzi l'attendibilità dei contenuti, puoi verificare che le immagini siano firmate da determinati firmatari. La distribuzione viene consentita solo se la versione firmata più recente è firmata da tutti i firmatari elencati. Per aggiungere un firmatario a un repository, vedi [Gestione dei firmatari attendibili](/docs/services/Registry/registry_trusted_content.html#trustedcontent_signers).
{:shortdesc}

Per configurare la politica per verificare che un'immagine sia firmata da un determinato firmatario:

1. Ottieni il nome firmatario (il nome che è stato utilizzato in `docker trust signer add`) e la chiave pubblica del firmatario.
2. Genera un segreto Kubernetes con il nome del firmatario e la sua chiave pubblica.

   ```
   kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
   ```
   {: pre}

3. Aggiungi il segreto all'elenco `signerSecrets` per il repository nella tua politica.

   ```yaml
   - name: example
     policy:
       trust:
         enabled: true
         signerSecrets:
         - name: <secret_name>
   ```
   {: codeblock}

## Controllo di chi può personalizzare le politiche
{: #assign_user_policy}

Se sul tuo cluster Kubernetes hai abilitato il controllo degli accessi in base al ruolo (RBAC), puoi creare un ruolo per controllare chi ha la capacità di amministrare le politiche di sicurezza sul tuo cluster. Per ulteriori informazioni sull'applicazione di regole RBAC al tuo cluster, vedi [la documentazione di {{site.data.keyword.containerlong_notm}}](/docs/containers/cs_users.html#rbac).
{:shortdesc}

Nel tuo ruolo, aggiungi una regola per le politiche di sicurezza:

```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```
{: codeblock}

Puoi creare più ruoli per controllare quali azioni possono essere eseguite dagli utenti. Ad esempio, modifica i `verbs` in modo che alcuni utenti possano utilizzare solo le politiche `get` o `list`. In alternativa, puoi omettere `clusterimagepolicies` dall'elenco `resources` per concedere l'accesso solo alle politiche degli spazi dei nomi Kubernetes.
{:tip}

Gli utenti che hanno accesso per eliminare le definizioni di risorse personalizzate (CRD) possono eliminare la definizione di risorsa per le politiche di sicurezza, il che elimina anche le tue politiche di sicurezza. Assicurati di controllare chi è autorizzato a eliminare le CRD. Per concedere l'accesso per eliminare le CRD, aggiungi una regola:

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```
{: codeblock}

Gli utenti e gli account del servizio con il ruolo `cluster-admin` hanno accesso a tutte le risorse. Il ruolo cluster-admin concede l'accesso per amministrare le politiche di sicurezza, anche se non modifichi il ruolo. Assicurati di controllare chi ha il ruolo `cluster-admin` e concedi l'accesso solo alle persone a cui desideri consentire di modificare le politiche di sicurezza.
{:tip}

## Distribuzione di immagini del contenitore con la sicurezza applicata
{: #deploy_containers}

Quando viene applicata una politica, puoi distribuire normalmente il contenuto nel tuo cluster. La tua politica viene applicata automaticamente dal cluster Kubernetes. Se la tua distribuzione corrisponde a una politica ed è consentita da tale politica, la distribuzione viene accettata dal cluster e applicata.
{:shortdesc}

Se Container Image Security Enforcement nega una distribuzione, la distribuzione viene creata ma la serie di repliche creata non può essere incrementata e non viene creato alcun pod. Puoi trovare la serie di repliche eseguendo `kubectl describe deployment <deployment-name>` e quindi vedere il motivo per cui la distribuzione è stata negata eseguendo `kubectl describe rs <replicaset-name>`.

**Messaggi di errore di esempio**

* Se la tua immagine non corrisponde ad alcuna politica o non ci sono politiche nello spazio dei nomi o nel cluster.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

* Se la tua immagine corrisponde a una politica ma non soddisfa i requisiti di Controllo vulnerabilità di tale politica.

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Refer to your image vulnerability report
   for more details by using the command `ibmcloud cr va`.
   ```
   {: screen}

* Se la tua immagine corrisponde a una politica ma non soddisfa i requisiti di attendibilità di tale politica.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

* Se la tua politica specifica l'applicazione dell'attendibilità per la tua immagine, ma l'immagine non proviene da un registro supportato.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

Puoi abilitare l'opzione `va` nella tua politica per applicare l'approvazione del Controllo vulnerabilità prima che un'immagine possa essere distribuita. Le immagini che non sono supportate dal Controllo vulnerabilità sono consentite.

Puoi abilitare l'opzione `trust` nella tua politica per applicare l'attendibilità dei contenuti. Se non specifichi alcun `signerSecrets`, la distribuzione viene consentita se l'immagine è firmata da chiunque. Se specifichi `signerSecrets`, l'ultima versione firmata dell'immagine deve essere stata firmata da tutti i firmatari specificati. Container Image Security Enforcement verifica che la chiave pubblica fornita appartenga al firmatario. Per ulteriori informazioni sull'attendibilità dei contenuti, vedi [Firma di immagini per contenuti attendibili](/docs/services/Registry/registry_trusted_content.html).

Una distribuzione viene consentita solo se tutte le immagini superano i controlli di Container Image Security Enforcement.

## Rimozione di Container Image Security Enforcement
{: #remove}

Prima di iniziare, [indirizza la tua CLI `kubectl`](/docs/containers/cs_cli_install.html#cs_cli_configure) al cluster.



1. Disabilita Container Image Security Enforcement.

   ```
   $ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config 
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config
   ```
   {: codeblock}

2. Rimuovi il grafico.

   ```
   helm delete --purge cise
   ```
   {: pre}
