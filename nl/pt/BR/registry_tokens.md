---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, API keys, tokens, automating access, creating API keys, authenticating,

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

# Automatizando o acesso ao {{site.data.keyword.registrylong_notm}}
{: #registry_access}

É possível usar uma chave de API do {{site.data.keyword.iamlong}} (IAM) para automatizar o acesso aos seus namespaces do {{site.data.keyword.registrylong_notm}}, de forma que seja possível enviar imagens por push e fazer pull de imagens.
{:shortdesc}

Está tentando usar suas imagens de registro em implementações do Kubernetes? Verifique [Acessando imagens em outros namespaces, {{site.data.keyword.cloud_notm}} regiões e contas do Kubernetes](/docs/containers?topic=containers-images#other).
{: tip}

As chaves API são vinculadas à sua conta e podem ser usadas no {{site.data.keyword.cloud_notm}} para que você não precise de credenciais diferentes para cada serviço. É possível usar a chave API na CLI ou como parte de automação para efetuar login como sua identidade do usuário.

Se você usar uma chave API, poderá controlar o acesso aos namespaces usando políticas do IAM. Para obter mais informações, consulte [Definindo políticas de função de acesso de usuário](/docs/services/Registry?topic=registry-user#user).

Para obter mais informações sobre chaves API do {{site.data.keyword.registrylong_notm}}, veja [Trabalhando com chaves API](/docs/iam?topic=iam-manapikey#manapikey).

Antes de iniciar, [instale o {{site.data.keyword.registrylong_notm}} e a CLI do Docker](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

## Automatizando o acesso aos seus namespaces usando chaves API
{: #registry_api_key}

É possível usar as chaves API para automatizar o push e o pull de imagens do Docker para/de seus namespaces.
{:shortdesc}

### Criando uma chave API
{: #registry_api_key_create}

É possível criar uma chave API que pode então ser usada para efetuar login no seu registro.
{:shortdesc}

É possível criar tanto chaves API do usuário quanto chaves API do ID de serviço.

- Para criar uma chave API do ID de serviço, consulte [Criando uma chave API para um ID de serviço](/docs/iam?topic=iam-serviceidapikeys#create_service_key).
- Para criar uma chave API do usuário, consulte [Criando uma chave API](/docs/iam?topic=iam-userapikey#create_user_key).

### Usando uma chave API para automatizar o acesso
{: #registry_api_key_use}

É possível usar uma chave API para automatizar o acesso a seus namespaces no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Use a chave API para efetuar login no seu registro executando o comando do Docker a seguir. Substitua `<your_apikey>` por sua chave de API e substitua `<registry_url>` pela URL para o registro no qual seus namespaces estão configurados.

- Para namespaces configurados no norte da Ásia-Pacífico, use `jp.icr.io`
- Para namespaces configurados no sul da Ásia-Pacífico, use `au.icr.io`
- Para namespaces configurados na UE Central, use `de.icr.io`
- Para namespaces configurados no sul do Reino Unido, use `uk.icr.io`
- Para namespaces configurados no sul dos EUA, use `us.icr.io`

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

Para obter informações de referência sobre o comando, consulte [Criar uma nova chave de API da plataforma {{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create).

## Opções de autenticação para todos os clientes
{: #registry_authentication}

É possível autenticar usando o comando `docker login` ou outros clientes de registro.
{:shortdesc}

A maioria dos usuários pode usar o comando `ibmcloud cr login` para simplificar o `docker login`, mas, se você estiver implementando a automação ou estiver usando um cliente diferente, talvez queira autenticar manualmente. Deve-se apresentar um nome de usuário e uma senha. No {{site.data.keyword.registrylong_notm}}, o nome do usuário indica o tipo de segredo que é apresentado na senha.

Os nomes de usuário a seguir são válidos:

- `iambearer` A senha contém um token de acesso do IAM. Esse tipo de autenticação é de curta duração, mas pode ser derivada de todos os tipos de identidade do IAM.
- `iamrefresh` A senha deve conter um token de atualização do IAM que é usado internamente para gerar e atualizar um token de acesso do IAM. Esse tipo de autenticação é mais duradouro e é usado pelo comando `ibmcloud cr login`.
- `iamapikey` A senha é uma chave API do IAM. Esse tipo de autenticação é o tipo preferencial para automação. É possível usar uma chave API do ID de usuário ou de serviço. Consulte [Criando uma chave API](#registry_api_key_create).

Você não tem que usar o comando `docker` para autenticar com o registro. Por exemplo, é possível iniciar os apps do Cloud Foundry por meio de imagens no registro usando a CLI do Cloud Foundry:

```
export CF_DOCKER_PASSWORD=<apikey>
ibmcloud cf push appname  -o <region>.icr.io/<my_namespace>/<image_repo> --docker-username iamapikey
```
{: pre}

Substitua `<apikey>` por sua chave de API, `<region>` pelo nome de sua [região](/docs/services/Registry?topic=registry-registry_overview#registry_regions), `<my_namespace>` por seu namespace e `<image_repo>` pelo repositório.

Para obter mais informações, consulte [Usando um registro de imagem privado](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-custom_docker_images#private_image_registry).
