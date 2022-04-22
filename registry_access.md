---

copyright:
  years: 2017, 2022
lastupdated: "2022-04-22"

keywords: API key, tokens, automating access, creating API keys, access, authentication, podman, skopeo, buildah, docker, client, authenticate, iam, domain, service id api key, user api key

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Accessing {{site.data.keyword.registrylong_notm}}
{: #registry_access}

To access your {{site.data.keyword.registrylong}} namespaces so that you can push and pull images, use {{site.data.keyword.iamlong}} (IAM).
{: shortdesc}

To set up and manage IAM access policies, see [Defining IAM access policies](/docs/Registry?topic=Registry-user#user).

From 5 July 2022, all accounts will require IAM access policies. If you started to use {{site.data.keyword.registryshort}} before the availability of [IAM API key policies in {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#registry-25feb2019) in February 2019, you must now ensure that you are using IAM access policies to manage access to the {{site.data.keyword.registrylong_notm}} service. For more information, see [IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy) and [Defining IAM access policies](/docs/Registry?topic=Registry-user).
{: important}

If you want to use your container images in Kubernetes deployments, see [Using an image pull secret to access images in other {{site.data.keyword.cloud_notm}} accounts or external private registries from nondefault Kubernetes namespaces](/docs/containers?topic=containers-registry#other).
{: tip}

Access to {{site.data.keyword.registrylong_notm}} is either [automated](#registry_access_automating), which typically uses [API keys](/docs/account?topic=account-manapikey), or [interactive](#registry_access_interactive), which typically uses bearer tokens.

## Accessing your namespaces in automation
{: #registry_access_automating}

You can use service ID API keys to automate the pushing and pulling of container images to and from your namespaces.

[API keys](x8051010){: term} are linked to user IDs or service IDs in your account and you can use them across {{site.data.keyword.cloud}}. You can use an API key in the CLI or as part of automation to authenticate as your user or service identity. A [user API key](#registry_access_user_apikey_create) is associated with a user and their access policies. A [service ID API key](#registry_access_serviceid_apikey_create) has its own access policies. You can have several service IDs with different fine grained policies so that your automation is granted specific and limited capabilities.

When you create an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong}} cluster, the cluster is created with an {{site.data.keyword.cloud_notm}} IAM service ID that is given an IAM Reader service access policy to {{site.data.keyword.registrylong_notm}}. The service ID credentials are authenticated in a nonexpiring service ID API key that is stored in image pull secrets in your cluster. The image pull secrets are added to the `default` Kubernetes namespace and to the list of secrets in the `default` service account for this Kubernetes namespace. If you require more service ID API keys or the service ID API key is missing, you can [create a service ID API key manually](#registry_access_serviceid_apikey_create).

You can use service ID API keys in the following places:

- {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} clusters. When you create {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}} clusters, one service ID is automatically created for each cluster. If you want more than one service ID, you can create them manually.
- Kubernetes and {{site.data.keyword.redhat_openshift_full}} clusters that aren't on {{site.data.keyword.cloud_notm}}. You must create your own service ID, API key, and pull secret.
- Docker CLI and other clients. You must create your own service ID and API key.

### Creating a service ID API key manually
{: #registry_access_serviceid_apikey_create}
{: help}
{: support}

Create a service ID API key that you can use to log in to the registry.

To create a service ID API key, complete the following steps:

1. Create a service ID, see [`ibmcloud iam service-id-create`](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_id_create).

2. Assign service policies to the service ID to control the level of access that is allowed when the service ID is used to authenticate with {{site.data.keyword.registrylong_notm}}, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

3. Create a service ID API key, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys) and [`ibmcloud iam service-api-key-create`](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_create).

### Creating a user API key manually
{: #registry_access_user_apikey_create}
{: help}
{: support}

Create a user API key that you can use to log in to the registry.

If you create a user API key, the user's access policies are used.

To create a user API key, see [Managing user API keys](/docs/account?topic=account-userapikey) and [`ibmcloud iam api-key-create`](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

### Using client software to authenticate in automation
{: #registry_access_apikey_auth}

Use an API key to log in to the registry by using common clients.

Clients require an API key and a domain, replace `<apikey>` with your API key and `<registry_domain>` with the domain of the registry where your namespaces are set up.

| Region | `<registry_domain>` |
|--------|-----------------|
| `global` | `icr.io` |
| `ap-north` | `jp.icr.io` |
| `ap-south` | `au.icr.io` |
| `br-sao` | `br.icr.io` |
| `ca-tor` | `ca.icr.io` |
| `eu-central` | `de.icr.io` |
| `jp-osa` | `jp2.icr.io` |
| `uk-south` | `uk.icr.io` |
| `us-south` | `us.icr.io` |
{: caption="Table 1. Registry domains" caption-side="bottom"}

For more information about how to use {{site.data.keyword.registrylong_notm}} in a {{site.data.keyword.contdelivery_short}} pipeline, see [Using a private image registry](/docs/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).

Examples of how to authenticate automatically with the registry are provided for the following clients:

- [Buildah](#registry_access_apikey_auth_example_other_buildah)
- [Docker](#registry_access_apikey_auth_docker)
- [Podman](#registry_access_apikey_auth_example_other_podman)
- [Skopeo](#registry_access_apikey_auth_other_example_skopeo)

#### Buildah
{: #registry_access_apikey_auth_example_other_buildah}

You can use Buildah to authenticate with the registry so that you can push and pull images to and from the registry.

Use the API key and [domain](#registry_access_apikey_auth) to log in to the registry by running the following Buildah command, replace `<apikey>` with the API key and `<registry_domain>` with the domain:

```txt
buildah login -u iamapikey -p <apikey> <registry_domain>
```
{: pre}

#### Docker
{: #registry_access_apikey_auth_docker}

You can use Docker to authenticate with the registry so that you can push and pull images to and from the registry.

Use the API key and [domain](#registry_access_apikey_auth) to log in to the registry by running the following Docker command, replace `<apikey>` with the API key and `<registry_domain>` with the domain:

```txt
docker login -u iamapikey -p <apikey> <registry_domain>
```
{: pre}

#### Podman
{: #registry_access_apikey_auth_example_other_podman}

You can use Podman to authenticate with the registry so that you can push and pull images to and from the registry.

Use the API key and [domain](#registry_access_apikey_auth) to log in to the registry by running the following Podman command, replace `<apikey>` with the API key and `<registry_domain>` with the domain:

```txt
podman login -u iamapikey -p <apikey> <registry_domain>
```
{: pre}

#### Skopeo
{: #registry_access_apikey_auth_other_example_skopeo}

You can use Skopeo to authenticate with the registry so that you can push and pull images to and from the registry.

For example, you can use the following Skopeo command to pull an image from Docker Hub and push it to your namespace. Replace `<registry_domain>` with the name of your [domain](#registry_access_apikey_auth), `<namespace>` with your namespace, and `<apikey>` with your API key:

```txt
skopeo --insecure-policy --override-os linux copy docker://busybox:latest docker://<registry_domain>/<namespace>/busybox:latest --dest-creds iamapikey:<apikey>
```
{: pre}

## Accessing your namespaces interactively
{: #registry_access_interactive}

You can use bearer tokens and refresh tokens to push and pull images to and from your namespaces interactively.

Examples of how to access your namespaces interactively are provided for the following clients:

- [Buildah](#registry_access_interactive_auth_buildah)
- [Docker](#registry_access_interactive_auth_docker)
- [Podman](#registry_access_interactive_auth_podman)
- [Skopeo](#registry_access_interactive_auth_skopeo)

### Buildah
{: #registry_access_interactive_auth_buildah}

Log in to the registry by using the Buildah CLI.

You can use the Buildah CLI to log in to the registry by using a bearer token, replace `<registry_domain>` with the [domain](#registry_access_apikey_auth):

```txt
ibmcloud iam oauth-tokens | sed -ne '/IAM token/s/.* //p' | buildah login -u iambearer --password-stdin <registry_domain>
```
{: pre}

### Docker
{: #registry_access_interactive_auth_docker}

Log in to the registry by using the Docker CLI.

You can use the Docker CLI to log in to the registry by using a refresh token in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started):

```txt
ibmcloud cr login --client docker
```
{: pre}

You can use the Docker CLI to log in to the registry by using a bearer token:

1. Generate a bearer token by using [`ibmcloud iam oauth-tokens`](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_oauth_tokens).

2. Log in to the registry by using the `docker login` command. Replace `<bearer_token>` with your bearer token and `<registry_domain>` with the [domain](#registry_access_apikey_auth):

    ```txt
    docker login -u iambearer --password <bearer_token> <registry_domain>
    ```
    {: pre}

### Podman
{: #registry_access_interactive_auth_podman}

Log in to the registry by using the CLI.

```txt
ibmcloud cr login --client podman
```
{: pre}

### Skopeo
{: #registry_access_interactive_auth_skopeo}

Log in to the registry by using the Skopeo CLI.

You can use the Skopeo CLI to log in to the registry by using a bearer token, replace `<registry_domain>` with the [domain](#registry_access_apikey_auth):

```txt
ibmcloud iam oauth-tokens | sed -ne '/IAM token/s/.* //p' | skopeo login -u iambearer --password-stdin <registry_domain>
```
{: pre}

## Accessing your namespaces programmatically
{: #registry_access_programmatic}

Use your own code to access to your namespaces in {{site.data.keyword.registrylong_notm}}.

Most users can use the [`ibmcloud cr login`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_login) command to simplify `docker login`, but if you are implementing automation or you are using a different client, you might want to authenticate manually. You must present a username and password. In {{site.data.keyword.registrylong_notm}}, the username indicates the type of secret that is presented in the password.

The following usernames are valid:

- `iambearer` The password contains an IAM [access token](x2113001){: term}. This type of authentication is short lived, but can be derived from all types of IAM identity. For example, from [`ibmcloud iam oauth-tokens`](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_oauth_tokens).
- `iamrefresh` The password contains an IAM refresh token that is used internally by the registry to generate an IAM access token. This type of authentication is longer lived. This authentication type is used by the `ibmcloud cr login` command.
- `iamapikey` The password is an IAM API key that is used internally by the registry to generate an IAM access token. This type of authentication is the preferred type for automation. You can use a user API key or a service ID API key. For more information, see [Accessing your namespaces in automation](#registry_access_automating).



