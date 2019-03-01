---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, user access role policies, access policies, policies

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

# Definindo políticas de função de acesso do usuário
{: #user access}

Como um administrador, é possível definir políticas de acesso para seu registro a fim de criar diferentes níveis de acesso para diferentes usuários. Por exemplo, é possível autorizar determinados usuários para configurar cotas enquanto outros usuários podem apenas visualizar cotas.
{: shortdesc}

Deve-se definir políticas de acesso para cada usuário que trabalhe com o {{site.data.keyword.registrylong}}. O escopo de uma política de acesso é baseado na função ou nas funções definidas pelo usuário que determinam as ações que eles podem executar. Algumas políticas são predefinidas, mas outras podem ser customizadas.

Se você começou a usar o {{site.data.keyword.registrylong_notm}} antes de 4 de outubro de 2018, deverá ativar o cumprimento de política antes que as políticas possam entrar em vigor, consulte [Ativando o cumprimento de política para usuários existentes](#existing_users).
{: tip}

Para descobrir mais sobre as políticas de função de acesso do {{site.data.keyword.iamlong}} (IAM), consulte [{{site.data.keyword.iamshort}}](/docs/iam/index.html#iamoverview).

## Criando políticas
{: #create}

Caso queira controlar o acesso aos recursos, deve-se designar funções aos usuários ou aos IDs de serviço. O acesso a recursos do {{site.data.keyword.registrylong_notm}} pode ser concedido ao recurso namespace por nome ou ao serviço inteiro, ou seja, todos os namespaces na conta.

Se você desejar conceder acesso a tudo, não especifique um tipo de recurso ou um recurso. Se você desejar conceder acesso a um namespace específico, especifique o tipo de recurso como `namespace` e use o nome do namespace como o recurso.

**Antes de iniciar**

- Decida quais funções cada usuário precisa e sobre quais recursos no {{site.data.keyword.registrylong_notm}}, consulte [Funções do IAM](/docs/services/Registry/iam.html#iam). Leve em consideração que é possível criar várias políticas. Por exemplo, é possível conceder acesso de gravação em um recurso, mas conceder somente acesso leitura em outro recurso e não conceder nenhum acesso em outro recurso. As políticas são aditivas, o que significa que uma política de leitura global e uma política de gravação com escopo de recursos concede acesso de leitura e gravação nesse recurso.

- [Convidar usuários e designar acesso](/docs/iam/iamuserinv.html#iamuserinv).

  Se você desejar que os usuários possam criar clusters no {{site.data.keyword.containerlong_notm}}, assegure-se de designar a função de Administrador do {{site.data.keyword.registrylong_notm}} a esses usuários e não designar um grupo de recursos. Consulte [Preparando para criar clusters](/docs/containers/cs_clusters.html#cluster_prepare).
  {: tip}

Para criar políticas para o {{site.data.keyword.registrylong_notm}}, o campo de nome do serviço deve ser `container-registry`.

- Para criar uma política para os usuários, consulte [Gerenciando acesso a recursos](/docs/iam/mngiam.html#iammanidaccser).
- Para criar uma política para IDs de serviço, execute o comando `ibmcloud iam service-policy-create` ou use a GUI para ligar funções a seus IDs de serviço. Para criar políticas, deve-se ter a função de Administrador. Você automaticamente tem a função de Administrador em sua própria conta. Para obter mais informações, consulte [Criando e trabalhando com IDs de serviço](/docs/iam/serviceid.html#serviceids) e [Gerenciando políticas de acesso do ID de serviço](/docs/iam/serviceidaccess.html#serviceidpolicy).

## Ativando o cumprimento de política para usuários existentes
{: #existing_users}

Para usuários provisionados após 4 de outubro de 2018, as políticas do IAM são ativadas por padrão. Para usuários provisionados antes de 4 de outubro de 2018, depois de criar suas políticas, deve-se ativar o cumprimento de política para que suas políticas entrem em vigor.

1. [Crie políticas](#create) para seus usuários e IDs de serviço.

2. Para ativar o cumprimento de política, execute o comando [`bx cr iam-policies-enable`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_iam_policies_enable).

    Deve-se ter a função de Gerenciador na conta para que seja possível executar o comando `ibmcloud cr iam-policies-enable`. Você automaticamente tem a função de Gerenciador em sua própria conta.
    {: tip}
