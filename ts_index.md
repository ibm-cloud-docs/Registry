---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-21"

keywords: troubleshooting, support, help, error messages, problem, registry, support ticket, ticket

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting {{site.data.keyword.registryshort_notm}}
{: #ts_index}
{: troubleshoot}
{: support}

Answers to common troubleshooting questions about how to use {{site.data.keyword.registrylong}}.
{: shortdesc}

## Troubleshooting topics
{: #gettinghelp_ts}

The following troubleshooting topics are available to help you:

### Troubleshooting CLI login
{: #gettinghelp_ts_cli_login}

Troubleshoot logging in problems.

- [Why can't I log in to {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-login)
- [Why does the {{site.data.keyword.registryshort}} login keep expiring?](/docs/Registry?topic=Registry-troubleshoot-login-expire)
- [Why can't I get started with {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-get-started)
- [Why do {{site.data.keyword.registryshort}} commands fail saying they’re not registered?](/docs/Registry?topic=Registry-troubleshoot-login-error)
- [macOS]{: tag-macos} [Why is `docker login` on my Mac failing when I use {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-docker-mac)

### Troubleshooting pull and push errors
{: #gettinghelp_ts_pull_push}

Troubleshoot pull and push problems.

- [Why can't I push or pull a Docker image when I use {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-push-pull-docker)
- [Why is pulling images in {{site.data.keyword.registryshort}} so slow?](/docs/Registry?topic=Registry-troubleshoot-pull-performance)
- [Why am I getting `Authorization required` errors in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-auth-req)
    - [Why am I getting an `Unauthorized` error when I use {{site.data.keyword.codeengineshort}} with {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-unauthorized-ce)
    - [Why have I got a problem when I pull an image with `cosign` when I use Podman in {{site.data.keyword.registryshort_notm}}?](/docs/Registry?topic=Registry-troubleshoot-cosign-podman)
- [Why am I getting `Access denied` errors in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-access-denied)
    - [Why am I getting errors for a resource in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-resource)
    - [Why am I getting errors about insufficient scope in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-scope)
    - [Why am I getting errors about my quota in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-quota)
    - [Why am I getting errors about using a private network in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-private)
    - [Why am I getting a `Forbidden` when I try to access {{site.data.keyword.registryshort}} when I'm using {{site.data.keyword.codeengineshort}}?](/docs/Registry?topic=Registry-troubleshoot-forbidden-ce)
    - [Why do images fail to pull from registry with ImagePullBackOff or authorization errors?](/docs/Registry?topic=Registry-ts-app-image-pull)

### Troubleshooting CLI commands
{: #gettinghelp_ts_cli_commands}

Troubleshoot CLI command problems.

- [Why can't I add a namespace in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-add-namespace)
- [Why aren't I authorized to access a specified resource in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-namespace-auth)
- [Why can't I find my image or my namespace in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-image-find)
- [Why don't all my namespaces show in the resource list in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-namespace-resource-list)
- [Why does it time out when I list images in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-image-timeout)
- [Why can't I pull the newest image by using the `latest` tag in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-docker-latest)
- [Why do all the tags get deleted when I delete an image in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-image-rm)
- [Why doesn't the retention command show all the images in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-image-list-retention)
- [Why do I get an error when I'm restoring an image in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-image-restore)
- [Why aren't all the tags restored when I restore by digest in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-image-restore-digest)
- [Why do I get a manifest unknown error in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-manifest-unknown)
- [Why do I get a manifest type error when I tag my image in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-type)
- [Why do I get a manifest version error in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-version)
- [Why do I get a manifest list invalid error in {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-manifest-list-error)
- [Why do I get an error about an invalid version of Vulnerability Advisor being specified?](/docs/Registry?topic=Registry-troubleshoot-va-version-error)

### Troubleshooting networking
{: #gettinghelp_ts_network}

Troubleshoot networking problems.

- [Why can't I access {{site.data.keyword.registryshort}} through a custom firewall?](/docs/Registry?topic=Registry-troubleshoot-firewall)
- [Why can't I connect to {{site.data.keyword.registryshort_notm}}?](/docs/Registry?topic=Registry-troubleshoot-connect)

### Troubleshooting Portieris
{: #gettinghelp_ts_portieris}

Troubleshoot Portieris problems.

- [Why don't my pods restart after my workers are down when I use {{site.data.keyword.registryshort}}?](/docs/Registry?topic=Registry-troubleshoot-pods)
