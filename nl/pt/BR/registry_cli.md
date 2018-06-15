---



copyright:
  years: 2017, 2018
lastupdated: "2018-05-31"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI (interface da linha de comandos)
{: #containerregcli}

A CLI do {{site.data.keyword.registrylong}} é um plug-in para gerenciar seu registro e seus recursos para sua conta. {{site.data.keyword.Bluemix_notm}}
{: shortdesc}

**Pré-requisitos**
* Antes de executar os comandos de registro, efetue login no {{site.data.keyword.Bluemix_notm}} com o comando `bx login` para gerar um token de acesso e autenticar sua sessão.

Para descobrir sobre como usar a CLI do {{site.data.keyword.registrylong_notm}}, veja [Introdução ao {{site.data.keyword.registrylong_notm}}](index.html).

**Nota**: não coloque informações pessoais em imagens de contêiner, nomes de namespace, campos de descrição (por exemplo, em tokens de registro) ou em quaisquer dados de configuração de imagem (por exemplo, nomes de imagem ou rótulos de imagem).


<table summary="Manage {}">
<caption>Tabela 1. Comandos para gerenciar o {{site.data.keyword.registrylong_notm}}
</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar o registro</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr build](#bx_cr_build)</td>
 <td>[bx cr info](#bx_cr_info)</td>
 <td>[bx cr image-inspect](#bx_cr_image_inspect)</td>
 <td>[bx cr image-list (imagens bx cr)](#bx_cr_image_list)</td>
 </tr>
 <tr>
 <td>[bx cr image-rm](#bx_cr_image_rm)</td>
 <td>[bx cr login](#bx_cr_login)</td>
 <td>[bx cr namespace-add](#bx_cr_namespace_add)</td>
 <td>[bx cr namespace-list (namespaces bx cr)](#bx_cr_namespace_list)</td>
 <td>[bx cr namespace-rm](#bx_cr_namespace_rm)</td>
 </tr>
 <tr>
 <td>[Cr bx plano](#bx_cr_plan)</td>
 <td>[bx cr plan-upgrade](#bx_cr_plan_upgrade)</td>
 <td>[Bx cr purê-archive-load](#bx_cr_ppa_archive_load)</td>
 <td>[Cota cr bx](#bx_cr_quota)</td>
 <td>[bx cr quota-set](#bx_cr_quota_set)</td>
 </tr>
 <tr>
 <td>[bx cr region](#bx_cr_region)</td>
 <td>[bx cr region-set](#bx_cr_region_set)</td>
 <td>[bx cr token-add](#bx_cr_token_add)</td>
 <td>[bx cr token-get](#bx_cr_token_get)</td>
 <td>[bx cr token-list (tokens bx cr)](#bx_cr_token_list)</td>
 </tr><tr>
 <td>[bx cr token-rm](#bx_cr_token_rm)</td>
 <td>[bx cr vulnerabilidade de avaliação (que va bx)](#bx_cr_va)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

Retorna os detalhes sobre o terminal de API de registro com relação ao qual os comandos são executados.

```
bx cr api
```
{: codeblock}


## Bx cr build
{: #bx_cr_build}

Constrói uma imagem do Docker no {{site.data.keyword.registrylong_notm}}.

```
bx cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg KEY=VALUE ...] [--file FILE | -f FILE] --tag TAG DIRECTORY
```
{: codeblock}

**Parâmetros**
<dl>
<dt>DIRECTORY</dt>
<dd>O local de seu contexto de compilação, que contém o Dockerfile e os arquivos de pré-requisito.</dd>
<dt>-- no-cache</dt>
<dd>(Opcional) Se especificado, camadas de imagem em cache de construções anteriores não serão usadas nesta compilação.</dd>
<dt>-- pull</dt>
<dd>(Opcional) Se especificado, as imagens base são puxadas mesmo se uma imagem com uma tag de correspondência já existe no host de construção.</dd>
<dt>-- quiet, -q</dt>
<dd>(Opcional) Se especificado, a saída de construção é suprimida, a menos que ocorra um erro.</dd>
<dt> -- build-arg KEY=VALUE</dt>
<dd>(Opcional) Especifique um argumento de construção adicional no formato 'KEY=VALUE'. Múltiplos argumentos de compilação podem ser especificados, incluindo este parâmetro, múltiplas vezes. O valor de cada argumento de construção está disponível como uma variável de ambiente quando você especifica uma linha ARG que corresponde à chave em seu Dockerfile.</dd>
<dt>-- file FILE, -f FILE</dt>
<dd>(Opcional) Se você usar os mesmos arquivos para múltiplas construções, será possível escolher um caminho para um Dockerfile diferente. Especifique o local do Dockerfile relativo ao contexto de compilação. Se não especificado, o padrão será `PATH/Dockerfile`, em que PATH é a raiz do contexto de compilação.</dd>
<dt>-- tag TAG, -t TAG</dt>
<dd>O nome completo da imagem que você deseja construir, que inclui a URL do registro e o namespace.</dd>
</dl>


## bx cr info
{: #bx_cr_info}

Exibe o nome e a conta do registro ao qual você está conectado.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
{: #bx_cr_image_inspect}

Exibe detalhes sobre uma imagem específica.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>-- format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go.

Para obter mais informações, veja [Formatando e filtrando a saída da CLI para comandos do {{site.data.keyword.registrylong_notm}}](registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>IMAGE</dt>
<dd>O nome da imagem para o qual deseja obter um relatório. É possível inspecionar múltiplas imagens listando cada imagem no comando com um espaço entre cada nome.

<p>Para localizar os nomes das suas imagens, execute `bx cr image-list`. Combine o conteúdo das colunas Repositório e Tag para criar o nome da imagem no formato `repository:tag`. Se uma tag não for especificada no nome da imagem, a imagem identificada como `latest` será inspecionada. </p>

</dd>
</dl>


## Bx cr image-list (imagens bx cr)
{: #bx_cr_image_list}

Exibe todas as imagens em sua conta. {{site.data.keyword.Bluemix_notm}}

<p>**Nota:** o nome da imagem é a combinação do conteúdo das colunas Repositório e Tag no formato `repository:tag`. </p>

```
 bx cr image-list [--no-trunc] [--format FORMAT] [-q, --quiet] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>--no-trunc</dt>
<dd>(Opcional) Não truncar as compilações de imagem.</dd>
<dt>-- format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go.

Para obter mais informações, veja [Formatando e filtrando a saída da CLI para comandos do {{site.data.keyword.registrylong_notm}}](registry_cli_reference.html#registry_cli_listing).

</dd>
<dt>-q, -- quiet</dt>
<dd>(Opcional) Cada imagem é listada no formato: `repository:tag`</dd>
<dt>-- restrict RESTRICTION</dt>
<dd>(Opcional) Limite a saída para exibir somente imagens no namespace especificado ou namespace e repositório. </dd>
<dt>--include-ibm</dt>
<dd>(Opcional) Inclui imagens públicas fornecidas pelo {{site.data.keyword.IBM_notm}} na saída. Sem essa opção, somente imagens privadas serão listadas, por padrão.</dd>
</dl>



## Bx cr image-rm
{: #bx_cr_image_rm}

Exclui uma ou mais imagens especificadas do seu registro.

```
bx cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>IMAGE</dt>
<dd>O nome da imagem para o qual deseja obter um relatório. É possível excluir múltiplas imagens ao mesmo tempo listando cada imagem no comando com um espaço entre cada nome.

<p>Para localizar os nomes das suas imagens, execute `bx cr image-list`. Combine o conteúdo das colunas Repositório e Tag para criar o nome da imagem no formato `repository:tag`. Se uma tag não for especificada no nome da imagem, a imagem identificada como `latest` será excluída por padrão.</p>

</dd>
</dl>


## bx cr login
{: #bx_cr_login}

Esse comando executa o comando `docker login` no registro. O comando `docker login` é necessário para poder executar os comandos `docker push` ou `docker pull` para o registro. Esse comando não é necessário para executar outros comandos `bx cr`. Se o Docker não estiver instalado, esse comando retornará uma mensagem de erro.

```
bx cr login
```
{: codeblock}


## Bx cr namespace-add
{: #bx_cr_namespace_add}

Inclui um namespace em sua conta. {{site.data.keyword.Bluemix_notm}}

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parâmetros**
<dl>
<dt>NAMESPACE</dt>
<dd>O namespace que deseja incluir. O namespace deve ser exclusivo em todas as contas do {{site.data.keyword.Bluemix_notm}} na mesma região.
  
<p>  
<strong>Nota</strong>: não coloque informações pessoais nos nomes do namespace.
</p>
  
</dd>
</dl>


## Bx cr namespace-list (namespaces bx cr)
{: #bx_cr_namespace_list}

Exibe todos os namespaces pertencentes à sua conta do {{site.data.keyword.Bluemix_notm}}.

```
bx cr namespace-list
```
{: codeblock}


## Bx cr namespace-rm
{: #bx_cr_namespace_rm}

Remove um namespace de sua conta do {{site.data.keyword.Bluemix_notm}}. As imagens nesse namespace são excluídas quando o namespace é removido.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parâmetros**
<dl>
<dt>NAMESPACE</dt>
<dd>O namespace que deseja remover.</dd>
</dl>


## Cr bx plano
{: #bx_cr_plan}

Exibe seu plano de precificação.

```
Cr bx plano
```
{: codeblock}


## Bx cr plan-upgrade
{: #bx_cr_plan_upgrade}

Upgrades para você o plano padrão.

Para obter informações sobre planos, veja [Planos de registro](registry_overview.html#registry_plans).

```
bx cr plan-upgrade [PLAN]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>PLANO</dt>
<dd>O nome do plano de precificação para o qual você deseja fazer upgrade. Se PLAN não for especificado, o padrão será `standard`.</dd>
</dl>


## Bx cr purê-archive-load
{: #bx_cr_ppa_archive_load}

Importa software IBM que é transferido por download do [IBM Passport Advantage ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www-01.ibm.com/software/passportadvantage/pao_customer.html) e é compactado para uso com o Helm para o namespace de registro privado.

As imagens de contêiner são enviadas por push para o namespace privado do {{site.data.keyword.registryshort_notm}}. Os gráficos de Helm são gravados em um diretório `ppa-import` criado no diretório em que o comando é executado. Opcionalmente, é possível usar o [Projeto de software livre Chart Museum ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) para hospedar gráficos de Helm.

**Exemplo de comando**:
```
bx cr ppa-archive-load --archive FILE --namespace NAMESPACE
```
{: codeblock}

**Parâmetros**:
<dl>
  <dt>-- archive FILE</dt>
  <dd>O caminho para o arquivo compactado que é transferido por download por meio do IBM Passport Advantage.</dd>
  <dt>-- namespace NAMESPACE</dt>
  <dd>Um dos seus namespaces. Imagens do contêiner do arquivo compactado são enviadas por push para esse namespace. Para listar os namespaces, execute `bx cr namespace-list`.</dd>
  <dt>--chartmuseum-uri URI</dt>
  <dd>(Opcional) Seu identificador de recurso exclusivo do [Chart Museum ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>-- USUÁRIO chartmuseum Usuário</dt>
  <dd>(Opcional) Seu nome de usuário do [Chart Museum ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>-- chartmuseum-password PASSWORD</dt>
  <dd>(Opcional) Sua senha do [Chart Museum ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
</dl>


## Cota cr bx
{: #bx_cr_quota}

Exibe suas cotas atuais para tráfego e armazenamento e informações de uso com relação a essas cotas.

```
Cota cr bx
```
{: codeblock}


## Bx conjunto de cota
{: #bx_cr_quota_set}

Modifique a cota especificada.

```
bx cr quota-set [--traffic TRAFFIC] [--storage STORAGE]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>-- traffic TRAFFIC</dt>
<dd>(Opcional) Muda sua cota de tráfego para o valor especificado em megabytes. A operação falhará se você não estiver autorizado a configurar o tráfego ou se configurar um valor que exceda o seu plano de precificação atual.</dd>
<dt>-- storage STORAGE</dt>
<dd>(Opcional) Muda sua cota de armazenamento para o valor especificado em megabytes. A operação falhará se você não estiver autorizado a configurar cotas de armazenamento ou se configurar um valor que exceda o seu plano de precificação atual.</dd>
</dl>


## bx cr region
{: #bx_cr_region}

Exibe a região de destino e o registro.

```
bx cr region
```
{: codeblock}

Para obter mais informações, consulte [Regiões](registry_overview.html#registry_regions).


## Bx cr region-set
{: #bx_cr_region_set}

Configure uma região de destino para os comandos do {{site.data.keyword.registrylong_notm}}. Para listar as regiões disponíveis, execute o comando sem parâmetros.

```
bx cr region-set [REGION]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>REGION</dt>
<dd>(Opcional) O nome de sua região de destino, por exemplo, `us-south`.

Para obter mais informações, consulte [Regiões](registry_overview.html#registry_regions).

</dd>
</dl>


## Bx cr token-add
{: #bx_cr_token_add}

Inclui um token que pode ser usado para controlar o acesso a um registro.

```
bx cr token-add [--description DESCRIPTION] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**Parâmetros**
<dl>
<dt>--description DESCRIPTION</dt>
<dd>(Opcional) Especifica o valor como uma descrição para o token, que é exibida quando você executa `bx cr token-list`. Se o seu token for criado automaticamente pelo {{site.data.keyword.containerlong_notm}}, a descrição será configurada para o nome do cluster do Kubernetes. Nesse caso, o token é removido automaticamente quando o cluster é removido.
  
<p> 
  <strong>Nota</strong>: não coloque informações pessoais na descrição do token.
</p>

  </dd>
<dt>-q, -- quiet</dt>
<dd>(Opcional) Exibe o token somente, sem nenhum texto circundante.</dd>
<dt>--non-expiring</dt>
<dd>(Opcional) Cria um token com acesso que não expira. Sem esse conjunto de parâmetros, o acesso por meio de um token expirará após 24 horas, por padrão.</dd>
<dt>--readwrite</dt>
<dd>(Opcional) Cria um token que concede acesso de leitura e gravação. Sem essa opção, o acesso será somente leitura, por padrão.</dd>
</dl>


## Bx cr token-get
{: #bx_cr_token_get}

Recuperar o token especificado do registro.

```
bx cr token-get TOKEN
```

{: codeblock}

**Parâmetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) O identificador exclusivo do token que você deseja recuperar.</dd>
</dl>


## Bx cr token-list (tokens bx cr)
{: #bx_cr_token_list}

Exibe todos os tokens que existem para sua conta do {{site.data.keyword.Bluemix_notm}}.

```
bx cr token-list --format FORMAT
```
{: codeblock}

**Parâmetros**
<dl>
<dt>-- format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go.

Para obter mais informações, veja [Formatando e filtrando a saída da CLI para comandos do {{site.data.keyword.registrylong_notm}}](registry_cli_reference.html#registry_cli_listing).

</dd>
</dl>


## Bx cr token-rm
{: #bx_cr_token_rm}

Remova um ou mais tokens especificados.

```
bx cr token-rm TOKEN [TOKEN...]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) TOKEN pode ser o próprio token ou o identificador exclusivo do token, conforme mostrado em `bx cr token-list`. É possível especificar múltiplos tokens e devem ser separados por um espaço.</dd>
</dl>


## Bx cr vulnerabilidade de avaliação (que va bx)
{: #bx_cr_va}

Visualize um relatório de avaliação de vulnerabilidade para suas imagens.

```
bx cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>IMAGE</dt>
<dd>O nome da imagem para o qual deseja obter um relatório. O relatório indica se a imagem em quaisquer vulnerabilidades de pacote conhecidas. É possível solicitar relatórios para múltiplas imagens ao mesmo tempo listando cada imagem no comando com um espaço entre cada nome.

<p>Para localizar os nomes das suas imagens, execute `bx cr image-list`. Combine o conteúdo das colunas Repositório e Tag para criar o nome da imagem no formato `repository:tag`. Se uma tag não for especificada no nome da imagem, o relatório avaliará a imagem identificada como `latest`. </p>

<p>Os seguintes sistemas operacionais são suportados:

<ul>

<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>

</p>

Para obter mais informações, consulte [Gerenciando a segurança de imagens com o Vulnerability Advisor](../va/va_index.html).

</dd>
<dt>-- output FORMAT, -o FORMAT</dt>
<dd>(Opcional) A saída de comando é retornada no formato escolhido. O formato padrão é `text`. Os seguintes formatos são suportados:

<ul>

<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
<dt>-- vulnerabilities, -v</dt>
<dd>(Opcional) A saída de comando é restrita para mostrar somente as vulnerabilidades.</dd>
<dt>-- configuration-issues, -c</dt>
<dd>(Opcional) A saída de comando é restrita para mostrar somente problemas de configuração.</dd>
<dt>--extended, -e </dt>
<dd>(Opcional) A saída de comando mostra informações adicionais sobre correções para pacotes vulneráveis.</dd>

</dl>
