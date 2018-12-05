---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Imágenes públicas de {{site.data.keyword.IBM_notm}}
{: #public_images}

Puede acceder a las imágenes que proporciona {{site.data.keyword.IBM}} desde la línea de mandatos. Ya no puede acceder a las imágenes públicas de {{site.data.keyword.IBM_notm}} mediante la interfaz gráfica de usuario.
{:shortdesc}

## Acceso a las imágenes públicas de IBM mediante la CLI
{: #public_images_cli}

Puede acceder a las imágenes públicas de {{site.data.keyword.IBM_notm}} mediante la línea de mandatos.
{:shortdesc}

**Antes de empezar**

- Inicie una sesión en [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login):

  ```
  ibmcloud login
  ```
  {: pre}

Para ver una lista de las imágenes públicas, siga estos pasos:

1. Establezca como destino el registro global:

   ```
   ibmcloud cr region-set global
   ```
   {: pre}

2. Obtenga una lista de las imágenes públicas de {{site.data.keyword.IBM_notm}}:

   ```
   ibmcloud cr images --include-ibm
   ```
   {: pre}
