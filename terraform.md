---

copyright:
  years: 2021
lastupdated: "2021-08-18"

keywords: Terraform for IBM Cloud Container Registry

subcollection: Registry

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
{:term: .term}
{:external: target="_blank" .external}

# Setting up Terraform for {{site.data.keyword.registrylong_notm}}
{: #registry_terraform-setup}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitier cloud environments that follow Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.registrylong}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud_notm}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't need to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can install from the {{site.data.keyword.cloud_notm}} catalog.
{: tip}

## Installing Terraform and creating a {{site.data.keyword.registryshort}} namespace
{: #registry_terraform-install}

Before you begin, ensure that you have the [required access](/docs/Registry?topic=Registry-iam) to create and work with {{site.data.keyword.registrylong_notm}} resources.

1. To install the Terraform CLI and configure the {{site.data.keyword.cloud}} Provider plug-in for Terraform, follow the [Terraform on {{site.data.keyword.cloud}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to provision, update, or delete {{site.data.keyword.registryshort}} resources.

2. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create a {{site.data.keyword.registryshort}} namespace and to assign a user an access policy in Identity and Access Management (IAM) for that namespace by using HashiCorp Configuration Language (HCL). For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.

    The following example creates a namespace in the default resource group with a name of your choice and attaches an image retention policy to that namespace that retains 10 images. To retrieve the ID of the default resource group, the `ibm_resource_group` data source is used. Then, the user `user@ibm.com` is assigned the Manager role in the IAM access policy for the namespace for a particular region. The region is retrieved from the `terraform.tfvars` file that you created in step 1.

    ```terraform
    data "ibm_resource_group" "group" {
        name = "default"
    }

    resource "ibm_cr_namespace" "cr_namespace" {
        name = "<namespace_name>"
        resource_group_id = data.ibm_resource_group.group.id
    }

    resource "ibm_cr_retention_policy" "cr_retention_policy" {
        namespace = ibm_cr_namespace.cr_namespace.id
        images_per_repo = 10
    }

    resource "ibm_iam_user_policy" "policy" {
        ibm_id = "user@ibm.com"
        roles  = ["Manager"]

        resources {
            service              = "container-registry"
            resource = ibm_cr_namespace.cr_namespace.id
            resource_type = "namespace"
            region = var.region
        }
    }
    ```
    {: codeblock}

    Updating a namespace by using Terraform is not supported. You can use Terraform to create and remove namespaces only.
    {: note}

3. Initialize the Terraform CLI.

    ```
    terraform init
    ```
    {: pre}

4. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.registryshort}} namespace and IAM access policy in your account.

    ```
    terraform plan
    ```
    {: pre}

5. Create the {{site.data.keyword.registryshort}} namespace and IAM access policy in {{site.data.keyword.cloud_notm}}.

    ```
    terraform apply
    ```
    {: pre}

6. From the [{{site.data.keyword.registryshort}} namespace overview page](https://cloud.ibm.com/registry/namespaces){: external}, verify that your namespace is created successfully.

7. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources#review-your-access-console).

## What's next?
{: #registry_terraform-setup-next}

Now that you successfully created your first {{site.data.keyword.registryshort}} namespace with Terraform on {{site.data.keyword.cloud_notm}}, you can choose between the following tasks:

- Learn how to [add images to your namespace](/docs/Registry?topic=Registry-registry_images_). 
- Explore other supported arguments and attributes for the [{{site.data.keyword.registryshort}} Terraform resources and data sources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cr_namespace){: external} that were used in this example.


