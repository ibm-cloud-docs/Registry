---

copyright:
  years: 2017, 2021
lastupdated: "2021-08-18"

keywords: troubleshooting, support, help, errors, problems, ts, registry, pods don't restart, workers down, pods, workers

subcollection: Registry

content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Why don't my pods restart after my workers were down?
{: #troubleshoot-pods}
{: troubleshoot}
{: support}

Pods do not restart after your cluster workers were down.
{: shortdesc}

With effect from 19 November 2020, Container Image Security Enforcement is deprecated. To enforce container image security, use [Portieris](https://github.com/IBM/portieris){: external}.
{: deprecated}

Container Image Security Enforcement is deployed. The cluster workers are showing as working correctly, but nothing is scheduled.
{: tsSymptoms}

By default, Container Image Security Enforcement adds a fail closed admission webhook. If all Container Image Security Enforcement pods are down, the pods are not available to approve their own recovery.
{: tsCauses}

To recover the cluster when it's in this state, you must change the webhook configuration to make it fail open instead of closed.
{: tsResolve}

You must have sufficient role-based access control (RBAC) privileges to use the `GET` and `PATCH` verbs on the following resources:

- `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
- `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration`

For more information about RBAC, see [Understanding RBAC permissions](/docs/containers?topic=containers-users#understand-rbac), [Creating custom RBAC permissions for users, groups, or service accounts](/docs/containers?topic=containers-users#rbac), and [Kubernetes - Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/){: external}.

To change the webhook configuration so that it fails open, and then, when at least one Container Image Security Enforcement pod is running, restore the webhook configuration so that it fails closed, complete the following steps:

1. Update `MutatingWebhookConfiguration` by running the following command.

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Ignore`, save, and close.

2. Update `ValidatingWebhookConfiguration` by running the following command.

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Ignore`, save, and close.

3. Wait for some Container Image Security Enforcement pods to start. If you want to check when the pods start, run the following command until you see the **STATUS** column for at least one pod is displaying `Running`:

    ```
    kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
    ```
    {: pre}

4. When at least one Container Image Security Enforcement pod is running, update `MutatingWebhookConfiguration` by running the following command.

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Fail`, save, and close.

5. Update `ValidatingWebhookConfiguration` by running the following command.

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Change `failurePolicy` to `Fail`, save, and close.


