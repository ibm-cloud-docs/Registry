---

copyright:
  years: 2019
lastupdated: "2019-08-07"

keywords: IBM Cloud Container Registry, changelog, release notes, changes, user access, DNS names, regions,

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

# Notas sobre a liberação
{: #registry_release_notes}

Conheça as mudanças mais recentes para o {{site.data.keyword.registrylong}} e o Vulnerability Advisor. As mudanças são agrupadas por data.
{:shortdesc}

## 1 de agosto de 2019
{: #01aug2019}

<dl>
  <dt>O comando `ibmcloud cr retention-run` está disponível</dt>
  <dd>O comando `ibmcloud cr retention-run` limpa seus namespaces retendo imagens para cada repositório em um namespace no {{site.data.keyword.registrylong_notm}} aplicando critérios especificados. Todas as outras imagens no namespace são excluídas.
  
  Para obter mais informações, consulte [`ibmcloud cr retention-run`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_retention_run) e [Retendo imagens](/docs/services/Registry?topic=registry-registry_retention).</dd>
</dl>

## 25 de julho de 2019
{: #25jul2019}

<dl>
  <dt>{{site.data.keyword.at_full_notm}} disponível para o {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Use o serviço {{site.data.keyword.at_full_notm}} para controlar como os usuários e aplicativos interagem com o serviço {{site.data.keyword.registrylong_notm}} no {{site.data.keyword.cloud}}.

  Para obter mais informações, consulte [Eventos do Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>

## 1 de julho de 2019
{: #1jul2019}

<dl>
  <dt>O comando `ibmcloud cr token-add` não está mais disponível</dt>
  <dd>O comando `ibmcloud cr token-add` foi descontinuado. Não é mais possível incluir tokens de registro na CLI ou na API.</dd>
</dl>

## 27 de junho de 2019
{: #27jun2019}

<dl>
  <dt>O Container Scanner não está mais disponível</dt>
  <dd>O Container Scanner foi descontinuado. O Vulnerability Advisor ainda varre imagens que são enviadas por push para o {{site.data.keyword.registrylong_notm}}.</dd>
</dl>

## 13 de junho de 2019
{: #13jun2019}

<dl>
  <dt>Remover tags de imagens</dt>
  <dd>Remover uma ou diversas tags de cada imagem especificada no {{site.data.keyword.registrylong_notm}}.

  Para remover uma tag específica de uma imagem, mas manter a imagem subjacente e quaisquer outras tags, use o comando [`ibmcloud cr image-untag`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_untag). Se, em vez disso, desejar excluir a imagem subjacente e todas as suas tags, use o comando [`ibmcloud cr image-rm`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_rm).

  Para obter mais informações, consulte [Removendo tags de imagens em seu repositório privado do {{site.data.keyword.cloud_notm}}](/docs/services/Registry?topic=registry-registry_images_#registry_images_untag).</dd>
</dl>

## 13 de maio de 2019
{: #13may2019}

<dl>
  <dt>Término do suporte para o Container Scanner</dt>
  <dd>O Container Scanner agora está descontinuado e não é mais utilizável.

  Para obter mais informações, consulte [Instalando o Container Scanner (descontinuado)](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 2 de abril de 2019
{: #2apr2019}

<dl>
  <dt>Disponibilidade geral do Container Image Security Enforcement</dt>
  <dd>Use o Container Image Security Enforcement para verificar suas imagens de contêiner antes de implementá-las em seu cluster no {{site.data.keyword.containerlong_notm}}. É possível controlar de onde as imagens serão implementadas, aplicar as políticas do Vulnerability Advisor e assegurar-se de que a [confiança de conteúdo](/docs/services/Registry?topic=registry-registry_trustedcontent) seja aplicada corretamente à imagem.

  Para obter mais informações, consulte [Impondo a segurança da imagem de contêiner](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 14 de março de 2019
{: #14mar2019}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponível para o {{site.data.keyword.registrylong_notm}}</dt>
  <dd>Use o serviço {{site.data.keyword.cloudaccesstraillong_notm}} para controlar como os usuários e aplicativos interagem com o serviço {{site.data.keyword.registrylong_notm}} no {{site.data.keyword.cloud}}.

  Para obter mais informações, consulte [Eventos do Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).
</dd>
</dl>

## 25 de fevereiro de 2019
{: #25feb2019}

<dl>
  <dt>Novos nomes de domínio</dt>
  <dd>O {{site.data.keyword.registrylong_notm}} está adotando novos nomes de domínio. Os novos nomes de domínio estão disponíveis no console e na CLI. É possível usar os novos nomes de domínio `icr.io` agora. Os nomes de domínio `registry.bluemix.net` existentes foram descontinuados, mas será possível continuar a usá-los até o término da data de suporte. Uma data de término do suporte ainda não está disponível. Para obter mais informações, consulte [Regiões](/docs/services/Registry?topic=registry-registry_overview#registry_regions) e [Apresentando os novos nomes de domínio do IBM Cloud Container Registry ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/blog/announcements/introducing-new-ibm-cloud-container-registry-domain-names).

  As assinaturas se aplicam ao nome inteiro da imagem, que inclui o nome do domínio. Se você estiver usando a confiança de conteúdo, deverá incluir novas assinaturas para que seja possível consumir a confiança de conteúdo sob o novo nome de domínio. Para obter mais informações sobre a assinatura de imagens, consulte [Assinando imagens para conteúdo confiável](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

<dl>
  <dt>Segredos de pull da chave de API do IAM para clusters do {{site.data.keyword.containerlong_notm}}</dt>
  <dd>Os novos segredos de pull da imagem de cluster para os domínios `icr.io` são autorizados usando uma chave de API do {{site.data.keyword.IBM_notm}}{{site.data.keyword.iamshort}} (IAM). Portanto, se você desejar ter mais controle sobre o acesso a seus recursos do {{site.data.keyword.registrylong_notm}}, será possível incluir políticas do IAM. Por exemplo, é possível mudar as políticas de chave de API no segredo de pull do cluster para que o pull das imagens seja feito somente de uma determinada região de registro ou namespace.
  
  Para obter mais informações, consulte [Entendendo como seu cluster é autorizado a extrair imagens do {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).</dd>
</dl>

<dl>
  <dt>Nova região no ap-north</dt>
  <dd>Uma nova região está disponível em `ap-north`. É possível usar a nova região usando o nome de domínio `jp.icr.io`.
  
  Para obter mais informações, consulte [Regiões](/docs/services/Registry?topic=registry-registry_overview#registry_regions).</dd>
</dl>

## 21 de fevereiro de 2019
{: #21feb2019}

<dl>
  <dt>Automatizando o acesso a seus namespaces</dt>
  <dd>Foi descontinuado o uso de tokens para automatizar o push e o pull de imagens do Docker de seus namespaces e para eles. Deve-se agora usar as chaves de API para automatizar seus namespaces do {{site.data.keyword.registrylong_notm}} para que seja possível enviar imagens por push e fazer pull delas.

  Para obter mais informações, consulte [Automatizando o acesso a seus namespaces usando chaves de API](/docs/services/Registry?topic=registry-registry_access#registry_api_key).</dd>
</dl>

## 8 de janeiro de 2019
{: #8jan2019}

 <dl>
  <dt>Término do suporte para a API do Vulnerability Advisor versão 2</dt>
  <dd>A versão 2 da API do Vulnerability Advisor foi descontinuada e não é mais utilizável. Use a versão 3 da API. Consulte [API do Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/container-registry/va).

  Para obter mais informações, consulte [Descontinuação da API do Vulnerability Advisor v2 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/cloud-archive/2018/12/vulnerability-advisor-v2-api-deprecation/).</dd>
</dl>

## 4 de outubro de 2018
{: #4oct2018}

<dl>
  <dt>Gerenciando o acesso de usuário</dt>
  <dd>Use o {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) para controlar o acesso por usuários ao {{site.data.keyword.registrylong_notm}} em sua conta. Quando as políticas do IAM são ativadas para sua conta no {{site.data.keyword.registrylong_notm}}, cada usuário que acessa o serviço em sua conta deve ter uma política de acesso designada com uma função de usuário do IAM definida. Essa política determina qual função o usuário tem dentro do contexto do serviço e quais ações o usuário pode executar.

  Para obter mais informações, consulte [Gerenciando o acesso de usuário com o {{site.data.keyword.iamshort}}](/docs/services/Registry?topic=registry-iam#iam), [Definindo políticas de função de acesso de usuário](/docs/services/Registry?topic=registry-user#user) e [Tutorial: Concedendo acesso aos recursos do IBM Cloud Container Registry](/docs/services/Registry?topic=registry-iam_access#iam_access).</dd>
</dl>

## 7 de agosto de 2018
{: #7aug2018}

<dl>
  <dt>Políticas de isenção disponíveis no Vulnerability Advisor</dt>
  <dd>Se você desejar gerenciar a segurança de uma organização do {{site.data.keyword.cloud_notm}}, será possível usar sua configuração de política para determinar se um problema está isento ou não. É possível usar o Container Image Security Enforcement para assegurar que a implementação seja permitida apenas por meio de imagens que não contêm problemas de segurança após a contabilidade para qualquer problema isento por sua política.

  Para obter mais informações, consulte [Configurando políticas de isenção organizacional](/docs/services/Registry?topic=va-va_index#va_managing_policy).</dd>
</dl>

## 25 de julho de 2018
{: #25jul2018}

<dl>
  <dt>{{site.data.keyword.cloudaccesstrailfull_notm}} disponível para o Vulnerability Advisor</dt>
  <dd>Use o serviço {{site.data.keyword.cloudaccesstrailfull_notm}} para controlar como os usuários e aplicativos interagem com o serviço {{site.data.keyword.registrylong_notm}} no {{site.data.keyword.cloud}}.

  Para obter mais informações, consulte [Eventos do Activity Tracker](/docs/services/Registry?topic=registry-at_events#at_events).</dd>
</dl>
  
## 12 de julho de 2018
{: #12jul2018}

<dl>
  <dt>API do Vulnerability Advisor versão 3</dt>
  <dd>A versão 3 da API muda o comportamento dos terminais de API que são usados para listar isenções. Deve-se verificar se o uso da API não depende do comportamento da versão 2.

  Para obter mais informações, consulte [Vulnerability Advisor for {{site.data.keyword.registrylong_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/container-registry/va).</dd>
</dl>

## 31 de maio de 2018
{: #31may2018}

<dl>
  <dt>Use o Helm para imagens do Passport Advantage</dt>
  <dd>Importe o software {{site.data.keyword.IBM_notm}} que é transferido por download de [IBM Passport Advantage Online for customers ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/software/passportadvantage/pao_customer.html) e empacotado para uso com o Helm em seu namespace do {{site.data.keyword.registrylong_notm}}.

  Para obter mais informações, consulte [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_ppa_archive_load).</dd>
</dl>

## 21 de março de 2018
{: #21mar2018}

<dl>
  <dt>Scanner de contêiner</dt>
  <dd>O Container Scanner permite que o Vulnerability Advisor relate qualquer problema localizado em contêineres em execução que não estão presentes na imagem base do contêiner.

  Para obter mais informações, consulte [Instalando o Container Scanner](/docs/services/Registry?topic=va-va_index#va_install_container_scanner).</dd>
</dl>

## 16 de março de 2018
{: #16mar2018}

<dl>
  <dt>Container Image Security Enforcement beta</dt>
  <dd>Use o Container Image Security Enforcement beta para verificar suas imagens de contêiner antes de implementá-las em seu cluster no {{site.data.keyword.containerlong_notm}}. É possível controlar de onde as imagens serão implementadas, aplicar as políticas do Vulnerability Advisor e assegurar-se de que a [confiança de conteúdo](/docs/services/Registry?topic=registry-registry_trustedcontent) seja aplicada corretamente à imagem.

  Para obter mais informações, consulte [Impondo a segurança da imagem de contêiner](/docs/services/Registry?topic=registry-security_enforce#security_enforce).</dd>
</dl>

## 20 de fevereiro de 2018
{: #20feb2018}

<dl>
  <dt>Conteúdo confiável</dt>
  <dd>O {{site.data.keyword.registrylong_notm}} fornece tecnologia de conteúdo confiável para que você possa assinar imagens para assegurar a integridade de imagens no namespace de registro. Ao puxar e enviar por push as imagens assinadas, é possível verificar se elas foram enviadas por push pela parte correta, como as ferramentas de integração contínua (CI).

  Para obter mais informações, veja [Assinando imagens para conteúdo confiável](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent).</dd>
</dl>

## 6 de novembro de 2017
{: #6nov2017}

<dl>
  <dt>Registro Global</dt>
  <dd>Um registro global está disponível. Ele não possui nenhuma região incluída em seu nome de domínio (`icr.io`). Somente imagens públicas que são fornecidas pela IBM são hospedadas nesse registro.

  Para obter mais informações, consulte [Registro global](/docs/services/Registry?topic=registry-registry_overview#registry_regions_global).</dd>
</dl>

## 29 de setembro de 2017
{: #29sep2017}

<dl>
  <dt>Construir imagens do Docker</dt>
  <dd>O comando `ibmcloud cr build` agora está disponível para executar construções de contêiner. É possível construir uma imagem Docker diretamente no {{site.data.keyword.cloud_notm}} ou criar uma imagem Docker
própria no computador local e transferi-la por upload (enviar por push) para o namespace no {{site.data.keyword.registrylong_notm}}.

  Para obter mais informações, consulte [Construindo imagens do Docker para usá-las com seu namespace](/docs/services/Registry?topic=registry-registry_images_#registry_images_creating) e [`ibmcloud cr build`](/docs/container-registry-cli-plugin?topic=container-registry-cli-plugin-containerregcli#bx_cr_build).</dd>
</dl>

## 24 de agosto de 2017
{: #24aug2017}

<dl>
  <dt>Interface gráfica com o usuário liberada</dt>
  <dd>A interface gráfica com o usuário do {{site.data.keyword.registrylong_notm}} está disponível no catálogo, consulte [Container Registry ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/kubernetes/catalog/registry).</dd>
</dl>

## 27 de junho de 2017
{: #27jun2017}

<dl>
  <dt>Disponibilidade geral do {{site.data.keyword.registrylong_notm}}</dt>
  <dd>O {{site.data.keyword.registrylong_notm}} está em disponibilidade geral como um serviço no {{site.data.keyword.cloud_notm}}. O {{site.data.keyword.registrylong_notm}} suporta o {{site.data.keyword.containerlong_notm}}.

  Para obter mais informações sobre o {{site.data.keyword.containerlong_notm}}, consulte o [Tutorial de introdução](/docs/containers?topic=containers-getting-started).</dd>
</dl>
