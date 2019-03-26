---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-07"

keywords: IBM Cloud Container Registry, user access role policies, access policies, policies, policy enforcement,

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

# Definizione delle politiche del ruolo di accesso utente
{: #user access}

Come amministratore, puoi definire le politiche di accesso per il tuo registro per creare diversi livelli di accesso per utenti diversi. Ad esempio, puoi autorizzare alcuni utenti ad impostare le quote mentre altri utenti le possono solo visualizzare.
{: shortdesc}

Devi definire le politiche di accesso per ogni utente che utilizza {{site.data.keyword.registrylong}}. L'ambito di una politica di accesso si basa su uno o più ruoli definiti dell'utente che determinano le azioni che è possibile eseguire. Alcune politiche sono predefinite, ma altre possono essere personalizzate.

Se hai iniziato ad utilizzare {{site.data.keyword.registrylong_notm}} prima del 4 ottobre 2018, devi abilitare l'applicazione della politica prima che le tue politiche abbiano effetto, consulta [Abilitazione dell'applicazione della politica per gli utenti esistenti](#existing_users).
{: tip}

Per trovare ulteriori informazioni sulle politiche del ruolo di accesso {{site.data.keyword.iamlong}} (IAM), consulta [{{site.data.keyword.iamshort}}](/docs/iam?topic=iam-iamoverview#iamoverview).

## Creazione delle politiche
{: #create}

Se vuoi controllare l'accesso alle risorse, devi assegnare i ruoli agli utenti o agli ID servizio. L'accesso alle risorse {{site.data.keyword.registrylong_notm}} può essere concesso alla risorsa dello spazio dei nomi per nome o al servizio completo, ossia, a tutti gli spazi dei nomi dell'account.

Se vuoi concedere l'accesso a tutto, non specificare un tipo di risorsa o una risorsa. Se vuoi concedere l'accesso a uno spazio dei nomi specifico, specifica il tipo di risorsa come `namespace` e utilizza il nome dello spazio dei nomi come risorsa.

**Prima di iniziare**

- Decidi di quali ruoli e risorse ha bisogno ogni utente in {{site.data.keyword.registrylong_notm}}, consulta [Ruoli IAM](/docs/services/Registry?topic=registry-iam#iam). Prendi in considerazione che puoi creare più politiche, ad esempio, puoi concedere l'accesso in scrittura a una risorsa ma concedere solo l'accesso in lettura a un'altra risorsa e non concedere l'accesso a un'altra risorsa. Le politiche sono addizionali, il che significa che una politica di lettura globale e una politica di scrittura dedicata alla risorsa concedono sia l'accesso in lettura che in scrittura a quella risorsa.

- [Invita gli utenti e assegna l'accesso](/docs/iam?topic=iam-iamuserinv#iamuserinv).

  Se vuoi che gli utenti possano creare i cluster in {{site.data.keyword.containerlong_notm}}, assicurati di assegnare il ruolo di Amministratore {{site.data.keyword.registrylong_notm}} a tali utenti e non assegnare un gruppo di risorse, consulta [Preparazione per la creazione dei cluster](/docs/containers?topic=containers-clusters#cluster_prepare).
  {: tip}

Per creare le politiche per {{site.data.keyword.registrylong_notm}}, il campo del nome del servizio deve essere `container-registry`.

- Per creare una politica per gli utenti, consulta [Gestione dell'accesso alle risorse](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).
- Per creare una politica per gli ID servizio, esegui il comando `ibmcloud iam service-policy-create` oppure utilizza la GUI per associare i ruoli ai tuoi ID servizio. Per creare le politiche, devi avere il ruolo di Amministratore. Hai automaticamente il ruolo di Amministratore per il tuo account. Per ulteriori informazioni, consulta [Creazione e gestione degli ID servizio](/docs/iam?topic=iam-serviceids#serviceids) e [Gestione delle politiche di accesso degli ID servizio](/docs/iam?topic=iam-serviceidpolicy#serviceidpolicy).

## Abilitazione dell'applicazione della politica per gli utenti esistenti
{: #existing_users}

Per gli utenti di cui è stato eseguito il provisioning dopo il 4 ottobre 2018, le politiche IAM sono abilitate per impostazione predefinita. Per gli utenti di cui è stato eseguito il provisioning prima del 4 ottobre 2018, dopo che hai creato le tue politiche, devi abilitare l'applicazione della politica in modo che le tue politiche abbiano effetto.

1. [Crea le politiche](#create) per i tuoi utenti e ID servizio.

2. Per abilitare l'applicazione della politica, esegui il comando [`bx cr iam-policies-enable`](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli#bx_cr_iam_policies_enable).

    Devi avere il ruolo di Gestore nell'account per poter eseguire il comando `ibmcloud cr iam-policies-enable`. Hai automaticamente il ruolo di Gestore nel tuo account.
    {: tip}
