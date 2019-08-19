---

copyright:
  years: 2019
lastupdated: "2019-08-07"

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

Découvrez les derniers changements apportés à {{site.data.keyword.registrylong}} et à Vulnerability Advisor. Les changements sont classés par date.
{:shortdesc}

## 1er août 2019
{: #01aug2019}

<dl>
  <dt>La commande `ibmcloud cr retention-run` est disponible</dt>
  <dd>La commande `ibmcloud cr retention-run` nettoie votre espace de nom en conservant les images pour chaque référentiel dans un espace de nom dans {{site.data.keyword.registrylong_notm}} en appliquant les critères spécifiés. Toutes les autres images contenues dans l'espace de nom sont supprimées.

  
  Pour plus d'informations, voir [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) et [Conservation des images](/docs/services/Registry?topic=registry-registry_retention).</dd>
</dl>

## 25 juillet 2019
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.at_full_notm}} disponible pour {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Utilisez le service {{site.data.keyword.at_full_notm}} pour contrôler comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.registrylong_notm}} dans {{site.data.keyword.cloud}}.

  Pour plus d'informations, voir [Evénements Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>

## 1er juillet 2019
{: #1jul2019}

<dl>
  <dt>La commande `ibmcloud cr token-add` n'est plus disponible</dt>
  <dd>La commande `ibmcloud cr token-add` n'est plus utilisée. Vous ne pouvez plus ajouter des jetons de registre dans l'interface de ligne de commande ou dans l'API.</dd>
</dl>

## 27 juin 2019
{: #27jun2019}

<dl>
  <dt>Container Scanner n'est plus disponible</dt>
  <dd>L'outil Container Scanner n'est plus utilisé. Vulnerability Advisor continue d'analyser les images qui sont envoyées à {{site.data.keyword.registrylong_notm}}.</dd>
</dl>

## 13 juin 2019
{: #13jun2019}

<dl>
  <dt>Suppression des étiquettes dans les images</dt>
  <dd>Suppression d'une ou plusieurs étiquettes de chaque image spécifiée dans {{site.data.keyword.registrylong_notm}}.

  Pour supprimer une étiquette d'une image et conserver l'image sous-jacente ainsi que toutes les étiquettes définies, utilisez la commande [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag). Si vous voulez supprimer l'image sous-jacente ainsi que toutes ses étiquettes, utilisez la commande [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm).

  Pour plus d'informations, voir [Suppression d'étiquettes d'images dans votre référentiel {{site.data.keyword.cloud_notm}} privé](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag).</dd>
</dl>

## 13 mai 2019
{: #13may2019}

<dl>
  <dt>Fin de prise en charge de Container Scanner</dt>
  <dd>Container Scanner est obsolète et n'est plus utilisable.

  Pour plus d'informations, voir [Installation de Container Scanner (obsolète)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 2 avril 2019
{: #2apr2019}

<dl>
  <dt>Disponibilité générale de Container Image Security Enforcement</dt>
  <dd>Utilisez Container Image Security Enforcement pour vérifier vos images de conteneur avant de les déployer sur votre cluster dans {{site.data.keyword.containerlong_notm}}. Vous pouvez contrôler l'emplacement depuis lequel les images sont déployées, mettre en application des règles Vulnerability Advisor et vous assurer que la [sécurité du contenu](/docs/services/Registry?topic=registry-registry_trustedcontent) est correctement appliquée à l'image.

  Pour plus d'informations, voir [Mise en application de la sécurité des images de conteneur](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 14 mars 2019
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponible pour {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Utilisez le service {{site.data.keyword.cloudaccesstraillong_notm}} pour savoir comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.registrylong_notm}} dans {{site.data.keyword.cloud}}.

  Pour plus d'informations, voir [Evénements Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).
</dd>
</dl>

## 25 février 2019
{: #25feb2019}

<dl>
  <dt>Nouveaux noms de domaine</dt>
  <dd>{{site.data.keyword.registrylong_notm}} adopte de nouveaux noms de domaine. Les nouveaux noms de domaine sont disponibles sur la console et sur l'interface de ligne de commande. Vous pouvez utiliser les nouveaux noms de domaine `icr.io` dès maintenant. Les noms de domaine `registry.bluemix.net` existants sont obsolètes, mais vous pouvez continuer de les utiliser jusqu'à la fin de la date de prise en charge. La date de fin de prise en charge n'est pas disponible à ce jour. Pour plus d'informations, voir [Régions](/docs/services/Registry?topic=registry-registry_overview#registry_regions) et [Introducing New IBM Cloud Container Registry Domain Names ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  Les signatures sont applicables au nom d'image entier, ce qui inclut le nom de domaine. Si vous utilisez Content Trust, vous devez ajouter de nouvelles signatures pour pouvoir consommer Content Trust sous le nouveau nom de domaine. Pour plus d'informations sur la signature d'images, voir [Signature d'images pour du contenu sécurisé](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

<dl>
  <dt>Secrets d'extraction de clé d'API IAM pour clusters {{site.data.keyword.containerlong_notm}} </dt>
  <dd>Les nouveaux secrets d'extraction d'image de cluster des domaines `icr.io` sont autorisés à l'aide d'une clé d'API {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM). Par conséquent, si vous souhaitez augmenter le contrôle des accès à vos ressources {{site.data.keyword.registrylong_notm}}, vous pouvez ajouter des politiques IAM. Vous pouvez, par exemple, changer les règles de clé d'API concernant l'extraction du secret du cluster afin que les images soient extraites uniquement à partir d'une région ou d'un espace de noms particulier du registre.
  
  Pour plus d'informations, voir [Comment votre cluster est-il autorisé à extraire des images d'{{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).</dd>
</dl>

<dl>
  <dt>Nouvelle région : ap-north</dt>
  <dd>Une nouvelle région est disponible dans `ap-north`. Vous pouvez utiliser la nouvelle région via le nom de domaine `jp.icr.io`.
  
  Pour plus d'informations, voir
[Régions](/docs/services/Registry?topic=registry-registry_overview#registry_regions).</dd>
</dl>

## 21 février 2019
{: #21feb2019}

<dl>
  <dt>Automatisation des accès à vos espaces de nom</dt>
  <dd>L'utilisation de jetons pour automatiser l'envoi et l'extraction d'images Docker vers et depuis vos espaces de nom est déprécié. Vous devez désormais utiliser des clés d'API pour automatiser l'accès à vos espaces de nom {{site.data.keyword.registrylong_notm}} pour pouvoir y transférer ou en extraire des images.

  Pour plus d'informations, voir [Automatisation de l'accès à vos espaces de nom à l'aide de clés d'API](/docs/services/Registry?topic=registry-registry_access#registry_api_key).</dd>
</dl>

## 8 janvier 2019
{: #8jan2019}

 <dl>
  <dt>Fin de prise en charge de l'API Vulnerability Advisor, version 2</dt>
  <dd>La version 2 de l'API Vulnerability Advisor est obsolète et n'est plus utilisable. Servez-vous de la version 3 de l'API. Voir [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/container-registry/va).

  Pour plus d'informations, voir [Vulnerability Advisor v2 API Deprecation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/).</dd>
</dl>

## 4 octobre 2018
{: #4oct2018}

<dl>
  <dt>Gestion des accès utilisateurs</dt>
  <dd>Utilisez {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) pour contrôler l'accès des utilisateurs à votre compte sur {{site.data.keyword.registrylong_notm}}. Lorsque les politiques IAM sont activées pour votre compte dans {{site.data.keyword.registrylong_notm}}, chaque utilisateur qui accède au service dans votre compte doit obtenir une politique d'accès avec un rôle d'utilisateur IAM défini. Cette règle détermine le rôle de l'utilisateur dans le contexte du service, ainsi que les actions qu'il peut exécuter.

  Pour plus d'informations, voir [Gestion des accès utilisateur à l'aide d'{{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam), [Définition de règles de rôle d'accès utilisateur](/docs/services/Registry?topic=registry-user#user) et [Tutoriel : Accorder l'accès à des ressources IBM Cloud Container Registry](/docs/services/Registry?topic=registry-iam_access#iam_access).</dd>
</dl>

## 7 août 2018
{: #7aug2018}

<dl>
  <dt>Règles d'exemption disponibles dans Vulnerability Advisor</dt>
  <dd>Si vous souhaitez gérer la sécurité d'une organisation {{site.data.keyword.cloud_notm}}, vous pouvez utiliser votre paramètre de règle pour déterminer si un problème est exempt ou non. Vous pouvez utiliser Container Image Security Enforcement pour garantir que le déploiement n'est permis qu'à partir d'images ne présentant pas de problèmes de sécurité une fois que ceux exemptés par votre règle ont été pris en compte.

  Pour plus d'informations, voir [Définition de règles d'exemption organisationnelles](/docs/services/Registry?topic=va-va_index#va_managing_policy).</dd>
</dl>

## 25 juillet 2018
{: #25jul2018}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponible pour Vulnerability Advisor</dt>
  <dd>Utilisez le service {{site.data.keyword.cloudaccesstrailfull_notm}} pour savoir comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.registrylong_notm}} dans {{site.data.keyword.cloud}}.

  Pour plus d'informations, voir [Evénements Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>
  
## 12 juillet 2018
{: #12jul2018}

<dl>
  <dt>API Vulnerability Advisor, version 3</dt>
  <dd>La version 3 de l'API modifie le comportement des noeuds finaux de l'API qui sont utilisés pour répertorier les exemptions. Vous devez vérifier que votre utilisation de l'API ne repose pas sur le comportement de la version 2.

  Pour plus d'informations, voir [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/container-registry/va).</dd>
</dl>

## 31 mai 2018
{: #31may2018}

<dl>
  <dt>Utilisation de Helm pour les images de Passport Advantage</dt>
  <dd>Importez le logiciel {{site.data.keyword.IBM_notm}}, téléchargé depuis [IBM Passport Advantage Online for customers ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/passportadvantage/pao_customer.html) et conditionné pour une utilisation avec Helm, dans votre espace de nom {{site.data.keyword.registrylong_notm}}.

  Pour plus d'informations, voir [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).</dd>
</dl>

## 21 mars 2018
{: #21mar2018}

<dl>
  <dt>Container Scanner</dt>
  <dd>Container Scanner active Vulnerability Advisor pour signaler tout problème lié à l'exécution de conteneurs ne se trouvant pas dans l'image de base du conteneur.

  Pour plus d'informations, voir [Installation de Container Scanner](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 16 mars 2018
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement version bêta</dt>
  <dd>Utilisez Container Image Security Enforcement version bêta pour vérifier vos images de conteneur avant de les déployer sur votre cluster dans {{site.data.keyword.containerlong_notm}}. Vous pouvez contrôler l'emplacement depuis lequel les images sont déployées, mettre en application des règles Vulnerability Advisor et vous assurer que la [sécurité du contenu](/docs/services/Registry?topic=registry-registry_trustedcontent) est correctement appliquée à l'image.

  Pour plus d'informations, voir [Mise en application de la sécurité des images de conteneur](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 20 février 2018
{: #20feb2018}

<dl>
  <dt>Contenu sécurisé</dt>
  <dd>{{site.data.keyword.registrylong_notm}} fournit une technologie de contenu sécurisé pour vous permettre de signer des images et garantir l'intégrité des images de votre espace de nom de registre. En extrayant et en transférant des images signées, vous pouvez vérifier que vos images ont été envoyées par la partie appropriée, comme les outils d'intégration continue.

  Pour plus d'informations, voir la rubrique sur la [signature d'images pour contenu sécurisé](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

## 6 novembre 2017
{: #6nov2017}

<dl>
  <dt>Base de registre globale</dt>
  <dd>Une base de registre globale est disponible. Elle n'a aucune région incluse dans son nom de domaine (`icr.io`). Seules des images publiques fournies par IBM sont hébergées dans ce registre.

  Pour plus d'informations, voir [Base de registre globale](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).</dd>
</dl>

## 29 septembre 2017
{: #29sep2017}

<dl>
  <dt>Génération d'images Docker</dt>
  <dd>La commande `ibmcloud cr build` est désormais disponible pour exécuter des générations de conteneur. Vous pouvez générer une image Docker directement dans {{site.data.keyword.cloud_notm}} ou créer votre propre image Docker sur votre ordinateur local et la télécharger (par commande push) dans votre espace de nom dans {{site.data.keyword.registrylong_notm}}.

  Pour plus d'informations, voir [Génération d'images Docker pour les utiliser avec votre espace de nom](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) et [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).</dd>
</dl>

## 24 août 2017
{: #24aug2017}

<dl>
  <dt>Interface graphique publiée</dt>
  <dd>L'interface graphique d'{{site.data.keyword.registrylong_notm}} est disponible dans le catalogue, voir [Registre de conteneurs ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/kubernetes/catalog/registry).</dd>
</dl>

## 27 juin 2017
{: #27jun2017}

<dl>
  <dt>Disponibilité générale d'{{site.data.keyword.registrylong_notm}}</dt>
  <dd>{{site.data.keyword.registrylong_notm}} est généralement disponible en tant que service dans {{site.data.keyword.cloud_notm}}. {{site.data.keyword.registrylong_notm}} prend en charge {{site.data.keyword.containerlong_notm}}.

  Pour plus d'informations sur {{site.data.keyword.containerlong_notm}}, voir le [tutoriel d'initiation](/docs/containers?topic=containers-getting-started).</dd>
</dl>
