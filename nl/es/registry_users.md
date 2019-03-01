---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

keywords: IBM Cloud Container Registry, user access role policies, access policies, policies

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

# Definición de políticas de rol de acceso de usuario
{: #user access}

Como administrador, puede definir políticas de acceso para el registro a fin de crear distintos niveles de acceso para distintos usuarios. Por ejemplo, puede autorizar a determinados usuarios a establecer cuotas, mientras que otros usuarios solo pueden ver cuotas.
{: shortdesc}

Debe definir políticas de acceso para cada usuario que trabaje con {{site.data.keyword.registrylong}}. El ámbito de una política de acceso se basa en el rol o los roles definidos por el usuario que determinan las acciones que pueden realizar. Algunas políticas están predefinidas, pero otras se pueden personalizar.

Si ha empezado a utilizar {{site.data.keyword.registrylong_notm}} antes del 4 de octubre de 2018, debe habilitar la imposición de políticas para que las políticas entren en vigor; consulte [Habilitación de la imposición de políticas para usuarios existentes](#existing_users).
{: tip}

Para obtener más información sobre las políticas de rol de acceso de {{site.data.keyword.iamlong}} (IAM), consulte [{{site.data.keyword.iamshort}}](/docs/iam/index.html#iamoverview).

## Creación de políticas
{: #create}

Si desea controlar el acceso a los recursos, debe asignar roles a los usuarios o ID de servicio. El acceso a los recursos de {{site.data.keyword.registrylong_notm}} se puede otorgar al recurso de espacio de nombres por nombre o a todo el servicio, es decir, a todos los espacios de nombres de la cuenta.

Si desea otorgar acceso a todo, no especifique un tipo de recurso ni un recurso. Si desea otorgar acceso a un espacio de nombres específico, especifique el tipo de recurso como `namespace` y utilice el nombre del espacio de nombres como recurso.

**Antes de empezar**

- Decida qué roles necesita cada usuario y sobre qué recursos de {{site.data.keyword.registrylong_notm}}; consulte [Roles de IAM](/docs/services/Registry/iam.html#iam). Tenga en cuenta que puede crear varias políticas; por ejemplo, puede otorgar acceso de escritura sobre un recurso, pero solo otorgar acceso de lectura sobre otro recurso y no otorgar ningún acceso sobre otro recurso. Las políticas son aditivas, lo que significa que una política de lectura global y una política de escritura limitada a un recurso otorga acceso tanto de lectura como de escritura sobre dicho recurso.

- [Invite a usuarios y asigne acceso](/docs/iam/iamuserinv.html#iamuserinv).

  Si desea que los usuarios puedan crear clústeres en {{site.data.keyword.containerlong_notm}}, asegúrese de asignar el rol de administrador de {{site.data.keyword.registrylong_notm}} a dichos usuarios y no asigne un grupo de recursos; consulte [Preparación para crear clústeres](/docs/containers/cs_clusters.html#cluster_prepare).
  {: tip}

Para crear políticas para {{site.data.keyword.registrylong_notm}}, el campo de nombre de servicio debe ser `container-registry`.

- Para crear una política para los usuarios, consulte [Gestión del acceso a los recursos](/docs/iam/mngiam.html#iammanidaccser).
- Para crear una política para los ID de servicio, ejecute el mandato `ibmcloud iam service-policy-create` o utilice la GUI para enlazar roles con los ID de servicio. Para crear políticas, debe tener el rol de Administrador. De forma automática tiene el rol de Administrador sobre su propia cuenta. Para obtener más información, consulte [Creación y trabajo con los ID de servicio](/docs/iam/serviceid.html#serviceids) y [Gestión de políticas de acceso a ID de servicio](/docs/iam/serviceidaccess.html#serviceidpolicy).

## Habilitación de la imposición de políticas para los usuarios existentes
{: #existing_users}

Para los usuarios suministrados después del 4 de octubre de 2018, las políticas de IAM están habilitadas de forma predeterminada. Para los usuarios suministrados antes del 4 de octubre de 2018, después de crear las políticas, debe habilitar la imposición de políticas para que las políticas entren en vigor.

1. [Cree políticas](#create) para los usuarios y los ID de servicio.

2. Para habilitar la imposición de políticas, ejecute el mandato [`bx cr iam-policies-enable`](/docs/container-registry-cli-plugin/container-registry-cli.html#bx_cr_iam_policies_enable).

    Debe tener el rol de Gestor en la cuenta para poder ejecutar el mandato `ibmcloud cr iam-policies-enable`. Tiene automáticamente el rol de Gestor en su propia cuenta.
    {: tip}
