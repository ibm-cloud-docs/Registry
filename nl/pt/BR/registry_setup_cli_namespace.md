---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

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

Antes de ser possível armazenar as imagens do Docker no {{site.data.keyword.registrylong}}, deve-se criar um namespace. Para trabalhar com namespaces, instale o plug-in da CLI `container-registry`.
{:shortdesc}

Não coloque informações pessoais em imagens de contêiner, nomes de namespace, campos de descrição (por exemplo, em tokens de registro) ou em qualquer dado de configuração de imagem (por
exemplo, nomes ou rótulos de imagem).
{: important}

Antes de iniciar, instale o  [ {{site.data.keyword.Bluemix_notm}}  CLI) ](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

## Instalando o plug-in da CLI `container-registry`
{: #cli_namespace_registry_cli_install}

Instale o plug-in da CLI `container-registry` para usar a linha de comandos para gerenciar seus namespaces e imagens do Docker no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. [Instale o plug-in da CLI `container-registry`.](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install)
2. Opcional: [configure o cliente Docker para executar comandos sem permissões raiz ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.docker.com/engine/installation/linux/linux-postinstall). Se você não realizar essa etapa, deverá executar os comandos `ibmcloud login`, `ibmcloud cr login`, `docker pull` e `docker push` com **sudo** ou como raiz.

Agora é possível configurar seu próprio namespace no {{site.data.keyword.registrylong_notm}}.

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

## Configurando um namespace
{: #registry_namespace_setup}

Deve-se criar um namespace para armazenar as imagens do Docker no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Antes de iniciar**

- [Instale a CLI do {{site.data.keyword.Bluemix_notm}} e o plug-in da CLI do `container-registry`](/docs/services/Registry?topic=registry-getting-started#gs_registry_cli_install).
- [Planeje como usar e nomear seus namespaces de registro](/docs/services/Registry?topic=registry-registry_overview#registry_namespaces).

Crie um namespace, veja [Configurar um namespace](/docs/services/Registry?topic=registry-getting-started#gs_registry_namespace_add) na documentação de Introdução.

Agora é possível [enviar por push imagens do Docker para seu namespace no {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_pushing_namespace) e compartilhar essas imagens com outros usuários em sua conta.

## Removendo namespaces
{: #registry_remove}

Se um namespace de registro não é mais requerido, é possível remover o namespace de sua conta do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1. Efetue login no {{site.data.keyword.Bluemix_notm}}.

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

    Substitua `<my_namespace>` pelo namespace que deseja remover.

    ```
    ibmcloud cr namespace-rm <my_namespace>
    ```
    {: pre}

    Após a exclusão de um namespace, pode levar alguns minutos antes que ele se torne disponível novamente para reutilização.
