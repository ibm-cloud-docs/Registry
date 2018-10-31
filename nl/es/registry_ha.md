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



# Alta disponibilidad y recuperación tras desastre
{: #ha-dr}

El servicio {{site.data.keyword.registrylong}} es un servicio regional de alta disponibilidad.
{:shortdesc}

* En cada región soportada, el tráfico se equilibra a través de la infraestructura de registro en varias zonas de disponibilidad, sin un único punto de fallo.

* Se realiza una copia de seguridad de forma regular de los datos almacenados en {{site.data.keyword.registrylong_notm}}, que proporciona más resiliencia.

* Si le preocupa la disponibilidad de sus imágenes en el caso de que toda una región no esté disponible, puede optar por enviar por push sus imágenes a varios registros regionales. 
  
  También puede elegir enviar por push sus imágenes a varios registros en caso de que accidentalmente borre o sobrescriba sus imágenes.

  Para obtener más información sobre regiones, consulte [Regiones](/docs/services/Registry/registry_overview.html#registry_regions).
