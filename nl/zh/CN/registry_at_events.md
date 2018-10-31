---

copyright:
  years: 2018
lastupdated: "2018-09-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.cloudaccesstrailshort}} 事件  
{: #at_events}

使用 {{site.data.keyword.cloudaccesstrailfull}} 服务可跟踪 {{site.data.keyword.Bluemix}} 中用户和应用程序如何与 {{site.data.keyword.registrylong}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服务会记录用户发起的更改 {{site.data.keyword.Bluemix_notm}} 中服务状态的活动。有关更多信息，请参阅 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)。 

下表列出了在调用时生成事件的 API 方法：

<table>
  <caption>生成事件的操作</caption>
  <tr>
    <th>操作</th>
	  <th>描述</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>创建漏洞顾问程序豁免。</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>删除漏洞顾问程序豁免。</td>
  </tr>
 </table>



## 在何处查找事件
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件位于生成事件的 {{site.data.keyword.Bluemix_notm}} 区域中提供的 {{site.data.keyword.cloudaccesstrailshort}} **帐户域**中。

漏洞顾问程序事件所在的区域对应于提供资源（例如，映像或名称空间）的 {{site.data.keyword.registrylong_notm}} 区域。






