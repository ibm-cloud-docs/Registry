---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, Docker Content Trust, keys

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

# Signature d'images pour du contenu sécurisé
{: #registry_trustedcontent}

{{site.data.keyword.registrylong}} fournit une technologie de contenu sécurisé pour vous permettre de signer des images et garantir l'intégrité des images de votre espace de nom de registre. En extrayant et en transférant des images signées, vous pouvez vérifier que vos images ont été envoyées par la partie appropriée, comme les outils d'intégration continue. Pour utiliser cette fonction, vous devez disposer de Docker version 18.03 ou ultérieure. Pour en savoir plus, consultez la documentation [Docker Content Trust ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/engine/security/trust/content_trust/) et la documentation sur le [projet Notary ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/theupdateframework/notary).
{:shortdesc}

Lorsque vous envoyez par commande push votre image avec le contenu sécurisé activé, votre client Docker envoie également un objet métadonnées signé au serveur d'accréditation {{site.data.keyword.Bluemix_notm}}. Lors de l'extraction d'une image balisée avec Docker Content Trust activé, votre client Docker contacte le serveur d'accréditation afin d'établir la version signée la plus récente de la balise demandée, vérifie la signature du contenu puis télécharge l'image signée.

Un nom d'image est composé d'un référentiel et d'une balise. Lorsque vous utilisez du contenu sécurisé, chaque référentiel utilise une clé de signature unique. Chaque balise d'un référentiel utilise la clé appartenant au référentiel. Si plusieurs équipes publient du contenu, chacun sur leur propre référentiel au sein de vos espaces de nom {{site.data.keyword.registrylong_notm}}, chaque équipe peut utiliser ses propres clés pour signer son contenu, ce qui vous permet de vérifier que chaque image est produite par l'équipe appropriée.

Un référentiel peut comporter du contenu signé et du contenu non signé. Si Docker Content Trust est activé, vous pouvez accéder au contenu signé d'un référentiel, même si ce dernier contient également du contenu non signé.

Docker Content Trust utilise un modèle de sécurité de type "approuver à la première utilisation". La clé de référentiel est extraite du serveur d'accréditation lorsque vous extrayez une image signée d'un référentiel pour la première fois, et cette clé est utilisée pour vérifier ultérieurement les images provenant de ce référentiel. Vous devez vous assurer de la fiabilité du serveur d'accréditation ou de l'image et de son diffuseur avant d'extraire le référentiel pour la première fois. Si les informations de confiance sur le serveur sont compromises et que vous n'avez pas extrait une image du référentiel auparavant, votre client Docker risque d'extraire des informations compromises du serveur d'accréditation. Si les données de confiance sont compromises après que vous avez extrait l'image pour la première fois, lors des extractions suivantes, votre client Docker ne parvient pas à vérifier les données compromises et n'extrait pas l'image. Pour plus d'informations sur le mode d'inspection des données de confiance d'une image, voir [Affichage d'images signées](#trustedcontent_viewsigned).

Pour plus d'informations sur le modèle de sécurité "approuver à la première utilisation", voir [The Update Framework (TUF) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://theupdateframework.github.io/).

## Configuration de votre environnement de contenu sécurisé
{: #trustedcontent_setup}

Par défaut, Docker Content Trust est désactivé. Activez l'environnement Content Trust avant de vous connecter à {{site.data.keyword.registrylong_notm}} et d'utiliser des images signées.
{:shortdesc}

1. Activez la variable d'environnement Docker Content Trust sur votre terminal.

   Linux ou Mac :

   ```
   export DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

   Windows :

   ```
   set DOCKER_CONTENT_TRUST=1
   ```
   {: codeblock}

2. Connectez-vous à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login [--sso]
   ```
   {: pre}

   Si vous disposez d'un ID fédéré, utilisez `ibmcloud login --sso` pour vous connecter. Entrez votre nom d'utilisateur et utilisez l'URL fournie dans votre sortie d'interface de ligne de commande pour extraire votre code d'accès à usage unique. Si la connexion échoue alors que vous omettez l'option `--sso`
et aboutit en incluant l'option `--sso`, ceci indique que votre ID est fédéré.
   {: tip}

3. Ciblez la région à utiliser. Si vous ne connaissez pas le nom de la région, vous pouvez exécuter la commande sans la région puis en sélectionner une.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

4. Connectez-vous à {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

   La sortie vous explique comment exporter la variable d'environnement Docker Content Trust.

   **Exemple**

   ```
   user:~ user$ ibmcloud cr login
    Logging in to 'registry.ng.bluemix.net'...
   Logged in to 'registry.ng.bluemix.net'.

   Pour configurer votre client Docker avec la sécurité du contenu, exportez la variable d'environnement suivante :
    export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
   ```
   {: screen}

5. Copiez et collez la commande de variable d'environnement dans votre terminal. Par exemple :

   ```
   export DOCKER_CONTENT_TRUST_SERVER=https://registry.ng.bluemix.net:4443
   ```
   {: pre}

Vous êtes à présent prêt à envoyer, extraire et gérer des images signées sécurisées.

Au cours de votre session avec Docker Content Trust activé, si vous voulez effectuer une opération avec du contenu sécurisé désactivé (par exemple, extraire une image non signée), utilisez la balise `--disable-content-trust` avec la commande.
{: tip}

## Envoi d'une image signée
{: #trustedcontent_push}

Lorsque vous envoyez par commande push une image signée pour la première fois, Docker crée automatiquement une paire de clés de signature : racine (root) et de référentiel. Pour signer une image dans un référentiel où des images signées ont été envoyées auparavant, vous devez disposer de la clé de signature de référentiel correcte chargées sur la machine qui envoie l'image.
{:shortdesc}

Avant de commencer, [configurez votre espace de nom de registre](/docs/services/Registry/index.html#registry_namespace_add).

1. [Configurez votre environnement de contenu sécurisé](#trustedcontent_setup).

2. [Envoyez votre image par commande push](/docs/services/Registry/index.html#registry_images_pushing). La balise est obligatoire pour du contenu sécurisé. La sortie de la commande est la suivante :

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

3. **Commencez par envoyer par commande push un référentiel signé.** Lorsque vous envoyez une image signée à un nouveau référentiel, la commande crée deux clés de signature, la clé racine (root) et la clé de référentiel, et stocke ces clés sur votre machine locale. Entrez et sauvegarder des phrases passe pour chaque clé, puis [sauvegardez vos clés](#trustedcontent_backupkeys). La sauvegarde de vos clés est essentielle car vos [options de récupération](/docs/services/Registry/ts_index.html#ts_recoveringtrustedcontent) sont limitées.

## Extraction d'une image signée
{: #trustedcontent_pull}

La première fois que vous extrayez une image signée avec Docker Content Trust activé, votre client Docker reconnaît la signature comme digne de confiance. Le client Docker extrait la version signée la plus récente de l'image que vous spécifiez. Les images non signées ou le contenu non approuvé ne sont pas extraits.
{:shortdesc}

1. [Configurez votre environnement de contenu sécurisé](#trustedcontent_setup).

2. Extrayez votre image. Remplacez `<source_image>` par le référentiel de l'image et `<tag>` par la balise de l'image que vous voulez utiliser, par exemple _latest_. Pour répertorier les images disponibles pour extraction, exécutez `ibmcloud cr image-list`.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    Spécifiez la balise lorsque vous extrayez ou envoyez par commande push une image signée. La balise `latest` est la valeur par défaut uniquement quand la sécurité du contenu est désactivée.
    {: tip}

## Gestion du contenu sécurisé
{: #trustedcontent_managetrust}

A l'aide de commandes `docker trust`, vous pouvez voir qui a signé des images et révoquer le statut de contenu sécurisé. Pour exécuter des commandes `docker trust`, vous devez disposer de Docker version 18.03 ou ultérieure.
{:shortdesc}

### Affichage d'images signées
{: #trustedcontent_viewsigned}

Vous pouvez vérifier les versions signées du référentiel ou de la balise d'une image, y compris les informations sur l'ID de clé et le signataire.
{:shortdesc}

1. [Configurez votre environnement de contenu sécurisé](#trustedcontent_setup).

2. Vérifiez les informations de balise, d'historique et de signataire pour chaque image.

   (Facultatif) Spécifiez la balise `<tag>` pour afficher les informations sur cette version de l'image.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### Révocation d'approbation
{: #trustedcontent_revoketrust}

Vous pouvez révoquer le statut de contenu sécurisé d'une image.
{:shortdesc}

Avant de commencer, récupérez la phrase passe de clé de référentiel que vous avez sauvegardé lorsque vous avez [envoyé par commande push le référentiel sécurisé pour la première fois](#trustedcontent_push). Si vous avez besoin d'identifier la clé utilisée pour l'image sécurisée, utilisez la commande `docker view` [](#trustedcontent_viewsigned).

1. [Configurez votre environnement de contenu sécurisé](#trustedcontent_setup).

2. Retirez toutes les métadonnées sécurisées pour le référentiel d'images. Entrez votre phrase passe de clé de référentiel lorsque vous y êtes invité.

   (Facultatif) Spécifiez une balise pour révoquer les métadonnées sécurisées uniquement pour cette version de l'image.

   ```
   docker trust revoke <image>:<tag>
   ```
   {: pre}

3. Vérifiez que l'approbation a été révoquée dans la liste du contenu sécurisé.

   (Facultatif) Incluez la balise si vous souhaitez vérifier le contenu révoqué pour une image balisée.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   Sortie de la commande précédente :

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## Sauvegarde de clés de signature
{: #trustedcontent_backupkeys}

Lorsque vous envoyez une image signée à un nouveau référentiel pour la première fois, Docker Content Trust crée deux clés de signature, la clé racine et la clé de référentiel, et stocke ces clés sur votre machine locale :

- Répertoire Linux et Mac : `~/.docker/trust/private`

- Répertoire Windows : `%HOMEPATH%\.docker\trust\private`

   Si vous avez changé votre répertoire de configuration Docker, recherchez le sous-répertoire `trust` ici.
   {: tip}

Vous devez sauvegarder toutes vos clés, et tout particulièrement la clé racine (root). si une clé est perdue ou compromise, vos [options de récupération](/docs/services/Registry/ts_index.html#ts_recoveringtrustedcontent) sont limitées.

Pour sauvegarder vos clés, consultez la [documentation Docker Content Trust ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys).

## Gestion des signataires de confiance
{: #trustedcontent_signers}

Vous pouvez ajouter et retirer des signataires pour la signature des images d'un référentiel.
{:shortdesc}

### Ajout de signataires à un référentiel sécurisé
{: #trustedcontent_addsigners}

Pour autoriser d'autres utilisateurs à signer des images d'un référentiel, ajoutez les clés de signature de ces utilisateurs à ce référentiel.
{:shortdesc}

**Avant de commencer**

- Les signataires d'image doivent disposer du droit d'envoi par commande push d'images à l'espace de nom.
- Les propriétaires de référentiel et autres signataires doivent disposer de Docker version 18.03 ou ultérieure.
- Créez un référentiel de contenu sécurisé en [envoyant par commande push une image signée](#trustedcontent_push). Les propriétaires de référentiel doivent posséder des clés d'administrateur du référentiel disponibles dans le dossier Docker trust sur leur machine locale. Si vous ne disposez pas de la clé d'administrateur du référentiel, contactez le propriétaire afin qu'il effectue cette tâche pour vous.

Lorsque vous ajoutez un signataire, vous ne pouvez plus utiliser la clé d'administrateur du référentiel pour signer des images dans ce référentiel. Vous devez suspendre la clé privée pour que l'un des signataires approuvés puisse signer. Pour conserver la possibilité de signer des images après l'ajout d'un signataire, suivez les instructions ci-après pour générer et ajouter un rôle signataire pour vous-même.
{:tip}

Pour partager des clés de signature :

1. Si le nouveau signataire n'a pas encore généré de paire de clés, une paire doit être générée et chargée.
  
    a. Générez la clé. Vous pouvez indiquer le nom de votre choix pour `<NAME>`, mais le nom sélectionné est visible lorsqu'une personne inspecte la fiabilité du référentiel. Travaillez avec le propriétaire du référentiel afin de respecter les conventions de dénomination qui pourraient être utilisées par l'organisation et de sélectionner un nom identifiable pour ce signataire.

      ```
      docker trust key generate <NAME>
      ```
      {: pre}
  
    b. Entrez une phrase passe pour la clé privée. Une clé publique (`.pub`) est générée, et la clé privée correspondante est automatiquement chargée dans la configuration sécurisée Docker.
  
    c. Le nouveau signataire doit envoyer la clé publique au propriétaire du référentiel.

2. Le propriétaire du référentiel doit ajouter la clé du signataire au référentiel.

    a. [Configurez l'environnement de contenu sécurisé](#trustedcontent_setup).

    b. Ajoutez la clé du signataire au référentiel.

      ```
      docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}

3. Le signataire peut configurer son environnement et signer une image.

    a. [Configurez l'environnement de contenu sécurisé](#trustedcontent_setup).

    b. Le signataire doit signer une image. Lorsque vous y êtes invité, entrez la phrase passe pour la clé privée.

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4. Pour vérifier que le signataire a été ajouté, voir [Affichage d'images signées](#trustedcontent_viewsigned).

### Retrait d'un signataire d'un référentiel
{: #trustedcontent_removesigner}

Si vous ne souhaitez plus qu'un signataire puisse signer des images dans votre référentiel, vous pouvez le retirer.
{:shortdesc}

Avant de commencer, les propriétaires de référentiel et autres signataires doivent disposer de Docker version 18.03 ou ultérieure.

Si vous retirez un signataire, le serveur d'accréditation n'approuve pas ses versions signées de l'image. Pour s'assurer que l'image peut être extraite après le retrait du signataire, vérifiez que ce dernier n'a pas signé la version la plus récente de l'image avant de poursuivre. Si le signataire à signé la version la plus récente de l'image, envoyez par commande push une mise à jour de l'image et signez-la avec votre clé avant de poursuivre.
{:tip}

Pour retirer un signataire :

1. [Configurez votre environnement de contenu sécurisé](#trustedcontent_setup).

2. Retirez le signataire.

   ```
   docker trust signer remove <NAME> <repository>
   ```
   {: pre}

3. Pour vérifier que le signataire a été retiré, affichez les données de confiance de l'image et vérifiez que le signataire ne figure plus dans la liste. Pour plus d'informations sur l'affichage des donnés de confiance, voir [Affichage d'images signées](#trustedcontent_viewsigned).
