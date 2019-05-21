---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

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

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

`container-registry` CLI 플러그인에서 제공되는 {{site.data.keyword.registrylong}} CLI를 사용하여 {{site.data.keyword.cloud_notm}} 계정의 레지스트리 및 해당 리소스를 관리할 수 있습니다.
{: shortdesc}

**전제조건**

* [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)를 설치하십시오. {{site.data.keyword.cloud_notm}} CLI를 사용하여 명령을 실행하기 위한 접두부는 `ibmcloud`입니다.
* 레지스트리 명령을 실행하기 전에 `ibmcloud login` 명령으로 {{site.data.keyword.cloud_notm}}에
로그인하여 액세스 토큰을 생성하고 세션을 인증하십시오.

명령행에서 `ibmcloud` CLI 및 `container-registry` CLI 플러그인에 대한 업데이트가 사용 가능할 때 알림을 받습니다. 사용 가능한 모든 명령과 플래그를 사용할 수 있도록 CLI를 최신 상태로 유지해야 합니다.

현재 버전의 `container-registry` CLI 플러그인을 보려면 `ibmcloud plugin list`를 실행하십시오.

{{site.data.keyword.registrylong_notm}} CLI를 사용하는 방법에 대해 알아보려면 [{{site.data.keyword.registrylong_notm}} 시작하기](/docs/services/Registry?topic=registry-getting-started#getting-started)를 참조하십시오.

일부 명령에 필요한 IAM 플랫폼 및 서비스 액세스 역할에 대한 자세한 정보는 [IAM(Identity and Access Management)으로 사용자 액세스 관리](/docs/services/Registry?topic=registry-iam#iam)를 참조하십시오.

컨테이너 이미지, 네임스페이스 이름, 설명 필드(예: 레지스트리 토큰) 또는 이미지 구성 데이터(예: 이미지 이름 또는 이미지 레이블)에 개인 정보를 입력하지 마십시오.
{:tip}

## `ibmcloud cr api`
{: #bx_cr_api}

명령이 실행되는 레지스트리 API 엔드포인트에 대한 세부사항을 리턴합니다.

```
ibmcloud cr api
```
{: codeblock}

**전제조건**

없음

## `ibmcloud cr build`
{: #bx_cr_build}

{{site.data.keyword.registrylong_notm}}에서 Docker 이미지를 빌드합니다.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`DIRECTORY`</dt>
<dd>빌드 컨텍스트의 위치이며, Dockerfile 및 전제조건 파일을 포함합니다. 작업 디렉토리를 빌드 컨텍스트가 저장된 위치로 설정한 경우 명령을 실행하면 `DIRECTORY`를 점(.)으로 바꿀 수 있습니다.</dd>
<dt>`--no-cache`</dt>
<dd>(선택사항) 지정된 경우, 이전 빌드에서 캐시된 이미지 계층이 이 빌드에 사용되지 않습니다.</dd>
<dt>`--pull`</dt>
<dd>(선택사항) 지정된 경우, 일치하는 태그가 있는 이미지가 이미 빌드 호스트에 있는 경우에도 기본 이미지를 가져옵니다.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(선택사항) 지정된 경우, 오류가 발생하지 않는 한 빌드 출력이 표시되지 않습니다.</dd>
<dt>`--build-arg KEY=VALUE`</dt>
<dd>(선택사항) `'KEY=VALUE'` 형식의 추가 빌드 인수를 지정합니다. 이 매개변수를 여러 번 포함하여 여러 빌드 인수를 지정할 수 있습니다. 각 빌드 인수 값은 Dockerfile의 키와 일치하는 ARG 행을 지정하는 경우 환경 변수로 사용 가능합니다.</dd>
<dt>`--file FILE`, `-f FILE`</dt>
<dd>(선택사항) 여러 빌드에 동일한 파일을 사용하는 경우 경로를 다른 Dockerfile로 선택할 수 있습니다. 빌드 컨텍스트에 대한 Dockerfile의 위치를 지정합니다. 지정하지 않은 경우 기본값은 `PATH/Dockerfile`이며, 여기서 PATH는 빌드 컨텍스트의 루트입니다.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>빌드할 이미지의 전체 이름이며, 레지스트리 URL 및 네임스페이스를 포함합니다.</dd>
</dl>

**예**

이전 빌드의 빌드 캐시를 사용하지 않는 Docker 이미지를 빌드하십시오. 이 경우 빌드 출력이 억제되고 태그는 *`us.icr.io/birds/bluebird:1`*이며 디렉토리는 사용자의 작업 디렉토리입니다.

```
ibmcloud cr build --no-cache --quiet --tag us.icr.io/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

보안 문제에 대한 면제 항목을 작성합니다. 보안 문제에 대해 서로 다른 범위에 적용되는 면제 항목을 작성할 수 있습니다. 범위는 계정, 네임스페이스, 저장소 또는 태그일 수 있습니다.

```
ibmcloud cr exemption-add --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>범위를 계정으로 설정하려면 `"*"`를 값으로 사용하십시오. 네임스페이스, 저장소 또는 태그를 범위로 설정하려면 다음 형식 중 하나로 값을 입력하십시오: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>면제할 보안 문제의 유형입니다. 유효한 문제 유형을 찾으려면 `ibmcloud cr exemption-types`를 실행하십시오.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>면제할 보안 문제의 ID입니다. 문제 ID를 찾으려면 `ibmcloud cr va <image>`(여기서 `<image>`는 이미지의 이름)를 실행하고 **취약성 ID** 또는 **구성 문제 ID** 열에 있는 값 중 관련된 값을 사용하십시오.
</dd>
</dl>

**예**

`us.icr.io/birds/bluebird` 저장소에 있는 모든 이미지에 대해 ID가 `CVE-2018-17929`인 CVE에 대한 CVE 면제 항목을 작성합니다.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

ID가 `CVE-2018-17929`인 CVE에 대한 계정 전체의 CVE 면제 항목을 작성합니다.

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

`us.icr.io/birds/bluebird:1` 태그가 지정된 단일 이미지에 대한 `application_configuration:nginx.ssl_protocols` 문제의 구성 문제 면제 항목을 작성합니다.

```
ibmcloud cr exemption-add --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

보안 문제에 대한 면제 항목을 나열합니다.

```
ibmcloud cr exemption-list [--scope SCOPE]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>(선택사항) 이 범위에 적용되는 면제 항목만을 나열합니다. 네임스페이스, 저장소 또는 태그를 범위로 설정하려면 다음 형식 중 하나로 값을 입력하십시오: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
</dl>

**예**

*`birds/bluebird`* 저장소에 있는 이미지에 적용되는 보안 문제에 대한 모든 면제 항목을 나열합니다. 출력에는 계정 전체의 면제 항목, *`birds`* 네임스페이스로 범위가 지정된 면제 항목 및 *`birds/bluebird`* 저장소로 범위가 지정되었지만 *`birds/bluebird`* 저장소 내의 특정 태그로 범위가 지정되지 않은 면제 항목이 포함됩니다.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

보안 문제에 대한 면제 항목을 삭제합니다. 기존 면제 항목을 보려면 `ibmcloud cr exemption-list`를 실행하십시오.

```
ibmcloud cr exemption-rm --scope SCOPE --issue-type ISSUE_TYPE --issue-id ISSUE_ID
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--scope SCOPE`</dt>
<dd>범위를 계정으로 설정하려면 `"*"`를 값으로 사용하십시오. 네임스페이스, 저장소 또는 태그를 범위로 설정하려면 다음 형식 중 하나로 값을 입력하십시오: `namespace`, `namespace/repository`, `namespace/repository:tag`
</dd>
<dt>`--issue-type ISSUE_TYPE`</dt>
<dd>제거할 보안 문제에 대한 면제 항목의 문제 유형입니다. 면제 항목의 문제 유형을 찾으려면 `ibmcloud cr exemption-list`를 실행하십시오.
</dd>
<dt>`--issue-id ISSUE_ID`</dt>
<dd>제거할 보안 문제에 대한 면제 항목의 ID입니다. 면제 항목의 문제 ID를 찾으려면 `ibmcloud cr exemption-list`를 실행하십시오.
</dd>
</dl>

**예**

`us.icr.io/birds/bluebird` 저장소에 있는 모든 이미지에 대해 ID가 `CVE-2018-17929`인 CVE에 대한 CVE 면제 항목을 삭제합니다.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

ID가 `CVE-2018-17929`인 CVE에 대한 계정 전체의 CVE 면제 항목을 삭제합니다.

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

`us.icr.io/birds/bluebird:1` 태그가 지정된 단일 이미지에 대한 `application_configuration:nginx.ssl_protocols` 문제의 구성 문제 면제 항목을 삭제합니다.

```
ibmcloud cr exemption-rm --scope us.icr.io/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

면제할 수 있는 보안 문제의 유형을 나열합니다.

```
ibmcloud cr exemption-types
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

IAM 인증을 사용 중인 경우 이 명령은 세부 단위의 인증을 사용으로 설정합니다. 자세한 정보는 [IAM(Identity and Access Management)으로 사용자 액세스 관리](/docs/services/Registry?topic=registry-iam#iam) 및 [사용자 액세스 역할 정책 정의](/docs/services/Registry?topic=registry-user#user)를 참조하십시오.

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

## `ibmcloud cr iam-policies-status`
{: #bx_cr_iam_policies_status}

대상 지정된 {{site.data.keyword.registryshort_notm}} 계정의 IAM 정책 상태를 표시합니다. 자세한 정보는 [IAM(Identity and Access Management)으로 사용자 액세스 관리](/docs/services/Registry?topic=registry-iam#iam) 및 [사용자 액세스 역할 정책 정의](/docs/services/Registry?topic=registry-user#user)를 참조하십시오.

```
ibmcloud cr iam-policies-status
```
{: codeblock}

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

특정 이미지에 대한 세부사항을 표시합니다.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(선택사항) Go 템플리트를 사용하여 출력 요소를 형식화합니다.

자세한 정보는 [{{site.data.keyword.registrylong_notm}} 명령에 대한 CLI 출력 형식화 및 필터링](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)을 참조하십시오.

</dd>
<dt>`IMAGE`</dt>
<dd>보고서를 가져올 이미지의 이름입니다. 각 이름 사이에 공백을 사용하여 명령에 각 이미지를 나열하면 여러 이미지를 검사할 수 있습니다.

<p>이미지의 이름을 찾으려면 `ibmcloud cr image-list`를 실행하십시오. **저장소** 및 **태그** 열의 컨텐츠를 결합하여 `repository:tag` 형식의 이미지 이름을 작성하십시오. 이미지 이름에 태그를 지정하지 않은 경우 `latest`로 태그 지정된 이미지가 검사됩니다. </p>

</dd>
</dl>

**예**

형식화 지시문 *`"{{ .Config.ExposedPorts }}"`*를 사용하여 *`us.icr.io/birds/bluebird:1`* 이미지용으로 노출된 포트에 대한 세부사항을 표시합니다.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

{{site.data.keyword.cloud_notm}} 계정의 모든 이미지를 표시합니다.

이미지 이름은 `repository:tag` 형식으로 되어 있는 **저장소** 및 **태그** 열의 컨텐츠 조합입니다.
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--no-trunc`</dt>
<dd>(선택사항) 이미지 요약을 자르지 않습니다.</dd>
<dt>`--format FORMAT`</dt>
<dd>(선택사항) Go 템플리트를 사용하여 출력 요소를 형식화합니다.

자세한 정보는 [{{site.data.keyword.registrylong_notm}} 명령에 대한 CLI 출력 형식화 및 필터링](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)을 참조하십시오.

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(선택사항) 각 이미지가 `repository:tag` 형식으로 나열됩니다.</dd>
<dt>`--restrict RESTRICTION`</dt>
<dd>(선택사항) 지정된 네임스페이스 또는 네임스페이스와 저장소의 이미지만 표시하도록 출력을 제한합니다. </dd>
<dt>`--include-ibm`</dt>
<dd>(선택사항) 출력에 {{site.data.keyword.IBM_notm}} 제공 공용 이미지를 포함합니다. 이 옵션을 사용하지 않으면 기본적으로 개인용 이미지만 나열됩니다.</dd>
</dl>

**예**

이미지 요약을 자르지 않고 `repository:tag` 형식으로 *`birds`* 네임스페이스의 이미지를 표시합니다.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

{{site.data.keyword.registrylong_notm}}에서 하나 이상의 지정된 이미지를 삭제합니다.

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**

<dl>
<dt>`IMAGE`</dt>
<dd>삭제할 이미지의 이름입니다. 각 이름 사이에 공백을 사용하여 명령에 각 이미지를 나열하면 동시에 여러 이미지를 삭제할 수 있습니다. `IMAGE`는 `repository:tag` 형식이어야 합니다(예: `us.icr.io/namespace/image:latest`).

<p>이미지의 이름을 찾으려면 `ibmcloud cr image-list`를 실행하십시오. **저장소** 및 **태그** 열의 컨텐츠를 결합하여 `repository:tag` 형식의 이미지 이름을 작성하십시오. 이미지 이름에 태그를 지정하지 않은 경우 기본적으로 `latest`로 태그 지정된 이미지가 삭제됩니다.</p>

</dd>
</dl>

**예**
`us.icr.io/birds/bluebird:1` 이미지를 삭제합니다.

```
ibmcloud cr image-rm us.icr.io/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

{{site.data.keyword.registrylong_notm}}에서 소스 이미지 SOURCE_IMAGE를 참조하는 새 이미지 TARGET_IMAGE를 작성합니다. 소스 및 대상 이미지가 동일한 지역에 있어야 합니다.

이미지의 이름을 찾으려면 `ibmcloud cr image-list`를 실행하십시오. **저장소** 및 **태그** 열의 컨텐츠를 결합하여 `repository:tag` 형식의 이미지 이름을 작성하십시오.
{: tip}

```
ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`SOURCE_IMAGE`</dt>
<dd>소스 이미지의 이름입니다. `SOURCE_IMAGE`는 `repository:tag` 형식이어야 합니다(예: `us.icr.io/namespace/image:latest`).

</dd>
<dt>`TARGET_IMAGE`</dt>
<dd>대상 이미지의 이름입니다. `TARGET_IMAGE`는 `repository:tag` 형식이어야 합니다(예: `us.icr.io/namespace/image:latest`).

</dd>
</dl>

**예**

또 다른 태그 참조 `latest`를 `us.icr.io/birds/bluebird:1` 이미지에 추가하십시오.

```
ibmcloud cr image-tag  us.icr.io/birds/bluebird:1 us.icr.io/birds/bluebird:latest
```
{: pre}

`us.icr.io/birds/bluebird:peck` 이미지를 동일한 네임스페이스 `birds/pigeon` 내의 또 다른 저장소에 복사합니다.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/birds/pigeon:peck
```
{: pre}

`us.icr.io/birds/bluebird:peck` 이미지를 사용자가 액세스 권한을 가진 또 다른 네임스페이스인 `animals`로 복사합니다.

```
ibmcloud cr image-tag us.icr.io/birds/bluebird:peck us.icr.io/animals/dog:bark
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

로그인된 레지스트리의 이름과 계정을 표시합니다.

```
ibmcloud cr info
```
{: codeblock}

**전제조건**

없음

## `ibmcloud cr login`
{: #bx_cr_login}

이 명령은 레지스트리에 대해 `docker login` 명령을 실행합니다. `docker login` 명령은 레지스트리의 `docker push` 또는 `docker pull` 명령을 실행하는 데 필요합니다. 이 명령은 다른 `ibmcloud cr` 명령을 실행하는 데는 필요하지 않습니다. Docker가 설치되지 않은 경우 이 명령은 오류 메시지를 리턴합니다.

```
ibmcloud cr login
```
{: codeblock}

**전제조건**

없음

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

네임스페이스의 이름을 선택하여 {{site.data.keyword.cloud_notm}} 계정에 추가합니다.

```
ibmcloud cr namespace-add NAMESPACE
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`NAMESPACE`</dt>
<dd>추가할 네임스페이스입니다. 동일한 지역의 모든 {{site.data.keyword.cloud_notm}} 계정에서 네임스페이스가 고유해야 합니다. 네임스페이스는 4 - 30자이고 소문자, 숫자, 하이픈 및 밑줄만 포함해야 합니다. 네임스페이스는 문자 또는 숫자로 시작하고 끝나야 합니다.
  
<p>  
<strong>팁</strong>: 네임스페이스 이름에 개인 정보를 입력하지 마십시오.
</p>
  
</dd>
</dl>

**예**

이름이 *`birds`*인 네임스페이스를 작성합니다.

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

{{site.data.keyword.cloud_notm}} 계정이 소유한 모든 네임스페이스를 표시합니다.

```
ibmcloud cr namespace-list
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

{{site.data.keyword.cloud_notm}} 계정에서 네임스페이스를 제거합니다. 네임스페이스가 제거되면 이 네임스페이스의 이미지가 삭제됩니다.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`NAMESPACE`</dt>
<dd>제거할 네임스페이스입니다.</dd>
<dt>`--force`, `-f`</dt>
<dd>(선택사항) 명령이 사용자 프롬프트 없이 실행되도록 강제 실행합니다.</dd>
</dl>

**예**

네임스페이스 *`birds`*를 제거합니다.

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

가격 플랜을 표시합니다.

```
ibmcloud cr plan
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

표준 플랜으로 업그레이드합니다.

플랜에 대한 정보는 [레지스트리 플랜](/docs/services/Registry?topic=registry-registry_overview#registry_plans)을 참조하십시오.

```
ibmcloud cr plan-upgrade [PLAN]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`PLAN`</dt>
<dd>(선택사항) 업그레이드할 가격 플랜의 이름입니다. `PLAN`을 지정하지 않은 경우 기본값은 `standard`입니다.</dd>
</dl>

**예**

표준 가격 플랜으로 업그레이드합니다.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

[IBM Passport Advantage Online for customers ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/software/passportadvantage/pao_customer.html)에서 다운로드했으며 Helm과 함께 사용할 수 있도록 패키징된 {{site.data.keyword.IBM_notm}} 소프트웨어를 {{site.data.keyword.registrylong_notm}} 네임스페이스로 가져옵니다.

컨테이너 이미지가 개인용 {{site.data.keyword.registryshort_notm}} 네임스페이스로 푸시됩니다. Helm 차트는 명령을 실행하는 디렉토리에 작성된 `ppa-import` 디렉토리에 기록됩니다. 선택적으로 [Chart Museum 오픈 소스 프로젝트 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/helm/charts/tree/master/stable/chartmuseum)를 사용하여 Helm 차트를 호스팅할 수 있습니다.

```
ibmcloud cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
  <dt>`--archive FILE`</dt>
  <dd>IBM Passport Advantage에서 다운로드한 압축 파일의 경로입니다.</dd>
  <dt>`--namespace NAMESPACE`</dt>
  <dd>네임스페이스 중 하나입니다. 압축 파일의 컨테이너 이미지가 이 네임스페이스에 푸시됩니다. 네임스페이스를 나열하려면 `ibmcloud cr namespace-list`를 실행하십시오.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(선택사항) [Chart Museum ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 고유 리소스 ID입니다.</dd>
  <dt>`--chartmuseum-user USER`</dt>
  <dd>(선택사항) [Chart Museum ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 사용자 이름입니다.</dd>
  <dt>`--chartmuseum-password PASSWORD`</dt>
  <dd>(선택사항) [Chart Museum ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/helm/charts/tree/master/stable/chartmuseum) 비밀번호입니다.</dd>
</dl>

**예**

IBM 소프트웨어를 가져오고 Helm과 함께 사용하도록  {{site.data.keyword.registrylong_notm}} 네임스페이스 *`birds`*에 패키지합니다. 여기서 압축된 파일의 경로는 *`downloads/compressed_file.tgz`*입니다.

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

트래픽과 스토리지에 대한 현재 할당량 및 이 할당량에 대한 사용량 정보를 표시합니다.

```
ibmcloud cr quota
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

지정된 할당량을 수정합니다.

```
ibmcloud cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 구성하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_configure)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--traffic TRAFFIC`</dt>
<dd>(선택사항) 트래픽 할당량을 지정된 값(MB)으로 변경합니다. 트래픽 설정 권한을 부여받지 않았거나 현재 가격 플랜을 초과하는 값을 설정한 경우 조작이 실패합니다.</dd>
<dt>`--storage STORAGE`</dt>
<dd>(선택사항) 스토리지 할당량을 지정된 값(MB)으로 변경합니다. 스토리지 할당량 설정 권한을 부여받지 않았거나 현재 가격 플랜을 초과하는 값을 설정한 경우 조작이 실패합니다.</dd>
</dl>

**예**

가져오기 트래픽에 대한 할당량 한계를 *7000*MB로 설정하고 스토리지를 *600*MB로 설정합니다.

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

대상 지정된 지역 및 레지스트리를 표시합니다.

```
ibmcloud cr region
```
{: codeblock}

**전제조건**

없음

자세한 정보는 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)을 참조하십시오.

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

{{site.data.keyword.registrylong_notm}} 명령의 대상 지역을 설정합니다. 사용 가능한 지역을 나열하려면 매개변수 없이 명령을 실행하십시오.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**전제조건**

없음

**명령 옵션**
<dl>
<dt>`REGION`</dt>
<dd>(선택사항) 대상 지역의 이름(예: `us-south`)입니다.

자세한 정보는 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)을 참조하십시오.

</dd>
</dl>

**예**

미국 남부 지역을 대상으로 지정합니다.

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-add`
{: #bx_cr_token_add}

레지스트리에 대한 액세스를 제어하는 데 사용할 수 있는 토큰을 추가합니다.

```
ibmcloud cr token-add [--description DESCRIPTION] [--quiet | -q] [--non-expiring] [--readwrite]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [플랫폼 관리 역할](/docs/services/Registry?topic=registry-iam#platform_management_roles)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--description DESCRIPTION`</dt>
<dd>(선택사항) `ibmcloud cr token-list` 실행 시 표시되는 토큰에 대한 설명으로 값을 지정합니다. {{site.data.keyword.containerlong_notm}}에서 자동으로 토큰이 작성된 경우 설명이 Kubernetes 클러스터 이름으로 설정됩니다. 이 경우 클러스터가 제거되면 토큰이 자동으로 제거됩니다.
  
<p> 
  <strong>팁</strong>: 토큰 설명에 개인 정보를 입력하지 마십시오.
</p>

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(선택사항) 주변 텍스트 없이 토큰만 표시합니다.</dd>
<dt>`--non-expiring`</dt>
<dd>(선택사항) 만료되지 않는 액세스 권한이 있는 토큰을 작성합니다. 이 매개변수를 설정하지 않으면 기본적으로 24시간 후에 토큰의 액세스 권한이 만료됩니다.</dd>
<dt>`--readwrite`</dt>
<dd>(선택사항) 읽기 및 쓰기 액세스 권한이 부여된 토큰을 작성합니다. 이 옵션을 사용하지 않는 경우 기본적으로 액세스 권한은 읽기 전용입니다.</dd>
</dl>

**예**

만료되지 않고 읽기/쓰기 액세스 권한이 있는 토큰을 *Token for my account*라는 설명과 함께 추가합니다.

```
ibmcloud cr token-add --description "Token for my account" --non-expiring --readwrite
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

레지스트리에서 지정된 토큰을 검색합니다.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [플랫폼 관리 역할](/docs/services/Registry?topic=registry-iam#platform_management_roles)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`TOKEN`</dt>
<dd>검색할 토큰의 고유 ID입니다. 토큰을 나열하려면 `ibmcloud cr token-list`를 실행하십시오.</dd>
</dl>

**예**

*10101010-101x-1x10-x1xx-x10xx10xxx10* 토큰을 검색합니다.

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

{{site.data.keyword.cloud_notm}} 계정에 대해 존재하는 모든 토큰을 표시합니다.

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [플랫폼 관리 역할](/docs/services/Registry?topic=registry-iam#platform_management_roles)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(선택사항) Go 템플리트를 사용하여 출력 요소를 형식화합니다.

자세한 정보는 [{{site.data.keyword.registrylong_notm}} 명령에 대한 CLI 출력 형식화 및 필터링](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing)을 참조하십시오.

</dd>
</dl>

**예**

형식화 지시문 *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`*를 사용하여 읽기 전용인 모든 토큰을 표시합니다.

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

이 예는 다음과 같은 형식의 출력을 생성합니다.

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

하나 이상의 지정된 레지스트리 토큰을 제거합니다.

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [플랫폼 관리 역할](/docs/services/Registry?topic=registry-iam#platform_management_roles)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`TOKEN`</dt>
<dd>`ibmcloud cr token-list`에 표시되는 바와 같이, TOKEN은 토큰 자체이거나 토큰의 고유 ID일 수 있습니다. 여러 토큰을 지정할 수 있으며 공백으로 구분해야 합니다.</dd>
<dt>`--force`, `-f`</dt>
<dd>(선택사항) 명령이 사용자 프롬프트 없이 실행되도록 강제 실행합니다.</dd>
</dl>

**예**

*10101010-101x-1x10-x1xx-x10xx10xxx10* 토큰을 제거합니다.

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

이미지의 취약성 평가 보고서를 봅니다.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**전제조건**

필수 권한에 대한 정보를 찾으려면 [{{site.data.keyword.registrylong_notm}}를 사용하기 위한 액세스 역할](/docs/services/Registry?topic=registry-iam#access_roles_using)을 참조하십시오.

**명령 옵션**
<dl>
<dt>`IMAGE`</dt>
<dd>보고서를 가져올 이미지의 이름입니다. 보고서에서는 이미지에 알려진 패키지 취약성이 있는지 여부를 알립니다. 각 이름 사이에 공백을 사용하여 명령에 각 이미지를 나열하면 동시에 여러 이미지에 대한 보고서를 요청할 수 있습니다.

<p>이미지의 이름을 찾으려면 `ibmcloud cr image-list`를 실행하십시오. **저장소** 및 **태그** 열의 컨텐츠를 결합하여 `repository:tag` 형식의 이미지 이름을 작성하십시오. 이미지 이름에 태그를 지정하지 않은 경우 보고서에서는 `latest`로 태그 지정된 이미지를 평가합니다.</p>

<p>다음 운영 체제가 지원됩니다.

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux(RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

자세한 정보는 [Vulnerability Advisor를 사용하여 이미지 보안 관리](/docs/services/va?topic=va-va_index)를 참조하십시오.

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(선택사항) 명령 출력이 취약한 패키지의 수정사항에 대한 추가 정보를 표시합니다.</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(선택사항) 명령 출력이 취약성만 표시하도록 제한됩니다.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(선택사항) 명령 출력이 구성 문제만 표시하도록 제한됩니다.</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(선택사항) 선택한 형식으로 명령 출력이 리턴됩니다. 기본 형식은 `text`입니다. 다음 형식이 지원됩니다.

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**예**

이미지에 대한 표준 취약성 평가 보고서를 봅니다.

```
ibmcloud cr vulnerability-assessment us.icr.io/birds/bluebird:1
```
{: pre}

취약성만 표시하는 JSON 형식의 `us.icr.io/birds/bluebird:1` 이미지에 대한 취약성 평가 보고서를 봅니다.

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json us.icr.io/birds/bluebird:1
```
{: pre}
