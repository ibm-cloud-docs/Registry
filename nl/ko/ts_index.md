---

copyright:
  years: 2017
lastupdated: "2017-10-30"

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

{{site.data.keyword.registrylong}} 사용에 대한 공통 문제점 해결 질문에 대한 답변입니다.{:shortdesc}


## {{site.data.keyword.registrylong_notm}}에 대한 도움 및 지원 받기
{: #gettinghelp}

{{site.data.keyword.registrylong_notm}}를 사용하는 중에
문제점이나 질문이 있으면 정보를 검색하거나 포럼을 통해 질문을 함으로써 도움을 받을 수 있습니다. 또는 {{site.data.keyword.IBM_notm}} 지원 티켓을 열 수도 있습니다. 

포럼을 사용하여 질문을 할 때는 {{site.data.keyword.registrylong_notm}} 개발 팀에서 볼 수 있도록 질문에 태그를 지정하십시오. 

-   {{site.data.keyword.registrylong_notm}}로 앱을 개발하거나 배치하는 데 관한 기술적 질문이 있는 경우, [Stack
Overflow](http://stackoverflow.com/search?q=+ibm-bluemix)에 질문을 게시하고 ibm-bluemix 및 container-registry로 질문에 태그를 지정하십시오.
-   서비스 및 시작하기 지시사항에 대한 질문의 경우에는
[IBM
developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) 포럼을 사용하십시오. bluemix 및 container-registry 태그를 포함하십시오. 

포럼 사용에 대한 세부사항은
[도움 받기](../../support/index.html#getting-help)를 참조하십시오. 

{{site.data.keyword.IBM_notm}} 지원 티켓 열기에 대한 정보나 지원 레벨 및 티켓 심각도에 대한 정보는 [지원 문의](../../support/index.html#contacting-support)를 참조하십시오. 

## {{site.data.keyword.registrylong_notm}}에 로그인 실패
{: #ts_login}

{{site.data.keyword.registrylong_notm}}에 로그인할 수 없습니다. 

{: tsSymptoms}
`bx cr login` 명령이 실패합니다. 

{: tsCauses}
-   container-registry 플러그인의 유효 기간이 지났으므로 업데이트해야 합니다.
-   Docker가 로컬 시스템에 설치되어 있지 않거나 실행 중이지 않습니다.
-   {{site.data.keyword.Bluemix_notm}} 로그인 신임 정보가 만료되었습니다.

{: tsResolve}
다음과 같은 방법으로 이 문제점을 해결할 수 있습니다.

-   최신 버전의 {{site.data.keyword.registryshort_notm}} 플러그인으로 업그레이드하려면 [{{site.data.keyword.registrylong_notm}}(`bx cr`) 플러그인](registry_setup_cli_namespace.html#registry_cli_update)을 참조하십시오.
-   Docker가 시스템에 설치되어 있는지 확인하십시오. 이미 설치된 경우 Docker 디먼을 다시 시작하십시오.
-   `bx login` 명령을 다시 실행하여 {{site.data.keyword.Bluemix_notm}} 로그인 신임 정보를 새로 고치십시오.


## {{site.data.keyword.registrylong_notm}} commands fail with `'cr' is not a registered command. See 'bx help'. `
{: #ts_login_error}

`cr`은 등록된 `bx` 명령이 아니므로 `bx cr` 명령을 실행할 수 없습니다.

{: tsSymptoms}
다음 오류 메시지 중 하나와 비슷한 오류 메시지가 표시됩니다. 

```
bx cr login 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

```
bx cr namespace 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

{: tsCauses}
-   container-registry 플러그인이 설치되지 않았습니다.


{: tsResolve}
다음과 같은 방법으로 이 문제점을 해결할 수 있습니다.

-   container-registry 플러그인을 설치하려면 [{{site.data.keyword.registryshort_notm}} CLI(bx cr) 플러그인 설치](registry_setup_cli_namespace.html#registry_cli_install)를 참조하십시오.


## 네임스페이스 설정 실패
{: #ts_problem}

{: tsSymptoms}
`bx cr namespace-add`를 실행하면 입력한 값을 네임스페이스로 설정할 수 없습니다.

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
You have exceeded your pull traffic quota for the current month. Review your pull traffic quota and pricing plan
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

-   [Docker가 사용자의 시스템에 설치되어 있는지 확인하십시오](index.html#registry_cli_install).
-   Docker 설치 경로를 확인하십시오. 
-   `bx login`을 실행하여 {{site.data.keyword.Bluemix_notm}}에
로그인하십시오. 그리고 나서 `bx cr login`을 실행하여 {{site.data.keyword.registrylong_notm}} CLI에 로그인하십시오. 
-   [{{site.data.keyword.registrylong_notm}}에서 Docker 이미지를 저장하고 가져오기 위한 할당량 한계 및 사용량을 검토하십시오](registry_quota.html#registry_quota_get).

## latest 태그를 사용하여 최신 이미지를 가져올 수 없음
{: #ts_docker_latest}

{: tsSymptoms}
사용자가 `docker pull` 명령을 실행했지만
해당 명령에서 최신 버전 빌드가 아닌 이미지 버전을 리턴했습니다. 

{: tsCauses}
태그 값을 지정하지 않고 Docker 명령을 실행할 때 이미지를 참조하도록 `latest` 태그가 기본적으로
적용됩니다. `latest` 태그는 최신 태그 값이 명시적으로 설정되지 않은 상태로 실행된
`docker build` 또는 `docker tag` 명령에
적용됩니다. 따라서 순서와 상관없이 `docker` 명령을 실행하거나
일부 이미지에 명시적으로 태그를 설정하고 최신이 아닌 빌드를 참조하도록 `latest` 태그를 지정하는 것이 가능합니다. 

{: tsResolve}
일반적으로, 매번 사용자의 이미지에 다른 순차 태그를 명시적으로
정의하고, `latest` 태그에 의존하지 않는 것이 더 좋습니다. 

## 사용자 정의 방화벽이 있는 레지스트리 액세스에 실패
{: #ts_firewall}

{: tsSymptoms}
인바운드 및 아웃바운드 네트워크 트래픽의 사용자 정의 설정을 통해
개발 환경에 추가 방화벽을 설정합니다. {{site.data.keyword.registrylong_notm}}에 액세스하려고 하면 연결에 실패합니다. 

{: tsCauses}
사용자 정의 트래픽에서 인바운드 및 아웃바운드 네트워크 트래픽용으로
특정 네트워크 그룹을 열어야 레지스트리와 통신할 수 있습니다.

{: tsResolve}
사용자 정의된 방화벽에서 다음 네트워크 그룹을 여십시오. 

1.  {{site.data.keyword.registrylong_notm}}에 연결하는 데 사용하려는 시스템의 공인 IP 주소를 참고하십시오. Kubernetes를 사용 중인 경우
작업자 노드의 공인 IP 주소를 사용하십시오. `bx cs workers <cluster_name_or_id>`를 실행하여 작업자 노드의 공인 IP 주소를 검색하십시오. 여기서 *&lt;cluster_name_or_id&gt;*는 클러스터의 ID 또는 이름입니다.
2.  방화벽에서 시스템과의 다음 연결을 허용하십시오. 
    -   시스템에 대한 INBOUND 연결의 경우 다음 소스 네트워크 그룹에서
시스템의 대상 공인 IP 주소로 수신 네트워크 트래픽을 허용하십시오. 

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

    -   시스템에 대한 OUTBOUND 연결의 경우 동일한 네트워크 그룹을 사용하고 시스템의 소스 공인 IP 주소에서
해당 네트워크 그룹으로 발신 네트워크 트래픽을 허용하십시오. 

