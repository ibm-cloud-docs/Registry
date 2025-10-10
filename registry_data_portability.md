---

copyright:
  years: 2024, 2025
lastupdated: "2025-10-10"

keywords: data portability

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.registryshort_notm}}
{: #data_portability}

Data portability involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes the following actions:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and other code.
- The conversion of the exported data and configuration to the format that is required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for {{site.data.keyword.registrylong}}, see [Your responsibilities](/docs/Registry?topic=Registry-registry_responsibilities).

## Procedures for exporting data
{: #data-portability-procedures}

{{site.data.keyword.registryshort_notm}} provides the mechanisms to export the content that is uploaded, stored, and processed by the service.

1. Refer to the new provider's documentation to find out how to name your images.

1. Log in to the new registry.

1. [Log in to {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-containerregcli#bx_cr_login).

    ```sh
    ibmcloud cr login
    ```
    {: pre}

1. Run the following commands for each region in which container images are stored.

    a. Set the {{site.data.keyword.cloud_notm}} region, where `REGION` is the name of the [region](/docs/Registry?topic=Registry-registry_overview#registry_regions).

    ```sh
    ibmcloud cr region-set REGION
    ```

    b. Export your container images by running the `ibmcloud cr images` command, with `"{{ .Repository }}:{{ .Tag }}"` as the format, and pass the command output to `xargs -L 1 docker pull`.

    ```sh
    ibmcloud cr images --format "{{ .Repository }}:{{ .Tag }}" | xargs -L 1 docker pull
    ```
    {: pre}

    c. Tag each image with the name for the new registry, where `DOMAIN_NAME` is the domain name (for example, `us.icr.io`), `NAMESPACE` is the namespace, `NAME` is the name, and `NEW_IMAGE_NAME` is the new image name.

    ```sh
    docker tag DOMAIN_NAME/NAMESPACE/NAME NEW_IMAGE_NAME
    ```
    {: pre}

    d. Push each image to the new registry, where `NEW_IMAGE_NAME` is the new image name.

    ```sh
    docker push NEW_IMAGE_NAME
    ```
    {: pre}

## Exported data formats
{: #data-portability-data-formats}

Container images are exported from {{site.data.keyword.registryshort_notm}} as either Docker Manifest v2 images or OCI images, depending on what format was used to upload them. No conversion is required to move existing container images to another OCI-compliant registry.

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS).
