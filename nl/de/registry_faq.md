---

copyright:
  years: 2018, 
lastupdated: "2018-09-03"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Häufig gestellte Fragen (FAQs)
{: #registry_faq}


## Wie liste ich öffentliche Images auf?
{: #faq_list_public_images}

Um öffentliche Images aufzulisten, können Sie die folgenden `ibmcloud`-Befehle ausführen, mit denen Sie die globale Registry als Ziel verwenden und die von IBM bereitgestellten öffentlichen Images auflisten können: 

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}


## Kann ich Tools verwenden, die nicht von Docker bereitgestellt werden, um meine Images zu generieren und sie mit einer Push-Operation in der Registry zu speichern? 
{: #faq_tools}

Ja, sofern diese Tools das OCI-Bildformat und das OCI-Protokoll unterstützen. 
