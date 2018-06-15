---

copyright:
  years: 2017, 2018
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Gestion des limites de quota pour le stockage et le trafic d'extraction
{: #registry_quota}

Vous pouvez limiter le volume de stockage et de trafic d'extraction pouvant
être utilisé dans votre compte
{{site.data.keyword.Bluemix}} en
définissant et en gérant des limites de quota personnalisées.
{:shortdesc}


## Définition des limites de quota pour le stockage et l'extraction des images
{: #registry_quota_set}

Vous pouvez limiter le volume de stockage et de trafic d'extraction (pull)
de vos images privées en définissant vos propres limites de quota.
{:shortdesc}

Avant de commencer, vérifiez que vous êtes le [propriétaire
ou le responsable de la facturation pour le compte {{site.data.keyword.Bluemix_notm}}](../../iam/users_roles.html#userroles) dans lequel vous voulez définir le quota.

Lorsque vous procédez à la mise à niveau vers le plan standard
d'{{site.data.keyword.registryshort_notm}}, vous
bénéficiez d'un volume illimité de stockage et de trafic d'extraction (pull) pour vos
images privées. Pour éviter de dépasser votre niveau de paiement défini dans vos
préférences, vous pouvez définir des quotas individuels pour le volume de stockage et de
trafic d'extraction. Les limites de quota sont appliquées à tous les espaces de nom que
vous configurez dans {{site.data.keyword.registrylong_notm}}. Si
vous utilisez le plan de service gratuit, vous pouvez également définir des quotas
personnalisés dans le cadre du volume gratuit de stockage et de trafic d'extraction.

Pour définir un quota, procédez comme suit :

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Examinez vos limites de quota en cours concernant le stockage et le trafic
d'extraction (pull).

    ```
    bx cr quota
    ```
    {: pre}

    Votre sortie sera similaire à ceci.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}

3.  Modifiez la limite de quota pour le stockage et le trafic d'extraction. Pour modifier l'utilisation du trafic d'extraction, indiquez l'option
**traffic** et remplacez
_&lt;quota_trafic&gt;_ par la valeur en mégaoctets que vous souhaitez
définir pour le quota de trafic d'extraction. Si vous voulez modifier le volume de
stockage de votre compte, indiquez l'option **storage** et
remplacez _&lt;quota_stockage&gt;_ par la valeur en mégaoctets que vous
voulez définir.

    **Remarque :** si vous bénéficiez du plan gratuit, vous ne pouvez pas définir comme quota une
quantité qui dépasse le niveau gratuit. La franchise du niveau gratuit pour le stockage
est de 512 Mo et le trafic est de 5120 Mo.

    ```
    bx cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    Exemple de définition d'une limite de quota de stockage de 600 mégaoctets et d'un trafic
d'extraction de 7000 mégaoctets :

    ```
    bx cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}


## Examen des limites de quota, de l'utilisation du stockage et de l'extraction des images
{: #registry_quota_get}

Vous pouvez examiner vos limites de quota et vérifier l'utilisation de votre
stockage actuel et du trafic d'extraction (pull) pour votre compte.
{:shortdesc}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Examinez vos limites de quota en cours concernant le stockage et le trafic
d'extraction (pull).

    ```
    bx cr quota
    ```
    {: pre}

    Votre sortie sera similaire à ceci.

    ```
    Getting quotas and usage for the current month, for account '<account_owner> Account'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    OK
    ```
    {: screen}


## Libération du stockage utilisé et modification des plans de service ou des
limites de quota dans le but de rester dans les limites de quota données
{: #registry_quota_freeup}

Si vous dépassez les limites de quota définies pour votre compte
{{site.data.keyword.Bluemix_notm}}, vous
pouvez libérer du stockage et modifier votre plan de service ou les limites de quota pour
continuer à envoyer des images par commande push ou à en extraire par commande pull vers
et depuis votre espace de nom.
{:shortdesc}

Pour libérer du stockage d'images dans votre compte {{site.data.keyword.Bluemix_notm}} :

1.  Répertoriez toutes les images de tous vos espaces de nom dans votre compte {{site.data.keyword.Bluemix_notm}}.

    ```
    bx cr images
    ```
    {: pre}

2.  Retirez une image de votre espace de nom. Remplacez _&lt;image_name&gt;_ par le nom de l'image que vous voulez supprimer.

    ```
    bx cr image-rm <image_name>
    ```
    {: pre}

    **Remarque :** en fonction de la taille de l'image, le retrait de cette dernière ainsi que la mise à disposition du
stockage peuvent prendre un certain temps.

3.  Examinez votre utilisation du quota de stockage.

    ```
    bx cr quota
    ```
    {: pre}

4. **Remarque :** vous ne pouvez pas réduire votre utilisation du trafic d'extraction (pull)
dans une période de facturation.

    Pour continuer à extraire des images de vos espaces de nom, sélectionnez l'une des options suivantes.

    -   Patientez jusqu'au début du cycle de facturation suivant.
    -   Si vous disposez d'un plan gratuit,
[procédez à une mise à niveau vers le plan de
service standard](registry_overview.html#registry_plan_upgrade).
    -   Si vous disposez déjà d'un plan standard,
[définissez de nouvelles limites de quota pour le
trafic d'extraction](#registry_quota_set).
