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

# Impondo a segurança de imagem de contêiner (Beta)
{: #security_enforce}

Com o Container Image Security Enforcement (Beta), é possível verificar as imagens de contêiner antes de implementá-las para o
cluster no {{site.data.keyword.containerlong}}. É possível controlar de onde as imagens serão implementadas, aplicar as políticas do Vulnerability Advisor e assegurar-se de que a [confiança de conteúdo](/docs/services/Registry/registry_trusted_content.html) seja aplicada corretamente à imagem. Se uma imagem não atender a seus requisitos de política, o pod não será implementado em seu cluster nem atualizado.
{:shortdesc}

O Container Image Security Enforcement recupera as informações sobre a confiança de conteúdo e as vulnerabilidades da imagem do {{site.data.keyword.registrylong}}. É possível optar por bloquear ou permitir a implementação de imagens armazenadas em outros registros, mas não é possível usar o cumprimento de vulnerabilidade ou de confiança para essas imagens.

## Instalando o Container Image Security Enforcement no cluster
{: #sec_enforce_install}

**Antes de iniciar**

* [Crie](/docs/containers/cs_clusters.html#clusters_ui) ou [atualize](/docs/containers/cs_cluster_update.html#update) o cluster que você deseja usar com o **Kubernetes versão 1.9 ou mais recente**.
* [Direcione a CLI do `kubectl`](/docs/containers/cs_cli_install.html#cs_cli_configure) para o cluster.

Conclua as etapas a seguir:

1. [Configure o Helm em seu cluster](/docs/containers/cs_integrations.html#helm).

2. Inclua o repositório de gráficos da IBM no cliente Helm.

   ```
   helm repo add ibm https://registry.bluemix.net/helm/ibm
   ```
   {: pre}

3. Instale o gráfico de Helm do Container Image Security Enforcement no cluster. Dê um nome a ele, como `cise`.

   ```
   helm install --name cise ibm/ibmcloud-image-enforcement
   ```
   {: pre}

Agora, o Container Image Security Enforcement está instalado e está aplicando a [política de
segurança padrão](#default_policies) para todos os namespaces do Kubernetes no cluster. Para obter informações sobre como customizar a política de segurança para namespaces do Kubernetes no cluster ou para o cluster em geral, consulte [Customizando políticas](#customize_policies).

## Políticas padrão
{: #default_policies}

O Container Image Security Enforcement instala algumas políticas por padrão para fornecer um ponto de início para a
construção da política de segurança.
{:shortdesc}

Para substituir essas políticas, use uma das opções a seguir:

* Grave um novo documento sobre políticas e aplique-o ao cluster usando `kubectl apply`
* Edite a política padrão usando `kubectl edit`

Para obter mais informações sobre como gravar políticas de segurança, consulte [Customizando políticas](#customize_policies).

### Política do cluster inteiro
{: #cluster-wide}

Por padrão, uma política em todo o cluster exige que todas as imagens em todos os registros tenham informações de confiança e não tenham vulnerabilidades relatadas no Vulnerability Advisor.
{:shortdesc}

**Arquivo `.yaml` padrão de política em todo o cluster**

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

Ao configurar `va` ou `trust` como `enabled: true` para um registro de contêiner diferente do {{site.data.keyword.registrylong_notm}}, todas as tentativas de implementar pods de imagens nesse registro serão negadas. Se desejar implementar imagens de outros registros, remova as políticas `va` e `trust`.
{:tip}

### Política Kube sistema
{: #kube-system}

Por padrão, uma política em todo o namespace é instalada para o namespace `kube-system`. Essa política permite que todas as imagens de qualquer registro de contêiner sejam implementadas no `kube-system` sem cumprimento, mas é possível mudar essa parte da política. A política padrão também inclui determinados repositórios que devem ser deixados no lugar para que seu cluster seja configurado corretamente.
{:shortdesc}

**Arquivo `.yaml` padrão de política do `kube-system`**

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
    -name: "*"
      policy: # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
    # IMPORTANT: When you create your own policy in this namespace, make sure to include these repositories. If you do not, the cluster might not function properly.
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```
{: codeblock}

### Política IBM no sistema
{: #ibm-system}

Por padrão, uma política em todo o namespace é instalada para o namespace `ibm-system`. Essa política permite que todas as imagens de qualquer registro de contêiner sejam implementadas no `ibm-system` sem cumprimento, mas é possível mudar essa parte da política. A política padrão também inclui determinados repositórios que devem ser deixados no lugar para que o cluster seja configurado corretamente e a instalação e o upgrade do Container Image Security Enforcement possam ser realizados.
{:shortdesc}

**Arquivo `.yaml` padrão de política do `ibm-system`**

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
    -name: "*"
      policy: # These policies allow all IBM Cloud Kubernetes Service images from the global and all regional registries to deploy in this namespace.
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
    # This policy allows Container Image Security Enforcement to use Hyperkube to configure your cluster. Essa política deverá existir se você desinstalar o Container Image Security Enforcement.
    - name: quay.io/coreos/hyperkube
      policies:
```
{: codeblock}

## Customizando políticas
{: #customize_policies}

É possível mudar a política que o Container Image Security Enforcement usa para permitir as imagens no nível do cluster ou do
namespace do Kubernetes. Na política, é possível especificar regras de cumprimento diferentes para imagens diferentes.
{:shortdesc}

Você deve ter um conjunto de política. Caso contrário, implementações em seu cluster falhar. Se você não desejar que
nenhuma política de segurança de imagem seja imposta, [remova o Container Image Security
Enforcement](#remove).
{:tip}

Quando você aplica uma implementação, o Container Image Security Enforcement verifica se o namespace do Kubernetes que está sendo implementado tem uma política para aplicar. Se não tiver, o Container Image Security Enforcement usará a política de todo o cluster. Sua implementação será negada se nenhuma política de todo o namespace ou de todo o cluster existir.

Antes de iniciar, [direcione a CLI do
kubectl](/docs/containers/cs_cli_install.html#cs_cli_configure) para o cluster. Em seguida, conclua as etapas a seguir:

1. Crie um arquivo `.yaml` de <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">definição de recurso customizado do Kubernetes <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

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
    <caption>Tabela 1. Compreendendo os componentes YAML</caption>
    <thead>
    <th>Campo</th>
    <th>descrição</th>
    </thead>
    <tbody>
    <tr>
    <td><code>tipo</code></td>
    <td>Para uma política em todo o cluster, especifique o `kind` como `ClusterImagePolicy`. Para uma política de namespace do Kubernetes, especifique como `ImagePolicy`.</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>Nomeie a definição de recurso customizado.</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>Especifique os repositórios do qual permitir imagens. Curingas (`*`) são permitidos em nomes de repositório. Os repositórios serão negados, a menos que uma entrada correspondente em `repositories` permita ou aplique verificação adicional. Uma lista vazia de `repositories` bloqueia a implementação de todas as imagens. Para permitir todas as imagens sem verificação de quaisquer políticas, configure o nome como `*` e omita as subseções de política.</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>Conclua as subseções para impor `trust` e `va`. Omitir as subseções de política equivale a especificar `enabled: false` para cada.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>Configure como `true` para permitir que apenas as imagens [assinadas para confiança de conteúdo](/docs/services/Registry/registry_trusted_content.html) sejam implementadas. Configure como `false` para ignorar se as imagens são assinadas.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>Se desejar permitir apenas as imagens assinadas por usuários específicos, especifique o segredo do Kubernetes com o nome do assinante. Omita esta seção ou deixe-a vazia para verificar se as imagens serão assinadas sem a exigência de assinantes específicos. Para obter mais informações, consulte [Especificando assinantes de conteúdo confiável em políticas customizadas](#signers).</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>Configure como `true` para permitir apenas as imagens que passam na varredura do [Vulnerability Advisor](/docs/services/va/va_index.html). Configure como `false` para ignorar a varredura do Vulnerability Advisor.</td>
    </tr>
    </tbody>
    </table>

2. Aplique o arquivo `.yaml` ao cluster.

   ```
   kubectl apply -f <filepath>
   ```
   {: pre}

### Especificando assinantes de conteúdo confiável em políticas customizadas
{: #signers}

Se você usar a confiança de conteúdo, será possível verificar se as imagens são assinadas por assinantes específicos. A
implementação será permitida somente se a versão assinada mais recente for assinada por todos os assinantes listados. Para incluir um assinante em um repositório, consulte [Gerenciando assinantes confiáveis](/docs/services/Registry/registry_trusted_content.html#trustedcontent_signers).
{:shortdesc}

Para configurar a política para verificar se uma imagem está assinada por um assinante específico:

1. Obtenha o nome do assinante (o nome usado em `docker trust signer add`) e a chave pública do assinante.
2. Gere um segredo do Kubernetes com o nome do assinante e sua chave pública.

   ```
   kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
   ```
   {: pre}

3. Inclua o segredo na lista `signerSecrets` do repositório em sua política.

   ```yaml
   - name: example
     policy:
       trust:
         enabled: true
         signerSecrets:
         - name: <secret_name>
   ```
   {: codeblock}

## Controlando quem pode customizar políticas
{: #assign_user_policy}

Se você tiver o controle de acesso baseado na função (RBAC) ativado no cluster do Kubernetes, será possível criar uma função para governar quem tem a capacidade de administrar políticas de segurança no cluster. Para obter mais informações sobre a aplicação das regras RBAC no cluster, consulte [a documentação do {{site.data.keyword.containerlong_notm}}](/docs/containers/cs_users.html#rbac).
{:shortdesc}

Em sua função, inclua uma regra para as políticas de segurança:

```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```
{: codeblock}

É possível criar múltiplas funções para controlar quais ações os usuários podem adotar. Por exemplo, mude os `verbs` para que alguns usuários possam usar apenas as políticas `get` ou `list`. Como alternativa, é possível omitir `clusterimagepolicies` da lista `resources` para conceder acesso apenas às políticas de namespace do Kubernetes.
{:tip}

Os usuários que têm acesso para excluir custom resource definitions (CRDs) podem excluir a definição de recurso para políticas de segurança, que também exclui suas políticas de segurança. Certifique-se de controlar quem tem permissão para excluir CRDs. Para conceder acesso para excluir CRDs, inclua uma regra:

```yaml
ApiGroups: [ "apiextensions.k8s.io/v1beta1" ]
  Recursos: [ "CustomResourceDefinition" ] verbos: [ "excluir" ]
```
{: codeblock}

Os usuários e as contas de serviço com a função `cluster-admin` têm acesso a todos os recursos. A função de administrador do cluster concede acesso para administrar políticas de segurança, mesmo se você não editar a função. Certifique-se de controlar quem tem a função `cluster-admin` e conceda acesso apenas às pessoas que você deseja permitir modificar políticas de segurança.
{:tip}

## Implementando imagens de contêiner com segurança reforçada
{: #deploy_containers}

Quando uma política é aplicada, é possível implementar conteúdo no cluster normalmente. Sua política é aplicada automaticamente pelo cluster do Kubernetes. Sua implementação será aceita pelo cluster e aplicada se ela corresponder e for permitida por uma política.
{:shortdesc}

Se o Container Image Security Enforcement negar uma implementação, ela será criada, mas o ReplicaSet criado por ela falhará ao ser escalado e nenhum pod será criado. É possível localizar o ReplicaSet executando `kubectl describe deployment <deployment-name>` e, em seguida, ver a razão pela qual a implementação foi negada executando `kubectl describe rs <replicaset-name>`.

**Mensagens de erro de amostra**

* Se a sua imagem não corresponder a nenhuma política ou se não houver políticas no namespace ou no cluster.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

* Se a sua imagem corresponder a uma política, mas não satisfizer os requisitos do Vulnerability Advisor dessa política.

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Consulte seu relatório de vulnerabilidade de imagem
   para obter mais detalhes usando o comando `ibmcloud cr va`.
   ```
   {: screen}

* Se a sua imagem corresponder a uma política, mas não satisfizer os requisitos de confiança dessa política.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

* Se a sua política especificar cumprimento de confiança para sua imagem, mas a sua imagem não for de um registro suportado.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

É possível ativar a opção `va` em sua política para exigir que o Vulnerability Advisor passe antes de uma imagem poder ser implementada. As imagens não suportadas pelo Vulnerability Advisor são permitidas.

É possível ativar a opção `trust` em sua política para cumprir a confiança de conteúdo. Se você não especificar `signerSecrets`, a implementação será permitida se a imagem for assinada por qualquer pessoa. Se você especificar `signerSecrets`, a versão assinada mais recentemente da imagem deverá ter sido assinada por todos os assinantes especificados. O Container Image Security Enforcement verifica se a chave pública fornecida pertence ao assinante. Para obter mais informações sobre a confiança de conteúdo, consulte [Assinando imagens para conteúdo confiável](/docs/services/Registry/registry_trusted_content.html).

Uma implementação será permitida somente se todas as imagens passarem nas verificações do Container Image Security Enforcement.

## Remover Imagem de Execução de Segurança do Contêiner
{: #remove}

Antes de iniciar, [direcione a CLI do
kubectl](/docs/containers/cs_cli_install.html#cs_cli_configure) para o cluster.



1. Desativar Segurança Enforcement. Imagem do Contêiner

   ```
   $ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config 
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config
   ```
   {: codeblock}

2. Remova o gráfico.

   ```
   Comando delete -- cise limpeza
   ```
   {: pre}
