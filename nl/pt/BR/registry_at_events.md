---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

keywords: IBM Cloud Container Registry, IBM Cloud Activity Tracker events, Activity Tracker events, events, track,

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

# Eventos do {{site.data.keyword.cloudaccesstrailshort}}
{: #at_events}

Use o serviço {{site.data.keyword.cloudaccesstrailfull}} para controlar como os usuários e aplicativos interagem com o serviço {{site.data.keyword.registrylong}} no {{site.data.keyword.cloud}}.
{:shortdesc}

O serviço {{site.data.keyword.cloudaccesstrailfull_notm}} registra as atividades iniciadas pelo usuário que mudam
o estado de um serviço no {{site.data.keyword.cloud_notm}}.
Para obter mais informações, consulte [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).

A tabela a seguir lista os métodos de API que geram um evento quando eles são chamados:

<table>
  <caption>Tabela 1. Ações que geram eventos</caption>
  <tr>
    <th>Ação</th>
	  <th>Descrição</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Crie uma isenção do Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Exclua uma isenção do Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.image.build`</td>
	  <td>Constrói uma imagem do Docker em {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.delete`</td>
	  <td>Exclui uma imagem do {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.inspect`</td>
	  <td>Exibe detalhes sobre uma imagem.</td>
  </tr>
  <tr>
    <td>`container-registry.image.list`</td>
	  <td>Lista as imagens em sua conta da {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.pull`</td>
	  <td>Extrai uma imagem do {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.push`</td>
	  <td>Envia por push uma imagem para o {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
    <td>`container-registry.image.rm`</td>
	  <td>Exclua uma ou mais imagens especificadas do {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.image.tag`</td>
	  <td>Inclui uma nova tag que se refere a uma imagem preexistente do {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
   <tr>
    <td>`container-registry.image.untag`</td>
	  <td>Remover uma ou diversas tags de cada imagem especificada no {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.create`</td>
	  <td>Inclui um namespace no {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.delete`</td>
	  <td>Exclui um namespace do {{site.data.keyword.registrylong_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.namespace.list`</td>
	  <td>Lista os namespaces em sua conta da {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.get`</td>
	  <td>Exibe as cotas atuais para tráfego e armazenamento e as informações de uso com relação a essas cotas.</td>
  </tr>
  <tr>
    <td>`container-registry.quota.set`</td>
	  <td>Modifica as cotas.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.delete`</td>
	  <td>Exclui um token de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.get`</td>
	  <td>Recupera as informações sobre um token de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytoken.list`</td>
	  <td>Lista os tokens de registro em sua conta {{site.data.keyword.IBM_notm}}.</td>
  </tr>
  <tr>
    <td>`container-registry.registrytokens.delete`</td>
	  <td>Exclui múltiplos tokens de registro.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.get`</td>
	  <td>Exibe as informações sobre o plano de precificação atual.</td>
  </tr>
  <tr>
    <td>`container-registry.plan.set`</td>
	  <td>Faça upgrade para o plano padrão.</td>
  </tr>
 </table>

## Onde procurar os eventos
{: #ui}

Os eventos do {{site.data.keyword.cloudaccesstrailshort}} estão disponíveis no **domínio de contas** do {{site.data.keyword.cloudaccesstrailshort}}, que está disponível na região do {{site.data.keyword.cloud_notm}} na qual os eventos são gerados, exceto em `ap-north`. Os eventos para `ap-north` são exibidos no `ap-south`.

A [região](/docs/services/Registry?topic=registry-registry_overview#registry_regions) na qual um {{site.data.keyword.registrylong_notm}} ou um evento do Vulnerability Advisor está disponível corresponde à região do {{site.data.keyword.registrylong_notm}} na qual o recurso (por exemplo, a imagem ou o namespace) está disponível.
