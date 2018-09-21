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


# FAQ (Foire aux questions)
{: #registry_faq}


## Comment établir la liste des images publiques ?
{: #faq_list_public_images}

Pour répertorier les images publiques, exécutez la commande `ibmcloud` suivante de manière à cibler la base de registre globale et à répertorier les images publiques fournies par IBM :

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}


## Puis-je utiliser des outils non Docker pour générer mes images et les envoyer (push) au registre ?
{: #faq_tools}

Oui, sous réserve que l'outil prenne en charge le protocole et le format d'image OCI.
