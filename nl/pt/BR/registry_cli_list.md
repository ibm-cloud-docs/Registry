---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-08"

keywords: IBM Cloud Container Registry, commands, format commands, filter command output, private registry, registry commands, formatting output, filtering output, output, Go template options, data types, 

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

# Formatando e filtrando a saída da CLI para comandos do {{site.data.keyword.registrylong_notm}}
{: #registry_cli_list}

É possível formatar e filtrar a saída da CLI para comandos suportados do {{site.data.keyword.registrylong}}.
{:shortdesc}

Por padrão, a saída da CLI é exibida em um formato legível. No entanto, essa visualização poderá limitar a sua capacidade de usar a saída, especialmente se o comando for executado programaticamente. Por exemplo, na saída da CLI `ibmcloud cr image-list`, talvez você queira classificar o campo `Size` pelo tamanho numérico, mas o comando retorna uma descrição de sequência do tamanho. O plug-in da CLI `container-registry` fornece a opção de formato que pode ser usada para aplicar um modelo Go à saída da CLI. O modelo Go é um recurso da [Linguagem de programação Go ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://golang.org/pkg/text/template/) que pode ser usado para customizar a saída da CLI.

É possível alterar a saída da CLI aplicando a opção de formato de duas maneiras diferentes:

1. Formatar dados em sua saída da CLI. Por exemplo, mude a saída do campo `Created` de horário do UNIX para horário padrão.
2. Filtrar dados em sua saída da CLI. Por exemplo, filtre por detalhes da imagem para exibir um subconjunto específico de imagens usando a condição `if gt` do modelo Go.

É possível usar a opção de formato com os comandos do {{site.data.keyword.registrylong_notm}} a seguir. Clique em um comando para visualizar uma lista de campos disponíveis e seus tipos de dados.

- [`ibmcloud cr image-list`](#registry_cli_list_imagelist)
- [`ibmcloud cr image-inspect`](#registry_cli_list_imageinspect)
- [`ibmcloud cr token-list`](#registry_cli_list_tokenlist)

Os exemplos de código a seguir demonstram como você pode usar as opções de formatação e filtragem.

- Execute o comando `ibmcloud cr image-list` a seguir para exibir o repositório, a tag e o status de segurança de todas as imagens com tamanho acima de 1 MB:

  ```
  ibmcloud cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .SecurityStatus.Status }}{{end}}"
  ```
  {: pre}

  A mensagem a seguir é um exemplo da saída do comando:

  ```
  example-<region>.icr.io/user1/ibmliberty:latest No Issues
  example-<region>.icr.io/user1/ibmnode:1 2 Issues
  example-<region>.icr.io/user1/ibmnode:test1 1 Issue
  example-<region>.icr.io/user1/ibmnode2:test2 7 Issues
  ```
  {: screen}

- Execute o seguinte comando `ibmcloud cr image-inspect` para exibir onde a documentação do {{site.data.keyword.IBM_notm}} está hospedada para uma imagem pública do {{site.data.keyword.IBM_notm}} especificada:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"
  ```
  {: pre}

  A mensagem a seguir é um exemplo da saída do comando:

  ```
  map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
  ```
  {: screen}

- Execute o comando `ibmcloud cr image-inspect` a seguir para exibir as portas expostas de uma imagem especificada:

  ```
  ibmcloud cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"
  ```
  {: pre}

  A mensagem a seguir é um exemplo da saída do comando:

  ```
  map[9080/tcp: 9443/tcp:]
  ```
  {: screen}

- Execute o comando `ibmcloud cr token-list` a seguir para exibir todos os tokens somente leitura:

  ```
  ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
  ```
  {: pre}

  A mensagem a seguir é um exemplo da saída do comando:

  ```
  0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
  ```
  {: screen}

## Opções de modelo e tipos de dados de Go no comando `ibmcloud cr image-list`
{: #registry_cli_list_imagelist}

Revise a tabela a seguir para localizar opções de modelo e tipos de dados de Go disponíveis para o comando [`ibmcloud cr image-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_list).
{:shortdesc}

|Campo|Tipo|Descrição|
|-----|----|-----------|
|`Created`|Número Inteiro (64 bits)|Exibe quando a imagem foi criada, expresso em número de segundos no [horário do UNIX ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://en.wikipedia.org/wiki/Unix_time).|
|`Digest`|Sequência de Caracteres|Exibe o identificador exclusivo para uma imagem.|
|`Namespace`|Sequência de Caracteres|Exibe o namespace no qual a imagem é armazenada.|
|`Repository`|Sequência de Caracteres|Exibe o repositório da imagem.|
|`SecurityStatus`|Estrut.|Exibe o status de vulnerabilidade para a imagem. É possível filtrar e formatar os valores a seguir: *Status*`string`, *IssueCount*`int` e *ExemptionCount*`int`. Os status possíveis são descritos em [Revisando um relatório de vulnerabilidade usando a CLI](/docs/services/Registry?topic=va-va_index#va_registry_cli).|
|`Size`|Número Inteiro (64 bits)|Exibe o tamanho da imagem em bytes.|
|`Tag`|Sequência de Caracteres|Exibe a tag para a imagem.|
{: caption="Tabela 1. Campos e tipos de dados disponíveis no comando <code>ibmcloud cr image-list</code>." caption-side="top"}

## Opções de modelo e tipos de dados de Go no comando `ibmcloud cr image-inspect`
{: #registry_cli_list_imageinspect}

Revise a tabela a seguir para localizar opções de modelo e tipos de dados disponíveis de Go para o comando [`ibmcloud cr image-inspect`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_image_inspect).
{:shortdesc}

|Campo|Tipo|Descrição|
|-----|----|-----------|
|`Architecture`|Sequência de Caracteres|Exibe a arquitetura do processador que foi usada para construir essa imagem e que é necessária para executar a imagem.|
|`Autor`|Sequência de Caracteres|Exibe o autor da imagem.|
|`Comment`|Sequência de Caracteres|Exibe a descrição da imagem.|
|`Config`|Objeto|Exibe os metadados de configuração para a imagem. Consulte os detalhes do campo em [`Configuração`](#registry_cli_list_imageinspect_config).|
|`Contêiner`|Sequência de Caracteres|Exibe o ID do contêiner que criou a imagem.|
|`ContainerConfig`|Objeto|Exibe a configuração padrão para contêineres que são iniciados por meio dessa imagem. Consulte os detalhes do campo em [`Configuração`](#registry_cli_list_imageinspect_config).|
|`Created`|Sequência de Caracteres|Exibe o [registro de data e hora do UNIX ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://en.wikipedia.org/wiki/Unix_time) quando a imagem foi criada.|
|`DockerVersion`|Sequência de Caracteres|Exibe a versão do Docker que foi usada para construir essa imagem.|
|`ID`|Sequência de Caracteres|Exibe o identificador exclusivo para uma imagem.|
|`S.O.`|Sequência de Caracteres|Exibe a família do sistema operacional que foi usada para construir essa imagem e que é necessária para executar a imagem.|
|`OsVersion`|Sequência de Caracteres|Exibe a versão do sistema operacional que foi usada para construir essa imagem.|
|`Parent`|Sequência de Caracteres|Exibe o ID da imagem pai que foi usada para construir essa imagem.|
|`RootFS`|Objeto|Exibe os metadados que descrevem o sistema de arquivos raiz para a imagem. Consulte os detalhes do campo em [`RootFS`](#registry_cli_list_imageinspect_rootfs).|
|`Size`|Número Inteiro (64 bits)|Exibe o tamanho da imagem em bytes.|
|`VirtualSize`|Número Inteiro (64 bits)|Exibe a soma do tamanho de cada camada na imagem em bytes.|
{: caption="Tabela 2. Campos e tipos de dados disponíveis no comando <code>ibmcloud cr image-inspect</code>." caption-side="top"}

### `Config`
{: #registry_cli_list_imageinspect_config}

|Campo|Tipo|Descrição|
|-----|----|-----------|
|`ArgsEscaped`|Booleano|Exibirá true se o comando já estiver escapado (específico do Windows).|
|`AttachStderr`|Booleano|Exibirá _true_ se o fluxo de erro padrão estiver anexado ao contêiner e _false_ se não estiver.|
|`AttachStdin`|Booleano|Exibirá _true_ se o fluxo de entrada padrão estiver anexado ao contêiner e _false_ se não estiver.|
|`AttachStdout`|Booleano|Exibirá _true_ se o fluxo de saída padrão estiver anexado ao contêiner e _false_ se não estiver.|
|`Cmd`|Matriz de sequências|Descreve os comandos e os argumentos passados para um contêiner executar quando for iniciado.|
|`Domainname`|Sequência de Caracteres|Exibe o nome completo do domínio do contêiner.|
|`PontoDeEntrada`|Matriz de sequências|Descreve o comando que é executado quando o contêiner é iniciado.|
|`Enviar`|Matriz de sequências|Exibe a lista de variáveis de ambiente no formulário de pares de valores da chave.|
|`ExposedPorts`|Mapa do valor da chave|Exibe a lista de portas expostas no formato `[123:,456:]`.|
|`Verificação de funcionamento`|Objeto|Descreve como verificar se o contêiner está funcionando corretamente. Consulte os detalhes do campo em [`Verificação de funcionamento`](#registry_cli_list_imageinspect_healthcheck).|
|`Hostname`|Sequência de Caracteres|Exibe o nome do host do contêiner.|
|`Image`|Sequência de Caracteres|Exibe o nome da imagem que foi transmitida pelo operador.|
|`Labels`|Mapa do valor da chave|Exibe a lista de rótulos que foram incluídos na imagem como pares de valores da chave.|
|`MacAddress`|Sequência de Caracteres|Exibe o endereço de Controle de Acesso à Mídia MAC que está designado para o contêiner.|
|`NetworkDisabled`|Booleano|Exibirá _true_ se a rede estiver desativada para o contêiner e _false_ se a rede estiver ativada para o contêiner.|
|`OnBuild`|Matriz de sequências|Exibe os metadados `ONBUILD` que foram definidos no Dockerfile de imagem.|
|`OpenStdin`|Booleano|Exibirá _true_ se o fluxo de entrada padrão estiver aberto e _false_ se o fluxo de entrada padrão estiver fechado.|
|`Cobertura`|Matriz de sequências|Exibe o formulário de shell de RUN, CMD, ENTRYPOINT.|
|`StdinOnce`|Booleano|Exibirá _true_ se o fluxo de entrada padrão for fechado após o cliente conectado se desconectar e _false_ se o fluxo de entrada padrão permanecer aberto.|
|`StopSignal`|Sequência de Caracteres|Descreve o sinal de parada do UNIX para enviar quando parar o contêiner.|
|`StopTimeout`|Número inteiro|Exibe o tempo limite em segundos para parar um contêiner.|
|`Tty`|Booleano|Exibe _true_ se um `pseudo-tty` estiver alocado para o contêiner e _false_ se não estiver.|
|`User`|Sequência de Caracteres|Exibe o usuário que executa comandos dentro do contêiner no qual a imagem é usada.|
|`Volumes`|Mapa do valor da chave|Exibe a lista de montagens do volume que são montadas em um contêiner.|
|`WorkingDir`|Sequência de Caracteres|Exibe o diretório ativo dentro do contêiner no qual os comandos especificados são executados.|
{: caption="Tabela 3. Campos e tipos de dados disponíveis em <code>Config</code>. " caption-side="top"}

### `Verificação de funcionamento`
{: #registry_cli_list_imageinspect_healthcheck}

|Campo|Tipo|Descrição|
|-----|----|-----------|
|`Interval`|Número Inteiro (64 bits)|Exibe o tempo para esperar entre as verificações de funcionamento em nanossegundos.|
|`Retries`|Número inteiro|Exibe o número de falhas consecutivas necessárias para que o funcionamento de um contêiner seja considerado incorreto.|
|`Test`|Matriz de sequências|Exibe como executar o teste de verificação de funcionamento. As opções disponíveis são:<ul><li>`{}`: herdam a verificação de funcionamento</li><li>`{"NONE"}`: a verificação de funcionamento é desativada</li><li>`{"CMD", args...}`: executam argumentos diretamente</li><li>`{"CMD-SHELL", command}`: executam o comando com o shell padrão do sistema</li></ul>|
|`Timeout`|Número Inteiro (64 bits)|Exibe o tempo para esperar antes de considerar a verificação de funcionamento como tendo falhado em nanossegundos.|
{: caption="Tabela 4. Campos e tipos de dados disponíveis na estrutura <code>Healthcheck</code>." caption-side="top"}

### `RootFS`
{: #registry_cli_list_imageinspect_rootfs}

|Opção|Tipo|Descrição|
|------|----|-----------|
|`BaseLayer`|Sequência de Caracteres|Exibe o descritor para a camada base na imagem.|
|`Layers`|Matriz de sequências|Exibe os descritores de cada camada de imagem.|
|`Type`|Sequência de Caracteres|Exibe o tipo de sistema de arquivo.|
{: caption="Tabela 5. Campos e tipos de dados disponíveis na estrutura <code>RootFS</code>." caption-side="top"}

## Opções de modelo e tipos de dados de Go no comando `ibmcloud cr token-list`
{: #registry_cli_list_tokenlist}

Revise a tabela a seguir para localizar opções de modelo e tipos de dados disponíveis de Go para o comando [`ibmcloud cr token-list`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_token_list).
{:shortdesc}

|Campo|Tipo|Descrição|
|-----|----|-----------|
|`Description`|Sequência de Caracteres|Exibe a descrição do token.|
|`Expiry`|Número Inteiro (64 bits)|Exibe o [registro de data e hora do UNIX ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://en.wikipedia.org/wiki/Unix_time) de quando o token expira.|
|`ID`|Sequência de Caracteres|Exibe o identificador exclusivo para um token.|
|`ReadOnly`|Booleano|Exibe _true_ quando é possível puxar imagens apenas e _false_ quando é possível enviar por push e puxar imagens para e do seu namespace.|
{: caption="Tabela 6. Campos e tipos de dados disponíveis no comando <code>ibmcloud cr token-list</code>." caption-side="top"}
