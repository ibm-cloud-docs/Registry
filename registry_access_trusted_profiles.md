---

copyright:
  years: 2025
lastupdated: "2025-08-12"

keywords: API key, tokens, automating access, access, authentication, Podman, Skopeo, Buildah, Docker, client, authenticate, iam, domain, service id api key, trusted profiles,

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Accessing {{site.data.keyword.registryshort_notm}} by using trusted profiles
{: #registry_access_trusted_profiles}

You can use trusted profiles to grant different {{site.data.keyword.cloud}} identities access to {{site.data.keyword.registrylong_notm}} resources in your account. Automatically grant federated users access to your account with conditions based on SAML attributes from your corporate directory.
{: shortdesc}

A user does not need to be a member of the account to assume a trusted profile. A user can use the profile if the user's identity provider (IdP) matches an IdP used in the conditions of trust.

When you initially create a trusted profile, you can build conditions of trust with the following entity types: federated users and service IDs. After you create the trusted profile, you can add more conditions to combine multiple entity types in the same profile.

For more information about trusted profiles, see [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=cli#create-profile-serviceid-cli).

## Accessing namespaces in automation by using a trusted profile
{: #registry_access_trusted_profiles_auto}

You can use service ID API keys to automate the pushing and pulling of container images to and from namespaces that the trusted profile has access to.

You can use service ID API keys in the following places:

- {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} clusters.
- Kubernetes and {{site.data.keyword.redhat_openshift_full}} clusters that aren't on {{site.data.keyword.cloud_notm}}.
- Docker command-line interface (CLI) and other clients.

### Creating a trusted profile
{: #registry_access_trusted_profiles_create}

A trusted profile needs to be created in the same account as the registry resources you want to access. A service ID in a separate account can then be added to that trusted profile to establish trust, see [Establishing trust with service IDs by using the CLI](/docs/account?topic=account-create-trusted-profile&interface=cli#create-profile-serviceid-cli). Make a note of the trusted profile ID because it is used as the username for the login.

### Creating a service ID API key manually
{: #registry_access_trusted_profiles_serviceid_apikey_create}
{: help}
{: support}

Create a service ID API key that you can use to log in to the registry.

To create a service ID API key, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys) and [`ibmcloud iam service-api-key-create`](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_create).

### Using client software to authenticate in automation
{: #registry_access_trusted_profiles_apikey_auth}

Use an API key to log in to the registry by using common clients.

Clients require an API key, username, and a domain, replace `API_KEY` with your API key, `PROFILE_ID` with the trusted profile ID, and `REGISTRY_DOMAIN` with the domain of the registry where your namespaces are set up.

{{registry_access.md#table_registry_access_domains}}

For more information about how to use {{site.data.keyword.registrylong_notm}} in a {{site.data.keyword.contdelivery_short}} pipeline, see [Using a private image registry](/docs/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).

Examples of how to authenticate automatically with the registry are provided for the following clients:

- [Buildah](#registry_access_trusted_profiles_apikey_auth_buildah)
- [Docker](#registry_access_trusted_profiles_apikey_auth_docker)
- [Podman](#registry_access_trusted_profiles_apikey_auth_podman)
- [Skopeo](#registry_access_trusted_profiles_apikey_auth_skopeo)

If you get a **400 Bad Request** message, the username and password combination is not valid.
{: tip}

#### Using Buildah to authenticate with the registry by using trusted profiles
{: #registry_access_trusted_profiles_apikey_auth_buildah}

You can use Buildah to authenticate with the registry so that you can push and pull images to and from the registry.

Use the API key, profile ID, and [domain](#registry_access_trusted_profiles_apikey_auth) to log in to the registry by running the following Buildah command, replace `PROFILE_ID` with the trusted profile ID, `API_KEY` with the API key, and `REGISTRY_DOMAIN` with the domain:

```txt
buildah login -u PROFILE_ID -p API_KEY REGISTRY_DOMAIN
```
{: pre}

#### Using Docker to authenticate with the registry by using trusted profiles
{: #registry_access_trusted_profiles_apikey_auth_docker}

You can use Docker to authenticate with the registry so that you can push and pull images to and from the registry.

Use the API key and [domain](#registry_access_trusted_profiles_apikey_auth) to log in to the registry by running the following Docker command, replace `PROFILE_ID` with the trusted profile ID, `API_KEY` with the API key, and `REGISTRY_DOMAIN` with the domain:

```txt
docker login -u PROFILE_ID -p API_KEY REGISTRY_DOMAIN
```
{: pre}

#### Using Podman to authenticate with the registry by using trusted profiles
{: #registry_access_trusted_profiles_apikey_auth_podman}

You can use Podman to authenticate with the registry so that you can push and pull images to and from the registry.

Use the API key and [domain](#registry_access_trusted_profiles_apikey_auth) to log in to the registry by running the following Podman command, replace `PROFILE_ID` with the trusted profile ID, `API_KEY` with the API key, and `REGISTRY_DOMAIN` with the domain:

```txt
podman login -u PROFILE_ID -p API_KEY REGISTRY_DOMAIN
```
{: pre}

#### Using Skopeo to authenticate with the registry by using trusted profiles
{: #registry_access_trusted_profiles_apikey_auth_skopeo}

You can use Skopeo to authenticate with the registry so that you can push and pull images to and from the registry.

For example, you can use the following Skopeo command to pull an image from Docker Hub and push it to your namespace. Replace `REGISTRY_DOMAIN` with the name of your [domain](#registry_access_trusted_profiles_apikey_auth), `NAMESPACE` with your namespace, `PROFILE_ID` with the trusted profile ID, `API_KEY` with your API key:

```txt
skopeo --insecure-policy --override-os linux copy docker://busybox:latest docker://REGISTRY_DOMAIN/NAMESPACE/busybox:latest --dest-creds PROFILE_ID:API_KEY
```
{: pre}
