---

copyright:
  years: 2018
lastupdated: "2018-09-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# 高可用性和灾难恢复
{: #ha-dr}

{{site.data.keyword.registrylong}} 服务是高可用性区域服务。
{:shortdesc}

* 在每个支持的区域中，流量在多个可用性区域的注册表基础结构之间负载均衡，不含单点故障。

* {{site.data.keyword.registrylong_notm}} 中存储的数据将定期备份，以提供额外弹性。

* 如果担心当整个区域不可用时您的映像也不可用，那么可选择将映像推送到多个区域注册表。 
  
  您还可以选择将映像推送到多个注册表，以防意外删除或覆盖映像。

  有关区域的更多信息，请参阅[区域](/docs/services/Registry/registry_overview.html#registry_regions)。
