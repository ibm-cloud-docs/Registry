---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-16"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, 

subcollection: registry

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
{:faq: data-hd-content-type='faq'}

# Frequently asked questions (FAQs)
{: #registry_faq}

Frequently asked questions about {{site.data.keyword.registrylong}}.
{: shortdesc}

## How do I list public images?
{: #faq_list_public_images}
{: faq}

To list public images, run the following `ibmcloud` commands to target the global registry and list the IBM-provided public images:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Can I use non-docker tools to build my images and push them to the registry?
{: #faq_tools}
{: faq}

Yes, provided that the tool supports OCI image format and protocol.
