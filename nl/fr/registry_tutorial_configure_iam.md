---

copyright:
  years: 2018
lastupdated: "2018-10-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Tutoriel : Octroi de droits d'accès aux ressources {{site.data.keyword.registrylong_notm}}
{: #iam_access}

Utilisez ce tutoriel pour apprendre comment accorder des droits d'accès à vos ressources en configurant {{site.data.keyword.iamlong}} (IAM) pour {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Ce tutoriel dure environ 45 minutes.

**Avant de commencer**

- Suivez les instructions décrites dans la rubrique [Initiation à {{site.data.keyword.registrylong_notm}}](/docs/services/Registry/index.html#index).

- Assurez-vous que vous disposez de la version la plus récente du plug-in container-registry pour l'interface de ligne de commande {{site.data.keyword.cloud_notm}}. Voir [Mise à jour du plug-in container-registry](https://console.bluemix.net/docs/services/Registry/registry_setup_cli_namespace.html#registry_cli_update).

- Vous devez avoir accès à deux comptes [{{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/) que vous pouvez utiliser dans le cadre de ce tutoriel, l'un pour l'utilisateur A et l'autre pour l'utilisateur B, chacun devant utiliser une adresse électronique unique. Vous travaillez dans votre propre compte ('utilisateur A) et vous invitez un autre utilisateur (utilisateur B) à utiliser votre compte. Vous pouvez choisir de créer un deuxième compte {{site.data.keyword.cloud_notm}} ou vous pouvez travailler avec un collègue qui possède un compte {{site.data.keyword.cloud_notm}}.

- Si vous avez commencé à utiliser {{site.data.keyword.registrylong_notm}} dans votre compte avant le 4 octobre 2018, vous devez activer l'application des règles IAM en exécutant la commande `ibmcloud cr iam-policies-enable`. Si vous avez invité d'autres utilisateurs à utiliser vos espaces de nom {{site.data.keyword.registrylong_notm}} dans votre compte IBM Cloud, utilisez un autre compte en tant qu'utilisateur A pour empêcher que leurs accès ne soient interrompus.

## Etape 1 : Autoriser un utilisateur à configurer le registre
{: #configure_registry}

Dans cette section, vous allez ajouter un deuxième utilisateur à votre compte et lui octroyer les droits nécessaires pour configurer {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Ajoutez l'utilisateur B au compte de l'utilisateur A :

    1. Connectez-vous au compte de l'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud login
        ```
        {: pre}

    2. Invitez l'utilisateur B à accéder au compte de l'utilisateur A en exécutant la commande suivante, où _`<user.b@example.com>`_ est l'adresse électronique de l'utilisateur B :

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. Procurez-vous l'ID de compte de l'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud target
        ```
        {: pre}

        Notez l'ID de compte qui figure entre parenthèses ( ) sur la ligne Compte.

2. Vérifiez que l'utilisateur B peut cibler le compte de l'utilisateur A mais qu'il ne peut pas encore effectuer quoi que ce soit avec {{site.data.keyword.registrylong_notm}} :

    1. Connectez-vous en tant qu'utilisateur B et exécutez la commande suivante pour cible le compte de l'utilisateur A, où _`<YourAccountID>`_ est l'ID de compte de l'utilisateur A :

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Essayez d'éditer votre quota de registre afin de le remplacer par 4 Go de trafic en exécutant la commande suivante :

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        La commande échoue car l'utilisateur B ne dispose pas des droits appropriés.

3. Accordez à l'utilisateur B le rôle Responsable afin qu'il puisse configurer {{site.data.keyword.registrylong_notm}} :

    1. Reconnectez-vous à votre compte en tant qu'utilisateur A (vous-même) en exécutant la commande suivante :

        ```
        ibmcloud login
        ```
        {: pre}

    2. Créez une règle qui affecte le rôle Responsable à l'utilisateur B en exécutant la commande suivante :

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. Vérifiez que l'utilisateur B peut désormais modifier des quotas dans le compte de l'utilisateur A :

    1. Connectez-vous en tant qu'utilisateur B afin de cibler le compte de l'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Essayez d'éditer votre quota de registre afin de le remplacer par 4 Go de trafic en exécutant la commande suivante :

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        La commande aboutit car l'utilisateur B dispose des droits d'accès appropriés.

    3. A présent, rétablissez le quota en exécutant la commande suivante :
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. Effectuez des opérations de nettoyage :

    1. Reconnectez-vous à votre compte en tant qu'utilisateur A (vous-même) en exécutant la commande suivante :
  
        ```
        ibmcloud login
        ```
        {: pre}
  
    2. Répertoriez les règles pour l'utilisateur B, localisez la règle que vous venez de créer en exécutant la commande suivante, et notez l'ID :
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. Supprimez la règle en exécutant la commande suivante, où _`<Policy_ID>`_ est votre ID de règle :
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Etape 2 : Autoriser un utilisateur à accéder à des espaces de nom spécifiques
{: #access_resources}

Dans cette section, vous allez créer des espaces de nom avec des exemples d'image et accorder des droits permettant d'y accéder. Vous allez créer des règles pour octroyer différents rôles d'accès à chaque espace de nom et vous allez afficher l'impact de ces actions.
{:shortdesc}

1. Créez trois nouveaux espaces de nom dans le compte de l'utilisateur A. Ces espaces de nom doivent être uniques dans la région, par conséquent, vous choisissez vos propres noms d'espace de nom. Cela dit, ce tutoriel utilise `namespace_a`, `namespace_b` et `namespace_c` en guise d'exemples :

    1. Connectez-vous en tant qu'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud login
        ```
        {: pre}

    2. Créez un espace de nom, `namespace_b`, en exécutant la commande suivante :

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}

        Les noms d'espace de nom doivent être uniques dans la région.
        {: tip}

    3. Créez un autre espace de nom, `namespace_c`, en exécutant la commande suivante :

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. Vérifiez que l'utilisateur B ne peut rien voir :

    1. Connectez-vous en tant qu'utilisateur B afin de cibler le compte de l'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Essayez de répertorier des images en tant qu'utilisateur B en exécutant la commande suivante :

        ```
        ibmcloud cr images
        ```
        {: pre}

        Cette commande renvoie une liste vide car l'utilisateur B n'a pas accès aux espaces de nom.

3. Créez des règles pour accorder à l'utilisateur B les droits lui permettant d'interagir avec les espaces de nom en exécutant la commande suivante :

    1. Connectez-vous en tant qu'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud login
        ```
        {: pre}

    2. Assurez-vous qu'au moins trois espaces de nom sont répertoriés en exécutant la commande suivante :

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        Les trois espaces de nom que vous avez créés dans ce tutoriel (`namespace_a`, `namespace_b` et `namespace_c`) s'affichent. Si vous ne voyez pas ces espaces de nom, revenez en arrière et suivez les instructions permettant de les recréer.

    3. Créez une règle qui affecte le rôle Lecteur sur `namespace_b` à l'utilisateur B en exécutant la commande suivante, où _`<Region>`_ est le nom abrégé de votre [région](/docs/services/Registry/registry_overview.html#registry_regions), par exemple, `us-south` :

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource <namespace_b> --roles Reader
        ```
        {: pre}

    4. Créez une seconde règle qui affecte les rôles Lecteur et Editeur sur `namespace_c` à l'utilisateur B en exécutant la commande suivante :

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        Cette commande ajoute deux rôles à la même ressource dans la même règle.
        {: tip}

4. Envoyez les images dans `namespace_a` et `namespace_b` :

    1. Extrayez l'image `hello-world` en exécutant la commande suivante :

        ```
        docker pull hello-world
        ```
        {: pre}

    2. Balisez l'image avec `namespace_a` en exécutant la commande suivante :

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

    3. Balisez l'image avec `namespace_b` en exécutant la commande suivante :

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

    4. Connectez-vous à {{site.data.keyword.registrylong_notm}} en exécutant la commande suivante :

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Envoyez l'image à `namespace_a` en exécutant la commande suivante :

        ```
        docker push registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

    6. Envoyez l'image à `namespace_b` en exécutant la commande suivante :

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

5. Vérifiez que l'utilisateur B peut interagir avec `namespace_b` et `namespace_c` mais pas avec `namespace_a`:

    1. Connectez-vous en tant qu'utilisateur B en exécutant la commande suivante :

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Vérifiez que l'utilisateur B peut voir `namespace_b` et `namespace_c`, mais pas `namespace_a` car il n'a pas accès à `namespace_a`, en exécutant la commande suivante :

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. Répertoriez vos images en exécutant la commande suivante :

        ```
        ibmcloud cr images
        ```
        {: pre}

        L'image dans `namespace_b` apparaît dans la liste, mais l'image dans `namespace_a` n'apparaît pas dans la liste, car l'utilisateur B n'a pas accès à `namespace_a`.

    4. Connectez-vous à {{site.data.keyword.registrylong_notm}} en exécutant la commande suivante :

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Extrayez l'image en exécutant la commande suivante :

        ```
        docker pull registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

    6. Envoyez l'image à `namespace_b` en exécutant la commande suivante :

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

        Cette commande échoue car l'utilisateur B ne dispose pas du rôle Editeur sur `namespace_b`.

    7. Balisez l'image avec `namespace_c` en exécutant la commande suivante :

        ```
        docker tag hello-world registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

    8. Envoyez l'image à `namespace_c` en exécutant la commande suivante :

        ```
        docker push registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

        La commande aboutit car l'utilisateur B dispose du rôle Editeur sur `namespace_c`.

    9. Extrayez l'image de `namespace_c` en exécutant la commande suivante :

        ```
        docker pull registry.<Region>.bluemix.net/namespace_c/hello-world
        ```
        {: pre}

        La commande aboutit car l'utilisateur B dispose du rôle Lecteur sur `namespace_c`.

6. Effectuez des opérations de nettoyage :

    1. Reconnectez-vous au compte de l'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud login
        ```
        {: pre}

    2. Répertoriez les règles pour l'utilisateur B en exécutant la commande suivante :

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        Recherchez les règles que vous venez de créer et notez les ID de règle.

    3. Supprimez les règles que vous venez de créer en exécutant la commande suivante, où _`<Policy_ID>`_ est l'ID de règle :

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Etape 3 : Créer un ID de service et octroyer des droits d'accès à une ressource
{: #service_id}

Dans cette section, vous allez configurer un ID de service et lui octroyer les droits nécessaires pour accéder à votre espace de nom {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Configurez un ID de service avec des droits d'accès à {{site.data.keyword.registrylong_notm}} et créez une clé d'API pour cet ID de service :

    1. Connectez-vous au compte de l'utilisateur A en exécutant la commande suivante :

        ```
        ibmcloud login
        ```
        {: pre}

    2. Créez un ID de service nommé `cr-roles-tutorial` avec la description `"Created during the access control tutorial for Container Registry"` en exécutant la commande suivante :

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. Créez une règle de service qui affecte le rôle Lecteur sur `namespace_a` pour l'ID de service en exécutant la commande suivante :

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. Créez une seconde règle de service qui affecte le rôle Editeur sur `namespace_b` en exécutant la commande suivante :

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. Créez une clé d'API pour l'ID de service en exécutant la commande suivante :

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Utilisez Docker pour vous connecter à la clé d'API de l'ID de service, où _`<API_Key>`_ est votre clé d'API, et pour interagir avec le registre :

    1. Connectez-vous à {{site.data.keyword.registrylong_notm}} en exécutant la commande suivante :

        ```
        docker login -u iamapikey -p <API_Key> registry.<Region>.bluemix.net
        ```
        {: pre}

    2. Extrayez votre image en exécutant la commande suivante :

        ```
        docker pull registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

        Cette commande aboutit.

    3. Envoyez votre image à `namespace_a` en exécutant la commande suivante :

        ```
        docker push registry.<Region>.bluemix.net/namespace_a/hello-world
        ```
        {: pre}

        Cette commande échoue car l'utilisateur ne dispose pas du rôle Editeur sur `namespace_a`.

    4. Envoyez votre image à `namespace_b` en exécutant la commande suivante :

        ```
        docker push registry.<Region>.bluemix.net/namespace_b/hello-world
        ```
        {: pre}

        La commande aboutit car l'utilisateur dispose du rôle Editeur sur `namespace_b`.

3. Effectuez des opérations de nettoyage :

    1. Répertoriez vos règles de service en exécutant la commande suivante :

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        Notez les ID de règle.

    2. Supprimez vos règles de service en exécutant la commande suivante pour chaque règle :

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. Supprimez votre ID de service en exécutant la commande suivante :

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. Reconnectez-vous à {{site.data.keyword.registrylong_notm}} en tant qu'utilisateur A :

        ```
        ibmcloud cr login
        ```
        {: pre}

## Etape 4 : Nettoyer
{: #clean_up}

Dans cette section, vous allez retirer les resources que vous avez créées au cours des sections précédentes afin de remettre votre compte tel dans l'état où il était au début de ce tutoriel.
{:shortdesc}

1. Connectez-vous à votre compte en exécutant la commande suivante :

    ```
    ibmcloud login
    ```
    {: pre}

2. Supprimez `namespace_a`, `namespace_b` et `namespace_c` en exécutant les commandes suivantes :

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. Retirez l'utilisateur B de votre compte en exécutant la commande suivante :

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

Félicitations ! Vous avez terminé ce tutoriel.
