---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 监视映像的漏洞
{: #registry_ui}

使用 {{site.data.keyword.Bluemix_notm}} 控制台，您可以查看有关潜在漏洞的信息，以及有关 {{site.data.keyword.registrylong}} 公共和专用存储库中映像安全性的信息。
{:shortdesc}

**安全报告**列显示有关映像的以下信息：
-   `安全` 未发现安全问题。
-   `有漏洞` 发现安全或配置问题，必须解决这些问题，才可部署映像。
-   `未完成` 扫描未完成。扫描可能仍在运行，或者映像的操作系统可能不兼容。等待然后再次尝试扫描。如果扫描仍未完成，请重新推送映像以启动新的扫描。不会阻止部署未完成扫描的映像。

-   `不受支持的操作系统` 映像中的操作系统不受支持。

要查看图形用户界面，请使用以下步骤：

1.  使用 IBM 标识登录到 {{site.data.keyword.Bluemix_notm}} 控制台 ([https://console.bluemix.net](https://console.bluemix.net))。
2.  如果有多个 {{site.data.keyword.Bluemix_notm}} 帐户，请从帐户菜单中选择您要使用的帐户和区域。
3.  单击**目录**。
4.  选择**容器**类别，然后单击**容器注册表**磁贴。
5.  要查看有关专用存储库中映像的信息，请单击**专用存储库**。此时将显示专用存储库中的映像列表和每个映像的安全报告状态。要了解有关潜在漏洞的更多信息（包括标记和映像摘要），请单击表中的行。
6.  要查看有关公共存储库中映像的信息，请单击**公共存储库**。此时将显示公共存储库中的映像列表以及指向每个映像的文档和安全报告的链接。要了解有关潜在漏洞的更多信息（包括标记和映像摘要），请单击表中的行。

要了解有关安全报告中信息的含义的更多信息，请参阅[使用漏洞顾问程序管理映像安全性](../va/va_index.html)。
