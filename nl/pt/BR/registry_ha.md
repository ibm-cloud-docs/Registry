---

copyright:
  years: 2018
lastupdated: "2018-09-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# Alta disponibilidade e recuperação de desastre
{: #ha-dr}

O {{site.data.keyword.registrylong}} é um serviço regional altamente disponível.
{:shortdesc}

* Em cada região suportada, a carga do tráfego é balanceada em toda a infraestrutura de registro em várias zonas de disponibilidade, sem nenhum ponto único de falha.

* Os dados armazenados no {{site.data.keyword.registrylong_notm}} são submetidos a backup regularmente, fornecendo resiliência adicional.

* Se você estiver preocupado com a disponibilidade de suas imagens no caso de uma região inteira ficar indisponível, será possível optar por enviar suas imagens por push para múltiplos registros regionais. 
  
  Também é possível optar por enviar suas imagens por push para múltiplos registros no caso de você excluir ou sobrescrever acidentalmente suas imagens.

  Para obter mais informações sobre regiões, consulte [Regiões](/docs/services/Registry/registry_overview.html#registry_regions).
