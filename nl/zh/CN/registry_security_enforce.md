---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, Vulnerability Advisor policies, container image security, policy requirements, policies, Container Image Security Enforcement

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

# 强制实施容器映像安全性 (Beta)
{: #security_enforce}

通过 Container Image Security Enforcement (Beta)，可以在将容器映像部署到 {{site.data.keyword.containerlong}} 中的集群之前，对这些映像进行验证。您可以控制从何处部署映像，强制实施漏洞顾问程序策略，以及确保[内容信任](/docs/services/Registry/registry_trusted_content.html)正确应用于映像。如果映像不符合策略需求，那么不会将 pod 部署到集群，也不会更新 pod。
{:shortdesc}

Container Image Security Enforcement 从 {{site.data.keyword.registrylong}} 检索有关映像内容信任和漏洞的信息。您可以选择是阻止还是允许部署存储在其他注册表中的映像，但不能对这些映像使用漏洞或信任强制实施。

## 在集群中安装 Container Image Security Enforcement
{: #sec_enforce_install}

**开始之前**

* [创建](/docs/containers/cs_clusters.html#clusters_ui)或[更新](/docs/containers/cs_cluster_update.html#update)要与 **Kubernetes V1.9 或更高版本**配合使用的集群。
* [设定 `kubectl` CLI 的目标](/docs/containers/cs_cli_install.html#cs_cli_configure)为集群。

请完成以下步骤：

1. [在集群中设置 Helm](/docs/containers/cs_integrations.html#helm)。

2. 将 IBM 图表存储库添加到 Helm 客户机。

   ```
   helm repo add ibm https://registry.bluemix.net/helm/ibm
   ```
   {: pre}

3. 将 Container Image Security Enforcement Helm chart 安装到集群中。为其提供名称，例如 `cise`。

   ```
   helm install --name cise ibm/ibmcloud-image-enforcement
   ```
   {: pre}

现在，Container Image Security Enforcement 已安装，并会将[缺省安全策略](#default_policies)应用于集群中的所有 Kubernetes 名称空间。有关为集群中的 Kubernetes 名称空间或集群总体定制安全策略的信息，请参阅[定制策略](#customize_policies)。

## 缺省策略
{: #default_policies}

缺省情况下，Container Image Security Enforcement 会安装一些策略，以便为您提供构建安全策略的起点。
{:shortdesc}

要覆盖这些策略，请使用下列其中一个选项：

* 编写新的策略文档，然后使用 `kubectl apply` 将其应用于集群
* 使用 `kubectl edit` 编辑缺省策略

有关编写安全策略的更多信息，请参阅[定制策略](#customize_policies)。

### 集群范围的策略
{: #cluster-wide}

缺省情况下，集群范围的策略会强制所有注册表中的所有映像都包含信任信息，并且在漏洞顾问程序中没有报告的漏洞。
{:shortdesc}

**缺省集群范围的策略 `.yaml` 文件**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ClusterImagePolicy
metadata:
  name: ibmcloud-default-cluster-image-policy
spec:
   repositories:
    # 这将强制部署到此集群的所有映像都通过信任和 VA 检查
    # 要进行覆盖，请为特定 Kubernetes 名称空间设置 ImagePolicy，或修改此策略
    - name: "*"
      policy:
        trust:
          enabled: true
        va:
          enabled: true
```
{: codeblock}

对于除 {{site.data.keyword.registrylong_notm}} 以外的容器注册表，将 `va` 或 `trust` 设置为 `enabled: true` 时，会拒绝任何从该注册表中的映像部署 pod 的尝试。如果要从其他注册表部署映像，请除去 `va` 和 `trust` 策略。
{:tip}

### Kube-system 策略
{: #kube-system}

缺省情况下，将为 `kube-system` 名称空间安装名称空间范围的策略。此策略允许将任何容器注册表中的所有映像部署到 `kube-system` 中，而无需强制实施，但您可以更改策略的此部分。缺省策略还包含必须保留不变的某些存储库，以便正确配置集群。
{:shortdesc}

**缺省 `kube-system` 策略 `.yaml` 文件**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: kube-system
spec:
   repositories:
    # 此策略允许将所有映像部署到此名称空间中。此策略可防止破坏此名称空间中的任何现有第三方应用程序。
    # 重要信息：请复查此策略，并将其替换为符合您需求的策略。如果您不在此名称空间中运行任何第三方应用程序，那么可以完全除去此策略。
    - name: "*"
      policy:
    # 这些策略允许全局和所有区域注册表中的所有 IBM Cloud Kubernetes Service 映像部署在此名称空间中。
    # 重要信息：在此名称空间中创建自己的策略时，请确保包含这些存储库。否则，集群可能无法正常运行。
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
```
{: codeblock}

### IBM-system 策略
{: #ibm-system}

缺省情况下，将为 `ibm-system` 名称空间安装名称空间范围的策略。此策略允许将任何容器注册表中的所有映像部署到 `ibm-system` 中，而无需强制实施，但您可以更改策略的此部分。缺省策略中还包含一些特定存储库，这些存储库必须保留不动才能正确配置集群，也才能安装或升级 Container Image Security Enforcement。
{:shortdesc}

**缺省 `ibm-system` 策略 `.yaml` 文件**

```yaml
apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
kind: ImagePolicy
metadata:
  name: ibmcloud-image-policy
  namespace: ibm-system
spec:
   repositories:
    # 此策略允许将所有映像部署到此名称空间中。此策略可防止破坏此名称空间中的任何现有第三方应用程序。
    # 重要信息：请复查此策略，并将其替换为符合您需求的策略。如果您不在此名称空间中运行任何第三方应用程序，那么可以完全除去此策略。
    - name: "*"
      policy:
    # 这些策略允许全局和所有区域注册表中的所有 IBM Cloud Kubernetes Service 映像部署在此名称空间中。
    # 重要信息：在此名称空间中创建自己的策略时，请确保包含这些存储库。否则，集群可能无法正常运行。
    - name: "registry*.bluemix.net/armada/*"
      policy:
    - name: "registry*.bluemix.net/armada-worker/*"
      policy:
    - name: "registry*.bluemix.net/armada-master/*"
      policy:
    # 此策略可防止 Container Image Security Enforcement 阻止其本身
    - name: "registry*.bluemix.net/ibm/ibmcloud-image-enforcement"
      policy:
    # 此策略允许 Container Image Security Enforcement 使用 Hyperkube 来配置集群。如果要卸载 Container Image Security Enforcement，那么此策略必须存在。
    - name: quay.io/coreos/hyperkube
      policies:
```
{: codeblock}

## 定制策略
{: #customize_policies}

您可以在集群或 Kubernetes 名称空间级别更改 Container Image Security Enforcement 用于许可映像的策略。在策略中，您可以为不同的映像指定不同的强制实施规则。
{:shortdesc}

您必须设置某个策略。否则，部署到集群会失败。如果不希望强制实施任何映像安全策略，请[除去 Container Image Security Enforcement](#remove)。
{:tip}

应用部署时，Container Image Security Enforcement 会检查要部署到的 Kubernetes 名称空间是否具有要应用的策略。如果没有，Container Image Security Enforcement 会使用集群范围的策略。如果不存在名称空间或集群范围的策略，那么将拒绝部署。

开始之前，请[设定 `kubectl` CLI 的目标](/docs/containers/cs_cli_install.html#cs_cli_configure)为集群。然后，完成以下步骤：

1. 创建 <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">Kubernetes 定制资源定义 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> `.yaml` 文件。

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
    <caption>表 1. 了解 YAML 的组成部分</caption>
    <thead>
    <th>字段</th>
    <th>描述</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>对于集群范围的策略，请将 `kind` 指定为 `ClusterImagePolicy`。对于 Kubernetes 名称空间策略，请指定为 `ImagePolicy`。</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>命名定制资源定义。</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>指定要允许使用其中映像的存储库。存储库名称中允许使用通配符 (`*`)。除非 `repositories` 中的匹配条目允许存储库或应用进一步验证，否则将拒绝这些存储库。`repositories` 列表为空将阻止部署所有映像。要在不验证任何策略的情况下允许所有映像，请将名称设置为 `*`，并省略 policy 子节。</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>填写 `trust` 和 `va` 强制实施的子节。如果省略 policy 子节，那么相当于为这两个子节指定 `enabled: false`。</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>设置为 `true` 仅允许部署已[签名以实现内容信任](/docs/services/Registry/registry_trusted_content.html)的映像。设置为 `false` 会忽略是否对映像签名。</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>如果希望只允许特定用户签名的映像，请指定包含签署者名称的 Kubernetes 私钥。省略此节或使其留空可验证是否已对映像签名，而不强制验证特定签署者。有关更多信息，请参阅[在定制策略中指定可信内容签署者](#signers)。</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>设置为 `true` 仅允许通过[漏洞顾问程序](/docs/services/va/va_index.html)扫描的映像。设置为 `false` 会忽略漏洞顾问程序扫描。</td>
    </tr>
    </tbody>
    </table>

2. 将 `.yaml` 文件应用于集群。

   ```
kubectl apply -f <filepath>
    ```
   {: pre}

### 在定制策略中指定可信内容签署者
{: #signers}

如果使用内容信任，那么可以验证映像是否由特定签署者签名。仅当所有列出的签署者均对最新的签名版本签名时，才允许部署。要将签署者添加到存储库，请参阅[管理可信签署者](/docs/services/Registry/registry_trusted_content.html#trustedcontent_signers)。
{:shortdesc}

要配置策略以验证映像是否由特定签署者签名，请执行以下操作：

1. 获取签署者名称（在 `docker trust signer add` 中使用的名称）和签署者的公用密钥。
2. 使用签署者名称及其公用密钥生成 Kubernetes 私钥。
    

   ```
    kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
    ```
   {: pre}

3. 将该私钥添加到策略中存储库的 `signerSecrets` 列表。
    

   ```yaml
   - name: example
     policy:
       trust:
         enabled: true
         signerSecrets:
         - name: <secret_name>
   ```
   {: codeblock}

## 控制可以定制策略的人员
{: #assign_user_policy}

如果在 Kubernetes 集群上启用了基于角色的访问控制 (RBAC)，那么可以创建角色来控制谁能够管理集群上的安全策略。有关将 RBAC 规则应用于集群的更多信息，请参阅 [{{site.data.keyword.containerlong_notm}} 文档](/docs/containers/cs_users.html#rbac)。
{:shortdesc}

在角色中，添加安全策略的规则：

```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```
{: codeblock}

可以创建多个角色来控制用户可以执行的操作。例如，更改 `verbs`，使得某些用户只能使用 `get` 或 `list` 策略。或者，可以省略 `resources` 列表中的 `clusterimagepolicies`，以仅授予对 Kubernetes 名称空间策略的访问权。
{:tip}

有权删除定制资源定义 (CRD) 的用户可以删除安全策略的资源定义，这样还会删除安全策略。确保控制允许谁来删除 CRD。要授予删除 CRD 的访问权，请添加规则：

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```
{: codeblock}

具有 `cluster-admin` 角色的用户和服务帐户有权访问所有资源。即使您不编辑 cluster-admin 角色，该角色也会授予管理安全策略的访问权。确保控制谁具有 `cluster-admin` 角色，并仅向您希望允许其修改安全策略的人员授予访问权。
{:tip}

## 部署强制实施了安全性的容器映像
{: #deploy_containers}

应用策略后，可以将内容正常部署到集群。策略由 Kubernetes 集群自动强制实施。如果部署与策略相匹配，并且该策略允许部署，那么部署会被集群接受并进行应用。
{:shortdesc}

如果 Container Image Security Enforcement 拒绝了部署，那么会创建部署，但它创建的 ReplicaSet 无法扩展，并且不会创建任何 pod。您可以通过运行 `kubectl describe deployment <deployment-name>` 来查找 ReplicaSet，然后通过运行 `kubectl describe rs <replicaset-name>`.

**样本错误消息**

* 如果映像与任何策略都不匹配，或者名称空间或集群中没有任何策略。

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

* 如果映像与策略相匹配，但不满足策略的漏洞顾问程序需求。

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Refer to your image vulnerability report 
   for more details by using the command `ibmcloud cr va`.
   ```
   {: screen}

* 如果映像与策略相匹配，但不满足该策略的信任需求。

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

* 如果策略为映像指定了信任强制实施，但映像并不是来自支持的注册表。

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

可以在策略中启用 `va` 选项以强制漏洞顾问程序在部署映像之前通过。这将允许漏洞顾问程序不支持的映像。

可以在策略中启用 `trust` 选项来强制实施内容信任。如果未指定任何 `signerSecrets`，那么允许部署由任何人签名的映像。如果指定 `signerSecrets`，那么最近签名的映像版本必须已由您指定的所有签署者签名。Container Image Security Enforcement 会验证提供的公用密钥是否属于签署者。有关内容信任的更多信息，请参阅[对映像签名以实现可信内容](/docs/services/Registry/registry_trusted_content.html)。

仅当所有映像都通过了 Container Image Security Enforcement 检查时，才允许部署。

## 除去 Container Image Security Enforcement
{: #remove}

开始之前，请[设定 `kubectl` CLI 的目标](/docs/containers/cs_cli_install.html#cs_cli_configure)为集群。



1. 禁用 Container Image Security Enforcement。

   ```
$ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config 
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config 
    ```
   {: codeblock}

2. 除去图表。

   ```
helm delete --purge cise
    ```
   {: pre}
