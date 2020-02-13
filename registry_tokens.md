---

copyright:
  years: 2017, 2020
lastupdated: "2020-02-13"

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
{:term: .term}
{:external: target="_blank" .external}

# Automating access to {{site.data.keyword.registrylong_notm}}
{: #registry_access}

To automate access to your {{site.data.keyword.registrylong}} namespaces so that you can push and pull images, use {{site.data.keyword.iamlong}} (IAM) [API keys](/docs/iam?topic=iam-manapikey#ibm-cloud-api-keys).
{:shortdesc}

If you want to use your registry images in Kubernetes deployments, see [Using an image pull secret in other Kubernetes namespaces or to access images in other accounts](/docs/containers?topic=containers-images#other).
{: tip}

API keys are linked to user and service IDs in your account and you can use them across {{site.data.keyword.cloud_notm}}. You can use an API key in the CLI or as part of automation to authenticate as your user or service identity. A [user API key](#registry_access_user_apikey) is associated with a user and their access policies. A [service ID API key](#registry_access_serviceid_apikey) has it's own access policies. You can have several service IDs with different fine grained policies so that your automation is granted specific and limited capabilities.

To set up and manage IAM policies, see [Defining access role policies](/docs/Registry?topic=registry-user#user).

## Automating access to your namespaces by using service ID API keys
{: #registry_access_serviceid_apikey}

You can use service ID API keys to automate the pushing and pulling of container images to and from your namespaces.
{:shortdesc}

When you create an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster, the cluster is created with an {{site.data.keyword.cloud_notm}} IAM service ID that is given an IAM **Reader** service access role policy to {{site.data.keyword.registrylong_notm}}. The service ID credentials are authenticated in a non-expiring service ID API key that is stored in image pull secrets in your cluster. The image pull secrets are added to the `default` Kubernetes namespace and to the list of secrets in the `default` service account for this Kubernetes namespace. If you require more service ID API keys or the service ID API key is missing, you can [create a service ID API key manually](#registry_access_serviceid_apikey_create).

You can use service ID API keys in the following places:

- {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} clusters. When you create {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}} clusters, one service ID is automatically created for each cluster. If you want more than one service ID, you can create them manually.
- Kubernetes and Red Hat OpenShift clusters that aren't on {{site.data.keyword.cloud_notm}}. You must create your own service ID, API key, and pull secret.
- Docker CLI and other clients.  You must create your own service ID and API key.

### Creating a service ID API key manually
{: #registry_access_serviceid_apikey_create}

Create a service ID API key that you can use to log in to your registry.
{:shortdesc}

To create a service ID API key, complete the following steps:

1. Create a service ID, see [`ibmcloud iam service-id-create`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_service_id_create).

2. Assign service policies to the service ID to control the level of access that is allowed when the service ID is used to authenticate with {{site.data.keyword.registrylong}}, see [Managing service ID access policies](/docs/iam?topic=iam-serviceidpolicy).

3. Create a service ID API key, see [Managing service ID API keys](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys) and [`ibmcloud iam service-api-key-create`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_create).

## Automating access to your namespaces by using user API keys
{: #registry_access_user_apikey}

You can use user API keys to automate the pushing and pulling of Docker images to and from your namespaces.
{: shortdesc}

### Creating a user API key manually
{: #registry_access_user_apikey_create}

Create a user API key that you can use to log in to your registry.
{:shortdesc}

If you create a user API key, the access policies are those of the user.

To create a user API key, see [Managing user API keys](/docs/iam?topic=iam-userapikey) and [`ibmcloud iam api-key-create`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Authentication
{: #registry_access_apikey_auth}

Use an API key to automate access to your namespaces in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Most users can use the `ibmcloud cr login` command to simplify `docker login`, but if you are implementing automation or you are using a different client, you might want to authenticate manually. You must present a username and password. In {{site.data.keyword.registrylong_notm}}, the username indicates the type of secret that is presented in the password.

The following usernames are valid:

- `iambearer` The password contains an IAM access token. This type of authentication is short lived, but can be derived from all types of IAM identity. For example, from [`ibmcloud iam oauth-tokens`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_oauth_tokens).
- `iamrefresh` The password must contain an IAM refresh token that is used internally to generate and refresh an IAM access token. This type of authentication is longer lived. This authentication type is used by the `ibmcloud cr login` command.
- `iamapikey` The password is an IAM API key. This type of authentication is the preferred type for automation. You can use either a user or service ID API key, see [Automating access to your namespaces by using service ID API keys](#registry_access_serviceid_apikey) and [Automating access to your namespaces by using user API keys](#registry_access_user_apikey).

You can authenticate by using one of the following clients:

- [Docker](#registry_access_apikey_auth_docker)
- [Other registry clients](#registry_access_apikey_auth_other), such as skopeo, Podman, or any tool that's supported by the {{site.data.keyword.registrylong}} V2 API.

### Using Docker to authenticate with an API key
{: #registry_access_apikey_auth_docker}

You can use Docker to authenticate with the registry so that you can push and pull images to and from the registry.
{: shortdesc}

Use the API key to log in to your registry by running the following Docker command. Replace `<apikey>` with your API key and `<registry_url>` with the URL to the registry where your namespaces are set up.

- For namespaces set up in AP-North, use `jp.icr.io`
- For namespaces set up in AP-South, use `au.icr.io`
- For namespaces set up in EU-Central, use `de.icr.io`
- For namespaces set up in UK-South, use `uk.icr.io`
- For namespaces set up in US-South, use `us.icr.io`

```
docker login -u iamapikey -p <apikey> <registry_url>
```
{: pre}

### Using clients other than Docker to authenticate with an API key
{: #registry_access_apikey_auth_other}

You can use clients other than Docker to authenticate with the registry so that you can push and pull images to and from the registry.
{: shortdesc}

For more information, see [Using a private image registry](/docs/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).

#### Example: skopeo
{: #registry_access_apikey_auth_other_example_skopeo}

You can use skopeo to authenticate with the registry. Replace `<region>` with the name of your [region](/docs/Registry?topic=registry-registry_overview#registry_regions), for example `us`, `<namespace>` with your namespace, and `<apikey>` with your API key,.

```
skopeo --insecure-policy --override-os linux copy docker://busybox:latest docker://<region>.icr.io/<namespace>/busybox:copy --dest-creds iamapikey:<apikey>
```
{: pre}

#### Example: Cloud Foundry
{: #registry_access_apikey_auth_other_example_cf}

You can start Cloud Foundry apps from images in the registry by using the Cloud Foundry CLI. Replace `<apikey>` with your API key, `<region>` with the name of your [region](/docs/Registry?topic=registry-registry_overview#registry_regions), for example `us`, `<namespace>` with your namespace, and `<image_repo>` with the repository.

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<namespace>/<image_repo> --docker-username iamapikey
```
{: pre}
