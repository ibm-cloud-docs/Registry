---

copyright:
  years: 2023, 2024
lastupdated: "2024-08-01"

keywords: registry, access, authorization required, error, API key, client, token, region, CRG0014E

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting `Authorization required` errors in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-auth-req}
{: troubleshoot}
{: support}

You are trying to access {{site.data.keyword.registrylong}} but are getting `Authorization required` errors.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get one of the following messages.
{: tsSymptoms}

- `Authorization required. See https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-auth-req`
- `You were not authorized to complete this operation.`
- `CRG0014E An error occurred when authenticating your request with IBM Cloud. Clear your browser cookies, log in to IBM Cloud, and try your request again.`
- `Status code 401 Unauthorized`, you might see this message if you are using {{site.data.keyword.codeenginefull_notm}}, see [Why am I getting an `Unauthorized` error when I'm using {{site.data.keyword.codeengineshort}}?](/docs/Registry?topic=Registry-troubleshoot-unauthorized-ce) for assistance.
- `UNAUTHORIZED: Authorization required`, you might see this message if you are using `cosign` with Podman, see [Why am I having problems when I try to pull an image with `cosign` when I'm using Podman?](/docs/Registry?topic=Registry-troubleshoot-cosign-podman) for assistance.

The following alternatives are possible causes:
{: tsCauses}

**Scenario A.** You're trying to push or a pull an image, but you don't have a valid credential.

- You attempted to log in to {{site.data.keyword.registryshort}} with an invalid API key.
- You attempted to access {{site.data.keyword.registryshort}} without logging in.
- A client attempted to access {{site.data.keyword.registryshort}} without a bearer token.
- A client attempted to access {{site.data.keyword.registryshort}} with an expired OAuth token.

For more information about how to fix this problem, see [Scenario A. You're trying to push or pull an image](#troubleshoot-auth-req-push-pull).

**Scenario B.** You're logged in to the wrong region of {{site.data.keyword.registryshort}}. To check which region you're logged in to, run the [`ibmcloud cr region`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region) command.

For more information about how to fix this problem, see [Scenario B. You're logged in to the wrong region](#troubleshoot-auth-req-region).

**Scenario C.** You're trying to use the API.

- You attempted to authenticate against the {{site.data.keyword.registryshort}} API with an invalid API key.
- You attempted to authenticate against the {{site.data.keyword.registryshort}} API with an invalid Account ID.

For more information about how to fix this problem, see [Scenario C. You're trying to use the API](#troubleshoot-auth-req-api).

You can fix this problem in the following ways:
{: tsResolve}

## Scenario A. You're trying to push or pull an image
{: #troubleshoot-auth-req-push-pull}

You can't access {{site.data.keyword.registryshort}} because you don't have a valid credential.

You can fix these problems in the following ways:

- Check the information about logging a client into {{site.data.keyword.registryshort}}, see [Push images to your namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pushing).
- Create and use a valid IAM API key to log a client, such as Docker, in to {{site.data.keyword.registryshort}} with username `iamapikey` and the API key as your password. For more information, see [Managing user API keys](/docs/account?topic=account-userapikey&interface=ui#userapikey).
- When you access {{site.data.keyword.registryshort}} by using automation, set up a service ID and API key. For more information, see [Accessing {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_access#registry_access_serviceid_apikey_create).

## Scenario B. You're logged in to the wrong region
{: #troubleshoot-auth-req-region}

You can't access {{site.data.keyword.registryshort}} because you're logged in to the wrong region.

To check which region you're logged in to, run the [`ibmcloud cr region`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region) command.

You can fix this problem in the following way:

If your image is in a different region of {{site.data.keyword.registryshort}}, you must log in to {{site.data.keyword.cloud_notm}} in the correct region by running the following commands.

1. `ibmcloud cr region-set <region>`, where `<region>` is the name of the region, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).
2. `ibmcloud cr login`

For more information, see [Targeting a local region](/docs/Registry?topic=Registry-registry_overview#registry_regions_local_target).

## Scenario C. You're trying to use the API
{: #troubleshoot-auth-req-api}

You can't access {{site.data.keyword.registryshort}} because you attempted to authenticate against the {{site.data.keyword.registryshort}} API with an invalid API key or Account ID.

You can fix this problem in the following ways:

- Use the `ibmcloud` CLI or IAM API to retrieve a valid OAuth token to authenticate against the {{site.data.keyword.registryshort}} API. For more information, see [{{site.data.keyword.registrylong_notm}} API - Authentication](https://{DomainName}/apidocs/container-registry#authentication).
- When you authenticate against the {{site.data.keyword.registryshort}} API, ensure that you use a valid Account ID. You can retrieve your Account ID by running the [`ibmcloud account show`](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_show) command.
