---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-05"

keywords: IBM Cloud Container Registry, Docker Content Trust, keys, trusted content, signing, signing images, repository keys, 

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

# Imagens de assinatura para conteúdo confiável
{: #registry_trustedcontent}

O {{site.data.keyword.registrylong}} fornece tecnologia de conteúdo confiável para que você possa assinar imagens para assegurar a integridade de imagens no namespace de registro. Ao puxar e enviar por push as imagens assinadas, é possível verificar se elas foram enviadas por push pela parte correta, como as ferramentas de integração contínua (CI). Para usar esse recurso, deve-se ter o Docker versão 18.03 ou mais recente. É possível saber mais ao revisar o [Docker Content Trust ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.docker.com/engine/security/trust/content_trust/) e a documentação do [Projeto do tabelião público![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/theupdateframework/notary).
{:shortdesc}

Quando você envia a imagem por push com conteúdo confiável ativado, o cliente Docker também envia por push um objeto de metadados assinado para o servidor de confiança do {{site.data.keyword.cloud_notm}}. Ao puxar uma imagem identificada com o Docker Content Trust ativado, o cliente Docker entra em contato com o servidor de confiança para estabelecer a versão assinada mais recente da tag solicitada, verifica a assinatura de conteúdo e faz download da imagem assinada.

Um nome de imagem é composto de um repositório e uma tag. Quando você estiver usando conteúdo confiável, cada
repositório usará uma chave de assinatura exclusiva. Cada tag de um repositório usa a chave que pertence ao repositório. Se você tiver várias equipes publicando conteúdo, cada uma em seu próprio repositório dentro de seus namespaces do {{site.data.keyword.registrylong_notm}}, cada equipe poderá usar suas próprias chaves para assinar seu conteúdo para que seja possível verificar se cada imagem é produzida pela equipe apropriada.

Um repositório pode conter tanto conteúdo assinado quanto não assinado. Quando o Docker Content Trust está ativado, é possível acessar o conteúdo assinado em um repositório, mesmo quando há outro conteúdo não assinado ao lado dele.

As imagens têm assinaturas separadas para nomes de domínio antigos (`registry.bluemix.net`) e novos (`icr.io`). As assinaturas existentes funcionam quando a imagem é extraída do nome de domínio antigo. Se você desejar puxar o conteúdo assinado por meio do novo nome de domínio, deverá assinar novamente a imagem no novo nome de domínio, `icr.io`; consulte [Assinando novamente uma imagem para o novo nome de domínio](#trustedcontent_resign).
{: note}

O Docker Content Trust usa um modelo de segurança trust on first (TOFU). A chave do repositório é puxada do servidor de confiança ao puxar uma imagem assinada de um repositório pela primeira vez e essa chave é usada para verificar imagens desse repositório no futuro. Deve-se verificar se você confia no servidor de confiança ou na imagem e em seu publicador antes de puxar o repositório pela primeira vez. Se as informações de confiança no servidor estiverem comprometidas e você não tiver puxado uma imagem do repositório antes, seu cliente Docker poderá puxar as informações comprometidas do servidor de confiança. Se os dados de confiança estiverem comprometidos depois que você puxar a imagem pela primeira vez, nos pulls subsequentes, o cliente Docker não verificará os dados comprometidos e não puxará a imagem. Para obter mais informações sobre como inspecionar dados de confiança para uma imagem, consulte [Visualizando imagens assinadas](#trustedcontent_viewsigned).

Para obter mais informações sobre o modelo de segurança TOFU, consulte [A estrutura de atualização ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://theupdateframework.github.io/).

## Configurando seu ambiente de conteúdo confiável
{: #trustedcontent_setup}

Por padrão, o Docker Content Trust fica desativado. Ative o ambiente do Content Trust antes de efetuar login no {{site.data.keyword.registrylong_notm}} e trabalhar com imagens assinadas.
{:shortdesc}

1. Ative a variável de ambiente do Docker Content Trust em seu terminal.

   Para Linux ou Mac:

   ```
   Export DOCKER_CONTENT_TRUST= 1
   ```
   {: codeblock}

   Para Windows:

   ```
   Conjunto de DOCKER_CONTENT_TRUST= 1
   ```
   {: codeblock}

2. Efetue login na CLI do {{site.data.keyword.cloud_notm}}.

   ```
   ibmcloud login [ -- sso ]
   ```
   {: pre}

   Se você tiver um ID federado, use `ibmcloud login --sso` para efetuar login. Insira seu nome do usuário e use a URL fornecida na saída da CLI para recuperar sua senha descartável. Se você tiver um ID federado, o login falhará sem o `--sso` e será bem-sucedido com a opção `--sso`.
   {: tip}

3. Tenha como destino a região que você deseja usar. Se você não souber o nome da região, execute o comando sem a região e escolha uma.

   ```
   ibmcloud cr region-set <region>
   ```
   {: pre}

4. Efetue login no {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

   A saída instrui você a exportar a variável de ambiente do Docker Content Trust.

   Por exemplo:

   ```
   user:~ user$ ibmcloud cr login
   Logging in to 'us.icr.io'...
   Logged in to 'us.icr.io'.

   Para configurar seu cliente Docker com confiança de conteúdo,
   exporte a variável de ambiente a seguir:
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io:4443
   ```
   {: screen}

5. Copie e cole o comando da variável de ambiente em seu terminal. Por exemplo:

   ```
   export DOCKER_CONTENT_TRUST_SERVER=https://us.icr.io: 4443
   ```
   {: pre}

Agora você está pronto para enviar por push, puxar e gerenciar imagens assinadas confiáveis.

Durante a sessão com o Docker Content Trust ativado, se você desejar executar uma operação com conteúdo confiável desativado
(como puxar uma imagem não assinada), use a sinalização `--disable-content-trust` com o comando.
{: tip}

## Enviando uma imagem assinada
{: #trustedcontent_push}

Quando você envia uma imagem assinada por push pela primeira vez, o Docker cria automaticamente um par de chaves de assinatura: raiz e repositório. Para assinar uma imagem em um repositório no qual as imagens assinadas foram enviadas por push anteriormente, deve-se ter a chave de assinatura do repositório correto carregada na máquina que está enviando a imagem por push.
{:shortdesc}

Antes de iniciar, [configure o namespace de registro](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add).

1. [Configurar o ambiente de conteúdo confiável](#trustedcontent_setup).

2. [Empurre a imagem](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing). A tag é obrigatória para o conteúdo confiável. Na saída de comando, você verá:

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

3. Na primeira vez em que você enviar por push uma imagem assinada para um novo repositório, o comando criará duas chaves de assinatura, a chave raiz e a chave do repositório, e as armazenará em sua máquina local. Insira e salve passphrases seguras para cada chave e, em seguida, [faça backup das chaves](#trustedcontent_backupkeys). Fazer backup das chaves é crítico porque as [opções de recuperação](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent) são limitadas.

   Essa ação é necessária somente na primeira vez em que você enviar por push um repositório assinado.
   {: tip}

## Puxando uma imagem assinada
{: #trustedcontent_pull}

A primeira vez que você puxa uma imagem assinada com o Docker Content Trust ativado, o cliente Docker reconhece a assinatura como confiável. O cliente Docker puxa a versão assinada mais recente da imagem especificada. Imagens não assinadas ou conteúdo não confiável não são puxados.
{:shortdesc}

1. [Configurar o ambiente de conteúdo confiável](#trustedcontent_setup).

2. Puxe sua imagem. Substitua `<source_image>` pelo repositório da imagem e `<tag>` pela tag da imagem que você deseja usar, como _latest_. Para listar imagens disponíveis a serem puxadas, execute `ibmcloud cr image-list`.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    Especifique a tag quando enviar por push ou puxar uma imagem assinada. A tag `latest` somente é usada como padrão quando a confiança de conteúdo está desativada.
    {: tip}

## Assinando novamente uma imagem para o novo nome de domínio
{: #trustedcontent_resign}

Para assinar novamente a imagem para o novo nome de domínio, `icr.io`, deve-se puxar, identificar e enviar por push a imagem.
{:shortdesc}

1. Puxe sua imagem assinada por meio do nome de domínio antigo. Substitua `<source_image>` pelo repositório da imagem e `<tag>` pela tag da imagem que você deseja usar, como _latest_. Para listar imagens disponíveis a serem puxadas, execute `ibmcloud cr image-list`.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

    Especifique a tag quando enviar por push ou puxar uma imagem assinada. A tag `latest` somente é usada como padrão quando a confiança de conteúdo está desativada.
    {: tip}

2. Execute o comando `docker tag` para o novo nome de domínio. Substitua `<old_domain_name>` pelo nome de domínio antigo, `<new_domain_name>` pelo novo nome do domínio, `<repository>` pelo nome do seu repositório e `<tag>` pelo nome da sua tag.

   ```
   docker tag <old_domain_name>/<repository>:<tag> <new_domain_name>/<repository>:t<tag>
   ```
   {: pre}

3. Envie por push sua imagem usando o novo nome de domínio, consulte [Enviar por push imagens do Docker para seu namespace](/docs/services/Registry?topic=registry-getting-started#gs_registry_images_pushing). A tag é obrigatória para o conteúdo confiável. Na saída de comando, você verá:

   ```
   Signing and pushing image metadata.
   ```
   {: screen}

## Gerenciando conteúdo confiável
{: #trustedcontent_managetrust}

Usando os comandos `docker trust`, é possível visualizar quem assinou as imagens e revogar o status do
conteúdo de confiança. Para executar os comandos `docker trust`, deve-se ter o Docker 18.03 ou mais recente.
{:shortdesc}

### Visualizando as imagens assinadas
{: #trustedcontent_viewsigned}

É possível revisar as versões assinadas de um repositório de imagem ou tag, incluindo informações sobre o ID da chave e o assinante.
{:shortdesc}

1. [Configurar o ambiente de conteúdo confiável](#trustedcontent_setup).

2. Revise a tag, a compilação e as informações de assinante de cada imagem.

   (Opcional) Especifique a tag `<tag>` para ver informações sobre essa versão da imagem.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

### Revogando confiança
{: #trustedcontent_revoketrust}

É possível revogar o status de conteúdo confiável de uma imagem.
{:shortdesc}

Antes de iniciar, recupere a passphrase da chave de repositório salva quando [enviou por push pela primeira vez o repositório confiável](#trustedcontent_push). Se precisar identificar qual chave será usada para a imagem confiável, use o [comando](#trustedcontent_viewsigned) `docker view`.

1. [Configurar o ambiente de conteúdo confiável](#trustedcontent_setup).

2. Remova todos os metadados confiáveis do repositório de imagem. Insira a passphrase da chave de repositório quando solicitada.

   (Opcional) Especifique uma tag para revogar metadados confiáveis apenas para essa versão da imagem.

   ```
   docker trust revoke <image>:<tag>
   ```
   {: pre}

3. Verifique se a confiança foi revogada na lista de conteúdo confiável.

   (Opcional) Se você desejar verificar o conteúdo revogado para uma imagem identificada, inclua a tag.

   ```
   docker trust inspect --pretty <image>:<tag>
   ```
   {: pre}

   Saída do comando anterior:

   ```
   No signatures or cannot access <image>:<tag>
   ```
   {: screen}

## Fazendo Backup de chaves de assinatura
{: #trustedcontent_backupkeys}

Quando você enviar pela primeira vez uma imagem assinada para um novo repositório, o Docker Content Trust criará duas chaves de assinatura, a chave raiz e a chave do repositório e as armazenará em sua máquina local:

- Diretório Linux e Mac: `~/.docker/trust/private`

- Diretório do Windows: `%HOMEPATH%\.docker\trust\private`

   Se você tiver mudado o diretório de configuração do Docker, procure o subdiretório `trust` lá.
   {: tip}

Deve-se fazer backup de todas as chaves, especialmente da chave raiz. Se uma chave for perdida ou comprometida, as [opções de recuperação](/docs/services/Registry?topic=registry-ts_index#ts_recoveringtrustedcontent) serão limitadas.

Para fazer backup das chaves, consulte [Documentação do Docker Content Trust ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.docker.com/engine/security/trust/trust_key_mng/#back-up-your-keys).

## Gerenciando assinantes confiáveis
{: #trustedcontent_signers}

É possível incluir e remover assinantes de imagens de assinatura em um repositório.
{:shortdesc}

### Incluindo assinantes para um repositório confiável
{: #trustedcontent_addsigners}

Para permitir que outros usuários assinem imagens em um repositório, inclua as chaves de assinatura para esses usuários nesse repositório.
{:shortdesc}

Antes de iniciar, conclua as tarefas a seguir:

- Os assinantes de imagem devem ter permissão para enviar imagens por push para o namespace.
- Os proprietários do repositório e os assinantes adicionais devem ter o Docker 18.03 ou mais recente instalado.
- Crie um repositório de conteúdo confiável [enviando uma imagem assinada por push](#trustedcontent_push). Os proprietários do repositório devem ter as chaves de administrador de repositório para o repositório disponível na pasta de confiança do Docker na máquina local. Se você não tiver a chave de administrador do repositório, entre em contato com o proprietário para executar essa tarefa para você.

Ao incluir um assinante, não é mais possível usar a chave de administrador do repositório para assinar imagens nesse repositório. Deve-se manter a chave privada para um dos assinantes aprovados assinar. Para reter a capacidade de assinar imagens depois de incluir um assinante, siga estas instruções novamente para gerar e incluir uma função de assinante para si mesmo.
{:tip}

Para compartilhar chaves de assinatura:

1. Se o novo assinante ainda não tiver gerado um par de chaves, um par de chaves deverá ser gerado e carregado.
  
    a. Gere a chave. É possível inserir qualquer nome para `<NAME>`, no entanto, o nome que você selecionar ficará visível quando alguém inspecionar a confiança no repositório. Trabalhe com o proprietário do repositório para atender quaisquer convenções de nomenclatura que possam ser usadas pela organização e para selecionar um nome que seja identificável para esse assinante.

      ```
      docker trust key generate <NAME>
      ```
      {: pre}
  
    b. Insira uma passphrase para a chave privada. Uma chave pública (`.pub`) é gerada e a chave privada correspondente é carregada automaticamente na configuração de confiança do Docker.
  
    c. O novo assinante deve enviar ao proprietário do repositório a chave pública.

2. O proprietário do repositório deve incluir a chave do assinante no repositório.

    a. [Configure o ambiente de conteúdo confiável](#trustedcontent_setup).

    b. Inclua a chave do assinante no repositório.

      ```
      docker trust signer add --key <NAME>.pub <NAME> <repository>
      ```
      {: pre}

3. O assinante pode configurar seu ambiente e assinar uma imagem.

    a. [Configure o ambiente de conteúdo confiável](#trustedcontent_setup).

    b. O assinante deve assinar uma imagem. Quando solicitado, insira a passphrase para a chave privada.

      ```
      docker trust sign <repository>:<tag>
      ```
      {: pre}

4. Para verificar se o assinante foi incluído, consulte [Visualizando as imagens assinadas](#trustedcontent_viewsigned).

### Removendo um signatário de um repositório
{: #trustedcontent_removesigner}

Se não desejar mais que um assinante possa assinar imagens em seu repositório, será possível removê-lo como assinante.
{:shortdesc}

Antes de iniciar, os proprietários do repositório e os assinantes adicionais devem ter o Docker 18.03 ou mais recente instalado.

Se você remover um assinante, o servidor de confiança não confiará em suas versões assinadas da imagem. Para garantir que a imagem possa ser puxada após a remoção do assinante, certifique-se de que o assinante não tenha assinado a versão mais recente da imagem antes de continuar. Se o assinante tiver assinado a versão mais recente da imagem, envie por push uma atualização para a imagem e a assine usando sua chave antes de continuar.
{:tip}

Para remover um assinante:

1. [Configurar o ambiente de conteúdo confiável](#trustedcontent_setup).

2. Remova o assinante.

   ```
   docker trust signer remove <NAME> <repository>
   ```
   {: pre}

3. Para verificar se o assinante foi removido, visualize os dados de confiança da imagem e verifique se ele não está mais listado. Para obter mais informações sobre como visualizar dados de confiança, consulte [Visualizando imagens assinadas](#trustedcontent_viewsigned).
