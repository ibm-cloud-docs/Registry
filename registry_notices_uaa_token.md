---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-02"

keywords: IBM Cloud Container Registry notices, notices, uaa tokens

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Announcing the end of {{site.data.keyword.registryshort}} support for UAA tokens from 12 August 2020
{: #registry_notices_uaa_token}

{{site.data.keyword.registrylong}} will not accept UAA tokens for authentication from 12 August 2020.
{: shortdesc}

{{site.data.keyword.registryshort}} supported IAM as its main form of authentication for several years. In parallel, {{site.data.keyword.registryshort}} continued to support UAA and registry tokens as deprecated forms of authentication. On 12 August 2020, UAA tokens will no longer be accepted for authenticating to {{site.data.keyword.registryshort}}. Registry tokens continue to work, but the end of support date for registry tokens is not available yet. All customers who are not already doing so must use IAM for authenticating to {{site.data.keyword.registryshort}}.

## Next steps to use IAM for authentication
{: #registry_notices_uaa_token_next}

If you have any automation that uses registry or UAA tokens to authenticate to {{site.data.keyword.registryshort}}, you need to update your automation to use IAM instead. For example, any scripts that perform an explicit `docker login` and pass something other than the IAM usernames mentioned here must be updated to instead pass a form of IAM authentication. API keys are the recommended approach for automation. Note `ibmcloud cr login` performs a `docker login` in the background, but it is already updated to log in with IAM.

Kubernetes clusters can use image pull secrets to pull images from private registries. If any Kubernetes namespaces in your cluster rely on pull secrets that contain a registry or UAA token, they need to be replaced with pull secrets that contain an IAM API key.

{{site.data.keyword.containerlong_notm}} clusters that were created before 25 February 2019, do not have IAM API keys in pull secrets and must be updated. This update is automated by the {{site.data.keyword.registryshort}} CLI plug-in, and instructions can be found here. Clusters that were created after 25 February 2019, already contain updated pull secrets. However, if you copied pull secrets that contain registry tokens to any Kubernetes namespaces other than default, you must ensure that those pull secrets contain an API key.

## Summary
{: #registry_notices_uaa_token_summary}

On 12 August 2020, UAA tokens will no longer be accepted to authenticate to {{site.data.keyword.registryshort}}. Registry tokens continue to work but are deprecated. An end of support date is not available yet. Ensure that you are not using UAA tokens for authentication and consider removing all uses of registry tokens and migrating fully to IAM. API keys are the recommended approach for automation and pull secrets.

Many benefits exist for using IAM API keys instead of registry tokens. With IAM API keys, you can add IAM policies for more fine-grained control over access. For example, you can create IAM access policies to restrict permissions to specific registry namespaces so that a cluster can pull images from those namespaces only.

## Original announcement
{: #registry_notices_uaa_token_announce}

The original announcement was published on 3 February 2020.
