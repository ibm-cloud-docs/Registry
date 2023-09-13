---

copyright:
  years: 2017, 2023
lastupdated: "2023-09-12"

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
- [Why do commands fail saying that I'm not logged in?](/docs/Registry?topic=Registry-troubleshoot-login-cloud)
- [Why do `cr` commands fail saying they’re not registered?](/docs/Registry?topic=Registry-troubleshoot-login-error)
- [macOS]{: tag-macos} [Why is Docker login on my Mac failing?](/docs/Registry?topic=Registry-troubleshoot-docker-mac)

### Troubleshooting pull and push errors
{: #gettinghelp_ts_pull_push}

Troubleshoot pull and push problems.

- [Why can't I push or pull a Docker image?](/docs/Registry?topic=Registry-troubleshoot-push-pull-docker)
- [Why is pulling images so slow?](/docs/Registry?topic=Registry-troubleshoot-pull-performance)
- [Why am I getting `Authorization required` errors?](/docs/Registry?topic=Registry-troubleshoot-auth-req)
    - [Why am I getting an `Unauthorized` error when I'm using {{site.data.keyword.codeengineshort}}?](/docs/Registry?topic=Registry-troubleshoot-unauthorized-ce)
- [Why am I getting `Access denied` errors?](/docs/Registry?topic=Registry-troubleshoot-access-denied)
    - [Why am I getting `Access denied` errors for a resource?](/docs/Registry?topic=Registry-troubleshoot-resource)
    - [Why am I getting `Access denied` errors about insufficient scope?](/docs/Registry?topic=Registry-troubleshoot-scope)
    - [Why am I getting `Access denied` errors about my quota?](/docs/Registry?topic=Registry-troubleshoot-quota)
    - [Why am I getting `Access denied` errors over a private network?](/docs/Registry?topic=Registry-troubleshoot-private)
    - [Why am I getting a `Forbidden` error when I'm using {{site.data.keyword.codeengineshort}}?](/docs/Registry?topic=Registry-troubleshoot-forbidden-ce)
    - [Why do images fail to pull from registry with ImagePullBackOff or authorization errors?](/docs/Registry?topic=Registry-ts-app-image-pull)

### Troubleshooting CLI commands
{: #gettinghelp_ts_cli_commands}

Troubleshoot CLI command problems.

- [Why can't I add a namespace?](/docs/Registry?topic=Registry-troubleshoot-add-namespace)
- [When I create a namespace, why aren't I authorized to access the specified resource?](/docs/Registry?topic=Registry-troubleshoot-namespace-auth)
- [Why can't I find my image or my namespace?](/docs/Registry?topic=Registry-troubleshoot-image-find)
- [Why don't all my namespaces show in the Resource list?](/docs/Registry?topic=Registry-troubleshoot-namespace-resource-list)
- [Why is it timing out when I list images?](/docs/Registry?topic=Registry-troubleshoot-image-timeout)
- [Why can't I pull the newest image by using the `latest` tag?](/docs/Registry?topic=Registry-troubleshoot-docker-latest)
- [Why do all the tags get deleted when I delete an image?](/docs/Registry?topic=Registry-troubleshoot-image-rm)
- [Why doesn't the retention command show all the images?](/docs/Registry?topic=Registry-troubleshoot-image-list-retention)
- [Why do I get an error when I'm restoring an image?](/docs/Registry?topic=Registry-troubleshoot-image-restore)
- [Why aren't all the tags restored when I restore by digest?](/docs/Registry?topic=Registry-troubleshoot-image-restore-digest)
- [Why do I get a manifest unknown error?](/docs/Registry?topic=Registry-troubleshoot-manifest-unknown)
- [Why do I get a manifest type error when I tag my image?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-type)
- [Why do I get a manifest version error?](/docs/Registry?topic=Registry-troubleshoot-manifest-error-version)
- [Why do I get a manifest list invalid error?](/docs/Registry?topic=Registry-troubleshoot-manifest-list-error)

### Troubleshooting networking
{: #gettinghelp_ts_network}

Troubleshoot networking problems.

- [Why can't I access the registry through a custom firewall?](/docs/Registry?topic=Registry-troubleshoot-firewall)
- [Why can't I connect to {{site.data.keyword.registryshort_notm}}?](/docs/Registry?topic=Registry-troubleshoot-connect)

### Troubleshooting Portieris
{: #gettinghelp_ts_portieris}

Troubleshoot Portieris problems.

- [Why don't my pods restart after my workers were down?](/docs/Registry?topic=Registry-troubleshoot-pods)
