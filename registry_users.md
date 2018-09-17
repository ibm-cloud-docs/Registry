staging>
copyright:
  years: 2018
lastupdated: "2018-09-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Assigning access
{: #iam}

As an administrator, you can define access policies for your registry to create different levels of access for different users. For example, you can authorize certain users to set quotas while others can only view quotas.
{: shortdesc}

You must define access policies for every user that works with {{site.data.keyword.registrylong}}. The scope of an access policy is based on a users defined role or roles that determine the actions that they are allowed to perform. Some policies are pre-defined, but others can be customized. The same policy is enforced whether the user makes the request from the {{site.data.keyword.registrylong_notm}} GUI or through the CLI, even when the actions are completed in IBM Cloud infrastructure (SoftLayer).

## Assigning user roles
{: #iam_user_roles}


### Assigning roles with the CLI
{: #roles_cli}

You can add users to an {{site.data.keyword.Bluemix_notm}} account to grant access to your registry by using the CLI.


**Before you begin**

Verify that you are assigned the `Manager` [Cloud Foundry role](/docs/iam/mngcf.html#mngcf) for the {{site.data.keyword.Bluemix_notm}} account in which you're working.

**To assign access to a specific user**

1. Invite the user to your account.

  ```
  ibmcloud account user-invite <user@email.com>
  ```
  {: pre}
  
2. Create an IAM access policy to set permissions for {{site.data.keyword.containerlong_notm}}. You can choose between Viewer, Editor, Operator, and Administrator for role.
  
  ```
  ibmcloud iam user-policy-create <user_email> --service-name container-registry --roles <role>
  ```
  {: pre}

**To assign access to a group**

1. If the user is not already part of your account, invite them.
  
  ```
  ibmcloud account user-invite <user_email>
  ```
  {: pre}

2. Create a group.
 
  ```
  ibmcloud iam access-group-create <team_name>
  ```
  {: pre}

3. Add the user to the group.
  
  ```
  ibmcloud iam access-group-user-add <team_name> <user_email>
  ```
  {: pre}

4. Add the user to the group. You can choose between Viewer, Editor, Operator, and Administrator for role.
 
  ```
  ibmcloud iam access-group-policy-create <team_name> --service-name container-registry --roles <role>
  ```
  {: pre}


The previous instructions show how to give a group of users access to all {{site.data.keyword.registrylong}} resources. As an administrator, you can also limit access to the service at the region level.
{: tip}



</staging>
