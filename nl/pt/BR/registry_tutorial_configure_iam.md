---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-19"

keywords: IBM Cloud Container Registry, user access, tutorial, access control, 

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

# Tutorial: concedendo acesso a recursos do {{site.data.keyword.registrylong_notm}}
{: #iam_access}

Use este tutorial para descobrir como conceder acesso a seus recursos configurando o {{site.data.keyword.iamlong}} (IAM) para {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

Este tutorial leva aproximadamente 45 minutos.

**Antes de iniciar**

- Conclua as instruções em [Introdução ao {{site.data.keyword.registrylong_notm}} ](/docs/services/Registry?topic=registry-getting-started#getting-started).

- Assegure-se de que você tenha a versão mais recente do plug-in da CLI `container-registry` para a CLI do {{site.data.keyword.cloud_notm}}, consulte [Atualizando o plug-in da CLI `container-registry`](/docs/services/Registry?topic=registry-registry_setup_cli_namespace#registry_cli_update).

- Deve-se ter acesso a duas contas do [{{site.data.keyword.cloud_notm}}
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login)
que podem ser usadas para este tutorial: uma para o Usuário A e outra para o Usuário B. Cada uma delas deve usar um
endereço de e-mail exclusivo. Você trabalha em sua própria conta, Usuário A, e convida outro usuário, Usuário B, para usar sua conta. É possível optar por criar uma segunda conta {{site.data.keyword.cloud_notm}} ou trabalhar com um colega que tenha uma conta {{site.data.keyword.cloud_notm}}.

- Se você começou a usar o {{site.data.keyword.registrylong_notm}} em sua conta antes de 4 de outubro de 2018, deverá ativar o cumprimento de política do IAM executando o comando `ibmcloud cr iam-policies-enable`. Se você convidou outros usuários que usam seus namespaces do {{site.data.keyword.registrylong_notm}} em sua conta do IBM Cloud, use uma conta diferente como Usuário A para evitar a interrupção de seu acesso.

## Etapa 1: autorizar um usuário a configurar o registro
{: #configure_registry}

Nesta seção, você inclui um segundo usuário em sua conta e concede a eles a capacidade de configurar o {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Incluir Usuário B na conta do Usuário A:

    1. Efetue login na conta do Usuário A, executando o comando a seguir:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Convide o Usuário B para acessar a conta do Usuário A executando o comando a seguir, em que _`<user.b@example.com>`_ é o endereço de e-mail do Usuário B:

        ```
        ibmcloud account user-invite <user.b@example.com>
        ```
        {: pre}

    3. Obtenha o ID da conta do Usuário A executando o comando a seguir:

        ```
        ibmcloud target
        ```
        {: pre}

        Anote o ID da conta que está entre parênteses () na linha Conta.

2. Prove que o Usuário B pode ter como destino a conta do Usuário A, mas ainda não pode fazer nada com o {{site.data.keyword.registrylong_notm}}:

    1. Efetue login como o Usuário B e destine a conta do Usuário A executando o comando a seguir, em que _`<YourAccountID>`_ é o ID da conta do Usuário A:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Tente editar sua cota de registro para 4 GB de tráfego, executando o comando a seguir:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        O comando falha porque o Usuário B não tem o acesso correto.

3. Conceda ao Usuário B a função de Gerenciador para que o Usuário B possa configurar o {{site.data.keyword.registrylong_notm}}:

    1. Efetue login novamente em sua conta como você mesmo, Usuário A, executando o comando a seguir:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Crie uma política que conceda a função de Gerenciador ao Usuário B executando o comando a seguir:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --roles Manager
        ```
        {: pre}

4. Prove que o Usuário B pode mudar agora as cotas na conta do Usuário A:

    1. Efetue login como Usuário B, direcionando a conta do Usuário A, executando o comando a seguir:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Tente editar sua cota de registro para 4 GB de tráfego, executando o comando a seguir:

        ```
        ibmcloud cr quota-set --traffic=4000
        ```
        {: pre}

        Funciona porque o Usuário B tem o tipo correto de acesso.

    3. Agora, mude a cota de volta ao executar o comando a seguir:
  
        ```
        ibmcloud cr quota-set --traffic=5120
        ```
        {: pre}

5. Limpeza:

    1. Efetue login novamente em sua conta como você mesmo, Usuário A, executando o comando a seguir:
  
        ```
        ibmcloud login
        ```
        {: pre}
  
    2. Liste as políticas para o Usuário B, localize a política que você acabou de criar executando o comando a seguir e observe o ID:
  
        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}
  
    3. Exclua a política executando o comando a seguir, em que _`<Policy_ID>`_ é o seu ID de Política:
  
        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Etapa 2: autorizar um usuário a acessar namespaces específicos
{: #access_resources}

Nesta seção, você cria alguns namespaces com imagens de amostra e concede acesso a eles. Você cria políticas para conceder funções diferentes a cada namespace e mostra o efeito que isso tem.
{:shortdesc}

1. Crie três novos namespaces na conta do Usuário A. Esses namespaces devem ser exclusivos na região, portanto, escolha seus próprios nomes de namespace, mas este tutorial usa `namespace_a`, `namespace_b` e `namespace_c` como exemplos:

    1. Efetue login como Usuário A, executando o comando a seguir:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Crie `namespace_a` executando o comando a seguir:

        ```
        ibmcloud cr namespace-add namespace_a
        ```
        {: pre}

        O namespace deve ser exclusivo em todas as contas do {{site.data.keyword.cloud_notm}} na mesma região. Os namespaces devem ter de 4 a 30 caracteres e conter apenas letras minúsculas, números, hífens (-) e sublinhados (_). Os namespaces devem iniciar e terminar com uma letra ou número.
        {: tip}

    3. Crie `namespace_b` executando o comando a seguir:

        ```
        ibmcloud cr namespace-add namespace_b
        ```
        {: pre}
            
    4. Crie `namespace_c` executando o comando a seguir:

        ```
        ibmcloud cr namespace-add namespace_c
        ```
        {: pre}

2. Prove que o Usuário B não pode ver nada:

    1. Efetue login como Usuário B, direcionando a conta do Usuário A, executando o comando a seguir:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Tente listar imagens como Usuário B executando o comando a seguir:

        ```
        ibmcloud cr images
        ```
        {: pre}

        Ele retorna uma lista vazia porque o Usuário B não tem acesso a nenhum namespace.

3. Crie políticas para conceder ao Usuário B a capacidade de interagir com os namespaces executando o comando a seguir:

    1. Efetue login como uma conta do Usuário A executando o comando a seguir:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Verifique se pelo menos três namespaces estão listados executando o comando a seguir:

        ```
        ibmcloud cr namespaces
        ```
        {: pre}

        Os três namespaces que você criou neste tutorial (`namespace_a`, `namespace_b` e `namespace_c`) são exibidos. Se você não vir esses namespaces, volte e siga as instruções para criá-los novamente.

    3. Crie uma política que conceda a função de Leitor em `namespace_b` para o Usuário B, executando o comando a seguir, em que _`<Region>`_ é o nome de sua [região](/docs/services/Registry?topic=registry-registry_overview#registry_regions), por exemplo, `us-south`:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Reader
        ```
        {: pre}

    4. Crie uma segunda política que conceda as funções de Leitor e Gravador em `namespace_c` para o Usuário B executando o comando a seguir:

        ```
        ibmcloud iam user-policy-create <user.b@example.com> --service-name container-registry --region <Region> --resource-type namespace --resource namespace_c --roles Reader,Writer
        ```
        {: pre}

        Esse comando inclui duas funções no mesmo recurso na mesma política.
        {: tip}

4. Envie por push imagens no `namespace_a` e `namespace_b`:

    1. Faça pull da imagem `hello-world` executando o comando a seguir:

        ```
        docker pull hello-world
        ```
        {: pre}

    2. Identifique a imagem para `namespace_a` executando o comando a seguir:

        ```
        docker tag hello-world < Region> .icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Identifique a imagem para `namespace_b` executando o comando a seguir:

        ```
        docker tag hello-world < Region> .icr.io/namespace_b/hello-world
        ```
        {: pre}

    4. Efetue login no {{site.data.keyword.registrylong_notm}} executando o comando a seguir:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Envie por push a imagem para `namespace_a` ao executar o comando a seguir:

        ```
        docker push < Region> .icr.io/namespace_a/hello-world
        ```
        {: pre}

    6. Envie a imagem por push para `namespace_b` executando o comando a seguir:

        ```
        docker push < Region> .icr.io/namespace_b/hello-world
        ```
        {: pre}

5. Prove que o Usuário B pode interagir com `namespace_b` e `namespace_c`, mas não com `namespace_a`:

    1. Efetue login como Usuário B executando o comando a seguir:

        ```
        ibmcloud login -c <YourAccountID>
        ```
        {: pre}

    2. Mostre que o Usuário B pode ver `namespace_b` e `namespace_c`, mas não `namespace_a`, pois o Usuário B não tem acesso a `namespace_a`, executando o comando a seguir:

        ```
        ibmcloud cr namespaces
        ```
        {:pre}

    3. Liste suas imagens ao executar o comando a seguir:

        ```
        ibmcloud cr images
        ```
        {: pre}

        A imagem em `namespace_b` é mostrada na lista, mas a imagem em `namespace_a` não, porque o Usuário B não tem acesso a `namespace_a`.

    4. Efetue login no {{site.data.keyword.registrylong_notm}} executando o comando a seguir:

        ```
        ibmcloud cr login
        ```
        {: pre}

    5. Faça pull da imagem executando o comando a seguir:

        ```
        docker pull < Region> .icr.io/namespace_b/hello-world
        ```
        {: pre}

    6. Envie a imagem por push para `namespace_b` executando o comando a seguir:

        ```
        docker push < Region> .icr.io/namespace_b/hello-world
        ```
        {: pre}

        Esse comando falha porque o Usuário B não tem a função de Gravador em `namespace_b`.

    7. Identifique a imagem com `namespace_c` ao executar o comando a seguir:

        ```
        docker tag hello-world <Region>.icr.io/namespace_c/hello-world
        ```
        {: pre}

    8. Envie por push a imagem para `namespace_c` ao executar o comando a seguir:

        ```
        docker push < Region> .icr.io/namespace_c/hello-world
        ```
        {: pre}

        O comando funciona porque o Usuário B possui a função de Gravador em `namespace_c`.

    9. Faça pull de `namespace_c` executando o comando a seguir:

        ```
        docker pull < Region> .icr.io/namespace_c/hello-world
        ```
        {: pre}

        O comando funciona porque o Usuário B possui a função de Leitor em `namespace_c`.

6. Limpeza:

    1. Efetue login novamente na conta do Usuário A executando o comando a seguir:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Liste as políticas para o Usuário B executando o comando a seguir:

        ```
        ibmcloud iam user-policies <user.b@example.com>
        ```
        {: pre}

        Localize as políticas que você acabou de criar e anote os IDs de Política.

    3. Exclua as políticas que você acabou de criar, executando o comando a seguir, em que _`<Policy_ID>`_ é o ID da Política:

        ```
        ibmcloud iam user-policy-delete <user.b@example.com> <Policy_ID>
        ```
        {: pre}

## Etapa 3: Criar um ID de serviço e conceder acesso a um recurso
{: #service_id}

Nesta seção, você configura um ID de serviço e concede a ele acesso ao namespace do {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Configure um ID de serviço com acesso ao {{site.data.keyword.registrylong_notm}} e crie uma chave de API para ele:

    1. Efetue login na conta do Usuário A executando o comando a seguir:

        ```
        ibmcloud login
        ```
        {: pre}

    2. Crie um ID de serviço denominado `cr-roles-tutorial` com a descrição `"Created during the access control tutorial for Container Registry"` executando o comando a seguir:

        ```
        ibmcloud iam service-id-create cr-roles-tutorial --description "Created during the access control tutorial for Container Registry"
        ```
        {: pre}

    3. Crie uma política de serviço para o ID de serviço que conceda a função de Leitor em `namespace_a` executando o comando a seguir:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_a --roles Reader
        ```
        {: pre}

    4. Crie uma segunda política de serviço que conceda a função de Gravador em `namespace_b` executando o comando a seguir:

        ```
        ibmcloud iam service-policy-create cr-roles-tutorial --service-name container-registry --region <Region> --resource-type namespace --resource namespace_b --roles Writer
        ```
        {: pre}

    5. Crie uma chave de API para o ID de serviço executando o comando a seguir:

        ```
        ibmcloud iam service-api-key-create cr-roles-tutorial-apikey cr-roles-tutorial
        ```
        {: pre}

2. Use o Docker para efetuar login com a chave de API do ID de serviço, em que _`<API_Key>`_ é a chave de API, e interaja com o registro:

    1. Efetue login no {{site.data.keyword.registrylong_notm}} executando o comando a seguir:

        ```
        docker login -u iamapikey -p <API_Key> <Region>.icr.io
        ```
        {: pre}

    2. Faça pull da sua imagem executando o comando a seguir:

        ```
        docker pull < Region> .icr.io/namespace_a/hello-world
        ```
        {: pre}

    3. Envie por push sua imagem para `namespace_a` executando o comando a seguir:

        ```
        docker push < Region> .icr.io/namespace_a/hello-world
        ```
        {: pre}

        Esse comando não funciona porque o usuário não tem a função de Gravador em `namespace_a`.

    4. Envie por push sua imagem para `namespace_b` executando o comando a seguir:

        ```
        docker push < Region> .icr.io/namespace_b/hello-world
        ```
        {: pre}

        Esse comando funciona porque o usuário possui a função de Gravador em `namespace_b`.

3. Limpeza:

    1. Liste as políticas de serviço executando o comando a seguir:

        ```
        ibmcloud iam service-policies cr-roles-tutorial
        ```
        {: pre}

        Anote seus IDs de Política.

    2. Exclua as políticas de serviço executando o comando a seguir para cada política:

        ```
        ibmcloud iam service-policy-delete cr-roles-tutorial <Policy_ID>
        ```
        {: pre}

    3. Exclua seu ID de serviço executando o comando a seguir:

        ```
        ibmcloud iam service-id-delete cr-roles-tutorial
        ```
        {: pre}

    4. Efetue login novamente no {{site.data.keyword.registrylong_notm}} como Usuário A:

        ```
        ibmcloud cr login
        ```
        {: pre}

## Etapa 4: limpando
{: #clean_up}

Nesta seção, você remove os recursos que você criou em seções anteriores para deixar sua conta como estava no início deste tutorial.
{:shortdesc}

1. Efetue login em sua conta executando o comando a seguir:

    ```
    ibmcloud login
    ```
    {: pre}

2. Exclua `namespace_a`, `namespace_b` e `namespace_c`, executando os comandos a seguir:

    ```
    ibmcloud cr namespace-rm namespace_a
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_b
    ```
    {: pre}

    ```
    ibmcloud cr namespace-rm namespace_c
    ```
    {: pre}

3. Remova o Usuário B de sua conta executando o comando a seguir:

   ```
   ibmcloud account user-remove <user.b@example.com>
   ```
   {: pre}

Bom trabalho! Você concluiu com êxito este tutorial.
