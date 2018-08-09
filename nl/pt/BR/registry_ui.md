---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Monitorando a vulnerabilidade de imagens
{: #registry_ui}

É possível visualizar informações sobre potenciais vulnerabilidades e a segurança de imagens nos repositórios públicos e privados do {{site.data.keyword.registrylong}} usando o console do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

A coluna **RELATÓRIO DE SEGURANÇA** mostra as informações sobre a imagem a seguir:
-   `Secure` Nenhum problema de segurança foi localizado.
-   `Vulnerable` Problemas de segurança ou configuração foram localizados e devem ser direcionados antes de poder implementar a imagem.
-   `Incomplete` A varredura não está completa. A varredura ainda pode estar em execução ou o sistema operacional da imagem pode não ser compatível. Aguarde e tente a varredura novamente. Se a varredura ainda não tiver sido concluída, envie a imagem por push novamente para iniciar uma nova varredura. As
imagens com varreduras incompletas não são bloqueadas para implementação.
-   `S.O. não suportado` O sistema operacional na imagem não é suportado.

Para visualizar a interface gráfica com o usuário, use as etapas a seguir:

1.  Efetue login no console do {{site.data.keyword.Bluemix_notm}} ([https://console.bluemix.net](https://console.bluemix.net)) com seu IBMid.
2.  Se você tiver múltiplas contas do {{site.data.keyword.Bluemix_notm}}, selecione a conta e região que você deseja usar por meio do menu de conta.
3.  Clique em **Catálogo**.
4.  Selecione a categoria **Contêineres** e clique no tile **Registro de contêiner**.
5.  Para visualizar informações sobre imagens em seus repositórios privados, clique em **Repositórios privados**. Uma lista de imagens em seus repositórios privados e o status do relatório de segurança para cada imagem são exibidos. Para descobrir mais informações sobre as vulnerabilidades em potencial, incluindo as tags e a compilação de imagem, clique na linha na tabela.
6.  Para visualizar informações sobre imagens nos repositórios públicos, clique em **Repositórios públicos**. Uma lista de imagens nos repositórios públicos com um link para a documentação e o relatório de segurança para cada imagem são exibidos. Para descobrir mais informações sobre as vulnerabilidades em potencial, incluindo as tags e a compilação de imagem, clique na linha na tabela.

Para saber mais sobre o significado das informações no relatório de segurança, veja [Gerenciando a segurança de imagem com o Vulnerability Advisor](../va/va_index.html).
