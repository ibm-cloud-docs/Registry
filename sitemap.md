---

copyright:
  years: 2021
lastupdated: "2021-12-07"

keywords: container registry

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Site map
{: #sitemap}




## Getting started with Container Registry
{: #sitemap_getting_started_with_container_registry}


[Getting started with Container Registry](/docs/Registry?topic=Registry-getting-started#getting-started)

* [Install the {{site.data.keyword.registrylong_notm}} CLI](/docs/Registry?topic=Registry-getting-started#gs_registry_cli_install)

* [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add)

* [Pull images from another registry to your local computer](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pulling)

* [Push Docker images to your namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pushing)

* [Next steps](/docs/Registry?topic=Registry-getting-started#gs_get_start_next)


## About Container Registry
{: #sitemap_about_container_registry}


[About Container Registry](/docs/Registry?topic=Registry-registry_overview#registry_overview)

* [Service plans](/docs/Registry?topic=Registry-registry_overview#registry_plans)

* [Quota limits and billing](/docs/Registry?topic=Registry-registry_overview#registry_plan_billing)

    * [Billing for storage and pull traffic](/docs/Registry?topic=Registry-registry_overview#registry_billing_traffic)

    * [Quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_overview#registry_quota_limits)

    * [Cost](/docs/Registry?topic=Registry-registry_overview#registry_cost)

* [Upgrading your service plan](/docs/Registry?topic=Registry-registry_overview#registry_plan_upgrade)

* [Find out more about the elements that are used in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_overview#overview_elements)

    * [Container image](/docs/Registry?topic=Registry-registry_overview#overview_elements_container_image)

    * [Dockerfile](/docs/Registry?topic=Registry-registry_overview#overview_elements_dockerfile)

    * [Docker V2 container images](/docs/Registry?topic=Registry-registry_overview#overview_elements_dockerv2_images)

    * [OCI container images](/docs/Registry?topic=Registry-registry_overview#overview_elements_oci_images)

    * [Registry](/docs/Registry?topic=Registry-registry_overview#overview_elements_registry)

    * [Registry namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace)

    * [Repository](/docs/Registry?topic=Registry-registry_overview#overview_elements_repository)

    * [Tag](/docs/Registry?topic=Registry-registry_overview#overview_elements_tag)

    * [Untagged image](/docs/Registry?topic=Registry-registry_overview#overview_elements_untagged)

* [Regions](/docs/Registry?topic=Registry-registry_overview#registry_regions)

    * [Global registry](/docs/Registry?topic=Registry-registry_overview#registry_regions_global)

    * [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local)

* [Support for Docker](/docs/Registry?topic=Registry-registry_overview#docker)


## Container Registry architecture and workload
{: #sitemap_container_registry_architecture_and_workload}


[Container Registry architecture and workload](/docs/Registry?topic=Registry-registry_architecture#registry_architecture)

* [Segmentation](/docs/Registry?topic=Registry-registry_architecture#registry_architecture_segregation)

* [Private connections](/docs/Registry?topic=Registry-registry_architecture#registry_architecture_private_connections)

* [Dependencies to other {{site.data.keyword.cloud_notm}} services](/docs/Registry?topic=Registry-registry_architecture#registry_architecture_dependencies_cloud)

* [Dependencies to third-party services](/docs/Registry?topic=Registry-registry_architecture#registry_architecture_dependencies_third_party)


## Public images
{: #sitemap_public_images}


[Public {{site.data.keyword.IBM_notm}} images](/docs/Registry?topic=Registry-public_images#public_images)

* [Accessing the public IBM images by using the CLI](/docs/Registry?topic=Registry-public_images#public_images_cli)

[Getting started with the `datashield-barbican` image](/docs/Registry?topic=RegistryImages-datashield-barbican_starter#datashield-barbican_starter)

* [Deploying the image](/docs/Registry?topic=RegistryImages-datashield-barbican_starter#datashield-barbican-deploy)

* [Creating a secret](/docs/Registry?topic=RegistryImages-datashield-barbican_starter#datashield-barbican-secret)

[Getting started with the `datashield-mariadb` image](/docs/Registry?topic=RegistryImages-datashield-mariadb_starter#datashield-mariadb_starter)

* [Deploying the image](/docs/Registry?topic=RegistryImages-datashield-mariadb_starter#datashield-mariadb-deploy)

    * [Accepted environment variables](/docs/Registry?topic=RegistryImages-datashield-mariadb_starter#datashield-mariadb-variables)

* [Connecting to the MariaDB instance](/docs/Registry?topic=RegistryImages-datashield-mariadb_starter#datashield-mariadb-connect)

[Getting started with the `datashield-nginx` image](/docs/Registry?topic=RegistryImages-datashield-nginx_starter#datashield-nginx_starter)

* [Deploying the image](/docs/Registry?topic=RegistryImages-datashield-nginx_starter#datashield-nginx-deploy)

[Getting started with the `datashield-vault` image](/docs/Registry?topic=RegistryImages-datashield-vault_starter#datashield-vault_starter)

* [Deploying the image](/docs/Registry?topic=RegistryImages-datashield-vault_starter#datashield-vault-deploy)

* [Accessing a protected instance of Vault](/docs/Registry?topic=RegistryImages-datashield-vault_starter#datashield-vault-access)

[Getting started with the `ibmcloud-secure-perimeter-health` image](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#ibmcloud-secure-perimeter-health)

* [How it works](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_how-it-works)

* [What is included](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_whats_included)

* [Provision a Kubernetes cluster within a Secure Perimeter by using {{site.data.keyword.containerlong_notm}}](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_provision_cluster)

* [Scan private networks within a Secure Perimeter](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_private_networks)

    * [Before you begin](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_private_networks_prereq)

* [Scan public networks outside a Secure Perimeter](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_public_networks)

    * [Before you begin](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_public_networks_prereq)

* [Analyzing scan results](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_scan_results)

* [Container argument reference](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_reference_container_arg)

* [Environment variable reference](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-health#sph_reference_env_var)

[Getting started with the `ibmcloud-secure-perimeter-network` image](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#ibmcloud-secure-perimeter-network)

* [How it works](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_how-it-works)

* [What is included](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_whats_included)

* [Prerequisites](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_prerequisites)

* [Provision a Kubernetes cluster within a Secure Perimeter by using {{site.data.keyword.containerlong_notm}}](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_provision_cluster)

* [Run initial configuration of your Secure Perimeter Vyatta](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_initial_setup)

* [Set up a Kubernetes pod within your Secure Perimeter](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_setup)

* [`config.json` reference](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_reference_config_json)

* [`rules.conf` reference](/docs/Registry?topic=RegistryImages-ibmcloud-secure-perimeter-network#spn_reference_rules_conf)

[Getting started with the `ibm/liberty` image](/docs/Registry?topic=RegistryImages-ibmliberty#ibmliberty)

* [How it works](/docs/Registry?topic=RegistryImages-ibmliberty#ibmliberty_how_it_works)

* [Tags](/docs/Registry?topic=RegistryImages-ibmliberty#ibmliberty_tags)

* [Getting started](/docs/Registry?topic=RegistryImages-ibmliberty#ibmliberty_get_started)

* [Monitoring the Java heap space usage for a container with the CLI](/docs/Registry?topic=RegistryImages-ibmliberty#ibmliberty_monitor_heap)

* [License for production use](/docs/Registry?topic=RegistryImages-ibmliberty#ibm/liberty_license)

[`ibmcloud-backup-restore` image - deprecated](/docs/Registry?topic=RegistryImages-ibmbackup_restore_starter#ibmbackup_restore_starter)

[`ibm-mq` public image](/docs/Registry?topic=RegistryImages-mq#mq)

[`ibm-node-strong-pm` public image - deprecated](/docs/Registry?topic=RegistryImages-node-strong#node-strong)


## What are containers?
{: #sitemap_what-are-containers?}

[What are containers?](https://www.ibm.com/cloud/learn/containers){: external}


## Release notes
{: #sitemap_release_notes}


[Release notes](/docs/Registry?topic=Registry-registry_release_notes#registry_release_notes)

* [1 November 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-01nov2021)

* [5 October 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-05oct2021)

* [2 September 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-02sep2021)

* [30 August 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-30aug2021)

* [19 August 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-19aug2021)

* [9 August 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-09aug2021)

* [8 July 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-08jul2021)

* [21 June 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-21jun2021)

* [10 May 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-10may2021)

* [4 May 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-04may2021)

* [18 February 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-18feb2021)

* [15 February 2021](/docs/Registry?topic=Registry-registry_release_notes#registry-15feb2021)

* [19 November 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-19nov2020)

* [21 October 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-21oct2020)

* [6 October 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-06oct2020)

* [27 August 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-27aug2020)

* [12 August 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-12aug2020)

* [30 July 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-30jul2020)

* [29 July 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-29jul2020)

* [13 July 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-13jul2020)

* [24 June 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-24jun2020)

* [18 May 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-18may2020)

* [30 April 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-30apr2020)

* [16 April 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-16apr2020)

* [3 February 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-3feb2020)

* [31 January 2020](/docs/Registry?topic=Registry-registry_release_notes#registry-31jan2020)

* [4 December 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-4dec2019)

* [25 October 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-25oct2019)

* [14 October 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-14oct2019)

* [23 September 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-23sep2019)

* [1 August 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-01aug2019)

* [25 July 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-25jul2019)

* [1 July 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-1jul2019)

* [27 June 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-27jun2019)

* [13 June 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-13jun2019)

* [13 May 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-13may2019)

* [2 April 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-2apr2019)

* [14 March 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-14mar2019)

* [25 February 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-25feb2019)

* [21 February 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-21feb2019)

* [8 January 2019](/docs/Registry?topic=Registry-registry_release_notes#registry-8jan2019)

* [4 October 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-4oct2018)

* [7 August 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-7aug2018)

* [25 July 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-25jul2018)

* [12 July 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-12jul2018)

* [31 May 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-31may2018)

* [21 March 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-21mar2018)

* [16 March 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-16mar2018)

* [20 February 2018](/docs/Registry?topic=Registry-registry_release_notes#registry-20feb2018)

* [6 November 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-6nov2017)

* [29 September 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-29sep2017)

* [24 August 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-24aug2017)

* [27 June 2017](/docs/Registry?topic=Registry-registry_release_notes#registry-27jun2017)


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

* [Deploying to non-default Kubernetes namespaces](/docs/Registry?topic=Registry-registry_tutorial_workflow#registry_tutorial_workflow_deploy_nondefault_namespaces)


## Granting access to Container Registry resources tutorial
{: #sitemap_granting_access_to_container_registry_resources_tutorial}


[Granting access to Container Registry resources tutorial](/docs/Registry?topic=Registry-iam_access#iam_access)

* [Before you begin](/docs/Registry?topic=Registry-iam_access#iam_access_prereq)

* [Authorize a user to configure the registry](/docs/Registry?topic=Registry-iam_access#configure_registry)

* [Authorize a user to access specific namespaces](/docs/Registry?topic=Registry-iam_access#access_resources)

* [Create a service ID and grant access to a resource](/docs/Registry?topic=Registry-iam_access#service_id)

* [Cleaning up](/docs/Registry?topic=Registry-iam_access#clean_up)


## Solution tutorials
{: #sitemap_solution_tutorials}


[Moving a VM based app to Kubernetes](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes)

* [Objectives](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-objectives)

* [Architecture](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-architecture)

    * [Traditional app architecture with VMs](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-2)

    * [Containerized architecture](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-3)

    * [VMs, containers, and Kubernetes](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-4)

    * [What IBM's doing for you](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-7)

* [Sizing clusters](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-sizing_clusters)

* [Decide what Database option to use](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-database_options)

* [Decide where to store application files](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-decide_where_to_store_data)

    * [Non-persistent data storage](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-11)

    * [Learn how to create persistent data storage for your app](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-12)

    * [Learn how to move existing data to persistent storage](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-13)

    * [Set up backups for persistent storage](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-14)

* [Prepare your code](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-prepare_code)

    * [Apply the 12-factor principles](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-16)

    * [Store credentials in Kubernetes secrets](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-17)

* [Containerize your app](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-build_docker_images)

* [Deploy your app to a Kubernetes cluster](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-deploy_to_kubernetes)

    * [Learn how to create a Kubernetes deployment yaml file](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-20)

* [Summary](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-summary)

* [Put everything learned to practice, run the JPetStore app in your cluster](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-runthejpetstore)

* [Related Content](/docs/Registry?topic=solution-tutorials-vm-to-containers-and-kubernetes#vm-to-containers-and-kubernetes-related)

[Resilient and secure multi-region Kubernetes clusters with {{site.data.keyword.cis_full_notm}}](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis)

* [Objectives](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-objectives)

* [Before you begin](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-prereqs)

* [Deploy an application to one location](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-2)

    * [Create a Kubernetes cluster](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-3)

    * [Deploy the application to the Kubernetes cluster](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-deploy_application)

    * [Get the Ingress Subdomain assigned to the cluster](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-CSALB_IP_subdomain)

    * [Configure the Ingress for your DNS subdomain](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-ingress)

* [And then to another location](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-0)

* [Configure multi-location load-balancing](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-4)

    * [Register a custom domain with {{site.data.keyword.cis_full_notm}}](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-create_cis_instance)

    * [Verify the Global Load Balancer name](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-glb)

    * [Configure Health Check for the Global Load Balancer](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-12)

    * [Define Origin Pools](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-13)

    * [Create the Global Load Balancer](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-17)

* [Secure the application](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-secure_via_CIS)

    * [Turn the Web Application Firewall On](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-20)

    * [Increase performance and protect from Denial of Service attacks](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-proxy_setting)

* [Remove resources](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-6)

    * [Remove Kubernetes Cluster resources](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-23)

    * [Remove {{site.data.keyword.cis_short_notm}} resources](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-24)

* [Related content](/docs/Registry?topic=solution-tutorials-multi-region-k8s-cis#multi-region-k8s-cis-7)

[Continuous Deployment to Kubernetes](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes)

* [Objectives](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-objectives)

* [Before you begin](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-prereq)

* [Create development Kubernetes cluster](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-create_kube_cluster)

* [Create a starter application](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-create_application)

* [Modify the application and deploy the updates](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-6)

* [Deploy to a production environment](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-deploytoproduction)

* [Setup Slack notifications](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-setup_slack)

* [Remove resources](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-removeresources)

* [Expand the Tutorial](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-expandTutorial)

* [Related Content](/docs/Registry?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes-related)


## Setting up the Container Registry CLI and your registry namespace
{: #sitemap_setting_up_the_container_registry_cli_and_your_registry_namespace}


[Setting up the Container Registry CLI and your registry namespace](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace)

* [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install)

* [Updating the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update)

* [Uninstalling the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_uninstall)

* [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan)

    * [User permissions for working with namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan_perm)

* [Setting up a namespace](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_setup)

* [Assigning existing namespaces to resource groups](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_namespace_assign)

* [Removing namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_remove)


## Setting up Container Registry as a private registry on Red Hat OpenShift
{: #sitemap_setting_up_container_registry_as_a_private_registry_on_red_hat_openshift}


[Setting up Container Registry as a private registry on Red Hat OpenShift](/docs/Registry?topic=Registry-registry_rhos#registry_rhos)

* [Set up {{site.data.keyword.openshiftlong_notm}} to use {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_rhoks)

* [Set up {{site.data.keyword.redhat_notm}} OpenShift Container Platform to use {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_os)

    * [Set up the {{site.data.keyword.redhat_notm}} OpenShift Container Platform internal registry to pull from {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_os_pull)

    * [Set up the {{site.data.keyword.redhat_notm}} OpenShift Container Platform build to push images to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_rhos#registry_rhos_os_push)


## Managing quota limits for storage and pull traffic
{: #sitemap_managing_quota_limits_for_storage_and_pull_traffic}


[Managing quota limits for storage and pull traffic](/docs/Registry?topic=Registry-registry_quota#registry_quota)

* [Setting quota limits for storing and pulling images](/docs/Registry?topic=Registry-registry_quota#registry_quota_set)

* [Reviewing quota limits and usage for storing and pulling images](/docs/Registry?topic=Registry-registry_quota#registry_quota_get)

* [Freeing up used storage and changing service plans or quota limits to stay within given quota limits](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup)


## Adding images to your namespace
{: #sitemap_adding_images_to_your_namespace}


[Adding images to your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_)

* [Pulling images from another registry](/docs/Registry?topic=Registry-registry_images_#registry_images_pulling_reg)

* [Pushing Docker images to your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_pushing_namespace)

* [Copying images between registries](/docs/Registry?topic=Registry-registry_images_#registry_images_copying)

* [Creating images that refer to a source image](/docs/Registry?topic=Registry-registry_images_#registry_images_source)

* [Building Docker images to use them with your namespace](/docs/Registry?topic=Registry-registry_images_#registry_images_creating)

* [Pushing images to {{site.data.keyword.registrylong_notm}} by using an API key](/docs/Registry?topic=Registry-registry_images_#registry_api_key_push_image)

* [Removing tags from images in your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_untag)

* [Deleting images from your private {{site.data.keyword.cloud_notm}} repository](/docs/Registry?topic=Registry-registry_images_#registry_images_remove)

    * [Deleting images from your private {{site.data.keyword.cloud_notm}} repository by using the CLI](/docs/Registry?topic=Registry-registry_images_#registry_images_remove_cli)

    * [Deleting images from your private {{site.data.keyword.cloud_notm}} repository by using the {{site.data.keyword.cloud_notm}} console](/docs/Registry?topic=Registry-registry_images_#registry_images_remove_gui)

* [Listing images in the trash](/docs/Registry?topic=Registry-registry_images_#registry_images_list_trash)

* [Restoring images](/docs/Registry?topic=Registry-registry_images_#registry_images_restore)

    * [Restoring images by digest](/docs/Registry?topic=Registry-registry_images_#registry_images_restore_digest)

    * [Restoring images by tag](/docs/Registry?topic=Registry-registry_images_#registry_images_restore_tag)

* [Deleting a private repository and any associated images](/docs/Registry?topic=Registry-registry_images_#registry_repo_remove)


## Accessing {{site.data.keyword.registrylong_notm}}
{: #sitemap_accessing_}


[Accessing {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_access#registry_access)

* [Accessing your namespaces in automation](/docs/Registry?topic=Registry-registry_access#registry_access_automating)

    * [Creating a service ID API key manually](/docs/Registry?topic=Registry-registry_access#registry_access_serviceid_apikey_create)

    * [Creating a user API key manually](/docs/Registry?topic=Registry-registry_access#registry_access_user_apikey_create)

    * [Using client software to authenticate in automation](/docs/Registry?topic=Registry-registry_access#registry_access_apikey_auth)

* [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive)

    * [Buildah](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_buildah)

    * [Docker](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_docker)

    * [Podman](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_podman)

    * [Skopeo](/docs/Registry?topic=Registry-registry_access#registry_access_interactive_auth_skopeo)

* [Accessing your namespaces programmatically](/docs/Registry?topic=Registry-registry_access#registry_access_programmatic)


## Defining access role policies
{: #sitemap_defining_access_role_policies}


[Defining access role policies](/docs/Registry?topic=Registry-user#user)

* [Creating policies](/docs/Registry?topic=Registry-user#create)

* [Enabling policy enforcement for existing users](/docs/Registry?topic=Registry-user#existing_users)


## Managing access
{: #sitemap_managing_access}


[Managing access](/docs/Registry?topic=Registry-iam#iam)

* [Platform management roles](/docs/Registry?topic=Registry-iam#platform_management_roles)

* [Service access roles](/docs/Registry?topic=Registry-iam#service_access_roles)

    * [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure)

    * [Access roles for using {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_using)


## Cleaning up your namespaces
{: #sitemap_cleaning_up_your_namespaces}


[Cleaning up your namespaces](/docs/Registry?topic=Registry-registry_retention#registry_retention)

* [Planning retention](/docs/Registry?topic=Registry-registry_retention#retention_plan)

* [Clean up your namespaces by retaining only images that meet your criteria](/docs/Registry?topic=Registry-registry_retention#retention_images)

* [Set a retention policy for your namespaces to retain only images that meet your criteria](/docs/Registry?topic=Registry-registry_retention#retention_policy_set)

* [Updating a retention policy so that it keeps all your images](/docs/Registry?topic=Registry-registry_retention#retention_policy_keep)

* [Clean up your namespaces by deleting untagged images](/docs/Registry?topic=Registry-registry_retention#retention_images_untagged)


## Managing your data
{: #sitemap_managing_your_data}


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


## Managing image security with Vulnerability Advisor
{: #sitemap_managing_image_security_with_vulnerability_advisor}


[Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index#va_index)

* [About Vulnerability Advisor](/docs/Registry?topic=va-va_index#about)

    * [Data protection](/docs/Registry?topic=va-va_index#about_data_protection)

* [Types of vulnerabilities](/docs/Registry?topic=va-va_index#types)

    * [Vulnerable packages](/docs/Registry?topic=va-va_index#packages)

    * [Configuration issues](/docs/Registry?topic=va-va_index#app_configurations)

* [Reviewing a vulnerability report](/docs/Registry?topic=va-va_index#va_reviewing)

    * [Reviewing a vulnerability report by using the {{site.data.keyword.cloud_notm}} console](/docs/Registry?topic=va-va_index#va_reviewing_gui)

    * [Reviewing a vulnerability report by using the CLI](/docs/Registry?topic=va-va_index#va_registry_cli)

* [Setting organizational exemption policies](/docs/Registry?topic=va-va_index#va_managing_policy)

    * [Setting organizational exemption policies by using the {{site.data.keyword.cloud_notm}} console](/docs/Registry?topic=va-va_index#va_managing_policy_gui)

    * [Setting organizational exemption policies by using the CLI](/docs/Registry?topic=va-va_index#va_managing_policy_cli)


## Setting up Terraform for {{site.data.keyword.registrylong_notm}}
{: #sitemap_setting_up_terraform_for_}


[Setting up Terraform for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_terraform-setup#registry_terraform-setup)

* [Installing Terraform and creating a {{site.data.keyword.registryshort}} namespace](/docs/Registry?topic=Registry-registry_terraform-setup#registry_terraform-install)

* [What's next?](/docs/Registry?topic=Registry-registry_terraform-setup#registry_terraform-setup-next)


## Enhancing security
{: #sitemap_enhancing_security}


[Managing security and compliance](/docs/Registry?topic=Registry-manage-security-compliance#manage-security-compliance)

* [Monitoring security and compliance posture with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-manage-security-compliance#monitor-container-registry)

    * [Available goals for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-manage-security-compliance#container-registry-available-goals)

* [Gaining security insight with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-manage-security-compliance#container-registry-security_insight)

[Signing images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent)

* [Signing images for trusted content by using {{site.data.keyword.redhat_notm}} Signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig)

    * [Using Skopeo to sign images](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig_skopeo)

    * [Using Podman to sign images](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig_podman)

    * [Using OpenShift CLI to sign images](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent_red_hat_sig_oc)

[Encrypting images for content confidentiality](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt)

* [Before you begin](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_prereqs)

* [Create the public-private key pair](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_create)

* [Encrypt the image](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_image)

* [Pull and decrypt the image](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_pull)

* [Storing keys](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_keys)

* [Next steps](/docs/Registry?topic=Registry-registry_encrypt#registry_encrypt_next)

[Securing your connection to {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_private#registry_private)

* [Using private network connections for image pushes and pulls](/docs/Registry?topic=Registry-registry_private#registry_private_images)

    * [Enabling {{site.data.keyword.cloud_notm}} service endpoint support for the account](/docs/Registry?topic=Registry-registry_private#registry_private_images_endpoints)

    * [Considerations](/docs/Registry?topic=Registry-registry_private#registry_private_images_considerations)

    * [Pushing and pulling images](/docs/Registry?topic=Registry-registry_private#registry_private_images_push)

* [Enforcing access to your account over private network connections](/docs/Registry?topic=Registry-registry_private#registry_private_account)

[Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_vpe#registry_vpe)

* [Before you begin](/docs/Registry?topic=Registry-registry_vpe#registry_vpe_prereqs)

* [Virtual private service endpoints](/docs/Registry?topic=Registry-registry_vpe#registry_vpe_endpoints)

* [Setting up a VPE for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_vpe#registry_vpe_endpoint_setup)

    * [Configuring an endpoint gateway](/docs/Registry?topic=Registry-registry_vpe#registry_endpoint-gateway-servicename)

[Using IAM IP address access restrictions](/docs/Registry?topic=Registry-registry_iam_ip#registry_iam_ip)

* [Granting access if you are using {{site.data.keyword.registrylong_notm}} over the public network](/docs/Registry?topic=Registry-registry_iam_ip#registry_iam_ip_public)

* [Granting access if you are using {{site.data.keyword.registrylong_notm}} over the private network](/docs/Registry?topic=Registry-registry_iam_ip#registry_iam_ip_private)

[Enforcing container image security by using Portieris](/docs/Registry?topic=Registry-security_enforce_portieris#security_enforce_portieris)

* [Installing Portieris in your cluster](/docs/Registry?topic=Registry-security_enforce_portieris#sec_enforce_install_portieris)

* [Policies](/docs/Registry?topic=Registry-security_enforce_portieris#policies_portieris)

* [Uninstalling Portieris](/docs/Registry?topic=Registry-security_enforce_portieris#uninstall_portieris)


## Observability
{: #sitemap_observability}


[Monitoring metrics](/docs/Registry?topic=Registry-registry_monitor#registry_monitor)

* [Platform metrics overview](/docs/Registry?topic=Registry-registry_monitor#registry_platform_metrics)

* [Enabling platform metrics by using the {{site.data.keyword.registryshort_notm}} CLI](/docs/Registry?topic=Registry-registry_monitor#registry_enable_platform_metrics)

* [Viewing metrics](/docs/Registry?topic=Registry-registry_monitor#registry_view_metrics)

    * [Starting the Monitoring UI from the Observability page](/docs/Registry?topic=Registry-registry_monitor#registry_view_metrics_opt2)

* [{{site.data.keyword.registryshort_notm}} predefined dashboards](/docs/Registry?topic=Registry-registry_monitor#registry_dashboards_dictionary)

* [Metrics available by service plan](/docs/Registry?topic=Registry-registry_monitor#metrics-by-plan)

    * [`Pull Traffic`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_pull_traffic)

    * [`Pull Traffic Quota`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_pull_traffic_quota)

    * [`Storage Quota`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_storage_quota)

    * [`Storage Used`](/docs/Registry?topic=Registry-registry_monitor#ibm_containerregistry_storage)

* [Attributes for segmentation](/docs/Registry?topic=Registry-registry_monitor#attributes)

    * [Global Attributes](/docs/Registry?topic=Registry-registry_monitor#global-attributes)

    * [Other Attributes](/docs/Registry?topic=Registry-registry_monitor#additional-attributes)

[Auditing the events](/docs/Registry?topic=Registry-at_events#at_events)

* [API methods](/docs/Registry?topic=Registry-at_events#at_events_api_methods)

* [Where to look for the events](/docs/Registry?topic=Registry-at_events#ui)

    * [{{site.data.keyword.at_full_notm}} events](/docs/Registry?topic=Registry-at_events#ui_at)

* [Analyzing Activity Tracker events](/docs/Registry?topic=Registry-at_events#at_events_analyze)

    * [Request data for `container-registry.account-vulnerability-report.list`](/docs/Registry?topic=Registry-at_events#at_events_analyze_report_list)

    * [Request data for `container-registry.account-vulnerability-status.list`](/docs/Registry?topic=Registry-at_events#at_events_analyze_status_list)

    * [Request and response data for `container-registry.image-vulnerability-report.read`](/docs/Registry?topic=Registry-at_events#at_events_analyze_report_read)

    * [Request and response data for `container-registry.image-vulnerability-status.read`](/docs/Registry?topic=Registry-at_events#at_events_analyze_status_read)

[Analyzing logs](/docs/Registry?topic=Registry-registry_logs#registry_logs)

* [Where to look for {{site.data.keyword.la_full_notm}} logs](/docs/Registry?topic=Registry-registry_logs#registry_logs_region)

[IAM and Activity Tracker actions by API method](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam)

* [{{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg)

    * [Auth](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_auth)

    * [Images](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_images)

    * [Messages](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_messages)

    * [Namespaces](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_namespace)

    * [Plans](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_plans)

    * [Quotas](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_quota)

    * [Retentions](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_retention)

    * [Settings](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_set)

    * [Tags](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_tags)

    * [Trash](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_reg_trash)

* [Vulnerability Advisor](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_vuln)

    * [Report](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_vuln_report)

    * [Exemption](/docs/Registry?topic=Registry-registry_at_iam#registry_at_iam_vuln_exempt)


## {{site.data.keyword.registrylong_notm}} CLI
{: #sitemap__cli}


[{{site.data.keyword.registrylong_notm}} CLI](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#containerregcli)

* [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#containerregcli_prereq)

* [`ibmcloud cr api`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_api)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_api_prereq)

* [`ibmcloud cr exemption-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add_option)

    * [Examples](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_add_example)

* [`ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list_option)

    * [Examples](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list_example)

* [`ibmcloud cr exemption-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm_option)

    * [Examples](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_rm_example)

* [`ibmcloud cr exemption-types`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_types_prereq)

* [`ibmcloud cr iam-policies-enable`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable_prereq)

* [`ibmcloud cr iam-policies-status`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_status)

* [`ibmcloud cr image-digests` (`ibmcloud cr digests`)](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_digests_example)

* [`ibmcloud cr image-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect_example)

* [`ibmcloud cr image-list` (`ibmcloud cr images`)](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list_example)

* [`ibmcloud cr image-prune-untagged`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_image_prune_untagged_example)

* [`ibmcloud cr image-restore`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_restore_example)

* [`ibmcloud cr image-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm_example)

* [`ibmcloud cr image-tag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag_option)

    * [Examples](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag_example)

* [`ibmcloud cr image-untag`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag_example)

* [`ibmcloud cr info`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_info)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_info_prereq)

* [`ibmcloud cr login`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_login)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_login_prereq)

* [`ibmcloud cr manifest-inspect`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_manifest_inspect_example)

* [`ibmcloud cr namespace-add`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_add_example)

* [`ibmcloud cr namespace-assign`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_namespace_assign)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_namespace_assign_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_namespace_assign_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_namespace_assign_example)

* [`ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_list_example)

* [`ibmcloud cr namespace-rm`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_namespace_rm_example)

* [`ibmcloud cr plan`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_prereq)

* [`ibmcloud cr plan-upgrade`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_plan_upgrade_example)

* [`ibmcloud cr platform-metrics`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_platform_metrics_example)

* [`ibmcloud cr private-only`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#ic_cr_private_only_example)

* [`ibmcloud cr quota`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_prereq)

* [`ibmcloud cr quota-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_quota_set_example)

* [`ibmcloud cr region`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_prereq)

* [`ibmcloud cr region-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_region_set_example)

* [`ibmcloud cr retention-policy-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list_prereq)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_list_example)

* [`ibmcloud cr retention-policy-set`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set_option)

    * [Examples](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_policy_set_example)

* [`ibmcloud cr retention-run`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run_example)

* [`ibmcloud cr trash-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list_option)

    * [Example](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_trash_list_example)

* [`ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va)

    * [Prerequisites](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va_prereq)

    * [Command options](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va_option)

    * [Examples](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_va_example)


## Understanding high availability and disaster recovery
{: #sitemap_understanding_high_availability_and_disaster_recovery}


[Understanding high availability and disaster recovery](/docs/Registry?topic=Registry-ha-dr#ha-dr)

* [Frequently asked questions about high availability and disaster recovery](/docs/Registry?topic=Registry-ha-dr#ha-dr_faq)

    * [Does the service replicate the data?](/docs/Registry?topic=Registry-ha-dr#ha-dr_replicate_data)

    * [Are users required to replicate the data?](/docs/Registry?topic=Registry-ha-dr#ha-dr_client)

    * [What data is backed-up or replicated?](/docs/Registry?topic=Registry-ha-dr#ha-dr_backup)

    * [Does {{site.data.keyword.cloud_notm}} replicate the service?](/docs/Registry?topic=Registry-ha-dr#ha-dr_service)

    * [Are users required to replicate the service?](/docs/Registry?topic=Registry-ha-dr#ha-dr_service_replicate)


## Formatting and filtering the CLI output for Container Registry commands
{: #sitemap_formatting_and_filtering_the_cli_output_for_container_registry_commands}


[Formatting and filtering the CLI output for Container Registry commands](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list)

* [Go template options and data types in the `ibmcloud cr image-digests` command](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imagedigests)

* [Go template options and data types in the `ibmcloud cr image-list` command](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imagelist)

* [Go template options and data types in the `ibmcloud cr image-inspect` command](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect)

    * [`Config`](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect_config)

    * [`Healthcheck`](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect_healthcheck)

    * [`RootFS`](/docs/Registry?topic=Registry-registry_cli_list#registry_cli_list_imageinspect_rootfs)


## Understanding your responsibilities when you are using {{site.data.keyword.registryshort_notm}}
{: #sitemap_understanding_your_responsibilities_when_you_are_using_}


[Understanding your responsibilities when you are using {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=Registry-registry_responsibilities#registry_responsibilities)

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

[Vulnerability Advisor for IBM Cloud Container Registry API](https://{DomainName}/apidocs/container-registry/va){: external}


## Related links
{: #sitemap_related_links}


[IBM Cloud Kubernetes Service documentation](/docs/containers?topic=containers-getting-started)

[Red Hat OpenShift on IBM Cloud documentation](/docs/openshift?topic=openshift-getting-started)

[IBM Developer - Containers](https://developer.ibm.com/technologies/containers/){: external}


## Troubleshooting
{: #sitemap_troubleshooting}


[Troubleshooting](/docs/Registry?topic=Registry-ts_index#ts_index)

* [Getting help and support for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-ts_index#gettinghelp)

[Why can't I log in to Container Registry?](/docs/Registry?topic=Registry-troubleshoot-login#troubleshoot-login)

[Why does the Container Registry login keep expiring?](/docs/Registry?topic=Registry-troubleshoot-login-expire#troubleshoot-login-expire)

[Why do I get a failure message when I run any command in Container Registry?](/docs/Registry?topic=Registry-troubleshoot-login-cloud#troubleshoot-login-cloud)

[Why do all the Container Registry commands fail?](/docs/Registry?topic=Registry-troubleshoot-login-error#troubleshoot-login-error)

[Why can't I add a namespace?](/docs/Registry?topic=Registry-troubleshoot-add-namespace#troubleshoot-add-namespace)

[Why don't all my namespaces show up in the **Resource list** page in the {{site.data.keyword.cloud_notm}} console?](/docs/Registry?topic=Registry-troubleshoot-namespace-resource-list#troubleshoot-namespace-resource-list)

[Why can't I push or pull a Docker image?](/docs/Registry?topic=Registry-troubleshoot-push-pull-docker#troubleshoot-push-pull-docker)

[Why can't I pull the most recent image by using the `latest` tag?](/docs/Registry?topic=Registry-troubleshoot-docker-latest#troubleshoot-docker-latest)

[Why does listing images timeout?](/docs/Registry?topic=Registry-troubleshoot-image-timeout#troubleshoot-image-timeout)

[I used the `ibmcloud cr image-rm` command to delete an image, why did all the tags get deleted too?](/docs/Registry?topic=Registry-troubleshoot-image-rm#troubleshoot-image-rm)

[Why doesn't an image show on the list that is produced by the `ibmcloud cr retention-run` command?](/docs/Registry?topic=Registry-troubleshoot-image-list-retention#troubleshoot-image-list-retention)

[When I'm restoring an image, why do I get an error that says that the tagged image exists?](/docs/Registry?topic=Registry-troubleshoot-image-restore#troubleshoot-image-restore)

[When I'm restoring an image from the trash by digest, why aren't some tags restored?](/docs/Registry?topic=Registry-troubleshoot-image-restore-digest#troubleshoot-image-restore-digest)

[Why can't I access the registry through a custom firewall?](/docs/Registry?topic=Registry-troubleshoot-firewall#troubleshoot-firewall)

[Why am I getting access denied errors even though I have an IAM access policy?](/docs/Registry?topic=Registry-troubleshoot-iam-policy#troubleshoot-iam-policy)

[Why don't my pods restart after my workers were down?](/docs/Registry?topic=Registry-troubleshoot-pods#troubleshoot-pods)

[Why am I getting a manifest type error when I try to tag my image?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-type#troubleshoot-manifest-error-type)

[Why am I getting a manifest version error when I try to tag my image?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-version#troubleshoot-manifest-error-version)

[Why does Docker login fail on my Mac?](/docs/Registry?topic=Registry-troubleshoot-docker-mac#troubleshoot-docker-mac)


## Frequently asked questions (FAQs)
{: #sitemap_frequently_asked_questions_faqs}


[Frequently asked questions (FAQs)](/docs/Registry?topic=Registry-registry_faq#registry_faq)

* [How do you list public images?](/docs/Registry?topic=Registry-registry_faq#faq_list_public_images)

* [Can you use non-docker tools to build my images and push them to the registry?](/docs/Registry?topic=Registry-registry_faq#faq_tools)

* [Is there a limit to the number of namespaces you can have?](/docs/Registry?topic=Registry-registry_faq#faq_namespace)

* [Do images in the trash count toward my quota?](/docs/Registry?topic=Registry-registry_faq#faq_trash)

* [How do you use access control with {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}}?](/docs/Registry?topic=Registry-registry_faq#faq_access_control)

* [What regions are available for {{site.data.keyword.registrylong_notm}}?](/docs/Registry?topic=Registry-registry_faq#faq_regions)

* [Why have I received a scan not found error message for a newly added image?](/docs/Registry?topic=Registry-registry_faq#faq_va_new_scan_error)

* [How is a Vulnerability Advisor scan triggered?](/docs/Registry?topic=Registry-registry_faq#faq_va_trigger_scan)

* [How often are the security notices updated?](/docs/Registry?topic=Registry-registry_faq#faq_va_update_security_notice)
