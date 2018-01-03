---

copyright:
  years: 2017
lastupdated: "2017-12-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Surveillance de la vulnérabilité des images
{: #registry_ui}

Vous pouvez examiner des informations sur les vulnérabilités potentielles et sur la sécurité des images dans les référentiels publics et privés {{site.data.keyword.registrylong}} en utilisant la console {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La colonne **Rapport de sécurité** présente les informations suivantes sur l'image :
-   `Sécurisée` Aucun problème de sécurité n'a été détecté.
-   `Vulnérable` Des problèmes de sécurité ou de configuration ont été détectés et doivent être corrigés avant que l'image ne puisse être déployée.
-   `Incomplet` L'analyse n'est pas terminée. Il se peut que l'analyse soit encore en cours ou que le système d'exploitation soit de l'image ne soit pas compatible. Patientez et relancez l'analyse. Si l'analyse est toujours incomplète, transférez à nouveau l'image pour lancer une nouvelle analyse. Le déploiement
des images dont l'analyse est incomplète n'est pas bloqué.
-   `Système d'exploitation non pris en charge` Le système d'exploitation dans l'image n'est pas pris en charge.
    
Pour afficher l'interface graphique, procédez comme suit :

1.  Connectez-vous à la console {{site.data.keyword.Bluemix_notm}} ([https://console.bluemix.net](https://console.bluemix.net)) avec votre IBMid.
2.  Si vous disposez de plusieurs comptes {{site.data.keyword.Bluemix_notm}}, sélectionnez le compte et la région à utiliser dans le menu Compte.
3.  Cliquez sur **Catalogue**.
4.  Sélectionnez la catégorie **Conteneurs** et cliquez sur la vignette **Container Registry**.
5.  Pour afficher des informations sur les images de vos référentiels privés, cliquez sur **Référentiels privés**. Une liste des images dans vos référentiels privés avec le statut du rapport de sécurité de chaque image est affichée. Pour plus d'informations sur les vulnérabilités potentielles, notamment les étiquettes et le sommaire de l'image, cliquez sur la ligne dans le tableau.
6.  Pour afficher des informations sur les images des référentiels publics, cliquez sur **Référentiels publics**. Une liste des images dans les référentiels publics avec un lien vers la documentation et le rapport de sécurité de chaque image est affichée. Pour plus d'informations sur des vulnérabilités potentielles, notamment les étiquettes et le sommaire de l'image, cliquez sur la ligne dans le tableau .

Pour plus d'informations sur la signification des informations dans le rapport de sécurité, voir [Gestion de la sécurité des images avec Vulnerability Advisor](../va/va_index.html).
