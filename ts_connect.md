---

copyright:
  years: 2023, 2025
lastupdated: "2025-10-14"

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

- **Scenario A.** Firewall or Calico rules are in place.
- **Scenario B.** The connection to {{site.data.keyword.registryshort_notm}} is through a proxy.
- **Scenario C.** IP allowlists are configured.
- **Scenario D.** Context-based restrictions are configured.

You can fix this problem in the following ways:
{: tsResolve}

- **Scenario A.** Check your [firewall](/docs/Registry?topic=Registry-troubleshoot-firewall) or [Calico](https://www.tigera.io/project-calico/){: external} rules.
- **Scenario B.** Connect to {{site.data.keyword.registryshort_notm}} without a proxy.
- **Scenario C.** Use IP addresses that are in your allowlist.
- **Scenario D.** Ensure that your [context-based restrictions](/docs/Registry?topic=Registry-registry-cbr&interface=ui) give you access to {{site.data.keyword.registryshort_notm}}.
