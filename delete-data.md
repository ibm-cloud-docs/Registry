---

copyright:
  years: 2020, 2023
lastupdated: "2023-01-31"

keywords: data, data encryption in IBM Cloud Container Registry, data storage for IBM Cloud Container Registry, personal data in IBM Cloud Container Registry, data deletion for IBM Cloud Container Registry, data in IBM Cloud Container Registry, data security in IBM Cloud Container Registry, deleting, namespace, images, private repositories, managing your data, service, data, trash

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Managing your data in {{site.data.keyword.registryshort_notm}}
{: #delete-data}

Information about your data and how it is stored in {{site.data.keyword.registrylong}}.
{: shortdesc}

The {{site.data.keyword.cloud_notm}} platform provides layered security controls across network and infrastructure. {{site.data.keyword.cloud_notm}} provides a group of security services that can be used by application developers to secure their mobile and web apps. For more information, see [How do I know that my data is safe?](/docs/overview?topic=overview-security)

## How your data is stored
{: #data-storage}

### Image data
{: #data-storage_image}

Image data is stored in {{site.data.keyword.cos_full_notm}}, which is encrypted at rest, and encrypted in transit between {{site.data.keyword.registrylong_notm}} and {{site.data.keyword.cos_full_notm}}. For more information about {{site.data.keyword.cos_full_notm}}, see [About IBM Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage).

Data that is stored in {{site.data.keyword.registrylong_notm}} is backed up regularly. For more information, see [High availability and disaster recovery](/docs/Registry?topic=Registry-ha-dr).

### Scanning data
{: #data-storage_va}

To scan images and containers in your account for security issues, {{site.data.keyword.registrylong_notm}} collects, stores, and processes the following information:

- Free-form fields, including IDs, descriptions, and image names ([registry](/docs/Registry?topic=Registry-registry_overview#overview_elements_registry), [namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace), [repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository) name, and image [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag))
- Metadata about the file modes and creation timestamps of the configuration files
- The content of system and application configuration files in images and containers
- Installed packages and libraries (including their versions)

Scan results, aggregated at a data center level, are processed to produce anonymized metrics to operate and improve the service. Scan results are deleted 30 days after they are generated. For more information, see [Data protection](/docs/Registry?topic=va-va_index#about_data_protection).

Do not put personal information into any field or location that {{site.data.keyword.registrylong_notm}} processes, as identified in the preceding list.
{: important}

## Deleting your data
{: #data-delete}

You can delete your {{site.data.keyword.registrylong_notm}} namespaces, images, and private repositories.

### Deleting the service
{: #data-delete_service}

When an {{site.data.keyword.cloud_notm}} account is canceled or removed, the resource instances that track the account's usage of {{site.data.keyword.registrylong_notm}} are deleted. As part of that action all namespaces, and the images that they contain, are removed in accordance with the data retention policy.

The {{site.data.keyword.registrylong_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.registrylong_notm}} service description, which you can find in the Service Description for {{site.data.keyword.cloud_notm}} in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).

### Deleting namespaces
{: #data-delete_namespaces}

If you no longer require a registry namespace, you can remove the namespace from your {{site.data.keyword.cloud_notm}} account. Deleting a namespace removes all images, trash, and trust information that is contained in the namespace. For more information, see [Removing namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_remove).

### Deleting images
{: #data-delete_images}

You can delete unwanted images from your private repository by using either the {{site.data.keyword.cloud_notm}} console or the CLI. For more information, see [Deleting images from your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove).

You can clean up your namespace by choosing to retain only the most recent images in each repository in that namespace in {{site.data.keyword.registrylong_notm}}. You can detect and delete old images from all the repositories in a namespace by running a one-off command, `ibmcloud cr retention-run`, or by setting a scheduled policy by running the `ibmcloud cr retention-policy-set` command. For more information, see [Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention).

### Deleting private repositories
{: #data-delete_private_repo}

You can delete private repositories that are no longer required, and any associated images, by using the {{site.data.keyword.cloud_notm}} console. For more information, see [Deleting a private repository and any associated images](/docs/Registry?topic=Registry-registry_images_#registry_repo_remove).

## Restoring deleted data
{: #data-restore}

You can restore images from the trash by [digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest) or by [tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag).

You can restore an image from the trash by running the `ibmcloud cr image-restore` command. To find out which images are in the trash, run the `ibmcloud cr trash-list` command. Images are stored in the trash for 30 days. For more information, see [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore).
