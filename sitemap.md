---

copyright:
  years: 2021, 2025
lastupdated: "2025-04-01"

keywords: container registry, site map, policy, storage, images, overview, registry

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Site map for {{site.data.keyword.registryshort_notm}}
{: #sitemap}



## Getting started
{: #sitemap_getting_started}


[Getting started](/docs/Registry?topic=Registry-getting-started#getting-started)

* [Before you begin](/docs/Registry?topic=Registry-getting-started#gs_registry_prereqs)

* [Install the {{site.data.keyword.registryshort_notm}} CLI](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install)

* [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add)

* [Pull images from a registry to your local computer](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pulling)

* [Tag the image](/docs/Registry?topic=Registry-getting-started#gs_registry_images_tag)

* [Push images to your namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pushing)

* [Verify that the image was pushed](/docs/Registry?topic=Registry-getting-started#gs_registry_images_verify)

* [Set up an audit trail for changes in {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-getting-started#gs_registry_audit)

* [Monitor metrics for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-getting-started#gs_registry_monitor)

* [Next steps in {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-getting-started#gs_get_start_next)


## About {{site.data.keyword.registryshort_notm}}
{: #sitemap_about_}


[About {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_overview#registry_overview)

* [Service plans](/docs/Registry?topic=Registry-registry_overview#registry_plans)

* [Quota limits and billing](/docs/Registry?topic=Registry-registry_overview#registry_plan_billing)

    * [Billing for storage and pull traffic](/docs/Registry?topic=Registry-registry_overview#registry_billing_traffic)

        * [Storage charges](/docs/Registry?topic=Registry-registry_overview#registry_billing_traffic_storage)

        * [Pull traffic charges](/docs/Registry?topic=Registry-registry_overview#registry_billing_traffic_pull_traffic)

    * [Quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_overview#registry_quota_limits)

        * [Storage quota limits](/docs/Registry?topic=Registry-registry_overview#registry_quota_limits_storage)

        * [Pull traffic quota limits](/docs/Registry?topic=Registry-registry_overview#registry_quota_limits_pull_traffic)

    * [Cost of {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_overview#registry_cost)

* [Upgrading your service plan](/docs/Registry?topic=Registry-registry_overview#registry_plan_upgrade)

* [Terms that are used in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_overview#overview_elements)

    * [Container image](/docs/Registry?topic=Registry-registry_overview#overview_elements_container_image)

    * [Digest](/docs/Registry?topic=Registry-registry_overview#overview_elements_digest)

    * [Dockerfile](/docs/Registry?topic=Registry-registry_overview#overview_elements_dockerfile)

    * [Docker V2 container images](/docs/Registry?topic=Registry-registry_overview#overview_elements_dockerv2_images)

    * [Domain name](/docs/Registry?topic=Registry-registry_overview#overview_elements_domain_name)

    * [Image manifest](/docs/Registry?topic=Registry-registry_overview#overview_elements_manifest)

    * [OCI container images](/docs/Registry?topic=Registry-registry_overview#overview_elements_oci_images)

    * [Registry](/docs/Registry?topic=Registry-registry_overview#overview_elements_registry)

    * [Registry namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace)

    * [Repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository)

    * [Tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag)

    * [Untagged image](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged)

* [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions)

    * [Global registry](/docs/Registry?topic=Registry-registry_overview#registry_regions_global)

        * [Targeting the global registry](/docs/Registry?topic=Registry-registry_overview#registry_regions_global_target)

    * [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local)

        * [Targeting a local region](/docs/Registry?topic=Registry-registry_overview#registry_regions_local_target)

* [Supported clients](/docs/Registry?topic=Registry-registry_overview#support_clients)

    * [Support for Docker](/docs/Registry?topic=Registry-registry_overview#docker)

    * [Support for other clients](/docs/Registry?topic=Registry-registry_overview#clients)


## Architecture and workload
{: #sitemap_architecture_and_workload}


[Architecture and workload](/docs/Registry?topic=Registry-registry_architecture#registry_architecture)

* [Segmentation of data](/docs/Registry?topic=Registry-registry_architecture#registry_architecture_segment)

* [Private connections](/docs/Registry?topic=Registry-registry_architecture#registry_architecture_private_connections)


## Public IBM images
{: #sitemap_public_ibm_images}


[Public IBM images](/docs/Registry?topic=Registry-public_images#public_images)

* [Accessing the public IBM images by using the CLI](/docs/Registry?topic=Registry-public_images#public_images_cli)


## What are containers?
{: #sitemap_what-are-containers}

[What are containers?](https://www.ibm.com/think/topics/containers){: external}


## Notifications
{: #sitemap_notifications}


[Notifications](/docs/Registry?topic=Registry-registry_notices#registry_notices)

* [Notifications topics](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics)

    * [2024](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2024)

    * [2023](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2023)

    * [2022](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2022)

    * [2021](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2021)

    * [2020](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2020)

    * [2019](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2019)

    * [2018](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2018)

    * [2017](/docs/Registry?topic=Registry-registry_notices#registry_notices_topics_2017)

[Firewall changes from 4 September 2024 for users that pull images from global](/docs/Registry?topic=Registry-registry_notices_firewall#registry_notices_firewall)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_firewall#registry_notices_firewall_know)

* [What actions you must take by 4 September 2024](/docs/Registry?topic=Registry-registry_notices_firewall#registry_notices_firewall_actions)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_firewall#registry_notices_firewall_announce)

[Vulnerability Advisor version 3 is being discontinued on 13 November 2023](/docs/Registry?topic=Registry-registry_notices_va_v3#registry_notices_va_v3)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_va_v3#notices_va_v3_change)

* [What actions you must take by 13 November 2023](/docs/Registry?topic=Registry-registry_notices_va_v3#notices_va_v3_action)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_va_v3#registry_notices_va_v3_announce)

[Upcoming public networking changes from 15 June 2023](/docs/Registry?topic=Registry-registry_notices_wildcard_domains#registry_notices_wildcard_domains)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_wildcard_domains#registry_notices_wildcard_domains_announce)

[Update Vulnerability Advisor to version 4 by 19 June 2023](/docs/Registry?topic=Registry-registry_notices_va_v4#registry_notices_va_v4)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_va_v4#notices_va_v4_change)

* [What actions you must take by 19 June 2023](/docs/Registry?topic=Registry-registry_notices_va_v4#notices_va_v4_action)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_va_v4#registry_notices_va_v4_announce)

[Changes to VPE gateways from 11 November 2022](/docs/Registry?topic=Registry-registry_notices_vpe#registry_notices_vpe)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_vpe#registry_notices_vpe_know)

* [How you benefit from this change](/docs/Registry?topic=Registry-registry_notices_vpe#registry_notices_vpe_benefit)

* [Understanding if you are impacted by this change](/docs/Registry?topic=Registry-registry_notices_vpe#registry_notices_vpe_impact)

* [What actions you must take](/docs/Registry?topic=Registry-registry_notices_vpe#registry_notices_vpe_actions)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_vpe#registry_notices_vpe_announce)

[Changes to private IP addresses from 15 December 2022](/docs/Registry?topic=Registry-registry_notices_ip_address#registry_notices_ip_address)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_ip_address#registry_notices_ip_address_know)

* [What actions you need to take](/docs/Registry?topic=Registry-registry_notices_ip_address#registry_notices_ip_address_actions)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_ip_address#registry_notices_ip_address_announce)

[Container Registry CLI stops returning security status results in lists from version 1.0.0](/docs/Registry?topic=Registry-registry_notices_lists#registry_notices_lists)

* [What actions you need to take](/docs/Registry?topic=Registry-registry_notices_lists#registry_notices_lists_action)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_lists#registry_notices_lists_announce)

[Private IP addresses changed on 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_private_network#registry_notices_iam_private_network)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_iam_private_network#registry_notices_iam_private_network_know)

* [How you benefit from this change](/docs/Registry?topic=Registry-registry_notices_iam_private_network#registry_notices_iam_pivate_network_benefit)

* [Understanding if you are impacted by this change](/docs/Registry?topic=Registry-registry_notices_iam_private_network#registry_notices_iam_pivate_network_impact)

* [What actions you need to take](/docs/Registry?topic=Registry-registry_notices_iam_private_network#registry_notices_iam_pivate_network_action)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_iam_private_network#registry_notices_iam_pivate_network_announce)

[IAM access policies are required from 5 July 2022](/docs/Registry?topic=Registry-registry_notices_iam_policy#registry_notices_iam_policy)

* [What are the changes?](/docs/Registry?topic=Registry-registry_notices_iam_policy#notices_iam_policy_change)

* [Check whether these changes affect you](/docs/Registry?topic=Registry-registry_notices_iam_policy#notices_iam_policy_affect)

* [Prepare for the changes](/docs/Registry?topic=Registry-registry_notices_iam_policy#notices_iam_policy_prepare)

* [What if I did not implement the changes in time?](/docs/Registry?topic=Registry-registry_notices_iam_policy#notices_iam_policy_unprepared)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_iam_policy#registry_notices_iam_policy_announce)

[Minimum supported Docker version from 1 March 2022](/docs/Registry?topic=Registry-registry_notices_docker#registry_notices_docker)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_docker#registry_notices_docker_announce)

[Ending exemption synchronization across regions on 31 January 2022](/docs/Registry?topic=Registry-registry_notices_exemptions#registry_notices_exemptions)

* [What are exemptions?](/docs/Registry?topic=Registry-registry_notices_exemptions#registry_notices_exemptions_desc)

* [What is the current behavior?](/docs/Registry?topic=Registry-registry_notices_exemptions#registry_notices_exemptions_behavior)

* [Which regions currently replicate exemptions?](/docs/Registry?topic=Registry-registry_notices_exemptions#registry_notices_exemptions_replicate)

* [Do I have any exemptions?](/docs/Registry?topic=Registry-registry_notices_exemptions#registry_notices_exemptions_own)

* [How does this change affect me?](/docs/Registry?topic=Registry-registry_notices_exemptions#registry_notices_exemptions_affect)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_exemptions#registry_notices_exemptions_announce)

[Billing for storage used by untagged images from 1 February 2022](/docs/Registry?topic=Registry-registry_notices_billing#registry_notices_billing)

* [What are untagged images?](/docs/Registry?topic=Registry-registry_notices_billing#registry_notices_billing_untagged_image)

* [Do I have any untagged images?](/docs/Registry?topic=Registry-registry_notices_billing#registry_notices_billing_untagged_image_own)

* [Do I need untagged images?](/docs/Registry?topic=Registry-registry_notices_billing#registry_notices_billing_untagged_image_need)

* [How does this change affect me?](/docs/Registry?topic=Registry-registry_notices_billing#registry_notices_billing_affect)

* [How can I remove untagged images?](/docs/Registry?topic=Registry-registry_notices_billing#registry_notices_billing_untagged_image_remove)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_billing#registry_notices_billing_announce)

[Support for the container build service ends on 5 October 2021](/docs/Registry?topic=Registry-registry_notices_cont_builds_eos#registry_notices_cont_builds_eos)

* [What you need to know](/docs/Registry?topic=Registry-registry_notices_cont_builds_eos#registry_notices_cont_builds_eos_what)

* [What actions you need to take](/docs/Registry?topic=Registry-registry_notices_cont_builds_eos#registry_notices_cont_builds_eos_action)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_cont_builds_eos#registry_notices_cont_builds_eos_announce)

[Changes to public IP addresses from 13 September 2021](/docs/Registry?topic=Registry-registry_notices_public_ip_address#registry_notices_public_ip_address)

* [What you need to know:](/docs/Registry?topic=Registry-registry_notices_public_ip_address#registry_notices_public_ip_address_know)

* [What actions you need to take](/docs/Registry?topic=Registry-registry_notices_public_ip_address#registry_notices_public_ip_address_action)

* [When the changes take effect](/docs/Registry?topic=Registry-registry_notices_public_ip_address#registry_notices_public_ip_address_change)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_public_ip_address#registry_notices_public_ip_address_announce)

[Using Notary v1 for signing images is deprecated from 8 July 2021](/docs/Registry?topic=Registry-registry_notices_notaryv1#registry_notices_notaryv1)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_notaryv1#registry_notices_notaryv1_announce)

[Registry tokens discontinued for authentication on 19 August 2021](/docs/Registry?topic=Registry-registry_notices_token_auth#registry_notices_token_auth)

* [What actions you must take by 19 August 2021](/docs/Registry?topic=Registry-registry_notices_token_auth#registry_notices_token_auth_action)

* [Learn more](/docs/Registry?topic=Registry-registry_notices_token_auth#registry_notices_token_auth_learn)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_token_auth#registry_notices_token_auth_announce)

[Deprecation of container builds - act by 6 September 2021](/docs/Registry?topic=Registry-registry_notices_container_builds#registry_notices_container_builds)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_container_builds#registry_notices_container_builds_know)

* [What actions you must take by 6 September 2021](/docs/Registry?topic=Registry-registry_notices_container_builds#registry_notices_container_builds_action)

* [Learn more](/docs/Registry?topic=Registry-registry_notices_container_builds#registry_notices_container_builds_learn)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_container_builds#registry_notices_container_builds_announce)

[End of support for UAA tokens from 12 August 2020](/docs/Registry?topic=Registry-registry_notices_uaa_token#registry_notices_uaa_token)

* [Next steps to use IAM for authentication](/docs/Registry?topic=Registry-registry_notices_uaa_token#registry_notices_uaa_token_next)

* [Summary](/docs/Registry?topic=Registry-registry_notices_uaa_token#registry_notices_uaa_token_summary)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_uaa_token#registry_notices_uaa_token_announce)

[Introducing retention policies from 23 September 2019](/docs/Registry?topic=Registry-registry_notices_retention#registry_notices_retention)

* [Setting retention policies in the CLI](/docs/Registry?topic=Registry-registry_notices_retention#registry_notices_retention_cli)

* [Learn more](/docs/Registry?topic=Registry-registry_notices_retention#registry_notices_retention_learn)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_retention#registry_notices_retention_announce)

[Registry token creation is discontinued from 1 July 2019](/docs/Registry?topic=Registry-registry_notices_token#registry_notices_token)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_token#registry_notices_token_affect)

* [How you benefit from this change](/docs/Registry?topic=Registry-registry_notices_token#registry_notices_token_benefit)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_token#registry_notices_token_announce)

[Introducing new domain names from 25 February 2019](/docs/Registry?topic=Registry-registry_notices_domain_names#registry_notices_domain_names)

* [What you need to know about this change](/docs/Registry?topic=Registry-registry_notices_domain_names#registry_notices_domain_names_know)

* [How you benefit from this change](/docs/Registry?topic=Registry-registry_notices_domain_names#registry_notices_domain_names_benefit)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_domain_names#registry_notices_domain_names_announce)

[Vulnerability Advisor version 2 API is being discontinued on 8 January 2019](/docs/Registry?topic=Registry-registry_notices_va_v2_dep#registry_notices_va_v2_dep)

* [What is changing?](/docs/Registry?topic=Registry-registry_notices_va_v2_dep#registry_notices_va_v2_dep_change)

* [End of support Date: 8 January 2019](/docs/Registry?topic=Registry-registry_notices_va_v2_dep#registry_notices_va_v2_dep_eos)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_va_v2_dep#registry_notices_va_v2_dep_announce)

[Support for IAM access policies](/docs/Registry?topic=Registry-registry_notices_iam_support#registry_notices_iam_support)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_iam_support#registry_notices_iam_support_announce)

[IBM Cloud Container Registry is available](/docs/Registry?topic=Registry-registry_notices_ibcr#registry_notices_ibcr)

* [Original announcement](/docs/Registry?topic=Registry-registry_notices_ibcr#registry_notices_ibcr_announce)


## Release notes
{: #sitemap_release_notes}


[Release notes](/docs/Registry?topic=Registry-registry_release_notes#registry_release_notes)

* [14 February 2025](/docs/Registry?topic=Registry-registry_release_notes#registry-14feb2025)

    * [Access {{site.data.keyword.registrylong_notm}} by using trusted profiles](/docs/Registry?topic=Registry-registry_release_notes#14feb2025_trustprof)

* [9 December 2024](/docs/Registry?topic=Registry-registry_release_notes#registry-09dec2024)

    * [Content delivery network (CDN) is enabled for users that pull {{site.data.keyword.registrylong_notm}} images from global (`icr.io`) over a public network](/docs/Registry?topic=Registry-registry_release_notes#09dec2024_cdn)

* [26 June 2024](/docs/Registry?topic=Registry-registry_release_notes#registry-26jun2024)

    * [Firewall changes from 4 September 2024 for users that pull {{site.data.keyword.registrylong_notm}} images from global (`icr.io`)](/docs/Registry?topic=Registry-registry_release_notes#26jun2024_firewall)

* [15 March 2024](/docs/Registry?topic=Registry-registry_release_notes#registry-15mar2024)

    * [New region in Madrid](/docs/Registry?topic=Registry-registry_release_notes#15mar2024_madrid)

* [13 November 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-13nov2023)

    * [Discontinuation of Vulnerability Advisor version 3](/docs/Registry?topic=Registry-registry_release_notes#13nov2023_va3)

* [11 October 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-11oct2023)

    * [Vulnerability Advisor version 3 is discontinued from 13 November 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-11oct2023_v3)

* [24 July 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-24jul2023)

    * [Added the option to output several {{site.data.keyword.registrylong_notm}} commands in JSON format](/docs/Registry?topic=Registry-registry_release_notes#registry-24jul2023_json_option)

    * [The `--json` option for {{site.data.keyword.registrylong_notm}} commands is deprecated](/docs/Registry?topic=Registry-registry_release_notes#registry-24jul2023_json)

* [19 June 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-19jun2023)

    * [Vulnerability Advisor version 3 is deprecated from 19 June 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-19jun2023_v3)

* [19 May 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-19may2023)

    * [Update Vulnerability Advisor to version 4 by 19 June 2023](/docs/Registry?topic=Registry-registry_release_notes#19may2023_va_v4)

* [26 April 2023](/docs/Registry?topic=Registry-registry_release_notes#registry-26apr2023)

    * [Using Portieris to block the deployment of images with issues is deprecated.](/docs/Registry?topic=Registry-registry_release_notes#26apr2023_portieris)

* [11 November 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-11nov2022)

    * [Change to virtual private endpoints](/docs/Registry?topic=Registry-registry_release_notes#11nov2022_vpe)

* [2 November 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-2nov2022)

    * [Changes to private IP addresses from 15 December 2022](/docs/Registry?topic=Registry-registry_release_notes#2nov2022_ip)

* [15 September 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-15sep2022)

    * [{{site.data.keyword.registryshort}} plug-in 1.0.0 is available](/docs/Registry?topic=Registry-registry_release_notes#15sep2022_v1)

    * [All releases of {{site.data.keyword.registryshort}} plug-in 0.1 are deprecated](/docs/Registry?topic=Registry-registry_release_notes#15sep2022_v0)

    * [Vulnerability Advisor 4 is available from {{site.data.keyword.registryshort}} plug-in 1.0.0](/docs/Registry?topic=Registry-registry_release_notes#15sep2022_va_version_4)

    * [New commands for setting and checking the Vulnerability Advisor version are available from {{site.data.keyword.registryshort}} plug-in 1.0.0](/docs/Registry?topic=Registry-registry_release_notes#15sep2022_va_version_commands)

* [3 August 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-03aug2022)

    * [The CLI stops returning security status results in lists by default from version 1.0.0](/docs/Registry?topic=Registry-registry_release_notes#03aug2022_list)

* [8 July 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-08jul2022)

    * [Context-based restrictions](/docs/Registry?topic=Registry-registry_release_notes#08jul2022_cbr)

* [5 July 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-05jul2022)

    * [Change to {{site.data.keyword.registryshort}} private IP addresses in all regions](/docs/Registry?topic=Registry-registry_release_notes#05jul2022_private_network)

    * [All accounts require IAM access policies](/docs/Registry?topic=Registry-registry_release_notes#05jul2022_iam)

* [23 June 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-23jun2022)

    * [Change to {{site.data.keyword.registryshort}} private IP addresses in the following regions only: `br-sao`, `ca-tor`](/docs/Registry?topic=Registry-registry_release_notes#23jun2022_private_network)

* [20 April 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-20apr2022)

    * [{{site.data.keyword.registryshort}} private IP addresses are changing from 23 June 2022](/docs/Registry?topic=Registry-registry_release_notes#20apr2022_private_network)

* [1 March 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-01mar2022)

    * [Amendment to the minimum supported Docker version for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#01mar2022_docker)

* [9 February 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-09feb2022)

    * [All accounts will require IAM access policies from 5 July 2022](/docs/Registry?topic=Registry-registry_release_notes#09feb2022_iam)

* [2 February 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-02feb2022)

    * [Replication of exemption policies between {{site.data.keyword.IBM_notm}} regions is discontinued](/docs/Registry?topic=Registry-registry_release_notes#02feb2022_exemption)

* [1 February 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-01feb2022)

    * [Storage that is used by untagged images is being charged for](/docs/Registry?topic=Registry-registry_release_notes#01feb2022_billing)

* [17 January 2022](/docs/Registry?topic=Registry-registry_release_notes#registry-17jan2022)

    * [View the activity tracker auditing events for {{site.data.keyword.redhat_notm}} signing](/docs/Registry?topic=Registry-registry_release_notes#17jan2022_sig)

* [7 December 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-07dec2021)

    * [Define configuration rules for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#07dec2021_gov)

* [1 November 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-01nov2021)

    * [Using Notary v1 for signing images is discontinued](/docs/Registry?topic=Registry-registry_release_notes#01nov2021_notary)

* [5 October 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-05oct2021)

    * [{{site.data.keyword.registryshort}} container builds are discontinued](/docs/Registry?topic=Registry-registry_release_notes#05oct2021_build)

* [2 September 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-02sep2021)

    * [Namespaces that are assigned to a resource group show in the Resource list page](/docs/Registry?topic=Registry-registry_release_notes#02sep2021_resource_list)

* [30 August 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-30aug2021)

    * [New region in Brazil](/docs/Registry?topic=Registry-registry_release_notes#30aug2021_brazil)

* [19 August 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-19aug2021)

    * [Using registry tokens is discontinued](/docs/Registry?topic=Registry-registry_release_notes#19aug2021_remove_tokens)

* [9 August 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-09aug2021)

    * [The `ibmcloud cr login` command logs you into the `<region>.icr.io` registry domain only](/docs/Registry?topic=Registry-registry_release_notes#09aug2021_bmx)

* [8 July 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-08jul2021)

    * [Using Notary v1 for signing images is deprecated](/docs/Registry?topic=Registry-registry_release_notes#08jul2021_notary)

* [21 June 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-21jun2021)

    * [Global registry](/docs/Registry?topic=Registry-registry_release_notes#21jun2021_global)

* [10 May 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-10may2021)

    * [New region in Canada](/docs/Registry?topic=Registry-registry_release_notes#10may2021_canada)

* [4 May 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-04may2021)

    * [The `ibmcloud cr ppa-archive-load` command is discontinued](/docs/Registry?topic=Registry-registry_release_notes#04may2021_ppa)

* [18 February 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-18feb2021)

    * [Increase the performance of the `ibmcloud cr image-list` and `ibmcloud cr image-digests` commands by using the `--no-va` option](/docs/Registry?topic=Registry-registry_release_notes#18feb2021_no-va)

* [15 February 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-15feb2021)

    * [New region in Japan](/docs/Registry?topic=Registry-registry_release_notes#15feb2021_japan)

* [19 November 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-19nov2020)

    * [You can use Portieris to enforce container image security](/docs/Registry?topic=Registry-registry_release_notes#19nov2020_portieris)

* [21 October 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-21oct2020)

    * [Find out about the usage on your account by using platform metrics](/docs/Registry?topic=Registry-registry_release_notes#21oct2020_metrics)

* [6 October 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-06oct2020)

    * [{{site.data.keyword.registryshort}} container builds are deprecated](/docs/Registry?topic=Registry-registry_release_notes#06oct2020_build)

* [27 August 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-27aug2020)

    * [Setting exemption policies by digest](/docs/Registry?topic=Registry-registry_release_notes#27aug2020_digest)

* [12 August 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-12aug2020)

    * [Using UAA tokens is discontinued](/docs/Registry?topic=Registry-registry_release_notes#12aug2020_tokens)

* [30 July 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-30jul2020)

    * [New access roles are required for Vulnerability Advisor exemption policies](/docs/Registry?topic=Registry-registry_release_notes#30jul2020_exemption)

* [29 July 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-29jul2020)

    * [You can set permissions so that access to resources within a namespace can be configured at the resource group level](/docs/Registry?topic=Registry-registry_release_notes#29jul2020_resource_group)

* [13 July 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-13jul2020)

    * [To work with namespaces, you must have the Manager role at the account level](/docs/Registry?topic=Registry-registry_release_notes#13jul2020_manager)

* [24 June 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-24jun2020)

    * [Restoring all tags for a digest in a repository is now an option](/docs/Registry?topic=Registry-registry_release_notes#24jun2020_tags)

* [18 May 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-18may2020)

    * [Retaining untagged images is now an option when you clean up your namespaces](/docs/Registry?topic=Registry-registry_release_notes#18may2020_untagged)

* [30 April 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-30apr2020)

    * [`ibmcloud cr image-prune-untagged` command is available](/docs/Registry?topic=Registry-registry_release_notes#30apr2020_prune)

* [16 April 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-16apr2020)

    * [You can use private network connections to securely route your data in {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#16apr2020_private_network)

    * [`ibmcloud cr private-only` command is available](/docs/Registry?topic=Registry-registry_release_notes#16apr2020_private)

* [3 February 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-3feb2020)

    * [Using {{site.data.keyword.registryshort}} tokens is deprecated](/docs/Registry?topic=Registry-registry_release_notes#3feb2020_tokens)

* [31 January 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-31jan2020)

    * [`ibmcloud cr image-digests` command is available](/docs/Registry?topic=Registry-registry_release_notes#31jan2020_digests)

* [4 December 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-4dec2019)

    * [Support for {{site.data.keyword.redhat_notm}} signatures is available](/docs/Registry?topic=Registry-registry_release_notes#4dec2019_signatures)

* [25 October 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-25oct2019)

    * [{{site.data.keyword.logs_full_notm}} platform services logs are available](/docs/Registry?topic=Registry-registry_release_notes#25oct2019_logs)

* [14 October 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-14oct2019)

    * [`ibmcloud cr manifest-inspect` command is available](/docs/Registry?topic=Registry-registry_release_notes#14oct2019_manifest)

* [23 September 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-23sep2019)

    * [You can create retention policies for your images](/docs/Registry?topic=Registry-registry_release_notes#23sep2019_retention_policy)

    * [You can restore deleted images from the trash](/docs/Registry?topic=Registry-registry_release_notes#23sep2019_restore_trash)

* [1 August 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-01aug2019)

    * [`ibmcloud cr retention-run` command is available](/docs/Registry?topic=Registry-registry_release_notes#01aug2019_retention)

* [25 July 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-25jul2019)

    * [{{site.data.keyword.atracker_full_notm}} available for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#25jul2019_at)

* [1 July 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-1jul2019)

    * [`ibmcloud cr token-add` command is no longer available](/docs/Registry?topic=Registry-registry_release_notes#1jul2019_token_add)

* [27 June 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-27jun2019)

    * [Container Scanner is no longer available](/docs/Registry?topic=Registry-registry_release_notes#27jun2019_cs)

* [13 June 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-13jun2019)

    * [Remove tags from images](/docs/Registry?topic=Registry-registry_release_notes#13jun2019_tags)

* [13 May 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-13may2019)

    * [End of support for Container Scanner](/docs/Registry?topic=Registry-registry_release_notes#13may2019_cs)

* [2 April 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-2apr2019)

    * [General Availability of Container Image Security Enforcement](/docs/Registry?topic=Registry-registry_release_notes#2apr2019_cise)

* [14 March 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-14mar2019)

    * [{{site.data.keyword.atracker_full_notm}} is available for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_release_notes#14mar2019_at)

* [25 February 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-25feb2019)

    * [New domain names](/docs/Registry?topic=Registry-registry_release_notes#25feb2019_dns)

    * [Adding IAM API key policies to control access to resources](/docs/Registry?topic=Registry-registry_release_notes#25feb2019_secrets)

    * [New region in `jp-tok`](/docs/Registry?topic=Registry-registry_release_notes#25feb2019_ap-north)

* [21 February 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-21feb2019)

    * [Automating access to your namespaces](/docs/Registry?topic=Registry-registry_release_notes#21feb2019_access)

* [8 January 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-8jan2019)

    * [End of support for Vulnerability Advisor API version 2](/docs/Registry?topic=Registry-registry_release_notes#8jan2019_va2)

* [4 October 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-4oct2018)

    * [Managing user access](/docs/Registry?topic=Registry-registry_release_notes#4oct2018_access)

* [7 August 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-7aug2018)

    * [Exemption policies available in Vulnerability Advisor](/docs/Registry?topic=Registry-registry_release_notes#7aug2018_exemption)

* [25 July 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-25jul2018)

    * [{{site.data.keyword.atracker_full_notm}} is available for Vulnerability Advisor](/docs/Registry?topic=Registry-registry_release_notes#25jul2018_at)

* [12 July 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-12jul2018)

    * [Vulnerability Advisor API version 3](/docs/Registry?topic=Registry-registry_release_notes#12jul2018_va3)

* [31 May 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-31may2018)

    * [Use Helm for Passport Advantage images](/docs/Registry?topic=Registry-registry_release_notes#31may2018_helm)

* [21 March 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-21mar2018)

    * [Container Scanner](/docs/Registry?topic=Registry-registry_release_notes#21mar2018_cs)

* [16 March 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-16mar2018)

    * [Container Image Security Enforcement beta](/docs/Registry?topic=Registry-registry_release_notes#16mar2018_cise)

* [20 February 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-20feb2018)

    * [Trusted content](/docs/Registry?topic=Registry-registry_release_notes#20feb2018_tc)

* [6 November 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-6nov2017)

    * [Global registry](/docs/Registry?topic=Registry-registry_release_notes#6nov2017_global)

* [29 September 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-29sep2017)

    * [Build Docker images](/docs/Registry?topic=Registry-registry_release_notes#29sep2017_docker)

* [24 August 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-24aug2017)

    * [Graphical user interface released](/docs/Registry?topic=Registry-registry_release_notes#24aug2017_gui)

* [27 June 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-27jun2017)

    * [Introducing {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_release_notes#27jun2017_ga)


## Container Registry and Vulnerability Advisor workflow tutorial
{: #sitemap_container_registry_and_vulnerability_advisor_workflow_tutorial}


[Container Registry and Vulnerability Advisor workflow tutorial](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow)

* [Objectives](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_objectives)

* [Services used](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_services)

* [Before you begin](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_prereqs)

* [From code to a running container](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_code_run)

    * [Create a namespace](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_create_namespace)

    * [Build and push an image](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_build_push_image)

    * [Deploy a container that uses your image](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_deploy)

* [Secure your images and clusters](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_secure)

    * [View the vulnerability report for your image](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_vulnerability_report)

    * [Enforce security in your cluster](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_enforce_security)

    * [Resolve vulnerabilities in your image](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_resolve_vulnerabilities)

* [Deploying to nondefault Kubernetes namespaces](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_deploy_nondefault_namespaces)


## Granting access to Container Registry resources tutorial
{: #sitemap_granting_access_to_container_registry_resources_tutorial}


[Granting access to Container Registry resources tutorial](/docs/Registry?topic=Registry-iam_access#iam_access)

* [Before you begin](/docs/Registry?topic=Registry-iam_access#iam_access_prereq)

* [Authorize a user to configure the registry](/docs/Registry?topic=Registry-iam_access#configure_registry)

* [Authorize a user to access specific namespaces](/docs/Registry?topic=Registry-iam_access#access_resources)

* [Create a service ID and grant access to a resource](/docs/Registry?topic=Registry-iam_access#service_id)

* [Cleaning up your account](/docs/Registry?topic=Registry-iam_access#clean_up)


## Solution tutorials
{: #sitemap_solution_tutorials}


[Moving a VM based app to Kubernetes](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes)

* [Objectives](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-objectives)

* [Architecture](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-architecture)

    * [Traditional app architecture with VMs](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-2)

    * [Containerized architecture](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-3)

    * [VMs, containers, and Kubernetes](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-4)

        * [Virtual machines vs containers](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-5)

        * [Kubernetes orchestration](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-6)

    * [What IBM is doing for you](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-7)

* [Sizing clusters](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-sizing_clusters)

* [Decide what Database option to use](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-database_options)

* [Decide where to store application files](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-decide_where_to_store_data)

    * [Non-persistent data storage](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-11)

    * [Learn how to create persistent data storage for your app](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-12)

    * [Learn how to move existing data to persistent storage](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-13)

    * [Set up backups for persistent storage](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-14)

* [Prepare your code](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-prepare_code)

    * [Apply the 12-factor principles](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-16)

    * [Store credentials in Kubernetes secrets](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-17)

* [Containerize your app](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-build_docker_images)

* [Deploy your app to a Kubernetes cluster](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-deploy_to_kubernetes)

    * [Learn how to create a Kubernetes deployment yaml file](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-20)

* [Summary](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-summary)

* [Put everything learned to practice, run the JPetStore app in your cluster](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-runthejpetstore)

* [Related Content](/docs/Registry?topic=Registry-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-related)

[Resilient and secure multi-region Kubernetes clusters with {{site.data.keyword.cis_full_notm}}](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis)

* [Objectives](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-objectives)

* [Before you begin](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-prereqs)

* [Deploy an application to one location](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-2)

    * [Create a Kubernetes cluster](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-3)

    * [Deploy the application to the Kubernetes cluster](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-deploy_application)

    * [Get the Ingress Subdomain assigned to the cluster](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-CSALB_IP_subdomain)

    * [Configure the Ingress for your DNS subdomain](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-ingress)

* [And then to another location](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-0)

* [Configure multi-location load-balancing](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-4)

    * [Register a custom domain with {{site.data.keyword.cis_full_notm}}](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-create_cis_instance)

    * [Configure Health Check for the Global Load Balancer](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-12)

    * [Define Origin Pools](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-13)

        * [One pool for the cluster in Dallas](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-14)

        * [One pool for the cluster in London](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-15)

    * [Create the Global Load Balancer](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-17)

* [Secure the application](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-secure_via_CIS)

    * [Turn the Web Application Firewall On](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-20)

    * [Increase performance and protect from Denial of Service attacks](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-proxy_setting)

* [Remove resources](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-6)

    * [Remove Kubernetes Cluster resources](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-23)

    * [Remove {{site.data.keyword.cis_short_notm}} resources](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-24)

* [Related content](/docs/Registry?topic=Registry-multi-region-k8s-cis#multi-region-k8s-cis-7)


## Setting up the CLI and namespace
{: #sitemap_setting_up_the_cli_and_namespace}


[Setting up the CLI and namespace](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace)

* [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)

* [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update)

    * [Updating `container-registry` CLI plug-in version 1.0](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update_v1)

    * [Updating `container-registry` CLI plug-in version 0.1](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update_v0)

* [Uninstalling the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_uninstall)

* [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan)

    * [User permissions for working with namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan_perm)

* [Setting up a namespace](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_setup)

* [Assigning existing namespaces to resource groups](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_assign)

* [Removing namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_remove)


## Setting up {{site.data.keyword.registryshort}} as a private registry on {{site.data.keyword.redhat_openshift_notm}}
{: #sitemap_setting_up_as_a_private_registry_on_}


[Setting up {{site.data.keyword.registryshort}} as a private registry on {{site.data.keyword.redhat_openshift_notm}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos)

* [Set up {{site.data.keyword.openshiftlong_notm}} to use {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_rhoks)

* [Set up {{site.data.keyword.redhat_openshift_notm}} Container Platform to use {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_os)

    * [Set up the {{site.data.keyword.redhat_openshift_notm}} Container Platform internal registry to pull from {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_os_pull)

    * [Set up the {{site.data.keyword.redhat_openshift_notm}} Container Platform build to push images to {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_os_push)


## Adding images to your namespace
{: #sitemap_adding_images_to_your_namespace}


[Adding images to your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_)

* [Pulling images from another registry](/docs/Registry?topic=Registry-registry_images_#registry_images_pulling_reg)

* [Pushing Docker images to your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_pushing_namespace)

* [Copying images between registries](/docs/Registry?topic=Registry-registry_images_#registry_images_copying)

* [Creating images that refer to a source image](/docs/Registry?topic=Registry-registry_images_#registry_images_source)

* [Building Docker images to use them with your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_creating)

* [Pushing images by using an API key](/docs/Registry?topic=Registry-registry_images_#registry_api_key_push_image)

* [Removing tags from images in your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_untag)

* [Deleting images from your private repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove)

    * [Deleting images from your private repository in the CLI](/docs/Registry?topic=Registry-registry_images_#registry_images_remove_cli)

    * [Deleting images from your private repository in the console](/docs/Registry?topic=Registry-registry_images_#registry_images_remove_gui)

* [Listing images in the trash](/docs/Registry?topic=Registry-registry_images_#registry_images_list_trash)

* [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore)

    * [Restoring images by digest](/docs/Registry?topic=Registry-registry_images_#registry_images_restore_digest)

    * [Restoring images by tag](/docs/Registry?topic=Registry-registry_images_#registry_images_restore_tag)

* [Deleting a private repository and any associated images](/docs/Registry?topic=Registry-registry_images_#registry_repo_remove)


## Using Helm charts
{: #sitemap_using_helm_charts}


[Using Helm charts](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts)

* [OCI support for Helm charts](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_oci)

* [Adding Helm charts to your namespace](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_add)

    * [Pulling charts from another registry or Helm repository](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_pull)

    * [Pushing Helm charts to your namespace](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_push)

    * [Copying charts between registries](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_copy)

    * [Installing a Helm chart to the cluster](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_install)

* [Deleting charts from your private repository](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_remove)

    * [Deleting charts from your private repository in the CLI](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_remove_cli)

    * [Deleting charts from your private repository in the console](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_remove_gui)

* [Listing charts in the trash](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_list_trash)

* [Restoring charts](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_restore)

    * [Restoring charts by digest](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_restore_digest)

    * [Restoring charts by tag](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_restore_tag)

* [Deleting a private repository and any associated charts](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_repo_remove)


## Cleaning up your namespaces
{: #sitemap_cleaning_up_your_namespaces}


[Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention#registry_retention)

* [Planning retention](/docs/Registry?topic=Registry-registry_retention#retention_plan)

* [Clean up your namespaces to keep a set number of images](/docs/Registry?topic=Registry-registry_retention#retention_images)

* [Set a retention policy for your namespaces](/docs/Registry?topic=Registry-registry_retention#retention_policy_set)

* [Update a retention policy to keep all your images](/docs/Registry?topic=Registry-registry_retention#retention_policy_keep)

* [Clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged)


## Managing quota limits for storage and pull traffic
{: #sitemap_managing_quota_limits_for_storage_and_pull_traffic}


[Managing quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_quota#registry_quota)

* [Setting quota limits for storing and pulling images](/docs/Registry?topic=Registry-registry_quota#registry_quota_set)

* [Reviewing quota limits and usage](/docs/Registry?topic=Registry-registry_quota#registry_quota_get)

* [Staying within quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup)


## Managing user access
{: #sitemap_managing_user_access}


[Accessing Container Registry](/docs/Registry?topic=Registry-registry_access#registry_access)

* [Accessing your namespaces in automation](/docs/Registry?topic=Registry-registry_access#registry_access_automating)

    * [Creating a service ID API key manually](/docs/Registry?topic=Registry-registry_access#registry_access_serviceid_apikey_create)

    * [Creating a user API key manually](/docs/Registry?topic=Registry-registry_access#registry_access_user_apikey_create)

    * [Using client software to authenticate in automation](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth)

        * [Using Buildah to authenticate with the registry](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth_example_other_buildah)

        * [Using Docker to authenticate with the registry](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth_docker)

        * [Using Podman to authenticate with the registry](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth_example_other_podman)

        * [Using Skopeo to authenticate with the registry](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth_other_example_skopeo)

* [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive)

    * [Using Buildah to access your namespace](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_buildah)

    * [Using Docker to access your namespace](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_docker)

    * [Using Podman to access your namespace](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_podman)

    * [Using Skopeo to access your namespace](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_skopeo)

* [Accessing your namespaces programmatically](/docs/Registry?topic=Registry-registry_access#registry_access_programmatic)

[Accessing Container Registry by using trusted profiles](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles)

* [Accessing namespaces in automation by using a trusted profile](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_auto)

    * [Creating a trusted profile](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_create)

    * [Creating a service ID API key manually](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_serviceid_apikey_create)

    * [Using client software to authenticate in automation](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_apikey_auth)

        * [Using Buildah to authenticate with the registry](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_apikey_auth_buildah)

        * [Using Docker to authenticate with the registry](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_apikey_auth_docker)

        * [Using Podman to authenticate with the registry](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_apikey_auth_podman)

        * [Using Skopeo to authenticate with the registry](/docs/Registry?topic=Registry-registry_access_trusted_profiles#registry_access_trusted_profiles_apikey_auth_skopeo)

[Managing IAM access](/docs/Registry?topic=Registry-iam#iam)

* [Access policies](/docs/Registry?topic=Registry-iam#iam_access_policies)

* [Assign roles](/docs/Registry?topic=Registry-iam#iam_assign_roles)

* [Context-based restrictions](/docs/Registry?topic=Registry-iam#iam_cbr)

* [Platform management roles](/docs/Registry?topic=Registry-iam#platform_management_roles)

* [Service access roles](/docs/Registry?topic=Registry-iam#service_access_roles)

    * [Access roles for configuring {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_configure)

    * [Access roles for using {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-iam#access_roles_using)

* [Assigning access to {{site.data.keyword.registryshort}} in the console](/docs/Registry?topic=Registry-iam&interface=ui#registry_iam_assign-access-console)

* [Assigning access to {{site.data.keyword.registryshort}} in the CLI](/docs/Registry?topic=Registry-iam&interface=cli#registry_iam_assign-access-cli)

* [Assigning access to {{site.data.keyword.registryshort}} by using the API](/docs/Registry?topic=Registry-iam&interface=api#registry_iam_assign-access-api)

* [Assigning access to {{site.data.keyword.registryshort}} by using Terraform](/docs/Registry?topic=Registry-iam&interface=terraform#registry_iam_assign-access-terraform)

[Defining IAM access policies](/docs/Registry?topic=Registry-user#user)

* [Creating policies](/docs/Registry?topic=Registry-user#create)

* [Setting up region-based policies for IAM](/docs/Registry?topic=Registry-user#create_region_policy_iam)

    * [Region-based user policies](/docs/Registry?topic=Registry-user#create_region_policy_user)

    * [Region-based service ID policies](/docs/Registry?topic=Registry-user#create_region_policy_service)


## Managing image security with Vulnerability Advisor
{: #sitemap_managing_image_security_with_vulnerability_advisor}


[Managing image security with Vulnerability Advisor](/docs/Registry?topic=Registry-va_index#va_index)

* [About Vulnerability Advisor](/docs/Registry?topic=Registry-va_index#about)

    * [Data protection](/docs/Registry?topic=Registry-va_index#about_data_protection)

* [Types of vulnerabilities](/docs/Registry?topic=Registry-va_index#types)

    * [Vulnerable packages](/docs/Registry?topic=Registry-va_index#packages)

    * [Configuration issues](/docs/Registry?topic=Registry-va_index#app_configurations)

* [Setting the version of Vulnerability Advisor](/docs/Registry?topic=Registry-va_index#va_set_version)

* [Reviewing a vulnerability report](/docs/Registry?topic=Registry-va_index#va_reviewing)

    * [Reviewing a vulnerability report by using the console](/docs/Registry?topic=Registry-va_index&interface=ui#va_reviewing_gui)

    * [Reviewing a vulnerability report by using the CLI](/docs/Registry?topic=Registry-va_index&interface=cli#va_registry_cli)

* [Setting organizational exemption policies](/docs/Registry?topic=Registry-va_index&interface=cli#va_managing_policy)

    * [Setting exemption policies by using the console](/docs/Registry?topic=Registry-va_index&interface=ui#va_managing_policy_gui)

    * [Setting exemption policies by using the CLI](/docs/Registry?topic=Registry-va_index&interface=cli#va_managing_policy_cli)


## Setting up Terraform
{: #sitemap_setting_up_terraform}


[Setting up Terraform](/docs/Registry?topic=Registry-registry_terraform-setup#registry_terraform-setup)

* [Installing Terraform and creating a {{site.data.keyword.registryshort}} namespace](/docs/Registry?topic=Registry-registry_terraform-setup#registry_terraform-install)

* [Next steps](/docs/Registry?topic=Registry-registry_terraform-setup#registry_terraform-setup-next)


## Enhancing security
{: #sitemap_enhancing_security}


[Managing security and compliance](/docs/Registry?topic=Registry-manage-security-compliance#manage-security-compliance)

[Using VPE for VPC to connect privately](/docs/Registry?topic=Registry-registry_vpe#registry_vpe)

* [Before you begin](/docs/Registry?topic=Registry-registry_vpe#registry_vpe_prereqs)

* [Virtual private endpoints](/docs/Registry?topic=Registry-registry_vpe#registry_vpe_endpoints)

* [Setting up a VPE for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_vpe#registry_vpe_endpoint_setup)

    * [Configuring an endpoint gateway](/docs/Registry?topic=Registry-registry_vpe#registry_endpoint-gateway-servicename)

[Securing your connection](/docs/Registry?topic=Registry-registry_private#registry_private)

* [Using private network connections](/docs/Registry?topic=Registry-registry_private#registry_private_images)

    * [Enabling service endpoint support for the account](/docs/Registry?topic=Registry-registry_private#registry_private_images_endpoints)

    * [Considerations for private network connections](/docs/Registry?topic=Registry-registry_private#registry_private_images_considerations)

    * [Pushing and pulling images](/docs/Registry?topic=Registry-registry_private#registry_private_images_push)

* [Enforcing access to your account](/docs/Registry?topic=Registry-registry_private#registry_private_account)

[Encrypting images for content confidentiality](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt)

* [Before you begin](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_prereqs)

* [Create the public-private key pair](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_create)

* [Encrypt the image](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_image)

* [Pull and decrypt the image](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_pull)

* [Storing keys](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_keys)

* [Next steps](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_next)

[Managing your data](/docs/Registry?topic=Registry-delete-data#delete-data)

* [How your data is stored](/docs/Registry?topic=Registry-delete-data#data-storage)

    * [Image data](/docs/Registry?topic=Registry-delete-data#data-storage_image)

    * [Scanning data](/docs/Registry?topic=Registry-delete-data#data-storage_va)

* [Deleting your data](/docs/Registry?topic=Registry-delete-data#data-delete)

    * [Deleting the service](/docs/Registry?topic=Registry-delete-data#data-delete_service)

    * [Deleting namespaces](/docs/Registry?topic=Registry-delete-data#data-delete_namespaces)

    * [Deleting images](/docs/Registry?topic=Registry-delete-data#data-delete_images)

    * [Deleting private repositories](/docs/Registry?topic=Registry-delete-data#data-delete_private_repo)

* [Restoring deleted data](/docs/Registry?topic=Registry-delete-data#data-restore)

[Signing images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent)

* [Signing images by using {{site.data.keyword.redhat_notm}} signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig)

    * [Using Skopeo to sign images](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig_skopeo)

    * [Using Podman to sign images](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig_podman)

    * [Signing images by using the {{site.data.keyword.redhat_openshift_notm}} CLI](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig_oc)

[Using IAM IP address access restrictions](/docs/Registry?topic=Registry-registry_iam_ip#registry_iam_ip)

* [Granting access if you are using a public network](/docs/Registry?topic=Registry-registry_iam_ip#registry_iam_ip_public)

* [Granting access if you are using a private network](/docs/Registry?topic=Registry-registry_iam_ip#registry_iam_ip_private)

[Enforcing container image security by using Portieris](/docs/Registry?topic=Registry-security_enforce_portieris#security_enforce_portieris)

* [Installing Portieris in your cluster](/docs/Registry?topic=Registry-security_enforce_portieris#sec_enforce_install_portieris)

* [Portieris policies](/docs/Registry?topic=Registry-security_enforce_portieris#policies_portieris)

* [Uninstalling Portieris](/docs/Registry?topic=Registry-security_enforce_portieris#uninstall_portieris)

[Protecting resources with context-based restrictions](/docs/Registry?topic=Registry-registry-cbr#registry-cbr)

* [How {{site.data.keyword.registryshort}} integrates with context-based restrictions](/docs/Registry?topic=Registry-registry-cbr#registry-cbr_overview)

* [Protecting specific resources](/docs/Registry?topic=Registry-registry-cbr#registry-cbr_protect)

* [Limitations](/docs/Registry?topic=Registry-registry-cbr#registry-cbr_limitations)

* [Creating rules](/docs/Registry?topic=Registry-registry-cbr#registry-cbr_create_rules)

    * [Creating rules in the {{site.data.keyword.cloud_notm}} console](/docs/Registry?topic=Registry-registry-cbr&interface=ui#registry-cbr_rules_ui)

    * [Creating rules by using the CLI](/docs/Registry?topic=Registry-registry-cbr&interface=cli#registry-cbr_rules_cli)

    * [Creating rules by using the API](/docs/Registry?topic=Registry-registry-cbr&interface=api#registry-cbr_rules_api)

* [Setting up region-based policies for context-based restrictions](/docs/Registry?topic=Registry-registry-cbr&interface=api#registry-cbr_region_policy)

[Accessing {{site.data.keyword.registryshort}} through a firewall](/docs/Registry?topic=Registry-registry_firewall#registry_firewall)


## Observability
{: #sitemap_observability}


[Monitoring metrics](/docs/Registry?topic=Registry-registry_monitor#registry_monitor)

* [Enabling metrics for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_monitor#registry_enable_platform_metrics)

* [Locations of platform metrics](/docs/Registry?topic=Registry-registry_monitor#registry_monitor_locations)

* [Where to look for metrics](/docs/Registry?topic=Registry-registry_monitor#registry_monitor_ui)

    * [{{site.data.keyword.mon_short}} metrics](/docs/Registry?topic=Registry-registry_monitor#registry_monitor_ui_at)

* [Viewing metrics](/docs/Registry?topic=Registry-registry_monitor#registry_view_metrics)

    * [Starting the Monitoring UI from the Observability page](/docs/Registry?topic=Registry-registry_monitor#registry_view_metrics_opt2)

* [Predefined dashboards](/docs/Registry?topic=Registry-registry_monitor#registry_dashboards_dictionary)

* [Platform metrics](/docs/Registry?topic=Registry-registry_monitor#metrics)

    * [`Pull Traffic`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_pull_traffic)

    * [`Pull Traffic Quota`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_pull_traffic_quota)

    * [`Storage Quota`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_storage_quota)

    * [`Storage`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_storage)

[Activity tracking events](/docs/Registry?topic=Registry-at_events#at_events)

* [Locations where activity tracking events are generated](/docs/Registry?topic=Registry-at_events#at-locations)

* [Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}](/docs/Registry?topic=Registry-at_events#atracker-locations)

* [Viewing activity tracking events for {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-at_events#at-viewing)

    * [Starting {{site.data.keyword.logs_full_notm}} from the Observability page](/docs/Registry?topic=Registry-at_events#at-launch-standalone)

* [Account management events](/docs/Registry?topic=Registry-at_events#at_actions_account)

* [Events for images](/docs/Registry?topic=Registry-at_events#at_actions_images)

* [Events for namespaces](/docs/Registry?topic=Registry-at_events#at_actions_namespaces)

* [Events for vulnerabilities](/docs/Registry?topic=Registry-at_events#at_actions_vuln)

* [Analyzing {{site.data.keyword.registryshort}} activity tracking events](/docs/Registry?topic=Registry-at_events#at_events_iam_analyze)

    * [Request data for vulnerability events](/docs/Registry?topic=Registry-at_events#at_events_vuln_events)

        * [Request data for the account vulnerability report](/docs/Registry?topic=Registry-at_events#at_events_analyze_report_list)

        * [Request data for the account vulnerability status](/docs/Registry?topic=Registry-at_events#at_events_analyze_status_list)

        * [Request and response data for the vulnerability report](/docs/Registry?topic=Registry-at_events#at_events_analyze_report_read)

        * [Request and response data for the vulnerability status](/docs/Registry?topic=Registry-at_events#at_events_analyze_status_read)

    * [Request data for image signing events](/docs/Registry?topic=Registry-at_events#at_events_sign_events)

[Logging](/docs/Registry?topic=Registry-registry_logs#registry_logs)

* [Locations where platform logs are generated](/docs/Registry?topic=Registry-registry_logs#log-locations)

* [Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}](/docs/Registry?topic=Registry-registry_logs#lr-locations)

* [Platform logs that are generated](/docs/Registry?topic=Registry-registry_logs#log-platform)

* [Viewing logs](/docs/Registry?topic=Registry-registry_logs#log-viewing)

    * [Launching {{site.data.keyword.logs_full_notm}} from the Observability page](/docs/Registry?topic=Registry-registry_logs#log-launch-standalone)

* [Fields by log type](/docs/Registry?topic=Registry-registry_logs#log-fields)

[IAM and activity tracker auditing event actions by API method](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam)

* [{{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg)

    * [Authorization API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_auth)

    * [Image API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_images)

    * [Message API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_messages)

    * [Namespace API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_namespace)

    * [Plan API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_plans)

    * [Quota API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_quota)

    * [Retention API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_retention)

    * [Settings API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_set)

    * [Tag API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_tags)

    * [Trash API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_trash)

* [Vulnerability Advisor API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_vuln)

    * [Report API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_vuln_report)

    * [Exemption API methods](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_vuln_exempt)


## Container Registry CLI
{: #sitemap_container_registry_cli}


[CLI](/docs/Registry?topic=Registry-containerregcli#containerregcli)

* [Prerequisites](/docs/Registry?topic=Registry-containerregcli#containerregcli_prereq)

    * [Notes](/docs/Registry?topic=Registry-containerregcli#containerregcli_prereq_notes)

* [`ibmcloud cr api`](/docs/Registry?topic=Registry-containerregcli#bx_cr_api)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_api_prereq)

* [`ibmcloud cr exemption-add`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add_option)

    * [Examples](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_add_example)

* [`ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_list)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_list_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_list_option)

    * [Examples](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_list_example)

* [`ibmcloud cr exemption-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_rm)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_rm_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_rm_option)

    * [Examples](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_rm_example)

* [`ibmcloud cr exemption-types`](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_types)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_types_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_exemption_types_option)

* [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=Registry-containerregcli#bx_cr_iam_policies_enable)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_iam_policies_enable_prereq)

* [`ibmcloud cr iam-policies-status`](/docs/Registry?topic=Registry-containerregcli#bx_cr_iam_policies_status)

* [`ibmcloud cr image-digests` (`ibmcloud cr digests`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_digests_example)

* [`ibmcloud cr image-inspect`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_inspect)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_inspect_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_inspect_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_inspect_example)

* [`ibmcloud cr image-list` (`ibmcloud cr images`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_list_example)

* [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#ic_cr_image_prune_untagged_example)

* [`ibmcloud cr image-restore`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_restore_example)

* [`ibmcloud cr image-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_rm_example)

* [`ibmcloud cr image-tag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_tag)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_tag_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_tag_option)

    * [Examples](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_tag_example)

* [`ibmcloud cr image-untag`](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_untag)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_untag_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_untag_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_image_untag_example)

* [`ibmcloud cr info`](/docs/Registry?topic=Registry-containerregcli#bx_cr_info)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_info_prereq)

* [`ibmcloud cr login`](/docs/Registry?topic=Registry-containerregcli#bx_cr_login)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_login_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_login_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_login__example)

* [`ibmcloud cr manifest-inspect`](/docs/Registry?topic=Registry-containerregcli#bx_cr_manifest_inspect)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_manifest_inspect_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_manifest_inspect_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_manifest_inspect_example)

* [`ibmcloud cr namespace-add`](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_add)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_add_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_add_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_add_example)

* [`ibmcloud cr namespace-assign`](/docs/Registry?topic=Registry-containerregcli#ic_cr_namespace_assign)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#ic_cr_namespace_assign_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#ic_cr_namespace_assign_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#ic_cr_namespace_assign_example)

* [`ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_list_example)

* [`ibmcloud cr namespace-rm`](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_rm)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_rm_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_rm_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_namespace_rm_example)

* [`ibmcloud cr plan`](/docs/Registry?topic=Registry-containerregcli#bx_cr_plan)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_plan_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_plan_option)

* [`ibmcloud cr plan-upgrade`](/docs/Registry?topic=Registry-containerregcli#bx_cr_plan_upgrade)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_plan_upgrade_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_plan_upgrade_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_plan_upgrade_example)

* [`ibmcloud cr platform-metrics`](/docs/Registry?topic=Registry-containerregcli#ic_cr_platform_metrics)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#ic_cr_platform_metrics_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#ic_cr_platform_metrics_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#ic_cr_platform_metrics_example)

* [`ibmcloud cr private-only`](/docs/Registry?topic=Registry-containerregcli#ic_cr_private_only)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#ic_cr_private_only_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#ic_cr_private_only_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#ic_cr_private_only_example)

* [`ibmcloud cr quota`](/docs/Registry?topic=Registry-containerregcli#bx_cr_quota)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_quota_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_quota_option)

* [`ibmcloud cr quota-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_quota_set)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_quota_set_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_quota_set_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_quota_set_example)

* [`ibmcloud cr region`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_prereq)

* [`ibmcloud cr region-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_region_set_example)

* [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_list_example)

* [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set_option)

    * [Examples](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_policy_set_example)

* [`ibmcloud cr retention-run`](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_retention_run_example)

* [`ibmcloud cr trash-list`](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#bx_cr_trash_list_example)

* [`ibmcloud cr va-version`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_prereq)

* [`ibmcloud cr va-version-set`](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set_option)

    * [Example](/docs/Registry?topic=Registry-containerregcli#ic_cr_va_version_set_example)

* [`ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)](/docs/Registry?topic=Registry-containerregcli#bx_cr_va)

    * [Prerequisites](/docs/Registry?topic=Registry-containerregcli#bx_cr_va_prereq)

    * [Command options](/docs/Registry?topic=Registry-containerregcli#bx_cr_va_option)

    * [Examples](/docs/Registry?topic=Registry-containerregcli#bx_cr_va_example)

[Formatting and filtering the CLI output](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list)

* [Go template options for `ibmcloud cr image-digests`](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imagedigests)

* [Go template options for `ibmcloud cr image-list`](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imagelist)

* [Go template options for `ibmcloud cr image-inspect`](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect)

    * [`Config` field details](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect_config)

    * [`Healthcheck` field details](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect_healthcheck)

    * [`RootFS` field details](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect_rootfs)

[CLI change log](/docs/Registry?topic=Registry-registry_cli_change_log#registry_cli_change_log)

* [Version 1.3.13](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-1313)

* [Version 1.3.12](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-1312)

* [Version 1.3.11](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-1311)

* [Version 1.3.10](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-1310)

* [Version 1.3.8](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-138)

* [Version 1.3.7](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-137)

* [Version 1.3.5](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-135)

* [Version 1.3.4](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-134)

* [Version 1.3.1](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-131)

* [Version 1.2.2](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-122)

* [Version 1.1.0](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-110)

* [Version 1.0.11](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-1011)

* [Version 1.0.8](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-108)

* [Version 0.1.587](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-log-01587)

* [Version 1.0.6](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-106)

* [Version 1.0.5](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-105)

* [Version 0.1.585](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-log-01585)

* [Version 1.0.2](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-102)

* [Version 0.1.584](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-log-01584)

* [Version 1.0.1](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-101)

* [Version 0.1.583](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-log-01583)

* [Version 1.0.0](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-logv1-100)

* [Version 0.1.582](/docs/Registry?topic=Registry-registry_cli_change_log#cli-change-log-01582)


## Service dependencies
{: #sitemap_service_dependencies}


[Service dependencies](/docs/Registry?topic=Registry-service-dependencies#service-dependencies)


## High availability and disaster recovery
{: #sitemap_high_availability_and_disaster_recovery}


[High availability](/docs/Registry?topic=Registry-ha-dr#ha-dr)

* [Ownership of responsibilities](/docs/Registry?topic=Registry-ha-dr#ha-responsibilities)

* [What level of availability do I need?](/docs/Registry?topic=Registry-ha-dr#ha-level)

* [What level of availability does {{site.data.keyword.cloud_notm}} offer?](/docs/Registry?topic=Registry-ha-dr#ha-service)

* [Locations for service availability](/docs/Registry?topic=Registry-ha-dr#ha-locations)

* [FAQ about high availability](/docs/Registry?topic=Registry-ha-dr#ha-dr_faq)

    * [Does {{site.data.keyword.cloud_notm}} replicate the service?](/docs/Registry?topic=Registry-ha-dr#ha-dr_service)

    * [Are users required to replicate the service?](/docs/Registry?topic=Registry-ha-dr#ha-dr_service_replicate)

[Business continuity and disaster recovery](/docs/Registry?topic=Registry-bc-dr#bc-dr)

* [Your responsibilities when you're using {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-bc-dr#bc-dr-responsibilities)

* [Disaster recovery strategy](/docs/Registry?topic=Registry-bc-dr#bc-dr-strategy)

* [Locations for service availability](/docs/Registry?topic=Registry-bc-dr#bc-dr-locations)

* [FAQ about disaster recovery](/docs/Registry?topic=Registry-bc-dr#bc-dr_faq)

    * [Does the service replicate the data?](/docs/Registry?topic=Registry-bc-dr#bc-dr_replicate_data)

    * [What data is backed up or replicated?](/docs/Registry?topic=Registry-bc-dr#bc-dr_backup)

    * [Are users required to replicate the data?](/docs/Registry?topic=Registry-bc-dr#bc-dr_client)


## Understanding data portability
{: #sitemap_understanding_data_portability}


[Understanding data portability](/docs/Registry?topic=Registry-data_portability#data_portability)

* [Responsibilities](/docs/Registry?topic=Registry-data_portability#data-portability-responsibilities)

* [Procedures for exporting data](/docs/Registry?topic=Registry-data_portability#data-portability-procedures)

* [Exported data formats](/docs/Registry?topic=Registry-data_portability#data-portability-data-formats)

* [Data ownership](/docs/Registry?topic=Registry-data_portability#data-portability-ownership)


## Your responsibilities
{: #sitemap_your_responsibilities}


[Your responsibilities](/docs/Registry?topic=Registry-registry_responsibilities#registry_responsibilities)

* [Incident and operations management](/docs/Registry?topic=Registry-registry_responsibilities#incident-and-ops)

* [Change management](/docs/Registry?topic=Registry-registry_responsibilities#change-management)

* [Identity and access management](/docs/Registry?topic=Registry-registry_responsibilities#iam-responsibilities)

* [Security and regulation compliance](/docs/Registry?topic=Registry-registry_responsibilities#security-compliance)

* [Disaster recovery](/docs/Registry?topic=Registry-registry_responsibilities#disaster-recovery)


## Terraform reference
{: #sitemap_terraform-reference}

[Terraform reference](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cr_namespace){: external}


## API reference
{: #sitemap_api_reference}


[IBM Cloud Container Registry API](https://{DomainName}/apidocs/container-registry){: external}

[Vulnerability Advisor 4 for IBM Cloud Container Registry API](https://{DomainName}/apidocs/vulnerability-advisor){: external}


## Related links
{: #sitemap_related_links}


[IBM Cloud Kubernetes Service documentation](/docs/containers?topic=containers-getting-started)

[Red Hat OpenShift on IBM Cloud documentation](/docs/openshift?topic=openshift-getting-started)

[IBM Developer - Containers](https://developer.ibm.com/technologies/containers/){: external}


## Troubleshooting
{: #sitemap_troubleshooting}


[Troubleshooting {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-ts_index#ts_index)

* [Troubleshooting topics](/docs/Registry?topic=Registry-ts_index#gettinghelp_ts)

    * [Troubleshooting CLI login](/docs/Registry?topic=Registry-ts_index#gettinghelp_ts_cli_login)

    * [Troubleshooting pull and push errors](/docs/Registry?topic=Registry-ts_index#gettinghelp_ts_pull_push)

    * [Troubleshooting CLI commands](/docs/Registry?topic=Registry-ts_index#gettinghelp_ts_cli_commands)

    * [Troubleshooting networking](/docs/Registry?topic=Registry-ts_index#gettinghelp_ts_network)

    * [Troubleshooting Portieris](/docs/Registry?topic=Registry-ts_index#gettinghelp_ts_portieris)


### Troubleshooting CLI login
{: #sitemap_troubleshooting_cli_login}


[Why can't I log in to {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-login#troubleshoot-login)

[Why does the {{site.data.keyword.registryshort}} login keep expiring?](/docs/Registry?topic=Registry-troubleshoot-login-expire#troubleshoot-login-expire)

[Why can't I get started with {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-get-started#troubleshoot-get-started)

[Why do commands fail saying they're not registered?](/docs/Registry?topic=Registry-troubleshoot-login-error#troubleshoot-login-error)

[Why is docker login on my Mac failing?](/docs/Registry?topic=Registry-troubleshoot-docker-mac#troubleshoot-docker-mac)


### Troubleshooting pull and push errors
{: #sitemap_troubleshooting_pull_and_push_errors}


[Why can't I push or pull a Docker image?](/docs/Registry?topic=Registry-troubleshoot-push-pull-docker#troubleshoot-push-pull-docker)

[Why is pulling images slow?](/docs/Registry?topic=Registry-troubleshoot-pull-performance#troubleshoot-pull-performance)

[Why am I getting Authorization required errors?](/docs/Registry?topic=Registry-troubleshoot-auth-req#troubleshoot-auth-req)

* [Scenario A. You're trying to push or pull an image](/docs/Registry?topic=Registry-troubleshoot-auth-req#troubleshoot-auth-req-push-pull)

* [Scenario B. You're logged in to the wrong region](/docs/Registry?topic=Registry-troubleshoot-auth-req#troubleshoot-auth-req-region)

* [Scenario C. You're trying to use the API](/docs/Registry?topic=Registry-troubleshoot-auth-req#troubleshoot-auth-req-api)

[Why am I getting an Unauthorized error when I use Code Engine?](/docs/Registry?topic=Registry-troubleshoot-unauthorized-ce#troubleshoot-unauthorized-ce)

[Why have I got a problem pulling an image with `cosign` when I use Podman?](/docs/Registry?topic=Registry-troubleshoot-cosign-podman#troubleshoot-cosign-podman)

[Why am I getting Access denied errors?](/docs/Registry?topic=Registry-troubleshoot-access-denied#troubleshoot-access-denied)

[Why am I getting errors for a resource?](/docs/Registry?topic=Registry-troubleshoot-resource#troubleshoot-resource)

[Why am I getting errors about insufficient scope?](/docs/Registry?topic=Registry-troubleshoot-scope#troubleshoot-scope)

[Why am I getting errors about my quota?](/docs/Registry?topic=Registry-troubleshoot-quota#troubleshoot-quota)

[Why am I getting errors about using a private network?](/docs/Registry?topic=Registry-troubleshoot-private#troubleshoot-private)

[Why am I getting a Forbidden error when I'm using Code Engine?](/docs/Registry?topic=Registry-troubleshoot-forbidden-ce#troubleshoot-forbidden-ce)

[Why do images fail to pull from registry with `ImagePullBackOff` or authorization errors?](/docs/Registry?topic=Registry-ts-app-image-pull#ts-app-image-pull)

* [Troubleshooting image pull secrets that use API keys](/docs/Registry?topic=Registry-ts-app-image-pull#img-pull-api-key)


### Troubleshooting CLI commands
{: #sitemap_troubleshooting_cli_commands}


[Why can't I add a namespace?](/docs/Registry?topic=Registry-troubleshoot-add-namespace#troubleshoot-add-namespace)

[Why aren't I authorized to access a specified resource?](/docs/Registry?topic=Registry-troubleshoot-namespace-auth#troubleshoot-namespace-auth)

[Why can't I find my image or my namespace?](/docs/Registry?topic=Registry-troubleshoot-image-find#troubleshoot-image-find)

[Why don't all my namespaces show in the resource list?](/docs/Registry?topic=Registry-troubleshoot-namespace-resource-list#troubleshoot-namespace-resource-list)

[Why does it time out when I list images?](/docs/Registry?topic=Registry-troubleshoot-image-timeout#troubleshoot-image-timeout)

[Why can't I pull the newest image by using the latest tag?](/docs/Registry?topic=Registry-troubleshoot-docker-latest#troubleshoot-docker-latest)

[Why do all the tags get deleted when I delete an image?](/docs/Registry?topic=Registry-troubleshoot-image-rm#troubleshoot-image-rm)

[Why doesn't the retention command show all the images?](/docs/Registry?topic=Registry-troubleshoot-image-list-retention#troubleshoot-image-list-retention)

[Why do I get an error when I'm restoring an image?](/docs/Registry?topic=Registry-troubleshoot-image-restore#troubleshoot-image-restore)

[Why aren't all the tags restored when I restore by digest?](/docs/Registry?topic=Registry-troubleshoot-image-restore-digest#troubleshoot-image-restore-digest)

[Why do I get a manifest unknown error?](/docs/Registry?topic=Registry-troubleshoot-manifest-unknown#troubleshoot-manifest-unknown)

[Why do I get a manifest type error when I tag my image?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-type#troubleshoot-manifest-error-type)

[Why do I get a manifest version error?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-version#troubleshoot-manifest-error-version)

[Why do I get a manifest list invalid error?](/docs/Registry?topic=Registry-troubleshoot-manifest-list-error#troubleshoot-manifest-list-error)

[Why do I get an error about an invalid version of Vulnerability Advisor being specified?](/docs/Registry?topic=Registry-troubleshoot-va-version-error#troubleshoot-va-version-error)


### Troubleshooting networking
{: #sitemap_troubleshooting_networking}


[Why can't I access {{site.data.keyword.registryshort_notm}} through a custom firewall?](/docs/Registry?topic=Registry-troubleshoot-firewall#troubleshoot-firewall)

[Why can't I connect to {{site.data.keyword.registryshort_notm}}?](/docs/Registry?topic=Registry-troubleshoot-connect#troubleshoot-connect)


### Troubleshooting Portieris
{: #sitemap_troubleshooting_portieris}


[Why don't my pods restart after my workers are down?](/docs/Registry?topic=Registry-troubleshoot-pods#troubleshoot-pods)


## FAQ
{: #sitemap_faq}


[FAQ](/docs/Registry?topic=Registry-registry_faq#registry_faq)

* [FAQ for {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_faq#registry_faq_registry)

    * [Where is the reference documentation for {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-registry_faq#faq_ref_docs)

    * [How do I set up the {{site.data.keyword.registryshort}} CLI?](/docs/Registry?topic=Registry-registry_faq#faq_setup_cli)

    * [How do I configure my firewall to allow connections to {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-registry_faq#faq_firewall)

    * [How many namespaces can you have?](/docs/Registry?topic=Registry-registry_faq#faq_namespace)

    * [Can I rename a namespace?](/docs/Registry?topic=Registry-registry_faq#faq_namespace_rename)

    * [Why don't I have authorization to create a namespace?](/docs/Registry?topic=Registry-registry_faq#faq_auth_namespace)

    * [How do I list image names?](/docs/Registry?topic=Registry-registry_faq#faq_list_images)

    * [How do you list public images?](/docs/Registry?topic=Registry-registry_faq#faq_list_public_images)

    * [What tools can I use to build and push images?](/docs/Registry?topic=Registry-registry_faq#faq_tools)

    * [Do images in the trash count toward my quota?](/docs/Registry?topic=Registry-registry_faq#faq_trash)

    * [How do I find the image digest?](/docs/Registry?topic=Registry-registry_faq#faq_digest)

    * [How do I use digests to work with images?](/docs/Registry?topic=Registry-registry_faq#faq_digest_use)

    * [Why can't I push the image into {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-registry_faq#faq_push_images)

    * [How do I list images that are more than a year old?](/docs/Registry?topic=Registry-registry_faq#faq_images_year_old)

    * [How do you use access control?](/docs/Registry?topic=Registry-registry_faq#faq_access_control)

    * [How can I share access to an image?](/docs/Registry?topic=Registry-registry_faq#faq_share_image)

    * [Do I have any untagged images?](/docs/Registry?topic=Registry-registry_faq#faq_untagged_image_1)

    * [Do I need untagged images?](/docs/Registry?topic=Registry-registry_faq#faq_untagged_image_2)

    * [What are eligible images?](/docs/Registry?topic=Registry-registry_faq#faq_eligible_image)

    * [What regions are available?](/docs/Registry?topic=Registry-registry_faq#faq_regions)

    * [How do I get the `docker pull` command to return the most recent version?](/docs/Registry?topic=Registry-registry_faq#faq_docker_pull)

    * [Why do my pods fail with an `ImagePullBackOff` error?](/docs/Registry?topic=Registry-registry_faq#faq_imagepullbackoff)

    * [Why am I getting an exceeded quota error?](/docs/Registry?topic=Registry-registry_faq#faq_quota_error)

* [FAQ for Vulnerability Advisor](/docs/Registry?topic=Registry-registry_faq#registry_faq_va)

    * [How do I manage vulnerabilities?](/docs/Registry?topic=Registry-registry_faq#faq_va_vuln)

    * [How much does Vulnerability Advisor cost?](/docs/Registry?topic=Registry-registry_faq#faq_va_cost)

    * [Can images from other registries be scanned by Vulnerability Advisor?](/docs/Registry?topic=Registry-registry_faq#faq_va_reg)

    * [How is a Vulnerability Advisor scan triggered?](/docs/Registry?topic=Registry-registry_faq#faq_va_trigger_scan)

    * [Why doesn't my image scan in Vulnerability Advisor v4?](/docs/Registry?topic=Registry-registry_faq#faq_va_v4_scan)

    * [Why doesn't a new image scan in Vulnerability Advisor?](/docs/Registry?topic=Registry-registry_faq#faq_va_new_scan_error)

    * [How often are the security notices updated in Vulnerability Advisor?](/docs/Registry?topic=Registry-registry_faq#faq_va_update_security_notice)

    * [Which version of a package is installed in my image?](/docs/Registry?topic=Registry-registry_faq#faq_va_package_version)

        * [Alpine package manager commands](/docs/Registry?topic=Registry-registry_faq#faq_va_package_version_alpine)

        * [Debian and Ubuntu package manager commands](/docs/Registry?topic=Registry-registry_faq#faq_va_package_version_debian_ubuntu)

        * [{{site.data.keyword.redhat_notm}} and CentOS package manager commands](/docs/Registry?topic=Registry-registry_faq#faq_va_package_version_redhat_centos)

    * [Does Vulnerability Advisor have versions?](/docs/Registry?topic=Registry-registry_faq#faq_va_versions)


## Getting help and support
{: #sitemap_getting_help_and_support}


[Getting help and support](/docs/Registry?topic=Registry-help-and-support#help-and-support)

* [Providing support case details](/docs/Registry?topic=Registry-help-and-support#support-case-details)
