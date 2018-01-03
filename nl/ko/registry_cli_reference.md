---

copyright:
  years: 2017
lastupdated: "2017-11-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 네임스페이스에서 Docker 이미지를 관리하기 위한 {{site.data.keyword.registrylong_notm}}(`bx cr`)
명령
{: #registry_cli_reference}

container-registry 플러그인을 사용하여 {{site.data.keyword.Bluemix}} 계정의 모든 사용자와 Docker 이미지를 공유하고 안전하게 저장할 수 있는, IBM이 호스팅하고 관리하는 개인용 레지스트리에서 고유의 이미지 네임스페이스를 설정할 수 있습니다.
{:shortdesc}


## bx cr 명령
{: #registry_cli_reference_bxcr}

{{site.data.keyword.registryshort_notm}} CLI에서 `bx cr` 명령을 실행하십시오.
{:shortdesc}

지원되는 명령은 [{{site.data.keyword.registrylong_notm}} CLI](../../cli/plugins/registry/index.html#containerregcli)를 참조하십시오.

## {{site.data.keyword.registrylong_notm}} 명령에 대한 CLI 출력 형식화 및 필터링
{: #registry_cli_listing}

지원되는 {{site.data.keyword.registrylong_notm}} 명령에 대한 CLI 출력을 형식화하고 필터링할 수 있습니다.
{:shortdesc}

기본적으로 CLI 출력은 사람이 읽을 수 있는 형식으로 표시됩니다. 그러나 이 보기는 특히 명령이 프로그래밍 방식으로 실행되는 경우 출력 사용 기능을 제한할 수 있습니다. 예를 들어, `bx cr image-list` CLI 출력에서 숫자 크기별로 `Size` 필드를 정렬할 수 있지만 명령에서 크기의 문자열 설명을 리턴합니다. container-registry 플러그인은 Go 템플리트를 CLI 출력에 적용하기 위해 사용할 수 있는 형식화 옵션을 제공합니다. Go 템플리트는 CLI 출력을 사용자 정의할 수 있는 [Go 프로그래밍 언어](https://golang.org/pkg/text/template/)의 기능입니다. 

다음 두 가지 방법으로 형식화 옵션을 적용하여 CLI 출력을 변경할 수 있습니다.

1.  CLI 출력에서 데이터를 형식화하십시오. 예를 들어, `Created` 필드 출력을 Unix 시간에서 표준 시간으로 변경하십시오.
2.  CLI 출력에서 데이터를 필터링하십시오. 예를 들어, Go 템플리트 `if gt` 조건을 사용하여 이미지의 특정 서브세트를 표시하려면 이미지 세부사항별로 필터링하십시오. 

다음 {{site.data.keyword.registrylong_notm}} 명령과 함께 형식화 옵션을 사용할 수 있습니다. 사용 가능한 필드와 해당 데이터 유형의 목록을 보려면 명령을 클릭하십시오. 

-   [`bx cr image-list `](registry_cli_reference.html#registry_cli_listing_imagelist)
-   [`bx cr image-inspect`](registry_cli_reference.html#registry_cli_listing_imageinspect)
-   [`bx cr token-list`](registry_cli_reference.html#registry_cli_listing_tokenlist)

다음 코드 예제는 형식화 및 필터링 옵션을 어떻게 사용할 수 있는지 보여줍니다.

-   사이즈가 1MB가 넘는 모든 이미지의 저장소, 태그 및 취약성 상태를 표시하려면 다음 `bx cr image-list` 명령을 실행하십시오. 

    ```
    bx cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .Vulnerable }}{{end}}"
    ```
    {: pre}

    출력 예: 

    ```
    example-registry.<region>.bluemix.net/user1/ibmliberty:latest OK
    example-registry.<region>.bluemix.net/user1/ibmnode:1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode:test1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode2:test2 Vulnerable
    ```
    {: screen}

-   지정된 IBM 공용 이미지에 대해 IBM 문서가 호스팅된 위치를 표시하려면 다음 `bx cr image-inspect` 명령을 실행하십시오. 

    ```
    bx cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"

    ```
    {: pre}

    출력 예: 

    ```
    map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
    ```
    {: screen}

-   지정된 이미지에 대한 노출된 포트를 표시하려면 다음 `bx cr image-inspect` 명령을 실행하십시오. 

    ```
    bx cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"

    ```
    {: pre}

    출력 예: 

    ```
    map[9080/tcp: 9443/tcp:]
    ```
    {: screen}

-   모든 읽기 전용 토큰을 표시하려면 다음 `bx cr token-list` 명령을 실행하십시오. 

    ```
    bx cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
    {: pre}

    출력 예: 

    ```
    0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
    ```
    {: screen}


### `bx cr image-list` 명령의 Go 템플리트 옵션 및 데이터 유형
{: #registry_cli_listing_imagelist}

`bx cr image-list` 명령에 사용 가능한 Go 템플리트 옵션 및 데이터 유형을 찾으려면 다음 표를 검토하십시오.
{:shortdesc}

|필드|유형|설명|
|-----|----|-----------|
|`Created`|정수(64비트)|[Unix 시간](https://en.wikipedia.org/wiki/Unix_time)의 초 수로 표시되는 이미지가 작성된 시간을 표시합니다. |
|`Digest`|문자열|이미지에 대한 고유 ID를 표시합니다. |
|`Namespace`|문자열|이미지가 저장된 네임스페이스를 표시합니다. |
|`Repository`|문자열|이미지의 저장소를 표시합니다. |
|`Size`|정수(64비트)|바이트 단위로 이미지의 크기를 표시합니다. |
|`Tag`|문자열|이미지에 대한 태그를 표시합니다. |
|`Vulnerable`|문자열|이미지에 대한 취약성 상태를 표시합니다. 가능한 상태는 [취약성 어드바이저를 사용하여 이미지 보안 관리](../va/va_index.html)에 설명되어 있습니다.|
{: caption="표 1. bx cr image-list 명령에서 사용 가능한 필드 및 데이터 유형." caption-side="top"}

### `bx cr image-inspect` 명령의 Go 템플리트 옵션 및 데이터 유형
{: #registry_cli_listing_imageinspect}

`bx cr image-inspect` 명령에 사용 가능한 Go 템플리트 옵션 및 데이터 유형을 찾으려면 다음 표를 검토하십시오.
{:shortdesc}

|필드|유형|설명|
|-----|----|-----------|
|`ID`|문자열|이미지에 대한 고유 ID를 표시합니다. |
|`Parent`|문자열|이 이미지를 빌드하는 데 사용된 상위 이미지의 ID를 표시합니다. |
|`Comment`|문자열|이미지의 설명을 표시합니다. |
|`Created`|문자열|이미지가 작성된 [Unix 시간소인](https://en.wikipedia.org/wiki/Unix_time)을 표시합니다. |
|`Container`|문자열|이미지를 작성한 컨테이너의 ID를 표시합니다. |
|`ContainerConfig`|오브젝트|이 이미지에서 시작된 컨테이너에 대한 기본 구성을 표시합니다. [Config](registry_cli_reference.html#config)의 필드 세부사항을 참조하십시오. |
|`DockerVersion`|문자열|이 이미지를 빌드하는 데 사용된 Docker 버전을 표시합니다. |
|`Author`|문자열|이미지의 작성자를 표시합니다. |
|`Config`|오브젝트|이미지에 대한 구성 메타데이터를 표시합니다. [Config](registry_cli_reference.html#config)의 필드 세부사항을 참조하십시오. |
|`Architecture`|문자열|이 이미지를 빌드하는 데 사용되고, 이미지를 실행하는 데 필요한 프로세서 아키텍처를 표시합니다. |
|`OS`|문자열|이 이미지를 빌드하는 데 사용되고, 이미지를 실행하는 데 필요한 운영 체제 제품군을 표시합니다. |
|`OsVersion`|문자열|이 이미지를 빌드하는 데 사용된 운영 체제의 버전을 표시합니다. |
|`Size`|정수(64비트)|바이트 단위로 이미지의 크기를 표시합니다. |
|`VirtualSize`|정수(64비트)|이미지에서 각 계층의 크기 합계를 바이트 단위로 표시합니다. |
|`RootFS`|오브젝트|이미지에 대한 루트 파일 시스템을 설명하는 메타데이터를 표시합니다. [RootFS](registry_cli_reference.html#rootfs)의 필드 세부사항을 참조하십시오. |
{: caption="표 2. bx cr image-inspect 명령에서 사용 가능한 필드 및 데이터 유형." caption-side="top"}

#### 구성

|필드|유형|설명|
|-----|----|-----------|
|`Hostname`|문자열|컨테이너의 호스트 이름을 정의합니다. |
|`Domainname`|문자열|컨테이너의 완전한 도메인 이름을 표시합니다. |
|`User`|문자열|이미지가 사용된 컨테이너 내부에서 명령을 실행하는 사용자를 표시합니다. |
|`AttachStdin`|부울|표준 입력 스트림이 컨테이너에 첨부된 경우 _true_를 표시하고 그렇지 않은 경우 _false_를 표시합니다. |
|`AttachStdout`|부울|표준 출력 스트림이 컨테이너에 첨부된 경우 _true_를 표시하고 그렇지 않은 경우 _false_를 표시합니다. |
|`AttachStderr`|부울|표준 오류 스트림이 컨테이너에 첨부된 경우 _true_를 표시하고 그렇지 않은 경우 _false_를 표시합니다. |
|`ExposedPorts`|키-값 맵핑|`[123:,456:]` 형식으로 노출된 포트의 목록을 표시합니다.|
|`Tty`|부울|pseudo-tty가 컨테이너에 할당된 경우 _true_를 표시하고 그렇지 않은 경우 _false_를 표시합니다. |
|`OpenStdin`|부울|표준 입력 스트림이 열린 경우 _true_를 표시하고 표준 입력 스트림이 닫힌 경우 _false_를 표시합니다. |
|`StdinOnce`|부울|접속된 클라이언트 연결이 끊어진 후에 표준 입력 스트림이 닫힌 경우 _true_를 표시하고 표준 입력 스트림이 계속 열려 있는 경우 _false_를 표시합니다. |
|`Env`|문자열의 배열|키-값 쌍의 형식으로 환경 변수의 목록을 표시합니다. |
|`Cmd `|문자열의 배열|컨테이너가 시작될 때 실행될 컨테이너에 전달되는 명령 및 인수를 설명합니다. |
|`Healthcheck`|오브젝트|컨테이너가 정상인지 확인하는 방법에 대해 설명합니다. [Healthcheck](registry_cli_reference.html#healthcheck)의 필드 세부사항을 참조하십시오. |
|`ArgsEscaped`|부울|명령이 이미 이스케이프된 경우 true를 표시합니다(Windows 특정). |
|`Image`|문자열|운영자에 의해 전달된 이미지의 이름을 표시합니다. |
|`Volumes`|키-값 맵핑|컨테이너에 마운트된 볼륨 마운트의 목록을 표시합니다. |
|`WorkingDir`|문자열|지정된 명령이 실행되는 컨테이너 내부의 작업 디렉토리를 표시합니다. |
|`Entrypoint`|문자열의 배열|컨테이너가 시작할 때 실행되는 명령을 설명합니다. |
|`NetworkDisabled`|부울|네트워킹을 컨테이너에 사용할 수 없는 경우 _true_를 표시하고 네트워킹을 컨테이너에 사용할 수 있는 경우 _false_를 표시합니다. |
|`MacAddress`|문자열|컨테이너에 지정된 MAC 주소를 표시합니다. |
|`OnBuild`|문자열의 배열|이미지 Dockerfile에 정의된 ONBUILD 메타데이터를 표시합니다. |
|`Labels`|키-값 맵핑|키-값 쌍으로 이미지에 추가된 레이블의 목록을 표시합니다. |
|`StopSignal`|문자열|컨테이너를 중지하려고 할 때 보내는 UNIX 중지 신호에 대해 설명합니다. |
|`StopTimeout`|정수|컨테이너를 중지하기 위한 제한시간을 초 단위로 표시합니다. |
|`Shell`|문자열의 배열|RUN, CMD, ENTRYPOINT의 쉘 형식을 표시합니다. |
{: caption="표. " caption-side="top"}

#### Healthcheck

|필드|유형|설명|
|-----|----|-----------|
|`Test`|문자열의 배열|상태 검사 테스트 수행 방법을 표시합니다. 사용 가능한 옵션은 다음과 같습니다.<ul><li>{}: 상태 검사 상속</li><li>{"NONE"}: 상태 검사 사용 안함</li><li>{"CMD", args...}: 인수 직접 실행</li><li>{"CMD-SHELL", command}: 시스템의 기본 쉘로 명령 실행</li></ul>|
|`Interval`|정수(64비트)|두 개의 상태 검사 사이에 대기하는 시간을 나노초 단위로 표시합니다. |
|`Timeout`|정수(64비트)|상태 검사를 실패한 것으로 간주하기 전에 대기하는 시간을 나노초 단위로 표시합니다. |
|`Retries`|정수|컨테이너를 비정상으로 간주하기 위해 필요한 연속적인 실패 수를 표시합니다. |
{: caption="표 4. Healthcheck 구조체에서 사용 가능한 필드 및 데이터 유형." caption-side="top"}

#### RootFS

|옵션 |유형|설명|
|------|----|-----------|
|`Type`|문자열|파일 시스템의 유형을 표시합니다. |
|`Layers`|문자열의 배열|각 이미지 계층의 디스크립터를 표시합니다. |
|`BaseLayer`|문자열|이미지에서 기본 계층에 대한 디스크립터를 표시합니다. |
{: caption="표 5. RootFS 구조체에서 사용 가능한 필드 및 데이터 유형." caption-side="top"}

### `bx cr token-list` 명령의 Go 템플리트 옵션 및 데이터 유형
{: #registry_cli_listing_tokenlist}

`bx cr token-list` 명령에 사용 가능한 Go 템플리트 옵션 및 데이터 유형을 찾으려면 다음 표를 검토하십시오.
{:shortdesc}

|필드|유형|설명|
|-----|----|-----------|
|`ID`|문자열|토큰에 대한 고유 ID를 표시합니다. |
|`Expiry`|정수(64비트)|토큰이 만료되는 [Unix 시간소인](https://en.wikipedia.org/wiki/Unix_time)을 표시합니다. |
|`ReadOnly`|부울|이미지를 가져오기만 가능할 때는 _true_를 표시하고 이미지를 네임스페이스에 푸시하고 네임스페이스에서 가져올 수 있을 때는 _false_를 표시합니다. |
|`Description`|문자열|토큰의 설명을 표시합니다. |
{: caption="표 6. bx cr token-list 명령에서 사용 가능한 필드 및 데이터 유형." caption-side="top"}
