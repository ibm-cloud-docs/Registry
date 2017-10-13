---

copyright:
  years: 2017
lastupdated: "2017-10-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# Troubleshooting
{: #ts_index}

Here are the answers to common troubleshooting questions about using {{site.data.keyword.registrylong}}.
{:shortdesc}


## Getting help and support for {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

If you have problems or questions when you are using {{site.data.keyword.registrylong_notm}}, you can get help by searching for information or by asking questions through a forum. You can also open a {{site.data.keyword.Bluemix_notm}} support ticket.

When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.registrylong_notm}} development team.

-   If you have technical questions about developing or deploying an app with {{site.data.keyword.registrylong_notm}}, post your question on [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) and tag your question with `ibm-bluemix` and `container-registry`.
-   For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) forum. Include the `bluemix` and `container-registry` tags.

See [Getting help](../../support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](../../support/index.html#contacting-support).

## Logging in to {{site.data.keyword.registrylong_notm}} fails
{: #ts_login}

You cannot log in to {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
The `bx cr login` command fails.

{: tsCauses}
-   The container-registry plug-in is out of date and needs updating.
-   Docker is not installed on your local machine, or is not running.
-   Your {{site.data.keyword.Bluemix_notm}} login credentials have expired.

{: tsResolve}
You can fix this problem in the following ways:

-   Upgrade to the most recent version of the {{site.data.keyword.registryshort_notm}} plug-in, see [Updating the {{site.data.keyword.registrylong_notm}} (`bx cr`) plug-in](registry_setup_cli_namespace.html#registry_cli_update).
-   Ensure that Docker is installed on your machine. If it is already installed, restart the Docker daemon.
-   Rerun the `bx login` command to refresh your {{site.data.keyword.Bluemix_notm}} login credentials.

## Setting up a namespace fails
{: #ts_problem}

{: tsSymptoms}
When you run `bx cr namespace-add`, you are unable to set your entered value as the namespace.

{: tsCauses}
-   You entered a namespace value that is already being used by another {{site.data.keyword.Bluemix_notm}} organization.
-   A namespace was recently deleted and you are reusing its name. If the namespace that was deleted contained many resources, the deletion might not yet be fully processed by {{site.data.keyword.registrylong_notm}}.
-   You used invalid characters in the namespace value.

{: tsResolve}
You can fix this problem in the following ways:

-   Follow any instructions that appear in the returned error message.
-   Check that you entered a valid namespace:
    -   Your namespace must be 4 - 30 characters long.
    -   Your namespace must start with at least one letter or number.
    -   Your namespace must contain lowercase letters, numbers, or underscores (_) only.
-   Choose a different value for your namespace.
-   If you are re-creating a namespace that was deleted, and it contained many images, try again later.

## Push or pull of a Docker image fails
{: #ts_pushpull}

{: tsSymptoms}
When you run commands to push or pull Docker images, you receive an error message. The error message varies depending on the root cause. Potential error messages might be:

```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan
```
{: screen}

```
You have exceeded your pull traffic quota for the current month. Review your pull traffic quota and pricing plan
```
{: screen}

```
unauthorized: authentication required
```
{: screen}

```
denied: requested access to the resource is denied
```
{: screen}

{: tsCauses}
-   Docker is not installed.
-   The Docker client is not logged in to {{site.data.keyword.registrylong_notm}}.
-   Your {{site.data.keyword.Bluemix_notm}} access token might have expired.
-   You exceeded the quota limit for storage or pull traffic that is set for your {{site.data.keyword.Bluemix_notm}} account.

{: tsResolve}
You can fix this problem in the following ways:

-   [Ensure that Docker is installed on your machine](index.html#registry_cli_install).
-   Check your Docker installation path.
-   Log in to {{site.data.keyword.Bluemix_notm}} by running `bx login`. Then, log in to the {{site.data.keyword.registrylong_notm}} CLI by running `bx cr login`.
-   [Review quota limits and usage for storing and pulling Docker images in {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).

## Unable to pull the latest image using the latest tag
{: #ts_docker_latest}

{: tsSymptoms}
You are trying to run the command `docker pull`, but it returned a version of your image that is not the latest version built.

{: tsCauses}
The `latest` tag is applied by default to reference an image when you run Docker commands without specifying the tag value. The `latest` tag is applied to the latest `docker build` or `docker tag` command that was run without a tag value explicitly set. Therefore, it's possible to run `docker` commands out-of-order or to explicitly set tags on some images, and the `latest` tag to refer to a build which is not the most recent.

{: tsResolve}
It is generally better to explicitly define a different sequential tag for your images every time, and not rely on the `latest` tag.

## Accessing the registry with a custom firewall fails
{: #ts_firewall}

{: tsSymptoms}
You set up an additional firewall in your development environment with custom settings for inbound and outbound network traffic. When trying to access {{site.data.keyword.registrylong_notm}}, the connection fails.

{: tsCauses}
Your custom firewall requires certain network groups to be opened for inbound and outbound network traffic to allow communication to and from the registry.

{: tsResolve}
Open the following network groups in your customized firewall.

1.  Note the public IP address of the machine that you want to use to connect to {{site.data.keyword.registrylong_notm}}. If you are using Kubernetes, use the public IP address of your worker node. Retrieve the public IP address of your worker node by running `bx cs workers <cluster_name_or_id>`, where *&lt;cluster_name_or_id&gt;* is the name or ID of your cluster.
2.  In your firewall, allow the following connections to and from your machine:
    -   For INBOUND connectivity to your machine, allow incoming network traffic from the following source network groups to the destination public IP address of your machine.

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   For OUTBOUND connectivity from your machine, use the same network groups and allow outgoing network traffic from the source public IP address of your machine to these network groups.

