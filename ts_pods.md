---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, pods won't restart, workers down, pods, workers

subcollection: Registry

content-type: troubleshoot

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:term: .term}
{:external: target="_blank" .external}
{:troubleshoot: data-hd-content-type='troubleshoot'}

# Why don't my pods restart after all my workers have been down?
{: #troubleshoot-pods}
{: troubleshoot}
{: support}

Pods do not restart after your cluster workers have been down.
{: shortdesc}

With effect from 19 November 2020, Container Image Security Enforcement is deprecated. To enforce container image security use [Portieris](https://github.com/IBM/portieris){: external}.
{: deprecated}

{: tsSymptoms}
Container Image Security Enforcement is deployed. The cluster workers are showing as working correctly, but nothing is scheduled.

{: tsCauses}
By default, Container Image Security Enforcement adds a fail closed admission webhook. If all Container Image Security Enforcement pods are down, the pods are not available to approve their own recovery.

{: tsResolve}
To recover the cluster when it's in this state, you must change the webhook configuration to make it fail open instead of closed.

You must have sufficient role-based access control (RBAC) privileges to use the following verbs:

- `GET`
- `PATCH`

On these resources:

- `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
- `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration`

For more information about RBAC, see [Assigning RBAC permissions](/docs/containers?topic=containers-users#role-binding) and [Kubernetes - Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/){: external}.

Complete the following steps to change the webhook configuration to make it fail open instead of closed, and then, when at least one Container Image Security Enforcement pod is running, restore the webhook configuration so that it fails closed:

1. Update `MutatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Change `failurePolicy` to `Ignore`, save, and close.

2. Update `ValidatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Change `failurePolicy` to `Ignore`, save, and close.

3. Wait for some Container Image Security Enforcement pods to start. You can check whether the pods have started by running the following command until you see the **STATUS** column for at least one pod is displaying `Running`:

   ```
   kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
   ```
   {: pre}

4. When at least one Container Image Security Enforcement pod is running, update `MutatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit MutatingWebhookConfiguration image-admission-config
   ```
   {: pre}

    Change `failurePolicy` to `Fail`, save, and close.

5. Update `ValidatingWebhookConfiguration` by running the following command:

   ```
   kubectl edit ValidatingWebhookConfiguration image-admission-config
   ```
   {: pre}

   Change `failurePolicy` to `Fail`, save, and close.
