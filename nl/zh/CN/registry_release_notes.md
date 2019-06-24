---

copyright:
  years: 2019
lastupdated: "2019-05-17"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# 发行说明
{: #registry_release_notes}

使用这些发行说明了解 {{site.data.keyword.registrylong}} 和漏洞顾问程序的最新更改。更改按日期分组。
{:shortdesc}

## 2019 年 5 月 13 日
{: #13may2019}

- **终止对容器扫描程序的支持**

  容器扫描程序已被弃用且不再可用。

  有关更多信息，请参阅[安装容器扫描程序（已弃用）](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)。

## 2019 年 4 月 2 日 
{: #2apr2019}

- **Container Image Security Enforcement 的一般可用性**

  先使用 Container Image Security Enforcement 来验证容器映像，然后再将其部署到 {{site.data.keyword.containerlong_notm}} 中的集群。您可以控制从何处部署映像，强制实施漏洞顾问程序策略，以及确保[内容信任](/docs/services/Registry?topic=registry-registry_trustedcontent)正确应用于映像。

  有关更多信息，请参阅[强制实施容器映像安全性](/docs/services/Registry?topic=registry-security_enforce#security_enforce)。

## 2019 年 3 月 14 日 
{: #14mar2019}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} 可用于 {{site.data.keyword.registrylong_notm}}**

  使用 {{site.data.keyword.cloudaccesstraillong_notm}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.cloud}} 中的 {{site.data.keyword.registrylong_notm}} 服务进行交互。


  有关更多信息，请参阅 [Activity Tracker 事件](/docs/services/Registry?topic=registry-at_events#at_events)。

## 2019 年 2 月 25 日
{: #25feb2019}

- **新的 DNS 名称**

  {{site.data.keyword.registrylong_notm}} 采用了新的域名。控制台和 CLI 中提供了新域名。您现在可以使用新的 `icr.io` 域名。不推荐使用现有的 `registry.bluemix.net` 域名，但暂时可以继续使用，稍后会公布支持结束日期。
有关更多信息，请参阅[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)和[介绍新的 IBM Cloud Container Registry 域名 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names)。

  如果使用内容信任，因为签名适用于整个映像名称（包括域名），那么您必须添加新的签名，使得您可以在新域名下使用内容信任。有关签署映像的更多信息，请参阅[对可信内容的映像签名](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)。

- ** {{site.data.keyword.containerlong_notm}} 集群的 IAM API 密钥拉取私钥**

  使用 IAM API 密钥授予 `icr.io` 域的新的集群映像拉取私钥，因此，如果您想要进一步控制对 {{site.data.keyword.registrylong_notm}} 资源的访问权，您可以添加 IAM 策略。例如，您可以更改集群拉取密钥中的 API 密钥策略，以仅从特定注册表区域或名称空间拉取映像。
  
  有关更多信息，请参阅[了解如何授权集群从 {{site.data.keyword.registrylong_notm}} 拉取映像](/docs/containers?topic=containers-images#cluster_registry_auth)。

- **亚太地区北部的新区域**

  `亚太地区北部`中有新的可用区域。您可以通过使用域名 `jp.icr.io` 来使用新的区域。
  
  有关更多信息，请参阅[区域](/docs/services/Registry?topic=registry-registry_overview#registry_regions)。

## 2019 年 2 月 21 日 
{: #21feb2019}

- **实现对名称空间的自动访问**

  不推荐使用令牌将 Docker 映像自动推送到名称空间，以及从名称空间自动拉出 Docker 映像。您现在必须使用 API 密钥自动访问 {{site.data.keyword.registrylong_notm}} 名称空间，使得您可以推送和拉取映像。

  有关更多信息，请参阅[使用 API 密钥自动访问名称空间](/docs/services/Registry?topic=registry-registry_access#registry_api_key)。

## 2019 年 1 月 8 日
{: #8jan2019}

- **漏洞顾问程序 API V2 支持结束**

  不推荐使用漏洞顾问程序的 API V2，并且该版本已不再可用。使用 API V3，请参阅[ {{site.data.keyword.registrylong_notm}} API 的漏洞顾问程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/apidocs/container-registry/va)。

  有关更多信息，请参阅[不推荐使用漏洞顾问程序 V2 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/12/vulnerability-advisor-v2-api-deprecation/)。

## 2018 年 10 月 4 日
{: #4oct2018}

- **管理用户访问权**

  在您的 {{site.data.keyword.registrylong_notm}} 帐户中，使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) 控制用户的访问。如果在 {{site.data.keyword.registrylong_notm}} 中为帐户启用了 IAM 策略，那么必须使用定义的 IAM 用户角色，为帐户中访问 {{site.data.keyword.registrylong_notm}} 服务的每个用户分配访问策略。该策略确定用户在服务的上下文中具有的角色，以及用户可以执行的操作。

  有关更多信息，请参阅[使用 {{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam) 管理用户访问权、[定义用户访问角色策略](/docs/services/Registry?topic=registry-user#user)以及[教程：授予对 IBM Cloud Container Registry 资源的访问权](/docs/services/Registry?topic=registry-iam_access#iam_access)。

## 2018 年 8 月 7 日
{: #7aug2018}

- **漏洞顾问程序中可用的豁免策略**

  如果想要管理 {{site.data.keyword.cloud_notm}} 组织的安全性，您可以使用策略设置以确定问题是否为豁免。您可以选择使用 Container Image Security Enforcement，确保在识别策略豁免的所有问题后，只允许部署不包含任何安全问题的映像。


  有关更多信息，请参阅[设置组织豁免策略](/docs/services/Registry?topic=va-va_index#va_managing_policy)。

## 2018 年 7 月 25 日
{: #25jul2018}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} 可用于漏洞顾问程序**

  使用 {{site.data.keyword.cloudaccesstrailfull_notm}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.cloud}} 中的 {{site.data.keyword.registrylong_notm}} 服务进行交互。


  有关更多信息，请参阅 [Activity Tracker 事件](/docs/services/Registry?topic=registry-at_events#at_events)。
  
## 2018 年 7 月 12 日
{: #12jul2018}

- **漏洞顾问程序 API V3**

  API V3 改变了用于列出豁免的 API 端点的行为。您应该检查您对 API 的使用是否不依赖于版本 2 的行为。

  有关更多信息，请参阅[ {{site.data.keyword.registrylong_notm}} 的漏洞顾问程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/apidocs/container-registry/va)。

## 2018 年 5 月 31 日
{: #31may2018}

- **使用 Helm for Passport Advantage 映像**

  将已从 [IBM Passport Advantage Online for customers ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/passportadvantage/pao_customer.html) 下载并已打包与 Helm 配合使用的 {{site.data.keyword.IBM_notm}} 软件导入到 {{site.data.keyword.registrylong_notm}} 名称空间。

  有关更多信息，请参阅 [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load)。

## 2018 年 3 月 21 日
{: #21mar2018}

- **容器扫描程序**

  容器扫描程序支持漏洞顾问程序报告在运行中的容器中发现的任何问题，这些问题在容器的基本映像中不存在。

  有关更多信息，请参阅[安装容器扫描程序](/docs/services/Registry?topic=va-va_index#va_install_container_scanner)。

## 2018 年 3 月 16 日
{: #16mar2018}

- **Container Image Security Enforcement beta**

  使用 Container Image Security Enforcement beta，可以在将容器映像部署到 {{site.data.keyword.containerlong_notm}} 中的集群之前，对这些映像进行验证。您可以控制从何处部署映像，强制实施漏洞顾问程序策略，以及确保[内容信任](/docs/services/Registry?topic=registry-registry_trustedcontent)正确应用于映像。

  有关更多信息，请参阅[强制实施容器映像安全性](/docs/services/Registry?topic=registry-security_enforce#security_enforce)。

## 2018 年 2 月 20 日 
{: #20feb2018}

- **可信内容**

  {{site.data.keyword.registrylong_notm}} 提供可信内容技术，以便您可以对映像签名，以确保注册表名称空间中映像的完整性。通过拉出和推送签名的映像，可以验证映像是否由正确的参与方（例如，连续集成 (CI) 工具）推送。

  有关更多信息，请参阅[对可信内容的映像签名](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent)。

## 2017 年 11 月 6 日 
{: #6nov2017}

- **全局注册表**

  我们为您提供了全局注册表，其名称 `icr.io` 中不包含区域。此注册表中仅托管 IBM 提供的公共映像。

  有关更多信息，请参阅[全球注册表](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global)。

## 2017 年 9 月 29 日
{: #29sep2017}

- **构建 Docker 映像**

  `ibmcloud cr build` 命令现在可用于运行容器构建。您可以直接在 {{site.data.keyword.cloud_notm}} 中构建 Docker 映像，也可以在本地计算机上创建自己的 Docker 映像，然后将其上传（推送）至 {{site.data.keyword.registrylong_notm}} 中的名称空间。


  有关更多信息，请参阅[构建 Docker 映像以用于名称空间](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating)以及
[`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build)。

## 2017 年 8 月 24 日 
{: #24aug2017}

- **发布的图形用户界面**

  {{site.data.keyword.registrylong_notm}} 图形用户界面在目录中提供，请参阅[容器注册表
![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/kubernetes/catalog/registry)。

## 2017 年 6 月 27 日
{: #27jun2017}

- **{{site.data.keyword.registrylong_notm}} 的一般可用性**

  {{site.data.keyword.registrylong_notm}} 通常可用作 {{site.data.keyword.cloud_notm}} 中的服务。{{site.data.keyword.registrylong_notm}} 支持 {{site.data.keyword.containerlong_notm}}。

  有关 {{site.data.keyword.containerlong_notm}} 的更多信息，请参阅[入门教程](/docs/containers?topic=containers-getting-started)。
