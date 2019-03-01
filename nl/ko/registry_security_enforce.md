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

# 컨테이너 이미지 보안 적용(베타)
{: #security_enforce}

Container Image Security Enforcement(베타)를 사용하면 컨테이너 이미지를 {{site.data.keyword.containerlong}}의 클러스터에 배치하기 전에 확인할 수 있습니다. 이미지가 배치되는 위치를 제어하고 Vulnerability Advisor 정책을 적용하며 [컨텐츠 신뢰](/docs/services/Registry/registry_trusted_content.html)가 올바르게 이미지에 적용되었는지 확인할 수 있습니다. 이미지가 정책 요구사항을 만족시키지 않는 경우에는 팟(Pod)이 클러스터에 배치되지 않거나 업데이트되지 않습니다.
{:shortdesc}

Container Image Security Enforcement는 {{site.data.keyword.registrylong}}에서 이미지 컨텐츠 신뢰 및 취약성에 대한 정보를 검색합니다. 사용자는 다른 레지스트리에 저장된 이미지의 배치를 차단하거나 허용하도록 선택할 수 있지만, 이러한 이미지에 대해 취약성 또는 신뢰 적용을 사용할 수는 없습니다.

## 클러스터에 Container Image Security Enforcement 설치
{: #sec_enforce_install}

**시작하기 전에**

* **Kubernetes 버전 1.9 이상**에서 사용할 클러스터를 [작성](/docs/containers/cs_clusters.html#clusters_ui)하거나 [업데이트](/docs/containers/cs_cluster_update.html#update)하십시오.
* 클러스터로 [`kubectl` CLI의 대상을 지정](/docs/containers/cs_cli_install.html#cs_cli_configure)하십시오.

다음 단계를 완료하십시오.

1. [클러스터에서 Helm을 설정](/docs/containers/cs_integrations.html#helm)하십시오.

2. Helm 클라이언트에 IBM 차트 저장소를 추가하십시오.

   ```
   helm repo add ibm https://registry.bluemix.net/helm/ibm
   ```
   {: pre}

3. 클러스터에 Container Image Security Enforcement Helm 차트를 설치하십시오. 이 차트에 `cise`와 같은 이름을 지정하십시오.

   ```
   helm install --name cise ibm/ibmcloud-image-enforcement
   ```
   {: pre}

Container Image Security Enforcement가 설치되었으며 클러스터의 모든 Kubernetes 네임스페이스에 [기본 보안 정책](#default_policies)을 적용합니다. 사용자 클러스터 또는 클러스터 전체에서 Kubernetes 네임스페이스의 보안 정책 사용자 정의에 대한 정보는 [정책 사용자 정의](#customize_policies)를 참조하십시오.

## 기본 정책
{: #default_policies}

Container Image Security Enforcement는 보안 정책 빌드를 위한 시작점을 제공하기 위해 기본적으로 몇 가지 정책을 설치합니다.
{:shortdesc}

이러한 정책을 대체하려면 다음 옵션 중 하나를 사용하십시오.

* 새 정책 문서 작성 후 `kubectl apply`를 사용하여 클러스터에 적용
* `kubectl edit`를 사용하여 기본 정책 편집

보안 정책 작성에 대한 자세한 정보는 [정책 사용자 정의](#customize_policies)를 참조하십시오.

### 클러스터 범위 정책
{: #cluster-wide}

기본적으로 클러스터 범위 정책은 모든 레지스트리의 모든 이미지가 신뢰 정보를 포함하고 Vulnerability Advisor의 보고된 취약성은 포함하지 않도록 합니다.
{:shortdesc}

**기본 클러스터 범위 정책 `.yaml` 파일**

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

{{site.data.keyword.registrylong_notm}}가 아닌 컨테이너 레지스트리에서 `va` 또는 `trust`를 `enabled: true`로 설정한 경우 이 레지스트리에 있는 이미지의 팟(Pod)을 배치하려는 시도가 거부됩니다. 다른 레지스트리의 이미지를 배치하려는 경우 `va` 및 `trust` 정책을 제거하십시오.
{:tip}

### Kube-system 정책
{: #kube-system}

기본적으로 네임스페이스 범위 정책이 `kube-system` 네임스페이스에 대해 설치됩니다. 이 정책을 사용하면 적용 없이 컨테이너 레지스트리의 모든 이미지를 `kube-system`에 배치할 수 있지만, 사용자는 이 정책 부분을 변경할 수 있습니다. 기본 정책은 클러스터를 올바르게 구성하기 위해 있어야 하는 특정 저장소 또한 포함하고 있습니다.
{:shortdesc}

**기본 `kube-system` 정책 `.yaml` 파일**

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

### IBM-system 정책
{: #ibm-system}

기본적으로 네임스페이스 범위 정책이 `ibm-system` 네임스페이스에 대해 설치됩니다. 이 정책을 사용하면 적용 없이 컨테이너 레지스트리의 모든 이미지를 `ibm-system`에 배치할 수 있지만, 사용자는 이 정책 부분을 변경할 수 있습니다. 기본 정책은 클러스터를 올바르게 구성하고 Container Image Security Enforcement를 설치하거나 업그레이드하기 위해 있어야 하는 특정 저장소 또한 포함하고 있습니다.
{:shortdesc}

**기본 `ibm-system` 정책 `.yaml` 파일**

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

## 정책 사용자 정의
{: #customize_policies}

클러스터 또는 Kubernetes 네임스페이스 레벨에서 Container Image Security Enforcement가 이미지를 허용하는 데 사용하는 정책을 변경할 수 있습니다. 정책에서 여러 이미지에 서로 다른 적용 규칙을 지정할 수 있습니다.
{:shortdesc}

몇 가지 정책을 설정해야 합니다. 그렇지 않으면 클러스터에 대한 배치에 실패합니다. 이미지 보안 정책이 적용되지 않도록 하려면 [Container Image Security Enforcement를 제거](#remove)하십시오.
{:tip}

배치를 적용할 때 Container Image Security Enforcement에서 사용자가 배치하는 Kubernetes 네임스페이스에 적용할 정책이 있는지 여부를 확인합니다. 없는 경우 Container Image Security Enforcement가 클러스터 범위 정책을 사용합니다. 네임스페이스 또는 클러스터 범위 정책이 없는 경우 배치가 거부됩니다.

시작하기 전에 클러스터로 [`kubectl` CLI의 대상을 지정](/docs/containers/cs_cli_install.html#cs_cli_configure)하십시오. 그런 다음, 다음 단계를 완료하십시오.

1. <a href="https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/" target="_blank">Kubernetes 사용자 정의 리소스 정의 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> `.yaml` 파일을 작성하십시오.

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
    <caption>표 1. YAML 컴포넌트 이해</caption>
    <thead>
    <th>필드</th>
    <th>설명</th>
    </thead>
    <tbody>
    <tr>
    <td><code>kind</code></td>
    <td>클러스터 범위 정책에서 `kind`를 `ClusterImagePolicy`으로 지정하십시오. Kubernetes 네임스페이스 정책의 경우에는 `ImagePolicy`로 지정하십시오.</td>
    </tr>
    <tr>
    <td><code>metadata/name</code></td>
    <td>사용자 정의 리소스 정의의 이름을 지정하십시오.</td>
    </tr>
    <tr>
    <td><code>spec/repositories/name</code></td>
    <td>이미지를 허용할 저장소를 지정하십시오. 와일드카드(`*`)가 저장소 이름에서 허용됩니다. `repositories`의 일치 항목이 허용하거나 추가 확인을 적용하지 않는 한 저장소는 거부됩니다. `repositories` 목록이 비어 있으면 모든 이미지의 배치를 차단합니다. 정책의 확인 없이 모든 이미지를 허용하려면 이름을 `*`로 설정하고 정책 하위 섹션을 생략하십시오.</td>
    </tr>
    <tr>
    <td><code>../../../policy</code></td>
    <td>`trust` 및 `va` 적용에 대한 하위 섹션을 완료하십시오. 정책 하위 섹션을 생략하면 각각에 `enabled: false`를 지정하는 경우와 같습니다.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/enabled</code></td>
    <td>[컨텐츠 신뢰를 위해 서명](/docs/services/Registry/registry_trusted_content.html)된 이미지만 배치하도록 하려면 `true`로 설정하십시오. 이미지가 서명되었는지 여부를 무시하려면 `false`로 설정하십시오.</td>
    </tr>
    <tr>
    <td><code>../../../../trust/signerSecrets/name</code></td>
    <td>특정 사용자가 서명한 이미지만 허용하려면 서명자 이름이 있는 Kubernetes 시크릿을 지정하십시오. 이 섹션을 생략하거나 비어 있게 두어 특정 서명자를 적용하지 않고 이미지가 서명되도록 하십시오. 자세한 정보는 [사용자 정의 정책에서 신뢰할 수 있는 컨텐츠 서명자 지정](#signers)을 참조하십시오.</td>
    </tr>
    <tr>
    <td><code>../../../../va/enabled</code></td>
    <td>[Vulnerability Advisor](/docs/services/va/va_index.html) 스캔을 통과한 이미지만 허용하려면 `true`로 설정하십시오. Vulnerability Advisor 스캔을 무시하려면 `false`로 설정하십시오.</td>
    </tr>
    </tbody>
    </table>

2. 클러스터에 `.yaml` 파일을 적용하십시오.

   ```
kubectl apply -f <filepath>
   ```
   {: pre}

### 사용자 정의 정책에 신뢰할 수 있는 컨텐츠 서명자 지정
{: #signers}

컨텐츠 신뢰를 사용하는 경우 특정 서명자가 이미지에 서명하도록 할 수 있습니다. 서명된 최신 버전이 나열된 모든 서명자에 의해 서명된 경우에만 배치가 허용됩니다. 저장소에 서명자를 추가하려면 [신뢰할 수 있는 서명자 관리](/docs/services/Registry/registry_trusted_content.html#trustedcontent_signers)를 참조하십시오.
{:shortdesc}

특정 서명자가 이미지에 서명했는지 확인하도록 정책을 구성하려면 다음을 수행하십시오.

1. 서명자 이름(`docker trust signer add`에 사용된 이름) 및 서명자의 공개 키를 가져오십시오.
2. 서명자 이름과 공개 키가 있는 Kubernetes 시크릿을 생성하십시오.

   ```
    kubectl create secret generic <secret_name> --from-literal=name=<signer_name> --from-file=publicKey=<key.pub>
   ```
   {: pre}

3. 정책의 저장소에 대한 `signerSecrets` 목록에 시크릿을 추가하십시오.

   ```yaml
   - name: example
     policy:
       trust:
         enabled: true
         signerSecrets:
         - name: <secret_name>
   ```
   {: codeblock}

## 정책을 사용자 정의할 수 있는 사용자 제어
{: #assign_user_policy}

Kubernetes 클러스터에서 역할 기반 액세스 제어(RBAC)를 사용하는 경우 역할을 작성하여 클러스터에서 보안 정책을 관리하는 기능을 가진 사용자를 통제할 수 있습니다. 클러스터에 RBAC 규칙을 적용하는 데 대한 자세한 정보는 [{{site.data.keyword.containerlong_notm}} 문서](/docs/containers/cs_users.html#rbac)를 참조하십시오.
{:shortdesc}

역할에서 보안 정책에 대한 규칙을 추가하십시오.

```yaml
- apiGroups: ["securityenforcement.admission.cloud.ibm.com"]
  resources: ["imagepolicies", "clusterimagepolicies"]
  verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
```
{: codeblock}

여러 역할을 작성하여 사용자가 수행할 수 있는 조치를 제어할 수 있습니다. 예를 들어, 일부 사용자가 `get` 또는 `list` 정책만 사용할 수 있도록 `verbs`를 변경하십시오. 또는 `resources` 목록에서 `clusterimagepolicies`를 생략하여 Kubernetes 네임스페이스 정책에 대한 액세스 권한만 부여할 수 있습니다.
{:tip}

사용자 정의 리소스 정의(CRD)를 삭제할 수 있는 액세스 권한을 가진 사용자는 보안 정책에 대한 리소스 정의를 삭제할 수 있으며, 이렇게 하면 보안 정책도 삭제됩니다. CRD를 삭제할 수 있는 사용자를 제어하십시오. CRD를 삭제할 수 있는 액세스 권한을 부여하려면 다음과 같이 규칙을 추가하십시오.

```yaml
- apiGroups: ["apiextensions.k8s.io/v1beta1"]
  resources: ["CustomResourceDefinition"]
  verbs: ["delete"]
```
{: codeblock}

`cluster-admin` 역할이 있는 사용자 및 서비스 계정에는 모든 리소스에 대한 액세스 권한이 있습니다. 역할을 편집하지 않는 경우에도 cluster-admin 역할은 보안 정책을 관리할 수 있는 액세스 권한을 부여합니다. `cluster-admin` 역할을 가진 사용자를 제어하고 보안 정책을 수정할 수 있도록 허용할 사용자에게만 액세스 권한을 부여하십시오.
{:tip}

## 보안이 적용되는 컨테이너 이미지 배치
{: #deploy_containers}

정책이 적용되면 일반적으로 클러스터에 컨텐츠를 배치할 수 있습니다. 정책은 Kubernetes 클러스터에서 자동으로 적용됩니다. 배치가 정책과 일치하고 이 정책에서 허용되는 경우 배치가 클러스터에서 허용되고 적용됩니다.
{:shortdesc}

Container Image Security Enforcement가 배치를 거부하면, 배치가 작성되어도 이 배치로 작성된 ReplicaSet은 확장에 실패하고 팟(Pod)이 작성되지 않습니다. `kubectl describe deployment <deployment-name>`을 실행하여 ReplicaSet을 찾은 다음 `kubectl describe rs <replicaset-name>`을 실행하여 배치가 거부된 이유를 확인할 수 있습니다.

**샘플 오류 메시지**

* 이미지가 정책과 일치하지 않거나 네임스페이스 또는 클러스터에 정책이 없는 경우.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, no image policies or cluster polices for <image-name>
   ```
   {: screen}

* 이미지가 정책과 일치하지만 정책의 Vulnerability Advisor 요구사항을 충족하지 않는 경우.

   ```
   admission webhook "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: The Vulnerability Advisor image scan assessment found issues with the container image that are not exempted. Refer to your image vulnerability report 
   for more details by using the command `ibmcloud cr va`.
   ```
   {: screen}

* 이미지가 정책과 일치하지만 정책의 신뢰 요구사항을 충족하지 않는 경우.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Deny, failed to get content trust information: No valid trust data for latest
   ```
   {: screen}

* 정책이 이미지에 신뢰 적용을 지정하지만 이미지를 지원되는 레지스트리에서 가져오지 않은 경우.

   ```
   admission webhook "trust.hooks.securityenforcement.admission.cloud.ibm.com" denied the request: Trust is not supported for images from this registry
   ```
   {: screen}

정책에 `va` 옵션을 사용하여 이미지를 배치하기 전에 Vulnerability Advisor가 수행되도록 할 수 있습니다. Vulnerability Advisor가 지원하지 않는 이미지가 허용됩니다.

정책에서 `trust` 옵션을 사용하여 컨텐츠 신뢰를 적용할 수 있습니다. `signerSecrets`를 지정하지 않으면 어떤 사용자가 이미지에 서명해도 배치가 허용됩니다. `signerSecrets`를 지정하면 최근에 서명된 버전의 이미지가 지정된 모든 사용자에 의해 서명되어 있어야 합니다. Container Image Security Enforcement는 제공된 공개 키가 서명자에게 속하는지 확인합니다. 컨텐츠 신뢰에 대한 자세한 정보는 [신뢰할 수 있는 컨텐츠의 이미지에 서명](/docs/services/Registry/registry_trusted_content.html)을 참조하십시오.

모든 이미지가 Container Image Security Enforcement 검사를 통과한 경우에만 배치가 허용됩니다.

## Container Image Security Enforcement 제거
{: #remove}

시작하기 전에 클러스터로 [`kubectl` CLI의 대상을 지정](/docs/containers/cs_cli_install.html#cs_cli_configure)하십시오.



1. Container Image Security Enforcement를 사용 안함으로 설정하십시오.

   ```
$ kubectl delete --ignore-not-found=true MutatingWebhookConfiguration image-admission-config
    $ kubectl delete --ignore-not-found=true ValidatingWebhookConfiguration image-admission-config
   ```
   {: codeblock}

2. 차트를 제거하십시오.

   ```
helm delete --purge cise
   ```
   {: pre}
