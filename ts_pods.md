---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-06"

keywords: troubleshooting, support, help, errors, problems, ts, registry, pods don't restart, workers down, pods, workers

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why don't my pods restart after my workers were down?
{: #troubleshoot-pods}
{: troubleshoot}
{: support}

Pods do not restart after your cluster workers were down.
{: shortdesc}

Portieris is deployed. The cluster workers are showing as working correctly, but nothing is scheduled.
{: tsSymptoms}

By default, Portieris adds a fail closed admission webhook. If all Portieris pods are down, the pods are not available to approve their own recovery.
{: tsCauses}

To recover the cluster when it's in this state, you must change the webhook configuration to make it fail open instead of closed.
{: tsResolve}

You must have sufficient role-based access control (RBAC) privileges to use the `GET` and `PATCH` verbs on the following resources:

- `admissionregistration.k8s.io/v1/MutatingWebhookConfiguration`
- `admissionregistration.k8s.io/v1/ValidatingWebhookConfiguration`

For more information about RBAC, see [Understanding RBAC permissions](/docs/containers?topic=containers-users#understand-rbac), [Creating custom RBAC permissions for users, groups, or service accounts](/docs/containers?topic=containers-users#rbac), and [Kubernetes - Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/){: external}.

To change the webhook configuration so that it fails open, and then, when at least one Portieris pod is running, restore the webhook configuration so that it fails closed, complete the following steps:

1. Update `MutatingWebhookConfiguration` by running the following command.

    ```sh
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Ignore`, save, and close.

2. Update `ValidatingWebhookConfiguration` by running the following command.

    ```sh
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Ignore`, save, and close.

3. Wait for some Portieris pods to start. If you want to check when the pods start, run the following command until you see the **STATUS** column for at least one pod is displaying `Running`:

    ```sh
    kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
    ```
    {: pre}

4. When at least one Portieris pod is running, update `MutatingWebhookConfiguration` by running the following command.

    ```sh
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Fail`, save, and close.

5. Update `ValidatingWebhookConfiguration` by running the following command.

    ```sh
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Fail`, save, and close.


