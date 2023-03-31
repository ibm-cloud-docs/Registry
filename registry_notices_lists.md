---

copyright:
  years: 2022, 2023
lastupdated: "2023-03-31"

keywords: IBM Cloud Container Registry notices, support, version, security status, lists

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort}} CLI stops returning security status results in lists by default from version 1.0.0
{: #registry_notices_lists}

From {{site.data.keyword.registrylong}} CLI plug-in version 1.0.0, when you use the `ibmcloud cr image-list` and `ibmcloud cr image-digests` commands to list images, they return Vulnerability Advisor security status results only if you use the `--va` option.
{: shortdesc}

The [`ibmcloud cr image-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list) and [`ibmcloud cr image-digests`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests) commands currently return the security status of each image by default. Some users store many images in the registry, and returning security status for every image when listing takes more processing time, which can lead to a poor experience and a smaller limit on the maximum number of images that can be listed.

To improve the user experience, a new major version, version 1.0.0, of the {{site.data.keyword.registrylong_notm}} CLI plug-in changes the default behavior for the `ibmcloud cr image-list` and `ibmcloud cr image-digests` commands so that they return Vulnerability Advisor security status results only if you use the `--va` option.

## Action required now
{: #registry_notices_lists_action}

If you want to continue to receive security status with your lists, prepare to upgrade by adding the new `--va` option to your commands.

If you require security status with your lists, add the `--restrict` option when you're using the `ibmcloud cr image-list` and `ibmcloud cr image-digests` commands to receive just the information that you require.

If you are an API user and require security status with your lists, ensure that you are restricting the repositories that you are requesting to ensure that you receive list results quickly and reliably.
