---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, Docker build command, delete images, add images, pull images, push images, copy images, delete private repositories,

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

# 네임스페이스에 이미지 추가
{: #registry_images_}

{{site.data.keyword.registrylong}}의 네임스페이스에 이미지를 추가하여 Docker 이미지를 안전하게 저장하고 다른 사용자와 공유할 수 있습니다.
{:shortdesc}

네임스페이스에 추가할 모든 이미지는 먼저 로컬 컴퓨터에 있어야 합니다. 다른 저장소에서 로컬 컴퓨터로 이미지를 다운로드(가져오기)하거나, Docker `build` 명령을 사용하여 Dockerfile에서 고유의 이미지를 빌드할 수 있습니다. 네임스페이스에 이미지를 추가하려면 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 로컬 이미지를 업로드(푸시)해야 합니다.

컨테이너 이미지, 네임스페이스 이름, 설명 필드 또는 모든 이미지 구성 데이터(예: 이미지 이름 또는 이미지 레이블)에 개인 정보를 입력하지 마십시오.
{: important}

## 다른 레지스트리에서 이미지 가져오기
{: #registry_images_pulling_reg}

개인용 또는 공용 레지스트리 소스에서 이미지를 가져온(다운로드) 후에 {{site.data.keyword.registrylong_notm}}에서 나중에 사용할 수 있도록 태그를 지정할 수 있습니다.
{:shortdesc}

<img src="images/images_pull.svg" width="800" style="width:800px;" alt="개인용 또는 공용 레지스트리의 이미지를 컴퓨터로 가져옵니다."/>

**시작하기 전에**

- 네임스페이스의 이미지로 작업하려면 [CLI를 설치](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)하십시오.
- [{{site.data.keyword.registrylong_notm}}에서 고유의 네임스페이스를 설정](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)하십시오.
- [루트 권한 없이 Docker 명령을 실행할 수 있는지 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/install/linux/linux-postinstall/)하십시오. 루트 권한이 필요하도록 Docker 클라이언트가 설정된 경우, `sudo`를 사용하여 `ibmcloud login`, `ibmcloud cr login`, `docker pull` 및 `docker push` 명령을 실행해야 합니다.

  루트 권한 없이 Docker 명령을 실행하도록 권한을 변경하는 경우 `ibmcloud login` 명령을 다시 실행해야 합니다.

이미지를 다운로드하고 시작하기 문서에서 [이미지 가져오기](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pulling)를 참조하십시오.

`unauthorized: authentication required` 또는 `denied: requested access to the resource is denied` 메시지가 표시되면 `ibmcloud cr login` 명령을 실행하십시오.
{:tip}

이미지를 가져와 네임스페이스에 대한 태그를 지정한 후에는 로컬 컴퓨터에서 네임스페이스로 이미지를 업로드(푸시)할 수 있습니다.

## 네임스페이스에 Docker 이미지 푸시
{: #registry_images_pushing_namespace}

이미지를 저장하고 다른 사용자와 공유하기 위해 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 이미지를 푸시(업로드)할 수 있습니다.
{:shortdesc}

<img src="images/images_push.svg" width="800" style="width:800px;" alt="사용자의 컴퓨터에서 {{site.data.keyword.registrylong_notm}}로 이미지 푸시"/>

**시작하기 전에**

- 네임스페이스의 이미지로 작업하려면 [CLI를 설치](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)하십시오.
- [{{site.data.keyword.registrylong_notm}}에서 고유의 네임스페이스를 설정](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)하십시오.
- 로컬 컴퓨터에서 이미지 [가져오기](#registry_images_pulling_reg) 또는 [빌드](#registry_images_creating)를 수행하고 네임스페이스 정보로 이미지에 태그를 지정하십시오.
- [루트 권한 없이 Docker 명령을 실행할 수 있는지 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/install/linux/linux-postinstall/)하십시오. 루트 권한이 필요하도록 Docker 클라이언트가 설정된 경우, `sudo`를 사용하여 `ibmcloud login`, `ibmcloud cr login`, `docker pull` 및 `docker push` 명령을 실행해야 합니다.

  루트 권한 없이 Docker 명령을 실행하도록 권한을 변경하는 경우 `ibmcloud login` 명령을 다시 실행해야 합니다.

이미지를 업로드(푸시)하려면 다음 단계를 완료하십시오.

1. CLI에 로그인하십시오.

   ```
   ibmcloud cr login
   ```
   {: pre}

   개인용 {{site.data.keyword.registrylong_notm}}에서 이미지를 가져오는 경우 로그인해야 합니다.
  {:tip}

2. 계정에서 사용 가능한 모든 네임스페이스를 보려면 `ibmcloud cr namespace-list` 명령을 실행하십시오.
3. [네임스페이스에 이미지를 업로드](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing)하십시오.

   `unauthorized: authentication required` 또는 `denied: requested access to the resource is denied` 메시지가 표시되면 `ibmcloud cr login` 명령을 실행하십시오.
   {:tip}

이미지를 {{site.data.keyword.registrylong_notm}}에 푸시한 후 다음 태스크 중 하나를 수행할 수 있습니다.

- [Vulnerability Advisor를 사용하여 보안을 관리](/docs/services/va?topic=va-va_index)함으로써 잠재적 보안 문제 및 취약성에 대한 정보를 찾습니다.
- [클러스터를 작성하고
이 이미지를 사용하여 컨테이너](/docs/containers?topic=containers-getting-started#getting-started)를 {{site.data.keyword.containerlong_notm}}의 클러스터에 배치합니다.

## 레지스트리 간에 이미지 복사
{: #registry_images_copying}

두 지역에 있는 사용자와 이미지를 공유할 수 있도록 한 지역의 레지스트리에서 이미지를 가져와 다른 지역의 레지스트리에 푸시할 수 있습니다.
{:shortdesc}

<img src="images/images_copy.svg" width="800" style="width:800px;" alt="개인용 또는 공용 레지스트리의 이미지를 개인용 {{site.data.keyword.cloud_notm}} 레지스트리에 복사합니다."/>

**시작하기 전에**

- 네임스페이스의 이미지로 작업하려면 [CLI를 설치](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)하십시오.
- [{{site.data.keyword.registrylong_notm}}에서 고유의 네임스페이스를 설정](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)하십시오.
- [루트 권한 없이 Docker 명령을 실행할 수 있는지 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/install/linux/linux-postinstall/)하십시오. 루트 권한이 필요하도록 Docker 클라이언트가 설정된 경우, `sudo`를 사용하여 `ibmcloud login`, `ibmcloud cr login`, `docker pull` 및 `docker push` 명령을 실행해야 합니다.

  루트 권한 없이 Docker 명령을 실행하도록 권한을 변경하는 경우 `ibmcloud login` 명령을 다시 실행해야 합니다.

두 레지스트리 간에 이미지를 복사하려면 다음 단계를 완료하십시오.

1. [레지스트리에서 이미지를 가져오십시오](#registry_images_pulling_reg).
2. [다른 레지스트리에 이미지를 푸시하십시오](#registry_images_pushing_namespace). 대상으로 지정하는 새 지역에 대한 올바른 도메인 이름을 사용해야 합니다.

이미지를 복사한 후 다음 태스크 중 하나를 수행할 수 있습니다.

- [Vulnerability Advisor를 사용하여 이미지 보안을 관리](/docs/services/va?topic=va-va_index)함으로써 잠재적 보안 문제 및 취약성에 대한 정보를 찾습니다.
- [클러스터를 작성하고
이 이미지를 사용하여 컨테이너](/docs/containers?topic=containers-getting-started#getting-started)를 {{site.data.keyword.containerlong_notm}}의 클러스터에 배치합니다.

## 소스 이미지를 참조하는 새 이미지 작성
{: #registry_images_source}

로그인한 지역에서 동일한 지역 내의 기존 이미지를 참조하는 {{site.data.keyword.registrylong_notm}}의 새 이미지를 작성하십시오. 이 조치는 Docker Engine 버전 1.12 이상을 사용하여 작성한 소스 이미지에 대해서만 지원됩니다.

이 메커니즘을 사용하여 작성된 새 이미지는 서명을 보유하지 않습니다. 새 이미지에 서명을 해야 하는 경우, 이 메커니즘을 사용하지 마십시오.
{: tip}

**시작하기 전에**

- 네임스페이스의 이미지로 작업하려면 [CLI를 설치](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)하십시오.
- 다른 이미지를 참조할 소스 이미지를 포함하는 {{site.data.keyword.registrylong_notm}}의 개인용 네임스페이스에 대한 액세스 권한이 있는지 확인하십시오.

명령에 대한 자세한 정보는 [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag)를 참조하십시오.

소스 이미지에서 새 이미지를 작성하려면 다음 단계를 완료하십시오.

1. CLI에 로그인하십시오.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. 다음 명령을 실행하여 새 참조를 추가하십시오. 여기서, `SOURCE_IMAGE`는 소스 이미지의 이름이며 `TARGET_IMAGE`는 대상 이미지의 이름입니다. 소스 및 대상 이미지가 동일한 지역에 있어야 합니다. `SOURCE_IMAGE` 및 `TARGET_IMAGE`는 `<REPOSITORY>:<TAG>` 형식이어야 합니다(예: `us.icr.io/namespace/image:latest`).

   ```
   ibmcloud cr image-tag [SOURCE_IMAGE] [TARGET_IMAGE]
   ```
   {: pre}

3. 다음 명령을 실행하여 이미지가 작성되었는지 확인하고 이미지가 소스 이미지와 동일한 이미지 요약으로 목록에 표시되는지 검사하십시오.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

## 네임스페이스와 사용할 Docker 이미지 빌드
{: #registry_images_creating}

{{site.data.keyword.cloud_notm}}에서 직접 Docker 이미지를 빌드하거나 로컬 컴퓨터에 고유 Docker 이미지를 작성하고 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 업로드(푸시)할 수 있습니다.
{:shortdesc}

**시작하기 전에**

- 네임스페이스의 이미지로 작업하려면 [CLI를 설치](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)하십시오.
- [{{site.data.keyword.registrylong_notm}}에서 고유의 네임스페이스를 설정](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_namespace_setup)하십시오.
- [루트 권한 없이 Docker 명령을 실행할 수 있는지 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/install/linux/linux-postinstall/)하십시오. 루트 권한이 필요하도록 Docker 클라이언트가 설정된 경우, `sudo`를 사용하여 `ibmcloud login`, `ibmcloud cr login`, `docker pull` 및 `docker push` 명령을 실행해야 합니다.

  루트 권한 없이 Docker 명령을 실행하도록 권한을 변경하는 경우 `ibmcloud login` 명령을 다시 실행해야 합니다.

Docker 이미지는 작성하는 모든 컨테이너의 기초가 됩니다. 이미지는 이미지를 빌드하는 지시사항이 포함된 파일인 Dockerfile에서 작성됩니다. Dockerfile은 앱, 해당 앱의 구성 및 그 종속 항목과 같이 개별적으로 저장되는 해당 지시사항의 빌드 아티팩트를 참조할 수 있습니다.

{{site.data.keyword.cloud_notm}} 컴퓨팅 리소스 및 인터넷 연결을 이용하거나 워크스테이션에 Docker가 설치되지 않은 경우 {{site.data.keyword.cloud_notm}}에서 직업 이미지를 빌드하십시오. 방화벽 뒤의 서버에 있는 빌드의 리소스에 액세스해야 하는 경우 로컬에서 이미지를 빌드하십시오.

고유 Docker 이미지를 빌드하려면 다음 단계를 완료하십시오.

1. 빌드 컨텍스트를 저장할 로컬 디렉토리를 작성하십시오. 빌드 컨텍스트에는 Dockerfile과 관련 빌드 아티팩트(예: 앱 코드)가 포함되어 있습니다. 명령행 창에서 이 디렉토리로 이동하십시오.
2. Dockerfile을 작성하십시오.
    1. 로컬 디렉토리에 Dockerfile을 작성하십시오.

        ```
    touch Dockerfile
        ```
        {: pre}

    2. 텍스트 편집기를 사용하여 Dockerfile을 여십시오. 최소한, 이미지를 빌드하려면 기본 이미지를 추가해야 합니다. `<source_image>`와 `<tag>`를 사용하려는 이미지 저장소와 태그로 대체하십시오. 다른 개인용 레지스트리의 이미지를 사용하는 경우, 이 {{site.data.keyword.registrylong_notm}}에서 이미지에 대한 전체 경로를 정의하십시오.

       ```
    FROM <source_image>:<tag>
       ```
       {: pre}

       **예제**
     공용 {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty(ibmliberty) 이미지를 기반으로 하는 Dockerfile을 작성하려면 다음 코드를 사용하십시오.

       ```
       FROM <region>.icr.io/ibmliberty:latest
       LABEL description="This is my test Dockerfile"
       EXPOSE 9080
       ```
       {: pre}

       이 예는 이미지 메타데이터에 레이블을 추가하고 포트 9080을 노출합니다. 사용할 수 있는 추가 Dockerfile 지시사항은 [Dockerfile 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/engine/reference/builder/)를 참조하십시오.

3. 이미지의 이름을 결정하십시오. 이미지 이름의 형식은 다음과 같아야 합니다.

   ```
   <region>.icr.io/<my_namespace>/<repo_name>:<tag>
   ```
   {: pre}

   여기서 `<my_namespace>`는 네임스페이스 정보이며, `<repo_name>`은 저장소 이름이고, `<tag>`는 이미지에 사용할 버전입니다. 네임스페이스를 찾으려면 `ibmcloud cr namespace-list` 명령을 실행하십시오.

4. Dockerfile을 포함하는 디렉토리의 경로를 기록해 두십시오. 작업 디렉토리를 빌드 컨텍스트가 저장된 위치로 설정한 상태에서 다음 단계의 명령을 실행하면 `<directory>`를 점(.)으로 바꿀 수 있습니다.
5. {{site.data.keyword.cloud_notm}}에서 직접 이미지를 빌드하거나, {{site.data.keyword.cloud_notm}}에 푸시하기 전에 로컬로 이미지를 빌드하고 테스트하십시오.
   - {{site.data.keyword.cloud_notm}}에서 직접 이미지를 빌드하려면 다음 명령을 실행하십시오.

     ```
    ibmcloud cr build -t <image_name> <directory>
     ```
     {: pre}

     여기서 `<image_name>`은 이미지 이름이며 `<directory>`는 디렉토리 경로입니다. 작업 디렉토리를 빌드 컨텍스트가 저장된 위치로 설정한 경우 명령을 실행하면 `<directory>`를 점(.)으로 바꿀 수 있습니다.
  
     `ibmcloud cr build` 명령에 대한 자세한 정보는 [{{site.data.keyword.registrylong_notm}} CLI](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_build)를 참조하십시오.

   - {{site.data.keyword.cloud_notm}}에 푸시하기 전에 로컬에서 이미지를 빌드하고 테스트하려면 다음 단계를 완료하십시오.
      1. 로컬 컴퓨터의 Dockerfile에서 이미지를 빌드하고 이미지 이름으로 태그를 지정하십시오.

         ```
      docker build -t <image_name> <directory>
         ```
         {: pre}

         여기서 `<image_name>`은 이미지 이름이며 `<directory>`는 디렉토리 경로입니다.

      2. 선택사항: 네임스페이스에 이미지를 푸시하기 전에 로컬 컴퓨터에서 이를 테스트하십시오.

         ```
      docker run <image_name>
         ```
         {: pre}

         `<image_name>`을 이미지 이름으로 대체하십시오.

      3. 이미지를 작성하고 여기에 사용자의 네임스페이스에 대한 태그를 지정한 후에 [{{site.data.keyword.registrylong_notm}}에서 네임스페이스로 이미지를 푸시](#registry_images_pushing_namespace)할 수 있습니다.

Vulnerability Advisor를 사용하여 이미지의 보안을 확인하려면 [Vulnerability Advisor로 이미지 보안 관리](/docs/services/va?topic=va-va_index)를 참조하십시오.

## API 키를 사용하여 이미지를 {{site.data.keyword.registrylong_notm}}에 푸시
{: #registry_api_key_push_image}

API 키를 사용하여 이미지를 {{site.data.keyword.registrylong_notm}}에 푸시하는 서비스 ID를 작성하십시오.
{:shortdesc}

1. 서비스 ID를 작성하십시오. [서비스 ID 작성 및 관련 작업 수행](/docs/iam?topic=iam-serviceids#serviceids)을 참조하십시오.
2. 레지스트리에 액세스할 수 있는 권한을 서비스 ID에 제공하는 정책을 작성하십시오(예: `Administrator` 및 `Manager` 역할). [Identity and Access Management를 사용한 사용자 액세스 관리](/docs/services/Registry?topic=registry-iam#iam)를 참조하십시오.
3. API 키를 작성하십시오. [서비스 ID의 API 키 작성](/docs/iam?topic=iam-serviceidapikeys#create_service_key)을 참조하십시오.
4. 이미지를 레지스트리에 푸시할 수 있도록 API 키를 사용하여 레지스트리에 로그인하십시오. [API 키를 사용하여 액세스 자동화](/docs/services/Registry?topic=registry-registry_access#registry_api_key_use)를 참조하십시오.
5. 이미지를 푸시하십시오. [Docker 이미지를 네임스페이스에 푸시](#registry_images_pushing_namespace)를 참조하십시오.

이제 클러스터를 사용하여 이미지를 가져올 수 있습니다. [이미지에서 컨테이너 빌드](/docs/containers?topic=containers-images#other_registry_accounts)를 참조하십시오.

## 개인용 {{site.data.keyword.cloud_notm}} 저장소에 있는 이미지에서 태그 제거
{: #registry_images_untag}

[`mcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag) 명령을 사용하여 태그를 이미지에서 제거하고 기본 이미지 및 기타 모든 태그를 그대로 남겨둘 수 있습니다.
{:shortdesc}

저장소 내에 동일한 이미지 요약에 대한 여러 태그가 존재하는 경우 기본 이미지 및 해당 태그를 모두 제거하려면 [개인용 {{site.data.keyword.cloud_notm}} 저장소에서 이미지 삭제](#registry_images_remove)를 참조하십시오.
{: tip}

CLI를 사용하여 태그를 제거하려면 다음 단계를 완료하십시오.

1. `ibmcloud login` 명령을 실행하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오.
2. 태그를 제거하려면 다음 명령을 실행하십시오.

   ```
   ibmcloud cr image-untag IMAGE
   ```
   {: pre}

   여기서 `IMAGE`는 `repository:tag` 형식으로 된 제거할 이미지의 이름입니다.

   이미지 이름에 태그를 지정하지 않은 경우 명령이 실패합니다. 명령에 각 개인용 {{site.data.keyword.cloud_notm}} 레지스트리 경로를 공백으로 구분하여 나열함으로써 여러 이미지에 대한 태그를 삭제할 수 있습니다.

   이미지의 이름을 찾으려면 `ibmcloud cr image-list`를 실행하십시오. **저장소** 및 **태그** 열의 컨텐츠를 결합하여 `repository:tag` 형식의 이미지 이름을 작성하십시오.
   {:tip}

3. 다음 명령을 실행하여 태그가 제거되었는지 확인하고 태그가 목록에 표시되지 않는지 검사하십시오.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

## 개인용 {{site.data.keyword.cloud_notm}} 저장소에서 이미지 삭제
{: #registry_images_remove}

그래픽 사용자 인터페이스(GUI) 또는 CLI를 사용하여 개인용 저장소에서 원치 않는 이미지를 삭제할 수 있습니다.
{:shortdesc}

개인용 저장소 및 해당 연관된 이미지를 삭제하려는 경우에는 [개인용 저장소 및 연관된 이미지 삭제](#registry_repo_remove)를 참조하십시오.

공용 {{site.data.keyword.IBM_notm}} 이미지는 개인용 {{site.data.keyword.cloud_notm}} 저장소에서 삭제할 수 없으며 할당량에 대해 계산되지 않습니다.

이미지 삭제는 실행 취소할 수 없습니다. 기존 배치에서 사용 중인 이미지를 삭제하면 스케일 업 또는 재스케줄(또는 둘 다)이 실패할 수 있습니다.
{: important}

저장소 내에 동일한 이미지 요약에 대한 여러 태그가 존재하는 경우 [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm) 명령은 기본 이미지와 해당 태그를 모두 제거합니다. 동일한 이미지가 다른 저장소 또는 네임스페이스에 있으면 해당 이미지 사본이 제거되지 않습니다. 이미지에서 태그를 제거하고 기본 이미지 및 기타 모든 태그를 그대로 남겨두려면 [개인용 {{site.data.keyword.cloud_notm}} 저장소에 있는 이미지에서 태그 제거](#registry_images_untag) 명령을 참조하십시오.
{: tip}

### CLI를 사용하여 개인용 {{site.data.keyword.cloud_notm}} 저장소에서 이미지 삭제
{: #registry_images_remove_cli}

CLI를 사용하여 개인용 저장소에서 원치 않는 이미지 및 해당 태그를 모두 삭제할 수 있습니다.
{:shortdesc}

이미지 삭제는 실행 취소할 수 없습니다. 기존 배치에서 사용 중인 이미지를 삭제하면 스케일 업 또는 재스케줄(또는 둘 다)이 실패할 수 있습니다.
{: important}

CLI를 사용하여 이미지를 삭제하려면 다음 단계를 완료하십시오.

1. `ibmcloud login` 명령을 실행하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오.
2. 이미지를 삭제하려면 다음 명령을 실행하십시오.

   ```
   ibmcloud cr image-rm IMAGE
   ```
   {: pre}

   여기서 `IMAGE`는 `repository:tag` 형식으로 된 제거할 이미지의 이름입니다.

   이미지 이름에 태그가 지정되지 않은 경우에는 `latest`로 태그 지정된 이미지가 기본적으로 삭제됩니다. 명령에 각 개인용 {{site.data.keyword.cloud_notm}} 레지스트리 경로를 공백으로 구분하여 나열함으로써 여러 이미지를 삭제할 수 있습니다.

   이미지의 이름을 찾으려면 `ibmcloud cr image-list`를 실행하십시오. **저장소** 및 **태그** 열의 컨텐츠를 결합하여 `repository:tag` 형식의 이미지 이름을 작성하십시오.
   {:tip}

3. 다음 명령을 실행하여 이미지가 삭제되었는지 확인하고 이미지가 목록에 표시되지 않는지 검사하십시오.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

### GUI를 사용하여 개인용 {{site.data.keyword.cloud_notm}} 저장소에서 이미지 삭제
{: #registry_images_remove_gui}

그래픽 사용자 인터페이스(GUI)를 사용하여 개인용 이미지 저장소에서 원치 않는 이미지 및 해당 태그를 모두 삭제할 수 있습니다.
{:shortdesc}

이미지 삭제는 실행 취소할 수 없습니다. 기존 배치에서 사용 중인 이미지를 삭제하면 스케일 업 또는 재스케줄(또는 둘 다)이 실패할 수 있습니다.
{: important}

GUI를 사용하여 이미지를 삭제하려면 다음 단계를 완료하십시오.

1. IBMid를 사용하여 {{site.data.keyword.cloud_notm}} 콘솔([https://cloud.ibm.com/login ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/login))에 로그인하십시오.
2. {{site.data.keyword.cloud_notm}} 계정이 여러 개인 경우 계정 메뉴에서 사용할 계정과 지역을 선택하십시오.
3. **카탈로그**를 클릭하십시오.
4. **컨테이너** 카테고리를 선택하고 **컨테이너 레지스트리** 타일을 클릭하십시오.
5. **이미지**를 클릭하십시오. 이미지 목록이 표시됩니다.
6. 삭제할 이미지가 포함된 행에서 선택란을 선택하십시오.

   이 조치는 실행 취소할 수 없으므로 올바른 이미지를 선택했는지 확인하십시오.
   {: important}

7. **이미지 삭제**를 클릭하십시오.

## 개인용 저장소 및 연관된 이미지 삭제
{: #registry_repo_remove}

그래픽 사용자 인터페이스(GUI)를 사용하여 더 이상 필요하지 않은 개인용 저장소 및 이와 연관된 이미지를 삭제할 수 있습니다.
{:shortdesc}

특정 저장소를 삭제하면 해당 저장소의 모든 이미지가 삭제됩니다. 이 조치는 실행 취소할 수 없습니다.
{: important}

**시작하기 전에**

보존할 이미지를 백업해야 합니다.

GUI를 사용하여 개인용 저장소를 삭제하려면 다음 단계를 완료하십시오.

1. IBMid를 사용하여 {{site.data.keyword.cloud_notm}} 콘솔([https://cloud.ibm.com/login ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/login))에 로그인하십시오.
2. {{site.data.keyword.cloud_notm}} 계정이 여러 개인 경우 계정 메뉴에서 사용할 계정과 지역을 선택하십시오.
3. **카탈로그**를 클릭하십시오.
4. **컨테이너** 카테고리를 선택하고 **컨테이너 레지스트리** 타일을 클릭하십시오.
5. **저장소**를 클릭하십시오. 개인용 저장소의 목록이 표시됩니다.
6. 삭제할 개인용 저장소가 포함된 행에서 선택란을 선택하십시오.

    이 조치는 실행 취소할 수 없으므로 올바른 저장소를 선택했는지 확인하십시오.
    {: important}

7. **저장소 삭제**를 클릭하십시오.
