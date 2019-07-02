---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-19"

keywords: IBM Cloud Container Registry, private image registry, namespaces, image security, cli, namespaces, tutorial, Docker, images, registry

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

# Tutorial de Introdução
{: #getting-started}

O {{site.data.keyword.registrylong}} fornece um registro de imagem privada de diversos locatários que pode ser usada para armazenar e compartilhar as imagens do Docker com usuários em sua conta do {{site.data.keyword.cloud_notm}}.
{:shortdesc}

O console do {{site.data.keyword.cloud_notm}} inclui um resumo de Iniciação rápida. Para saber mais sobre como usar o console do {{site.data.keyword.cloud_notm}}, consulte [Gerenciando a segurança da imagem com o Vulnerability Advisor](/docs/services/va?topic=va-va_index).

Não coloque informações pessoais em imagens de contêiner, nomes de namespace, campos de descrição (por exemplo, em tokens de registro) ou em qualquer dado de configuração de imagem (por
exemplo, nomes ou rótulos de imagem).
{: important}

## Instalar a CLI do {{site.data.keyword.registrylong_notm}}
{: #gs_registry_cli_install}

1. Instale a CLI do {{site.data.keyword.cloud_notm}} para que seja possível executar os comandos `ibmcloud` do {{site.data.keyword.cloud_notm}}. Consulte [Introdução à CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started). Essa instalação também instala os plug-ins da CLI para o {{site.data.keyword.containerlong_notm}} e o {{site.data.keyword.registrylong_notm}}.

## Configurar um namespace
{: #gs_registry_namespace_add}

1. Efetue login no {{site.data.keyword.cloud_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

   Se você tiver uma identidade federada, efetue login usando o comando a seguir:

   ```
   ibmcloud login --sso
   ```
   {: pre}

2. Inclua um namespace para criar seu próprio repositório de imagem. Substitua `<my_namespace>` por seu namespace preferencial.

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

   O namespace deve ser exclusivo em todas as contas do {{site.data.keyword.cloud_notm}} na mesma região. Os namespaces devem ter de 4 a 30 caracteres e conter apenas letras minúsculas, números, hífens (-) e sublinhados (_). Os namespaces devem iniciar e terminar com uma letra ou número.
   {: tip}

3. Para verificar se o namespace foi criado, execute o comando `ibmcloud cr namespace-list`.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Puxar imagens de outro registro para sua máquina local
{: #gs_registry_images_pulling}

1. [Instale a CLI do Docker Engine ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.docker.com/products/container-runtime#/download). Para Windows 8, ou OS X Yosemite 10.10.x ou anterior, instale o [Docker Toolbox ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.docker.com/toolbox/). O {{site.data.keyword.registrylong_notm}} suporta o Docker Engine v1.12.6 ou mais recente.

2. Faça download (_puxe_) da imagem para sua máquina local. Substitua `<source_image>` pelo repositório da imagem e `<tag>` pela tag da imagem que você deseja usar, por exemplo, _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Veja este exemplo, em que `<source_image>` é `hello-world` e `<tag>` é `latest`:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Identifique a imagem. Substitua `<source_image>` pelo repositório e `<tag>` pela tag da sua imagem local que passou por pull anteriormente. Substitua `<region>` pelo nome de sua [região](/docs/services/Registry?topic=registry-registry_overview#registry_regions). Substitua `<my_namespace>` pelo namespace criado em [Configurar um namespace](#gs_registry_namespace_add). Defina o repositório e a tag da imagem que você deseja usar em seu namespace substituindo `<new_image_repo>` e `<new_tag>`.

   ```
   docker tag <source_image>:<tag> <region>.icr.io/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Para localizar o nome de sua região, execute o comando `ibmcloud cr region`.
   {: tip}

   Veja este exemplo, em que `<source_image>` é `hello-world`, `<tag>` é `latest`, `<region>` é `uk`, `<my_namespace>` é `namespace1`, `<new_image_repo>` é `hw_repo` e `<new_tag>` é `1`:

   ```
   docker tag hello-world:latest uk.icr.io/namespace1 /hw_repo: 1
   ```
   {: pre}

## Enviar por push imagens do Docker para seu namespace
{: #gs_registry_images_pushing}

1. Execute o comando `ibmcloud cr login` para registrar seu daemon local do Docker no {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Faça upload (_enviar por push_) da imagem para seu namespace. Substitua `<my_namespace>` pelo namespace criado em [Configurar um namespace](#gs_registry_namespace_add) e `<image_repo>` e `<tag>` pelo repositório e pela tag da imagem que você escolheu ao identificar a imagem.

   ```
   docker push <region>.icr.io/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}
   
   Veja este exemplo, em que `<region>` é `uk`, `<my_namespace>` é `namespace1`, `<image_repo>` é `hw_repo` e `<tag>` é `1`:

   ```
   docker push uk.icr.io/namespace1 /hw_repo: 1
   ```
   {: pre}

3. Verifique se a imagem foi enviada por push com sucesso executando o comando a seguir.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Bom Trabalho! Você configurou um namespace no {{site.data.keyword.registrylong_notm}} e enviou sua primeira imagem para o seu namespace.

## Etapas seguintes
{: #gs_get_start_next}

- [Gerenciar segurança de imagem com o Vulnerability Advisor](/docs/services/va?topic=va-va_index)
- [Revisar seus planos de serviço e uso](/docs/services/Registry?topic=registry-registry_overview#registry_plans)
- [Armazenar e gerenciar mais imagens em seu namespace](/docs/services/Registry?topic=registry-registry_images_)
- [Definindo políticas de função de acesso do usuário](/docs/services/Registry?topic=registry-user#user)
- [Configurar clusters e nós do trabalhador](/docs/containers?topic=containers-clusters#clusters)
