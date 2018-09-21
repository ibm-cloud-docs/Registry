---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Automatizando o acesso ao {{site.data.keyword.registrylong_notm}}
{: #registry_access}

É possível usar tokens de registro ou uma chave API do {{site.data.keyword.iamlong}} (IAM) para automatizar o acesso a seus namespaces do {{site.data.keyword.registrylong_notm}} de forma que possa enviar por push e fazer pull das imagens.
{:shortdesc}

Está tentando usar suas imagens de registro em implementações do Kubernetes? Verifique [Acessando imagens em outros namespaces, {{site.data.keyword.Bluemix_notm}} regiões e contas do Kubernetes](/docs/containers/cs_images.html#other).
{: tip}

As chaves API são vinculadas à sua conta e podem ser usadas no {{site.data.keyword.Bluemix_notm}} para que você não precise de credenciais diferentes para cada serviço. É possível usar a chave API na CLI ou como parte de automação para efetuar login como sua identidade do usuário.

Os tokens de registro têm o escopo definido somente para {{site.data.keyword.registrylong_notm}}. É possível limitá-los ao acesso somente leitura e escolher se eles estão expirando ou não expirando.

Para obter mais informações sobre chaves API do {{site.data.keyword.registrylong_notm}}, veja [Trabalhando com chaves API](/docs/iam/apikeys.html#manapikey).

Antes de iniciar, [instale o {{site.data.keyword.registrylong_notm}} e a CLI do Docker](registry_setup_cli_namespace.html#registry_cli_install).


## Automatizando o acesso aos seus namespaces usando chaves API
{: #registry_api_key}

É possível usar as chaves API para automatizar o push e o pull de imagens do Docker para/de seus namespaces.
{:shortdesc}

### Criando uma chave API
{: #registry_api_key_create}

É possível criar uma chave API que pode então ser usada para efetuar login no seu registro. 
{:shortdesc}

É possível criar tanto chaves API do usuário quanto chaves API do ID de serviço.

-  Para criar uma chave API do ID de serviço, consulte [Criando uma chave API para um ID de serviço](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id).
-  Para criar uma chave API do usuário, consulte [Criando uma chave API](/docs/iam/userid_keys.html#creating-an-api-key).


### Usando uma chave API para automatizar o acesso
{: #registry_api_key_use}

É possível usar uma chave API para automatizar o acesso a seus namespaces no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Use a chave API para efetuar login no seu registro executando o comando do Docker a seguir. Substitua &lt;your_apikey&gt; por sua chave API e substitua &lt;registry_url&gt; pela URL para o registro no qual seus namespaces estão configurados.

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Para obter informações de referência sobre o comando, consulte
[Criar uma nova chave API da plataforma {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/ibmcloud/cli_api_policy.html#ibmcloud_iam_api_key_create).


## Automatizando o acesso aos seus namespaces usando tokens
{: #registry_tokens}

É possível usar tokens para automatizar o push e o pull de imagens do Docker e de seus namespaces do {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Todos em posse de um token de registro podem acessar informações protegidas. Criando um token para sua conta do {{site.data.keyword.Bluemix_notm}}, é possível conceder acesso a todos os namespaces que você configurar em uma região para usuários fora de sua conta do {{site.data.keyword.Bluemix_notm}}. Cada usuário ou app com esse token poderá enviar imagens para seus namespaces e extrair deles sem instalar o plug-in de registro de contêiner.

Ao criar um token para sua conta do {{site.data.keyword.Bluemix_notm}}, é possível decidir se esse token autoriza o acesso somente leitura (pull) ou de gravação (push e pull) para o registro. Também será possível especificar se um token é permanente ou se ele expirará após 24 horas. É possível criar e usar diversos tokens para controlar diferentes tipos de acesso.

Use as tarefas a seguir para gerenciar seus tokens:

-  [Criando um token para sua conta do {{site.data.keyword.Bluemix_notm}}](#registry_tokens_create)
-  [Usando um token para automatizar o acesso a seus namespaces](#registry_tokens_use)
-  [Removendo um token de sua conta do {{site.data.keyword.Bluemix_notm}}](#registry_tokens_remove)


### Criando um token para sua conta do {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_create}

É possível criar um token para conceder acesso a todos os namespaces do {{site.data.keyword.registrylong_notm}} em uma região.
{:shortdesc}

1.  Crie um token. O exemplo a seguir cria um token sem expiração que tem acesso de leitura e de gravação a todos os namespaces configurados em uma região.

    ```
    ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="ícone de lâmpada"/> Entendendo os componentes deste comando</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>Opcional. Use essa opção para descrever o token para que seja possível identificá-lo mais facilmente mais tarde.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>Opcional. Use essa opção para criar um token sem expiração. Se você não especifica esta opção, o token torna-se inválido depois de 24 horas. <br> **Dica:** quando você não precisar mais de um token sem expiração para bloquear o acesso aos seus namespaces, lembre-se de remover o token.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>Opcional. Use essa opção para criar um token que permite aos usuários enviar por push e fazer pull de imagens de seus namespaces. Se você não especificar esta opção, o token poderá ser usado somente para extrair imagens.</td>
        </tr>
        </tbody>
        </table>

    A saída da CLI é semelhante à seguinte saída:

    ```
    Identificador de Token 58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
    Token              <token_value>
    ```
    {: screen}

2.  Verifique se o token foi criado.

    ```
    ibmcloud cr token-list
    ```
    {: pre}


### Usando um token para automatizar o acesso a seus namespaces
{: #registry_tokens_use}

É possível usar um token em seu comando `docker login` para automatizar o acesso a seus namespaces no {{site.data.keyword.registrylong_notm}}. Dependendo do acesso configurado para o token, somente leitura ou leitura/gravação, os usuários poderão enviar por push e puxar as
imagens para e dos namespaces.
{:shortdesc}

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Liste todos os tokens em sua conta do {{site.data.keyword.Bluemix_notm}} e anote o ID de token que você deseja usar.

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  Recupere o valor do token para o token. Substitua
&lt;token_id&gt; pelo ID do token.

    ```
    ibmcloud cr token-get <token_id>
    ```
    {: pre}

    Seu valor do token é exibido em **Token** na saída da CLI.

4.  Use o token como parte de seu comando `docker login`. Substitua &lt;token_value&gt; pelo valor do token que você recuperou na etapa anterior e &lt;registry_url&gt; pela URL para o registro no qual seus namespaces estão configurados.

    -   Para os namespaces configurados no sul dos EUA: `registry.ng.bluemix.net`
    -   Para os namespaces configurados no sul do Reino Unido: `registry.eu-gb.bluemix.net`
    -   Para os namespaces configurados no centro da UE: `registry.eu-de.bluemix.net`
    -   Para os namespaces configurados no sul da AP: `registry.au-syd.bluemix.net`

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}
    
    Para o parâmetro `-u`, assegure-se de digitar a sequência `token`, não o ID do token.
    {: tip}

    Depois de efetuar login no Docker usando o token, é possível enviar por push ou puxar imagens para/de seus namespaces.


### Removendo um token de sua conta do {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_remove}

Remova um token do {{site.data.keyword.registrylong_notm}} quando você não precisar mais dele.
{:shortdesc}

Os tokens expirados do {{site.data.keyword.registrylong_notm}} são removidos automaticamente de sua conta do {{site.data.keyword.Bluemix_notm}} e não precisam ser removidos manualmente.
{:tip}

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2.  Liste todos os tokens em sua conta do {{site.data.keyword.Bluemix_notm}} e anote o ID de token que você deseja remover.

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  Remova o token.

    ```
    ibmcloud cr token-rm <token_id>
    ```
    {: pre}
    
    
## Opções de autenticação para todos os clientes
{: #registry_authentication}

É possível autenticar usando o comando `docker login` ou outros clientes de registro.
{:shortdesc}

A maioria dos usuários pode usar o comando `ibmcloud cr login` para simplificar o `docker login`, mas, se você estiver implementando a automação ou estiver usando um cliente diferente, talvez queira autenticar manualmente. Deve-se apresentar um nome de usuário e uma senha. No {{site.data.keyword.registrylong_notm}}, o nome do usuário indica o tipo de segredo que é apresentado na senha.

Os nomes de usuário a seguir são válidos:

-  `iambearer` A senha contém um token de acesso do IAM. Esse tipo de autenticação é de curta duração, mas pode ser derivada de todos os tipos de identidade do IAM.
-  `iamrefresh` A senha deve conter um token de atualização do IAM que é usado internamente para gerar e atualizar um token de acesso do IAM. Esse tipo de autenticação é mais duradouro e é usado pelo comando `ibmcloud cr login`.
-  `iamapikey` A senha é uma chave API do IAM. Esse tipo de autenticação é o tipo preferencial para automação. É possível usar uma chave API do ID de usuário ou de serviço. Consulte [Criando uma chave API](#registry_api_key_create).
-  `token` A senha é um token de registro. É possível usar esse nome de usuário para automação.

Não é necessário usar o comando do Docker para autenticar com o registro. Por exemplo, é possível executar o comando `ibmcloud cf push` a seguir, que autentica e autoriza um pull do registro usando uma chave API do IAM:


```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o registry.<region>.bluemix.net/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Substitua _&lt;apikey&gt;_ pela sua chave API, _&lt;region&gt;_ pelo nome de sua [região](registry_overview.html#registry_regions), _&lt;my_namespace&gt;_ pelo seu namespace e _&lt;image_repo&gt;_ pelo repositório.

Para obter mais informações, consulte [Usando um registro de imagem privado](/docs/services/ContinuousDelivery/pipeline_custom_docker_images.html#private_image_registry).
