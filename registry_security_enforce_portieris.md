---

copyright:
  years: 2021
lastupdated: "2021-08-18"

keywords: Portieris, container image security, Portieris policies, installing Portieris, security, security enforcement, removing Portieris, uninstalling Portieris

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

# Enforcing container image security by using Portieris
{: #security_enforce_portieris}

You can use [Portieris](https://github.com/IBM/portieris){: external} to enforce image security policies. Portieris is a Kubernetes admission controller that verifies your container images before you deploy them to your cluster in {{site.data.keyword.containerlong}}.
{: shortdesc}

You can use Portieris to enforce policies on image signatures and on vulnerabilities that are detected by Vulnerability Advisor. If an image doesn't meet your policy requirements, the resource that contains the pod is not deployed to your cluster.

Portieris is supported on OpenShift.

## Installing Portieris in your cluster
{: #sec_enforce_install_portieris}

Install Portieris in your cluster.
{: shortdesc}

To install Portieris in your {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong}} cluster, see [Enabling image security enforcement in your cluster](/docs/containers?topic=containers-images#portieris-image-sec). If you use this installation, it is deployed and maintained for you and it runs in the control plane, which gives higher availability.

If you prefer to install Portieris directly, or you're not using {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}}, see [Installing Portieris](https://github.com/IBM/portieris#installing-portieris){: external}.

## Policies
{: #policies_portieris}

Portieris has two types of policy. Image policy resources and cluster image policy resources. You can override the default Portieris policies.
{: shortdesc}

For more information about Portieris policies, see [Portieris policies](https://github.com/IBM/portieris/blob/master/POLICIES.md){: external}.

## Uninstalling Portieris
{: #uninstall_portieris}

How to uninstall Portieris.
{: shortdesc}

To uninstall Portieris, see [Uninstalling Portieris](https://github.com/IBM/portieris#uninstalling-portieris){: external}.


