---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, namespaces, Docker images, CLI, commands, installing, registry CLI, removing namespaces, 

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

# Configurando a CLI do {{site.data.keyword.registrylong_notm}} e
o seu namespace de registro
{: #registry_setup_cli_namespace}

Para gerenciar suas imagens do Docker no {{site.data.keyword.registrylong}}, será preciso instalar o plug-in da CLI `container-registry` e criar um namespace.
{:shortdesc}

Não coloque informações pessoais em suas imagens de contêiner, nomes de namespace, campos de descrição ou em quaisquer dados de configuração de imagem (por exemplo, nomes de imagem ou rótulos de imagem).
{: important}

Antes de começar, para instalar a CLI do {{site.data.keyword.cloud_notm}}, consulte [Introdução à CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started).

## Instalando o plug-in da CLI `container-registry`
{: #cli_namespace_registry_cli_install}

Instale o plug-in da CLI `container-registry` para usar a linha de comandos para gerenciar seus namespaces e imagens do Docker no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Instale o plug-in da CLI `container-registry`.](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Opcional: [configure o cliente Docker para executar comandos sem permissões raiz ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.docker.com/install/linux/linux-postinstall/). Se você não realizar essa etapa, deverá executar os comandos `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` com `sudo` ou como raiz.

Agora, é possível configurar seu próprio [namespace](#registry_namespace_setup) no {{site.data.keyword.registrylong_notm}}.

## Atualizando o plug-in da CLI `container-registry`
{: #registry_cli_update}

É possível que você queira atualizar o plug-in da CLI `container-registry` periodicamente para usar novos recursos.
{:shortdesc}

1. Atualize o plug-in da CLI `container-registry`.

    ```
    ibmcloud plugin update container-registry
    ```
    {: pre}

2. Verifique se o plug-in da CLI `container-registry` foi atualizado com êxito.

    ```
    ibmcloud plugin list
    ```
     {: pre}

## Desinstalando o plug-in da CLI `container-registry`
{: #registry_cli_uninstall}

Se você não precisar mais do plug-in da CLI `container-registry`, será possível desinstalá-lo.
{:shortdesc}

1. Desinstale o plug-in da CLI `container-registry`.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

2. Verifique se o plug-in da CLI `container-registry` foi desinstalado com êxito.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    O plug-in da CLI `container-registry` não é exibido nos resultados.

## Planejando namespaces
{: #registry_setup_cli_namespace_plan}

O {{site.data.keyword.registrylong_notm}} fornece um registro privado de imagem de vários locatários que é hospedado e gerenciado pela IBM. É possível armazenar e compartilhar as imagens do Docker nesse registro, configurando um namespace de registro.
{:shortdesc}

É possível configurar múltiplos namespaces, por exemplo, para ter repositórios separados para seus ambientes temporários e de produção. Se você deseja usar o registro em múltiplas regiões do {{site.data.keyword.cloud_notm}}, deve-se configurar um namespace para cada região. Os nomes de namespace são exclusivos dentro de regiões. É possível usar o mesmo nome de namespace para cada região, a menos que alguém já tenha um namespace com esse nome configurado nessa região.

É possível controlar o acesso a seus namespaces usando políticas do IAM. Para obter mais informações, consulte [Definindo políticas de função de acesso de usuário](/docs/services/Registry?topic=registry-user#user).

Para trabalhar somente com as imagens públicas fornecidas pela IBM, você não precisa configurar um namespace.

Se você não tiver certeza se um namespace já está configurado para sua conta, execute o comando `ibmcloud cr namespace-list` para recuperar informações existentes de namespace.
{:tip}

Considere as regras a seguir ao escolher um namespace:

- Seu namespace deve ser exclusivo em todas as contas do {{site.data.keyword.cloud_notm}} na mesma região.
- Seu namespace deve ter entre 4 e 30 caracteres.
- Seu namespace deve começar e terminar com uma letra ou número.
- Seu namespace deve conter apenas letras minúsculas, números, hifens (-) e sublinhados (_).

Não coloque informações pessoais nos nomes de namespace.
{: important}

Depois de configurar seu primeiro namespace, você é designado ao plano de serviço grátis do {{site.data.keyword.registrylong_notm}}, se ainda não tiver [feito upgrade de seu plano](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade).

## Configurando um namespace
{: #registry_namespace_setup}

Deve-se criar um namespace para armazenar as imagens do Docker no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Antes de iniciar**

- [Instale a CLI do {{site.data.keyword.cloud_notm}} e o plug-in `container-registry` da CLI](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Planeje como usar e nomear seus namespaces de registro](#registry_setup_cli_namespace_plan).

Para criar um namespace, veja [Configurar um namespace](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add)na documentação de Introdução.

O namespace deve ser exclusivo em todas as contas do {{site.data.keyword.cloud_notm}} na mesma região. Os namespaces devem ter de 4 a 30 caracteres e conter apenas letras minúsculas, números, hífens (-) e sublinhados (_). Os namespaces devem iniciar e terminar com uma letra ou número.
{: tip}

Agora é possível [enviar por push imagens do Docker para seu namespace no {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) e compartilhar essas imagens com outros usuários em sua conta. Para controlar o acesso aos namespaces no IAM do {{site.data.keyword.cloud_notm}}, consulte [Criando políticas](/docs/services/Registry?topic=registry-user#create).

## Removendo namespaces
{: #registry_remove}

Se um namespace de registro não é mais requerido, é possível remover o namespace de sua conta do {{site.data.keyword.cloud_notm}}.
{:shortdesc}

1. Efetue login no {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Lista de espaços disponíveis.

    ```
    ibmcloud cr namespace-list
    ```
    {: pre}

3. Remover um namespace.

    **Atenção:** quando você remove um namespace, qualquer imagem armazenada nesse namespace também é excluída. Esta ação não pode ser desfeita.

    Substitua `<my_namespace>` pelo namespace que você deseja remover.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    Após a exclusão de um namespace, pode levar alguns minutos antes que ele se torne disponível novamente para reutilização.
