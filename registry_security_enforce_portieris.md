---

copyright:
  years: 2021, 2023
lastupdated: "2023-04-13"

keywords: Portieris, image security, Portieris policies, installing Portieris, security, removing Portieris, policies, cluster

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# Enforcing container image security by using Portieris
{: #security_enforce_portieris}

You can use [Portieris](https://github.com/IBM/portieris){: external} to enforce image security policies in {{site.data.keyword.registrylong}}.
{: shortdesc}

Portieris is a Kubernetes admission controller that verifies your container images before you deploy them to your cluster in {{site.data.keyword.containerlong_notm}}.

You can use Portieris to enforce policies on image signatures and on vulnerabilities that are detected by Vulnerability Advisor. If an image doesn't meet your policy requirements, the resource that contains the pod is not deployed to your cluster.

If Portieris is deployed and the cluster workers are showing as working correctly, but nothing is scheduled, see [Why don't my pods restart after my workers were down?](/docs/Registry?topic=Registry-troubleshoot-pods) for assistance.
{: tip}

Portieris is supported on {{site.data.keyword.redhat_openshift_full}}.

## Installing Portieris in your cluster
{: #sec_enforce_install_portieris}

Install Portieris in your cluster.

To install Portieris in your {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster, see [Enabling image security enforcement in your cluster](/docs/containers?topic=containers-images#portieris-image-sec). If you use this installation, it is deployed and maintained for you and it runs in the control plane, which gives higher availability.

If you prefer to install Portieris directly, or you're not using {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}}, see [Installing Portieris](https://github.com/IBM/portieris#installing-portieris){: external}.

## Portieris policies
{: #policies_portieris}

Portieris has two types of policy. Image policy resources and cluster image policy resources. You can override the default Portieris policies.

For more information about Portieris policies, see [Portieris policies](https://github.com/IBM/portieris/blob/main/POLICIES.md){: external}.

## Uninstalling Portieris
{: #uninstall_portieris}

How to uninstall Portieris.

[Uninstall Portieris](https://github.com/IBM/portieris#uninstalling-portieris){: external}.
