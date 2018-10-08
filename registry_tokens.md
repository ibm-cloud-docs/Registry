---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Automating access to {{site.data.keyword.registrylong_notm}}
{: #registry_access}

You can use either registry tokens or an {{site.data.keyword.iamlong}} (IAM) API key to automate access to your  {{site.data.keyword.registrylong_notm}} namespaces so that you can push and pull images.
{:shortdesc}

Are you trying to use your registry images in Kubernetes deployments? Check out [Accessing images in other Kubernetes namespaces, {{site.data.keyword.Bluemix_notm}} regions, and accounts](/docs/containers/cs_images.html#other).
{: tip}

API keys are linked to your account and can be used across {{site.data.keyword.Bluemix_notm}} so that you don't need different credentials for each service. You can use the API key in the CLI or as part of automation to log in as your user identity.

Registry tokens are scoped for {{site.data.keyword.registrylong_notm}} only. You can limit them to read-only access, and you can choose whether they are expiring or non-expiring.

If you use an API key, you can control access to your namespaces by using IAM policies. For more information, see [Defining user access role policies](/docs/services/Registry/registry_users.html#user).

For more information about {{site.data.keyword.registrylong_notm}} API keys, see [Working with API keys](/docs/iam/apikeys.html#manapikey).

Before you begin, [install the {{site.data.keyword.registrylong_notm}} and Docker CLI](registry_setup_cli_namespace.html#registry_cli_install).

## Automating access to your namespaces by using API keys
{: #registry_api_key}

You can use API keys to automate the pushing and pulling of Docker images to and from your namespaces.
{:shortdesc}

### Creating an API key
{: #registry_api_key_create}

You can create an API key that you can then use to log in to your registry. 
{:shortdesc}

You can create both user API keys and service ID API keys.

-  To create a service ID API key, see [Creating an API key for a service ID](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id).
-  To create a user API key, see [Creating an API key](/docs/iam/userid_keys.html#creating-an-api-key).

### Using an API key to automate access
{: #registry_api_key_use}

You can use an API key to automate access to your namespaces in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Use the API key to log in to your registry by running the following Docker command. Replace &lt;your_apikey&gt; with your API key, and replace &lt;registry_url&gt; with the URL to the registry where your namespaces are set up.

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

For reference information about the command, see [Create a new {{site.data.keyword.Bluemix_notm}} platform API key](/docs/cli/reference/ibmcloud/cli_api_policy.html#ibmcloud_iam_api_key_create).

## Automating access to your namespaces by using tokens
{: #registry_tokens}

You can use tokens to automate the pushing and pulling of Docker images to and from your {{site.data.keyword.registrylong_notm}} namespaces.
{:shortdesc}

Everyone in possession of a registry token can access secured information. By creating a token for your {{site.data.keyword.Bluemix_notm}} account, you can grant access to all of your namespaces that you set up in a region for users outside your {{site.data.keyword.Bluemix_notm}} account. Every user or app in possession of this token can push and pull images to and from your namespaces without installing the container-registry plug-in.

When you create a token for your {{site.data.keyword.Bluemix_notm}} account, you can decide whether that token authorizes read-only (pull) or write access (push and pull) to the registry. You can also specify whether a token is permanent or if it expires after 24 hours. You can create and use multiple tokens to control different types of access.

If you log in to {{site.data.keyword.registrylong_notm}} by using a registry token, your IAM access policies are not enforced. If you want to restrict access to one or more namespaces for an ID that is used in automation, consider using an IAM service ID API key instead of a registry token. For more information about creating an API key and using it with {{site.data.keyword.registrylong_notm}}, see [Automating access to your namespaces by using API keys](#registry_api_key).

Use the following tasks to manage your tokens:

-  [Creating a token for your {{site.data.keyword.Bluemix_notm}} account](#registry_tokens_create)
-  [Using a token to automate access to your namespaces](#registry_tokens_use)
-  [Removing a token from your {{site.data.keyword.Bluemix_notm}} account](#registry_tokens_remove)

### Creating a token for your {{site.data.keyword.Bluemix_notm}} account
{: #registry_tokens_create}

You can create a token to grant access to all your {{site.data.keyword.registrylong_notm}} namespaces in a region.
{:shortdesc}

1.  Create a token. The following example creates a non-expiring token that has read and write access to all namespaces that are set up in a region.

    ```
    ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="light bulb icon"/> Understanding this command's components</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>Optional. Use this option to describe your token so that you can identify it more easily later.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>Optional. Use this option to create a non-expiring token. If you do not specify this option, the token becomes invalid after 24 hours. <br> **Tip:** When you no longer need a non-expiring token to block access to your namespaces, remember to remove the token.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>Optional. Use this option to create a token that allows users to push and pull images to and from your namespaces. If you do not specify this option, the token can be used to pull images only.</td>
        </tr>
        </tbody>
        </table>

    Your CLI output looks similar to the following output:

    ```
    Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad
    Token              <token_value>
    ```
    {: screen}

2.  Verify that the token was created.

    ```
    ibmcloud cr token-list
    ```
    {: pre}

### Using a token to automate access to your namespaces
{: #registry_tokens_use}

You can use a token in your `docker login` command to automate access to your namespaces in {{site.data.keyword.registrylong_notm}}. Depending on whether you set read-only or read/write access for your token, users can push and pull images to and from your namespaces.
{:shortdesc}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  List all tokens in your {{site.data.keyword.Bluemix_notm}} account and note the token ID that you want to use.

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  Retrieve the token value for the token. Replace &lt;token_id&gt; with the ID of the token.

    ```
    ibmcloud cr token-get <token_id>
    ```
    {: pre}

    Your token value is displayed in **Token** in your CLI output.

4.  Use the token as part of your `docker login` command. Replace &lt;token_value&gt; with the token value that you retrieved in the previous step and &lt;registry_url&gt; with the URL to the registry where your namespaces are set up.

    -   For namespaces set up in US-South: `registry.ng.bluemix.net`
    -   For namespaces set up in UK-South: `registry.eu-gb.bluemix.net`
    -   For namespaces set up in EU-Central: `registry.eu-de.bluemix.net`
    -   For namespaces set up in AP-South: `registry.au-syd.bluemix.net`

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}
    
    For the `-u` parameter, ensure that you type in the string `token`, not the token ID.
    {: tip}

    After you log in to Docker by using the token, you can push or pull images to and from your namespaces.

### Removing a token from your {{site.data.keyword.Bluemix_notm}} account
{: #registry_tokens_remove}

Remove a {{site.data.keyword.registrylong_notm}} token when you do not need it anymore.
{:shortdesc}

Expired {{site.data.keyword.registrylong_notm}} tokens are removed automatically from your {{site.data.keyword.Bluemix_notm}} account and do not need to be removed manually.
{:tip}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  List all tokens in your {{site.data.keyword.Bluemix_notm}} account and note the token ID that you want to remove.

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  Remove the token.

    ```
    ibmcloud cr token-rm <token_id>
    ```
    {: pre}

## Authentication options for all clients
{: #registry_authentication}

You can authenticate by using the `docker login` command or other registry clients. 
{:shortdesc}

Most users can use the `ibmcloud cr login` command to simplify `docker login`, but if you are implementing automation or you are using a different client, you might want to authenticate manually. You must present a user name and password. In {{site.data.keyword.registrylong_notm}}, the user name indicates the type of secret that is presented in the password.

The following user names are valid:

-  `iambearer` The password contains an IAM access token. This type of authentication is short lived, but can be derived from all types of IAM identity.
-  `iamrefresh` The password must contain an IAM refresh token that is used internally to generate and refresh an IAM access token. This type of authentication is longer lived and is used by the `ibmcloud cr login` command.
-  `iamapikey` The password is an IAM API key. This type of authentication is the preferred type for automation. You can use either a user or service ID API key, see [Creating an API key](#registry_api_key_create).
-  `token` The password is a registry token. You can use this user name for automation.

You do not have to use the `docker` command to authenticate with the registry. For example, you can run the following `ibmcloud cf push` command that authenticates and authorizes a pull from the registry by using an IAM API key:

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o registry.<region>.bluemix.net/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Replace _&lt;apikey&gt;_ with your API key, _&lt;region&gt;_ with the name of your [region](registry_overview.html#registry_regions), _&lt;my_namespace&gt;_ with your namespace, and _&lt;image_repo&gt;_ with the repository.

For more information, see [Using a private image registry](/docs/services/ContinuousDelivery/pipeline_custom_docker_images.html#private_image_registry).
