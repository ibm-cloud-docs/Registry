---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, high availability


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

# 高可用性和灾难恢复
{: #ha-dr}

{{site.data.keyword.registrylong}} 服务是一种高度可用的区域性服务。
{:shortdesc}

* 在每个受支持的区域中，流量会通过多个可用性区域 (zone) 在整个注册表基础架构中实现负载均衡，而没有单点故障。

* 为了提供额外的弹性，会定期对 {{site.data.keyword.registrylong_notm}} 中存储的数据进行备份。

* 如果您担心在整个区域不可用时无法使用您的映像，那么可以选择将映像推送到多个区域注册表中。
  
  您还可以选择将映像推送到多个注册表中，以防意外删除或覆盖映像。

  有关区域的更多信息，请参阅[区域](/docs/services/Registry/registry_overview.html#registry_regions)。
