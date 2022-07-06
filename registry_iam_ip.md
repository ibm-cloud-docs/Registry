---

copyright:
  years: 2021, 2022
lastupdated: "2022-07-06"

keywords: access restrictions, IP addresses, access, public, private, network

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Using IAM IP address access restrictions
{: #registry_iam_ip}

You can enable IAM IP address access restrictions when you're using {{site.data.keyword.registrylong}}.
{: shortdesc}

To enable IAM IP address access restrictions, you must ensure that the {{site.data.keyword.iamshort}} (IAM) access list is configured so that the {{site.data.keyword.registryshort}} OAuth service can still function. The OAuth service is used to authenticate image pulls and pushes in {{site.data.keyword.registryshort}}.

You must ensure that the IP addresses of any computers that can originate pulls and pushes are added to the IAM IP address access list, see [Allowing specific IP addresses](/docs/account?topic=account-ips).


