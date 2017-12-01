---

copyright:
  years: 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Comandos do {{site.data.keyword.registrylong_notm}} (`bx cr`)
para gerenciar imagens do Docker em seu namespace
{: #registry_cli_reference}

É possível usar o plug-in de registro de contêiner para configurar seu próprio namespace de imagem em um registro privado hospedado e gerenciado pela IBM, no qual é possível armazenar e compartilhar
de forma segura as imagens do Docker com todos os usuários em sua conta do {{site.data.keyword.Bluemix}}.
{:shortdesc}


## Comandos bx cr
{: #registry_cli_reference_bxcr}

Execute os comandos bx cr na CLI do {{site.data.keyword.registryshort_notm}}.
{:shortdesc}

Para comandos suportados, veja [CLI do {{site.data.keyword.registrylong_notm}}](../../cli/plugins/registry/index.html#containerregcli).

## Formatando e filtrando a saída da CLI para comandos do {{site.data.keyword.registrylong_notm}}
{: #registry_cli_listing}

É possível formatar e filtrar a saída da CLI para comandos suportados do {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Por padrão, a saída da CLI é exibida em um formato legível. No entanto, essa visualização poderá limitar a sua capacidade de usar a saída, especialmente se o comando for executado programaticamente. Por exemplo, na saída da CLI `bx cr image-list`, você pode desejar classificar o campo `Size` por tamanho numérico, mas o comando retorna uma descrição de sequência do tamanho. O plug-in de registro de contêiner fornece a opção de formato que pode ser usada para aplicar um modelo Go à saída da CLI. O modelo Go é um recurso da [linguagem de programação Go](https://golang.org/pkg/text/template/) que permite customizar a saída da CLI.

É possível alterar a saída da CLI aplicando a opção de formato de duas maneiras diferentes:

1.  Formatar dados em sua saída da CLI. Por exemplo, mude a saída de campo `Created` de horário UNIX para horário padrão.
2.  Filtrar dados em sua saída da CLI. Por exemplo, filtre por detalhes da imagem para exibir um subconjunto específico de imagens usando a condição `if gt` do modelo Go.

É possível usar a opção de formato com os comandos do {{site.data.keyword.registrylong_notm}} a seguir. Clique em um comando para visualizar uma lista de campos disponíveis e os seus tipos de dados.

-   [bx cr image-list](registry_cli_reference.html#registry_cli_listing_imagelist)
-   [bx cr image-inspect](registry_cli_reference.html#registry_cli_listing_imageinspect)
-   [bx cr token-list](registry_cli_reference.html#registry_cli_listing_tokenlist)

Os exemplos de código a seguir demonstram como você pode usar as opções de formatação e filtragem.

-   Execute o comando a seguir para exibir o repositório, a tag e o status de vulnerabilidade de todas as imagens que tenham um tamanho acima de 1 MB:

    ```
    bx cr image-list --format "{{ if gt .Size 1000000 }}{{ .Repository }}:{{ .Tag }} {{ .Vulnerable }}{{end}}"
    ```
    {: pre}

    Saída de exemplo:

    ```
    example-registry.<region>.bluemix.net/user1/ibmliberty:latest OK
    example-registry.<region>.bluemix.net/user1/ibmnode:1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode:test1 Vulnerable
    example-registry.<region>.bluemix.net/user1/ibmnode2:test2 Vulnerable
    ```
    {: screen}

-   Execute o comando a seguir para exibir em que local a documentação da IBM está hospedada para uma imagem pública da IBM especificada:

    ```
    bx cr image-inspect ibmliberty --format "{{ .ContainerConfig.Labels }}"

    ```
    {: pre}

    Saída de exemplo:

    ```
    map[doc.url:/docs/images/docker_image_ibmliberty/ibmliberty_starter.html]
    ```
    {: screen}

-   Execute o comando a seguir para exibir as portas expostas para uma imagem especificada:

    ```
    bx cr image-inspect ibmliberty --format "{{ .Config.ExposedPorts }}"

    ```
    {: pre}

    Saída de exemplo:

    ```
    map[9080/tcp: 9443/tcp:]
    ```
    {: screen}

-   Execute o comando a seguir para exibir todos os tokens somente leitura:

    ```
    bx cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
    ```
    {: pre}

    Saída de exemplo:

    ```
    0a3fb35f-e8eb-5232-b9fb-b1bdcb36d68a - 1495798639 - true - demo
    ```
    {: screen}


### Opções e tipos de dados do modelo Go no comando `bx cr image-list`
{: #registry_cli_listing_imagelist}

Revise a tabela a seguir para localizar as opções os tipos de dados do modelo Go disponíveis para o
comando `bx cr image-list`.
{:shortdesc}

|Campo|Type|descrição|
|-----|----|-----------|
|`Created`|Número Inteiro (64 bits)|Exibe quando a imagem é criada, expresso em número de segundos no [horário do Unix](https://en.wikipedia.org/wiki/Unix_time).|
|`Digest`|Sequência de Caracteres|Exibe o identificador exclusivo para uma imagem.|
|`Namespace`|Sequência de Caracteres|Exibe o namespace no qual a imagem é armazenada.|
|`Repository`|Sequência de Caracteres|Exibe o repositório da imagem.|
|`Size`|Número Inteiro (64 bits)|Exibe o tamanho da imagem em bytes.|
|`Tag`|Sequência de Caracteres|Exibe a tag para a imagem.|
|`Vulnerable`|Sequência de Caracteres|Exibe o status de vulnerabilidade para a imagem. Os status possíveis são descritos em [Gerenciando a segurança de imagens com o Vulnerability Advisor](../va/va_index.html).|
{: caption="Tabela 1. Campos e tipos de dados disponíveis no comando bx cr image-list." caption-side="top"}

### Opções e tipos de dados do modelo Go no comando `bx cr image-inspect`
{: #registry_cli_listing_imageinspect}

Revise a tabela a seguir para localizar as opções os tipos de dados do modelo Go disponíveis para o
comando `bx cr image-inspect`.
{:shortdesc}

|Campo|Type|descrição|
|-----|----|-----------|
|`ID`|Sequência de Caracteres|Exibe o identificador exclusivo para uma imagem.|
|`Parent`|Sequência de Caracteres|Exibe o ID da imagem pai que foi usada para construir essa imagem.|
|`Comment`|Sequência de Caracteres|Exibe a descrição da imagem.|
|`Created`|Sequência de Caracteres|Exibe o [registro de data e hora do Unix](https://en.wikipedia.org/wiki/Unix_time) de quando a imagem é criada.|
|`Contêiner`|Sequência de Caracteres|Exibe o ID do contêiner que criou a imagem.|
|`ContainerConfig`|Objeto|Exibe a configuração padrão para contêineres que são iniciados por meio dessa imagem. Veja detalhes do campo em [Configuração](registry_cli_reference.html#config).|
|`DockerVersion`|Sequência de Caracteres|Exibe a versão do Docker que foi usada para construir essa imagem.|
|`Autor`|Sequência de Caracteres|Exibe o autor da imagem.|
|`Config`|Objeto|Exibe os metadados de configuração para a imagem. Veja detalhes do campo em [Configuração](registry_cli_reference.html#config).|
|`Architecture`|Sequência de Caracteres|Exibe a arquitetura do processador que foi usada para construir essa imagem e que é necessária para executar a imagem.|
|`S.O.`|Sequência de Caracteres|Exibe a família do sistema operacional que foi usada para construir essa imagem e que é necessária para executar a imagem.|
|`OsVersion`|Sequência de Caracteres|Exibe a versão do sistema operacional que foi usada para construir essa imagem.|
|`Size`|Número Inteiro (64 bits)|Exibe o tamanho da imagem em bytes.|
|`VirtualSize`|Número Inteiro (64 bits)|Exibe a soma do tamanho de cada camada na imagem em bytes.|
|`RootFS`|Objeto|Exibe os metadados que descrevem o sistema de arquivos raiz para a imagem. Veja detalhes do campo em [RootFS](registry_cli_reference.html#rootfs).|
{: caption="Tabela 2. Campos e tipos de dados disponíveis no comando bx cr image-inspect." caption-side="top"}

#### Config

|Campo|Type|descrição|
|-----|----|-----------|
|`Hostname`|Sequência de Caracteres|Exibe o nome do host do contêiner.|
|`Domainname`|Sequência de Caracteres|Exibe o nome completo do domínio do contêiner.|
|`User`|Sequência de Caracteres|Exibe o usuário que executa comandos dentro do contêiner no qual a imagem é usada.|
|`AttachStdin`|Booleano|Exibirá _true_ se o fluxo de entrada padrão estiver anexado ao contêiner e _false_ se não estiver.|
|`AttachStdout`|Booleano|Exibirá _true_ se o fluxo de saída padrão estiver anexado ao contêiner e _false_ se não estiver.|
|`AttachStderr`|Booleano|Exibirá _true_ se o fluxo de erro padrão estiver anexado ao contêiner e _false_ se não estiver.|
|`ExposedPorts`|Mapa do valor da chave|Exibe a lista de portas expostas no formato `[123:,456:]`.|
|`Tty`|Booleano|Exibirá _true_ se um pseudo-tty estiver alocado para o contêiner e _false_ se não estiver.|
|`OpenStdin`|Booleano|Exibirá _true_ se o fluxo de entrada padrão estiver aberto e _false_ se o fluxo de entrada padrão estiver fechado.|
|`StdinOnce`|Booleano|Exibirá _true_ se o fluxo de entrada padrão for fechado após o cliente conectado se desconectar e _false_ se o fluxo de entrada padrão permanecer aberto.|
|`Enviar`|Matriz de sequências|Exibe a lista de variáveis de ambiente no formulário de pares de valores da chave.|
|`Cmd`|Matriz de sequências|Descreve os comandos e argumentos que serão transmitidos para um contêiner a serem executados quando o contêiner for iniciado.|
|`Verificação de funcionamento`|Objeto|Descreve como verificar se o contêiner está funcional. Veja detalhes do campo em [Verificação de funcionamento](registry_cli_reference.html#healthcheck).|
|`ArgsEscaped`|Booleano|Exibirá true se o comando já estiver escapado (específico do Windows).|
|`Image`|Sequência de Caracteres|Exibe o nome da imagem que foi transmitida pelo operador.|
|`Volumes`|Mapa do valor da chave|Exibe a lista de montagens do volume que são montadas em um contêiner.|
|`WorkingDir`|Sequência de Caracteres|Exibe o diretório ativo dentro do contêiner no qual os comandos especificados são executados.|
|`PontoDeEntrada`|Matriz de sequências|Descreve o comando que é executado quando o contêiner é iniciado.|
|`NetworkDisabled`|Booleano|Exibirá _true_ se a rede estiver desativada para o contêiner e _false_ se a rede estiver ativada para o contêiner.|
|`MacAddress`|Sequência de Caracteres|Exibe o endereço de Controle de Acesso à Mídia MAC que está designado para o contêiner.|
|`OnBuild`|Matriz de sequências|Exibe os metadados ONBUILD que foram definidos no Dockerfile de imagem.|
|`Labels`|Mapa do valor da chave|Exibe a lista de rótulos que foram incluídos na imagem como pares de valores da chave.|
|`StopSignal`|Sequência de Caracteres|Descreve o sinal de parada do UNIX para enviar quando parar o contêiner.|
|`StopTimeout`|Número inteiro|Exibe o tempo limite em segundos para parar um contêiner.|
|`Cobertura`|Matriz de sequências|Exibe o formulário de shell de RUN, CMD, ENTRYPOINT.|
{: caption="Tabela. " caption-side="top"}

#### Verificação de funcionamento

|Campo|Type|descrição|
|-----|----|-----------|
|`Test`|Matriz de sequências|Exibe como executar o teste de verificação de funcionamento. As opções disponíveis são:<ul><li>{}: herdam a verificação de funcionamento</li><li>{"NONE"}: a verificação de funcionamento é desativada</li><li>{"CMD", args...}: argumentos exec diretamente</li><li>{"CMD-SHELL", command}: execute o comando com o shell padrão do sistema</li></ul>|
|`Interval`|Número Inteiro (64 bits)|Exibe o tempo para esperar entre as verificações de funcionamento em nanossegundos.|
|`Timeout`|Número Inteiro (64 bits)|Exibe o tempo para esperar antes de considerar a verificação de funcionamento como tendo falhado em nanossegundos.|
|`Retries`|Número inteiro|Exibe o número de falhas consecutivas que são necessárias para considerar um contêiner como inoperante.|
{: caption="Tabela 4. Campos e tipos de dados disponíveis na estrutura de Verificação de funcionamento." caption-side="top"}

#### RootFS

|Opção|Type|descrição|
|------|----|-----------|
|`Type`|Sequência de Caracteres|Exibe o tipo de sistema de arquivo.|
|`Layers`|Matriz de sequências|Exibe os descritores de cada camada de imagem.|
|`BaseLayer`|Sequência de Caracteres|Exibe o descritor para a camada base na imagem.|
{: caption="Tabela 5. Campos e tipos de dados disponíveis na estrutura RootFS." caption-side="top"}

### Opções e tipos de dados do modelo Go no comando `bx cr token-list`
{: #registry_cli_listing_tokenlist}

Revise a tabela a seguir para localizar as opções os tipos de dados do modelo Go disponíveis para o
comando `bx cr token-list`.
{:shortdesc}

|Campo|Type|descrição|
|-----|----|-----------|
|`ID`|Sequência de Caracteres|Exibe o identificador exclusivo para um token.|
|`Expiry`|Número Inteiro (64 bits)|Exibe o [registro de data e hora do Unix](https://en.wikipedia.org/wiki/Unix_time) de quando o token expira.|
|`ReadOnly`|Booleano|Exibe _true_ quando é possível puxar imagens apenas e _false_ quando é possível
enviar por push e puxar imagens para e do seu namespace.|
|`Description`|Sequência de Caracteres|Exibe a descrição do token.|
{: caption="Tabela 6. Campos e tipos de dados disponíveis no comando bx cr token-list." caption-side="top"}
