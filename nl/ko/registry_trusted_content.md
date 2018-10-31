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

# 신뢰할 수 있는 컨텐츠의 이미지에 서명
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}}에서는 사용자가 이미지에 서명하여 레지스트리 네임스페이스에서 이미지의 무결성을 보장할 수 있도록 신뢰할 수 있는 컨텐츠 기술을 제공합니다. 서명된 이미지를 가져오고 푸시하여 CI(Continuous Integration) 도구와 같이 올바른 당사자가 이미지를 푸시했는지 확인할 수 있습니다. 이 기능을 사용하려면 Docker 버전 1.11 이상이 있어야 합니다. [Docker Content Trust ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/engine/security/trust/content_trust/) 및 [Notary 프로젝트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/theupdateframework/notary) 문서를 검토하여 더 자세히 알아볼 수 있습니다.
{:shortdesc}

사용자가 신뢰할 수 있는 컨텐츠가 사용되는 이미지를 푸시할 때 Docker 클라이언트도 {{site.data.keyword.Bluemix_notm}} 신뢰 서버에 서명된 메타데이터 오브젝트를 푸시합니다. Docker Content Trust가 사용되는 태그 지정된 이미지를 가져올 때 Docker 클라이언트는 신뢰 서버에 접속하여 사용자가 요청한 태그의 서명된 최신 버전을 확립하고 컨텐츠 서명을 확인하고 서명된 이미지를 다운로드합니다.

이미지 이름은 저장소와 태그로 구성됩니다. 신뢰할 수 있는 컨텐츠를 사용할 때 각 저장소는 고유한 서명 키를 사용합니다. 저장소 내 각 태그는 저장소에 속한 키를 사용합니다. 여러 팀이 컨텐츠를 공개하는 경우, {{site.data.keyword.registrylong_notm}} 네임스페이스 내 고유 저장소마다 각 팀이 고유 키를 사용하여 해당 컨텐츠에 서명하면 사용자는 해당 팀에서 각 이미지가 생성되었음을 확인할 수 있습니다.

저장소에는 서명된 컨텐츠와 서명되지 않은 컨텐츠가 포함될 수 있습니다. Docker Content Trust를 사용하는 경우 서명되지 않은 다른 컨텐츠가 함께 있는 경우에도 저장소에 있는 서명된 컨텐츠에 액세스할 수 있습니다.

Docker Content Trust는 "trust on first use" 보안 모델을 사용합니다. 처음 저장소에서 서명된 이미지를 가져올 때 저장소 키를 신뢰 서버에서 가져오게 되며, 이 키는 향후 이 저장소에서 이미지를 확인하는 데 사용됩니다. 처음 저장소를 가져오려면 먼저 신뢰 서버 또는 이미지 및 해당 공개자를 신뢰하는지 확인해야 합니다. 서버의 신뢰 정보가 손상되었으며 전에 저장소에서 이미지를 가져오지 않은 경우 Docker 클라이언트가 신뢰 서버에서 손상된 정보를 가져올 수 있습니다. 처음 이미지를 가져온 후 신뢰 데이터가 손상된 경우 후속 가져오기에서 Docker 클라이언트가 손상된 데이터를 확인하는 데 실패하며 이미지를 가져오지 않습니다. 이미지의 신뢰 데이터를 검사하는 방법에 대한 자세한 정보는 [서명된 이미지 보기](#trustedcontent_viewsigned)를 참조하십시오.

"trust on first use" 보안 모델에 대한 자세한 정보는 [TUF(The Update Framework) ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://theupdateframework.github.io/)를 참조하십시오. 


## 신뢰할 수 있는 컨텐츠 환경 설정
{: #trustedcontent_setup}

기본적으로 Docker Content Trust는 사용으로 설정되지 않습니다. {{site.data.keyword.registrylong_notm}}에 로그인하고 서명된 이미지에 대한 작업을 수행하기 전에 Content Trust 환경을 사용으로 설정하십시오.
{:shortdesc}

1.  터미널에서 Docker Content Trust 환경 변수를 사용으로 설정하십시오.

    Linux 또는 Mac의 경우:

    ```
export DOCKER_CONTENT_TRUST=1
    ```
    {: codeblock}

    Windows의 경우:

    ```
set DOCKER_CONTENT_TRUST=1
    ```
    {: codeblock}

2.  {{site.data.keyword.Bluemix_notm}} CLI에 로그인하십시오.

    ```
    ibmcloud login [--sso]
    ```
    {: pre}

    연합 ID가 있는 경우에는 `ibmcloud login --sso`를 사용하여 로그인하십시오. 사용자 이름을 입력하고 CLI 출력에서 제공된 URL을 사용하여 일회성 패스코드를 검색하십시오. 로그인이 `--sso`가 없으면 실패하고 `--sso` 옵션이 있으면 성공하는 경우 연합 ID가 있는 것입니다.
    {:tip}

3.  사용할 지역을 대상으로 지정하십시오. 지역 이름을 모르는 경우 지역 없이 명령을 실행한 다음 지역을 선택할 수 있습니다.

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

4.  {{site.data.keyword.registrylong_notm}}에 로그인하십시오.

    ```
    ibmcloud cr login
    ```
    {: pre}

    출력에서는 Docker Content Trust 환경 변수를 내보내도록 지시합니다. 
    
    **예**

    ```
    user:~ user$ ibmcloud cr login
    Logging in to 'registry.ng.bluemix.net'...
    Logged in to 'registry.ng.bluemix.net'.

    컨텐츠 신뢰를 사용하도록 Docker 클라이언트를 설정하려면 다음 환경 변수를 내보내십시오.
    export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
    {: screen}

5.  터미널에서 환경 변수 명령을 복사하고 붙여넣으십시오. 예를 들어, 다음과 같습니다.

    ```
export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
    ```
    {: pre}


이제 신뢰할 수 있고 서명된 이미지를 푸시하고 가져오고 관리할 수 있습니다.

Docker Content Trust가 사용으로 설정된 세션 중에 신뢰할 수 있는 컨텐츠를 사용 안함으로 설정하여 조작을 수행하려는 경우(예: 서명되지 않은 이미지 가져오기) 명령과 함께 `--disable-content-trust` 플래그를 사용하십시오.
{: tip}

## 서명된 이미지 푸시
{: #trustedcontent_push}

서명된 이미지를 처음 푸시할 때 Docker가 서명된 키 쌍(루트 및 저장소)을 자동으로 작성합니다. 이전에 서명된 이미지를 푸시한 저장소에서 이미지에 서명하려면 이미지를 푸시하는 시스템에 올바른 저장소 서명 키를 로드해야 합니다.
{:shortdesc}

시작하기 전에 [레지스트리 네임스페이스를 설정](index.html#registry_namespace_add)하십시오.

1.  [신뢰할 수 있는 컨텐츠 환경을 설정](#trustedcontent_setup)하십시오.

2.  [이미지를 푸시](index.html#registry_images_pushing)하십시오. 태그는 신뢰할 수 있는 컨텐츠에 필수입니다. 명령 출력에 "Signing and pushing image metadata"가 표시됩니다.

3.  **서명된 저장소를 처음으로 푸시**하십시오. 새 저장소에 서명된 이미지를 푸시하면 명령이 두 개의 서명 키인 루트 키와 저장소 키를 작성하고 로컬 시스템에 저장합니다. 각 키에 대해 보안 비밀번호 문구를 입력하고 저장한 다음 [키를 백업](#trustedcontent_backupkeys)하십시오. [복구 옵션](ts_index.html#ts_recoveringtrustedcontent)이 제한되어 있으므로 키 백업이 중요합니다.


## 서명된 이미지 가져오기
{: #trustedcontent_pull}

Docker Content Trust가 사용되는 서명된 이미지를 처음 가져올 때 Docker 클라이언트가 서명을 신뢰할 수 있음으로 인식합니다. Docker 클라이언트가 사용자가 지정한 최신 서명 버전의 이미지를 가져옵니다. 서명되지 않은 이미지 또는 신뢰할 수 없는 컨텐츠는 가져오지 않습니다.
{:shortdesc}


1.  [신뢰할 수 있는 컨텐츠 환경을 설정](#trustedcontent_setup)하십시오.

2.  이미지를 가져오십시오. _&lt;source_image&gt;_를 이미지의 저장소로 바꾸고 _&lt;tag&gt;_는 사용할 이미지의 태그(예: _latest_)로 바꾸십시오. 가져올 수 있는 이미지를 나열하려면 `ibmcloud cr image-list`를 실행하십시오.

    ```
    docker pull <source_image>:<tag>
    ```
    {: pre}

    서명된 이미지를 푸시하거나 가져올 때 태그를 지정하십시오. `latest` 태그는 컨텐츠 신뢰가 사용되지 않는 경우에만 기본값으로 지정됩니다.
    {: tip}

## 신뢰할 수 있는 컨텐츠 관리
{: #trustedcontent_managetrust}

`docker trust` 명령을 사용하면 이미지에 서명한 사용자를 볼 수 있으며 신뢰 컨텐츠 상태를 철회할 수 있습니다. `docker trust` 명령을 실행하려면 Docker 17.12 이상이 필요합니다.
{:shortdesc}

### 서명된 이미지 보기
{: #trustedcontent_viewsigned}

키 ID와 서명자에 대한 정보를 포함해 서명된 버전의 이미지 저장소 또는 태그를 검토할 수 있습니다.
{:shortdesc}

1.  [신뢰할 수 있는 컨텐츠 환경을 설정](#trustedcontent_setup)하십시오.

2.  각 이미지의 태그, 요약 및 서명자 정보를 검토하십시오. 

    (선택사항) 해당 이미지 버전에 대한 정보를 보려면 태그 _&lt;tag&gt;_를 지정하십시오.

    ```
docker trust view <image>:<tag>
    ```
    {: pre}

### 신뢰 철회
{: #trustedcontent_revoketrust}

이미지의 신뢰할 수 있는 컨텐츠 상태를 철회할 수 있습니다.
{:shortdesc}

시작하기 전에 [신뢰할 수 있는 저장소를 처음 푸시](#trustedcontent_push)할 때 저장한 저장소 키 비밀번호 문구를 검색하십시오. 신뢰할 수 있는 이미지에 사용되는 키를 식별해야 하는 경우 `docker view` [명령](#trustedcontent_viewsigned)을 사용하십시오.

1.  [신뢰할 수 있는 컨텐츠 환경을 설정](#trustedcontent_setup)하십시오.

2.  이미지 저장소에 대한 신뢰할 수 있는 모든 메타데이터를 제거하십시오. 프롬프트가 표시되면 저장소 키 비밀번호 문구를 입력하십시오. **선택사항**: 이 버전의 이미지에 대한 신뢰할 수 있는 메타데이터를 철회하려면 태그를 지정하십시오.

    ```
docker trust revoke <image>:<tag>
    ```
    {: pre}

3.  신뢰할 수 있는 컨텐츠의 목록에서 신뢰가 철회되었는지 확인하십시오. **선택사항**: 태그 지정된 이미지에 대한 철회된 컨텐츠를 확인하려면 태그를 포함하십시오.

    ```
$ docker trust view <image>:<tag>

    No signatures for <image>:<tag>
    ```
    {: codeblock}


## 서명 키 백업
{: #trustedcontent_backupkeys}

사용자가 새 저장소에 서명된 이미지를 처음 푸시하면 Docker Content Trust가 두 개의 서명 키인 루트 키와 저장소 키를 작성하고 로컬 시스템에 저장합니다.

*  Linux 및 Mac 디렉토리: `~/.docker/trust/private`

*  Windows 디렉토리: `%HOMEPATH%\.docker\trust\private`

   Docker 구성 디렉토리를 변경한 경우 이 디렉토리에서 `trust` 서브디렉토리를 찾으십시오.
   {: tip}

모든 키, 특히 루트 키를 백업해야 합니다. 키가 유실되었거나 손상된 경우 [복구 옵션](ts_index.html#ts_recoveringtrustedcontent)이 제한됩니다.

키를 백업하려는 경우에는 [Docker Content Trust 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys)를 참조하십시오.


## 신뢰할 수 있는 서명자 관리
{: #trustedcontent_signers}

저장소의 서명 이미지에서 서명자를 제거하고 추가할 수 있습니다.
{:shortdesc}

### 신뢰할 수 있는 저장소에 서명자 추가
{: #trustedcontent_addsigners}

다른 사용자가 저장소의 이미지에 서명할 수 있게 하려면 이 저장소에 해당 사용자의 서명 키를 추가하십시오.
{:shortdesc}

시작하기 전에:
- 이미지 서명자에게 네임스페이스에 이미지를 푸시하는 권한이 있어야 합니다. 
- 저장소 소유자 및 추가 서명자의 경우 Docker 17.12 이상이 설치되어 있어야 합니다.
- [서명된 이미지를 푸시](#trustedcontent_push)하여 신뢰할 수 있는 컨텐츠 저장소를 작성하십시오. 저장소 소유자에게 로컬 시스템의 Docker 신뢰 폴더에서 사용 가능한 저장소의 저장소 관리 키가 있어야 합니다. 저장소 관리 키가 없는 경우에는 이 태스크를 대신 수행하도록 소유자에게 요청하십시오.

서명자를 추가하는 경우 이 저장소의 이미지에 서명하는 데 저장소 관리 키를 더 이상 사용할 수 없습니다. 승인된 서명자 중 하나가 서명할 개인 키를 보유하고 있어야 합니다. 서명자 추가 후 이미지에 서명하는 기능을 유지하려면 다시 다음 지시사항에 따라 직접 서명자 역할을 생성하고 추가하십시오.
{:tip}

서명 키를 공유하려면 다음을 수행하십시오.

1.  새 서명자가 키 쌍을 아직 생성하지 않은 경우 키 쌍을 생성하고 로드해야 합니다. 
  
    a. 키를 생성하십시오. <em>NAME</em>에 대해 임의의 이름을 입력할 수 있지만 다른 사용자가 저장소에서 신뢰를 검사할 때 선택한 이름이 표시됩니다. 저장소 소유자와 함께 작업하여 조직이 사용할 수 있는 이름 지정 규칙을 충족시키고 이 서명자에 대해 식별 가능한 이름을 선택하십시오.

      ```
docker trust key generate <NAME>
      ```
      {: pre}
  
    b. 개인 키의 비밀번호 문구를 입력하십시오. 공개 키(`.pub`)가 생성되고 해당 개인 키는 Docker 신뢰 구성에 자동으로 로드됩니다.
  
    c. 새 서명자가 저장소 소유자에게 공개 키를 전송해야 합니다.

2.  저장소 소유자가 서명자의 키를 저장소에 추가해야 합니다.

    a. [신뢰할 수 있는 컨텐츠 환경을 설정](#trustedcontent_setup)하십시오.
    
    b. 저장소에 서명자의 키를 추가하십시오.

      ```
docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}
    
3.  서명자는 해당 환경을 설정하고 이미지에 서명할 수 있습니다.

    a. [신뢰할 수 있는 컨텐츠 환경을 설정](#trustedcontent_setup)하십시오.
    
    b. 서명자는 이미지에 서명해야 합니다. 프롬프트가 표시되면 개인 키의 비밀번호 문구를 입력하십시오.

      ```
docker trust sign <repository>:<tag>
      ```
      {: pre}

4.  서명자가 추가되었는지 확인하려면 [서명된 이미지 보기](#trustedcontent_viewsigned)를 참조하십시오.



### 저장소에서 서명자 제거
{: #trustedcontent_removesigner}

서명자가 더 이상 사용자 저장소의 이미지에 서명하지 않도록 하려면 서명자로 제거할 수 있습니다.
{:shortdesc}

시작하기 전에:
- 저장소 소유자 및 추가 서명자의 경우 Docker 17.12 이상이 설치되어 있어야 합니다.

서명자를 제거하면 신뢰 서버가 이미지의 서명된 버전을 신뢰하지 않습니다. 서명자를 제거한 후 이미지를 가져올 수 있게 하려면 계속하기 전에 서명자가 최신 버전의 이미지에 서명하지 않아야 합니다. 서명자가 최신 버전의 이미지에 서명한 경우 이미지에 업데이트를 푸시하고 계속하기 전에 키를 사용하여 이 이미지에 서명하십시오.
{:tip}

서명자를 제거하려면 다음을 수행하십시오.

1. [신뢰할 수 있는 컨텐츠 환경을 설정](#trustedcontent_setup)하십시오.

2. 서명자를 제거하십시오.

    ```
docker trust signer remove <NAME> <repository>
    ```
    {: pre}
    
3. 서명자가 제거되었는지 확인하려면 이미지의 신뢰 데이터를 보고 서명자가 더 이상 나열되지 않는지 확인하십시오. 신뢰 데이터 보기에 대한 자세한 정보는 [서명된 이미지 보기](#trustedcontent_viewsigned)를 참조하십시오.
