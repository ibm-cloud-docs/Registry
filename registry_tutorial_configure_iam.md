---

copyright:
  years: 2018, 2019
lastupdated: "2019-12-10"

keywords: user access, tutorial, access control, granting access, authorizing, 

subcollection: registry

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

# Granting access to {{site.data.keyword.registrylong_notm}} resources tutorial
{: #iam_access}

Use this tutorial to find out how to grant access to your resources by configuring {{site.data.keyword.iamlong}} (IAM) for {{site.data.keyword.registrylong}}.
{:shortdesc}

This tutorial takes approximately 45 minutes.

## Before you begin
{: #iam_access_prereq}

Before you begin, you must complete the following tasks:

- Complete the instructions in [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started#getting-started).

- Ensure that you have the most recent version of the `container-registry` CLI plug-in for the {{site.data.keyword.cloud_notm}} CLI, see [Updating the `container-registry` CLI plug-in](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).

- Ensure that you have access to two [{{site.data.keyword.cloud_notm}} accounts ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login) that you can use for this tutorial, one for User A and one for User B, each must use a unique email address. You work in your own account, User A, and invite another user, User B, to use your account. You can choose to create a second {{site.data.keyword.cloud_notm}} account, or you can work with a colleague that has an {{site.data.keyword.cloud_notm}} account.

- If you started to use {{site.data.keyword.registrylong_notm}} in your account before 4 October 2018, you must enable IAM policy enforcement by running the `ibmcloud cr iam-policies-enable` command. If you have invited other users that use your {{site.data.keyword.registrylong_notm}} namespaces into your {{site.data.keyword.cloud_notm}} account, use a different account as User A to prevent disruption to their access.

## Step 1: Authorize a user to configure the registry
{: #configure_registry}

In this section, you add a second user to your account and grant them the ability to configure {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Add User B to User A's account:

    1. Log in to User A's account, by running the following command:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Invite User B to access User A's account by running the following command, where `<user.b@example.com>` is User B's email address:

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. Get User A's Account ID by running the following command:

        ```
        ibmcloud target
        ```
        {: pre}

        Make a note of the Account ID that is in the parentheses ( ) in the Account row.

2. Prove that User B can target User A's account but can't do anything with {{site.data.keyword.registrylong_notm}} yet:

    1. Log in as User B and target User A's account by running the following command, where `<YourAccountID>` is User A's Account ID:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Try to edit your registry quota to 4 GB of traffic by running the following command:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        The command fails because User B doesn't have the correct access.

3. Grant User B the Manager role so that User B can configure {{site.data.keyword.registrylong_notm}}:

    1. Log back in to your account as yourself, User A, by running the following command:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Create a policy that grants the Manager role to User B by running the following command:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. Prove that User B can now change quotas in User A's account:

    1. Log in as User B, targeting User A's account by running the following command:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Try to edit your registry quota to 4 GB of traffic by running the following command:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        It works because User B has the correct type of access.

    3. Now change the quota back by running the following command:
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. Clean up:

    1. Log back in to your account as yourself, User A, by running the following command:
  
        ```
        ibmcloud login
        ```
        {: pre}
  
    2. List the policies for User B, find the policy you just created by running the following command, and note the ID:
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. Delete the policy by running the following command, where `<Policy_ID>` is your Policy ID:
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Step 2: Authorize a user to access specific namespaces
{: #access_resources}

In this section, you create some namespaces with sample images, and grant access to them. You create policies to grant different roles to each namespace, and show what effect that has.
{:shortdesc}

1. Create three new namespaces in User A's account. These namespaces must be unique across the region, so choose your own namespace names, but this tutorial uses `namespace_a`, `namespace_b` and `namespace_c` as examples:

    1. Log in as User A, by running the following command:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Create `namespace_a` by running the following command:

        ```
        ibmcloud cr namespace-add namespace_a
        ```
        {: pre}

        The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters, and contain lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.
        {: tip}

    3. Create `namespace_b` by running the following command:

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}

    4. Create `namespace_c` by running the following command:

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. Prove that User B can't see anything:

    1. Log in as User B, targeting User A's account by running the following command:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Try to list images as User B by running the following command:

        ```
        ibmcloud cr images
        ```
        {: pre}

        It returns an empty list because User B doesn't have access to any namespaces.

3. Create policies to grant User B the ability to interact with the namespaces by running the following command:

    1. Log in as User A's account by running the following command:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Check that at least three namespaces are listed by running the following command:

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        The three namespaces that you created in this tutorial (`namespace_a`, `namespace_b`, and `namespace_c`) are shown. If you do not see these namespaces, go back and follow the instructions to create them again.

    3. Create a policy that grants the Reader role on `namespace_b` to User B by running the following command, where `<cloud_region>` is the name of your {{site.data.keyword.cloud_notm}} region, for example `us-south`:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_b --roles Reader
        ```
        {: pre}

        To see the names of the {{site.data.keyword.cloud_notm}} regions, run the [`ibmcloud regions`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_regions) command.
        {: tip}

    4. Create a second policy that grants the Reader and Writer roles on `namespace_c` to User B by running the following command:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        This command adds two roles to the same resource in the same policy.
        {: tip}

4. Push images into `namespace_a` and `namespace_b`:

    1. Pull the `hello-world` image by running the following command:

        ```
        docker pull hello-world
        ```
        {: pre}

    2. Tag the image to `namespace_a` by running the following command, where `<registry_region>` is the name of your [{{site.data.keyword.registrylong_notm}} region](/docs/services/Registry?topic=registry-registry_overview#registry_regions), for example `us-south`:

        ```
        docker tag hello-world <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Tag the image to `namespace_b` by running the following command:

        ```
        docker tag hello-world <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. Log in to {{site.data.keyword.registrylong_notm}} by running the following command:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Push the image to `namespace_a` by running the following command:

        ```
        docker push <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. Push the image to `namespace_b` by running the following command:

        ```
        docker push <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

5. Prove that User B can interact with `namespace_b` and`namespace_c`, but not `namespace_a`:

    1. Log in as User B by running the following command:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Show that User B can see `namespace_b` and `namespace_c`, but not `namespace_a` because User B doesn't have access to `namespace_a`, by running the following command:

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. List your images by running the following command:

        ```
        ibmcloud cr images
        ```
        {: pre}

        The image in `namespace_b` is shown in the list, but the image in `namespace_a` doesn't, because User B doesn't have access to `namespace_a`.

    4. Log in to {{site.data.keyword.registrylong_notm}} by running the following command:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Pull the image by running the following command:

        ```
        docker pull <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. Push the image to `namespace_b` by running the following command:

        ```
        docker push <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        This command fails because User B doesn't have the Writer role in `namespace_b`.

    7. Tag the image with `namespace_c` by running the following command:

        ```
        docker tag hello-world <registry_region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. Push the image to `namespace_c` by running the following command:

        ```
        docker push <registry_region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        The command works because User B has the Writer role in `namespace_c`.

    9. Pull from `namespace_c` by running the following command:

        ```
        docker pull <registry_region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

        The command works because User B has the Reader role in `namespace_c`.

6. Clean up:

    1. Log back in to User A's account by running the following command:

        ```
        ibmcloud login
        ```
        {: pre}

    2. List the policies for User B by running the following command:

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        Find the policies you just created and note the Policy IDs.

    3. Delete the policies you just created by running the following command, where `<Policy_ID>` is the Policy ID:

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Step 3: Create a service ID and grant access to a resource
{: #service_id}

In this section, you configure a service ID and grant it access to your {{site.data.keyword.registrylong_notm}} namespace.
{:shortdesc}

1. Set up a service ID with access to {{site.data.keyword.registrylong_notm}} and create an API key for it:

    1. Log in to User A's account by running the following command:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Create a service ID named `cr-roles-tutorial` with the description `"Created during the access control tutorial for Container Registry"` by running the following command:

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. Create a service policy for the service ID that grants the Reader role on `namespace_a` by running the following command:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. Create a second service policy that grants the Writer role on `namespace_b` by running the following command:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <cloud_region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. Create an API key for the service ID by running the following command:

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Use Docker to log in with the service ID API key, where `<API_Key>` is your API key, and interact with the registry:

    1. Log in to {{site.data.keyword.registrylong_notm}} by running the following command:

        ```
        docker login -u iamapikey -p <API_Key> <registry_region>.icr.io
        ```
        {: pre}

    2. Pull your image by running the following command:

        ```
        docker pull <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Push your image to `namespace_a` by running the following command:

        ```
        docker push <registry_region>.icr.io/namespace_a/hello-world
        ```
        {: pre}

        This command doesn't work because the user doesn't have the Writer role in `namespace_a`.

    4. Push your image to `namespace_b` by running the following command:

        ```
        docker push <registry_region>.icr.io/namespace_b/hello-world
        ```
        {: pre}

        This command works because the user has the Writer role in `namespace_b`.

3. Clean up:

    1. List your service policies by running the following command:

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        Note your Policy IDs.

    2. Delete your service policies by running the following command for each policy:

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. Delete your service ID by running the following command:

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. Log back in to {{site.data.keyword.registrylong_notm}} as User A:

        ```
        ibmcloud cr login
        ```
        {: pre}

## Step 4: Cleaning up
{: #clean_up}

In this section, you remove the resources that you created in previous sections to leave your account as it was at the start of this tutorial.
{:shortdesc}

1. Log in to your account by running the following command:

    ```
    ibmcloud login
    ```
    {: pre}

2. Delete `namespace_a`, `namespace_b`, and `namespace_c` by running the following commands:

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. Remove User B from your account by running the following command:

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}
