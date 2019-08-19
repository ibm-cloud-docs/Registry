---

copyright:
  years: 2019,
lastupdated: "2019-08-01"

keywords: IBM Cloud Container Registry, retention, delete images, retain images

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

# Retendo imagens
{: #registry_retention}

É possível decidir se excluir ou reter imagens.
{:shortdesc}

## Planejando a retenção
{: #retention_plan}

O comando [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) opera em uma base por namespace, portanto, usando múltiplos namespaces em seu pipeline, isso significa que é possível aplicar critérios de retenção diferentes para melhor se adequar aos seus requisitos.

Considere um pipeline de entrega típico com ambientes de desenvolvimento, preparação e produção. Como o código é entregue, a integração e a implementação contínuas enviam por push as imagens para o registro e, em seguida, as implementam diretamente em seu ambiente de desenvolvimento. Após o teste, algumas construções do desenvolvimento são promovidas para a preparação e, em seguida, potencialmente para a produção. Nesse cenário, a taxa de mudança de imagem é mais rápida no desenvolvimento e mais lenta na produção. Se todos os seus ambientes fizerem pull em imagens do mesmo namespace, poderá ser difícil escolher um número apropriado de imagens para retenção devido a essa diferença na velocidade.

Uma boa abordagem é entregar todas as imagens em um namespace de desenvolvimento, por exemplo, `project-development` e, em seguida, usar o comando [`ibmcloud cr image-tag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_tag) para identificar a imagem em um namespace diferente quando ela for promovida para um estágio superior do pipeline. No exemplo anterior, é possível ter três namespaces: desenvolvimento, `project-development`, preparação, `project-staging` e produção,
`project-production`. Quando você está promovendo de desenvolvimento para preparação, as imagens são identificadas do namespace `project-development` para o namespace `project-staging`
e as imagens do namespace `project-staging` são usadas para implementação. Da mesma forma, quando você está promovendo de preparação para produção, as imagens são identificadas do namespace `project-staging` para o namespace `project-production` e as imagens do namespace `project-production` são usadas na implementação de produção.

Você obtém as vantagens a seguir usando essa técnica:

* É possível escolher configurações de retenção diferentes para namespaces de desenvolvimento, preparação e produção.
* Você minimiza as chances de remover acidentalmente uma imagem que pode estar em uso em seus ambientes de preparação ou de produção, em comparação com o uso de um único namespace para todas as imagens.
* É possível usar diferentes políticas do [IAM](/docs/services/Registry?topic=registry-iam). Por exemplo, é possível ter acesso mais restritivo a imagens de produção.
* É possível assinar imagens de produção, mas deixar as imagens de desenvolvimento e preparação sem assinatura.

## Limpe seus namespaces retendo apenas imagens que atendam aos seus critérios
{: #retention_images}

Retenha imagens para cada repositório em um namespace no {{site.data.keyword.registrylong_notm}} ao aplicar critérios especificados. Todas as outras imagens no namespace são excluídas.
{:shortdesc}

O comando [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) lista as imagens que serão excluídas e fornece a opção de cancelar antes da exclusão.

Quando uma imagem, dentro de um repositório, é referenciada por múltiplas tags, essa imagem é contada apenas uma vez. As imagens mais recentes são retidas. A idade é determinada de quando a imagem foi criada, não de quando foi enviada para o registro.
{: tip}

A exclusão de uma imagem não pode ser desfeita. A exclusão de uma imagem que está sendo usada por uma implementação existente pode causar falha de aumento de capacidade, reagendamento ou ambos.
{: important}

Para reduzir o número de imagens em cada repositório em seu namespace usando a CLI, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.cloud_notm}} executando o comando `ibmcloud login`.
2. Escolha o registro no qual você deseja limpar suas imagens executando o comando a seguir e selecionando a região apropriada:

   ```
   ibmcloud cr region-set
   ```
   {: pre}

3. Para reter algumas imagens e excluir as outras, execute o comando a seguir:

   ```
  ibmcloud cr retention-run --images IMAGECOUNT NAMESPACE
   ```
   {: pre}

   Em que `IMAGECOUNT` é o número de imagens que você deseja reter para cada repositório em seu namespace, `NAMESPACE`.

3. Verifique se as imagens foram excluídas, executando o comando a seguir e verifique se as imagens não são mostradas na lista.

   ```
   ibmcloud cr image-list
   ```
   {: pre}
