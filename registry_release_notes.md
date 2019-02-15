---


The following features and changes to the {{site.data.keyword.registrylong}} service are available.

## 21 February 2019
{: 21February2019}

- **New DNS names**
  {{site.data.keyword.registrylong_notm}} is adopting new domain names. The new domain names are available in the console and the CLI from `<DATE>`. You can use the new `icr.io` domain names now. The existing `registry.bluemix.net` domain names are deprecated, but you can continue to use them for the time being, an end of support date will be announced later. For more information, see [Regions](/docs/services/Registry/registry_overview.html#registry_regions).

  Images have separate signatures for old (`registry.bluemix.net`) and new (`icr.io`) domain names. Existing signatures work when the image is pulled from the old domain name. If you have an existing signature on your image, you must re-sign the image on the new domain name, `icr.io`. For more information about signing images, see [Signing images for trusted content](/docs/services/Registry/registry_trusted_content.html#registry_trustedcontent).

- **User access**
  The new `icr.io` domains are authorized by using an IAM API key, therefore, if you want more control over access to your {{site.data.keyword.registrylong_notm}} resources, you can add IAM policies. For example, you can change the API key policies in the cluster's pull secret so that images are pulled from a certain registry region or namespace only. For more information, see [Understanding how your cluster is authorized to pull images from {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).</staging>
  
