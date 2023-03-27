---

copyright:
  years: 2023
lastupdated: "2023-03-27"

keywords: registry, access, authorization required, error, API key, client, token, region

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting authorization required errors?
{: #troubleshoot-auth-req}
{: troubleshoot}
{: support}

You're trying to access {{site.data.keyword.registrylong}} but are getting `Authorization required` errors.
{: shortdesc}

When you try to access {{site.data.keyword.registryshort}}, you get one of the following messages.
{: tsSymptoms}

- `Authorization required.`
- `You were not authorized to complete this operation.`
- `An error occurred when authenticating your request.`
- `Status code 401 Unauthorized`
    You might see this message if you're using {{site.data.keyword.codeenginefull_notm}}. For more information, see [Why am I getting an unauthorized error when I'm using {{site.data.keyword.codeengineshort}}?](/docs/Registry?topic=Registry-troubleshoot-unauthorized-ce)

The following alternatives are possible causes:
{: tsCauses}

- You attempted to log in to {{site.data.keyword.registryshort}} with an invalid API key.
- You attempted to access {{site.data.keyword.registryshort}} without logging in.
- A client attempted to access {{site.data.keyword.registryshort}} without a bearer token.
- A client attempted to access {{site.data.keyword.registryshort}} with an expired OAuth token.
- You attempted to authenticate against the {{site.data.keyword.registryshort}} API with an invalid API key.
- You attempted to authenticate against the {{site.data.keyword.registryshort}} API with an invalid Account ID.
- You logged in to a different region of {{site.data.keyword.registryshort}}.

You can fix this problem in the following ways:
{: tsResolve}

- Check the information about logging a client into {{site.data.keyword.registryshort}}, see [Push images to your namespace](/docs/Registry?topic=Registry-getting-started&interface=ui#gs_registry_images_pushing) in [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started&interface=ui).
- Create and use a valid IAM API key to log a client, such as Docker, in to {{site.data.keyword.registryshort}} with username `iamapikey` and the API key as your password. For more information, see [Managing user API keys](/docs/account?topic=account-userapikey&interface=ui#userapikey).
- Use the `ibmcloud` CLI or IAM API to retrieve a valid OAuth token to authenticate against the {{site.data.keyword.registryshort}} API. For more information, see [{{site.data.keyword.registrylong_notm}} API - Authentication](https://{DomainName}/apidocs/container-registry#authentication).
- When you authenticate against the {{site.data.keyword.registryshort}} API, ensure that you use a valid Account ID.
- When you access {{site.data.keyword.registryshort}} by using automation, set up a service ID and API key. For more information, see [Accessing {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_access#registry_access_serviceid_apikey_create).
- If your image is in a different region of {{site.data.keyword.registryshort}}, you must log in to {{site.data.keyword.cloud_notm}} in that region by runnning the [`ibmcloud cr region-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set) and [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login) commands. For more information, see [Targeting a local region](/docs/Registry?topic=Registry-registry_overview#registry_regions).
