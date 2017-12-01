---

copyright:
  years: 2017
lastupdated: "2017-10-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip} 
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# Detecção de Problemas
{: #ts_index}

Aqui estão as respostas para perguntas comuns sobre
resolução de problemas no uso do {{site.data.keyword.registrylong}}.
{:shortdesc}


## Obtendo ajuda e suporte para o {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Se tiver problemas ou perguntas quando estiver usando o {{site.data.keyword.registrylong_notm}},
será possível obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte da {{site.data.keyword.IBM_notm}}.

Quando você estiver usando os fóruns para fazer uma pergunta, marque a sua pergunta para que ela seja vista pela equipe de desenvolvimento do {{site.data.keyword.registrylong_notm}}.

-   Se você tiver questões técnicas sobre como desenvolver ou implementar um app com o {{site.data.keyword.registrylong_notm}}, poste sua pergunta no [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) e marque a sua pergunta com `ibm-bluemix` e `registro de contêiner`.
-   Para perguntas sobre o serviço e instruções de introdução, use o fórum do [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Inclua as tags `bluemix` e `registro de contêiner`.

Consulte
[Obtendo
ajuda](../../support/index.html#getting-help) para mais detalhes sobre como usar os fóruns.

Para obter informações sobre como abrir um chamado de suporte do {{site.data.keyword.IBM_notm}} ou sobre níveis de suporte e severidades de chamado, veja [Entrando em contato com o suporte](../../support/index.html#contacting-support).

## O login no {{site.data.keyword.registrylong_notm}} falha
{: #ts_login}

Não é possível efetuar login no {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
O comando `bx cr login` falha.

{: tsCauses}
-   O plug-in de registro de contêiner está desatualizado e precisa ser atualizado.
-   O Docker não está instalado em sua máquina local ou não está em execução.
-   Suas credenciais de login do {{site.data.keyword.Bluemix_notm}} expiraram.

{: tsResolve}
É possível corrigir esse problema das maneiras a seguir:

-   Faça upgrade para a versão mais recente do plug-in do {{site.data.keyword.registryshort_notm}}, veja [Atualizando o plug-in do {{site.data.keyword.registrylong_notm}} (`bx cr`)](registry_setup_cli_namespace.html#registry_cli_update).
-   Assegure-se de que o Docker esteja instalado em sua máquina. Se ele já estiver instalado, reinicie o daemon do Docker.
-   Execute novamente o comando `bx login` para atualizar as credenciais de login do {{site.data.keyword.Bluemix_notm}}.


## Os comandos do {{site.data.keyword.registrylong_notm}} falham com `'cr' is not a registered command. See 'bx help'. `
{: #ts_login_error}

Não é possível executar um comando `bx cr` porque `cr` não é um comando `bx` registrado.

{: tsSymptoms}
Você vê uma mensagem de erro semelhante a uma das mensagens de erro a seguir: 

```
bx cr login 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

```
bx cr namespace 
'cr' is not a registered command. See 'bx help'. 
```
{: pre}

{: tsCauses}
-   O plug-in de registro de contêiner não está instalado.


{: tsResolve}
É possível corrigir esse problema da maneira a seguir:

-   Instale o plug-in de registro de contêiner, veja [Instalando o plug-in da CLI do {{site.data.keyword.registryshort_notm}} (bx cr)](registry_setup_cli_namespace.html#registry_cli_install).


## Falha na configuração de um namespace
{: #ts_problem}

{: tsSymptoms}
Quando você executa `bx cr namespace-add`, não é possível configurar seu valor inserido como o namespace.

{: tsCauses}
-   Você inseriu um valor de namespace que já está sendo usado por outra organização do {{site.data.keyword.Bluemix_notm}}.
-   Um namespace foi excluído recentemente e você está reutilizando o seu nome. Se o namespace que foi excluído
continha muitos recursos, a exclusão ainda não poderá ser totalmente processada pelo {{site.data.keyword.registrylong_notm}}.
-   Você usou caracteres inválidos no valor de namespace.

{: tsResolve}
É possível corrigir esse problema das maneiras a seguir:

-   Siga as instruções que aparecem na mensagem de erro retornada.
-   Verifique se você inseriu um namespace válido:
    -   O namespace deve ter de 4 a 30 caracteres de comprimento.
    -   O namespace deve iniciar com pelo menos uma letra ou um número.
    -   O namespace deve conter somente letras minúsculas, números ou sublinhados (_).
-   Escolha um valor diferente para o seu namespace.
-   Se você estiver recriando um namespace que foi excluído e ele continha muitas imagens, tente novamente mais tarde.

## Falha ao enviar por push ou puxar uma imagem do Docker
{: #ts_pushpull}

{: tsSymptoms}
Ao executar comandos para enviar por push ou puxar imagens do Docker, você receberá uma mensagem
de erro. A
mensagem de erro varia dependendo da causa raiz. Potenciais mensagens de erro podem ser:

```
Você excedeu a sua cota de armazenamento. Exclua uma ou mais imagens ou revise a sua cota de armazenamento e o plano de precificação
```
{: screen}

```
Você excedeu a sua cota de tráfego extraído para o mês atual. Revise a sua cota de tráfego extraído e o plano de precificação
```
{: screen}

```
desautorizado: autenticação necessária
```
{: screen}

```
negado: o acesso solicitado ao recurso foi negado
```
{: screen}

{: tsCauses}
-   O Docker não está instalado.
-   O cliente Docker não está com login efetuado no {{site.data.keyword.registrylong_notm}}.
-   Seu token de acesso do {{site.data.keyword.Bluemix_notm}} pode ter expirado.
-   Você excedeu o limite de cota para armazenamento ou tráfego extraído que está configurado para a sua conta do {{site.data.keyword.Bluemix_notm}}.

{: tsResolve}
É possível corrigir esse problema das maneiras a seguir:

-   [Assegure-se de que o Docker esteja instalado em sua máquina](index.html#registry_cli_install).
-   Verifique seu caminho de instalação do Docker.
-   Efetue login no {{site.data.keyword.Bluemix_notm}} executando
`bx login`. Em seguida, efetue login na CLI do {{site.data.keyword.registrylong_notm}} executando `bx cr
login`.
-   [Revise os limites de cota e uso para armazenar e puxar imagens do Docker no {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).

## Não é possível puxar a imagem mais recente usando a tag mais recente
{: #ts_docker_latest}

{: tsSymptoms}
Você está tentando executar o comando `docker pull`, mas ele retornou uma
versão de sua imagem que não é a versão mais recente construída.

{: tsCauses}
A tag `latest` é aplicada por padrão para referenciar uma imagem quando você executa comandos
do Docker sem especificar o valor de tag. A tag `latest` é aplicada ao comando
`docker build` ou `docker tag` mais recente que foi executado sem um valor
de tag configurado explicitamente. Portanto, é possível executar comandos `docker` fora de ordem
ou configurar explicitamente tags em algumas imagens e a tag `latest` para consultar uma construção
que não é a mais recente.

{: tsResolve}
Geralmente, é melhor definir explicitamente uma tag sequencial diferente para suas imagens
toda vez e não depender da tag `latest`.

## O acesso ao registro com um firewall customizado falha
{: #ts_firewall}

{: tsSymptoms}
Você configura um firewall adicional em seu ambiente de desenvolvimento com configurações customizadas
para o tráfego de rede de entrada e de saída. Quando você tenta acessar o {{site.data.keyword.registrylong_notm}}, a conexão falha.

{: tsCauses}
Seu firewall customizado requer que determinados grupos de rede sejam abertos para o tráfego de rede de entrada e de saída para permitir a comunicação para e do registro.

{: tsResolve}
Abra os grupos de rede a seguir em seu firewall customizado.

1.  Observe o endereço IP público da máquina que você deseja usar para se conectar ao {{site.data.keyword.registrylong_notm}}. Se você estiver usando o Kubernetes, use o
endereço IP público do seu nó do trabalhador. Recupere o endereço IP público do seu nó do trabalhador executando `bx cs workers <cluster_name_or_id>`, em que *&lt;cluster_name_or_id&gt;* é o nome ou ID de seu cluster.
2.  No seu firewall, permita as seguintes conexões para e de sua máquina:
    -   Para conectividade de ENTRADA com a sua máquina, permita o tráfego de rede de entrada dos grupos de rede de
origem a seguir para o endereço IP público de destino da sua máquina.

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   Para conectividade de SAÍDA de sua máquina, use os mesmos grupos de rede e permita o tráfego de rede de
saída do endereço IP público de origem da sua máquina para esses grupos de rede.

