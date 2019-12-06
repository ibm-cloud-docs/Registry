---

copyright:
  years: 2017, 2019
lastupdated: "2019-12-06"

keywords: API keys, tokens, automating access, creating API keys, authenticating, access, authentication,

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

# Automating access to {{site.data.keyword.registrylong_notm}}
{: #registry_access}

You can use an {{site.data.keyword.iamlong}} (IAM) API key to automate access to your {{site.data.keyword.registrylong}} namespaces so that you can push and pull images.
{:shortdesc}

Are you trying to use your registry images in Kubernetes deployments? Check out [Accessing images in other Kubernetes namespaces, {{site.data.keyword.cloud_notm}} regions, and accounts](/docs/containers?topic=containers-images#other).
{: tip}

API keys are linked to your account and can be used across {{site.data.keyword.cloud_notm}} so that you don't need different credentials for each service. You can use the API key in the CLI or as part of automation to log in as your user identity.

If you use an API key, you can control access to your namespaces by using IAM policies. For more information, see [Defining user access role policies](/docs/services/Registry?topic=registry-user#user).

For more information about {{site.data.keyword.registrylong_notm}} API keys, see [Working with API keys](/docs/iam?topic=iam-manapikey#manapikey).

Before you begin, [install the {{site.data.keyword.registrylong_notm}} and Docker CLI](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Automating access to your namespaces by using API keys
{: #registry_api_key}

You can use API keys to automate the pushing and pulling of Docker images to and from your namespaces.
{:shortdesc}

### Creating an API key
{: #registry_api_key_create}

You can create an API key that you can then use to log in to your registry.
{:shortdesc}

You can create both user API keys and service ID API keys.

- To create a service ID API key, see [Creating an API key for a service ID](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
- To create a user API key, see [Creating an API key](/docs/iam?topic=iam-userapikey#create_user_key).

### Using an API key to automate access
{: #registry_api_key_use}

You can use an API key to automate access to your namespaces in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Use the API key to log in to your registry by running the following Docker command. Replace `<your_apikey>` with your API key, and replace `<registry_url>` with the URL to the registry where your namespaces are set up.

- For namespaces set up in AP-North, use `jp.icr.io`
- For namespaces set up in AP-South, use `au.icr.io`
- For namespaces set up in EU-Central, use `de.icr.io`
- For namespaces set up in UK-South, use `uk.icr.io`
- For namespaces set up in US-South, use `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

For reference information about the command, see [Create a new {{site.data.keyword.cloud_notm}} platform API key](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Authentication options for all clients
{: #registry_authentication}

You can authenticate by using the `docker login` command or other registry clients.
{:shortdesc}

Most users can use the `ibmcloud cr login` command to simplify `docker login`, but if you are implementing automation or you are using a different client, you might want to authenticate manually. You must present a user name and password. In {{site.data.keyword.registrylong_notm}}, the user name indicates the type of secret that is presented in the password.

The following user names are valid:

- `iambearer` The password contains an IAM access token. This type of authentication is short lived, but can be derived from all types of IAM identity.
- `iamrefresh` The password must contain an IAM refresh token that is used internally to generate and refresh an IAM access token. This type of authentication is longer lived and is used by the `ibmcloud cr login` command.
- `iamapikey` The password is an IAM API key. This type of authentication is the preferred type for automation. You can use either a user or service ID API key, see [Creating an API key](#registry_api_key_create).

You do not have to use the `docker` command to authenticate with the registry. For example, you can start Cloud Foundry apps from images in the registry by using the Cloud Foundry CLI:

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Replace `<apikey>` with your API key, `<region>` with the name of your [region](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` with your namespace, and `<image_repo>` with the repository.

For more information, see [Using a private image registry](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
