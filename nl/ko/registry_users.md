---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-27"

keywords: IBM Cloud Container Registry, user access role policies, access policies, policies

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

# 사용자 액세스 역할 정책 정의
{: #user access}

관리자로서 여러 사용자에 대해 서로 다른 액세스 레벨을 작성하도록 레지스트리에 대한 액세스 정책을 정의할 수 있습니다. 예를 들어, 다른 사용자는 할당량을 볼 수만 있지만 특정 사용자에게 할당량을 설정할 수 있는 권한을 부여할 수 있습니다.
{: shortdesc}

{{site.data.keyword.registrylong}}에 대해 작업하는 모든 사용자에 대한 액세스 정책을 정의해야 합니다. 액세스 정책의 범위는 수행하도록 허용되는 조치를 판별하는 사용자의 정의된 역할을 기반으로 합니다. 일부 정책은 사전 정의되어 있지만 일부는 사용자 정의할 수 있습니다.

2018년 10월 4일 이전에 {{site.data.keyword.registrylong_notm}}를 사용하기 시작한 경우 정책 적용을 사용으로 설정해야 정책이 적용될 수 있습니다. [기존 사용자에 대한 정책 적용 사용](#existing_users)을 참조하십시오.
{: tip}

{{site.data.keyword.iamlong}}(IAM) 액세스 역할 정책에 대해 자세히 알아보려면 [{{site.data.keyword.iamshort}}](/docs/iam?topic=iam-iamoverview#iamoverview)를 참조하십시오.

## 정책 작성
{: #create}

리소스에 대한 액세스를 제어하려면 사용자 또는 서비스 ID에 역할을 지정해야 합니다. {{site.data.keyword.registrylong_notm}} 리소스에 대한 액세스는 이름별로 네임스페이스 리소스에 부여하거나 전체 서비스, 즉 계정의 모든 네임스페이스에 부여할 수 있습니다.

모든 항목에 대한 액세스를 부여하려면 리소스 유형 또는 리소스를 지정하지 마십시오. 특정 네임스페이스에 대한 액세스를 부여하려면 리소스 유형을 `namespace`로 지정하고 네임스페이스 이름을 리소스로 사용하십시오.

**시작하기 전에**

- 각 사용자에게 필요한 역할과 {{site.data.keyword.registrylong_notm}}의 리소스를 결정하십시오. [IAM 역할](/docs/services/Registry?topic=registry-iam#iam)의 내용을 참조하십시오. 여러 정책을 작성할 수 있음을 고려하십시오. 예를 들어, 하나의 리소스에 대한 쓰기 액세스를 부여하지만 다른 리소스에 대해서는 읽기 액세스만 부여하고 또 다른 리소스에 대해서는 액세스를 부여하지 않을 수 있습니다. 정책은 가산적입니다. 이는 글로벌 읽기 정책 및 리소스 범위의 쓰기 정책이 해당 리소스에 대한 읽기 및 쓰기 액세스를 둘 다 부여함을 의미합니다.

- [사용자를 초대하고 액세스를 지정하십시오](/docs/iam?topic=iam-iamuserinv#iamuserinv).

  사용자가 {{site.data.keyword.containerlong_notm}}에서 클러스터를 작성할 수 있도록 하려면 해당 사용자에게 {{site.data.keyword.registrylong_notm}} 관리자 역할을 지정하고 리소스 그룹을 지정하지 않았는지 확인하십시오. [클러스터 작성 준비](/docs/containers?topic=containers-clusters#cluster_prepare)를 참조하십시오.
  {: tip}

{{site.data.keyword.registrylong_notm}}에 대한 정책을 작성하려면 서비스 이름 필드가 `container-registry`여야 합니다.

- 사용자에 대한 정책을 작성하려면 [리소스에 대한 액세스 관리](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)를 참조하십시오.
- 서비스 ID에 대한 정책을 작성하려면 `ibmcloud iam service-policy-create` 명령을 실행하거나 GUI를 사용하여 역할을 서비스 ID에 바인드하십시오. 정책을 작성하려면 관리자 역할이 있어야 합니다. 사용자 고유의 계정에 관리자 역할이 자동으로 보유됩니다. 자세한 정보는 [서비스 ID 작성 및 관련 작업 수행](/docs/iam?topic=iam-serviceids#serviceids) 및 [서비스 ID 액세스 정책 관리](/docs/iam?topic=iam-serviceidpolicy#serviceidpolicy)를 참조하십시오.

## 기존 사용자에 대한 정책 적용 사용
{: #existing_users}

2018년 10월 4일 이후에 프로비저닝된 사용자의 경우 기본적으로 IAM 정책이 사용으로 설정됩니다. 2018년 10월 4일 이전에 프로비저닝된 사용자의 경우 정책을 작성한 후 정책이 적용될 수 있도록 정책 적용을 사용으로 설정해야 합니다.

1. 사용자 및 서비스 ID에 대한 [정책을 작성](#create)하십시오.

2. 정책 적용을 사용으로 설정하려면 [`bx cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable) 명령을 실행하십시오.

    `ibmcloud cr iam-policies-enable` 명령을 실행할 수 있도록 계정에 관리자 역할이 있어야 합니다. 사용자 고유의 계정에 자동으로 관리자 역할이 보유됩니다.
    {: tip}
