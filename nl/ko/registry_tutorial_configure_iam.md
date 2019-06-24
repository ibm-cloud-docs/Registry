---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-20"

keywords: IBM Cloud Container Registry, user access, tutorial, access control, 

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

# 튜토리얼: {{site.data.keyword.registrylong_notm}} 리소스에 대한 액세스 부여
{: #iam_access}

{{site.data.keyword.registrylong_notm}}용 {{site.data.keyword.iamlong}}(IAM)를 구성하여 리소스에 대한 액세스를 부여하는 방법을 알아보려면 이 튜토리얼을 사용하십시오.
{:shortdesc}

이 튜토리얼은 완료하는 데 약 45분이 소요됩니다.

**시작하기 전에**

- [{{site.data.keyword.registrylong_notm}} 시작하기](/docs/services/Registry?topic=registry-getting-started#getting-started)의 지시사항을 완료하십시오.

- {{site.data.keyword.cloud_notm}} CLI용 `container-registry` CLI 플러그인의 최신 버전이 있는지 확인하십시오. [`container-registry` CLI 플러그인 업데이트](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update)를 참조하십시오.

- 이 튜토리얼에 사용할 수 있는 두 개의 [{{site.data.keyword.cloud_notm}} 계정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/login)에 대한 액세스 권한이 있어야 합니다. 하나는 User A이고 다른 하나는 User B이며 각각은 고유한 이메일 주소를 사용해야 합니다. 사용자는 고유 계정인 User A에서 작업하며 계정을 사용하도록 다른 사용자 User B를 초대합니다. 두 번째 {{site.data.keyword.cloud_notm}} 계정을 작성하도록 선택하거나 {{site.data.keyword.cloud_notm}} 계정이 있는 동료와 함께 작업할 수 있습니다.

- 2018년 10월 4일 이전에 계정에서 {{site.data.keyword.registrylong_notm}}를 사용하기 시작한 경우 `ibmcloud cr iam-policies-enable` 명령을 실행하여 IAM 정책 적용을 사용으로 설정해야 합니다. {{site.data.keyword.registrylong_notm}} 네임스페이스를 사용하는 다른 사용자를 IBM Cloud 계정으로 초대한 경우 액세스가 중단되지 않도록 하려면 User A와 다른 계정을 사용하십시오.

## 1단계: 사용자에게 레지스트리를 구성할 수 있는 권한 부여
{: #configure_registry}

이 섹션에서는 두 번째 사용자를 계정에 추가하여 {{site.data.keyword.registrylong_notm}}를 구성할 수 있는 기능을 부여합니다.
{:shortdesc}

1. User A의 계정에 User B를 추가하십시오.

    1. 다음 명령을 실행하여 User A의 계정에 로그인하십시오.

        ```
    ibmcloud login
        ```
        {: pre}

    2. 다음 명령을 실행하여 User A의 계정에 액세스하도록 User B를 초대하십시오. 여기서 _`<user.b@example.com>`_은 User B의 이메일 주소입니다.

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. 다음 명령을 실행하여 User A의 계정 ID를 가져오십시오.

        ```
        ibmcloud target
        ```
        {: pre}

        계정 행의 괄호 ( ) 안에 있는 계정 ID를 기록해 두십시오.

2. User B가 User A의 계정을 대상으로 지정할 수 있지만 아직 {{site.data.keyword.registrylong_notm}}에 대해 어떤 작업도 수행할 수 없음을 입증하십시오.

    1. 다음 명령을 실행하여 User B로 로그인하고 User A의 계정을 대상으로 지정하십시오. 여기서 _`<YourAccountID>`_는 User A의 계정 ID입니다.

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 다음 명령을 실행하여 레지스트리 할당량을 4GB의 트래픽으로 편집해 보십시오.

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        User B에 올바른 액세스 권한이 없으므로 이 명령은 실패합니다.

3. User B가 {{site.data.keyword.registrylong_notm}}를 구성할 수 있도록 User B에 관리자 역할을 부여하십시오.

    1. 다음 명령을 실행하여 사용자 자신(User A)으로 사용자 계정에 다시 로그인하십시오.

        ```
    ibmcloud login
        ```
        {: pre}

    2. 다음 명령을 실행하여 User B에 관리자 역할을 부여하는 정책을 작성하십시오.

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. 이제 User B가 User A 계정의 할당량을 변경할 수 있음을 입증하십시오.

    1. 다음 명령을 실행하여 User A의 계정을 대상으로 지정하여 User B로 로그인하십시오.

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 다음 명령을 실행하여 레지스트리 할당량을 4GB의 트래픽으로 편집해 보십시오.

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        User B에 올바른 유형의 액세스 권한이 있으므로 이 명령이 작동합니다.

    3. 이제 다음 명령을 실행하여 할당량을 다시 변경하십시오.
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. 정리:

    1. 다음 명령을 실행하여 사용자 자신(User A)으로 사용자 계정에 다시 로그인하십시오.
  
        ```
    ibmcloud login
        ```
        {: pre}
  
    2. 다음 명령을 실행하여 User B에 대한 정책을 나열하고 방금 작성한 정책을 찾은 후 ID를 기록해 두십시오.
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. 다음 명령을 실행하여 정책을 삭제하십시오. 여기서 _`<Policy_ID>`_는 정책 ID입니다.
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## 2단계: 사용자에게 특정 네임스페이스에 액세스할 수 있는 권한 부여
{: #access_resources}

이 섹션에서는 샘플 이미지가 포함된 일부 네임스페이스를 작성하여 액세스를 부여합니다. 각 네임스페이스에 여러 역할을 부여하는 정책을 작성하고 미치는 영향을 표시합니다.
{:shortdesc}

1. User A의 계정에 세 개의 새 네임스페이스를 작성하십시오. 이러한 네임스페이스는 지역 전체에서 고유해야 하므로 고유한 네임스페이스 이름을 선택하십시오. 이 튜토리얼에서는 `namespace_a`, `namespace_b` 및 `namespace_c`를 예제로 사용합니다.

    1. 다음 명령을 실행하여 User A로 로그인하십시오.

        ```
    ibmcloud login
        ```
        {: pre}

    2. 다음 명령을 실행하여 `namespace_a`를 작성하십시오. 

        ```
        ibmcloud cr namespace-add namespace_a
        ```
        {: pre}

        네임스페이스 이름은 지역에서 고유해야 합니다.
        {: tip}

    3. 다음 명령을 실행하여 `namespace_b`를 작성하십시오. 

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}
            
    4. 다음 명령을 실행하여 `namespace_c`를 작성하십시오. 

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. User B가 어떤 항목도 볼 수 없음을 입증하십시오.

    1. 다음 명령을 실행하여 User A의 계정을 대상으로 지정하여 User B로 로그인하십시오.

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 다음 명령을 실행하여 User B로 이미지를 나열해 보십시오.

        ```
    ibmcloud cr images
        ```
        {: pre}

        User B에게 네임스페이스에 대한 액세스 권한이 없으므로 이 명령은 비어 있는 목록을 리턴합니다.

3. 다음 명령을 실행하여 User B에게 네임스페이스와 상호작용할 수 있는 기능을 부여하기 위한 정책을 작성하십시오.

    1. 다음 명령을 실행하여 User A의 계정으로 로그인하십시오.

        ```
    ibmcloud login
        ```
        {: pre}

    2. 다음 명령을 실행하여 세 개 이상의 네임스페이스가 나열되는지 확인하십시오.

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        이 튜토리얼에서 작성한 세 개의 네임스페이스(`namespace_a`, `namespace_b` 및 `namespace_c`)가 표시됩니다. 이러한 네임스페이스가 표시되지 않으면 되돌아가서 지시사항에 따라 다시 작성하십시오.

    3. 다음 명령을 실행하여 User B에게 `namespace_b`에 대한 독자 역할을 부여하는 정책을 작성하십시오. 여기서 _`<Region>`_은 [지역](/docs/services/Registry?topic=registry-registry_overview#registry_regions)의 이름(예: `us-south`)입니다.

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Reader
        ```
        {: pre}

    4. 다음 명령을 실행하여 User B에게 `namespace_c`에 대한 독자 및 작성자 역할을 부여하는 두 번째 정책을 작성하십시오.

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        이 명령은 동일한 정책의 동일한 리소스에 두 개의 역할을 추가합니다.
        {: tip}

4. 이미지를 `namespace_a` 및 `namespace_b`에 푸시하십시오.

    1. 다음 명령을 실행하여 `hello-world` 이미지를 가져오십시오.

        ```
        docker pull hello-world
        ```
        {: pre}

    2. 다음 명령을 실행하여 이미지에 `namespace_a`로 태그를 지정하십시오.

        ```
        docker tag hello-world <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. 다음 명령을 실행하여 이미지에 `namespace_b`로 태그를 지정하십시오.

        ```
        docker tag hello-world <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. 다음 명령을 실행하여 {{site.data.keyword.registrylong_notm}}에 로그인하십시오.

        ```
  ibmcloud cr login
        ```
        {: pre}

    5. 다음 명령을 실행하여 이미지를 `namespace_a`에 푸시하십시오.

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. 다음 명령을 실행하여 이미지를 `namespace_b`에 푸시하십시오.

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

5. User B가 `namespace_b` 및 `namespace_c`와 상호작용할 수 있지만 `namespace_a`와는 상호작용할 수 없음을 입증하십시오.

    1. 다음 명령을 실행하여 User B로 로그인하십시오.

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. 다음 명령을 실행하여 User B가 `namespace_b` 및 `namespace_c`를 볼 수 있지만 User B에게 `namespace_a`에 대한 액세스 권한이 없으므로 `namespace_a`는 볼 수 없음을 표시하십시오.

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. 다음 명령을 실행하여 이미지를 나열하십시오.

        ```
    ibmcloud cr images
        ```
        {: pre}

        `namespace_b`의 이미지는 목록에 표시되지만 User B에게 `namespace_a`에 대한 액세스 권한이 없으므로 `namespace_a`의 이미지는 표시되지 않습니다.

    4. 다음 명령을 실행하여 {{site.data.keyword.registrylong_notm}}에 로그인하십시오.

        ```
  ibmcloud cr login
        ```
        {: pre}

    5. 다음 명령을 실행하여 이미지를 가져오십시오.

        ```
        docker pull <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. 다음 명령을 실행하여 이미지를 `namespace_b`에 푸시하십시오.

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        User B에게 `namespace_b`의 작성자 역할이 없으므로 이 명령이 실패합니다.

    7. 다음 명령을 실행하여 이미지에 `namespace_c`로 태그를 지정하십시오.

        ```
        docker tag hello-world <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. 다음 명령을 실행하여 이미지를 `namespace_c`에 푸시하십시오.

        ```
        docker push <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        User B에게 `namespace_c`의 작성자 역할이 있으므로 이 명령이 작동합니다.

    9. 다음 명령을 실행하여 `namespace_c`에서 가져오십시오.

        ```
        docker pull <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        User B에게 `namespace_c`의 독자 역할이 있으므로 이 명령이 작동합니다.

6. 정리:

    1. 다음 명령을 실행하여 User A의 계정에 다시 로그인하십시오.

        ```
    ibmcloud login
        ```
        {: pre}

    2. 다음 명령을 실행하여 User B에 대한 정책을 나열하십시오.

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        방금 작성한 정책은 찾은 후 정책 ID를 기록해 두십시오.

    3. 다음 명령을 실행하여 방금 작성한 정책을 삭제하십시오. 여기서 _`<Policy_ID>`_는 정책 ID입니다.

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## 3단계: 서비스 ID를 작성하고 리소스에 대한 액세스 부여
{: #service_id}

이 섹션에서는 서비스 ID를 구성하고 {{site.data.keyword.registrylong_notm}} 네임스페이스에 대한 액세스를 부여합니다.
{:shortdesc}

1. {{site.data.keyword.registrylong_notm}}에 대한 액세스 권한이 있는 서비스 ID를 설정하고 이에 대한 API 키를 작성하십시오.

    1. 다음 명령을 사용하여 User A의 계정에 로그인하십시오.

        ```
    ibmcloud login
        ```
        {: pre}

    2. 다음 명령을 실행하여 이름이 `cr-roles-tutorial`이고 `"Created during the access control tutorial for Container Registry"`라는 설명이 포함된 서비스 ID를 작성하십시오.

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. 다음 명령을 실행하여 `namespace_a`에 대한 독자 역할을 부여하는 서비스 ID에 대한 서비스 정책을 작성하십시오.

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. 다음 명령을 실행하여 `namespace_b`에 대한 작성자 역할을 부여하는 두 번째 서비스 정책을 작성하십시오.

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. 다음 명령을 실행하여 서비스 ID에 대한 API 키를 작성하십시오.

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Docker를 사용하여 서비스 ID API 키로 로그인하십시오. 여기서 _`<API_Key>`_는 API 키이며 레지스트리와 상호작용합니다.

    1. 다음 명령을 실행하여 {{site.data.keyword.registrylong_notm}}에 로그인하십시오.

        ```
        docker login -u iamapikey -p <API_Key> <Region>.icr.io
        ```
        {: pre}

    2. 다음 명령을 실행하여 이미지를 가져오십시오.

        ```
        docker pull <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. 다음 명령을 실행하여 이미지를 `namespace_a`에 푸시하십시오.

        ```
        docker push <Region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        사용자에게 `namespace_a`의 작업자 역할이 없으므로 이 명령이 작동하지 않습니다.

    4. 다음 명령을 실행하여 이미지를 `namespace_b`에 푸시하십시오.

        ```
        docker push <Region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        사용자에게 `namespace_b`의 작성자 역할이 있으므로 이 명령이 작동합니다.

3. 정리:

    1. 다음 명령을 실행하여 서비스 정책을 나열하십시오.

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        정책 ID를 기록해 두십시오.

    2. 각 정책에 대해 다음 명령을 실행하여 서비스 정책을 삭제하십시오.

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. 다음 명령을 실행하여 서비스 ID를 삭제하십시오.

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. User A로 {{site.data.keyword.registrylong_notm}}에 다시 로그인하십시오.

        ```
  ibmcloud cr login
        ```
        {: pre}

## 4단계: 정리
{: #clean_up}

이 섹션에서는 계정을 이 튜토리얼의 시작 시와 동일한 상태로 두기 위해 이전 섹션에서 작성한 리소스를 제거합니다.
{:shortdesc}

1. 다음 명령을 실행하여 계정에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2. 다음 명령을 실행하여 `namespace_a`, `namespace_b` 및 `namespace_c`를 삭제하십시오.

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. 다음 명령을 실행하여 계정에서 User B를 제거하십시오.

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

수고하셨습니다! 이 튜토리얼을 완료했습니다.
