---
title: "Déployer des clients Windows | Microsoft Docs"
description: "Découvrez comment déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 9555a16d97224a1cf49a426ab225468b07403f60
ms.openlocfilehash: 0e5e624fdfc2b5ee5b497d1063bd4e2d15df578b
ms.contentlocale: fr-fr
ms.lasthandoff: 12/29/2016


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Comment déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’installer des clients Configuration Manager, vérifiez que toutes les [conditions préalables](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) sont réunies et que vous avez réalisé toutes les configurations de déploiement requises.   

##  <a name="BKMK_ClientPush"></a> Guide pratique pour installer des clients à l’aide d’une installation poussée du client  

Vous pouvez configurer l'installation poussée du client pour un site, et l'installation du client est exécutée automatiquement sur les ordinateurs qui sont découverts dans les limites configurées pour le site lorsque ces limites sont configurées en tant que groupe de limites. Vous pouvez également lancer une installation poussée du client en exécutant l'Assistant Installation poussée du client pour un regroupement ou une ressource spécifique dans un regroupement.  

L’Assistant Installation poussée du client permet également d’installer le client Configuration Manager selon les résultats d’une [requête](../../../core/servers/manage/queries-technical-reference.md). Pour que l’installation réussisse, l’un des éléments retournés par la requête doit correspondre à l’attribut **ResourceID** de la classe **Ressource système**.   

Si le serveur de site ne parvient pas à contacter l’ordinateur client ou à démarrer le processus d’installation, il répète la tentative d’installation automatiquement toutes les heures pendant une période maximale de sept jours.  

Pour vous aider à suivre le processus d'installation du client, installez un système de site de point d'état de secours avant d'installer les clients. Lorsqu'un point d'état de secours est installé, il est automatiquement attribué aux clients lorsque ces derniers sont installés par la méthode d'installation poussée du client. Affichez les rapports de déploiement et d'affectation de client pour suivre la progression de l'installation du client. 

Les fichiers journaux des clients fournissent des informations de dépannage plus détaillées et ne nécessitent pas de point d’état de secours. Par exemple, le fichier CCM.log sur le serveur de site enregistre tous les problèmes de connexion du serveur de site à l'ordinateur, et le fichier CCMSetup.log sur le client enregistre le processus d'installation.  

> [!IMPORTANT]  
>  Afin que l'installation poussée du client réussisse, assurez-vous que toutes les conditions préalables sont respectées. Celles-ci sont répertoriées dans la section « Dépendances liées aux méthodes d’installation » de la rubrique [Configuration requise pour le déploiement de clients sur des ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Pour configurer le site en vue de l'utilisation automatique de l'installation poussée du client pour des ordinateurs découverts

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** > **Sites**.  

3.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation poussée du client automatique à l’échelle du site.  

4.  Dans l’onglet **Accueil** du groupe **Paramètres**, choisissez **Paramètres d’installation du client** > **Installation poussée du client**.  

5.  Dans l’onglet **Général** de la boîte de dialogue **Propriétés de l’installation poussée du client**, sélectionnez **Activer l’installation poussée du client automatique à l’échelle du site**. Sélectionnez les types de systèmes vers lesquels Configuration Manager doit transférer (push) le logiciel client.  

6.  Indiquez si vous souhaitez installer le client sur les contrôleurs de domaine.  

7.  Sous l’onglet **Comptes**, spécifiez un ou plusieurs comptes que doit utiliser Configuration Manager pour se connecter à l’ordinateur sur lequel installer le logiciel client. Cliquez sur l’icône **Créer**, entrez le **nom d’utilisateur** et le **mot de passe** (pas plus de 38 caractères), confirmez le mot de passe, puis cliquez sur **OK**. Vous devez spécifier au moins un compte d'installation poussée du client, qui doit avoir des droits d'administrateur local sur chaque ordinateur sur lequel vous souhaitez installer le client. Si vous ne spécifiez pas de compte d’installation Push du client, Configuration Manager essaie d’utiliser le compte d’ordinateur de système de site, ce qui provoque l’échec de l’installation Push du client sur plusieurs domaines.  

    
    > [!NOTE]  
    >  Si vous avez l'intention d'utiliser la méthode d'installation poussée du client à partir d'un site secondaire, le compte doit être spécifié sur le site secondaire qui déclenche l'installation poussée du client.  
    >   
    >  Pour plus d’informations sur le compte d’installation Push du client, consultez la procédure « Pour utiliser l’Assistant Installation Push du client », ci-dessous.  

8.  Renseignez l’onglet **Propriétés de l’installation**.

     Les [propriétés d’installation du client](../../../core/clients/deploy/about-client-installation-properties.md) spécifiées sous cet onglet sont publiées sur les services de domaine Active Directory si le schéma est étendu pour Configuration Manager et sont lues par les installations du client dans lesquelles CCMSetup est exécuté sans propriétés d’installation.  

    > [!NOTE]  
    >  Si vous activez l’installation Push du client sur un site secondaire, assurez-vous que la propriété SMSSITECODE est définie sur le nom de site Configuration Manager de son site principal parent. Si vous étendez le schéma Active Directory pour Configuration Manager, vous pouvez également définir cette option sur AUTO pour rechercher automatiquement l’attribution de site correcte.  

### <a name="to-use-the-client-push-installation-wizard"></a>Pour utiliser l’Assistant Installation Push du client

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Configuration du site** > **Sites**.  

3.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation poussée du client automatique à l’échelle du site.  

4.  Dans l’onglet **Accueil** du groupe **Paramètres**, choisissez **Paramètres d’installation du client** > **Installation poussée du client**.  

5.  Renseignez l’onglet **Propriétés de l’installation**.  

     Les [propriétés d’installation du client](../../../core/clients/deploy/about-client-installation-properties.md) spécifiées sous cet onglet sont publiées sur les services de domaine Active Directory si le schéma est étendu pour Configuration Manager et sont lues par les installations du client dans lesquelles CCMSetup est exécuté sans propriétés d’installation.  

6.  Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

7.  Dans l'espace de travail **Ressources et Conformité** , sélectionnez un ou plusieurs ordinateurs ou un regroupement d'ordinateurs.  

8.  Dans l'onglet **Accueil** , sélectionnez l'une des options suivantes :  

    -   Si vous souhaitez installer le client sur un seul ordinateur ou plusieurs ordinateurs, dans le groupe **Appareil**, choisissez **Installer le client**.  

    -   Si vous souhaitez installer le client dans un regroupement d’ordinateurs, dans le groupe **Regroupement**, choisissez **Installer le client**.  

9. Dans la page **Avant de commencer** de l’**Assistant Installation du client**, consultez les informations, puis choisissez **Suivant**.  

10. Renseignez la page **Options d’installation**.  

11. Passez en revue les paramètres d'installation, puis fermez l'Assistant.  

> [!NOTE]  
>  L'assistant peut être utilisé pour installer des clients même si le client n'est pas configuré pour l'installation poussée du client.  

##  <a name="BKMK_ClientSUP"></a> Guide pratique pour installer des clients à l’aide d’une installation basée sur une mise à jour logicielle  
 L’installation du client en fonction des mises à jour logicielles publie le client sur un point de mise à jour logicielle, sous forme de mise à jour logicielle. Utilisez cette méthode pour une première installation ou une mise à niveau.  

 Si le client est installé sur un ordinateur, Configuration Manager fournit le client avec la stratégie client, ce qui inclut le nom du serveur du point de mise à jour logicielle ainsi que le port à partir duquel les mises à jour logicielles sont obtenues.   

> [!IMPORTANT]  
>  Pour pouvoir utiliser l'installation basée sur les mises à jour logicielles, vous devez utiliser le même serveur Windows Server Update Services (WSUS) pour l'installation du client et les mises à jour logicielles. Ce serveur doit être utilisé comme le point de mise à jour logicielle actif dans un site principal. Pour plus d’informations, consultez [Installer un point de mise à jour logicielle](../../../sum/get-started/install-a-software-update-point.md).  

Si un ordinateur ne dispose pas du client Configuration Manager, vous devez configurer et attribuer un objet de stratégie de groupe (GPO) dans les services de domaine Active Directory pour spécifier le nom du serveur du point de mise à jour logicielle.  

Il est impossible d'ajouter des propriétés de ligne de commande à une installation du client basé sur des mises à jour logicielles. Si vous avez étendu le schéma Active Directory pour Configuration Manager, les ordinateurs clients demandent automatiquement les propriétés d’installation aux services de domaine Active Directory au moment de l’installation.  

Si vous n'avez pas étendu le schéma Active Directory, vous pouvez utiliser la stratégie de groupe pour ajouter les paramètres d'installation du client aux ordinateurs de votre site. Ces paramètres s'appliquent automatiquement à toutes les installations du client basé sur les mises à jour logicielles. Pour plus d’informations, consultez [Comment fournir des propriétés d’installation du client (Stratégie de groupe et installation du client basé sur les mises à jour logicielles)](#BKMK_Provision) et [Comment affecter des clients à un site dans System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Les procédures ci-dessous vous permettent de configurer des ordinateurs sans client Configuration Manager pour qu’ils utilisent le point de mise à jour logicielle pour l’installation du client et les mises à jour logicielles, et pour qu’ils publient le logiciel client sur le point de mise à jour logicielle.  

> [!NOTE]  
>  Si les ordinateurs sont dans un état de redémarrage en attente suite à une précédente installation de logiciel, une installation du client basée sur une mise à jour logicielle peut entraîner le redémarrage de l'ordinateur.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configurez un objet de stratégie de groupe dans les services de domaine Active Directory de manière à spécifier le point de mise à jour logicielle pour l’installation du client et les mises à jour logicielles :  

1.  Utilisez la console de gestion des stratégies de groupe pour ouvrir un objet de stratégie de groupe nouveau ou existant.  

2.  Dans la console, développez **Configuration ordinateur**, **Modèles d’administration**, **Composants Windows**, puis choisissez **Windows Update**.  

3.  Ouvrez les propriétés du paramètre **Spécifier l’emplacement intranet du service de mise à jour Microsoft**, puis choisissez **Activé**.  

4.  Dans la zone **Set the intranet update service for detecting updates** (Définir le service intranet de mise à jour pour la détection des mises à jour), spécifiez le nom et le port du serveur du point de mise à jour logicielle  :  

    -   Si le système de site Configuration Manager est configuré pour utiliser un nom de domaine complet (FQDN), utilisez le format de domaine complet.  

    -   Si le système de site Configuration Manager n’est pas configuré pour utiliser un nom de domaine complet (FQDN), utilisez un format de nom court.  

    > [!NOTE]  
    >  Pour identifier le numéro de port, consultez [Comment déterminer les paramètres de port utilisés par WSUS dans System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

     Exemple : **http://server1.contoso.com:8530**  

5.  Dans la zone **Configurer le serveur intranet de statistiques**, spécifiez le nom du serveur intranet de statistiques. Il ne s’agit pas nécessairement du même que celui du serveur du point de mise à jour logicielle. De même, il n’est pas nécessaire que le format soit identique s’il s’agit du même serveur.  

6.  Attribuez l’objet de stratégie de groupe aux ordinateurs sur lesquels vous souhaitez installer le client et recevoir les mises à jour logicielles.  

### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>Pour publier le client Configuration Manager dans le point de mise à jour logicielle  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** > **Sites**.  

3.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation du client en fonction des mises à jour logicielles.  

4.  Dans l’onglet **Accueil** du groupe **Paramètres**, choisissez **Paramètres d’installation du client**, puis **Installation du client en fonction des mises à jour logicielles**.  

5.  Sélectionnez **Activer l’installation du client basée sur les mises à jour logicielles**.  

6.  Si la version du logiciel client sur le serveur de site Configuration Manager est ultérieure à celle sur le point de mise à jour logicielle, la boîte de dialogue **Version plus récente du package client détectée** s’affiche. Cliquez sur **Oui** pour publier la version la plus récente.  

    > [!NOTE]  
    >  Si le logiciel client n’a pas été publié auparavant sur le point de mise à jour logicielle, cette boîte de dialogue est vide.  

La mise à jour logicielle du client Configuration Manager n’est pas mise à jour automatiquement quand il existe une nouvelle version du client. Si vous mettez à niveau le site, ce qui comprend une nouvelle version du client, vous devez répéter cette procédure et cliquer sur **Oui** à l'étape 6.  

##  <a name="BKMK_ClientGP"></a> Guide pratique pour installer des clients à l’aide d’une stratégie de groupe  
 Vous pouvez utiliser la stratégie de groupe dans les services de domaine Active Directory pour publier ou attribuer le client Configuration Manager en vue de l’installer sur les ordinateurs dans votre entreprise. Le client est installé au démarrage de l’ordinateur. Quand vous utilisez la stratégie de groupe, le client s’affiche dans **Ajout/Suppression de programmes** dans le Panneau de configuration pour permettre à l’utilisateur de procéder à l’installation.  

 Utilisez le package Windows Installer (CCMSetup.msi) pour les installations basées sur la stratégie de groupe. Ce fichier se trouve dans le dossier **&lt;répertoire d’installation de ConfigMgr\>\bin\i386** sur le serveur de site Configuration Manager. Vous ne pouvez pas ajouter des propriétés à ce fichier pour modifier le comportement de l’installation.  

> [!IMPORTANT]  
>  Vous devez disposer d’autorisations d’administrateur pour accéder aux fichiers d’installation du client.  

-   Si le schéma Active Directory est étendu pour Configuration Manager et que l’option **Publier ce site dans les services d’annuaire Active Directory** est sélectionnée sous l’onglet **Avancé** de la boîte de dialogue **Propriétés du site**, les ordinateurs clients demandent automatiquement les propriétés d’installation aux services de domaine Active Directory. Pour plus d’informations sur les propriétés d’installation qui sont publiées, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Si le schéma Active Directory n’a pas été étendu, vous pouvez appliquer la procédure de cette rubrique pour stocker les propriétés d’installation dans le Registre des ordinateurs : [Guide pratique pour fournir les propriétés d’installation du client (installation basée sur une stratégie de groupe et sur les mises à jour logicielles)](#BKMK_Provision). Ces propriétés d’installation sont utilisées quand le client est installé.  

Pour plus d'informations sur l'utilisation de la stratégie de groupe dans les services de domaine Active Directory pour installer des logiciels, consultez la documentation de votre serveur Windows.  

##  <a name="BKMK_Manual"></a> Guide pratique pour installer des clients manuellement  
 Vous pouvez installer manuellement le logiciel client sur les ordinateurs dans votre entreprise à l’aide du programme CCMSetup.exe. Ce programme et ses fichiers de prise en charge se trouvent dans le dossier **Client** du dossier d’installation de Configuration Manager sur le serveur de site et sur les points de gestion dans votre site. Ce dossier est partagé sur le réseau sous  

 \\\\*&lt;nom du serveur de site\>*\SMS_*&lt;code de site\>*\Client\  

 où *&lt;nom du serveur de site\>* est le nom d’un des serveurs hébergeant un point de gestion et *&lt;code de site\>* est le code du site principal auquel le client appartiendra.  Pour exécuter CCMSetup.exe à partir de la ligne de commande sur le client, vous devez mapper un lecteur réseau à cet emplacement, puis exécuter la commande.  

> [!IMPORTANT]  
>  Vous devez disposer d’autorisations d’administrateur pour accéder aux fichiers d’installation du client.  

 Le programme CCMSetup.exe copie toutes les conditions préalables nécessaires sur l’ordinateur client, puis fait appel au package Windows Installer (Client.msi) pour installer le client. Vous ne pouvez pas exécuter Client.msi directement.  

 Vous pouvez spécifier des propriétés de ligne de commande pour CCMSetup.exe et Client.msi afin de modifier le comportement de l'installation du client. Spécifiez les propriétés de CCMSetup (propriétés commençant par **/**) avant de spécifier les propriétés de Client.msi. Exemple :  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  
et le client s’installe en utilisant les propriétés suivantes :  

|Propriété|Description|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Cette propriété de CCMSetup spécifie le point de gestion SMSMP01 pour télécharger les fichiers requis d'installation du client.|  
|**/logon**|Cette propriété de CCMSetup spécifie que l’installation doit s’arrêter si un client Configuration Manager se trouve déjà sur l’ordinateur.|  
|**SMSSITECODE=AUTO**|Cette propriété de Client.msi spécifie que le client doit essayer de trouver le code de site Configuration Manager à utiliser, par exemple, en utilisant les services de domaine Active Directory.|  
|**FSP=SMSFP01**|Cette propriété de Client.msi spécifie que le point d'état de secours appelé SMSFP01 sera utilisé pour recevoir les messages d'état envoyés par l'ordinateur client.|  

 Pour obtenir des détails sur toutes les propriétés de CCMSetup.exe, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="examples"></a>Exemples
 Ces exemples ont trait à des clients Active Directory sur l’intranet, et utilisent les valeurs suivantes pour représenter les différents aspects du site :  

 **MPSERVER** = serveur hébergeant le point de gestion   
**FSPSERVER** = serveur hébergeant le point d’état de secours  
**ABC** = code de site  
**contoso.com** = nom de domaine  

 Tous les serveurs de système de site sont configurés avec un nom de domaine complet intranet, et le site est publié dans la forêt Active Directory du client.  

 Sur l’ordinateur client, connectez-vous en tant qu’administrateur local, mappez un lecteur (z:) à \\\MPSERVER\SMS_ABC\Client, indiquez le lecteur z à l’invite de commandes, puis exécutez l’une des commandes suivantes.  

 **Exemple 1 :**  

```  
CCMSetup.exe  
```  
Cet exemple installe le client sans propriété supplémentaire, si bien que le client est configuré automatiquement avec les propriétés d’installation du client publiées sur les services de domaine Active Directory. Par exemple, le client est configuré automatiquement pour le code de site (l’emplacement réseau du client doit être inclus dans un groupe de limites configuré pour l’attribution du client), un point de gestion, le point d’état de secours et, éventuellement, pour communiquer uniquement avec le protocole HTTPS. Pour plus d’informations sur les propriétés d’installation du client qui peuvent être configurées automatiquement pour les clients Active Directory, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Exemple 2 :**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  
Dans cet exemple, aucune configuration automatique n’est effectuée par les services de domaine Active Directory, et l’emplacement réseau du client n’a pas besoin d’être inclus dans un groupe de limites configuré pour l’attribution du client. En effet, l'installation spécifie le site, un point de gestion intranet et Internet, un point d'état de secours qui accepte les connexions en provenance d'Internet, ainsi que l'utilisation d'un certificat PKI client (s'il en existe un) ayant la période de validité la plus longue.  

##  <a name="BKMK_ClientLogonScript"></a> Guide pratique pour installer des clients à l’aide de scripts d’ouverture de session  
 Configuration Manager prend en charge les scripts d’ouverture de session pour installer le logiciel client Configuration Manager. Vous pouvez utiliser le fichier programme **CCMSetup.exe** dans un script de connexion pour déclencher l'installation du client.  

 L'installation via un script d'ouverture de session utilise les mêmes méthodes que l'installation manuelle du client. Vous pouvez spécifier la propriété d'installation **/logon** pour CCMSsetup.exe, ce qui empêche l'installation du client s'il existe déjà une version du client sur l'ordinateur. Cette propriété empêche la réinstallation du client à chaque exécution du script d'ouverture de session.  

 Si aucune source d’installation utilisant la propriété **/Source** n’est spécifiée, et si aucun point de gestion à partir duquel obtenir l’installation n’est spécifié à l’aide de la propriété **/MP**, le programme CCMSetup.exe peut localiser le point de gestion en utilisant les services de domaine Active Directory si le schéma a été étendu pour Configuration Manager, et le site est publié dans les services de domaine Active Directory. Alternativement, le client peut utiliser le service de nom de domaine (DNS) ou WINS pour rechercher un point de gestion.  

##  <a name="BKMK_ClientApp"></a> Guide pratique pour installer des clients à l’aide d’un package et d’un programme  
 Vous pouvez utiliser Configuration Manager pour créer et déployer un package et un programme qui mettent à niveau le logiciel client sur les ordinateurs sélectionnés dans votre hiérarchie. Un fichier de définition de package pour renseigner les propriétés du package avec les valeurs généralement utilisées est fourni avec Configuration Manager. Vous pouvez personnaliser le comportement de l'installation du client en spécifiant des propriétés de ligne de commande supplémentaires.  

> [!NOTE]  
>  Vous ne pouvez pas mettre à niveau des clients Configuration Manager 2007 avec cette méthode. Au lieu de cela, utilisez la mise à niveau automatique des clients, qui crée et déploie automatiquement un package contenant la dernière version du client. Pour plus d’informations, consultez [Mettre à niveau les clients dans System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Pour plus d’informations sur la migration à partir de versions précédentes du client Configuration Manager, consultez [Planification d’une stratégie de migration de clients dans System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md).  

 
###<a name="to-create-a-package-and-program-for-the-client-software"></a>Pour créer un package et un programme pour le logiciel client  

Pour créer un package et un programme Configuration Manager que vous pouvez déployer sur les ordinateurs clients Configuration Manager afin de mettre à niveau le logiciel client, utilisez la procédure suivante.  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un package à partir de la définition**.  

4.  Dans la page **Définition du package** de l’Assistant, sélectionnez **Microsoft** dans la liste déroulante **Éditeur** et **Mise à niveau du client Configuration Manager** dans la liste **Définition du package**.  

5.  Dans la page **Fichiers sources**, sélectionnez **Toujours obtenir les fichiers depuis le dossier source**.  

6.  Dans la page **Dossier source**, sélectionnez **Chemin d’accès réseau (nom UNC)**, puis entrez le chemin d’accès réseau à l’ordinateur et au dossier contenant les fichiers d’installation du client.  

    > [!NOTE]  
    >  L’ordinateur sur lequel le déploiement de Configuration Manager est effectué doit avoir accès au dossier réseau spécifié. Dans le cas contraire, l’installation échoue.  

    Si vous souhaitez changer l'une des propriétés d'installation du client, vous pouvez modifier les paramètres de la ligne de commande CCMSetup.exe dans l'onglet **Général** de la boîte de dialogue du programme **Propriétés des mises à niveau silencieuses de l'Agent Configuration Manager** . Les propriétés d'installation par défaut sont **/noservice SMSSITECODE=AUTO**.  

9. Distribuez le package à tous les points de distribution qui doivent héberger le package de mise à niveau des clients. Vous pouvez ensuite déployer le package sur des regroupements d’ordinateurs contenant les clients à mettre à niveau.  

## <a name="how-to-install-clients-to-intune-mdm-managed-windows-devices"></a>Guide pratique pour installer des clients sur des appareils Windows gérés par la gestion MDM d’Intune

Vous pouvez déployer les fichiers d’installation du client sur les ordinateurs qui sont inscrits dans Microsoft Intune. 

Pour que l’appareil reste dans un état géré une fois le logiciel client installé, il doit se trouver dans le réseau d’entreprise et dans une limite de site Configuration Manager. 

> [!NOTE]
> Une fois le logiciel client installé, l’appareil est désinscrit d’Intune.

### <a name="to-install-clients-with-intune"></a>Pour installer des clients avec Intune :

1. Dans Intune, [créez une application](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) contenant le fichier d’installation du client Configuration Manager **ccmsetup.msi**.

2. Dans l’Éditeur de logiciel Intune, utilisez les paramètres de ligne de commande suivants :

  **CCMSETUPCMD="/MP:&lt;Nom de domaine complet du point de gestion> SMSMP=&lt;Nom de domaine complet du point de gestion> SMSSITECODE=&lt;Votre code de site> DNSSUFFIX=&lt;Suffixe DNS du point de gestion>"**

3. [Déployez l’application](/intune/deploy-use/deploy-apps-in-microsoft-intune) sur les ordinateurs Windows inscrits.

##  <a name="BKMK_ClientImage"></a> Guide pratique pour installer des clients à l’aide d’une image de l’ordinateur  
Vous pouvez préinstaller le logiciel client Configuration Manager sur un ordinateur d’image maître qui vous permettra de copier d’autres ordinateurs.   

### <a name="to-prepare-the-client-computer-for-imaging"></a>Pour préparer l'ordinateur client à la mise en image  

1.  Installez manuellement le logiciel client Configuration Manager sur l’ordinateur d’image maître. Pour plus d'informations, voir [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Ne spécifiez aucun code de site Configuration Manager pour le client dans les propriétés de la ligne de commande CCMSetup.exe.  

2.  Entrez **net stop ccmexec** dans l'invite de commande pour vérifier que le service **Hôte de l'agent SMS** (Ccmexec.exe) ne s'exécute pas sur l'ordinateur d'image maître.  

3.  Supprimez tous les certificats enregistrés dans le magasin local sur l'ordinateur d'image maître.  Par exemple, si vous utilisez des certificats d'infrastructure à clé publique (PKI), vous devez supprimer les certificats dans le magasin **Personnel** de l' **Ordinateur** et de l' **Utilisateur** avant de mettre l'ordinateur en image.

4.  Si les clients sont installés dans une hiérarchie Configuration Manager différente de celle de l’ordinateur d’image maître, supprimez la clé racine approuvée de cet ordinateur.  
    > [!NOTE]  
    >  Si les clients ne peuvent pas demander aux services de domaine Active Directory de localiser un point de gestion, ils peuvent utiliser une clé racine approuvée pour déterminer les points de gestion approuvés. Si tous les clients mis en image sont déployés sur la même hiérarchie que celle de l'ordinateur maître, conservez la clé racine approuvée. Si les clients vont être déployés dans différentes hiérarchies, supprimez la clé racine approuvée, et il est recommandé de préparer la mise en service de la nouvelle clé racine approuvée sur les clients. Pour plus d’informations, consultez  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Utilisez votre logiciel d'acquisition d'images pour capturer l'image de l'ordinateur maître.  

6.  Déployez l'image vers les ordinateurs de destination.  

##  <a name="BKMK_ClientWorkgroup"></a> Guide pratique pour installer des clients sur les ordinateurs d’un groupe de travail  
 Configuration Manager prend en charge l’installation du client sur des ordinateurs de groupe de travail. Installez le client sur les ordinateurs du groupe de travail à l'aide de la méthode spécifiée dans [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual).  

 Conditions préalables :  

-   Le client doit être installé manuellement sur chaque ordinateur du groupe de travail. Durant l’installation, l’utilisateur connecté doit disposer des droits d’administrateur local.  

-   Pour accéder aux ressources du domaine du serveur de site Configuration Manager, le compte d’accès réseau doit être configuré pour le site. Spécifiez ce compte comme une propriété du composant de distribution de logiciels. Pour plus d'informations, voir [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitations :  

-   Les clients du groupe de travail ne peuvent pas localiser les points de gestion depuis les services de domaine Active Directory et doivent à la place utiliser DNS, WINS ou un autre point de gestion.  

-   L'itinérance globale n'est pas prise en charge parce que les clients ne peuvent pas demander d'information de site aux services de domaine Active Directory.  

-   Les méthodes de découverte d'Active Directory ne découvriront pas les ordinateurs dans des groupes de travail.  

-   Vous ne pouvez pas déployer de logiciels vers les utilisateurs d'ordinateurs de groupe de travail.  

-   Vous ne pouvez pas utiliser la méthode d'installation poussée du client pour installer le client sur des ordinateurs du groupe de travail.  

-   Les clients du groupe de travail ne peuvent pas utiliser Kerberos pour l’authentification et peuvent donc nécessiter une approbation manuelle.  

-   Un client de groupe de travail ne peut pas être configuré comme point de distribution. Configuration Manager impose que les ordinateurs faisant office de points de distribution soient membres d’un domaine.  

### <a name="to-install-the-client-on-workgroup-computers"></a>Pour installer le client sur des ordinateurs d'un groupe de travail  

Vérifiez les conditions préalables et suivez les instructions de la section [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual).  

   Dans cet exemple, le client est installé pour être géré sur l’intranet, tandis que le code de site et le suffixe DNS sont spécifiés pour localiser un point de gestion : `**CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**`  

     

   Dans cet exemple, le client doit se trouver à un emplacement réseau configuré dans un groupe de limites pour que l'attribution de site automatique aboutisse. La commande inclut un point d’état de secours sur le serveur FSPSERVER pour faciliter le suivi du déploiement du client et identifier les problèmes de communication du client : `**CCMSetup.exe FSP=fspserver.constoso.com**`  

      

##  <a name="BKMK_ClientInternet"></a> Guide pratique pour installer des clients pour la gestion des clients sur Internet  
 Si le site Configuration Manager prend en charge la gestion du client basée sur Internet pour des clients pouvant être sur l’intranet ou sur Internet, deux options s’offrent à vous au moment d’installer les clients sur l’intranet :  

-   Vous pouvez inclure la propriété de Client.msi CCMHOSTNAME=*&lt;nom_domaine_complet_internet_du_point_de_gestion_internet\>* quand vous installez le client, par exemple avec la méthode d’installation manuelle ou push du client. Lorsque vous utilisez cette méthode, vous devez également attribuer directement le client au site et vous ne pouvez pas utiliser l'attribution de site automatique. La section [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual) de cette rubrique fournit un exemple de cette méthode de configuration.  

-   Vous pouvez installer le client dans l’optique d’une gestion du client sur l’intranet, puis attribuer au client un point de gestion du client basé sur Internet en définissant les propriétés du client Configuration Manager dans le Panneau de configuration ou en utilisant un script. Lorsque vous utilisez cette méthode, vous pouvez utiliser l'attribution automatique des clients. Pour plus d'informations, voir la section [Comment configurer les clients en vue de les gérer via Internet après leur installation](#BKMK_ConfigureIBCM_MP) de cette rubrique.  

 Si vous devez installer des clients sur Internet parce qu'ils basés uniquement sur Internet ou que vous devez les installer avant de les rapatrier sur l'intranet, optez pour l'une des méthodes prises en charge suivantes :  

-   Définissez pour ces clients un mécanisme leur permettant de se connecter temporairement à l’intranet avec un réseau privé virtuel (VPN), puis installez-les en utilisant la méthode d’installation du client appropriée.  

-   Utilisez une méthode d’installation indépendante de Configuration Manager. Par exemple, créez un package des fichiers sources d’installation du client sur un média amovible, que vous pouvez ensuite envoyer aux utilisateurs avec des instructions d’installation. Les fichiers sources d’installation du client se trouvent dans le dossier *&lt;chemin_installation\>*\Client sur le serveur de site et les points de gestion Configuration Manager. Incorporez au support un script à copier manuellement vers le dossier du client et depuis ce dossier, installez le client à l'aide de CCMSetup.exe et de toutes les propriétés de ligne commande CCMSetup appropriées.  

> [!NOTE]  
>  Configuration Manager ne prend pas en charge l’installation directe d’un client depuis le point de gestion Internet ou le point de mise à jour logicielle Internet.  

 Étant donné que les clients gérés via Internet doivent communiquer avec leurs systèmes de site Internet, vérifiez que des certificats pour infrastructure à clé publique (PKI) sont également installés sur ces clients avant d'installer ces derniers. Vous devez installer ces certificats indépendamment de Configuration Manager. Pour plus d’informations sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Pour installer des clients sur Internet en spécifiant des propriétés de ligne de commande CCMSetup  

1.  Suivez les instructions de la section [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual) et incluez toujours les éléments suivants :  

    -   Propriété de ligne de commande CCMSetup **/source:***&lt;chemin_local_du_dossier_Client_copié\>*  

    -   Propriété de ligne de commande CCMSetup **/UsePKICert:**  

    -   Propriété Client.msi **CCMHOSTNAME=***&lt;nom_de_domaine_complet_du_point_de_gestion_internet\>*  

    -   Propriété Client.msi **SMSSIGNCERT=***&lt;chemin_local_du_certificat_de_signature_du_serveur_de_site_exporté\>*  

    -   Propriété Client.msi **SMSSITECODE=***&lt;code_de_site_du_point_de_gestion_internet\>*  

    > [!NOTE]  
    >  Si le site comporte plusieurs points de gestion basés sur Internet, le choix du point de gestion basé sur Internet importe peu pour la propriété CCMHOSTNAME. Quand un client Configuration Manager se connecte au point de gestion basé sur Internet spécifié, le point de gestion envoie au client une liste des points de gestion basés sur Internet disponibles du site, puis le client en sélectionne un au hasard.  

2.  Si vous ne souhaitez pas que le client vérifie la liste de révocation de certificats (CRL), spécifiez la propriété de ligne de commande CCMSetup **/NoCRLCheck**.  

3.  Si vous utilisez un point d’état de secours basé sur Internet, spécifiez la propriété Client.msi **FSP=***&lt;nom_de_domaine_complet_internet_du_point_d’état_de_secours_basé_sur_internet\>*.  

4.  Si vous installez le client pour la gestion des clients Internet uniquement, spécifiez la propriété Client.msi **CCMALWAYSINF=1**.  

5.  Vérifiez si vous devez spécifier des propriétés de ligne de commande CCMSetup supplémentaires. Par exemple, vous pouvez avoir besoin de spécifier un critère de sélection de certificat si le client possède plusieurs certificats d’infrastructure à clé publique (PKI) valides. Pour obtenir la liste des propriétés disponibles, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

   Exemple : `**CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**`  

   Dans cet exemple, les fichiers sources du client sont installés à partir d'un dossier du lecteur D avec les paramètres suivants : utilisation d'un certificat PKI client et sélection du certificat ayant la plus longue période de validité pour la gestion des clients sur Internet uniquement, attribution du client au point de gestion Internet nommé SERVER1 et au point d'état de secours Internet du domaine contoso.com, et attribution du client au site ABC.  

###  <a name="BKMK_ConfigureIBCM_MP"></a>Pour configurer des clients en vue de leur gestion sur Internet après l’installation  
 Pour attribuer le point de gestion Internet après avoir installé le client, utilisez l'une des procédures suivantes. La première procédure reposant sur une configuration manuelle, elle est adaptée à un nombre de clients limité. En revanche, si vous avez un grand nombre de clients à configurer, la deuxième procédure est plus appropriée.  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Pour configurer les clients en vue de les gérer via Internet après leur installation en leur attribuant le point de gestion Internet dans les propriétés Configuration Manager  

1.  Accédez à **Configuration Manager** dans le Panneau de configuration de l'ordinateur client, puis double-cliquez dessus pour ouvrir ses propriétés.  

2.  Sous l'onglet **Internet** , entrez le nom de domaine complet du point de gestion Internet dans la zone de texte FQDN Internet.  

    > [!NOTE]  
    >  L'onglet **Internet** est disponible uniquement si le client dispose d'un certificat PKI client.  

3.  Entrez les paramètres de serveur proxy si le client doit accéder à Internet en utilisant un serveur proxy.  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Pour configurer les clients en vue de les gérer via Internet après leur installation au moyen d'un script  

1.  Ouvrez un éditeur de texte, tel que le Bloc-notes.  

2.  Copiez et insérez le code suivant dans le fichier. Remplacez *mp.contoso.com* par le nom de domaine complet Internet de votre point de gestion Internet.  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set newInternetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Si vous devez supprimer un point de gestion Internet spécifié pour éviter que le client utilise un point de gestion Internet, supprimez la valeur entre guillemets de sorte que cette ligne se présente ainsi : **newInternetBasedManagementPointFQDN = ""**.  

4.  Enregistrez le fichier avec une extension .vbs.  

5.  Utilisez cscript pour exécuter le script sur les ordinateurs clients en utilisant l'une des méthodes suivantes :  

    -   Déployez le fichier sur les clients Configuration Manager existants en utilisant un package et un programme.  

    -   Exécutez le fichier localement sur les clients Configuration Manager existants en double-cliquant sur le fichier de script dans l'Explorateur Windows.  

 Vous devrez peut-être redémarrer le client pour que les modifications prennent effet.  

##  <a name="BKMK_Provision"></a> Guide pratique pour fournir les propriétés d’installation du client (installation basée sur une stratégie de groupe et sur les mises à jour logicielles)  
 Vous pouvez utiliser la stratégie de groupe Windows pour fournir les propriétés d’installation du client Configuration Manager aux ordinateurs. Ces propriétés sont stockées dans le Registre de l’ordinateur et lues quand le logiciel client est installé. Cette procédure n’est généralement pas nécessaire, mais peut s’avérer indispensable dans certains scénarios d’installation du client, par exemple :  

-   Vous utilisez la méthode d’installation du client à l’aide des paramètres de la stratégie de groupe ou celle basée sur les mises à jour logicielles, mais vous n’avez pas étendu le schéma Active Directory pour Configuration Manager.  

-   Vous souhaitez redéfinir les propriétés de l'installation du client sur certains ordinateurs.  

> [!NOTE]  
>  Si les propriétés d'installation sont fournies sur la ligne de commande CCMSetup.exe, les propriétés d'installation fournies aux ordinateurs ne seront pas utilisées.  

 Le modèle d’administration Stratégie de groupe nommé ConfigMgrInstallation.adm, qui se trouve sur le média d’installation de Configuration Manager, peut être utilisé pour fournir les propriétés d’installation aux ordinateurs clients.   

### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Pour configurer et attribuer des propriétés d'installation du client à l'aide d'un objet de stratégie de groupe  

1.  Importez le modèle administratif ConfigMgrInstallation.adm dans un objet de stratégie de groupe nouveau ou existant, à l'aide d'un éditeur comme l'Éditeur d'objets de stratégie de groupe Windows. Le fichier se trouve dans le dossier **TOOLS\ConfigMgrADMTemplates** du média d’installation de Configuration Manager.  

2.  Affichez les propriétés du paramètre importé **Configurer les paramètres de déploiement du client**.  

3.  Choisissez **Activé**.  

4.  Dans la zone **CCMSetup** , entrez les propriétés de ligne de commande CCMSetup requises. Pour afficher la liste de toutes les propriétés de ligne de commande CCMSetup et des exemples de leur utilisation, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Attribuez l’objet stratégie de groupe aux ordinateurs auxquels vous souhaitez fournir les propriétés d’installation du client Configuration Manager.  

 Pour plus d'informations sur la stratégie de groupe Windows, voir la documentation de Windows Server.  

### <a name="see-also"></a>Voir aussi
[Méthodes d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md)
