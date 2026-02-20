---

copyright:
  years: 2026
lastupdated: "2026-02-20"

keywords: registry, unable to create namespace, forbidden from creating a namespace, forbidden from creating resource instances

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I forbidden to create a {{site.data.keyword.registryshort_notm}} instance in my account?
{: #troubleshoot-create-namespace}
{: troubleshoot}
{: support}

When you try to create a namespace, you receive a message that says that it is forbidden to create an {{site.data.keyword.registrylong}} instance in your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

You receive the following message `The request could not be completed because it is forbidden to create an IBM Cloud Container Registry instance in your account. Review your IBM Cloud Catalog management settings.`
{: tsSymptoms}

A catalog filter under **Manage > Catalogs > Settings** prevents the creation of any services. By default, the {{site.data.keyword.cloud_notm}} catalog, module registry, and community registry are visible to all users in this account. You can make products available for specific users by turning off visibility to public catalogs and adding products to your private catalogs. If you don't have any private catalogs in your account and you turn off visibility, users can't create instances of any products.
{: tsCauses}

You must ensure that {{site.data.keyword.registryshort}} is allowed when a namespace is being created, see [Settings](/content-mgmt/catalog-settings) in Catalog management.
{: tsResolve}

You can run the following command to include just {{site.data.keyword.registryshort}}, which might be helpful if you are keen to hide everything else:

```sh
ibmcloud catalog filter create --include-all false --include-list public.bluemix.container.registry
```
{: pre}
