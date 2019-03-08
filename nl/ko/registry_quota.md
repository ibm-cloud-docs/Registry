---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry, quota limits, custom quota limits, pull traffic

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

# 스토리지 및 가져오기 트래픽의 할당량 한계 관리
{: #registry_quota}

사용자 정의 할당량 한계를 설정하고 관리하여 {{site.data.keyword.Bluemix}} 계정에서 사용할 수 있는 스토리지 및 가져오기 트래픽의 양을 제한할 수 있습니다.
{:shortdesc}

##  이미지를 저장하고 가져오기 위한 할당량 한계 설정
{: #registry_quota_set}

고유의 할당량 한계를 설정하여 개인용 이미지에 대한 스토리지 및 가져오기 트래픽의 양을 제한할 수 있습니다.
{:shortdesc}

{{site.data.keyword.registryshort_notm}}
표준 플랜으로 업그레이드하면 개인용 이미지에 대한 무제한의 스토리지 및 가져오기 트래픽 양을 활용할 수 있습니다. 선호하는 결제 레벨을 초과하지 않도록, 스토리지 및 가져오기 트래픽 양에 대한 개별 할당량을 설정할 수 있습니다. 할당량 한계는
{{site.data.keyword.registrylong_notm}}에 설정하는 모든 네임스페이스에 적용됩니다. 무료 서비스 플랜을
사용하는 경우, 무료 스토리지 및 가져오기 트래픽 양의 범위 내에서 사용자 정의 할당량을 설정할 수도 있습니다.

할당량을 설정하려면 다음을 수행하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2. 스토리지 및 가져오기 트래픽의 현재 할당량 한계를 검토하십시오.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    출력은
다음과 같이 표시됩니다.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

3. 스토리지 및 가져오기 트래픽의 할당량 한계를 변경하십시오. 가져오기 트래픽 사용량을 변경하려면 **traffic** 옵션을 지정하고 `<traffic_quota>`를 가져오기 트래픽 할당량에 설정하려는 메가바이트 단위의 값으로 대체하십시오. 사용자의 계정에서 스토리지의 양을 변경하려는 경우, **storage** 옵션을 지정하고 `<storage_quota>`를 설정하려는 메가바이트 단위의 값으로 대체하십시오.

    무료 플랜을 사용 중인 경우에는 무료 계층을 초과하는 양으로 할당량을 설정할 수 없습니다. 무료 계층 허용량은 스토리지의 경우 512MB이고 트래픽의 경우 5120MB입니다.
    {:tip}

    ```
    ibmcloud cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    스토리지의 할당량 한계를 600MB, 가져오기 트래픽의 할당량 한계를 7000MB로 설정하는 예:

    ```
    ibmcloud cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}

## 이미지를 저장하고 가져오기 위한 할당량 한계 및 사용량 검토
{: #registry_quota_get}

할당량 한계를 검토하고 사용자의 계정에 대한 현재 스토리지 및 가져오기 트래픽 사용량을 검토할 수 있습니다.
{:shortdesc}

1. {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2. 스토리지 및 가져오기 트래픽의 현재 할당량 한계를 검토하십시오.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    출력은
다음과 같이 표시됩니다.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

## 지정된 할당량 한계를 넘지 않도록 사용된 스토리지의 여유 공간을 확보하고 서비스 플랜 또는 할당량 한계 변경
{: #registry_quota_freeup}

{{site.data.keyword.Bluemix_notm}} 계정에 설정된 할당량 한계를 초과한 경우, 계속해서 네임스페이스로 이미지를 푸시하고 네임스페이스에서 이미지 가져오도록 스토리지의 여유 공간을 확보하고 서비스 플랜 또는 할당량 한계를 변경할 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 계정에서 이미지 스토리지의 여유 공간을 확보하려면 다음을 수행하십시오.

1. {{site.data.keyword.Bluemix_notm}} 계정의 모든 네임스페이스에서 모든 이미지를 나열하십시오.

    ```
    ibmcloud cr images
    ```
    {: pre}

2. 네임스페이스에서 이미지를 제거하십시오. `<image_name>`을 제거하려는 이미지의 이름으로 대체하십시오.

    ```
    ibmcloud cr image-rm <image_name>
    ```
    {: pre}

    이미지의 크기에 따라, 이미지가 제거되고 스토리지를 사용할 수 있게 되기까지 다소 시간이 소요될 수 있습니다.
    {:tip}

3. 스토리지 할당 사용량을 검토하십시오.

    ```
    ibmcloud cr quota
    ```
    {: pre}

4. 청구 기간에는 가져오기 트래픽 사용량을 줄일 수 없습니다.
   {:tip}

    네임스페이스에서 이미지를 계속 가져오려면 다음 옵션 중 하나를 선택하십시오.

    - 다음 청구 주기가 시작될 때까지 기다리십시오.
    - 무료 플랜인 경우, [표준 서비스 플랜으로 업그레이드](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade)하십시오.
    - 이미 표준 플랜인 경우, [가져오기 트래픽에 대한 새 할당량 한계를 설정](#registry_quota_set)하십시오.
