---
title: Composants de site | Microsoft Docs
description: "Apprenez à configurer des composants de site pour modifier le comportement des rôles système de site et la création des rapports d’état de site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e22ffc898dc93f702f13417878aa6050d4cdd4ec


---
# <a name="site-components-for-system-center-configuration-manager"></a>Composants de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Sur chaque site System Center Configuration Manager, vous pouvez configurer des composants de site pour modifier le comportement des rôles système de site et la création des rapports d’état de site. Les configurations de composants de site s’appliquent à un site donné et à chaque instance d’un rôle de système de site applicable au niveau de ce site.  

## <a name="about-site-components"></a>À propos des composants de site  
 La plupart des options des différents composants de site sont suffisamment explicites quand elles apparaissent dans la console Configuration Manager. Toutefois, les informations suivantes peuvent être utiles pour mieux comprendre certaines configurations plus complexes ou vous diriger vers du contenu supplémentaire qui les explique :  

**Distribution de logiciels :**  

-   **Paramètres de distribution de contenu**  : vous pouvez configurer les paramètres qui modifient la façon dont le serveur de site transfère du contenu vers ses points de distribution. Si vous augmentez les valeurs des paramètres de distribution simultanée, la distribution de contenu risque d’utiliser davantage de bande passante réseau.  

-   **Compte d’accès réseau :** pour plus d’informations sur la configuration et l’utilisation du compte d’accès réseau, consultez [Compte d’accès réseau](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA)  

**Point de mise à jour logicielle :**  

-   pour plus d’informations sur les options de configuration du composant de point de mise à jour logicielle, consultez [Installer un point de mise à jour logicielle](../../../../sum/get-started/install-a-software-update-point.md).  

**Point de gestion :**  

-   **Points de gestion :** vous pouvez configurer le site pour publier des informations sur ses points de gestion dans les services de domaine Active Directory.  

     Les clients Configuration Manager utilisent des points de gestion pour l’emplacement du service, pour rechercher des informations sur le site, telles que les appartenances à des groupes de limites et les options de sélection de certificats PKI, mais également pour rechercher d’autres points de gestion du site ainsi que des points de distribution, d’où ils peuvent télécharger des logiciels. Les clients utilisent également les points de gestion pour terminer l'attribution de site et télécharger la stratégie client et leurs informations client.  

     Comme la plus sûre des méthodes pour que les clients trouvent des points de gestion est de publier ceux-ci dans les services de domaines Active Directory, vous aurez généralement toujours besoin de sélectionner tous les points de gestion en fonctionnement pour publier dans les services de domaine Active Directory. Cette méthode d’emplacement du service requiert toutefois l’extension du schéma pour Configuration Manager (il existe un conteneur **Gestion du système** disposant des autorisations de sécurité appropriées pour que le serveur de site puisse publier dans ce conteneur), la configuration du site Configuration Manager pour publier dans les services de domaine Active Directory et l’appartenance des clients à la même forêt Active Directory que celle du serveur de site.  

     Quand des clients sur l’intranet ne peuvent pas utiliser les services de domaine Active Directory pour rechercher des points de gestion, utilisez la publication [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

     Pour obtenir des informations générales sur l’emplacement du service, consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publier les points de gestion d’intranet sélectionnés dans DNS :** spécifiez cette option quand des clients sur l’intranet ne trouvent pas de points de gestion à partir des services de domaine Active Directory, mais qu’ils peuvent utiliser un enregistrement de ressource d’emplacement de service DNS (SRV RR) pour trouver un point de gestion dans leur site attribué.  

    Pour que Configuration Manager puisse publier des points de gestion intranet dans DNS, toutes les conditions suivantes doivent être remplies :  

    -   Vos serveurs DNS ont une version de BIND 8.1.2 ou ultérieure.  

    -   Vos serveurs DNS sont configurés pour les mises à jour automatiques et prennent en charge les enregistrements de ressource d'emplacement de service.  

    -   Les noms de domaine complets spécifiés pour les points de gestion dans Configuration Manager ont des entrées d’hôte (enregistrements A ou AAA) dans DNS.  

    > [!WARNING]  
    >  Pour que les clients identifient leurs points de gestion publiés dans DNS, vous devez attribuer les clients à un site spécifique (et non utiliser l'attribution automatique de site), et vous devez configurer ces clients pour qu'ils utilisent le code de site avec le suffixe du domaine de leur point de gestion. Pour plus d’informations, consultez [Localisation de points de gestion](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_LocatingMPs) dans [Guide pratique pour affecter des clients à un site dans System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

     Si les clients Configuration Manager ne peuvent pas utiliser les services de domaine Active Directory ou DNS pour rechercher des points de gestion sur l’intranet, ils peuvent recourir à l’utilisation de [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). Le premier point de gestion installé pour le site est automatiquement publié dans WINS lorsqu'il est configuré pour accepter les connexions client HTTP sur l'intranet.  

**Rapport d'état :**  

-   Ces paramètres configurent directement le niveau de détail qui est fourni dans les rapports d’état à partir de sites et de clients.  

**Notification par courrier électronique :**  

-   Spécifiez les détails de compte ou de serveur de messagerie pour que Configuration Manager envoie des notifications par e-mail en cas d’alertes.  

**Évaluation de l’appartenance au regroupement :**  

-   Cette tâche permet de définir la fréquence à laquelle l’appartenance à un regroupement est évaluée de façon incrémentielle. L'évaluation incrémentielle met à jour une appartenance à un regroupement uniquement avec de nouvelles ressources ou des ressources modifiées.  

#### <a name="to-edit-the-site-components-at-a-site"></a>Pour modifier les composants de site sur un site  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration du site** > **Sites**, puis sélectionnez le site comportant les composants de site que vous allez configurer.  

2.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Configurer les composants de site** , puis sélectionnez le composant de site que vous souhaitez configurer.  

##  <a name="a-namebkmkservicemgra-use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Utiliser Configuration Manager Service Manager pour gérer les composants de site  
Vous pouvez utiliser Configuration Manager Service Manager pour contrôler les services Configuration Manager et afficher l’état de tout service ou thread de travail Configuration Manager (collectivement appelés composants Configuration Manager) :  

-   Les composants Configuration Manager peuvent s’exécuter sur n’importe quel système de site.  

-   Ils sont gérés de la même façon que les services dans Windows : vous pouvez les démarrer, les arrêter, les suspendre, les reprendre ou les interroger.  

Un service Configuration Manager s’exécute dès qu’il a une tâche à effectuer (quand un fichier de configuration est enregistré dans la boîte de réception d’un composant, par exemple). Si vous devez identifier le composant impliqué dans une opération, vous pouvez utiliser **Configuration Manager Service Manager** pour agir sur plusieurs services et threads Configuration Manager, puis afficher les effets sur le comportement de Configuration Manager. Vous pouvez par exemple arrêter les services Configuration Manager un par un jusqu’à ce qu’une réponse spécifique disparaisse. Vous pourrez ainsi déterminer le service qui provoque ce comportement.  

> [!TIP]  
>  La procédure suivante peut servir à manipuler des opérations de composants Configuration Manager.  

#### <a name="to-use-the-configuration-manager-service-manager"></a>Pour utiliser le Gestionnaire de service de Configuration Manager  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance** >  **État du système**, puis cliquez sur **État du composant**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Composant** , cliquez sur **Démarrer**, puis sélectionnez **Gestionnaire de service de Configuration Manager**.  

3.  Lorsque le Gestionnaire de service de Configuration Manager s'ouvre, connectez-vous au site que vous souhaitez gérer.  

     Si vous ne voyez pas le site que vous souhaitez gérer, cliquez sur **Site**, puis sur **Connecter**, et entrez le nom du serveur de site du site correct.  

4.  Développez le site et accédez à **Composants** ou à **Serveurs** selon l'emplacement où se trouvent les composants que vous souhaitez gérer.  

5.  Dans le volet droit, sélectionnez un ou plusieurs composants, puis dans le menu **Composant** , cliquez sur **Requête** pour mettre à jour l'état de votre sélection.  

6.  Après la mise à jour de l'état du composant, utilisez l'une des quatre actions en option dans le menu **Composant** pour modifier le fonctionnement des composants. Après avoir demandé une action, vous devez demander au composant d'afficher son nouvel état.  

7.  Fermez Configuration Manager Service Manager quand vous avez fini de modifier l’état opérationnel des composants.  



<!--HONumber=Dec16_HO3-->

