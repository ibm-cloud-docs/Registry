---

copyright:
  years: 2017, 2025
lastupdated: "2025-10-14"

keywords: docker, latest, image, tag, latest tag, most recent

subcollection: Registry

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I pull the newest image by using the `latest` tag in {{site.data.keyword.registryshort_notm}}?
{: #troubleshoot-docker-latest}
{: troubleshoot}
{: support}

You're unable to pull the most recent image by using the `latest` [tag](#x2040924){: term} in {{site.data.keyword.registrylong}}.
{: shortdesc}

You're trying to run the command `docker pull`, but it returned a version of your image that isn't the most recent version built.
{: tsSymptoms}

The `latest` tag is applied by default to reference an image when you run Docker commands without specifying the tag value. The `latest` tag is applied to the most recent `docker build` or `docker tag` command that was run without a tag value explicitly set. Therefore, it's possible to run `docker` commands out of order or to explicitly set tags on some images. Both scenarios cause the `latest` tag to refer to a build that isn't the most recent. For more information about Docker tags, see [docker image tag](https://docs.docker.com/reference/cli/docker/image/tag/){: externa}.
{: tsCauses}

It is generally better to explicitly define a different sequential tag for your images every time, and not rely on the `latest` tag.
{: tsResolve}
