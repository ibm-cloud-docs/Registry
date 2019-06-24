---

copyright:
  years: 2019
lastupdated: "2019-05-17"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# Notes sur l'édition
{: #registry_release_notes}

Utilisez ces notes sur l'édition pour prendre connaissance des modifications les plus récentes apportées à {{site.data.keyword.registrylong}} et Vulnerability Advisor. Les changements sont classés par date.
{:shortdesc}

## 13 mai 2019
{: #13may2019}

- **Fin du support pour Container Scanner**

  Container Scanner est obsolète et n'est plus utilisable.

  Pour plus d'informations, voir [Installation de Container Scanner (obsolète)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).

## 2 avril 2019
{: #2apr2019}

- **Disponibilité générale de Container Image Security Enforcement**

  Utilisez Container Image Security Enforcement pour vérifier vos images de conteneur avant de les déployer sur votre cluster dans {{site.data.keyword.containerlong_notm}}. Vous pouvez contrôler l'emplacement depuis lequel les images sont déployées, mettre en application des règles Vulnerability Advisor et vous assurer que la [sécurité du contenu](/docs/services/Registry?topic=registry-registry_trustedcontent) est correctement appliquée à l'image.

  Pour plus d'informations, voir [Mise en application de la sécurité des images de conteneur](/docs/services/Registry?topic=registry-security_enforce#security_enforce).

## 14 mars 2019
{: #14mar2019}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} disponible pour {{site.data.keyword.registrylong_notm}}**

  Utilisez le service {{site.data.keyword.cloudaccesstraillong_notm}} pour savoir comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.registrylong_notm}} dans {{site.data.keyword.cloud}}.

  Pour plus d'informations, voir [Evénements Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).

## 25 février 2019
{: #25feb2019}

- **Nouveaux noms DNS**

  {{site.data.keyword.registrylong_notm}} adopte de nouveaux noms de domaine. Les nouveaux noms de domaine sont disponibles sur la console et sur l'interface de ligne de commande. Vous pouvez utiliser les nouveaux noms de domaine `icr.io` dès maintenant. Les noms de domaine `registry.bluemix.net` existants sont obsolètes, mais vous pouvez toujours les utiliser pour l'instant ; la date de fin de prise en charge de ces noms vous sera communiquée ultérieurement. Pour plus d'informations, voir [Régions](/docs/services/Registry?topic=registry-registry_overview#registry_regions) et [Introducing New IBM Cloud Container Registry Domain Names ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  Si vous utilisez du content approuvé, les signatures s'appliquant à l'ensemble du nom d'image, y compris le nom de domaine, vous devez ajouter de nouvelles signatures afin de pouvoir consommer du contenu approuvé sous le nouveau nom de domaine. Pour plus d'informations sur la signature d'images, voir [Signature d'images pour du contenu sécurisé](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).

- **La clé d'API IAM extrait les secrets pour les clusters {{site.data.keyword.containerlong_notm}}**

  La nouvelle image de cluster extrait les secrets pour les domaines `icr.io` autorisés en utilisant une clé d'API IAM. De ce fait, si vous souhaitez davantage de contrôle sur l'accès à vos ressources {{site.data.keyword.registrylong_notm}}, vous pouvez ajouter des règles IAM. Vous pouvez, par exemple, changer les règles de clé d'API concernant l'extraction du secret du cluster afin que les images soient extraites uniquement à partir d'une région ou d'un espace de noms particulier du registre.
  
  Pour plus d'informations, voir [Comment votre cluster est-il autorisé à extraire des images d'{{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).

- **Nouvelle région dans ap-north**

  Une nouvelle région est disponible dans `ap-north`. Vous pouvez utiliser la nouvelle région via le nom de domaine `jp.icr.io`.
  
  Pour plus d'informations, voir
[Régions](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## 21 février 2019
{: #21feb2019}

- **Automatisation de l'accès à vos espaces de nom**

  L'utilisation de jetons pour automatiser l'envoi et l'extraction d'images Docker vers et depuis vos espaces de nom est déprécié. Vous devez désormais utiliser des clés d'API pour automatiser l'accès à vos espaces de nom {{site.data.keyword.registrylong_notm}} pour pouvoir y transférer ou en extraire des images.

  Pour plus d'informations, voir [Automatisation de l'accès à vos espaces de nom à l'aide de clés d'API](/docs/services/Registry?topic=registry-registry_access#registry_api_key).

## 8 janvier 2019
{: #8jan2019}

- **Fin du support pour l'API Vulnerability Advisor version 2**

  La version 2 de l'API Vulnerability Advisor est obsolète et n'est plus utilisable. Servez-vous de la version 3 de l'API. Voir [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/container-registry/va).

  Pour plus d'informations, voir [Vulnerability Advisor v2 API Deprecation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2018/12/vulnerability-advisor-v2-api-deprecation/).

## 4 octobre 2018
{: #4oct2018}

- **Gestion des accès utilisateur**

  Utilisez {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) pour contrôler l'accès des utilisateurs à votre compte sur {{site.data.keyword.registrylong_notm}}. Lorsque des règles IAM sont activées pour votre compte dans {{site.data.keyword.registrylong_notm}}, chaque utilisateur qui accède au service {{site.data.keyword.registrylong_notm}} dans votre compte doit se voir affecter une règle d'accès avec un rôle utilisateur IAM défini. Cette règle détermine le rôle de l'utilisateur dans le contexte du service, ainsi que les actions qu'il peut exécuter.

  Pour plus d'informations, voir [Gestion des accès utilisateur à l'aide d'{{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam), [Définition de règles de rôle d'accès utilisateur](/docs/services/Registry?topic=registry-user#user) et [Tutoriel : Accorder l'accès à des ressources IBM Cloud Container Registry](/docs/services/Registry?topic=registry-iam_access#iam_access).

## 7 août 2018
{: #7aug2018}

- **Règles d'exemption dispense disponibles dans Vulnerability Advisor**

  Si vous souhaitez gérer la sécurité d'une organisation {{site.data.keyword.cloud_notm}}, vous pouvez utiliser votre paramètre de règle pour déterminer si un problème est exempt ou non. Vous pouvez décider d'utiliser Container Image Security Enforcement pour garantir que le déploiement n'est permis qu'à partir d'images ne présentant pas de problèmes de sécurité une fois que ceux exemptés par votre règle ont été pris en compte.

  Pour plus d'informations, voir [Définition de règles d'exemption organisationnelles](/docs/services/Registry?topic=va-va_index#va_managing_policy).

## 25 juillet 2018
{: #25jul2018}

- **{{site.data.keyword.cloudaccesstrailfull_notm}} disponible pour Vulnerability Advisor**

  Utilisez le service {{site.data.keyword.cloudaccesstrailfull_notm}} pour savoir comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.registrylong_notm}} dans {{site.data.keyword.cloud}}.

  Pour plus d'informations, voir [Evénements Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).
  
## 12 juillet 2018
{: #12jul2018}

- **API Vulnerability Advisor version 3**

  La version 3 de l'API modifie le comportement des noeuds finaux de l'API qui sont utilisés pour répertorier les exemptions. Vous devez vous assurer que votre utilisation de l'API ne repose pas sur le comportement de la version 2.

  Pour plus d'informations, voir [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/container-registry/va).

## 31 mai 2018
{: #31may2018}

- **Utilisation de Helm pour des images Passport Advantage**

  Importez le logiciel {{site.data.keyword.IBM_notm}}, téléchargé depuis [IBM Passport Advantage Online for customers ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/passportadvantage/pao_customer.html) et conditionné pour une utilisation avec Helm, dans votre espace de nom {{site.data.keyword.registrylong_notm}}.

  Pour plus d'informations, voir [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).

## 21 mars 2018
{: #21mar2018}

- **Container Scanner**

  Container Scanner active Vulnerability Advisor pour signaler tout problème lié à l'exécution de conteneurs ne se trouvant pas dans l'image de base du conteneur.

  Pour plus d'informations, voir [Installation de Container Scanner](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).

## 16 mars 2018
{: #16mar2018}

- **Container Image Security Enforcement version bêta**

  Utilisez Container Image Security Enforcement version bêta pour vérifier vos images de conteneur avant de les déployer sur votre cluster dans {{site.data.keyword.containerlong_notm}}. Vous pouvez contrôler l'emplacement depuis lequel les images sont déployées, mettre en application des règles Vulnerability Advisor et vous assurer que la [sécurité du contenu](/docs/services/Registry?topic=registry-registry_trustedcontent) est correctement appliquée à l'image.

  Pour plus d'informations, voir [Mise en application de la sécurité des images de conteneur](/docs/services/Registry?topic=registry-security_enforce#security_enforce).

## 20 février 2018
{: #20feb2018}

- **Contenu sécurisé**

  {{site.data.keyword.registrylong_notm}} fournit une technologie de contenu sécurisé pour vous permettre de signer des images et garantir l'intégrité des images de votre espace de nom de registre. En extrayant et en transférant des images signées, vous pouvez vérifier que vos images ont été envoyées par la partie appropriée, comme les outils d'intégration continue.

  Pour plus d'informations, voir la rubrique sur la [signature d'images pour contenu sécurisé](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).

## 6 novembre 2017
{: #6nov2017}

- **Base de registre globale**

  Une base de registre globale dont le nom ne comporte aucune région (`icr.io`) est disponible. Seules des images publiques fournies par IBM sont hébergées dans ce registre.

  Pour plus d'informations, voir [Base de registre globale](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## 29 septembre 2017
{: #29sep2017}

- **Génération d'images Docker**

  La commande `ibmcloud cr build` est désormais disponible pour exécuter des générations de conteneur. Vous pouvez générer une image Docker directement dans {{site.data.keyword.cloud_notm}} ou créer votre propre image Docker sur votre ordinateur local et la télécharger (par commande push) dans votre espace de nom dans {{site.data.keyword.registrylong_notm}}.

  Pour plus d'informations, voir [Génération d'images Docker pour les utiliser avec votre espace de nom](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) et [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).

## 24 août 2017
{: #24aug2017}

- **Interface graphique publiée**

  L'interface graphique {{site.data.keyword.registrylong_notm}} est disponible dans le catalogue. Voir [Container Registry ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/kubernetes/catalog/registry).

## 27 juin 2017
{: #27jun2017}

- **Disponibilité générale : {{site.data.keyword.registrylong_notm}}**

  {{site.data.keyword.registrylong_notm}} est généralement disponible en tant que service dans {{site.data.keyword.cloud_notm}}. {{site.data.keyword.registrylong_notm}} prend en charge {{site.data.keyword.containerlong_notm}}.

  Pour plus d'informations sur {{site.data.keyword.containerlong_notm}}, voir le [tutoriel d'initiation](/docs/containers?topic=containers-getting-started).
