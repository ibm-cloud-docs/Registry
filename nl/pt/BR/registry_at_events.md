---

copyright:
  years: 2018
lastupdated: "2018-09-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Eventos do {{site.data.keyword.cloudaccesstrailshort}}  
{: #at_events}

Use o serviço {{site.data.keyword.cloudaccesstrailfull}} para controlar como os usuários e aplicativos interagem com o serviço {{site.data.keyword.registrylong}} no {{site.data.keyword.Bluemix}}. 
{:shortdesc}

O serviço {{site.data.keyword.cloudaccesstrailfull_notm}} registra as atividades iniciadas pelo usuário que mudam
o estado de um serviço no {{site.data.keyword.Bluemix_notm}}. 
Para obter mais informações, consulte [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). 

A tabela a seguir lista os métodos de API que geram um evento quando eles são chamados:

<table>
  <caption>Ações que geram eventos</caption>
  <tr>
    <th>Action</th>
	  <th>descrição</th>
  </tr>
  <tr>
    <td>`container-registry.exemption.create`</td>
	  <td>Crie uma isenção do Vulnerability Advisor.</td>
  </tr>
  <tr>
    <td>`container-registry.exemption.delete`</td>
	  <td>Exclua uma isenção do Vulnerability Advisor.</td>
  </tr>
 </table>



## Onde procurar os eventos
{: #ui}

Os eventos do {{site.data.keyword.cloudaccesstrailshort}} estão disponíveis no
{{site.data.keyword.cloudaccesstrailshort}} **domínio de contas** disponível na região do
{{site.data.keyword.Bluemix_notm}} na qual eles são gerados.

A região na qual um evento do Vulnerability Advisor está disponível corresponde à região do {{site.data.keyword.registrylong_notm}} na qual o recurso (por exemplo, a imagem ou o namespace) está disponível.






