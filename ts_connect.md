---

copyright:
  years: 2023
lastupdated: "2023-02-07"

keywords: registry, connect, firewall, proxy

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I connect to {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-connect}
{: troubleshoot}
{: support}

You are unable to connect to {{site.data.keyword.registrylong}} and you get the message `connection reset`.
{: shortdesc}

You can't connect to {{site.data.keyword.registrylong_notm}} and you receive the following message: `connection reset`.
{: tsSymptoms}

The following alternatives are possible causes:
{: tsCauses}

- Firewall or Calico rules are in place.
- The connection to {{site.data.keyword.registryshort_notm}} is through a proxy.
- IP allowlists are configured.
- Context-based restrictions are configured.

You can fix this problem in the following ways:
{: tsResolve}

- Check your [firewall](/docs/Registry?topic=Registry-troubleshoot-firewall&interface=ui) or [Calico](https://projectcalico.docs.tigera.io/about/about-calico){: external} rules.
- Connect to {{site.data.keyword.registryshort_notm}} without a proxy.
- Use IP addresses that are in your allowlist.
- Ensure that your [context-based restrictions](/docs/Registry?topic=Registry-iam&interface=ui#iam_cbr) give you access to {{site.data.keyword.registryshort_notm}}.
