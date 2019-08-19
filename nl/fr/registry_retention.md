---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# Conservation des images
{: #registry_retention}

Vous pouvez décider si vous souhaitez supprimer ou conserver les images.
{:shortdesc}

## Planification de la rétention
{: #retention_plan}

La commande [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) fonctionne par espaces de nom, ce qui signifie qu'en utilisant plusieurs espaces de noms dans votre pipeline, vous pouvez appliquer différents critères de conservation pour répondre au mieux à vos besoins.

Pensez à un pipeline de livraison typique avec des environnements de développement, de préproduction et de production. Au fur et à mesure que le code est livré, l'intégration et le déploiement continus placent les images dans le registre et les déploient ensuite directement dans votre environnement de développement. Après les tests, certaines versions issues du développement sont transférées vers la préproduction, puis éventuellement vers la production. Dans ce scénario, le taux de changement d'image est le plus rapide en développement et le plus lent en production. Si tous vos environnements extraient des images du même espace de nom, il peut être difficile de choisir un nombre approprié d'images à conserver en raison de cette différence de vitesse.

Une bonne approche consiste à livrer toutes les images dans un espace de noms de développement, par exemple, `project-development`, puis à utiliser la commande [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) pour étiqueter l'image dans un espace de noms différent lorsqu'elle est promue à un niveau supérieur du pipeline. Dans l'exemple précédent, vous pouvez avoir trois espaces de nom : développement, `project-development`, préproduction, `project-staging` et production, `project-production`. Lorsque vous faites la promotion du développement à la préproduction, les images passent de l'espace de nom `project-development` à l'espace de nom `project-staging`, et les images appartenant à l'espace de nom `project-staging` sont utilisées pour le déploiement. De même, lorsque vous faites la promotion de la préproduction à la production, les images passent de l'espace de noms`project-staging` à l'espace de noms `project-production`, et les images de l'espace de nom `project-production` sont utilisées dans le déploiement de production.

En utilisant cette technique, vous obtenez les avantages suivants :

* Vous pouvez choisir différents paramètres de conservation pour les espaces de nom de développement, de préproduction et de production.
* Vous minimisez les risques de supprimer accidentellement une image qui pourrait être utilisée dans vos environnements de préproduction ou de production, par rapport à l'utilisation d'un seul espace de nom pour toutes les images.
* Vous pouvez utiliser différentes politiques [IAM](/docs/services/Registry?topic=registry-iam). Par exemple, vous pouvez avoir un accès plus restrictif aux images de production.
* Vous pouvez signer des images de production, mais ne pas signer les images de développement et de préproduction.

## Nettoyage de vos espaces de nom en conservant uniquement les images qui répondent à vos critères
{: #retention_images}

Conservez les images pour chaque référentiel au sein d'un espace de nom dans {{site.data.keyword.registrylong_notm}} en appliquant les critères spécifiés. Toutes les autres images contenues dans l'espace de nom sont supprimées.
{:shortdesc}

La commande [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) répertorie les images à supprimer et vous offre la possibilité d'annuler l'opération avant leur destruction.

Lorsqu'une image, dans un référentiel, est référencée par plusieurs balises, cette image n'est comptée qu'une seule fois. Les images les plus récentes sont conservées. L'âge est déterminé par la date de création de l'image, et non par la date à laquelle elle a été transférée dans le registre.
{: tip}

La suppression d'une image est irréversible. La suppression d'une image qui est utilisée par un déploiement existant peut entraîner l'échec d'une augmentation et/ou d'une replanification.
{: important}

Pour réduire le nombre d'images dans chaque référentiel de votre espace de nom à l'aide de l'interface CLI, suivez les étapes suivantes :

1. Connectez-vous à {{site.data.keyword.cloud_notm}} en exécutant la commande `ibmcloud login`.
2. Choisissez le registre dans lequel vous voulez nettoyer vos images en exécutant la commande suivante et en sélectionnant la région appropriée :

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. Pour conserver certaines images et en supprimer d'autres, exécutez la commande suivante :

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   où `IMAGECOUNT` représente le nombre d'images que vous voulez conserver pour chaque référentiel dans votre espace de nom, `NAMESPACE`.

3. Vérifiez que les images ont été supprimées en exécutant la commande suivante, et vérifiez que les images n'apparaissent pas dans la liste.

   ```
   ibmcloud cr image-list
   ```
   {: pre}
