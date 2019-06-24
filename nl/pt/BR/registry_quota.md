---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: IBM Cloud Container Registry, quota limits, custom quota limits, pull traffic, quotas, storage,

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

# Gerenciando os limites de cota para armazenamento e tráfego de pull
{: #registry_quota}

É possível limitar a quantia de armazenamento e tráfego extraído que pode ser usada em sua conta do {{site.data.keyword.cloud}} configurando e gerenciando os limites
de cota customizados.
{:shortdesc}

## Configurando limites de cota para armazenar e puxar imagens
{: #registry_quota_set}

É possível limitar a quantia de armazenamento e tráfego extraído para as suas imagens privadas configurando
os seus próprios limites de cota.
{:shortdesc}

Ao fazer upgrade para o plano padrão do {{site.data.keyword.registryshort_notm}}, você se beneficiará de
uma quantia ilimitada de armazenamento e de tráfego extraído para as suas imagens privadas. Para evitar exceder o seu nível de pagamento preferencial, será possível configurar cotas individuais para a
quantia de armazenamento e tráfego extraído. Limites de cota são aplicados a todos os namespaces que você configurou no
{{site.data.keyword.registrylong_notm}}. Se você estiver usando o plano
de serviço grátis, também poderá configurar cotas customizadas em sua quantia de armazenamento livre e tráfego extraído.

Para configurar uma cota:

1. Efetue login no {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Revise os seus limites de cota atuais para armazenamento e tráfego extraído.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Sua
saída é semelhante à mostrada a seguir.

    ```
    Obtendo cotas e uso para o mês atual, para a conta 'Conta <account_owner>'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    Ok
    ```
    {: screen}

3. Mude o limite de cota para armazenamento e tráfego extraído. Para mudar o uso do tráfego de pull, especifique a opção **traffic** e substitua `<traffic_quota>` pelo valor em megabytes que você deseja configurar para a cota de tráfego de pull. Se desejar mudar a quantia de armazenamento em sua conta, especifique a opção **storage** e substitua `<storage_quota>` pelo valor em megabytes que você deseja configurar.

    Se você estiver no plano grátis, não será possível configurar sua cota para uma quantia que excede a camada grátis. O abono da camada grátis para armazenamento é de 512 MB e o tráfego é de 5120 MB.
    {:tip}

    ```
    ibmcloud cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    Exemplo para configurar seu limite de cota de armazenamento para 600 megabytes e o tráfego extraído para 7.000 megabytes:

    ```
    ibmcloud cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}

## Revisando limites de cota e uso para armazenar e puxar imagens
{: #registry_quota_get}

É possível revisar os seus limites de cota e verificar o seu armazenamento atual e uso de tráfego extraído
para a sua conta.
{:shortdesc}

1. Efetue login no {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud login
    ```
    {: pre}

2. Revise os seus limites de cota atuais para armazenamento e tráfego extraído.

    ```
    ibmcloud cr quota
    ```
    {: pre}

    Sua
saída é semelhante à mostrada a seguir.

    ```
    Obtendo cotas e uso para o mês atual, para a conta 'Conta <account_owner>'...

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB

    Ok
    ```
    {: screen}

## Liberando o armazenamento usado e mudando planos de serviço ou limites de cota para permanecer dentro dos limites de cota fornecidos
{: #registry_quota_freeup}

Se você excedeu os seus limites de cota que estiverem configurados para a sua conta do {{site.data.keyword.cloud_notm}}, será possível liberar o armazenamento e
mudar o seu plano de serviço ou os limites de cota para continuar enviando por push e puxando imagens para e de seu
namespace.
{:shortdesc}

Para liberar o armazenamento de imagem em sua conta do {{site.data.keyword.cloud_notm}}:

1. Liste todas as imagens em todos os seus namespaces de sua conta do {{site.data.keyword.cloud_notm}}.

    ```
    ibmcloud cr images
    ```
    {: pre}

2. Remova uma imagem de seu namespace. Substitua `<image_name>` pelo nome da imagem que você deseja remover.

    ```
    ibmcloud cr image-rm <image_name>
    ```
    {: pre}

    Dependendo do tamanho
da imagem, pode demorar um pouco para a imagem ser removida e para o armazenamento ficar disponível.
    {:tip}

3. Revise o uso de sua cota de armazenamento.

    ```
    ibmcloud cr quota
    ```
    {: pre}

4. Não é possível reduzir o uso de seu tráfego extraído em um período de faturamento.
   {:tip}

    Para continuar a puxar imagens de seus namespaces, escolha entre as opções a seguir.

    - Espere até que o próximo ciclo de faturamento seja iniciado.
    - Se você tem um plano grátis, [faça upgrade para o plano
de serviço padrão](/docs/services/Registry?topic=registry-registry_overview#registry_plan_upgrade).
    - Se você já tem um plano padrão, [configure novos limites
de cota para o tráfego extraído](#registry_quota_set).
