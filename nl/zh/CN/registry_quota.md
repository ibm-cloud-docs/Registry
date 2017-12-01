---

copyright:
  years: 2017
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 管理存储量和拉出流量的配额限制
{: #registry_quota}

可以通过设置和管理定制配额限制，从而限制可在 {{site.data.keyword.Bluemix}} 帐户中使用的存储量和拉出流量。
{:shortdesc}


## 设置存储和拉出映像的配额限制
{: #registry_quota_set}

可以通过设置自己的配额限制，从而限制专用映像的存储量和拉出流量。
{:shortdesc}

开始之前，请确保您是要在其中设置配额的 [{{site.data.keyword.Bluemix_notm}} 帐户的所有者或记帐管理员](../../iam/users_roles.html#userroles)。

升级到 {{site.data.keyword.registryshort_notm}} 标准套餐后，可以享受无限的专用映像存储量和拉出流量。为了避免超过首选支付级别，可以分别为存储量和拉出流量设置配额。配额限制会应用于在 {{site.data.keyword.registrylong_notm}} 中设置的所有名称空间。如果使用的是免费服务套餐，那么还可以将定制配额设置为在免费存储量和拉出流量范围内。

要设置配额，请执行以下操作：

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    bx login
    ```
    {: pre}

2.  查看存储量和拉出流量的当前配额限制。

    ```
    bx cr quota
    ```
    {: pre}

    输出类似于以下内容。


    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

3.  更改存储量和拉出流量的配额限制。要更改拉出流量使用量，请指定**流量**选项，并将 _&lt;traffic_quota&gt;_ 替换为要为拉出流量配额设置的值（以兆字节为单位）。如果要更改您的帐户中的存储量，请指定**存储量**选项，并将 _&lt;storage_quota&gt;_ 替换为要设置的值（以兆字节为单位）。


    **注：**如果使用的是免费套餐，那么无法将配额设置为超过免费层的量。免费层的存储量配额为 512 MB，流量为 5120 MB。

    ```
    bx cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    以下示例将存储量配额限制设置为 600 兆字节，将拉出流量设置为 7000 兆字节：


    ```
    bx cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}


## 查看存储和拉出映像的配额限制和使用量
{: #registry_quota_get}

针对您的帐户，可以查看配额限制，并检查当前存储量和拉出流量使用量。
{:shortdesc}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    bx login
    ```
    {: pre}

2.  查看存储量和拉出流量的当前配额限制。

    ```
    bx cr quota
    ```
    {: pre}

    输出类似于以下内容。


    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED
    Pull traffic   5.1 GB   0 B
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}


## 释放已用存储量以及更改服务套餐或配额限制以不超出给定配额限制范围
{: #registry_quota_freeup}

如果超过了为 {{site.data.keyword.Bluemix_notm}} 帐户设置的配额限制，那么可以释放存储量以及更改服务套餐或配额限制，以继续向名称空间推送映像和从名称空间中拉出映像。
{:shortdesc}

要释放 {{site.data.keyword.Bluemix_notm}} 帐户中的映像存储量，请执行以下操作：

1.  列出 {{site.data.keyword.Bluemix_notm}} 帐户的所有名称空间中的所有映像。

    ```
    bx cr images
    ```
    {: pre}

2.  从名称空间中除去映像。将 _&lt;image_name&gt;_ 替换为要除去的映像的名称。


    ```
    bx cr image-rm <image_name>
    ```
    {: pre}

    **注：**根据映像的大小，可能需要一些时间才能除去映像并使存储量可用。

3.  查看存储量配额使用情况。

    ```
    bx cr quota
    ```
    {: pre}

4. **注：**在结算周期内，无法减少拉出流量使用量。

    要继续从名称空间中拉出映像，请在以下选项中进行选择。

    -   等待下一个结算周期开始。
    -   如果您有免费套餐，请[升级到标准服务套餐](registry_overview.html#registry_plan_upgrade)。
    -   如果您已经有标准套餐，请[为拉出流量设置新的配额限制](#registry_quota_set)。
