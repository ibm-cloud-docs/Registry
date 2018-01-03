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


# Automatizando o acesso ao {{site.data.keyword.registrylong_notm}}
{: #registry_access}

É possível usar tokens de registro ou uma chave API do {{site.data.keyword.iamlong}} (IAM) para automatizar o acesso a seus namespaces do {{site.data.keyword.registrylong_notm}} de forma que possa enviar por push e puxar as imagens.
{:shortdesc}

As chaves API são vinculadas à sua conta e podem ser usadas no {{site.data.keyword.Bluemix_notm}} para que você não precise de credenciais diferentes para cada serviço. É possível usar a chave API na CLI ou como parte de automação para efetuar login como sua identidade do usuário.

Os tokens de registro têm o escopo definido somente para {{site.data.keyword.registrylong_notm}}. É possível limitá-los ao acesso somente leitura e escolher se eles estão expirando ou não expirando.

Para obter mais informações sobre chaves API do {{site.data.keyword.registrylong_notm}}, veja [Trabalhando com chaves API](../../iam/apikeys.html#manapikey).

Antes de iniciar, [instale o {{site.data.keyword.registrylong_notm}} e a CLI do Docker](registry_setup_cli_namespace.html#registry_cli_install).


## Automatizando o acesso aos seus namespaces usando chaves API
{: #registry_api_key}

É possível usar as chaves API para automatizar o push e o pull de imagens do Docker para/de seus namespaces.
{:shortdesc}

### Criando uma chave API
{: #registry_api_key_create}

É possível criar uma chave API que pode então ser usada para efetuar login no seu registro.
{:shortdesc} 

Crie uma chave API do IAM, veja [Criando uma chave API](../../iam/userid_keys.html#creating-an-api-key). 

### Usando uma chave API para automatizar o acesso
{: #registry_api_key_use}

É possível usar uma chave API para automatizar o acesso a seus namespaces no {{site.data.keyword.registrylong_notm}}.
{:shortdesc} 

Use a chave API para efetuar login no seu registro executando o comando do Docker a seguir. Substitua &lt;your_apikey&gt; por sua chave API e substitua &lt;registry_url&gt; pela URL para o registro no qual seus namespaces estão configurados.

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}


Para obter informações de referência sobre o comando, veja [Criar uma nova chave API da plataforma {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_api_key_create).


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
    bx cr token-add --description "This is a token" --non-expiring --readwrite
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
        <td>Opcional. Use essa opção para criar um token que permite aos usuários enviar por push e extrair imagens de seus namespaces. Se você não especificar esta opção, o token poderá ser usado somente para extrair imagens.</td>
        </tr>
        </tbody>
        </table>

    A saída da CLI é semelhante à seguinte saída:

    ```
    Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
    Token              <token_value>
    ```
    {: screen}

2.  Verifique se o token foi criado.

    ```
    bx cr token-list
    ```
    {: pre}


### Usando um token para automatizar o acesso a seus namespaces 
{: #registry_tokens_use}

É possível usar um token em seu comando `docker login` para automatizar o acesso a seus namespaces no {{site.data.keyword.registrylong_notm}}. Dependendo se você configurou o acesso somente leitura ou de leitura/gravação para o seu token, os usuários podem enviar por push e puxar imagens para/de seus namespaces.
{:shortdesc}

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Liste todos os tokens em sua conta do {{site.data.keyword.Bluemix_notm}} e anote o ID de token que você deseja usar.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Recupere o valor do token para o token. Substitua
&lt;token_id&gt; pelo ID do token.

    ```
    bx cr token-get <token_id>
    ```
    {: pre}

    Seu valor do token é exibido em **Token** na saída da CLI.

4.  Use o token como parte de seu comando `docker login`. Substitua &lt;token_value&gt; pelo valor do token que você recuperou na etapa anterior e &lt;registry_url&gt; pela URL para o registro no qual seus namespaces estão configurados.

    -   Para namespaces configurados no sul dos EUA: registry.ng.bluemix.net
    -   Para namespaces configurados no Sul do Reino Unido: registry.eu-gb.bluemix.net
    -   Para namespaces configurados no Centro da Europa: registry.eu-de.bluemix.net
    -   Para namespaces configurados no Sul da Ásia-Pacífico: registry.au-syd.bluemix.net

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}

    Depois de efetuar login no Docker usando o token, é possível enviar por push ou puxar imagens para/de seus namespaces.


### Removendo um token de sua conta do {{site.data.keyword.Bluemix_notm}}
{: #registry_tokens_remove}

Remova um token do {{site.data.keyword.registrylong_notm}} quando você não precisar mais dele.
{:shortdesc}

**Nota:** Os tokens do {{site.data.keyword.registrylong_notm}} expirados são removidos automaticamente da sua conta do {{site.data.keyword.Bluemix_notm}} e não precisam ser removidos manualmente.

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Liste todos os tokens em sua conta do {{site.data.keyword.Bluemix_notm}} e anote o ID de token que você deseja remover.

    ```
    bx cr token-list
    ```
    {: pre}

3.  Remova o token.

    ```
    bx cr token-rm <token_id>
    ```
    {: pre}
    


