---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# 문제점 해결
{: #ts_index}

{{site.data.keyword.registrylong}} 사용에 대한 공통 문제점 해결 질문에 대한 답변입니다.
{:shortdesc}


## {{site.data.keyword.registrylong_notm}}에 대한 도움 및 지원 받기
{: #gettinghelp}

{{site.data.keyword.registrylong_notm}}를 사용하는 중에 문제점이나 질문이 있으면 정보를 검색하거나 포럼을 통해 질문을 함으로써 도움을 받을 수 있습니다. 또는 {{site.data.keyword.IBM_notm}} 지원 티켓을 열 수도 있습니다.

포럼을 사용하여 질문을 할 때는 {{site.data.keyword.registrylong_notm}} 개발 팀에서 볼 수 있도록 질문에 태그를 지정하십시오.

-   {{site.data.keyword.registrylong_notm}}로 앱을 개발하거나 배치하는 데 관한 기술적 질문이 있는 경우, [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix)에 질문을 게시하고 `ibm-bluemix` 및 `container-registry`로 질문에 태그를 지정하십시오.
-   서비스 및 시작하기 지시사항에 대한 질문의 경우에는 [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) 포럼을 사용하십시오. `bluemix` 및 `container-registry` 태그를 포함하십시오.

포럼 사용에 대한 세부사항은 [지원 센터 사용](/docs/get-support/howtogetsupport.html#using-avatar)을 참조하십시오.

{{site.data.keyword.IBM_notm}} 지원 티켓 열기 또는 지원 레벨 및 티켓 심각도에 대한 정보는 [지원 티켓 열기](/docs/get-support/howtogetsupport.html#open-ticket)를 참조하십시오.

## {{site.data.keyword.registrylong_notm}}에 로그인 실패
{: #ts_login}

{{site.data.keyword.registrylong_notm}}에 로그인할 수 없습니다.

{: tsSymptoms}
`ibmcloud cr login` 명령이 실패합니다.

{: tsCauses}
-   container-registry 플러그인의 유효 기간이 지났으므로 업데이트해야 합니다.
-   Docker가 로컬 컴퓨터에 설치되어 있지 않거나 실행 중이 아닙니다. 
-   {{site.data.keyword.Bluemix_notm}} 로그인 신임 정보가 만료되었습니다.

{: tsResolve}
다음과 같은 방법으로 이 문제점을 해결할 수 있습니다.

-   최신 버전의 container-registry 플러그인으로 업그레이드하십시오. [container-registry 플러그인 업데이트](registry_setup_cli_namespace.html#registry_cli_update)를 참조하십시오.
-   Docker가 컴퓨터에 설치되어 있는지 확인하십시오. 이미 설치된 경우 Docker 디먼을 다시 시작하십시오.
-   `ibmcloud login` 명령을 다시 실행하여 {{site.data.keyword.Bluemix_notm}} 로그인 신임 정보를 새로 고치십시오.
  
## {{site.data.keyword.registrylong_notm}}에 대한 명령 실행이 실패하며 `FAILED You are not logged in to IBM Cloud.`가 나타남 
{: #ts_login_cloud}

{{site.data.keyword.Bluemix_notm}}에 로그인된 경우에도 {{site.data.keyword.registrylong_notm}}에서 명령을 실행할 수 없습니다.

{: tsSymptoms}
모든 `ibmcloud cr` 명령이 실패합니다.

{: tsCauses}
-   container-registry 플러그인의 유효 기간이 지났으므로 업데이트해야 합니다.

{: tsResolve}
다음과 같은 방법으로 이 문제점을 해결할 수 있습니다.

-   최신 버전의 container-registry 플러그인으로 업그레이드하십시오. [container-registry 플러그인 업데이트](registry_setup_cli_namespace.html#registry_cli_update)를 참조하십시오.



## {{site.data.keyword.registrylong_notm}} 명령이 `'cr' is not a registered command. See 'ibmcloud help'.`라는 메시지가 출력되며 실패함
{: #ts_login_error}

`cr`은 등록된 `ibmcloud` 명령이 아니므로 `ibmcloud cr` 명령을 실행할 수 없습니다.

{: tsSymptoms}
다음 오류 메시지 중 하나와 비슷한 오류 메시지가 표시됩니다.

```
ibmcloud cr login
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' is not a registered command. See 'ibmcloud help'.
```
{: pre}

{: tsCauses}
-   container-registry 플러그인이 설치되지 않았습니다.


{: tsResolve}
다음과 같은 방법으로 이 문제점을 해결할 수 있습니다.

-   container-registry 플러그인을 설치하십시오. [{{site.data.keyword.registryshort_notm}} CLI(container-registry 플러그인) 설치](registry_setup_cli_namespace.html#registry_cli_install)를 참조하십시오.


## 네임스페이스 설정 실패
{: #ts_problem}

{: tsSymptoms}
`ibmcloud cr namespace-add`를 실행할 때 입력한 값을 네임스페이스로 설정할 수 없습니다.

{: tsCauses}
-   다른 {{site.data.keyword.Bluemix_notm}} 조직에서 이미 사용 중인 네임스페이스 값을 입력했습니다.
-   네임스페이스가 최근에 삭제되었으며 그 이름을 재사용하고 있습니다. 삭제된 네임스페이스에
많은 리소스가 포함되어 있는 경우, {{site.data.keyword.registrylong_notm}}에서 아직 삭제를 완전하게 처리하지 못했을 수 있습니다.
-   네임스페이스 값에 올바르지 않은 문자를 사용했습니다.

{: tsResolve}
다음과 같은 방법으로 이 문제점을 해결할 수 있습니다.

-   리턴된 오류 메시지에 표시된 지시사항을 따르십시오.
-   올바른 네임스페이스를 입력했는지 확인하십시오.
    -   네임스페이스의 길이는 4 - 30자여야 합니다.
    -   네임스페이스는 하나 이상의 문자 또는 숫자로 시작해야 합니다.
    -   네임스페이스에는 소문자, 숫자 또는 밑줄(_)만 포함되어야 합니다.
-   네임스페이스에 대한 다른 값을 선택하십시오.
-   삭제했던 네임스페이스를 다시 작성 중이며 여기에 다수의 이미지가 포함된 경우, 나중에 다시 시도하십시오.


## Docker 이미지의 푸시 또는 가져오기 실패
{: #ts_pushpull}

{: tsSymptoms}
Docker 이미지를 푸시하거나 가져오기 위해 명령을 실행할 때 오류 메시지를 수신합니다. 오류
메시지는 근본 원인에 따라 다양합니다. 잠재적 오류 메시지는 다음과 같습니다.

```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan
```
{: screen}

```
You have exceeded your pull traffic quota for the current month. 
Review your pull traffic quota and pricing plan
```
{: screen}

```
unauthorized: authentication required
```
{: screen}

```
denied: requested access to the resource is denied
```
{: screen}

{: tsCauses}
-   Docker가 설치되지 않았습니다.
-   Docker 클라이언트가 {{site.data.keyword.registrylong_notm}}에 로그인되어 있지 않습니다.
-   {{site.data.keyword.Bluemix_notm}} 액세스 토큰이 만료되었습니다.
-   {{site.data.keyword.Bluemix_notm}} 계정에 설정된 스토리지 또는 가져오기 트래픽에 대한 할당량 한계를 초과했습니다.

{: tsResolve}
다음과 같은 방법으로 이 문제점을 해결할 수 있습니다.

-   [Docker가 사용자의 컴퓨터에 설치되어 있는지 확인](index.html#registry_cli_install)하십시오. 
-   Docker 설치 경로를 확인하십시오.
-   `ibmcloud login`을 실행하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 그 후 `ibmcloud cr login`을 실행하여 {{site.data.keyword.registrylong_notm}} CLI에 로그인하십시오.
-   [{{site.data.keyword.registrylong_notm}}에서 Docker 이미지를 저장하고 가져오기 위한 할당량 한계 및 사용량을 검토](registry_quota.html#registry_quota_get)하십시오.


## `latest` 태그를 사용하여 최신 이미지를 가져올 수 없음
{: #ts_docker_latest}

{: tsSymptoms}
사용자가 `docker pull` 명령을 실행했지만 해당 명령에서 빌드된 최신 버전이 아닌 이미지 버전을 리턴했습니다. 

{: tsCauses}
태그 값을 지정하지 않고 Docker 명령을 실행할 때 이미지를 참조하도록 `latest` 태그가 기본적으로 적용됩니다. `latest` 태그는 태그 값이 명시적으로 설정되지 않은 상태로 실행된 최신 `docker build` 또는 `docker tag` 명령에 적용됩니다. 따라서 순서와 상관없이 `docker` 명령을 실행하거나 일부 이미지에 명시적으로 태그를 설정하고 최신이 아닌 빌드를 참조하도록 `latest` 태그를 지정하는 것이 가능합니다.

{: tsResolve}
일반적으로, 매번 사용자의 이미지에 다른 순차 태그를 명시적으로 정의하고, `latest` 태그에 의존하지 않는 것이 더 좋습니다.


## 레지스트리에 다른 IBM 이미지를 추가할 수 없음
{: #ts_ppa}


{: tsSymptoms}
다른 IBM 제품(예: {{site.data.keyword.Bluemix_notm}} 프라이빗)에서 사용한 컨텐츠를 가져오려는 경우, 레지스트리의 [IBM Passport Advantage ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/software/passportadvantage/index.html)에서 이미지 및 기타 라이센스 부여된 소프트웨어를 저장할 수 없습니다.

{: tsCauses}
IBM Passport Advantage의 이미지 및 Helm 차트와 같은 소프트웨어 패키지는 `ibmcloud cr ppa-archive-load` 명령을 사용하여 레지스트리로 가져와야 합니다.

{: tsResolve}
시작하기 전에:
* `ibmcloud login [--sso]`를 실행하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.
* `ibmcloud cr login`을 실행하여 {{site.data.keyword.registrylong_notm}}에 로그인하십시오.
* 사용자의 클러스터로 [`kubectl` CLI의 대상을 지정](/docs/containers/cs_cli_install.html#cs_cli_configure)하십시오. 
* 클러스터에서 Helm을 아직 설정하지 않은 경우 [이제 클러스터에서 Helm을 설정](/docs/containers/cs_integrations.html#helm)하십시오.
* 조직 내에서 차트를 공유하려는 경우 [Chart Museum 오픈 소스 프로젝트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum)를 설치할 수 있습니다. 지시사항은 이 [developerWorks 레시피 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/)를 참조하십시오.


### {{site.data.keyword.Bluemix_notm}}에 사용할 IBM Passport Advantage 제품 가져오기

1.  [IBM Passport Advantage![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/software/passportadvantage/index.html)에서 가져올 압축 파일을 얻으십시오.

2.  사용할 지역을 대상으로 지정하십시오. 지역 이름을 모르는 경우 지역 없이 명령을 실행한 다음 지역을 선택하십시오.

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

3.  압축된 아카이브 파일을 가져오십시오. 압축 파일의 경로 및 이미지를 푸시할 레지스트리 네임스페이스를 지정하십시오.

    ```
    ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
    ```
    {: pre}

    이 명령은 압축 파일을 확장하고 포함된 이미지를 로컬 Docker 클라이언트로 로드한 다음 레지스트리의 네임스페이스로 이미지를 푸시합니다.
    
    IBM Passport Advantage 아카이브의 Helm 차트를 Chart Museum에 업로드하려는 경우에는 명령에 다음 옵션을 포함하십시오. `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **출력 예**
    
    ```
user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

    OK
    ```
    {: screen}

4.  압축 파일에 Helm 차트가 있는 경우 이러한 차트는 현재 작업 디렉토리에 작성된 아카이브 디렉토리 `ppa-import`에 배치됩니다. 디렉토리를 열어 Helm 차트 `<helm_chart>`의 이름을 가져온 다음 해당 값을 검사하십시오.

    ```
helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    이전 단계에서 차트를 Chart Museum에 업로드한 경우 `helm inspect`를 사용하여 Chart Museum에서 차트를 검사할 수 있습니다.
    {: tip}

5.  `helm inspect values` 명령으로 출력된 값에 따라 Helm 차트 `<helm_chart>`를 구성하십시오.

6.  `helm install` 명령을 사용하여 Helm 차트 `<helm_chart>`를 배치하십시오. `--set` 옵션을 사용하여 필요에 따라 차트에서 값을 대체할 수 있습니다.

    ```
helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## 사용자 정의 방화벽이 있는 레지스트리 액세스에 실패
{: #ts_firewall}

{: tsSymptoms}
인바운드 및 아웃바운드 네트워크 트래픽의 사용자 정의 설정을 통해 개발 환경에 추가 방화벽을 설정합니다. {{site.data.keyword.registrylong_notm}}에 액세스하려고 하면 연결에 실패합니다.

{: tsCauses}
사용자 정의 트래픽에서 인바운드 및 아웃바운드 네트워크 트래픽용으로 특정 네트워크 그룹을 열어야 레지스트리와 통신할 수 있습니다.

{: tsResolve}
사용자 정의된 방화벽에서 다음 네트워크 그룹을 여십시오.

1.  {{site.data.keyword.registrylong_notm}}에 연결하는 데 사용할 컴퓨터의 공인 IP 주소를 기록하십시오. Kubernetes를 사용 중인 경우 작업자 노드의 공인 IP 주소를 사용하십시오. `ibmcloud ks workers <cluster_name_or_id>`를 실행하여 작업자 노드의 공인 IP 주소를 검색하십시오. 여기서 *&lt;cluster_name_or_id&gt;*는 클러스터의 이름 또는 ID입니다.
2.  방화벽에서 사용자의 컴퓨터와 관련된 다음 연결을 허용하십시오. 
    -   사용자의 컴퓨터에 대한 인바운드 연결의 경우, 다음 소스 네트워크 그룹에서 컴퓨터의 대상 공인 IP 주소로의 수신 네트워크 트래픽을 허용하십시오. 

        `registry.bluemix.net`:

        ```
169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   사용자의 컴퓨터에 대한 아웃바운드 연결의 경우, 동일한 네트워크 그룹을 사용하고 컴퓨터의 소스 공인 IP 주소에서 해당 네트워크 그룹으로의 발신 네트워크 트래픽을 허용하십시오. 


## 누락되거나 손상된 키 복구
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
[신뢰할 수 있는 컨텐츠](registry_trusted_content.html) 사용 시 서명 키가 누락되었거나 손상되었으므로 신뢰할 수 있는 이미지를 더 이상 관리할 수 없습니다.

{: tsCauses}
저장소 또는 루트 키가 누락되었거나 손상되었습니다.

{: tsResolve}
누락되었거나 손상된 키 복구를 위한 옵션은 키 유형(저장소 또는 루트)에 따라 다릅니다.

*  [저장소 키](#trustedcontent_lostrepokey)의 경우 저장소의 새 서명 키 세트를 생성할 수 있습니다.
*  [루트 키](#trustedcontent_lostrootkey)의 경우 저장소 삭제를 요청하고 새 저장소를 작성할 수 있습니다.


### 저장소 키
{: #trustedcontent_lostrepokey}

저장소 키가 누락되었거나 손상된 경우 저장소의 새 서명 키 세트를 생성하십시오.
{:shortdesc}

순환시킬 수 있는 유일한 서명 역할은 `targets`이며 이는 저장소 관리자입니다. 다른 역할이 손상된 경우 이 역할에 대해 새 키를 생성하고 이전 키를 제거한 다음 새 키를 서명자로 추가하십시오.
{:tip}

시작하기 전에 처음 [서명된 이미지를 푸시](registry_trusted_content.html#trustedcontent_push)할 때 작성한 루트 키 비밀번호 문구를 검색하십시오.

1.  [Notary 프로젝트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli)의 CLI 버전을 설치하십시오. 

2.  [신뢰할 수 있는 컨텐츠 환경을 설정](registry_trusted_content.html#trustedcontent_setup)하십시오.

3.  이전 단계에서 사용한 내보내기 명령의 URL을 기록하십시오. 예를 들어, `https://registry.ng.bluemix.net:4443`입니다.

4.  레지스트리 토큰을 생성하십시오.

    ```
    ibmcloud cr token-add --readwrite
    ```
    {: pre}

5.	이 키로 서명된 컨텐츠를 더 이상 신뢰하지 않도록 키를 순환시키십시오. _&lt;URL&gt;_을 2단계에서 기록한 내보내기 명령의 URL로 바꾸고 _&lt;image&gt;_를 저장소 키가 손상된 이미지로 바꾸십시오.

    ```
notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	프롬프트가 표시되면 루트 키 비밀번호 문구를 입력하십시오. 그런 다음, 프롬프트가 표시되면 새 저장소의 새 루트 키 비밀번호 문구를 입력하십시오.

7.	새 서명 키를 사용하는 [서명된 이미지를 푸시](registry_trusted_content.html#trustedcontent_push)하십시오.


### 루트 키
{: #trustedcontent_lostrootkey}

루트 키가 손상된 경우 이 루트 키를 사용한 신뢰할 수 있는 컨텐츠 저장소를 업데이트할 수 없습니다.
{:shortdesc}

손상된 루트 키를 사용하는 저장소가 있는 [네임스페이스를 삭제](registry_setup_cli_namespace.html#registry_remove)할 수 있으며, 이렇게 하면 이미지와 신뢰 데이터가 삭제됩니다.

네임스페이스에 손상되지 않은 루트 키를 사용하는 저장소가 있는 경우(예: 프로덕션 이미지의 네임스페이스) 손상된 루트 키와 연관된 신뢰 데이터만 삭제할 수 있습니다. 지원 티켓을 여십시오.

1.  [{{site.data.keyword.Bluemix_notm}} 지원에 문의](/docs/get-support/howtogetsupport.html#getting-customer-support)하십시오. 문제에 대한 간략한 설명, 계정 ID 및 손상된 루트 키를 사용하는 이미지 저장소가 포함된 네임스페이스 목록을 포함하십시오.

2.  {{site.data.keyword.Bluemix_notm}}에서 문제를 처리한 후에는 로컬 컴퓨터에서 Docker Content Trust 저장소를 삭제하십시오. 

    * Linux 및 Mac 디렉토리: `~/.docker/trust/private` 및 `~/.docker/trust/tuf`

    * Windows 디렉토리: `%HOMEPATH%\.docker\trust\private` 및 `%HOMEPATH%\.docker\trust\tuf`

    루트 키가 손상되었으므로, 이 단계는 다른 신뢰 서버의 서명 키를 포함한 모든 서명 키를 삭제합니다.
    {:tip}

3.  {{site.data.keyword.containershort_notm}} 클러스터에서 [{{site.data.keyword.Bluemix_notm}} 이미지 적용](registry_security_enforce.html)을 사용하는 경우, 각 이미지 적용 팟(Pod)을 다시 시작하십시오. 팟(Pod)의 롤링 다시 시작을 자동으로 수행하도록 Kubernetes를 트리거하려는 경우에는 팟(Pod)의 일부 메타데이터를 변경할 수 있습니다. 예를 들어, [대상 클러스터에 Kubernetes CLI를 지정](/docs/containers/cs_cli_install.html#cs_cli_configure)하고 배치를 수정하십시오.

    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  신뢰할 수 있는 컨텐츠 저장소를 생성하십시오.

    *  새 신뢰할 수 있는 컨텐츠를 작성하려는 경우 [새 서명된 이미지를 푸시](registry_trusted_content.html#trustedcontent_push)하십시오.

    *  이전 신뢰할 수 있는 컨텐츠를 변경하지 않으려는 경우에는 레지스트리의 최신 이미지에 서명을 추가하십시오. 

       ```
docker trust sign <image>:<tag>
       ```
       {: pre}
       

## Container Image Security Enforcement의 설치가 실패하며 `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists.`가 나타남
{: #ts_install_cise_fail}

{: tsSymptoms}
Container Image Security Enforcement 설치가 실패했으며 다음 메시지를 수신했습니다.

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
이전 설치가 실패했으며 그 다음에 설치 제거를 수행했으나 설치와 연관된 일부 Kubenetes 작업이 제거되지 않았습니다.

{: tsResolve}
다음 명령을 실행하여 나머지 Kubenetes 작업을 제거하십시오.

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}


## 모든 작업자가 작동 중지 상태가 된 후 팟(Pod)이 다시 시작되지 않음
{: #ts_pods}


{: tsSymptoms}
모든 클러스터 작업자가 작동 중지 상태가 된 후 팟(Pod)이 다시 시작되지 않습니다. Container Image Security Enforcement는 배치되어 있습니다. 클러스터 작업자 상태가 정상으로 표시되지만 아무것도 스케줄되지 않습니다. 

{: tsCauses}
기본적으로 Container Image Security Enforcement는 실패 시 작동 중지(fail closed) 허가 웹훅을 추가합니다. 모든 Container Image Security Enforcement 팟(Pod)이 작동 중지 상태가 되면 팟(Pod)이 자기 자신의 복구를 승인할 수 없게 됩니다. 

{: tsResolve}
이 상태의 클러스터를 복구하려면 실패 시 작동 중지 대신 실패 시 작동(fail open)으로 웹훅 구성을 변경해야 합니다.  

다음 verb를
*  `GET`
*  `PATCH`

다음 대상에 사용하려면 충분한 역할 기반 액세스 제어(RBAC) 권한이 있어야 합니다. 
*  `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
*  `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration` 

RBAC에 대한 자세한 정보는 [사용자 정의 Kubernetes RBAC 역할을 사용하여 사용자에게 권한 부여](/docs/containers/cs_users.html#rbac) 및 [Kubernetes: Using RBAC Authorization
![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)을 참조하십시오. 

실패 시 작동 중지 대신 실패 시 작동으로 웹훅 구성을 변경한 후 하나 이상의 Container Image Security Enforcement 팟(Pod)이 실행 중인 경우 실패 시 작동 중지로 웹훅 구성을 복원하려면 다음 단계를 완료하십시오. 

1.  다음 명령을 실행하여 `MutatingWebhookConfiguration`을 업데이트하십시오. 

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    `failurePolicy`를 `Ignore`로 변경하고 저장한 후 닫으십시오. 

2.  다음 명령을 실행하여 `ValidatingWebhookConfiguration`을 업데이트하십시오. 

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    `failurePolicy`를 `Ignore`로 변경하고 저장한 후 닫으십시오. 

3.  임의의 Container Image Security Enforcement 팟(Pod)이 시작될 때까지 기다리십시오. 하나 이상의 팟(Pod)에 대한 **상태** 열이 `Running`을 표시할 때까지 다음 명령을 실행하여 팟(Pod)의 시작 여부를 확인할 수 있습니다. 

    ```
    kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
    ```
    {: pre}

4.  하나 이상의 Container Image Security Enforcement 팟(Pod)이 실행 중이면 다음 명령을 실행하여 `MutatingWebhookConfiguration`을 업데이트하십시오. 

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    `failurePolicy`를 `Fail`로 변경하고 저장한 후 닫으십시오. 

5.  다음 명령을 실행하여 `ValidatingWebhookConfiguration`을 업데이트하십시오. 

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    `failurePolicy`를 `Fail`로 변경하고 저장한 후 닫으십시오. 
