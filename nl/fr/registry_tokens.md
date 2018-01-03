---

copyright:
  years: 2017
lastupdated: "2017-12-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Automatisation de l'accès à {{site.data.keyword.registrylong_notm}}
{: #registry_access}

Vous pouvez utiliser des jetons de registre ou bien une clé d'API {{site.data.keyword.iamlong}} (IAM) pour automatiser l'accès à vos espaces de nom {{site.data.keyword.registrylong_notm}} pour pouvoir y transférer ou en extraire des images.
{:shortdesc}

Les clés d'API sont liées à votre compte et peuvent être utilisées à travers {{site.data.keyword.Bluemix_notm}} de sorte que vous n'avez pas besoin de données d'identification différentes pour chaque service. Vous pouvez utiliser la clé d'API dans l'interface de ligne de commande ou dans le cadre de l'automatisation pour vous connecter sous votre identité utilisateur.

La portée des jetons du registre est limitée à {{site.data.keyword.registrylong_notm}}. Vous pouvez les limiter à un accès en lecture seule et spécifier s'ils doivent expirer ou non.

Pour plus d'informations sur les clés d'API {{site.data.keyword.registrylong_notm}}, voir [Utilisation des clés d'API](../../iam/apikeys.html#manapikey).

Avant de commencer, [installez l'interface de ligne de commande d'{{site.data.keyword.registrylong_notm}} et l'interface de ligne de commande de Docker](registry_setup_cli_namespace.html#registry_cli_install).


## Automatisation de l'accès à vos espaces de nom à l'aide de clés d'API
{: #registry_api_key}

Vous pouvez utiliser des clés d'API pour automatiser l'envoi et l'extraction d'images Docker vers et depuis vos espaces de nom.
{:shortdesc}

### Création d'une clé d'API
{: #registry_api_key_create}

Vous pouvez créer une clé d'API afin de l'utiliser pour vous connecter à votre registre.
{:shortdesc} 

Créez une clé d'API IAM. Voir [Création de clés d'API](../../iam/userid_keys.html#creating-an-api-key). 

### Utilisation d'une clé d'API pour automatiser les accès
{: #registry_api_key_use}

Vous pouvez utiliser une clé d'API pour automatiser l'accès à vos espaces de nom dans {{site.data.keyword.registrylong_notm}}.
{:shortdesc} 

Utilisez la clé d'API pour vous connecter à votre registre en exécutant la commande Docker suivante. Remplacez &lt;your_apikey&gt; par votre clé d'API et &lt;registry_url&gt; par l'URL du registre où sont définis vos espaces de nom.

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}


Pour les informations de référence sur la commande, voir [Créer une nouvelle clé d'API pour la plateforme {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_api_key_create).


## Automatisation de l'accès à vos espaces de nom à l'aide de jetons
{: #registry_tokens}

Vous pouvez utiliser des jetons pour automatiser l'envoi et l'extraction d'images Docker vers et depuis vos espaces de nom {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Quiconque est en possession d'un jeton de registre peut accéder à des informations sécurisées. En créant un jeton pour votre compte {{site.data.keyword.Bluemix_notm}}, vous pouvez accorder un accès à tous vos espaces de nom configurés dans une région à des utilisateurs ne faisant pas partie de votre compte {{site.data.keyword.Bluemix_notm}}. Chaque utilisateur ou application en possession de ce jeton peut transférer des images vers vos espaces de nom, et en extraire, sans avoir à installer le plug-in container-registry. 

Quand vous créez un jeton pour votre compte {{site.data.keyword.Bluemix_notm}}, vous pouvez décider s'il octroie un accès en lecture seule (pull) ou en écriture (push et pull) au registre. Vous pouvez également spécifier s'il doit être permanent ou expirer au bout de 24 heures. Pour pouvez créer et utiliser plusieurs jetons destinés à des types d'accès différents.

Utilisez les tâches suivantes pour gérer vos jetons :

-  [Création d'un jeton pour votre compte {{site.data.keyword.Bluemix_notm}}](#registry_tokens_create)
-  [Utilisation d'un jeton pour automatiser l'accès à vos espaces de nom](#registry_tokens_use)
-  [Retrait d'un jeton de votre compte {{site.data.keyword.Bluemix_notm}}](#registry_tokens_remove)


### Création d'un jeton pour votre compte {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_create}

Vous pouvez créer un jeton pour accorder un accès à tous vos espaces de nom {{site.data.keyword.registrylong_notm}} dans une région.
{:shortdesc}

1.  Créez un jeton. L'exemple suivant créé un jeton n'expirant pas et doté d'un accès en lecture et écriture à tous les espaces de nom configurés dans une région.

    ```
    bx cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="light bulb icon"/> Description des composantes de cette commande</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>Facultatif. Utilisez cette option pour décrire votre jeton afin qu'il soit plus facilement identifiable plus tard.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>Facultatif. Utilisez cette option pour créer un jeton n'expirant pas. Si vous ne spécifiez pas cette option, il devient périmé au bout de 24 heures. <br> **Conseil :** afin de bloquer l'accès à vos espaces de nom, prenez soin de retirer un jeton qui n'expire pas quand vous n'en avez plus besoin.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>Facultatif. Utilisez cette option pour créer un jeton permettant aux utilisateurs d'envoyer (par commande push) des images à vos espaces de nom et d'en extraire (par commande pull). Si vous ne spécifiez pas cette option, le jeton ne peut être utilisé que pour extraire des images (commande pull).</td>
        </tr>
        </tbody>
        </table>

    Votre sortie CLI sera similaire à ceci :

    ```
    Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
    Token              <token_value>
    ```
    {: screen}

2.  Vérifiez que le jeton a été créé.

    ```
    bx cr token-list
    ```
    {: pre}


### Utilisation d'un jeton pour automatiser l'accès à vos espaces de nom 
{: #registry_tokens_use}

Vous pouvez utiliser un jeton dans votre commande `docker login` pour automatiser l'accès à vos espaces de nom dans {{site.data.keyword.registrylong_notm}}. Selon que vous avez affecté un accès en lecture seule ou en lecture/écriture à votre jeton, les utilisateurs peuvent extraire (par pull) des images de vos espaces de nom ou bien en envoyer et en extraire (push et pull).
{:shortdesc}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Répertoriez tous les jetons dans votre compte {{site.data.keyword.Bluemix_notm}} et notez l'ID du jeton que vous voulez utiliser.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Extrayez la valeur de jeton de ce jeton. Remplacez &lt;token_id&gt; par l'ID du jeton concerné.

    ```
    bx cr token-get <token_id>
    ```
    {: pre}

    Votre valeur de jeton est affichée dans la zone **Jeton** de la sortie de l'interface de ligne de commande.

4.  Utilisez le jeton avec votre commande `docker login`. Remplacez la valeur de &lt;token_value&gt; par la valeur de jeton que vous avez extraite à l'étape précédente et la valeur de &lt;registry_url&gt; par l'URL du registre où sont configurés vos espaces de nom.

    -   Pour les espaces de nom définis sur la région Sud des Etats-Unis : registry.ng.bluemix.net
    -   Pour les espaces de nom définis sur la région Sud du Royaume-Uni : registry.eu-gb.bluemix.net
    -   Pour les espaces de nom définis sur la région Centre Europe : registry.eu-de.bluemix.net
    -   Pour les espaces de nom définis sur la région Asie-Pacifique sud : registry.au-syd.bluemix.net

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}

    Une fois que vous vous êtes connecté à Docker en utilisant le jeton, vous pouvez transférer dans vos espaces de nom des images (push) ou en extraire (pull).


### Retrait d'un jeton de votre compte {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_remove}

Retirez un jeton {{site.data.keyword.registrylong_notm}} quand vous n'en n'avez plus besoin.
{:shortdesc}

**Remarque :** les jetons {{site.data.keyword.registrylong_notm}} arrivés à expiration sont retirés automatiquement de votre compte {{site.data.keyword.Bluemix_notm}}, vous n'avez pas besoin de les retirer manuellement.

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Répertoriez tous les jetons dans votre compte {{site.data.keyword.Bluemix_notm}} et notez l'ID du jeton que vous voulez utiliser.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Supprimez le jeton.

    ```
    bx cr token-rm <token_id>
    ```
    {: pre}
    


