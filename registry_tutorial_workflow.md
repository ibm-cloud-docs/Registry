---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-03"

keywords: Vulnerability Advisor, tutorial, workflow, image, vulnerabilities, registry, services, container, namespace, vulnerability, cluster, vulnerable image

subcollection: Registry

content-type: tutorial
services: containers
account-plan: lite
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort_notm}} and Vulnerability Advisor workflow
{: #registry_tutorial_workflow}
{: toc-content-type="tutorial"}
{: toc-services="containers"}
{: toc-completion-time="2h"}

Use this tutorial to find out about the basic functions of both {{site.data.keyword.registrylong}} and Vulnerability Advisor.
{: shortdesc}

These two services are pre-integrated and work together seamlessly in {{site.data.keyword.cloud_notm}}, and their features provide a robust but straightforward workflow for users of containers. You can use these services to store your container images, ensure the security of your images and Kubernetes clusters, control the images that you can use to deploy to your clusters, and more.

Much of the information that is provided in this tutorial is available in greater detail in the "How To" sections of the documentation. This tutorial combines all those tasks into a workflow that helps you to use {{site.data.keyword.registrylong_notm}} and Vulnerability Advisor. To learn more about each task, click the relevant link.

## Objectives
{: #registry_tutorial_workflow_objectives}

The tutorial has the following objectives.

- Understand the core features of {{site.data.keyword.registrylong_notm}} and Vulnerability Advisor.
- Use the functions of these services to create a workflow.

## Services used
{: #registry_tutorial_workflow_services}

This tutorial uses the following {{site.data.keyword.cloud_notm}} services:

- [{{site.data.keyword.registrylong_notm}}](https://cloud.ibm.com/registry/repos)
- [{{site.data.keyword.containerlong_notm}}](https://cloud.ibm.com/kubernetes/catalog/about)

## Before you begin
{: #registry_tutorial_workflow_prereqs}

Before you begin, complete the following tasks:

- [Install Git](https://git-scm.com/){: external}.
- [Install {{site.data.keyword.cloud_notm}} Developer Tools](https://github.com/IBM-Cloud/ibm-cloud-developer-tools){: external}, a script to install `docker`, `kubectl`, `helm`, `ibmcloud` CLI, and required plug-ins by following the instructions in the `README.md` file in the repository.
- [Create a cluster](/docs/containers?topic=containers-clusters).
- Ensure that you have the correct access permissions for adding and removing [namespaces](x2031005){: term}, see [Access roles for configuring {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#access_roles_configure).

## From code to a running container
{: #registry_tutorial_workflow_code_run}
{: step}

Using [{{site.data.keyword.registrylong_notm}}](https://www.ibm.com/cloud/container-registry){: external} to store your container images is the easiest way to get an application up and running with {{site.data.keyword.containerlong_notm}}. The following steps show you how to build a container image, store it in {{site.data.keyword.registrylong_notm}}, and create a Kubernetes deployment that uses that image.

### Create a namespace
{: #registry_tutorial_workflow_create_namespace}

Create a [namespace](x2031005){: term} to store your container images in {{site.data.keyword.registrylong_notm}}. If you create a namespace in version 0.1.485 of the {{site.data.keyword.registryshort_notm}} CLI or later, or in the {{site.data.keyword.cloud_notm}} console on or after 29 July 2020, it is created in a [resource group](x2161955){: term}. Namespaces created in version 0.1.484 of the {{site.data.keyword.registryshort_notm}} CLI or earlier, or in the {{site.data.keyword.cloud_notm}} console before 29 July 2020, aren't assigned to [resource groups](/docs/account?topic=account-rgs). For more information, see [Planning namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan).

1. To log in to {{site.data.keyword.cloud_notm}} and target the `us-south` region, run the following command.

    ```txt
    ibmcloud login -r us-south [--sso]
    ```
    {: pre}

    If you have a federated ID, use `ibmcloud login -r us-south --sso` to log in. Enter your username and use the provided URL in your CLI output to retrieve your one-time passcode. If you have a federated ID, the login fails without the `--sso` and succeeds with the `--sso` option.
    {: tip}

2. Set `us-south` as the target region for the {{site.data.keyword.registrylong_notm}} commands.

    ```txt
    ibmcloud cr region-set us-south
    ```
    {: pre}

3. Create a namespace by running the following command. Choose a name for your namespace, and replace `<my_namespace>` with that name.

    The namespace must be unique across all {{site.data.keyword.cloud_notm}} accounts in the same region. Namespaces must have 4 - 30 characters and include lowercase letters, numbers, hyphens (-), and underscores (_) only. Namespaces must start and end with a letter or number.
    {: tip}

    If you want to create the namespace in a specific resource group, see [Set up a namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).
    {: tip}

    ```txt
    ibmcloud cr namespace-add <my_namespace>
    ```
    {: pre}

    Throughout this tutorial, replace `<my_namespace>` with your chosen namespace.

    If you have trouble adding a namespace, see [Why can't I add a namespace?](/docs/Registry?topic=Registry-troubleshoot-add-namespace) for assistance.
    {: tip}

### Build and push an image
{: #registry_tutorial_workflow_build_push_image}

To [build a container image and push it to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_images_#registry_images_creating), you require an application and a [Dockerfile](x9860414){: term}. To get the application and the Dockerfile, and the other artifacts that you require, clone the [GitHub repository](https://github.com/IBM/registry-va-workflow){: external} that is associated with this tutorial. For the rest of this tutorial, ensure that you run all commands from the directory of the cloned repository.

1. To build the image, run the following command:

    ```txt
    docker build -t us.icr.io/<my_namespace>/hello-world:1 .
    ```
    {: pre}

    Docker must be running on your computer or the `docker` commands fail. {{site.data.keyword.registrylong_notm}} supports other clients as well as Docker. To log in by using other clients, see [Accessing your namespaces interactively](/docs/Registry?topic=Registry-registry_access#registry_access_interactive).
    {: tip}

2. Log your local Docker daemon into {{site.data.keyword.registrylong_notm}} by running the [`ibmcloud cr login`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_login) command:

    ```txt
    ibmcloud cr login
    ```
    {: pre}

    If you have trouble logging in, see [Why can't I log in to {{site.data.keyword.registryshort_notm}}?](/docs/Registry?topic=Registry-troubleshoot-login) for assistance.
    {: tip}

3. Push the image by running the following command:

    ```txt
    docker push us.icr.io/<my_namespace>/hello-world:1
    ```
    {: pre}

4. Confirm that your image uploaded successfully by running the following command:

    ```txt
    ibmcloud cr images
    ```
    {: pre}

    You can [automate access to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_access) with [API keys](x8051010){: term} and [grant access to {{site.data.keyword.registrylong_notm}} resources](/docs/Registry?topic=Registry-iam_access) by using IAM.
    {: tip}

### Deploy a container that uses your image
{: #registry_tutorial_workflow_deploy}

Now that you have an image that is stored in {{site.data.keyword.registrylong_notm}}, you can run a container on {{site.data.keyword.containerlong_notm}} that uses that image, see [Deploying apps with the CLI](/docs/containers?topic=containers-deploy_app#app_cli).

Throughout this tutorial, replace `<my_cluster>` with the name of your free Kubernetes cluster.

1. Run the following command:

    ```txt
    ibmcloud ks cluster-config <my_cluster> --export
    ```
    {: pre}

    This command produces an `export` command that sets the `KUBECONFIG` environment variable.

2. Run the `export` command, which was generated by the previous command, by copying and pasting it.

3. Update the following line in the `hello-world.yaml` file by replacing `<my_namespace>` with your namespace:

    ```txt
    image: us.icr.io/<my_namespace>/hello-world:1
    ```
    {: pre}

4. Run your image as a deployment and expose it by creating a service that is accessed through the IP address of the worker node:

    ```txt
    kubectl apply -f hello-world.yaml
    ```
    {: pre}

5. Find the port that is used on the worker node by examining your new service by running the following command:

    ```txt
    kubectl describe service hello-world
    ```
    {: pre}

    Note the number on the `NodePort:` line. Throughout this tutorial, use the number to replace the variable `<node_port>`.

6. In the output of the following command, note the public IP address. Throughout this tutorial, replace the variable `<public_ip>` with the IP address:

    ```txt
    ibmcloud ks workers <my_cluster>
    ```
    {: pre}

7. Access your service by running the following command. You can also use a web browser.

    ```txt
    curl <public_ip>:<node_port>
    ```
    {: pre}

    If you see "Hello, world!", you're good to go.

## Secure your images and clusters
{: #registry_tutorial_workflow_secure}
{: step}

When you push an image to a namespace, the image is automatically scanned by [Vulnerability Advisor](/docs/Registry?topic=va-va_index) to find [potential vulnerabilities](/docs/Registry?topic=va-va_index#types). If vulnerabilities are found, instructions are provided to help fix the reported vulnerabilities.

To demonstrate these features, you must push an intentionally vulnerable image.

Images are continually updated and new CVEs are discovered. As a result, you might see more vulnerabilities present in your image. If so, fix those vulnerabilities by using the information that is provided by Vulnerability Advisor.
{: note}

### View the vulnerability report for your image
{: #registry_tutorial_workflow_vulnerability_report}

When a vulnerability is found in one of your images, a [report](/docs/Registry?topic=va-va_index#va_reviewing) is produced that gives you more information about the vulnerability and the steps to resolve the vulnerability.

1. Build and push a vulnerable image:
    1. Build a vulnerable image by running the following command:

        ```txt
        docker build -t us.icr.io/<my_namespace>/hello-world:2 -f Dockerfile-vulnerable .
        ```
        {: pre}

    2. Push the vulnerable image by running the following command:

        ```txt
        docker push us.icr.io/<my_namespace>/hello-world:2
        ```
        {: pre}

    You can read the Dockerfile to better understand how this image was made vulnerable. In short, a Debian base image is used, and the `apt` package is rolled back to a version that is vulnerable to `CVE-2019-3462`.

2. List your images, and take note of the `SECURITY STATUS` column by running the following command:

    ```txt
    ibmcloud cr images
    ```
    {: pre}

    This column conveys the number of issues present in your image. Because the number isn't zero, this image is vulnerable.

3. Run the `ibmcloud cr vulnerability-assessment` (alias `ibmcloud cr va`) command to get more information about the vulnerability:

    ```txt
    ibmcloud cr va us.icr.io/<my_namespace>/hello-world:1
    ```
    {: pre}

    Among other things, this output includes the ID of the vulnerability (if applicable), the affected package, and the steps to resolve the issue.

### Enforce security in your cluster
{: #registry_tutorial_workflow_enforce_security}

Despite the vulnerability that is present in your image, you're still able to deploy a container to your cluster by using this image, which you might not want. By using [Portieris](/docs/Registry?topic=Registry-security_enforce_portieris), you can enforce security in several ways. For example, you can prevent vulnerable images from being used in deployments to your cluster.

1. [Install Portieris](/docs/Registry?topic=Registry-security_enforce_portieris#sec_enforce_install_portieris).

2. The [Portieris default policies](/docs/Registry?topic=Registry-security_enforce_portieris#policies_portieris) are too restrictive for this tutorial because they involve [image signing](/docs/Registry?topic=Registry-registry_trustedcontent). Therefore, you must create custom policies. View the `security.yaml` file in the [GitHub repository](https://github.com/IBM/registry-va-workflow){: external}, and read about customizing [policies](/docs/Registry?topic=Registry-security_enforce_portieris#policies_portieris) to understand this file's contents. In short, this policy requires all images in your namespace to have no issues reported by Vulnerability Advisor.

3. Update the following line in the `security.yaml` file by replacing `<my_namespace>` with your namespace:

    ```txt
    - name: us.icr.io/<my_namespace>/*
    ```
    {: pre}

4. Apply the custom policies:

    ```txt
    kubectl apply -f security.yaml
    ```
    {: pre}

5. To update `hello-world.yaml` so that it references your vulnerable image, change the tag from `1` to `2` as shown here:

    ```txt
    image: us.icr.io/<my_namespace>/hello-world:2
    ```
    {: pre}

6. Try to patch the existing deployment by running the following command:

    ```txt
    kubectl apply -f hello-world.yaml
    ```
    {: pre}

    You see the following error message:

    ```txt
    Deny "us.icr.io/<my_namespace>/hello-world:2", the Vulnerability Advisor image scan assessment
    found issues with the container image that are not exempted. Refer to your image vulnerability
    report for more details by using the `ibmcloud cr va` command.
    ```
    {: screen}

    The Vulnerability Advisor verdict is subject to any [exemption policies](/docs/Registry?topic=va-va_index#va_managing_policy) that you create. If you want to use an image that Vulnerability Advisor considers vulnerable, you can exempt one or more vulnerabilities so that Vulnerability Advisor doesn't consider them in its verdict. You can see whether an issue is exempted by looking at the `Policy Status` column in the output of the `ibmcloud cr va` command, and you can also list your exemptions by running the [`ibmcloud cr exemption-list`](/docs/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_exemption_list) command.
    {: note}

### Resolve vulnerabilities in your image
{: #registry_tutorial_workflow_resolve_vulnerabilities}

Vulnerability Advisor provides steps to resolve each vulnerability that is present in an image. The steps are displayed in the `How To Resolve` column in the output of the `ibmcloud cr va` command. If you follow the steps, you can resolve the issues in your image.

Because CVEs are frequently discovered and patched, this Dockerfile includes a contrived vulnerability that is introduced by rolling a package back to a known vulnerable version. Therefore, to fix the vulnerability, you can comment out the line that rolls back `apt`.

1. To prevent `apt` from being rolled back, comment out the following line in `Dockerfile-vulnerable` by putting a number sign (`#`) at the beginning of the line as shown here:

    ```txt
    # RUN apt-get install --allow-downgrades -y apt=1.4.8
    ```
    {: pre}

2. Build and push the image again:
    1. Build the image again by running the following command:

        ```txt
        docker build -t us.icr.io/<my_namespace>/hello-world:2 -f Dockerfile-vulnerable .
        ```
        {: pre}

    2. Push the image again by running the following command:

        ```txt
        docker push us.icr.io/<my_namespace>/hello-world:2
        ```
        {: pre}

3. Wait for the scan to complete and then run the following command to ensure that no issues are present in the image:

    ```txt
    ibmcloud cr images
    ```
    {: pre}

4. To patch the deployment, run the following command:

    ```txt
    kubectl apply -f hello-world.yaml
    ```
    {: pre}

5. Wait for the deployment to complete. To check whether the deployment is complete, run the following command:

    ```txt
    kubectl rollout status deployment hello-world
    ```
    {: pre}

    This deployment succeeds, and you can access your service and see "Hello, world!" displayed.

6. Delete the deployment and the service before proceeding:

    ```txt
    kubectl delete -f hello-world.yaml
    ```
    {: pre}

## Deploying to nondefault Kubernetes namespaces
{: #registry_tutorial_workflow_deploy_nondefault_namespaces}
{: step}

An {{site.data.keyword.containerlong_notm}} cluster can automatically pull images from {{site.data.keyword.registrylong_notm}} to the `default` Kubernetes namespace. However, if you want to deploy to namespaces other than `default`, you must take extra steps.

Kubernetes and {{site.data.keyword.registrylong_notm}} namespaces are different. For more information about {{site.data.keyword.registrylong_notm}} namespaces, see [Registry namespace](/docs/Registry?topic=Registry-registry_overview#overview_elements_namespace). For more information about Kubernetes namespaces, see [Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/){: external}.
{: tip}

1. In your cluster, create a Kubernetes namespace called `test`:

    ```txt
    kubectl create namespace test
    ```
    {: pre}

2. To deploy your deployment and service into this Kubernetes namespace, in the `hello-world.yaml` file change the `metadata.namespace` fields for both the deployment and the service from `default` to `test`. This snippet shows the `metadata.namespace` field in context:

    ```txt
    metadata:
        name: hello-world
        namespace: test
    ```
    {: codeblock}

3. Apply the configuration.

    1. Apply the configuration with Portieris that is still enabled in your cluster by running the following command:

        ```txt
        kubectl apply -f hello-world.yaml
        ```
        {: pre}

        Because Portieris is still enabled in your cluster, your deployment fails immediately and you see the following message:

        ```txt
        Error from server: error when creating "hello-world.yaml": admission webhook
        "va.hooks.securityenforcement.admission.cloud.ibm.com" denied the request:
        Deny "us.icr.io/<my_namespace>/hello-world:2", no valid ImagePullSecret defined for us.icr.io
        ```
        {: screen}

        This error is because Portieris determines that this deployment can't succeed because the `test` namespace is unable to pull images from your {{site.data.keyword.registrylong_notm}} namespace. The `default` Kubernetes namespace in an {{site.data.keyword.containerlong_notm}} cluster comes preconfigured with [image pull secrets](/docs/containers?topic=containers-registry#cluster_registry_auth) to pull images from {{site.data.keyword.registrylong_notm}}. However, these secrets aren't present in your new namespace.

    2. Apply the configuration after Portieris is removed from your cluster.

        1. [Remove Portieris](/docs/Registry?topic=Registry-security_enforce_portieris#uninstall_portieris).
        2. Apply the configuration by running the following command:

            ```txt
            kubectl apply -f hello-world.yaml
            ```
            {: pre}

            The `kubectl apply` command completes successfully. However, when you inspect the deployment's [pod](x8461823){: term} by running the `kubectl describe pod <pod_name> -n test` command, where `<pod_name>` is the name of the pod, the events log indicates that the cluster isn't authorized to pull the image.
            
            You can find the pod name by running `kubectl get pod -n test`.
            {: tip}

4. You must [set up an image pull secret](/docs/containers?topic=containers-registry#other) in your namespace so that you can deploy containers to that namespace. Several options are available, but this tutorial follows the steps to [copy an image pull secret](/docs/containers?topic=containers-registry#copy_imagePullSecret) to the `test` namespace. Rather than copying all the `icr.io` secrets, you can copy the `us.icr.io` secret because your image is in that local registry. The following command copies the `default-us-icr-io` secret to the `test` namespace, giving it the name `test-us-icr-io`:

    ```txt
    kubectl get secret default-us-icr-io -o yaml | sed 's/default/test/g' | kubectl -n test create -f -
    ```
    {: pre}

5. Two options are available to [use the image pull secret](/docs/containers?topic=containers-registry#use_imagePullSecret). This tutorial uses the option to refer to the image pull secret in the deployment `.yaml` file by populating the `spec.imagePullSecrets` field. The following snippet shows the required lines in context; you must add the final two lines:

    ```txt
    spec:
        containers:
        - name: hello-world
        image: us.icr.io/<my_namespace>/hello-world:1
        imagePullPolicy: Always
        imagePullSecrets:
        - name: test-us-icr-io
    ```
    {: codeblock}

6. Delete your deployment and reapply the configuration:
    1. Delete your deployment by running the following command:

        ```txt
        kubectl delete -f hello-world.yaml
        ```
        {: pre}

    2. Reapply the configuration by running the following command:

        ```txt
        kubectl apply -f hello-world.yaml
        ```
        {: pre}

    This time the command succeeds, and you can access your container by using a `curl` command or a web browser.


