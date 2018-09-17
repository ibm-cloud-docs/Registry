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

## Understanding access policies and permissions
{: #access_policies}

<dl>
  <dt>Do I have to set access policies?</dt>
    <dd>You must define access policies for every user that works with {{site.data.keyword.registrylong}}. The scope of an access policy is based on a users defined role or roles that determine the actions that they are allowed to perform. Some policies are pre-defined, but others can be customized. The same policy is enforced whether the user makes the request from the {{site.data.keyword.registrylong_notm}} GUI or through the CLI, even when the actions are completed in IBM Cloud infrastructure (SoftLayer).</dd>
    
  <dt>What are the types of permissions?</dt>
  <dd><p><strong>Platform</strong>: {{site.data.keyword.registrylong_notm}} is configured to use {{site.data.keyword.Bluemix_notm}} platform roles to determine the actions that individuals can perform on a registry. The role permissions build on each other, which means that the `Editor` role has all of the same permissions as the `Viewer` role, plus the permissions that are granted to an editor. You can set these policies by region. These policies must be set along with infrastructure policies and have corresponding RBAC roles that are automatically assigned to the default namespace. Example actions are...</p><p><strong>Infrastructure</strong>: You can determine the access levels for your infrastructure...You must set this type of policy along with {{site.data.keyword.containerlong_notm}} platform access policies. To learn about the available roles, check out [infrastructure permissions](/docs/iam/infrastructureaccess.html#infrapermission). In addition to granting specific infrastructure roles, you must also grant device access to users that work with infrastructure. To start assigning roles, follow the steps in [Customizing infrastructure permissions for a user](#infra_access). <strong>Note</strong>: Make sure that your {{site.data.keyword.Bluemix_notm}} account is [set up with access to the IBM Cloud infrastructure (SoftLayer) portfolio](cs_troubleshoot_clusters.html#cs_credentials) so that authorized users can perform actions in the IBM Cloud infrastructure (SoftLayer) account based on the assigned permissions.</p><p><strong>RBAC</strong>: Role-based access control (RBAC) is a way of securing your resources that are in your registry and deciding who can perform which registry actions. Every user who is assigned a platform access policy is automatically assigned a registry role. IS THIS REQUIRED? In Kubernetes, [Role Based Access Control (RBAC) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#api-overview) determines the actions that a user can perform on the resources inside of a cluster. <strong>Note</strong>: RBAC roles are automatically set in conjunction with the platform role for the default namespace. As a cluster administrator, you can [update or assign roles](#rbac) for other namespaces.</p> <p><strong>Cloud Foundry</strong>: Not all services can be managed with Cloud IAM. If you are using one of these services, you can continue to use the [Cloud Foundry user roles](/docs/iam/cfaccess.html#cfaccess) to control access to your services. Example actions are binding a service or creating a new service instance.</p></dd>
</dl>

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
