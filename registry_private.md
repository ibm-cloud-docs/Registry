---

copyright:
  years: 2020, 2021
lastupdated: "2021-05-10"

keywords: private DNS, isolation for IBM Cloud Container Registry, service endpoints for IBM Cloud Container Registry, private network for IBM Cloud Container Registry, network isolation in IBM Cloud Container Registry, non-public routes for IBM Cloud Container Registry, private connection for IBM Cloud Container Registry

subcollection: Registry

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

# Securing your connection to {{site.data.keyword.registryshort_notm}}
{: #registry_private}

You can use private network connections to securely route your data in {{site.data.keyword.registrylong}}.
{: shortdesc}

If you use cloud-based services for production workloads, you can use a secure private connection so that you ensure that you adhere to any compliance regulations. You can use {{site.data.keyword.cloud_notm}} service endpoints to connect to {{site.data.keyword.cloud_notm}} services over the private {{site.data.keyword.cloud_notm}} network.

Service endpoints make it easier to securely route network traffic between different {{site.data.keyword.cloud_notm}} services and your registry over the private {{site.data.keyword.cloud_notm}} network. This network routing ensures that your data doesn't go over the public internet.

To learn more about {{site.data.keyword.cloud_notm}} service endpoints, see [Secure access to services by using service endpoints](/docs/account?topic=account-service-endpoints-overview).

## Using private network connections for image pushes and pulls
{: #registry_private_images}

You must set up your account with the correct authority so that you can set up a private network connection for pushing and pulling images.
{: shortdesc}

{{site.data.keyword.registrylong_notm}} is a multi-tenant offering and you are, therefore, not required to create your own service endpoints to connect to the registry over private connections.

### Enabling {{site.data.keyword.cloud_notm}} service endpoint support for the account
{: #registry_private_images_endpoints}

To connect to {{site.data.keyword.cloud_notm}} services over a private network, you must meet the following criteria.

- You must be able to access the classic infrastructure.
- You must enable [virtual routing and forwarding](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) (VRF) and connectivity to service endpoints for your account.
- You must also have a billable account.

To enable your {{site.data.keyword.cloud_notm}} account to use virtual routing and forwarding (VRF) and service endpoints, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

### Considerations
{: #registry_private_images_considerations}

- Private domain names aren't used by the container-registry CLI plug-in. If you push an image on the private domain name, and then use the CLI on a public connection to run the `ibmcloud cr images` command, the image is listed with all the other images that have the same public domain name.

- If you have private {{site.data.keyword.containerlong_notm}} clusters, you aren't required to change anything. {{site.data.keyword.containerlong_notm}} already modifies the connection, which is referenced by the public domain name, to use a private connection. This behavior is unchanged.

  - If you use {{site.data.keyword.containerlong_notm}}, you can optionally reference your images from private clusters by using the private registry domain name. However, you must create more `imagePullSecrets` for the extra domain names, see [Understanding how to authorize your cluster to pull images from a registry](/docs/openshift?topic=openshift-registry#cluster_registry_auth).

- Pull traffic is not charged for image pulls that use private connections.

- If you use [image signing](/docs/Registry?topic=Registry-registry_trustedcontent) and want to use the private domain names, you must re-sign any images that you already have because the domain name forms part of the signed artifact.

### Pushing and pulling images
{: #registry_private_images_push}

Private connections are available so that you can push and pull images. You use the same `icr.io` domain name, with the prefix `private.`, see [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

You can't use private connections for image management operations by using the {{site.data.keyword.registrylong_notm}} CLI.
{: note}

1. Run the `docker login` command to authenticate with your registry. Replace `<apikey>` with your API key and `<private_registry_url>` with the URL to the private registry where your namespaces are set up. The private registry URLs are described in the following list.

   - For namespaces that are set up in `ap-north`, use the following private registry URL `private.jp.icr.io`.
   - For namespaces that are set up in `ap-south`, use the following private registry URL `private.au.icr.io`.
   - For namespaces that are set up in `ca-tor`, use the following private registry URL `private.ca.icr.io`.
   - For namespaces that are set up in `eu-central`, use the following private registry URL `private.de.icr.io`.
   - For namespaces that are set up in `jp-osa`, use the following private registry URL `private.jp2.icr.io`.
   - For namespaces that are set up in `uk-south`, use the following private registry URL `private.uk.icr.io`.
   - For namespaces that are set up in `us-south`, use the following private registry URL `private.us.icr.io`.

   ```
   docker login -u iamapikey -p <apikey> <private_registry_url>
   ```
   {: pre}

   For more information, see [Automating access to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_access).

## Enforcing access to your account over private network connections
{: #registry_private_account}

You can prevent or allow image pulls or pushes over public network connections for your account by using the [`ibmcloud cr private-only`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only) command.

You can also use this command to check whether the use of private connections is set for your account.

After you enable the use of private connections on your account, any attempts to pull and push images or access signatures over the public network are rejected.
{: important}

Because the use of private connections doesn't apply to the management API, you can still use the CLI over a public connection.
{: tip}

- To prevent image pulls or pushes over public network connections for your account, run the following command.

  ```
  ibmcloud cr private-only --enable
  ```
  {: pre}

- To reinstate image pulls or pushes over public network connections for your account, run the following command.

  ```
  ibmcloud cr private-only --disable
  ```
  {: pre}

- To check whether the use of public connections is prevented for image pushes or pulls in your account, run the following command.
  
  ```
  ibmcloud cr private-only --status
  ```
  {: pre}
