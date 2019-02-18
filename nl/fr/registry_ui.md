---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-04"

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

La colonne **Statut de sécurité** présente les informations suivantes sur l'image :

- `Sécurisée` Aucun problème de sécurité n'a été détecté.
- `Vulnérable` Des problèmes de sécurité ou de configuration ont été détectés et doivent être corrigés avant que l'image ne puisse être déployée.
- `Incomplet` L'analyse n'est pas terminée. Il se peut que l'analyse soit encore en cours ou que le système d'exploitation soit de l'image ne soit pas compatible. Patientez et relancez l'analyse. Si l'analyse est toujours incomplète, transférez à nouveau l'image pour lancer une nouvelle analyse. Le déploiement
des images dont l'analyse est incomplète n'est pas bloqué.
- `Système d'exploitation non pris en charge` Le système d'exploitation dans l'image n'est pas pris en charge.

Pour afficher l'interface graphique, procédez comme suit :

1. Connectez-vous à la console {{site.data.keyword.Bluemix_notm}} ([https://console.bluemix.net ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net)) avec votre IBMid.
2. Si vous disposez de plusieurs comptes {{site.data.keyword.Bluemix_notm}}, sélectionnez le compte et la région à utiliser dans le menu Compte.
3. Cliquez sur **Catalogue**.
4. Sélectionnez la catégorie **Conteneurs** et cliquez sur la vignette **Container Registry**.
5. Pour afficher des informations sur les images de vos référentiels privés, cliquez sur **Images**. Une liste des images de vos référentiels privés avec le statut de sécurité pour chacune d'elle s'affiche.
6. Pour plus d'informations sur les vulnérabilités potentielles, notamment les balises et l'historique des images, cliquez sur la ligne correspondant à l'image dans le tableau. L'onglet **Détails de l'image** s'ouvre.
7. Pour en savoir plus sur les problèmes par type, cliquez sur l'onglet **Problèmes par type**.
8. Pour obtenir des informations sur les conteneurs associés, cliquez sur l'onglet **Conteneurs associés**.

Pour plus d'informations sur la signification des informations dans le rapport de sécurité, voir [Gestion de la sécurité des images avec Vulnerability Advisor](/docs/services/va/va_index.html).
