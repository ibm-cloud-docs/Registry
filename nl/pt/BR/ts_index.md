---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

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

Aqui estão as respostas para perguntas comuns sobre resolução de problemas no uso do {{site.data.keyword.registrylong}}.
{:shortdesc}


## Obtendo ajuda e suporte para o {{site.data.keyword.registrylong_notm}}
{: #gettinghelp}

Se tiver problemas ou perguntas quando estiver usando o {{site.data.keyword.registrylong_notm}}, será possível obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte da {{site.data.keyword.IBM_notm}}.

Quando você estiver usando os fóruns para fazer uma pergunta, marque a sua pergunta para que ela seja vista pela equipe de desenvolvimento do {{site.data.keyword.registrylong_notm}}.

-   Se você tiver questões técnicas sobre como desenvolver ou implementar um app com o {{site.data.keyword.registrylong_notm}}, poste sua pergunta no [Stack Overflow](http://stackoverflow.com/search?q=+ibm-bluemix) e marque a sua pergunta com `ibm-bluemix` e `registro de contêiner`.
-   Para perguntas sobre o serviço e instruções de introdução, use o fórum do [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix). Inclua as tags `bluemix` e `registro de contêiner`.

Consulte [Usando o centro de suporte](/docs/get-support/howtogetsupport.html#using-avatar) para obter mais detalhes sobre o uso dos fóruns.

Para obter informações sobre como abrir um chamado de suporte da {{site.data.keyword.IBM_notm}} ou sobre os níveis de suporte e severidades dos chamados, consulte [Abrindo um chamado de suporte](/docs/get-support/howtogetsupport.html#open-ticket).

## O login no {{site.data.keyword.registrylong_notm}} falha
{: #ts_login}

Não é possível efetuar login no {{site.data.keyword.registrylong_notm}}.

{: tsSymptoms}
O comando  ` ibmcloud cr login `  falha.

{: tsCauses}
-   O plug-in de registro de contêiner está desatualizado e precisa ser atualizado.
-   O Docker não está instalado no computador local ou não está em execução.
-   Suas credenciais de login do {{site.data.keyword.Bluemix_notm}} expiraram.

{: tsResolve}
É possível corrigir esse problema das maneiras a seguir:

-   Para fazer upgrade para a versão mais recente do plug-in do contêiner de registro, veja [Atualizando o plug-in de registro de contêiner](registry_setup_cli_namespace.html#registry_cli_update).
-   Assegure-se de que o Docker esteja instalado no computador. Se ele já estiver instalado, reinicie o daemon do Docker.
-   Execute novamente o comando `ibmcloud login` para atualizar suas credenciais de login do {{site.data.keyword.Bluemix_notm}}.
  
## A execução de qualquer comando do {{site.data.keyword.registrylong_notm}} falha com `FAILED You are not logged in to IBM Cloud. ` 
{: #ts_login_cloud}

Não é possível executar comandos no {{site.data.keyword.registrylong_notm}}, mesmo que você esteja conectado ao {{site.data.keyword.Bluemix_notm}}.

{: tsSymptoms}
Todos os comandos  ` ibmcloud cr `  falham.

{: tsCauses}
-   O plug-in de registro de contêiner está desatualizado e precisa ser atualizado.

{: tsResolve}
É possível corrigir esse problema da maneira a seguir:

-   Para fazer upgrade para a versão mais recente do plug-in do contêiner de registro, veja [Atualizando o plug-in de registro de contêiner](registry_setup_cli_namespace.html#registry_cli_update).



## Os comandos do {{site.data.keyword.registrylong_notm}} falham com `'cr' is not a registered command. Consulte 'ibmcloud help'. `
{: #ts_login_error}

Não é possível executar um comando `ibmcloud cr` porque `cr` não é um comando `ibmcloud` registrado.

{: tsSymptoms}
Você vê uma mensagem de erro semelhante a uma das mensagens de erro a seguir:

```
ibmcloud cr login
'cr' is not a registered command. Veja 'ibmcloud help'.
```
{: pre}

```
ibmcloud cr namespace
'cr' is not a registered command. Veja 'ibmcloud help'.
```
{: pre}

{: tsCauses}
-   O plug-in de registro de contêiner não está instalado.


{: tsResolve}
É possível corrigir esse problema da maneira a seguir:

-   Instale o plug-in de registro de contêiner, consulte [Instalando a CLI do {{site.data.keyword.registryshort_notm}} (plug-in de registro de contêiner)](registry_setup_cli_namespace.html#registry_cli_install).


## Falha na configuração de um namespace
{: #ts_problem}

{: tsSymptoms}
Ao executar `ibmcloud cr namespace-add`, não é possível configurar seu valor inserido como o namespace.

{: tsCauses}
-   Você inseriu um valor de namespace que já está sendo usado por outra organização do {{site.data.keyword.Bluemix_notm}}.
-   Um namespace foi excluído recentemente e você está reutilizando o seu nome. Se o namespace que foi excluído continha muitos recursos, a exclusão ainda não poderá ser totalmente processada pelo {{site.data.keyword.registrylong_notm}}.
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
Ao executar comandos para enviar por push ou puxar imagens do Docker, você receberá uma mensagem de erro. A mensagem de erro varia dependendo da causa raiz. Potenciais mensagens de erro podem ser:

```
Você excedeu a sua cota de armazenamento. Exclua uma ou mais imagens ou revise a sua
cota de armazenamento e o plano de precificação
```
{: screen}

```
Você excedeu a sua cota de tráfego extraído para o mês atual. 
Revise a sua cota de tráfego extraído e o plano de precificação
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

-   [Assegure-se de que o Docker esteja instalado no computador](index.html#registry_cli_install).
-   Verifique seu caminho de instalação do Docker.
-   Efetue login no {{site.data.keyword.Bluemix_notm}} executando `ibmcloud login`. Em seguida, efetue login na CLI do {{site.data.keyword.registrylong_notm}} executando `ibmcloud cr login`.
-   [Revise os limites de cota e uso para armazenar e puxar imagens do Docker no {{site.data.keyword.registrylong_notm}}](registry_quota.html#registry_quota_get).


## Não é possível puxar a imagem mais recente usando a tag `latest`
{: #ts_docker_latest}

{: tsSymptoms}
Você está tentando executar o comando `docker pull`, mas ele retornou uma versão da imagem que não é a versão mais recente construída.

{: tsCauses}
A tag `latest` é aplicada por padrão para referenciar uma imagem quando você executa comandos do Docker sem especificar o valor de tag. A tag `latest` é aplicada ao comando `docker build` ou `docker tag` mais recente que foi executado sem um valor de tag explicitamente configurado. Portanto, é possível executar comandos `docker` fora de ordem ou configurar explicitamente tags em algumas imagens e a tag `latest` para consultar uma construção que não é a mais recente.

{: tsResolve}
Geralmente, é melhor definir explicitamente uma tag sequencial diferente para suas imagens toda vez e não depender da tag `latest`.


## Não é possível incluir outras imagens da IBM no registro
{: #ts_ppa}


{: tsSymptoms}
Ao tentar importar conteúdo usado em outros produtos IBM, como o {{site.data.keyword.Bluemix_notm}} Private, você não é capaz de armazenar suas imagens e outro software licenciado do [IBM Passport Advantage ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/software/passportadvantage/index.html) no registro.

{: tsCauses}
Os pacotes de software, como imagens e gráficos de Helm do IBM Passport Advantage, devem ser importados para o registro com o comando `ibmcloud cr ppa-archive-load`.

{: tsResolve}
Antes de iniciar:
* Efetue login no {{site.data.keyword.Bluemix_notm}} executando `ibmcloud login [--sso]`.
* Efetue login no {{site.data.keyword.registrylong_notm}} executando `ibmcloud cr login`.
* [Direcione a CLI do `kubectl`](/docs/containers/cs_cli_install.html#cs_cli_configure) para o cluster.
* Se ainda não tiver configurado o Helm no cluster, [configure o Helm em seu cluster agora](/docs/containers/cs_integrations.html#helm).
* Se desejar compartilhar os gráficos em sua organização, será possível instalar o [Projeto de software livre Chart Museum ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum). Para obter instruções, consulte esta [orientação do developerWorks ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/deploy-chartmuseum-into-ibm-cloud-kubernetes-service-iks/).


### Importando produtos IBM Passport Advantage para uso no {{site.data.keyword.Bluemix_notm}}

1.  Obtenha o arquivo compactado que você deseja importar do [IBM Passport Advantage![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/software/passportadvantage/index.html).

2.  Tenha como destino a região que você deseja usar. Se não souber o nome da região, execute o comando sem a região e, em seguida, escolha uma região.

    ```
    ibmcloud cr region-set <region>
    ```
    {: pre}

3.  Importe o arquivo archive compactado. Especifique o caminho para o arquivo compactado e o namespace do registro para o qual você deseja enviar as imagens por push.

    ```
    ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
    ```
    {: pre}

    Esse comando expande o arquivo compactado, carrega as imagens contidas para o cliente local do Docker e, em seguida, envia as imagens por push para o namespace em seu registro.
    
    Se desejar fazer upload de gráficos de Helm do archive do IBM Passport Advantage para um museu de gráficos, inclua as opções a seguir no comando: `ibmcloud cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **Exemplo de saída**
    
    ```
    user:~ user$ ibmcloud cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extraindo gráfico 'charts/ibm-integration-bus-prod-1.0.0.tgz' para '/Users/user/Downloads/ppa-import/charts'.

    Ok
    ```
    {: screen}

4.  Se os arquivos compactados contiverem gráficos de Helm, esses gráficos serão colocados em um diretório de archive chamado `ppa-import`, criado no diretório atualmente em funcionamento. Abra o diretório para obter o nome do gráfico de Helm, `<helm_chart>`e, em seguida, inspecione seus valores.

    ```
    helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    Se você tiver transferido gráficos por upload para um museu de gráficos na etapa anterior, será possível usar `helm inspect` para inspecionar o gráfico no museu de gráficos.
    {: tip}

5.  Configure o gráfico Helm,`<helm_chart>`, de acordo com os valores gerados pelo comando `helm inspect values`.

6.  Implemente o gráfico Helm, `<helm_chart>`, usando o `comando install` comando. Será possível substituir valores no gráfico, conforme necessário, usando a opção `--set`.

    ```
    helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## O acesso ao registro com um firewall customizado falha
{: #ts_firewall}

{: tsSymptoms}
Você configura um firewall adicional em seu ambiente de desenvolvimento com configurações customizadas para o tráfego de rede de entrada e de saída. Quando você tenta acessar o {{site.data.keyword.registrylong_notm}}, a conexão falha.

{: tsCauses}
Seu firewall customizado requer que determinados grupos de rede sejam abertos para o tráfego de rede de entrada e de saída para permitir a comunicação para e do registro.

{: tsResolve}
Abra os grupos de rede a seguir em seu firewall customizado.

1.  Anote o endereço IP público do computador que deseja usar para se conectar ao {{site.data.keyword.registrylong_notm}}. Se você estiver usando o Kubernetes, use o endereço IP público do seu nó do trabalhador. Recupere o endereço IP público de seu nó do trabalhador executando `ibmcloud ks workers <cluster_name_or_id>`, em que *&lt;cluster_name_or_id&gt;* é o nome ou ID de seu cluster.
2.  No firewall do computador, permita a entrada e a saída das conexões a seguir:
    -   Para a conectividade INBOUND para o computador, permita o tráfego de rede recebido dos seguintes grupos de rede de origem para o endereço IP público de destino do computador.

        `registry.bluemix.net`:

        ```
        169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

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

    -   Para a conectividade OUTBOUND do computador, use os mesmos grupos de rede e permita o tráfego de rede de saída do endereço IP público de origem do computador para esses grupos de rede.


## Recuperando chaves perdidas ou comprometidas
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
Ao usar o [conteúdo confiável](registry_trusted_content.html), não será mais possível gerenciar imagens confiáveis porque suas chaves de assinatura estão perdidas ou comprometidas.

{: tsCauses}
Seu repositório ou chave raiz está perdida ou comprometida.

{: tsResolve}
Suas opções para recuperar chaves perdidas ou afetadas dependem do tipo de chave: repositório ou raiz:

*  Para [chaves de repositório](#trustedcontent_lostrepokey), é possível gerar um novo conjunto de chaves de assinatura para o repositório.
*  Para [chaves raiz](#trustedcontent_lostrootkey), é possível solicitar que o repositório seja excluído e criar um novo repositório.


### Chaves de Repositório
{: #trustedcontent_lostrepokey}

Se a chave de repositório estiver perdida ou comprometida, gere um novo conjunto de chaves de assinatura para seu repositório.
{:shortdesc}

A única função de assinatura que você pode girar é `targets`, que é o administrador de repositório. Se outras funções forem afetadas, gere novas chaves para essas funções, remova as antigas e inclua as novas como assinantes.
{:tip}

Antes de iniciar, recupere a passphrase da chave raiz criada quando você [enviou uma imagem assinada por push](registry_trusted_content.html#trustedcontent_push) pela primeira vez.

1.  Instale a versão da CLI do [projeto Notary ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli).

2.  [Configurar o ambiente de conteúdo confiável](registry_trusted_content.html#trustedcontent_setup).

3.  Observe a URL do comando de exportação na etapa anterior. Por exemplo, `https://registry.ng.bluemix.net:4443`.

4.  Gere um token de registro.

    ```
    ibmcloud cr token-add --readwrite
    ```
    {: pre}

5.	Gire as chaves para que o conteúdo assinado com elas não seja mais confiável. Substitua _&lt;URL&gt;_ pela URL do comando de exportação observado na Etapa 2 e _&lt;image&gt;_ pela imagem cuja chave do repositório foi afetada.

    ```
    notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	Se solicitado, insira a passphrase da chave raiz. Em seguida, insira uma nova passphrase de chave raiz para a nova chave de repositório, quando solicitada.

7.	[Envie uma imagem assinada por push](registry_trusted_content.html#trustedcontent_push) que use as novas chaves de assinatura.


### As chaves raiz
{: #trustedcontent_lostrootkey}

Se a sua chave raiz estiver perdida ou comprometida, não será possível atualizar nenhum repositório de conteúdo confiável que tenha usado essa chave raiz.
{:shortdesc}

É possível [excluir os namespaces](registry_setup_cli_namespace.html#registry_remove) que possuem repositórios que usam a chave raiz afetada, que exclui suas imagens e dados de confiança.

Se o namespace contiver repositórios com chaves raízes não afetadas, como um namespace para imagens de produção, talvez você queira excluir apenas os dados de confiança associados à chave raiz afetada. Abra um chamado de suporte.

1.  [Entre em contato com o {{site.data.keyword.Bluemix_notm}} Suporte](/docs/get-support/howtogetsupport.html#getting-customer-support). Inclua uma breve descrição de seu problema, o ID da conta e uma lista dos namespaces que contêm os repositórios de imagem com chaves raízes afetadas.

2.  Depois que o {{site.data.keyword.Bluemix_notm}} tratar do problema, exclua o repositório do Docker Content Trust no computador local.

    * Diretório Linux e Mac: `~/.docker/trust/private` e `~/.docker/trust/tuf`

    * Diretório Windows: `%HOMEPATH%\ .docker \trust\private` e `%HOMEPATH%\ .docker \trust \tuf`

    Como a chave raiz é afetada, essa etapa excluirá todas as chaves de assinatura, incluindo para outros servidores de confiança.
    {:tip}

3.  Se você usar o [{{site.data.keyword.Bluemix_notm}} Image Enforcement](registry_security_enforce.html) no cluster do {{site.data.keyword.containershort_notm}}, reinicie cada pod de cumprimento de imagem. Para acionar o Kubernetes para executar um reinício de rolagem dos pods automaticamente, é possível mudar alguns metadados no pod. Por exemplo, [tenha como destino a CLI do Kubernetes para o seu cluster](/docs/containers/cs_cli_install.html#cs_cli_configure) e modifique a implementação.

    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  Gerar repositórios de conteúdo confiável.

    *  Se desejar criar um novo conteúdo confiável, [envie por push novas imagens assinadas](registry_trusted_content.html#trustedcontent_push).

    *  Se você não desejar mudar o conteúdo confiável anterior, inclua uma assinatura nas imagens mais recentes no registro.

       ```
       docker trust sign <image>:<tag>
       ```
       {: pre}
       

## A instalação do Container Image Security Enforcement falha com `helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists`
{: #ts_install_cise_fail}

{: tsSymptoms}
A instalação do Container Image Security Enforcement falhou e você recebeu a mensagem a seguir:

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
A instalação anterior falhou e a desinstalação subsequente não removeu todas as tarefas do Kubernetes que estão associadas à instalação.

{: tsResolve}
Remova as tarefas restantes do Kubernetes executando o comando a seguir:

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}


## Os pods não são reiniciados após a indisponibilidade de todos os trabalhadores
{: #ts_pods}


{: tsSymptoms}
Os pods não são reiniciados após a indisponibilidade de todos os trabalhadores do cluster. O Container Image Security Enforcement é implementado. Os trabalhadores do cluster estão sendo mostrados como funcionais, mas nada está planejado.

{: tsCauses}
Por padrão, o Container Image Security Enforcement inclui um webhook de admissão de falha fechada. Se todos os pods do Container Image Security Enforcement estiverem indisponíveis, os pods não estarão disponíveis para aprovar as suas próprias recuperações.

{: tsResolve}
Para recuperar o cluster quando ele estiver nesse estado, será necessário mudar a configuração do webhook para que ele falhe aberto em vez de fechado. 

Deve-se ter privilégios suficientes de controle de acesso baseado em função (RBAC) para usar os verbos a seguir:
*  `GET`
*  `PATCH`

nesses recursos:
*  `admissionregistration.k8s.io/v1beta1/MutatingWebhookConfiguration`
*  `admissionregistration.k8s.io/v1beta1/ValidatingWebhookConfiguration` 

Para obter mais informações sobre o RBAC, consulte [Autorizando os usuários com as funções RBAC do Kubernetes customizadas](/docs/containers/cs_users.html#rbac) e [Kubernetes: usando a autorização RBAC
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

Conclua as etapas a seguir para mudar a configuração do webhook para que ele falhe aberto em vez de fechado e, em seguida, quando pelo menos um pod do Container Image Security Enforcement estiver em execução, restaure a configuração do webhook para que ele falhe fechado:

1.  Atualize `MutatingWebhookConfiguration` executando o comando a seguir:

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Mude `failurePolicy` para `Ignore`, salve e feche.

2.  Atualize `ValidatingWebhookConfiguration` executando o comando a seguir:

    ````
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Mude `failurePolicy` para `Ignore`, salve e feche.

3.  Aguarde até que alguns pods do Container Image Security Enforcement sejam iniciados. É possível verificar se os pods foram iniciados executando o comando a seguir até que a coluna **STATUS** para pelo menos um pod exiba `Running`:

    ```
    kubectl get po -n ibm-system -l app=ibmcloud-image-enforcement
    ```
    {: pre}

4.  Quando pelo menos um pod do Container Image Security Enforcement estiver em execução, atualize `MutatingWebhookConfiguration` executando o comando a seguir:

    ```
    kubectl edit MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Mude `failurePolicy` para `Fail`, salve e feche.

5.  Atualize `ValidatingWebhookConfiguration` executando o comando a seguir:

    ```
    kubectl edit ValidatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Mude `failurePolicy` para `Fail`, salve e feche.
