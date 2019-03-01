---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, vulnerability of images, security of images, security issues

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

# Monitorando a vulnerabilidade de imagens
{: #registry_ui}

É possível visualizar informações sobre potenciais vulnerabilidades e a segurança de imagens nos repositórios públicos e privados do {{site.data.keyword.registrylong}} usando o console do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

A coluna **Status de segurança** mostra as informações a seguir sobre a imagem:

- `Secure` Nenhum problema de segurança foi localizado.
- `Vulnerable` Problemas de segurança ou configuração foram localizados e devem ser direcionados antes de poder implementar a imagem.
- `Incomplete` A varredura não está completa. A varredura ainda pode estar em execução ou o sistema operacional da imagem pode não ser compatível. Aguarde e tente a varredura novamente. Se a varredura ainda não tiver sido concluída, envie a imagem por push novamente para iniciar uma nova varredura. As
imagens com varreduras incompletas não são bloqueadas para implementação.
- `S.O. não suportado` O sistema operacional na imagem não é suportado.

Para visualizar a interface gráfica com o usuário, use as etapas a seguir:

1. Efetue login no console do {{site.data.keyword.cloud_notm}}
([https://cloud.ibm.com/login
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login))
com o seu IBMid.
2. Se você tiver múltiplas contas do {{site.data.keyword.Bluemix_notm}}, selecione a conta e região que você deseja usar por meio do menu de conta.
3. Clique em **Catálogo**.
4. Selecione a categoria **Contêineres** e clique no tile **Registro de contêiner**.
5. Para visualizar informações sobre imagens em seus repositórios particulares, clique em **Imagens**. Uma lista de imagens em seus repositórios privados e o status de segurança para cada imagem é exibido.
6. Para descobrir mais informações sobre as vulnerabilidades potenciais, incluindo as tags e a compilação de imagem, clique na linha da imagem na tabela. A guia **Detalhes de imagem** é aberta.
7. Para saber mais sobre os problemas por tipo, clique na guia **Problemas por tipo**.
8. Para saber mais sobre os contêineres associados, clique na guia **Contêineres associados**.

Para saber mais sobre o significado das informações no relatório de segurança, veja [Gerenciando a segurança de imagem com o Vulnerability Advisor](/docs/services/va/va_index.html).
