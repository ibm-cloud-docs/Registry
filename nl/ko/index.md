---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# {{site.data.keyword.registrylong_notm}} 시작하기
{: #index}

{{site.data.keyword.registrylong}}에서는 Docker 이미지를 안전하게 저장하고 {{site.data.keyword.Bluemix_notm}} 계정의 사용자들과 공유하기 위해 사용할 수 있는 멀티 테넌트 개인용 이미지 레지스트리를 제공합니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 콘솔에는 간략한 빠른 시작이 포함되어 있습니다. {{site.data.keyword.Bluemix_notm}} 콘솔 사용 방법에 대해 자세히 알아보려면 [Vulnerability Advisor를 사용하여 이미지 보안 관리](/docs/services/va/va_index.html)를 참조하십시오.

컨테이너 이미지, 네임스페이스 이름, 설명 필드(예: 레지스트리 토큰) 또는 이미지 구성 데이터(예: 이미지 이름 또는 이미지 레이블)에 개인 정보를 입력하지 마십시오.
{:tip}

## {{site.data.keyword.registrylong_notm}} CLI 설치
{: #registry_cli_install}

1. {{site.data.keyword.Bluemix_notm}} `ibmcloud` 명령을 실행할 수 있도록 [{{site.data.keyword.Bluemix_notm}} CLI ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://clis.ng.bluemix.net/ui/home.html)를 설치하십시오. 이를 설치하면 {{site.data.keyword.containerlong_notm}} 및 {{site.data.keyword.registrylong_notm}}용 플러그인도 설치됩니다.

## 네임스페이스 설정
{: #registry_namespace_add}

1. {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

   ```
    ibmcloud login
   ```
   {: pre}

2. 네임스페이스를 추가하여 고유의 이미지 저장소를 작성하십시오. _&lt;my_namespace&gt;_를 선호하는 네임스페이스로 대체하십시오.

   ```
    ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

3. 네임스페이스가 작성되었는지 확인하려면 `ibmcloud cr namespace-list` 명령을 실행하십시오.

   ```
    ibmcloud cr namespace-list
   ```
   {: pre}

## 다른 레지스트리의 이미지를 로컬 시스템으로 가져오기
{: #registry_images_pulling}

1. [Docker CLI ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 설치](https://www.docker.com/community-edition#/download)하십시오. Windows 8 또는 OS X Yosemite 10.10.x 이하의 경우 [Docker Toolbox ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.docker.com/toolbox/)를 대신 설치하십시오.

2. 로컬 시스템에 이미지를 다운로드(_가져오기_)하십시오. _&lt;source_image&gt;_를 이미지의 저장소로 바꾸고 _&lt;tag&gt;_를 사용할 이미지(예: _latest_)로 바꾸십시오.

   ```
    docker pull <source_image>:<tag>
   ```
   {: pre}

   예를 들어, 여기서 _&lt;source_image&gt;_는 `hello-world`이고 _&lt;tag&gt;_는 `latest`입니다.

   ```
    docker pull hello-world:latest
   ```
   {: pre}

3. 이미지에 태그를 지정하십시오. _&lt;source_image&gt;_는 저장소로 대체하고, _&lt;tag&gt;_는
이전에 가져온 로컬 이미지의 태그로 대체하십시오. _&lt;region&gt;_을 [지역](registry_overview.html#registry_regions)의 이름으로 대체하십시오. _&lt;my_namespace&gt;_를 [네임스페이스 설정](index.html#registry_namespace_add)에서 작성한 네임스페이스로 대체하십시오. _&lt;new_image_repo&gt;_ 및 _&lt;new_tag&gt;_를 대체하여
네임스페이스에서 사용하려는 이미지의 태그 및 저장소를 정의하십시오.

   ```
    docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   예를 들어 _&lt;source_image&gt;_는 `hello-world`, _&lt;tag&gt;_는 `latest`, _&lt;region&gt;_은 `eu-gb`, _&lt;my_namespace&gt;_는 `namespace1`, _&lt;new_image_repo&gt;_는 `hw_repo`, _&lt;new_tag&gt;_는 `1`인 경우에는 다음과 같습니다.

   ```
    docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

## Docker 이미지를 네임스페이스에 푸시
{: #registry_images_pushing}

1. `ibmcloud cr login` 명령을 실행하여 로컬 Docker 디먼을 {{site.data.keyword.registrylong_notm}}에 로그인시키십시오.

   ```
  ibmcloud cr login
   ```
   {: pre}

2. 네임스페이스에 이미지를 업로드(_푸시_)하십시오. _&lt;my_namespace&gt;_는 [네임스페이스 설정](index.html#registry_namespace_add)에서 작성한 네임스페이스로 대체하고, _&lt;image_repo&gt;_ 및 _&lt;tag&gt;_는 이미지에 태그를 지정할 때 선택한 해당 이미지의 태그 및 저장소로 대체하십시오.

   ```
    docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}

   예를 들어 _&lt;region&gt;_은 `eu-gb`, _&lt;my_namespace&gt;_는 `namespace1`, _&lt;image_repo&gt;_는 `hw_repo`, _&lt;tag&gt;_는 `1`인 경우에는 다음과 같습니다.

   ```
    docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

3. 다음 명령을 실행하여 이미지가 푸시되었는지 확인하십시오.

   ```
    ibmcloud cr image-list
   ```
   {: pre}

과정이 완료되었습니다! {{site.data.keyword.registrylong_notm}}에 네임스페이스를 설정하고 첫 번째 이미지를 사용자의 네임스페이스로 푸시했습니다.

**다음 단계**

- [Vulnerability Advisor로 이미지 보안 관리](../va/va_index.html)
- [서비스 플랜 및 사용량 검토](registry_overview.html#registry_plans)
- [네임스페이스의 추가 이미지 저장 및 관리](registry_images_.html)
- [사용자 액세스 역할 정책 정의](/docs/services/Registry/registry_users.html#user)
- [클러스터 및 작업자 노드 설정](/docs/containers/cs_clusters.html#clusters)
