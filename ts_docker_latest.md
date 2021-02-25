---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-25"

keywords: troubleshooting, support, help, errors, problems, ts, registry, pulling the latest Docker image fails, docker pull, latest

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

# Why can't I pull the most recent image by using the `latest` tag?
{: #troubleshoot-docker-latest}
{: troubleshoot}
{: support}

You're unable to pull the most recent image by using the `latest` tag in {{site.data.keyword.registrylong}}.
{: shortdesc}

{: tsSymptoms}
You are trying to run the command `docker pull`, but it returned a version of your image that is not the most recent version built.

{: tsCauses}
The `latest` tag is applied by default to reference an image when you run Docker commands without specifying the tag value. The `latest` tag is applied to the most recent `docker build` or `docker tag` command that was run without a tag value explicitly set. Therefore, it's possible to run `docker` commands out of order or to explicitly set tags on some images, both of which cause the `latest` tag to refer to a build that is not the most recent.

{: tsResolve}
It is generally better to explicitly define a different sequential tag for your images every time, and not rely on the `latest` tag.
