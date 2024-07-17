---

copyright:
  years: 2024, 2024
lastupdated: "2024-07-17"

keywords: iam, access, policy, permission, access policy

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I get started with {{site.data.keyword.registryshort}}?
{: #troubleshoot-get-started}
{: troubleshoot}
{: support}

You're trying to use the [getting started instructions](/docs/Registry?topic=Registry-getting-started) for {{site.data.keyword.registrylong}}, but you can't get any {{site.data.keyword.registryshort}} commands to work.
{: shortdesc}

You can't run any commands in {{site.data.keyword.registryshort}} because you don't have permission.
{: tsSymptoms}

The [getting started instructions](/docs/Registry?topic=Registry-getting-started) assume that you’re in your own account with permission to do everything. If you’re a member of an account that is owned and administered by someone else, you might not have the correct permissions to configure and operate the registry service.
{: tsCauses}

Ask your administrator to add you to an existing access policy, or create an access policy that gives you the correct [service access role](/docs/Registry?topic=Registry-iam&interface=ui#service_access_roles) for working with {{site.data.keyword.registryshort}}. For more information, see [Managing IAM access for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam&interface=ui) and [Defining IAM access policies for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-user).
{: tsResolve}

If you send the following text to your administrator, it might help them to set up the correct IAM service access role permissions. Replace `<account_name>` with the name of the account that you want to access.

*I need to have the Manager service access role on `container-registry` in the account `<account_name>` so that I can manage the {{site.data.keyword.registrylong_notm}} service. (You might need to justify this request in more detail by specifying the actions that you require regarding [service access roles](/docs/Registry?topic=Registry-iam&interface=ui#service_access_roles)). You can grant me the Manager role with the `ibmcloud iam user-policy-create $MYUSER --roles Manager --service-name container-registry` command, but you can also use other indirect ways to grant permissions consistently, for example by using access groups and templates, according to the account policy. For more information about assigning access, see [Assigning access to {{site.data.keyword.registryshort}} in the console](/docs/Registry?topic=Registry-iam&interface=ui#registry_iam_assign-access-console).*
