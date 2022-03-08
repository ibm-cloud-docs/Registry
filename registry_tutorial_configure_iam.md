---

copyright:
  years: 2018, 2022
lastupdated: "2022-03-08"

keywords: user access, tutorial, access control, granting access, authorizing, 

subcollection: Registry

content-type: tutorial
account-plan: lite
completion-time: 45m

---

{{site.data.keyword.attribute-definition-list}}

# Granting access to {{site.data.keyword.registrylong_notm}} resources tutorial
{: #iam_access}
{: toc-content-type="tutorial"}
{: toc-completion-time="45m"}

Use this tutorial to find out how to grant access to your resources by configuring {{site.data.keyword.iamlong}} (IAM) for {{site.data.keyword.registrylong}}.
{: shortdesc}

From 5 July 2022, all accounts will require IAM access policies. If you started to use {{site.data.keyword.registryshort}} before the availability of [IAM API key policies in {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#registry-25feb2019) in February 2019, you must now ensure that you are using {{site.data.keyword.iamlong}} (IAM) access role policies to manage access to the {{site.data.keyword.registrylong_notm}} service. For more information, see [Access to {{site.data.keyword.registrylong_notm}} requires IAM access policies from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy) and [Defining access role policies](/docs/Registry?topic=Registry-user).
{: important}

For more information about how to use {{site.data.keyword.iamlong}} to manage access to your resources, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

## Before you begin
{: #iam_access_prereq}

Before you begin, you must complete the following tasks:

- Complete the instructions in [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).
- Ensure that you have the most recent version of the `container-registry` CLI plug-in for the {{site.data.keyword.cloud_notm}} CLI, see [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update).
- Ensure that you have access to two [{{site.data.keyword.cloud_notm}} accounts](https://cloud.ibm.com/login){: external} that you can use for this tutorial, one for User A and one for User B, each must use a unique email address. You work in your own account, User A, and invite another user, User B, to use your account. You can choose to create a second {{site.data.keyword.cloud_notm}} account, or you can work with a colleague that has an {{site.data.keyword.cloud_notm}} account.
- Ensure that you have the correct access permissions for adding and removing namespaces, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).
- If you started to use {{site.data.keyword.registrylong_notm}} in your account before 4 October 2018, you must enable IAM policy enforcement by running the `ibmcloud cr iam-policies-enable` command. If you invited other users that use your {{site.data.keyword.registrylong_notm}} namespaces into your {{site.data.keyword.cloud_notm}} account, use a different account as User A to prevent disruption to their access.

## Authorize a user to configure the registry
{: #configure_registry}
{: step}

Add a second user to your account and grant them the ability to configure {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

1. Add User B to User A's account.

    1. Log in to User A's account, by running the following command.

        ```txt
        ibmcloud login
        ```
        {: pre}

    2. Invite User B to access User A's account by running the following command, where `<user.b@example.com>` is User B's email address.

        ```txt
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. Get User A's Account ID by running the following command.

        ```txt
        ibmcloud target
        ```
        {: pre}

        Make a note of the Account ID that is in the parentheses ( ) in the Account row.

2. Prove that User B can target User A's account but can't do anything with {{site.data.keyword.registrylong_notm}} yet.

    1. Log in as User B and target User A's account by running the following command, where `<YourAccountID>` is User A's Account ID.

        ```txt
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Try to edit your registry quota to 4 GB of traffic by running the following command.

        ```txt
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        The command fails because User B doesn't have the correct access.

3. Grant User B the Manager role so that User B can configure {{site.data.keyword.registrylong_notm}}.

    1. Log back in to your account as yourself, User A, by running the following command.

        ```txt
        ibmcloud login
        ```
        {: pre}

    2. Create a policy that grants the Manager role to User B by running the following command.

        ```txt
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. Prove that User B can now change quotas in User A's account.

    1. Log in as User B, targeting User A's account by running the following command.

        ```txt
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Try to edit your registry quota to 4 GB of traffic by running the following command.

        ```txt
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        It works because User B has the correct type of access.

    3. Now change the quota back by running the following command.

        ```txt
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. Clean up.

    1. Log back in to your account as yourself, User A, by running the following command.

        ```txt
        ibmcloud login
        ```
        {: pre}

    2. List the policies for User B, find the policy that you created by running the following command, and note the ID.

        ```txt
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

    3. Delete the policy by running the following command, where `<Policy_ID>` is your Policy ID.

        ```txt
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Authorize a user to access specific namespaces
{: #access_resources}
{: step}

Create some namespaces with sample images, and grant access to them. You create policies to grant different roles to each namespace, and show what effect that has.
{: shortdesc}

1. Create three new namespaces in User A's account. These namespaces must be unique across the region, so choose your own namespace names, but this tutorial uses `namespace_a`, `namespace_b` and `namespace_c` as examples.

    1. Log in as User A, by running the following command.

        ```txt
        ibmcloud login
        ```
        {: pre}

    2. Create `namespace_a` by running the following command.

        ```txt
        ibmcloud cr namespace-add namespace_a
        ```
        {: pre}

        The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters, and contain lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.
        {: tip}

    3. Create `namespace_b` by running the following command.

        ```txt
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}

    4. Create `namespace_c` by running the following command.

        ```txt
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. Prove that User B can't see anything.

    1. Log in as User B, targeting User A's account by running the following command.

        ```txt
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Try to list the namespaces as User B by running the following command.

        ```txt
        ibmcloud cr namespaces
        ```
        {: pre}

        It returns an empty list because User B doesn't have access to any namespaces.

3. Create policies to grant User B the ability to interact with the namespaces by running the following command.

    1. Log in as User A's account by running the following command.

        ```txt
        ibmcloud login
        ```
        {: pre}

    2. Check that at least three namespaces are listed by running the following command.

        ```txt
        ibmcloud cr namespaces
        ```
        {: pre}

        The three namespaces that you created in this tutorial (`namespace_a`, `namespace_b`, and `namespace_c`) are shown. If you do not see these namespaces, go back and follow the instructions to create them again.

    3. Create a policy that grants the Reader role on `namespace_b` to User B by running the following command, where `<cloud_region>` is the name of your {{site.data.keyword.cloud_notm}} region, for example `us-south`.

        ```txt
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_b --roles Reader
        ```
        {: pre}

        To see the names of the {{site.data.keyword.cloud_notm}} regions, run the [`ibmcloud regions`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_regions) command.
        {: tip}

    4. Create a second policy that grants the Reader and Writer roles on `namespace_c` to User B by running the following command.

        ```txt
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        This command adds two roles to the same resource in the same policy.
        {: tip}

4. Push images into `namespace_a` and `namespace_b`.

    1. Pull the `hello-world` image by running the following command.

        ```txt
        docker pull hello-world
        ```
        {: pre}

    2. Tag the image to `namespace_a` by running the following command, where `<registry_region>` is the name of your [{{site.data.keyword.registrylong_notm}} region](/docs/Registry?topic=Registry-registry_overview#registry_regions), for example `us-south`.

        ```txt
        docker tag hello-world <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Tag the image to `namespace_b` by running the following command.

        ```txt
        docker tag hello-world <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. Log in to {{site.data.keyword.registrylong_notm}} by running the [`ibmcloud cr login`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_login) command.

        ```txt
        ibmcloud cr login
        ```
        {: pre}

        {{site.data.keyword.registrylong_notm}} supports other clients as well as Docker. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).
        {: tip}

    5. Push the image to `namespace_a` by running the following command.

        ```txt
        docker push <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. Push the image to `namespace_b` by running the following command.

        ```txt
        docker push <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

5. Prove that User B can interact with `namespace_b` and `namespace_c`, but not `namespace_a`.

    1. Log in as User B by running the following command.

        ```txt
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Show that User B can see `namespace_b` and `namespace_c`, but not `namespace_a` because User B doesn't have access to `namespace_a`, by running the following command.

        ```txt
        ibmcloud cr namespaces
        ```
        {: pre}

    3. List your images by running the following command.

        ```txt
        ibmcloud cr images
        ```
        {: pre}

        The image in `namespace_b` is shown in the list, but the image in `namespace_a` doesn't, because User B doesn't have access to `namespace_a`.

    4. Log in to {{site.data.keyword.registrylong_notm}} by running the following command.

        ```txt
        ibmcloud cr login
        ```
        {: pre}

        {{site.data.keyword.registrylong_notm}} supports other clients as well as Docker. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).
        {: tip}

    5. Pull the image by running the following command.

        ```txt
        docker pull <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. Push the image to `namespace_b` by running the following command.

        ```txt
        docker push <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        This command fails because User B doesn't have the Writer role in `namespace_b`.

    7. Tag the image with `namespace_c` by running the following command.

        ```txt
        docker tag hello-world <registry_region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. Push the image to `namespace_c` by running the following command.

        ```txt
        docker push <registry_region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        The command works because User B has the Writer role in `namespace_c`.

    9. Pull from `namespace_c` by running the following command.

        ```txt
        docker pull <registry_region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        The command works because User B has the Reader role in `namespace_c`.

6. Clean up:

    1. Log back in to User A's account by running the following command.

        ```txt
        ibmcloud login
        ```
        {: pre}

    2. List the policies for User B by running the following command.

        ```txt
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        Find the policies that you created and note the Policy IDs.

    3. Delete the policies that you created by running the following command, where `<Policy_ID>` is the Policy ID.

        ```txt
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Create a service ID and grant access to a resource
{: #service_id}
{: step}

Configure a service ID and grant it access to your {{site.data.keyword.registrylong_notm}} namespace.
{: shortdesc}

1. Set up a service ID with access to {{site.data.keyword.registrylong_notm}} and create an [API key](x8051010){: term} for it.

    1. Log in to User A's account by running the following command.

        ```txt
        ibmcloud login
        ```
        {: pre}

    2. Create a service ID named `cr-roles-tutorial` with the description `"Created during the access control tutorial for Container Registry"` by running the following command.

        ```txt
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. Create a service policy for the service ID that grants the Reader role on `namespace_a` by running the following command.

        ```txt
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. Create a second service policy that grants the Writer role on `namespace_b` by running the following command.

        ```txt
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. Create an API key for the service ID by running the following command.

        ```txt
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Use Docker to log in with the service ID API key, where `<API_Key>` is your API key, and interact with the registry.

    1. Log in to {{site.data.keyword.registrylong_notm}} by running the following command.

        ```txt
        docker login -u iamapikey -p <API_Key> <registry_region>.icr.io
        ```
        {: pre}

        {{site.data.keyword.registrylong_notm}} supports other clients as well as Docker. To log in by using other clients, see [Accessing your namespaces in automation](/docs/Registry?topic=Registry-registry_access#registry_access_automating).
        {: tip}

    2. Pull your image by running the following command.

        ```txt
        docker pull <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Push your image to `namespace_a` by running the following command.

        ```txt
        docker push <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        This command doesn't work because the user doesn't have the Writer role in `namespace_a`.

    4. Push your image to `namespace_b` by running the following command.

        ```txt
        docker push <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        This command works because the user has the Writer role in `namespace_b`.

3. Clean up:

    1. Log back in to {{site.data.keyword.registrylong_notm}} as User A.

        ```txt
        ibmcloud cr login
        ```
        {: pre}

        {{site.data.keyword.registrylong_notm}} supports other clients as well as Docker. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).
        {: tip}

    2. List your service policies by running the following command.

        ```txt
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        Note your Policy IDs.

    3. Delete your service policies by running the following command for each policy.

        ```txt
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    4. Delete your service ID by running the following command.

        ```txt
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

## Cleaning up
{: #clean_up}
{: step}

Remove the resources that you created in previous sections to leave your account as it was at the start of this tutorial.
{: shortdesc}

1. Log in to User A's account by running the following command.

    ```txt
    ibmcloud login
    ```
    {: pre}

2. Delete `namespace_a`, `namespace_b`, and `namespace_c` by running the following commands.

    ```txt
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```txt
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```txt
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. Remove User B from your account by running the following command.

    ```txt
    ibmcloud account user-remove <user.b@example.com>
    ```
    {: pre}


