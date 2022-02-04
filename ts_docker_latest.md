---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-10"

keywords: troubleshooting, support, help, errors, problems, ts, registry, pulling the latest Docker image fails, docker pull, latest

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I pull the most recent image by using the `latest` tag?
{: #troubleshoot-docker-latest}
{: troubleshoot}
{: support}

You're unable to pull the most recent image by using the `latest` tag in {{site.data.keyword.registrylong}}.
{: shortdesc}

You are trying to run the command `docker pull`, but it returned a version of your image that is not the most recent version built.
{: tsSymptoms}

The `latest` tag is applied by default to reference an image when you run Docker commands without specifying the tag value. The `latest` tag is applied to the most recent `docker build` or `docker tag` command that was run without a tag value explicitly set. Therefore, it's possible to run `docker` commands out of order or to explicitly set tags on some images. Both scenarios cause the `latest` tag to refer to a build that isn't the most recent.
{: tsCauses}

It is generally better to explicitly define a different sequential tag for your images every time, and not rely on the `latest` tag.
{: tsResolve}


