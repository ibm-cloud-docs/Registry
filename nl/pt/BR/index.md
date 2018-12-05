---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Introdução ao {{site.data.keyword.registrylong_notm}}
{: #index}

O {{site.data.keyword.registrylong}} fornece um registro privado
de imagem de múltiplos locatários que é possível usar para armazenar e compartilhar com segurança as suas imagens do Docker com usuários em sua
conta do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

O console do {{site.data.keyword.Bluemix_notm}} inclui um resumo de Iniciação rápida. Para saber mais sobre como usar o console do {{site.data.keyword.Bluemix_notm}}, consulte [Gerenciando a segurança da imagem com o Vulnerability Advisor](/docs/services/va/va_index.html).

Não coloque informações pessoais em imagens de contêiner, nomes de namespace, campos de descrição (por exemplo, em tokens de registro) ou em qualquer dado de configuração de imagem (por
exemplo, nomes ou rótulos de imagem).
{:tip}

## Instalar a CLI do {{site.data.keyword.registrylong_notm}}
{: #registry_cli_install}

1. Instale a CLI do [{{site.data.keyword.Bluemix_notm}}
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://clis.ng.bluemix.net/ui/home.html) para que os
comandos do {{site.data.keyword.Bluemix_notm}} `ibmcloud` possam ser executados. Essa instalação também instala os plug-ins para {{site.data.keyword.containerlong_notm}} e {{site.data.keyword.registrylong_notm}}.

## Configurar um namespace
{: #registry_namespace_add}

1. Efetue login no {{site.data.keyword.Bluemix_notm}}.

   ```
   ibmcloud login
   ```
   {: pre}

2. Inclua um namespace para criar seu próprio repositório de imagem. Substitua _&lt;my_namespace&gt;_ pelo seu namespace preferencial.

   ```
   ibmcloud cr namespace-add <my_namespace>
   ```
   {: pre}

3. Para verificar se o namespace foi criado, execute o comando `ibmcloud cr namespace-list`.

   ```
   ibmcloud cr namespace-list
   ```
   {: pre}

## Puxar imagens de outro registro para sua máquina local
{: #registry_images_pulling}

1. [Instale a CLI do Docker ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.docker.com/community-edition#/download). Para Windows 8, ou OS X Yosemite 10.10.x ou anterior, instale o [Docker Toolbox ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.docker.com/toolbox/).

2. Faça download (_puxe_) da imagem para sua máquina local. Substitua _&lt;source_image&gt;_ pelo repositório da imagem e _&lt;tag&gt;_ pela tag da imagem que deseja usar, por exemplo, _latest_.

   ```
   docker pull <source_image>:<tag>
   ```
   {: pre}

   Exemplo, em que _&lt;source_image&gt;_ é `hello-world` e _&lt;tag&gt;_ é `latest`:

   ```
   docker pull hello-world:latest
   ```
   {: pre}

3. Identifique a imagem. Substitua _&lt;source_image&gt;_ pelo repositório e
_&lt;tag&gt;_ pela tag de sua imagem local extraída anteriormente. Substitua _&lt;region&gt;_ pelo nome de sua [região](registry_overview.html#registry_regions). Substitua _&lt;my_namespace&gt;_ pelo namespace criado em [Configurar um namespace](index.html#registry_namespace_add). Defina o repositório e identifique a imagem que você deseja usar
em seu namespace substituindo _&lt;new_image_repo&gt;_ e _&lt;new_tag&gt;_.

   ```
   docker tag <source_image>:<tag> registry.<region>.bluemix.net/<my_namespace>/<new_image_repo>:<new_tag>
   ```
   {: pre}

   Exemplo, em que _&lt;source_image&gt;_ é `hello-world`, _&lt;tag&gt;_ é `latest`, _&lt;region&gt;_ é `eu-gb`, _&lt;my_namespace&gt;_ é `namespace1`, _&lt;new_image_repo&gt;_ é `hw_repo` e _&lt;new_tag&gt;_ é `1`:

   ```
   docker tag hello-world:latest registry.eu-gb.bluemix.net/namespace1 /hw_repo: 1
   ```
   {: pre}

## Enviar por push imagens do Docker para seu namespace
{: #registry_images_pushing}

1. Execute o comando `ibmcloud cr login` para registrar seu daemon local do Docker no {{site.data.keyword.registrylong_notm}}.

   ```
   ibmcloud cr login
   ```
   {: pre}

2. Faça upload (_enviar por push_) da imagem para seu namespace. Substitua _&lt;my_namespace&gt;_ pelo namespace criado em [Configurar um namespace](index.html#registry_namespace_add) e _&lt;image_repo&gt;_ e _&lt;tag&gt;_ pelo repositório e a tag da imagem que você escolheu quando identificou a imagem.

   ```
   docker push registry.<region>.bluemix.net/<my_namespace>/<image_repo>:<tag>
   ```
   {: pre}

   Exemplo, em que _&lt;region&gt;_ é `eu-gb`, _&lt;my_namespace&gt;_ é `namespace1`, _&lt;image_repo&gt;_ é `hw_repo` e _&lt;tag&gt;_ é `1`:

   ```
   docker push registry.eu-gb.bluemix.net/namespace1/hw_repo:1
   ```
   {: pre}

3. Verifique se a imagem foi enviada por push com sucesso executando o comando a seguir.

   ```
   ibmcloud cr image-list
   ```
   {: pre}

Bom Trabalho! Você configurou um namespace no {{site.data.keyword.registrylong_notm}} e enviou sua primeira imagem para o seu namespace.

**O que Vem a Seguir?**

- [Gerenciar segurança de imagem com o Vulnerability Advisor](../va/va_index.html)
- [Revisar seus planos de serviço e uso](registry_overview.html#registry_plans)
- [Armazenar e gerenciar mais imagens em seu namespace](registry_images_.html)
- [Definindo políticas de função de acesso do usuário](/docs/services/Registry/registry_users.html#user)
- [Configurar clusters e nós do trabalhador](/docs/containers/cs_clusters.html#clusters)
