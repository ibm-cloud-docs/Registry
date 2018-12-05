---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Incluindo imagens para seu namespace
{: #registry_images_}

É possível armazenar e compartilhar, de forma segura, imagens do Docker com outros usuários ao incluir imagens em seu namespace no
{{site.data.keyword.registrylong}}.
{:shortdesc}

Todas as imagens que desejar incluir no namespace deverão existir primeiro no computador local. É possível fazer download
(puxar) de uma imagem de outro repositório para o computador local ou construir a sua própria imagem de um Dockerfile usando o comando `build` do Docker. Para incluir uma imagem em seu namespace, deve-se fazer upload da (enviar por push) imagem local para seu namespace no
{{site.data.keyword.registrylong_notm}}.

Não coloque informações pessoais em imagens de contêiner, nomes de namespace, campos de descrição (por exemplo, em tokens de registro) ou em qualquer dado de configuração de imagem (por
exemplo, nomes ou rótulos de imagem).
{:tip}

## Puxando imagens de outro registro
{: #registry_images_pulling}

É possível puxar (fazer download) de uma imagem de qualquer origem de registro privado ou público e, depois, identificá-la para
uso posterior no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

<img src="images/images_pull.svg" width="800" style="width:800px;" alt="Puxe uma imagem de um registro privado ou público para o seu computador."/>

**Antes de iniciar**

- [Instale a CLI](registry_setup_cli_namespace.html#registry_cli_install) para trabalhar com imagens em seu namespace.
- [Configure seu próprio namespace no {{site.data.keyword.registrylong_notm}}](registry_setup_cli_namespace.html#registry_namespace_add).
- [Certifique-se de que seja possível executar comandos do Docker sem permissões raiz](https://docs.docker.com/engine/installation/linux/linux-postinstall). Caso o cliente Docker esteja configurado para requerer permissões raiz, deve-se executar os comandos
`ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` com `sudo`.

  Caso as permissões para executar comandos do Docker mudem sem privilégios de administrador,
deve-se executar o comando `ibmcloud login` novamente.

Faça download da imagem, veja [Puxar uma imagem](index.html#registry_images_pulling) na documentação de Introdução.

Se você receber uma mensagem `unauthorized: authentication required` ou `denied: requested access to the resource is denied`, execute o comando `ibmcloud cr login`.
{:tip}

Depois de puxar uma imagem e identificá-la para o namespace, é possível fazer upload (enviar por
push) da imagem do computador local para o namespace.

## Enviando por push imagens do Docker para seu namespace
{: #registry_images_pushing}

É possível enviar por push (upload) uma imagem para seu namespace no {{site.data.keyword.registrylong_notm}} para armazenar e compartilhar com segurança sua imagem
com outros usuários.
{:shortdesc}

<img src="images/images_push.svg" width="800" style="width:800px;" alt="Envie uma imagem por push do seu computador para o seu registro privado."/>

**Antes de iniciar**

- [Instale a CLI](registry_setup_cli_namespace.html#registry_cli_install) para trabalhar com imagens em seu namespace.
- [Configure seu próprio namespace no registro privado do {{site.data.keyword.registrylong_notm}}](registry_setup_cli_namespace.html#registry_namespace_add).
- [Puxe](#registry_images_pulling) ou [construa](#registry_images_creating) uma imagem no
computador local e identifique-a com as informações do namespace.
- [Certifique-se de que seja possível executar comandos do Docker sem permissões raiz](https://docs.docker.com/engine/installation/linux/linux-postinstall). Caso o cliente Docker esteja configurado para requerer permissões raiz, deve-se executar os comandos
`ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` com `sudo`.

  Caso as permissões para executar comandos do Docker mudem sem privilégios de administrador,
deve-se executar o comando `ibmcloud login` novamente.

Para fazer upload de uma imagem (enviá-la por push), conclua as etapas a seguir:

1. Efetue login no CLI.

   ```
   ibmcloud cr login
   ```
   {: pre}

   Deve-se efetuar login se você puxa uma imagem de seu {{site.data.keyword.registrylong_notm}} privado.
  {:tip}

2. Para visualizar todos os namespaces disponíveis em sua conta, execute o comando `ibmcloud cr namespace-list`.
3. [Faça upload da imagem para seu namespace.](index.html#registry_images_pushing)

   Se você receber uma mensagem `unauthorized: authentication required` ou `denied: requested access to the resource is denied`, execute o comando `ibmcloud cr login`.
   {:tip}

Após enviar por push sua imagem para seu registro privado, será possível executar uma das tarefas a seguir:

- [Gerenciar a segurança com o Vulnerability Advisor](../va/va_index.html) para localizar informações sobre possíveis problemas e vulnerabilidade de segurança.
- [Criar um cluster e usar essa imagem para implementar um contêiner](/docs/containers/container_index.html#container_index)
para o cluster no {{site.data.keyword.containerlong_notm}}.

## Copiando imagens entre registros
{: #registry_images_copying}

É possível puxar uma imagem de um registro em uma região e enviá-la por push para um registro em outra região para que seja possível
compartilhar a imagem com usuários em ambas as regiões.
{:shortdesc}

<img src="images/images_copy.svg" width="800" style="width:800px;" alt="Copie uma imagem de qualquer registro privado ou público para seu registro privado do {{site.data.keyword.Bluemix_notm}}."/>

**Antes de iniciar**

- [Instale a CLI](registry_setup_cli_namespace.html#registry_cli_install) para trabalhar com imagens em seu namespace.
- [Configure seu próprio namespace no registro privado do {{site.data.keyword.registrylong_notm}}](registry_setup_cli_namespace.html#registry_namespace_add).
- [Certifique-se de que seja possível executar comandos do Docker sem permissões raiz](https://docs.docker.com/engine/installation/linux/linux-postinstall). Caso o cliente Docker esteja configurado para requerer permissões raiz, deve-se executar os comandos
`ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` com `sudo`.

  Caso as permissões para executar comandos do Docker mudem sem privilégios de administrador,
deve-se executar o comando `ibmcloud login` novamente.

Para copiar uma imagem entre dois registros, conclua as etapas a seguir:

1. [Puxe uma imagem a partir de um registro](#registry_images_pulling).
2. [Empurre a imagem para outro registro](#registry_images_pushing). Certifique-se de usar o nome de domínio correto para a nova região que você está destinando.

Após copiar sua imagem, será possível fazer uma das tarefas a seguir:

- [Gerenciando a segurança de imagens com o Vulnerability Advisor](../va/va_index.html) para localizar informações sobre potenciais problemas e vulnerabilidades de segurança.
- [Criar um cluster e usar essa imagem para implementar um contêiner](/docs/containers/container_index.html#container_index)
para o cluster no {{site.data.keyword.containerlong_notm}}.

## Construindo imagens do Docker para usá-las com seu namespace
{: #registry_images_creating}

É possível construir uma imagem Docker diretamente no {{site.data.keyword.Bluemix_notm}} ou criar uma imagem Docker
própria no computador local e transferi-la por upload (enviar por push) para o namespace no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Antes de iniciar**

- [Instale a CLI](registry_setup_cli_namespace.html#registry_cli_install) para trabalhar com imagens em seu namespace.
- [Configure seu próprio namespace no registro privado do {{site.data.keyword.registrylong_notm}}](registry_setup_cli_namespace.html#registry_namespace_add).
- [Certifique-se de que seja possível executar comandos do Docker sem permissões raiz](https://docs.docker.com/engine/installation/linux/linux-postinstall). Caso o cliente Docker esteja configurado para requerer permissões raiz, deve-se executar os comandos
`ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` com `sudo`.

  Caso as permissões para executar comandos do Docker mudem sem privilégios de administrador,
deve-se executar o comando `ibmcloud login` novamente.

Uma imagem do Docker é a base para cada contêiner que você cria. Uma imagem é criada por meio
de um Dockerfile, que é um arquivo que contém instruções para construir a imagem. Um Dockerfile pode
referenciar os artefatos de construção em suas instruções que são armazenadas separadamente, como um app, a configuração
do app e suas dependências.

Se você deseja aproveitar os recursos de cálculo do {{site.data.keyword.Bluemix_notm}} e a conexão de Internet ou o Docker não está instalado em sua estação de trabalho, construa sua imagem diretamente no {{site.data.keyword.Bluemix_notm}}. Se você precisa acessar recursos em sua construção que estão em servidores sob seu firewall, construa sua imagem localmente.

Para construir sua própria imagem do Docker, conclua as etapas a seguir:

1. Crie um diretório local no qual você deseja armazenar o contexto de compilação. O contexto de compilação contém seu Dockerfile e artefatos de construção relacionados, como o código do app. Navegue para esse diretório em uma janela de linha de comandos.
2. Crie um Dockerfile.
    1. Crie um Dockerfile em seu diretório local.

        ```
        touch Dockerfile
        ```
        {: pre}

    2. Use um editor de texto para abrir o Dockerfile. Deve-se incluir, no mínimo, a imagem base para construir a imagem. Substitua
_&lt;source_image&gt;_ e _&lt;tag&gt;_ pelo repositório de imagem e pela tag que você
deseja usar. Se você estiver usando uma imagem de outro registro privado, defina o caminho completo para a imagem nesse registro
privado.

       ```
       FROM <source_image>:<tag>
       ```
       {: pre}

       **Exemplo**
     Para criar um Dockerfile que seja baseado na imagem pública do {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty (ibmliberty), use o código a seguir:

       ```
       FROM registry.<region>.bluemix.net/ibmliberty:latest
    LABEL description="This is my test Dockerfile"
    EXPOSE 9080
       ```
       {: pre}

       Este exemplo inclui um rótulo nos metadados da imagem e expõe a porta 9080. Para obter mais instruções do Dockerfile que podem ser usadas, consulte a
[Referência do Dockerfile](https://docs.docker.com/engine/reference/builder/).

3. Decida sobre um nome para sua imagem. O nome da imagem deve estar no formato a seguir:

   ```
   registry.<region>.bluemix.net/<my_namespace>/<repo_name>:<tag>
   ```
   {: pre}

   em que _&lt;my_namespace&gt;_ é sua informação de namespace, _&lt;repo_name&gt;_ é o nome de seu repositório e _&lt;tag&gt;_ é a versão que você deseja usar para sua imagem. Para localizar seu namespace, execute o comando `ibmcloud cr namespace-list`.

4. Anote o caminho para o diretório que contém o Dockerfile. Se você executa os comandos nas etapas a seguir enquanto seu diretório ativo está configurado para onde o contexto de compilação é armazenado, é possível substituir _&lt;directory&gt;_ por um ponto (.).
5. Escolha construir a imagem diretamente no {{site.data.keyword.Bluemix_notm}} ou construir e testar a imagem localmente
antes de enviá-la por push para o {{site.data.keyword.Bluemix_notm}}.
   - Para construir a imagem diretamente no {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir:

     ```
     ibmcloud cr build -t <image_name> <directory>
     ```
     {: pre}

     em que _&lt;image_name&gt;_ é o nome de sua imagem e _&lt;directory&gt;_ é o caminho para o diretório. Se você executar o comando quando seu diretório ativo estiver configurado para onde seu contexto de compilação estiver armazenado, será possível substituir _&lt;directory&gt;_ por um ponto (.).
  
     Para obter mais informações sobre o comando `ibmcloud cr build`, consulte [CLI do {{site.data.keyword.registrylong_notm}}](/docs/services/Registry/registry_cli.html#bx_cr_build).

   - Para construir e testar sua imagem localmente antes de enviá-la por push para o {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:
      1. Construa a imagem do Dockerfile no computador local e identifique-a com o nome da imagem.

         ```
         docker build -t <image_name> <directory>
         ```
         {: pre}

         em que _&lt;image_name&gt;_ é o nome de sua imagem e _&lt;directory&gt;_ é o caminho para o diretório.

      2. Opcional: teste a imagem no computador local antes de enviá-la por push para o namespace.

         ```
         docker run <image_name>
         ```
         {: pre}

         Substitua _&lt;image_name&gt;_ pelo nome de sua imagem.

      3. Após criar a imagem e identificá-la para o seu namespace, [será possível enviar a imagem para o registro privado do seu namespace](#registry_images_pushing).

Para usar o Vulnerability Advisor para verificar a segurança de sua imagem, veja [Gerenciando a segurança de imagens com o Vulnerability Advisor](../va/va_index.html).

## Excluindo imagens de seu repositório privado do  {{site.data.keyword.Bluemix_notm}}
{: #registry_images_remove}

É possível excluir imagens indesejadas de seu repositório privado usando a interface gráfica com o usuário (GUI) ou a CLI.
{:shortdesc}

Se desejar excluir um repositório privado e suas imagens associadas, consulte [Excluindo um repositório privado e quaisquer imagens associadas](#registry_repo_remove).

As imagens públicas da {{site.data.keyword.IBM_notm}} não podem ser excluídas de seu repositório privado do {{site.data.keyword.Bluemix_notm}} e não são consideradas para sua cota.

A exclusão de uma imagem não pode ser desfeita. A exclusão de uma imagem que está sendo usada por uma implementação existente pode causar falha de aumento de capacidade, reagendamento ou ambos.
{:tip}

### Excluindo imagens de seu repositório privado do {{site.data.keyword.Bluemix_notm}} usando a CLI
{: #registry_images_remove_cli}

É possível excluir imagens indesejadas de seu repositório privado usando a CLI.
{:shortdesc}

A exclusão de uma imagem não pode ser desfeita. A exclusão de uma imagem que está sendo usada por uma implementação existente pode causar falha de aumento de capacidade, reagendamento ou ambos.
{:tip}

Para excluir uma imagem usando a CLI, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} executando o comando `ibmcloud login`.
2. Para excluir uma imagem, execute o comando a seguir:

   ```
   ibmcloud cr image-rm IMAGE
   ```
   {: pre}

   Em que _IMAGE_ é o nome da imagem que você deseja remover, no formato `repository:tag`.

   Se uma tag não for especificada no nome da imagem, a imagem identificada por último (`latest`) será excluída, por padrão. É possível excluir múltiplas imagens listando cada caminho de registro privado do {{site.data.keyword.Bluemix_notm}} no comando com um espaço entre cada caminho.

   Para localizar os nomes de suas imagens, execute `ibmcloud cr image-list`. Combine o conteúdo das colunas Repositório e Tag para criar o nome da imagem no formato `repository:tag`.
   {:tip}

3. Execute o comando a seguir para ver se a imagem foi excluída e verifique se ela não é mostrada na lista.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

### Excluindo imagens de seu repositório privado do {{site.data.keyword.Bluemix_notm}} usando a GUI
{: #registry_images_remove_gui}

É possível excluir imagens indesejadas de seu repositório de imagem privada usando a interface gráfica com o usuário (GUI).
{:shortdesc}

A exclusão de uma imagem não pode ser desfeita. A exclusão de uma imagem que está sendo usada por uma implementação existente pode causar falha de aumento de capacidade, reagendamento ou ambos.
{:tip}

Para excluir uma imagem usando a GUI, conclua as etapas a seguir:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}
([https://console.bluemix.net](https://console.bluemix.net)) com seu IBMid.
2. Se você tiver múltiplas contas do {{site.data.keyword.Bluemix_notm}}, selecione a conta e região que você deseja usar por meio do menu de conta.
3. Clique em **Catálogo**.
4. Selecione a categoria **Contêineres** e clique no tile **Registro de contêiner**.
5. Clique em **Imagens**. Uma lista de suas imagens é exibida.
6. Na linha que contém a imagem que você deseja excluir, selecione a caixa de opção.

   Assegure-se de selecionar a imagem correta, porque essa ação não pode ser desfeita.
   {: tip}

7. Clique em **Excluir imagem**.

## Excluindo um repositório privado e quaisquer imagens associadas
{: #registry_repo_remove}

É possível excluir repositórios privados que não são mais necessários e quaisquer imagens associadas usando a interface gráfica com o usuário (GUI).
{:shortdesc}

Quando você exclui um repositório, todas as imagens nesse repositório são excluídas. Essa ação não pode ser desfeita.
{:tip}

**Antes de iniciar**

Deve-se fazer backup de todas as imagens que deseja manter.

Para excluir um repositório privado usando a GUI, conclua as etapas a seguir:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}
([https://console.bluemix.net](https://console.bluemix.net)) com seu IBMid.
2. Se você tiver múltiplas contas do {{site.data.keyword.Bluemix_notm}}, selecione a conta e região que você deseja usar por meio do menu de conta.
3. Clique em **Catálogo**.
4. Selecione a categoria **Contêineres** e clique no tile **Registro de contêiner**.
5. Clique em **Repositórios**. Uma lista de seus repositórios privados é exibida.
6. Na linha que contém o repositório privado que você deseja excluir, selecione a caixa de opção.

    Assegure-se de que tenha selecionado o repositório correto, porque essa ação não pode ser desfeita.
    {: tip}

7. Clique em **Excluir repositório**.
