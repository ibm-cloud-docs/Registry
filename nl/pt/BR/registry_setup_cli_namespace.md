---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-1"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Configurando a CLI do {{site.data.keyword.registrylong_notm}} e
o seu namespace de registro
{: #registry_setup_cli_namespace}

Antes de poder armazenar as imagens do Docker no {{site.data.keyword.registrylong}}, deve-se instalar a CLI do {{site.data.keyword.Bluemix_notm}} e o plug-in do {{site.data.keyword.registrylong_notm}} e, depois, configurar um namespace de registro para criar seu próprio repositório de imagem no {{site.data.keyword.registrylong_notm}}.
{:shortdesc}


**Nota**: não coloque informações pessoais em imagens de contêiner, nomes de namespace, campos de descrição (por exemplo, em tokens de registro) ou em quaisquer dados de configuração de imagem (por exemplo, nomes de imagem ou rótulos de imagem).


## Instalando o plug-in da CLI do {{site.data.keyword.registrylong_notm}} (`bx cr`)
{: #registry_cli_install}

Instale a CLI do {{site.data.keyword.registrylong_notm}} para usar a linha de comandos para gerenciar seus namespaces e
imagens do Docker no registro privado do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1.  [Instale o plug-in de registro de contêiner.](index.html#registry_cli_install)
2.  Opcional: [configure o cliente Docker para executar comandos sem permissões raiz](https://docs.docker.com/engine/installation/linux/linux-postinstall). Caso não execute essa etapa, deve-se executar os comandos `bx login`, `bx cr login`, `docker pull`
e `docker push` com **sudo** ou como raiz.

Agora é possível configurar seu próprio namespace no registro privado do {{site.data.keyword.registrylong_notm}}.

## Atualizando o plug-in do {{site.data.keyword.registrylong_notm}} (`bx cr`)
{: #registry_cli_update}

Talvez você queira atualizar a CLI do {{site.data.keyword.registrylong_notm}} periodicamente para usar novos
recursos.
{:shortdesc}

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Atualize o plug-in de registro de contêiner.

    ```
    bx plugin update container-registry -r Bluemix
    ```
    {: pre}

3.  Verifique se o plug-in foi atualizado com êxito.

    ```
    bx plugin list
    ```
     {: pre}


## Desinstalando o plug-in do {{site.data.keyword.registrylong_notm}} (`bx cr`)
{: #registry_cli_uninstall}

Se você não precisar mais do plug-in de registro de contêiner, será possível desinstalá-lo.
{:shortdesc}

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Desinstale o plug-in de registro de contêiner.

    ```
    bx plugin uninstall container-registry
    ```
    {: pre}

3.  Verifique se o plug-in foi desinstalado com êxito.

    ```
    bx plugin list
    ```
    {: pre}

    O plug-in de registro de contêiner não é exibido nos resultados.


## Configurando um namespace
{: #registry_namespace_add}

Para armazenar com segurança as suas imagens do Docker, deve-se criar um namespace no registro privado do {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Antes de iniciar:

-   [Instale a CLI do {{site.data.keyword.Bluemix_notm}} e o plug-in de registro de contêiner](#registry_cli_install).
-   [Planeje como usar e nomear seus namespaces de registro](registry_overview.html#registry_namespaces).

Crie um namespace, veja [Configurar um namespace](index.html#registry_namespace_add) na documentação de Introdução.

Agora é possível [enviar por push imagens do Docker para seu namespace no registro do {{site.data.keyword.Bluemix_notm}}](registry_images_.html#registry_images_pushing) e compartilhar essas imagens com outros usuários em sua conta.

## Removendo namespaces
{: #registry_remove}

Se um namespace de registro não é mais requerido, é possível remover o namespace de sua conta do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login
    ```
    {: pre}

2.  Lista de espaços disponíveis.

    ```
    bx cr namespace-list
    ```
    {: pre}

3.  Remover um namespace.

    **Atenção:** quando você remove um namespace, qualquer imagem armazenada nesse namespace também é excluída. Esta ação não pode ser desfeita.

    Substitua _&lt;my_namespace&gt;_ pelo
namespace que você deseja remover.

    ```
    bx cr namespace-rm <my_namespace>
    ```
    {: pre}

    Depois de excluir um namespace, dependendo do número de imagens
armazenadas, pode levar alguns minutos antes que o namespace
se torne disponível novamente para reutilização.
