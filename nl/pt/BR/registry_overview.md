---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Sobre o {{site.data.keyword.registrylong_notm}}
{: #registry_overview}

Use o {{site.data.keyword.registrylong}} para armazenar com segurança
e acessar as imagens privadas do Docker em uma arquitetura altamente disponível e escalável.
{:shortdesc}

O {{site.data.keyword.registrylong_notm}} fornece um registro privado
de imagem de múltiplos locatários, altamente disponível e escalável que é hospedado e gerenciado pela IBM. É possível usar o registro privado configurando o seu próprio namespace de imagem e enviando por push imagens do Docker para o seu namespace.

<img src="images/registry_architecture.png" alt="Imagem mostrando como é possível interagir com o IBM Cloud Container Registry. O Container Registry contém os repositórios público e privado e as APIs para interagir com o serviço. O cliente Docker local pode fazer pull e enviar por push as imagens para/de seus repositórios privados no registro e pode fazer pull dos repositórios públicos. A UI da web do IBM Cloud (console) interage com a API do Container Registry para listar imagens. A CLI do Container Registry interage com a API para listar, criar, inspecionar e remover imagens, bem como outras funções administrativas. Seu cliente Docker local também pode fazer pull e enviar por push as imagens de seu armazenamento de imagem local para outros registros."/>

**Figura 1. Como o {{site.data.keyword.registrylong_notm}} interage com as imagens do Docker**

Uma imagem do Docker é a base para cada contêiner que você cria. Uma imagem é criada por meio
de um Dockerfile, que é um arquivo que contém instruções para construir a imagem. Um Dockerfile pode
referenciar os artefatos de construção em suas instruções que são armazenadas separadamente, como um app, a configuração
do app e suas dependências. As imagens geralmente são armazenadas em um registro que pode ser acessado pelo público (registro público) ou configurado com acesso
limitado para um pequeno grupo de usuários (registro privado). Usando o {{site.data.keyword.registrylong_notm}}, apenas os usuários com acesso à sua conta do {{site.data.keyword.Bluemix_notm}} podem acessar as suas imagens.

Ao enviar por push imagens para o {{site.data.keyword.registrylong_notm}}, você se beneficia dos recursos integrados do
Vulnerability Advisor que varrem potenciais problemas de segurança e vulnerabilidades. O Vulnerability Advisor verifica
se há pacotes vulneráveis em imagens base específicas do Docker e vulnerabilidades conhecidas em definições
de configuração do app. Quando vulnerabilidades forem localizadas, informações sobre a vulnerabilidade serão
fornecidas. É possível usar essas informações para resolver problemas de segurança para que contêineres não sejam implementados
por meio de imagens vulneráveis.

Revise a tabela a seguir para localizar uma visão geral de benefícios por usar o {{site.data.keyword.registrylong_notm}}.

|Benefício|descrição|
|-------|-----------|
|Registro privado altamente disponível e escalável|<ul><li>Configure o seu próprio namespace de imagem em um registro privado de múltiplos locatários, altamente disponível e escalável
que é hospedado e gerenciado pela IBM.</li><li>Armazene com segurança as suas imagens privadas do Docker e as compartilhe com os usuários em sua conta do {{site.data.keyword.Bluemix_notm}}.</li></ul>|
|Conformidade de segurança de imagem com o Vulnerability Advisor|<ul><li>Benefício da varredura automática de imagens em seu namespace.</li><li>Revise as recomendações que são específicas para o sistema operacional para corrigir potenciais
vulnerabilidades e proteger os seus contêineres de serem comprometidos.</li></ul>|
|Limites de cota para armazenamento e tráfego extraído|<ul><li>Benefício do armazenamento livre e de tráfego extraído para as suas imagens privadas até você atingir a sua
cota grátis.</li><li>Configure os limites de cota customizados para a quantia de armazenamento e de tráfego extraído por mês para evitar exceder
o seu nível de pagamento preferencial.</li></ul>|
{: caption="Tabela 1. Benefícios do {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Planos de serviço
{: #registry_plans}

É possível escolher entre os planos de serviço grátis ou padrão do {{site.data.keyword.registrylong_notm}}
para armazenar suas imagens do Docker e disponibilizar essas imagens para os usuários em sua conta do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

O plano de serviço do {{site.data.keyword.registrylong_notm}} determina a quantidade de armazenamento e extrai o tráfego que pode
ser usado para suas imagens privadas. O plano de serviço é associado à sua conta do {{site.data.keyword.Bluemix_notm}}
e os limites de armazenamento e o tráfego de extração de imagem são aplicados a todos os namespaces configurados em sua conta.

A tabela a seguir mostra os planos de serviço disponíveis do {{site.data.keyword.registrylong_notm}} e as suas características. Para obter mais informações sobre como o faturamento funciona e o que acontece ao exceder os limites do plano de serviço, veja [Limites de cota e faturamento no {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).

|Características|Livre|Padrão|
|---------------|----|--------|
|descrição|Experimente o registro privado no {{site.data.keyword.registrylong_notm}}
para armazenar e compartilhar com segurança suas imagens do Docker. Esse plano será o plano de serviço padrão ao configurar o seu
primeiro namespace no {{site.data.keyword.registrylong_notm}}.|Benefícios do armazenamento ilimitado e uso de tráfego de extração para gerenciar as imagens do Docker para todos os namespaces em sua conta
do {{site.data.keyword.Bluemix_notm}}.|
|Quantidade de armazenamento para imagens|500 MB|Ilimitado|
|Tráfego extraído|5 GB por mês|Ilimitado|
|Faturamento|Se você exceder seu armazenamento ou os limites de tráfego de extração, não será possível enviar por push nem
extrair imagens do seu namespace. Para obter mais informações, veja [Limites de cota e faturamento no {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).|<ul><li>Armazenamento: você é cobrado por Gigabyte/Meses de uso. Os primeiros 0,5 GB/mês são gratuitos. Depois, você é cobrado conforme indicado na calculadora de precificação.</li><li>Tráfego integral: você é cobrado por uso de Gigabyte por mês. Os primeiros 5 GB são livres. Depois, você é cobrado conforme indicado na calculadora de precificação. Se você exceder seu armazenamento ou os limites de tráfego de extração, não será possível enviar por push nem
extrair imagens do seu namespace. Para obter mais informações sobre armazenamento, tráfego de pull e calculadora de precificação, veja [Limites de cota e faturamento no {{site.data.keyword.registrylong_notm}}](#registry_plan_billing).</li></ul>|
{: caption="Tabela 2. Planos do {{site.data.keyword.registrylong_notm}}" caption-side="top"}

## Limites de cota e faturamento
{: #registry_plan_billing}

Localize informações e exemplos de como o processo de faturamento e limites de cota funcionam no
{{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Cada imagem é construída por meio de uma série de camadas que representam, cada uma, uma mudança incremental da imagem base. Quando você enviar por push ou puxar uma imagem, a quantia de armazenamento e tráfego extraído necessária para cada camada será incluída em seu uso mensal. Camadas idênticas são compartilhadas automaticamente entre as imagens em sua conta do {{site.data.keyword.Bluemix_notm}} e serão reutilizadas ao criar outras imagens. O armazenamento para cada camada idêntica é cobrado somente uma vez, independentemente de quantas imagens em sua conta referenciam a camada.

Exemplo para enviar imagens por push:

> Você envia por push uma imagem para o seu namespace que é baseada na imagem do Ubuntu. A imagem do Ubuntu contém várias camadas. Como você ainda não tem essas camadas em sua conta, a quantia de armazenamento que essas camadas requerem será incluída em seu uso mensal.
>
> Posteriormente, você cria uma segunda imagem que é baseada na imagem do Ubuntu. Você muda a imagem base do Ubuntu, por exemplo, incluindo comandos ou arquivos adicionais em seu Dockerfile. Cada mudança representa uma nova camada de imagem. Quando você enviar por push a segunda imagem, o {{site.data.keyword.registrylong_notm}} reconhecerá que todas as camadas da imagem base do Ubuntu já estão armazenadas em sua conta. Você não será cobrado por armazenar essas camadas uma segunda vez, mesmo que tenha enviado por push a sua imagem para outro namespace. O {{site.data.keyword.registrylong_notm}} determina o tamanho de todas as novas camadas e inclui a quantia de armazenamento em seu uso mensal.

### Faturamento para armazenamento e tráfego extraído
{: #registry_billing_traffic}

Dependendo do plano de serviço que escolher, você será cobrado pelo armazenamento e tráfego
extraído que usa por mês.
{:shortdesc}

**Armazenamento: **

  Cada plano de serviço do {{site.data.keyword.registrylong_notm}} é fornecido com uma determinada quantia de armazenamento que pode ser usada para armazenar com segurança as suas imagens do Docker nos namespaces de sua conta do {{site.data.keyword.Bluemix_notm}}. Se você estiver no plano padrão, você será cobrado por GB/mês de uso. Os primeiros 0,5 GB/mês são gratuitos. Se você estiver no plano grátis, será possível armazenar as suas imagens no {{site.data.keyword.registrylong_notm}} de graça até atingir os limites de cota para o plano grátis. Um GB/mês é uma média de 1 GB de armazenamento para um mês (730 horas).

  Exemplo para o plano padrão:

  > Você usa 5 GB em exatamente metade do mês e, depois, você envia várias imagens para o seu namespace e usa 10 GB pelo restante do mês. O seu uso mensal é calculado como segue:
  >
  > (5 GB x 0,5 (meses)) + (10 GB x 0,5 (meses)) = 2,5 + 5 = 7,5 GB/meses
  >
  > No plano padrão, os primeiros 0,5 GB/meses são grátis; portanto, você será cobrado por 7 GB/meses (7,5 GB/meses - 0,5 GB/meses).

  

**Puxe o tráfego: **

  Cada plano de serviço do {{site.data.keyword.registrylong_notm}} inclui uma determinada quantia de tráfego
extraído grátis para as suas imagens privadas que são armazenadas em seu namespace. Tráfego extraído é a largura da banda que você usa quando puxa uma camada de uma imagem do seu namespace para a sua máquina local. Se você estiver no plano padrão, será cobrado por GB de uso por mês. Os primeiros 5 GB cada mês são grátis. Se você estiver no plano grátis, será possível puxar imagens do seu namespace até atingir o limite de cota para o plano grátis.

  Exemplo para o plano padrão:

  > No mês, você extraiu imagens que contêm camadas com um tamanho total de 14 GB. O seu uso mensal é calculado como segue:
  >
  > No plano padrão, os primeiros 5 GB por mês são grátis; portanto, você será cobrado por 9 GB (14 GB - 5 GB).

  

### Limites de cota para armazenamento e tráfego extraído
{: #registry_quota_limits}

Dependendo do plano de serviço que você escolher, será possível enviar por push e puxar imagens para e de
seu namespace até que você atinja os seus limites de cota específicos do plano ou customizados.
{:shortdesc}

**Armazenamento: **

  Quando você atingir ou exceder os limites de cota para o seu plano, não será possível enviar por push qualquer imagem para os namespaces em sua conta do {{site.data.keyword.Bluemix_notm}} até você [liberar espaço removendo imagens](registry_quota.html#registry_quota_freeup) de seus namespaces ou [fazer upgrade para o plano padrão](#registry_plan_upgrade). Se você configurar os limites de cota para armazenamento em seu plano grátis ou padrão, também será possível [aumentar esse limite de cota](registry_quota.html#registry_quota_set) para ativar o envio por push de novas imagens novamente.

  Exemplo para o plano padrão:

  > O seu limite de cota atual para armazenamento está configurado como 1 GB. Todas as imagens privadas que são armazenadas nos namespaces de sua conta do {{site.data.keyword.Bluemix_notm}} já usam 900 MB desse armazenamento. Você tem 100 MB de armazenamento disponível até atingir o seu limite de cota. Um usuário deseja enviar por push uma imagem com um tamanho de 2 GB na máquina local. Como o limite de cota ainda não foi atingido, o {{site.data.keyword.registrylong_notm}} permite que o usuário envie por push esta imagem.
  >
  > Após o envio por push, o {{site.data.keyword.registrylong_notm}} determina o tamanho real da imagem em seu namespace, que pode variar do tamanho em sua máquina local e verifica se o limite para armazenamento é atingido. Neste exemplo, o uso de armazenamento aumenta de 900 MB para 2 GB. Com o seu limite de cota atual configurado como 1 GB, o {{site.data.keyword.registrylong_notm}} impede que você envie por push imagens adicionais para o namespace.

**Puxe o tráfego: **

  Quando você atingir ou exceder os limites de cota para o seu plano, não será possível puxar qualquer imagem dos
namespaces em sua conta do {{site.data.keyword.Bluemix_notm}}
até que você espere o próximo período de faturamento iniciar, [faça upgrade para o plano padrão](#registry_plan_upgrade) ou [aumente os seus limites
de cota para tráfego extraído](registry_quota.html#registry_quota_set).

  Exemplo para o plano padrão:

  > No mês, seu limite de cota para tráfego extraído está configurado para 5 GB. Você já puxou imagens de seus namespaces e usou
4,5 GB desse tráfego extraído. Você tem 0,5 GB de tráfego extraído disponível até atingir o seu limite
de cota. Um usuário deseja puxar uma imagem do seu namespace com um tamanho de 1 GB. Como o limite de
cota ainda não foi atingido, o {{site.data.keyword.registrylong_notm}} permite
que o usuário puxe essa imagem.
  >
  > Após a imagem ser puxada, o {{site.data.keyword.registrylong_notm}} determina a largura da banda que você usou
durante a extração e verifica se o limite para o tráfego extraído é atingido. Nesse exemplo, o uso do tráfego de extração aumenta de 4,5 GB para 5,5 GB. Com o seu limite de cota atual configurado como 5 GB, o {{site.data.keyword.registrylong_notm}} impede que você puxe imagens do
seu namespace.

### Estimando custos
{: #registry_estimating_costs}

Use a calculadora de precificação do {{site.data.keyword.Bluemix_notm}} para estimar o custo de seu plano.
{:shortdesc}

É possível precificar seu app usando as calculadoras de custo que são fornecidas pelo {{site.data.keyword.Bluemix_notm}}.

1.  Abra a folha de precificação, veja [Precificação do {{site.data.keyword.Bluemix_notm}}](https://www.ibm.com/cloud-computing/bluemix/pricing).
2.  Na seção **Pagar conforme o uso**, clique em **Estimar seus custos com a nossa calculadora**. A calculadora é aberta.
3.  Role até a seção **Registro de contêiner** na seção **Encargos de contêiner**.
4.  Insira suas estimativas de armazenamento e de tráfego nos campos fornecidos.

Seus custos estimados são exibidos na calculadora.

## Fazendo upgrade de seu plano de serviço
{: #registry_plan_upgrade}

É possível fazer upgrade do seu plano de serviços para obter benefícios de armazenamento ilimitado e de uso de tráfego extraído para gerenciar
as imagens do Docker para todos os namespaces na sua conta do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Se desejar descobrir qual plano de serviço você tem, execute o comando `ibmcloud cr plan`.

1.  Efetue login no {{site.data.keyword.Bluemix_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

    Se você tiver um ID federado, use `ibmcloud login --sso` para efetuar login na CLI do {{site.data.keyword.Bluemix_notm}}. Insira seu nome do usuário e use a URL fornecida na saída da CLI para recuperar sua senha descartável. Você sabe que tem um ID federado quando o login falha sem a opção `--sso` e é bem-sucedido com a opção `--sso`.
    {:tip}

2.  Faça upgrade para o plano padrão.

    ```
    ibmcloud cr plan-upgrade standard
    ```
    {: pre}

    Quando você tem uma conta Lite do {{site.data.keyword.Bluemix_notm}}, deve-se fazer upgrade para uma conta Pay As You Go ou de Assinatura do {{site.data.keyword.Bluemix_notm}} antes de executar `ibmcloud cr plan-upgrade`.
    {:tip}


## Aprendendo o básico
{: #registry_planning}

Prepare-se para armazenar e compartilhar suas imagens do Docker com o {{site.data.keyword.registrylong_notm}} com segurança,
aprendendo noções básicas de registro.
{:shortdesc}

Não coloque informações pessoais em imagens de contêiner, nomes de namespace, campos de descrição (por exemplo, em tokens de registro) ou em qualquer dado de configuração de imagem (por
exemplo, nomes ou rótulos de imagem).
{:tip}


### Entendendo os termos usados no {{site.data.keyword.registrylong_notm}}
{: #terms}


<dl>
  <dt>Registro</dt>
  <dd>Um registro é um serviço que fornece a infraestrutura para armazenar imagens do Docker e que pode ser acessado usando a URL do host de registro e uma porta opcional. Os registros podem ser acessados pelo público (registro público) ou configurados com acesso limitado para um pequeno grupo de usuários (registro privado). O {{site.data.keyword.registrylong_notm}} fornece um registro privado de imagens, altamente disponível e com diversos locatários, que é hospedado e gerenciado pela IBM. É possível usar
o registro privado configurando o seu próprio namespace de imagem e começar a enviar por push imagens do Docker para o seu
namespace.</dd>
</dl>

<dl>
  <dt>Namespace</dt>
  <dd>Os namespaces são uma maneira de organizar repositórios de suas imagens no {{site.data.keyword.registrylong_notm}}. O namespace está associado à sua
conta do {{site.data.keyword.Bluemix_notm}}. Ao configurar seu próprio namespace no {{site.data.keyword.registrylong_notm}}, o namespace é anexado à URL de registro conforme a seguir: <code>registry.<em>&lt;region&gt;</em>.bluemix.net/my_namespace</code>.

  Cada usuário em sua conta do {{site.data.keyword.Bluemix_notm}} pode
visualizar e trabalhar com imagens que estão armazenadas em seu namespace de registro. É possível configurar múltiplos namespaces, por exemplo, para ter repositórios separados para seus ambientes temporários e de produção.</dd>
</dl>

<dl>
  <dt>Repositório</dt>
  <dd>Um repositório de imagem é uma coleção de imagens identificadas e relacionadas no registro. O repositório é geralmente usado de forma intercambiável com a imagem, mas um repositório retém potencialmente múltiplas variantes identificadas de uma imagem.</dd>
</dl>

<dl>
  <dt>Image</dt>
  <dd>Um sistema de arquivos e seus parâmetros de execução usados dentro de um tempo de execução do contêiner para criar um contêiner. O sistema de arquivos consiste em uma série de camadas, combinadas no tempo de execução, criadas à medida que a imagem é construída por atualizações sucessivas. A imagem não retém o estado à medida que o contêiner é executado.</dd>
</dl>

<dl>
  <dt>Tag</dt>
  <dd>Uma tag é um identificador de uma imagem em um repositório. É possível usar tags para distinguir diferentes versões da mesma imagem base em um repositório. Quando você executa um comando do Docker e não especifica a tag de uma imagem do repositório, a imagem identificada como <code>latest</code> é usada por padrão.</dd>
</dl>

<dl>
  <dt>Dockerfile</dt>
  <dd>Um Dockerfile é um arquivo de texto que contém instruções para construir uma imagem do Docker. Geralmente, uma imagem é construída sobre uma imagem base que contém um sistema operacional de base, como Ubuntu. É possível mudar incrementalmente a imagem base com suas instruções do Dockerfile para definir o ambiente que o app precisa executar. Cada mudança na imagem base descreve uma nova camada da imagem. É possível fazer múltiplas mudanças em uma única linha do Dockerfile. As instruções em um Dockerfile também podem referenciar os artefatos de construção que são armazenados separadamente, como um app, a configuração do app e suas dependências.</dd>
</dl>

Para saber mais sobre termos específicos do Docker, [consulte o glossário do Docker](https://docs.docker.com/glossary/).


### Planejando namespaces
{: #registry_namespaces}

O {{site.data.keyword.registrylong_notm}} fornece um registro privado de imagem de vários locatários que é hospedado e
gerenciado pela IBM. É possível armazenar e compartilhar suas imagens do Docker de forma segura nesse registro, configurando um namespace de
registro.
{:shortdesc}

É possível configurar múltiplos namespaces, por exemplo, para ter repositórios separados para seus
ambientes temporários e de produção. Se você deseja usar o registro em múltiplas regiões do {{site.data.keyword.Bluemix_notm}}, deve-se configurar um namespace para
cada região. Os nomes de namespace são exclusivos dentro de regiões. É possível usar o mesmo nome de namespace para cada região, a menos que
alguém já tenha um namespace com esse nome configurado nessa região.

Para trabalhar somente com as imagens públicas fornecidas pela IBM, você não precisa configurar um
namespace.

Se você não tiver certeza se um namespace já está configurado para sua conta, execute o comando `ibmcloud cr namespace-list` para recuperar informações existentes de namespace. Se você for um cliente existente do {{site.data.keyword.containerlong_notm}} que usa [grupos de contêineres únicos e escaláveis](../../containers/cs_classic.html),
então já terá um namespace. É possível criar namespaces adicionais, mas não é possível executar `cf ic namespace set` para mais de um namespace.
{:tip}

Considere as regras a seguir ao escolher um namespace:

-   O namespace deve ser exclusivo em uma região do {{site.data.keyword.Bluemix_notm}}.
-   O namespace deve ter de 4 a 30 caracteres de comprimento.
-   O namespace deve iniciar com pelo menos uma letra ou um número.
-   O namespace deve conter somente letras minúsculas, números ou sublinhados (_).

Não coloque informações pessoais nos nomes de namespace.
{:tip}

Depois de configurar seu primeiro namespace, você é designado ao plano de serviço grátis do {{site.data.keyword.registrylong_notm}}, se ainda não tiver [feito upgrade de seu plano](#registry_plan_upgrade).

## Regiões
{: #registry_regions}

Os registros do {{site.data.keyword.registrylong_notm}} estão disponíveis em várias regiões.
{:shortdesc}

### Regiões locais
{: #registry_regions_local}

Uma região é uma área geográfica acessada por um terminal dedicado. Os registros do {{site.data.keyword.registrylong_notm}} estão disponíveis nas regiões a seguir:

-   ap-south: `registry.au-syd.bluemix.net`
-   eu-central: `registry.eu-de.bluemix.net`
-   uk-south: `registry.eu-gb.bluemix.net`
-   us-south: `registry.ng.bluemix.net`

Todos os artefatos de registro estão com escopo definido para o registro regional específico com o qual você está trabalhando atualmente. Por exemplo, namespaces, imagens, tokens, configurações de cota e configurações do plano devem ser gerenciados separadamente para cada registro regional.

Se desejar usar uma região diferente de sua região local, será possível destinar a região que você deseja acessar executando o comando `ibmcloud cr region-set`. É possível executar o comando sem parâmetros para obter uma lista de regiões disponíveis ou especificar a região como um parâmetro.

Para executar o comando com parâmetros, substitua _&lt;region&gt;_ pelo nome da região, por exemplo, `eu-central`.

```
ibmcloud cr region-set <region>
```
{: pre}

Por exemplo, para ter como destino a região eu-central, execute o comando a seguir:

```
ibmcloud cr region-set eu-central
```
{: pre}

Depois de destinar uma região diferente, efetue login no registro novamente: `ibmcloud cr login`.

### Registro Global
{: #registry_regions_global}

Está disponível um registro global que não tem nenhuma região incluída em seu nome (`registry.bluemix.net`). Somente imagens públicas fornecidas pela IBM são hospedadas nesse registro. Para gerenciar suas próprias imagens, por exemplo, ao configurar namespaces ou identificar e enviar imagens por push para um registro, use um [registro regional local](#registry_regions_local).
{:shortdesc}

É possível destinar o registro global executando o comando `ibmcloud cr region-set`.

Por exemplo, para ter como destino o registro global, execute o comando a seguir:

```
ibmcloud cr region-set global
```
{: pre}

Para obter mais informações sobre o comando `ibmcloud cr region-set`, consulte [CLI do {{site.data.keyword.registrylong_notm}}](registry_cli.html#bx_cr_region_set).

Depois de ter destinado o registro global, execute o comando `ibmcloud cr login` para registrar seu daemon local do Docker no registro global para que possa puxar as imagens públicas fornecidas pela {{site.data.keyword.IBM_notm}}.
