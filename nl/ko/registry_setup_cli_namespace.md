---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.registrylong_notm}} CLI 및 레지스트리 네임스페이스 설정
{: #registry_setup_cli_namespace}

{{site.data.keyword.registrylong}}에 Docker 이미지를 저장하려면 먼저 {{site.data.keyword.Bluemix_notm}} CLI 및 container-registry 플러그인을 설치하고 {{site.data.keyword.registrylong_notm}}에서 고유한 이미지 저장소를 작성하기 위한 레지스트리 네임스페이스를 설정해야 합니다.
{:shortdesc}

컨테이너 이미지, 네임스페이스 이름, 설명 필드(예: 레지스트리 토큰) 또는 이미지 구성 데이터(예: 이미지 이름 또는 이미지 레이블)에 개인 정보를 입력하지 마십시오.
{:tip}

시작하기 전에 [{{site.data.keyword.Bluemix_notm}} CLI ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://clis.ng.bluemix.net/ui/home.html)를 설치하십시오. 


## {{site.data.keyword.registrylong_notm}} CLI(container-registry 플러그인) 설치
{: #registry_cli_install}

{{site.data.keyword.Bluemix_notm}} 개인용 레지스트리에서 Docker 이미지 및 네임스페이스를 관리하기 위해 명령행을 사용하도록 {{site.data.keyword.registrylong_notm}} CLI를 설치합니다.
{:shortdesc}

1.  [container-registry 플러그인을 설치](index.html#registry_cli_install)하십시오.
2.  선택사항: [루트 권한 없이 명령을 실행하도록 Docker 클라이언트를 구성](https://docs.docker.com/engine/installation/linux/linux-postinstall)하십시오. 이 단계를 수행하지 않은 경우 `sudo`를 사용하여, 또는 root로 `ibmcloud login`, `ibmcloud cr login`, `docker pull` 및 **docker push** 명령을 실행해야 합니다. 

이제 {{site.data.keyword.registrylong_notm}} 개인용 레지스트리에서 고유의 네임스페이스를 설정할 수 있습니다.

## container-registry 플러그인 업데이트
{: #registry_cli_update}

새 기능을 사용하기 위해 {{site.data.keyword.registrylong_notm}} CLI를 주기적으로 업데이트하고자 할 수 있습니다.
{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2.  container-registry 플러그인을 업데이트하십시오.

    ```
    ibmcloud plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  플러그인이 업데이트되었는지 확인하십시오.

    ```
    ibmcloud plugin list
    ```
     {: pre}


## container-registry 플러그인 설치 제거
{: #registry_cli_uninstall}

container-registry 플러그인이 더 이상 필요하지 않으면 설치 제거할 수 있습니다.
{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2.  container-registry 플러그인을 설치 제거하십시오.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

3.  플러그인이 설치 제거되었는지 확인하십시오.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    container-registry 플러그인이 결과에 표시되지 않습니다.


## 네임스페이스 설정
{: #registry_namespace_add}

Docker 이미지를 안전하게 저장하려면 {{site.data.keyword.registrylong_notm}} 개인용 레지스트리에서 네임스페이스를 작성해야 합니다.
{:shortdesc}

시작하기 전에:

-   [{{site.data.keyword.Bluemix_notm}} CLI 및 container-registry 플러그인을 설치](#registry_cli_install)하십시오.
-   [레지스트리 네임스페이스의 사용 방법 및 이름 지정 방법을 계획](registry_overview.html#registry_namespaces)하십시오.

네임스페이스를 작성하려면 시작 문서의 [네임스페이스 설정](index.html#registry_namespace_add)을 참조하십시오.

이제 [{{site.data.keyword.Bluemix_notm}} 레지스트리의 네임스페이스로 Docker 이미지를 푸시](registry_images_.html#registry_images_pushing)하고 계정의 다른 사용자와 해당 이미지를 공유할 수 있습니다.

## 네임스페이스 제거
{: #registry_remove}

더 이상 레지스트리 네임스페이스가 필요하지 않으면 {{site.data.keyword.Bluemix_notm}} 계정에서 네임스페이스를 제거할 수 있습니다.
{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2.  사용 가능한 네임스페이스를 나열하십시오.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3.  네임스페이스를 제거하십시오.

    **주의:** 네임스페이스를 제거하면 해당 네임스페이스에 저장된 이미지도 삭제됩니다. 이 조치는 실행 취소할 수 없습니다.

    _&lt;my_namespace&gt;_를 제거하려는 네임스페이스로 대체하십시오.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    네임스페이스를 삭제한 후에는 저장된 이미지의 수에 따라서 그 네임스페이스를 다시 재사용할 수 있게 되려면 몇 분이 걸릴 수 있습니다.
