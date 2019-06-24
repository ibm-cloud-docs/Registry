---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: IBM Cloud Container Registry, public images, commands, questions, registry, faq, Vulnerability Advisor,

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
{:faq: data-hd-content-type='faq'}

# Perguntas mais frequentes (FAQs)
{: #registry_faq}

Perguntas mais frequentes sobre o {{site.data.keyword.registrylong}}.
{: shortdesc}

## Como listar imagens públicas?
{: #faq_list_public_images}
{: faq}

Para listar imagens públicas, execute os comandos `ibmcloud` a seguir para ter como destino o registro global e listar as imagens públicas fornecidas pela IBM:

```
ibmcloud cr region-set global
```
{: pre}

```
ibmcloud cr images --include-ibm
```
{: pre}

## Posso usar ferramentas que não são do Docker para construir minhas imagens e enviá-las por push para o registro?
{: #faq_tools}
{: faq}

Sim, desde que a ferramenta suporte o formato e o protocolo de imagem do OCI.

## Como utilizo o controle de acesso com o IAM?
{: #faq_access_control}
{: faq}

É possível criar políticas do {{site.data.keyword.IBM_notm}}{{site.data.keyword.iamshort}} (IAM) para controlar o acesso aos seus namespaces no {{site.data.keyword.registrylong_notm}}. Para obter mais informações, consulte [Tutorial: concedendo acesso aos recursos do {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam_access) e [Gerenciando o acesso de usuário com o Identity and Access Management](/docs/services/Registry?topic=registry-iam).

## Quais regiões estão disponíveis para o {{site.data.keyword.registrylong_notm}}?
{: #faq_regions}
{: faq}

É possível hospedar imagens em [regiões locais](/docs/services/Registry?topic=registry-registry_overview#registry_regions_local). As imagens públicas hospedadas pela IBM estão disponíveis no [Registro global](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).

## Por que eu recebo uma mensagem de erro de varredura não localizada para uma imagem recém-incluída?
{: #faq_va_new_scan_error}
{: faq}

Se você receber o relatório de vulnerabilidade imediatamente após incluir a imagem no registro, você poderá receber o erro a seguir:

```
BXNVA0009E:  <imagename> não foi varrida. Tente novamente mais tarde.
Se esse problema persistir, entre em contato com o suporte para obter ajuda; veja https://console.bluemix.net/docs/support/index.html#contacting-support
```
{: screen}

Você recebe essa mensagem porque os resultados das imagens são varridos assincronicamente para as solicitações e o processo de varredura leva algum tempo para ser concluído. Durante a operação normal, a varredura é concluída dentro dos primeiros minutos após a inclusão da imagem no registro, dependendo de variáveis como o tamanho da imagem e a quantia de tráfego que o registro está recebendo.

Se você receber essa mensagem como parte de um pipeline de construção e vir esse erro regularmente, tente incluir alguma lógica de nova tentativa que contenha uma pausa curta.

Se você ainda vir um desempenho inaceitável, entre em contato com o suporte. Consulte [Obtendo ajuda e suporte para o {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-ts_index#gettinghelp).

## Como uma varredura do Vulnerability Advisor é acionada?
{: #faq_va_trigger_scan}
{: faq}

A varredura de uma imagem é acionada de uma das maneiras a seguir:

- Se uma nova imagem for enviada por push para o registro.
- Se a imagem não tiver sido varrida por 7 dias, ela será enfileirada para nova varredura, o que pode levar algum tempo para ser concluído.
- Se um novo aviso de segurança for liberado para um pacote instalado na imagem, ele será enfileirado para nova varredura, o que pode levar algum tempo para ser concluído. As novas varreduras que são acionadas pela liberação de novos avisos de segurança estão disponíveis somente para imagens do Ubuntu e do Debian.

## Com que frequência os avisos de segurança são atualizados?
{: #faq_va_update_security_notice}
{: faq}

Os avisos de segurança para o Vulnerability Advisor são carregados dos sites do sistema operacional de fornecedores aproximadamente a cada 12 horas.
